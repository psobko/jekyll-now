---
layout: post
title: Testing HealthKit Type Identifiers
---

So I wanted to see what kind of HealthKit data types I could read which were measured from the iWatch. I tried reading every possible data type in `HKTypeIdentifiers`:

```objective-c
 [NSSet setWithObjects:
 //Body Measurements
[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierBodyMassIndex         ],     // Scalar(Count),               Discrete
[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierBodyFatPercentage     ],     // Scalar(Percent, 0.0 - 1.0),  Discrete
[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierHeight                ],     // Length,                      Discrete
[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierBodyMass              ],     // Mass,                        Discrete
[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierLeanBodyMass          ],     // Mass,                        Discrete

// Fitness
[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierStepCount             ],      // Scalar(Count),               Cumulative
[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierDistanceWalkingRunning],      // Length,                      Cumulative
[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierDistanceCycling       ],      // Length,                      Cumulative
[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierDistanceWheelchair    ],      // Length,                      Cumulative
[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierBasalEnergyBurned     ],      // Energy,                      Cumulative
[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierActiveEnergyBurned    ],      // Energy,                      Cumulative
[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierFlightsClimbed        ],      // Scalar(Count),               Cumulative
//[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierNikeFuel              ],    // Scalar(Count),               Cumulative
//[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierAppleExerciseTime     ],    // Time                         Cumulative
[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierPushCount             ],      // Scalar(Count),               Cumulative

// Vitals
[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierHeartRate             ],      // Scalar(Count)/Time,          Discrete
[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierBodyTemperature       ],      // Temperature,                 Discrete
[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierBasalBodyTemperature  ],      // Basal Body Temperature,      Discrete
[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierBloodPressureSystolic ],      // Pressure,                    Discrete
[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierBloodPressureDiastolic],      // Pressure,                    Discrete
[HKQuantityType quantityTypeForIdentifier:HKQuantityTypeIdentifierRespiratoryRate       ],      // Scalar(Count)/Time,          Discrete

];
```

Not all of the data types returned results, but here's what I was able to pull out:

