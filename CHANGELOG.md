# Changelog
All notable changes to this project will be documented in this file.

## 2.0.6 - 2022-08-03
* Added update campaigns and feature flag configurations instantaneously with Real-Time Streaming Architecture: [`documentation`](https://developers.kameleoon.com/java-sdk.html#streaming) or [`product Updates`](https://www.kameleoon.com/en/blog/real-time-streaming)
* Added **KameleoonConfiguration**, it can be used as parameter during initialization of a client. Related to [`KameleoonClientFactory.create`](https://developers.kameleoon.com/java-sdk.html#com-kameleoon-kameleoonclientfactory)
* Added support for **Experiment** & **Exclusive Campaign** conditions. Related to [`triggerExperiment`](https://developers.kameleoon.com/java-sdk.html#triggerexperiment)
* Fixed an issue when an user which was already registered with a variation gets new randomly selected variation. Related to [`triggerExperiment`](https://developers.kameleoon.com/java-sdk.html#triggerexperiment)
* Added method to obtain a list of feature flags: [`obtainFeatureList`](https://developers.kameleoon.com/java-sdk.html#obtainfeaturelist)
* Added method to obtain a list of feature flags targeted for specified visitor code: [`obtainFeatureListForVisitorCode`](https://developers.kameleoon.com/java-sdk.html#obtainfeaturelistforvisitorcode)
* Added method to obtain a list of experiments: [`obtainExperimentList`](https://developers.kameleoon.com/java-sdk.html#obtainexperimentlist)
* Added method to obtain a list of experiments targeted for specified visitor code: [`obtainExperimentListForVisitorCode`](https://developers.kameleoon.com/java-sdk.html#obtainexperimentlistforvisitorcode)
* Added method to obtain all variables for feature flag: [`obtainFeatureAllVariables`](https://developers.kameleoon.com/java-sdk.html#obtainfeatureallvariables)
* Added an indication of feature flag (Id, Key) when exception happens. Related to [`activateFeature`](https://developers.kameleoon.com/java-sdk.html#activatefeature), [`obtainFeatureVariable`](https://developers.kameleoon.com/java-sdk.html#obtainfeaturevariable)
* Added an indication of experiment (Id) when exception happens. Related to [`triggerExperiment`](https://developers.kameleoon.com/java-sdk.html#triggerexperiment)
* Added new data type [`Device`](https://developers.kameleoon.com/java-sdk.html#device). Possible values are: **PHONE**, **TABLET**, **DESKTOP**. 
* Removed obsolete data type `Interest`
* Added support of `is among the values` operator for Custom Data

## 2.0.5 - 2022-04-12
* Added method for retrieving data from remote source: [`retrieveDataFromRemoteSource`](https://developers.kameleoon.com/java-sdk.html#retrievedatafromremotesource)
* Removed error notification when configration file is missed

## 2.0.4 - 2022-02-28
* Added support of multi-environment for feature flags, Related to [`activateFeature`](https://developers.kameleoon.com/java-sdk.html#activatefeature), [`obtainFeatureVariable`](https://developers.kameleoon.com/java-sdk.html#obtainfeaturevariable)
* Added scheduling functionality for [`activateFeature`](https://developers.kameleoon.com/java-sdk.html#activatefeature)
* Adding URI encoding for [`CustomData`](https://developers.kameleoon.com/java-sdk.html#customdata) & [`PageView`](https://developers.kameleoon.com/java-sdk.html#pageview)
* Added VisitorCodeNotValid exception when exceeding the limit of 255 chars for [`activateFeature`](https://developers.kameleoon.com/java-sdk.html#activatefeature) ,  [`triggerExperiment`](https://developers.kameleoon.com/java-sdk.html#triggerexperiment) , [`trackConversion`](https://developers.kameleoon.com/java-sdk.html#trackConversion) , 
    [`addData`](https://developers.kameleoon.com/java-sdk.html#addData) , [`flush`](https://developers.kameleoon.com/java-sdk.html#flush)
* Added boolean, number and JSON objects to [`obtainFeatureVariable`](https://developers.kameleoon.com/java-sdk.html#obtainfeaturevariable) as a returned values (before it returns only strings)
* Added checking for status of site_code (Enable / Disable). Related to [`activateFeature`](https://developers.kameleoon.com/java-sdk.html#activatefeature) and [`triggerExperiment`](https://developers.kameleoon.com/java-sdk.html#triggerexperiment)

## 2.0.3 - 2021-06-16
* Added DEVIATED status

## 2.0.2 - 2021-05-24
* Added Kameleoon-Client header

## 2.0.1 - 2021-02-26
* Added topLevelDomain

## 2.0.0 - 2021-02-16
* Updated the configuration file path.
* Added obtainFeatureVariable() method.