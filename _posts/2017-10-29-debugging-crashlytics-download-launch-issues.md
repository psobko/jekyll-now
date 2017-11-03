Sometimes with Crashlytics beta you can run into scenarios where the application will either close immediately upon launch, or won't even install and alerts the user:

> "Unable to Download App
> _______ could not be installed at this time"

Most of the time time this is a profile issue, though there are some very specific errors which can occur either in the code or on the test device.

## For Developers
To start check to make sure it's not caused by the usual offenders:

* Building the app with the wrong provisioning profile or a profile which was revoked
* Entitlements which don't match the profile (`YourAppName.entitlements` in Xcode)
* Cached profiles in Xcode which haven't updated

Ideally provisioning profiles should be freshly downloaded followed by a project clean as part of your build process to avoid these types of issues.


### Debugging
If nothing appears to be wrong you can check the device logs when installing (assuming you have access to the device or it's logs), look for any errors coming from the `installd` process.

To check the profile of the build you can open terminal and run the following command with the path to the .mobileprovision file of the build:

`security cms -D -i /path/to/TestApp.app/embedded.mobileprovision`

To find the .app file you'll need access to the iOS App File (`*.ipa`) or the Xcode Archive. Download either if you store build ouput as part of your build process, if the project was archived on a local machine you can find the archive in: `~/Library/Developer/Xcode/Archives/<date archived>/` or by using Xcode's organizer and right-clicking the build in question.

Opening a local archive will look something like:

`$ security cms -D -i ~/Library/Developer/Xcode/Archives/<date archived>/<app name and date>.xcarchive>/Products/Aplications/<app name>.app/embedded.mobileprovision`

To open an `ipa` you'll need to `unzip` it (or you can just give it the `.zip` extension to open it in Finder). Inside you should find `/Payload/<app name>.app/embedded.mobileprovision`.

The command should look like this:
`unzip -p <ipa file>.ipa Payload/<app name>.app/embedded.mobileprovision | security cms -D`

The output you get will look something like this:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>AppIDName</key>
	<string>[THE NAME OF THE APPLICATION]</string>
	<key>ApplicationIdentifierPrefix</key>
	<array>
	<string>[TEAM IDENTIFIER]</string>
	</array>
	<key>CreationDate</key>
	<date>2017-10-24T15:21:18Z</date>
	<key>Platform</key>
	<array>
		<string>iOS</string>
	</array>
	<key>DeveloperCertificates</key>
	<array>
		<data>[CERTIFICIATE DATA]</data>
	</array>
	<key>Entitlements</key>
	<dict>
		<key>keychain-access-groups</key>
		<array>
			<string>[TEAM IDENTIFIER].*</string>
		</array>
		<key>get-task-allow</key>
		<true/>
		<key>application-identifier</key>
		<string>[APP IDENTIFIER]</string>
		<key>com.apple.developer.team-identifier</key>
		<string>[TEAM IDENTIFIER]</string>
		[OTHER ENTITLEMENTS AARE LISTED HERE]
	</dict>
	<key>ExpirationDate</key>
	<date>2018-10-24T15:21:18Z</date>
	<key>Name</key>
	<string>[NAME OF PROVISIONIN PROFILE]</string>
	<key>ProvisionedDevices</key>
	<array>
		<string>[DEVICE UDID]</string>
		<string>[DEVICE UDID]</string>
		[MORE UDIDs...]
	</array>
	<key>TeamIdentifier</key>
	<array>
		<string>[TEAM IDENTIFIER]</string>
	</array>
	<key>TeamName</key>
	<string>[TEAM NAME]</string>
	<key>TimeToLive</key>
	<integer>365</integer>
	<key>UUID</key>
	<string>[UUDID]</string>
	<key>Version</key>
	<integer>1</integer>
</dict>
```
These two tools give you enough to quickly identify the issue.


## For Testers

It's always a good idea to deploy to a test device first before sending the build notification, just to make sure everything is running smoothly. If everything seems fine but there are still issues on a test device you can try a few things:

* Delete any copies of the existing app and **restart the device**
* Make sure Crashlytics profile is installed on the device
* If it is installed delete it and download it again by tapping on the "install" button in the Crashlytics email

Here are the steps for checking/deleting a profile:

![_config.yml]({{ site.baseurl }}/images/removing-profile-step-1.png) 
![_config.yml]({{ site.baseurl }}/images/removing-profile-step-2.png) 
![_config.yml]({{ site.baseurl }}/images/removing-profile-step-3.png) 
![_config.yml]({{ site.baseurl }}/images/removing-profile-step-4.png) 