```
Reading results for HKQuantityTypeIdentifierDistanceCycling:
0 results for HKQuantityTypeIdentifierDistanceCycling

Reading results for HKQuantityTypeIdentifierDistanceWheelchair:
0 results for HKQuantityTypeIdentifierDistanceWheelchair

Reading results for HKQuantityTypeIdentifierBloodPressureDiastolic:
0 results for HKQuantityTypeIdentifierBloodPressureDiastolic

Reading results for HKQuantityTypeIdentifierDistanceWalkingRunning:
    "162.02 m C33FC4D5-48AA-419A-A75D-FC31009A83B5 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-03 23:55:41 -0400 - 2016-07-04 00:05:40 -0400)",
    "81.68 m AFD4C4B5-9B2C-4AAC-980D-454BBC4989C5 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:05:40 -0400 - 2016-07-04 00:15:39 -0400)",
    "84.93 m DE3CC77A-DDF2-4517-B31E-F913278E724A \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:15:39 -0400 - 2016-07-04 00:22:44 -0400)",
    "61.53 m B1C6776F-8750-4AB0-A6F2-B1BF939DA7F9 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:32:43 -0400 - 2016-07-04 00:40:09 -0400)",
    "20.54 m 949D2734-1669-483C-AE92-28C565FB640E \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:40:09 -0400 - 2016-07-04 00:43:47 -0400)",
    "9.68 m 4794797B-D16E-4A8E-A122-EBF41A620E39 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:43:47 -0400 - 2016-07-04 00:52:52 -0400)",
    "14.37 m 7950541F-2080-46F5


Reading results for HKQuantityTypeIdentifierBasalEnergyBurned:
    "20.888 kcal 16C499A4-789A-459E-AAAC-865138B05FCD \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-03 23:57:54 -0400 - 2016-07-04 00:12:55 -0400)",
    "20.058 kcal 977F1EA6-45F2-442E-AFB3-BF8436ABF486 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:12:55 -0400 - 2016-07-04 00:27:57 -0400)",
    "20.335 kcal 6E75BFBE-A9D3-465E-A592-085BAB7AA9B4 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:27:57 -0400 - 2016-07-04 00:42:58 -0400)",
    "18.179 kcal FAA4DF9F-A1B4-4E69-A7BE-978E3FCB4ECF \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:42:58 -0400 - 2016-07-04 00:57:59 -0400)",
    "19.176 kcal 11E1D510-3C06-4711-A552-D09F9772DAF1 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:57:59 -0400 - 2016-07-04 01:13:01 -0400)",
    "18.689 kcal B9CCB30C-9B83-453B-9B3A-AA7911E51E77 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 01:13:01 -0400 - 2016-07-04 01:28:03 -0400)",

Reading results for HKQuantityTypeIdentifierBasalBodyTemperature:
0 results for HKQuantityTypeIdentifierBasalBodyTemperature

Reading results for HKQuantityTypeIdentifierPushCount:
0 results for HKQuantityTypeIdentifierPushCount

Reading results for HKQuantityTypeIdentifierStepCount:
    "210 count 8F82708F-F446-443A-91B9-865E5C7D4A76 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-03 23:55:41 -0400 - 2016-07-04 00:05:40 -0400)",
    "123 count 79549B09-B0CB-4862-9366-EE529C8F07C1 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:05:40 -0400 - 2016-07-04 00:15:39 -0400)",
    "113 count 39650D20-162D-4401-914A-99ED1A3D9BF7 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:15:39 -0400 - 2016-07-04 00:22:44 -0400)",
    "82 count FB8B70DD-C691-4FD0-9F90-4580BD6A4F64 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:32:43 -0400 - 2016-07-04 00:40:09 -0400)",
    "27 count 3A141A33-6C5E-4A8F-9669-058C0CB433BC \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:40:09 -0400 - 2016-07-04 00:43:47 -0400)",
    "18 count 8C2D1865-82A4-4919-9F90-63B9BE44F191 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:43:47 -0400 - 2016-07-04 00:52:52 -0400)",
    
Reading results for HKQuantityTypeIdentifierFlightsClimbed:
    "1 count 42F7371D-54D5-4709-AC68-9DF79ECB2A4D \"Peter's iPhone\" (10.0) \"iPhone\"  (2016-07-04 17:24:06 -0400 - 2016-07-04 17:24:06 -0400)",
    "1 count 701F1B22-8694-4FF2-ADE6-DD4CFE8E0CCB \"Peter's iPhone\" (10.0) \"iPhone\"  (2016-07-04 17:26:36 -0400 - 2016-07-04 17:26:36 -0400)",
    "1 count 5B66EFFD-5240-411D-A48F-AA2E733B74E6 \"Peter's iPhone\" (10.0) \"iPhone\"  (2016-07-04 17:29:02 -0400 - 2016-07-04 17:29:02 -0400)",
    "1 count 690179A6-4B7F-4756-8E3C-8953E38DADE7 \"Peter's iPhone\" (10.0) \"iPhone\"  (2016-07-04 18:45:15 -0400 - 2016-07-04 18:45:15 -0400)"
÷ 	
Reading results for HKQuantityTypeIdentifierBodyTemperature:
0 results for HKQuantityTypeIdentifierBodyTemperature

Reading results for HKQuantityTypeIdentifierBloodPressureSystolic:
0 results for HKQuantityTypeIdentifierBloodPressureSystolic

Reading results for HKQuantityTypeIdentifierBloodPressureSystolic:
0 results for HKQuantityTypeIdentifierBloodPressureSystolic

Reading results for HKQuantityTypeIdentifierHeartRate:
    "1.31667 count/s E096E079-4BEF-4D88-B380-0E4037B1BB1D \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:03:11 -0400 - 2016-07-04 00:03:11 -0400)",
    "1.1 count/s F5E46916-0E24-47C3-BBA7-8FC695B8D4A6 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:10:57 -0400 - 2016-07-04 00:10:57 -0400)",
    "1.21667 count/s D4AEC739-EF97-4B55-A3B2-4B227217B69D \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:17:37 -0400 - 2016-07-04 00:17:37 -0400)",
    "1.38333 count/s 17725BB4-EC7B-4C03-B2EB-F6577748DFE4 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:18:10 -0400 - 2016-07-04 00:18:10 -0400)",
    "1.68333 count/s 29F36E7E-357E-40DA-80C4-6173B67BED51 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:25:15 -0400 - 2016-07-04 00:25:15 -0400)",
    "1.33333 count/s 03BC7704-8F7D-4A1B-ADB8-2BDE07501D5C \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:29:34 -0400 - 2016-07-04 00:29


Reading results for HKQuantityTypeIdentifierDistanceWheelchair:
0 results for HKQuantityTypeIdentifierDistanceWheelchair

Reading results for HKQuantityTypeIdentifierStepCount:
    "210 count 8F82708F-F446-443A-91B9-865E5C7D4A76 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-03 23:55:41 -0400 - 2016-07-04 00:05:40 -0400)",
    "123 count 79549B09-B0CB-4862-9366-EE529C8F07C1 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:05:40 -0400 - 2016-07-04 00:15:39 -0400)",
    "113 count 39650D20-162D-4401-914A-99ED1A3D9BF7 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:15:39 -0400 - 2016-07-04 00:22:44 -0400)",
    "82 count FB8B70DD-C691-4FD0-9F90-4580BD6A4F64 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:32:43 -0400 - 2016-07-04 00:40:09 -0400)",
    "27 count 3A141A33-6C5E-4A8F-9669-058C0CB433BC \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:40:09 -0400 - 2016-07-04 00:43:47 -0400)",
    "18 count 8C2D1865-82A4-4919-9F90-63B9BE44F191 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:43:47 -0400 - 2016-07-04 00:52:52 -0400)",
    
Reading results for HKQuantityTypeIdentifierActiveEnergyBurned:
    "1.645 kcal B50A39CF-3CE3-46DF-A5B8-1C7B31605A8A \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-03 23:59:16 -0400 - 2016-07-04 00:00:17 -0400)",
    "0.037 kcal 140CFA8F-AC84-490C-AC09-B145DEC4494A \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:01:08 -0400 - 2016-07-04 00:02:00 -0400)",
    "0.229 kcal 5CA6DD86-1583-49DF-AFB2-FCFD8AEC79CE \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:02:00 -0400 - 2016-07-04 00:03:01 -0400)",
    "0.176 kcal F032C943-AA95-4F6C-A723-7F49F142F4E6 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:03:01 -0400 - 2016-07-04 00:04:02 -0400)",
    "0.458 kcal 0A6D2A5C-EA62-4EA6-8699-74CE3D622C10 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:04:02 -0400 - 2016-07-04 00:05:04 -0400)",
    "0.478 kcal 7667F45C-ED44-4AFF-BB7F-5634FDD16720 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:05:04 -0400 - 2016-07-04 00:06:05 -0400)",

Reading results for HKQuantityTypeIdentifierRespiratoryRate:
0 results for HKQuantityTypeIdentifierRespiratoryRate

Reading results for HKQuantityTypeIdentifierBasalEnergyBurned:
    "20.888 kcal 16C499A4-789A-459E-AAAC-865138B05FCD \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-03 23:57:54 -0400 - 2016-07-04 00:12:55 -0400)",
    "20.058 kcal 977F1EA6-45F2-442E-AFB3-BF8436ABF486 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:12:55 -0400 - 2016-07-04 00:27:57 -0400)",
    "20.335 kcal 6E75BFBE-A9D3-465E-A592-085BAB7AA9B4 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:27:57 -0400 - 2016-07-04 00:42:58 -0400)",
    "18.179 kcal FAA4DF9F-A1B4-4E69-A7BE-978E3FCB4ECF \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:42:58 -0400 - 2016-07-04 00:57:59 -0400)",
    "19.176 kcal 11E1D510-3C06-4711-A552-D09F9772DAF1 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:57:59 -0400 - 2016-07-04 01:13:01 -0400)",
    "18.689 kcal B9CCB30C-9B83-453B-9B3A-AA7911E51E77 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 01:13:01 -0400 - 2016-07-04 01:28:03 -0400)",

Reading results for HKQuantityTypeIdentifierFlightsClimbed:
    "1 count 42F7371D-54D5-4709-AC68-9DF79ECB2A4D \"Peter's iPhone\" (10.0) \"iPhone\"  (2016-07-04 17:24:06 -0400 - 2016-07-04 17:24:06 -0400)",
    "1 count 701F1B22-8694-4FF2-ADE6-DD4CFE8E0CCB \"Peter's iPhone\" (10.0) \"iPhone\"  (2016-07-04 17:26:36 -0400 - 2016-07-04 17:26:36 -0400)",
    "1 count 5B66EFFD-5240-411D-A48F-AA2E733B74E6 \"Peter's iPhone\" (10.0) \"iPhone\"  (2016-07-04 17:29:02 -0400 - 2016-07-04 17:29:02 -0400)",
    "1 count 690179A6-4B7F-4756-8E3C-8953E38DADE7 \"Peter's iPhone\" (10.0) \"iPhone\"  (2016-07-04 18:45:15 -0400 - 2016-07-04 18:45:15 -0400)"

Reading results for HKQuantityTypeIdentifierPushCount:
0 results for HKQuantityTypeIdentifierPushCount

Reading results for HKQuantityTypeIdentifierBloodPressureDiastolic:
0 results for HKQuantityTypeIdentifierBloodPressureDiastolic

Reading results for HKQuantityTypeIdentifierRespiratoryRate:
0 results for HKQuantityTypeIdentifierRespiratoryRate

Reading results for HKQuantityTypeIdentifierActiveEnergyBurned:
    "1.645 kcal B50A39CF-3CE3-46DF-A5B8-1C7B31605A8A \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-03 23:59:16 -0400 - 2016-07-04 00:00:17 -0400)",
    "0.037 kcal 140CFA8F-AC84-490C-AC09-B145DEC4494A \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:01:08 -0400 - 2016-07-04 00:02:00 -0400)",
    "0.229 kcal 5CA6DD86-1583-49DF-AFB2-FCFD8AEC79CE \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:02:00 -0400 - 2016-07-04 00:03:01 -0400)",
    "0.176 kcal F032C943-AA95-4F6C-A723-7F49F142F4E6 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:03:01 -0400 - 2016-07-04 00:04:02 -0400)",
    "0.458 kcal 0A6D2A5C-EA62-4EA6-8699-74CE3D622C10 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:04:02 -0400 - 2016-07-04 00:05:04 -0400)",
    "0.478 kcal 7667F45C-ED44-4AFF-BB7F-5634FDD16720 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:05:04 -0400 - 2016-07-04 00:06:05 -0400)",

Reading results for HKQuantityTypeIdentifierBodyTemperature:
0 results for HKQuantityTypeIdentifierBodyTemperature

Reading results for HKQuantityTypeIdentifierDistanceCycling:
0 results for HKQuantityTypeIdentifierDistanceCycling

Reading results for HKQuantityTypeIdentifierBasalBodyTemperature:
0 results for HKQuantityTypeIdentifierBasalBodyTemperature

Reading results for HKQuantityTypeIdentifierHeartRate:
    "1.31667 count/s E096E079-4BEF-4D88-B380-0E4037B1BB1D \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:03:11 -0400 - 2016-07-04 00:03:11 -0400)",
    "1.1 count/s F5E46916-0E24-47C3-BBA7-8FC695B8D4A6 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:10:57 -0400 - 2016-07-04 00:10:57 -0400)",
    "1.21667 count/s D4AEC739-EF97-4B55-A3B2-4B227217B69D \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:17:37 -0400 - 2016-07-04 00:17:37 -0400)",
    "1.38333 count/s 17725BB4-EC7B-4C03-B2EB-F6577748DFE4 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:18:10 -0400 - 2016-07-04 00:18:10 -0400)",
    "1.68333 count/s 29F36E7E-357E-40DA-80C4-6173B67BED51 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:25:15 -0400 - 2016-07-04 00:25:15 -0400)",
    "1.33333 count/s 03BC7704-8F7D-4A1B-ADB8-2BDE07501D5C \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:29:34 -0400 - 2016-07-04 00:29

Reading results for HKQuantityTypeIdentifierDistanceWalkingRunning:
    "162.02 m C33FC4D5-48AA-419A-A75D-FC31009A83B5 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-03 23:55:41 -0400 - 2016-07-04 00:05:40 -0400)",
    "81.68 m AFD4C4B5-9B2C-4AAC-980D-454BBC4989C5 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:05:40 -0400 - 2016-07-04 00:15:39 -0400)",
    "84.93 m DE3CC77A-DDF2-4517-B31E-F913278E724A \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:15:39 -0400 - 2016-07-04 00:22:44 -0400)",
    "61.53 m B1C6776F-8750-4AB0-A6F2-B1BF939DA7F9 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:32:43 -0400 - 2016-07-04 00:40:09 -0400)",
    "20.54 m 949D2734-1669-483C-AE92-28C565FB640E \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:40:09 -0400 - 2016-07-04 00:43:47 -0400)",
    "9.68 m 4794797B-D16E-4A8E-A122-EBF41A620E39 \"Peter\U2019s Apple\U00a0Watch\" (3.0) \"Apple Watch\"  (2016-07-04 00:43:47 -0400 - 2016-07-04 00:52:52 -0400)",
```

For the data with no results, I'm wondering if that's because the watch doesn't record that type of data without a third party app or if it's just unavailable at this time?