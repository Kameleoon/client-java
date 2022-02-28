# Changelog
All notable changes to this project will be documented in this file.

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