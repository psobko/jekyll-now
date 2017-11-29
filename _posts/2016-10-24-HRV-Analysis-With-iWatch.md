---
layout: post
title: HRV Analysis with iWatch?
---


Getting precise RR intervals requires a resolution which is much smaller than a duration of RR intervals (1/100s or 100Hz). ECG machines are able to get precise measurements like this, but the pulse width when using pulse oximeters is often much more than 100ms. This is because the PPG sensors on the iWatch measure blood flow in distant capillaries vs measuring electrical ECG pulses from the heart, leaving the shape of the pulse to be stretched in time. Analyzing HRV usually requires measurements with a resolution between 40-100Hz.

With the watchOS3 the best resolution we can get is 5s/0.2Hz, while we don't know exactly what the sampling rate is of the PPG sensors on the watch I'm betting that heart rate is determined as a moving average over a period of several beats (probably to filter out the inaccuracy of the R peak position estimations it's making). Apple [tell's us](https://support.apple.com/en-us/HT204666) that the sensor will adjust the sampling rate to compensate for low signal levels. This kind of filtering cancels out high frequency high frequency heart rate variations, decreasing RR interval resolution even more.

I wonder if the low resolution on the watch is a limitation of the sensor hardware itself, or if Apple just doesn't want to allocate so many resources to sensor? Without access to raw sensor data it's hard to estimate it's accuracy.