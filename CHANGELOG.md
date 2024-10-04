# Changelog
All notable changes to this project will be documented in this file.

## 4.6.0 - 2024-10-04
### Features
* Introduced new evaluation methods for clarity and improved efficiency when working with the SDK:
  - [`getVariation`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#getvariation)
  - [`getVariations`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#getvariations)
* These methods replace the deprecated ones:
  - [`getFeatureVariationKey`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#getfeaturevariationkey)
  - [`getFeatureVariable`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#getfeaturevariable)
  - [`getFeatureVariables`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#getfeaturevariables)
  - [`getActiveFeatures`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#getactivefeatures)
  - [`getFeatureVariationVariables`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#getfeaturevariationvariables)
* A new version of the [`isFeatureActive`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#isfeatureactive) method now includes an optional `track` parameter, which controls whether the assigned variation is tracked (default: `true`).
* Enhanced top-level domain validation within the SDK. The implementation now includes automatic trimming of extraneous symbols and provides a [warning](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#log-levels) when an invalid domain is detected.
* Enhanced the [`getEngineTrackingCode`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#getenginetrackingcode) method to properly handle `JS` and `CSS` variables.

## 4.5.1 - 2024-08-13
### Bug fixes
* Fixed an issue that caused duplicate entries in feature flag results for both anonymous and authorized/identified visitors during data reconciliation. This problem occurred when custom data of type mapping ID was not consistently sent for all sessions.

## 4.5.0 - 2024-08-01
### Features
* Added [`waitInit`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#waitinit) method, which allows to check if the client has been successfully initialized before proceeding with other operations.
### Bug fixes
* Resolved an issue where the SDK could become stuck during prolonged Data API outages.

## 4.4.0 - 2024-07-11
### Features
* Enhanced [logging](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#logging):
    - Introduced [log levels](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#log-levels):
        - `None`
        - `Error`
        - `Warning`
        - `Info`
        - `Debug`
    - Added support for [custom logger](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#custom-handling-of-logs) implementations.
* Improved the tracking mechanism to consolidate multiple visitors into a single request. The new approach combines information on all affected visitors into one request, which is sent once per interval.
* Added a new variation of the [`flush(boolean instant, String visitorCode)`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#flush) with `instant` parameter. If the parameter's value is `true` the visitor's data is tracked instantly. Otherwise, the visitor's data will be tracked with next tracking interval. Default value of the parameter is `false`.
* Added new configuration parameter `trackingInterval` (`tracking_interval_millisecond`) to [`KameleoonClientConfig`](https://developers.kameleoon.com/java-sdk.html#additional-configuration) and the [configuration](https://developers.kameleoon.com/java-sdk.html#additional-configuration) file, which is used to set interval for tracking requests. Default value is `1000` milliseconds.
* New Kameleoon Data type [`UniqueIdentifier`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#uniqueidentifier) is introduced. It will be used in all methods instead of `isUniqueIdentifier` parameter. All methods with `isUniqueIdentifier` parameter are marked as deprecated:
    - [`flush`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#flush)
    - [`trackConversion`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#trackconversion)
    - [`getFeatureVariationKey`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#getfeaturevariationkey)
    - [`getFeatureVariable`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#getfeaturevariable)
    - [`getFeatureVariables`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#getfeaturevariables)
    - [`isFeatureActive`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#isfeatureactive)
    - [`getRemoteVisitorData`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#getremotevisitordata)
### Bug fixes
* Resolved an issue where the [`flush(null, isUniqueIdentifier)`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#flush) method was incorrectly sending requests with `isUniqueIdentifier` applied to each visitor. Now, `isUniqueIdentifier` is only considered if `visitorCode` is provided and not null.

## 4.3.0 - 2024-06-13
### Features
* The [Likelihood to convert](https://developers.kameleoon.com/feature-management-and-experimentation/using-visit-history-in-feature-flags-and-experiments) targeting condition is now available. Pre-loading the data is required using [`getRemoteVisitorData`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#getremotevisitordata) with the `kcs` parameter set to `true`.
* Added [`getActiveFeatures`](https://developers.kameleoon.com/java-sdk.html#getActiveFeatures) method uses for obtaining a information about the active feature flags that are available for the visitor.
* Method [`getActiveFeatureListForVisitorCode`](https://developers.kameleoon.com/java-sdk.html#getActiveFeatureListForVisitorCode) is deprecated
### Bug fixes
* Resolved an issue where the [`getVisitorCode`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#getvisitorcode) did not apply the provided `defaultVisitorCode`.


## 4.2.1 - 2024-05-06
### Bug fixes
* Stability and performance improvements

## 4.2.0 - 2024-04-27
### Features
* Added a new optional parameter `isUniqueIdentifier` that provides additional capabilities with [cross-device experimentation](https://developers.kameleoon.com/core-concepts/cross-device-experimentation) in the following methods:
    - [`flush`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#flush)
    - [`trackConversion`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#trackconversion)
    - [`getFeatureVariationKey`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#getfeaturevariationkey)
    - [`getFeatureVariable`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#getfeaturevariable)
    - [`isFeatureActive`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#isfeatureactive)
    - [`getFeatureVariables`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#getfeaturevariables)
    - [`getRemoteVisitorData`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#getremotevisitordata)
* New targeting conditions are now available (some of them may require [`getRemoteVisitorData`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#getremotevisitordata) pre-loaded data)
  - Browser Cookie
  - Operating System
  - IP Geolocation
  - Kameleoon Segment
  - Target Feature Flag
  - Previous Page
  - Number of Page Views
  - Time since First Visit
  - Time since Last Visit
  - Number of Visits Today
  - Total Number of Visits
  - New or Returning Visitor
* New Kameleoon Data types were introduced:
  - [`Cookie`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#cookie)
  - [`OperatingSystem`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#operatingsystem)
  - [`Geolocation`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#geolocation)

## 4.1.1 - 2024-04-04
### Bug fixes
* Stability and performance improvements

## 4.1.0 - 2024-02-16
### Features
* Added support for additional Data API servers across the world for even faster network requests.
* Increased limit for requests to Data API: [rate limits](https://developers.kameleoon.com/apis/data-api-rest/overview/#rate-limits)
* Added [`getVisitorWarehouseAudience`](https://developers.kameleoon.com/java-sdk.html#getvisitorwarehouseaudience) method to retrieve all data associated with a visitor's warehouse audiences and adds it to the visitor.

## 4.0.5 - 2023-12-12
### Bug fixes
* Stability and performance improvements

## 4.0.4 - 2023-12-06
### Bug fixes
* Stability and performance improvements

## 4.0.3 - 2023-11-24
### Bug fixes
* Resolved an issue where the [`KameleoonClient`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#initialize-the-kameleoon-client) could throw `NullPointerException` in certain cases.

## 4.0.2 - 2023-11-21
### Bug fixes
* Stability and performance improvements

## 4.0.1 - 2023-11-07
### Features
* Changed the parameter `HttpServletResponse` in method [`setLegalConsent`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#setlegalconsent) to optional.


## 4.0.0 - 2023-11-03
### Breaking changes
* Removed all deprecated methods and exceptions related to **experiments**:
    - `triggerExperiment`
    - `getVariationAssociatedData` (`obtainVariationAssociatedData`)
    - `getExperimentList`
    - `getExperimentListForVisitor`
    - `ExperimentConfigurationNotFound`
    - `NotTargeted`
    - `NotAllocated`
    - `SiteCodeDisabled`
* Removed additional methods that were deprecated in 3.x versions:
    - `activateFeature`
    - `obtainVisitorCode`
    - `retrieveDataFromRemoteSource`
* Renamed the following classes, methods and exceptions:
    - `KameleoonConfiguration` to [`KameleoonClientConfig`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#example-code)
    - `getFeatureAllVariables` to [`getFeatureVariationVariables`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#getfeaturevariationvariables)
    - `FeatureConfigurationNotFound` to `FeatureNotFound`
    - `VariationConfigurationNotFound` to `FeatureVariationNotFound`
    - `CredentialsNotFound` to `ConfigCredentialsInvalid`
    - `VisitorCodeNotValid` to `VisitorCodeInvalid`
* Changes in the [configuration](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#additional-configuration) file:
    - removed `visitor_data_maximum_size`
    - renamed `session_duration` to `session_duration_minute`
    - renamed `refresh_interval` to `refresh_interval_minute`
* Added new exception `FeatureEnvironmentDisabled` indicating that the feature flag is disabled for certain environments. The following methods can throw the new exception:
    - [`getFeatureVariationKey`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#getfeaturevariationkey)
    - [`getFeatureVariable`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#getfeaturevariable)
    - [`getFeatureVariables`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#getfeaturevariables)
    - [`getFeatureVariationVariables`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#getfeaturevariationvariables)
* Removed parameter `topLevelDomain` from [`getVisitorCode`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#getvisitorcode). Instead, use the `topLevelDomain` parameter in the [configuration](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#additional-configuration) (using either the `KameleoonClientConfig` object or the external configuration file).
* Added new exception `SiteCodeIsEmpty` for method [`KameleoonClientFactory.create`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#create) indicating that the provided sitecode is empty.

### Features
* Added [`setLegalConsent`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#setlegalconsent) method to determine the types data Kameleoon includes in tracking requests. This helps you adhere to legal and regulatory requirements while responsibly managing visitor data. You can find more information in the [Consent management policy](https://help.kameleoon.com/consent-management-policy/).
* Added [`getFeatureVariables`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#getfeaturevariables) method to retrieve all variable keys and their corresponding values assigned to a visitor's variation for a specific feature flag.
* Added new configuration parameters to [`KameleoonClientConfig`](https://developers.kameleoon.com/java-sdk.html#additional-configuration) and the [configuration](https://developers.kameleoon.com/java-sdk.html#additional-configuration) file:
    - `topLevelDomain`(`top_level_domain`), which is used to set the domain name.
    - `defaultTimeout` (`default_timeout_millisecond`) that designates the predefined timeout for network requests.

### Bug fixes
* Stability and performance improvements

## 3.3.1 - 2023-09-28
### Bug fixes
* Stability and performance improvements

## 3.3.0 - 2023-09-25
### Features
* Added new parameter [`sessionDuration`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#additional-configuration) to `KameleoonConfiguration` and `session_duration` field to the external configuration file. The session duration setting determines the time (in minutes) that a visitor's data is retained in RAM. When a session expires, the visitor data is deleted. You can restore the data using [`getRemoteVisitorData`](https://developers.kameleoon.com/java-sdk.html#getRemoteVisitorData). The `visitorDataMaximumSize` method has been deprecated. Use the new `sessionDuration` method instead.
* Starting from this release, it is now imperative that your application gracefully handles `HttpException` exceptions (using the `exceptionally` method of the `CompletableFuture` instance) for the following methods:
    - [`getRemoteData`](https://developers.kameleoon.com/java-sdk.html#getRemoteData)
    - [`getRemoteVisitorData`](https://developers.kameleoon.com/java-sdk.html#getRemoteVisitorData)
* Introduced a new data parameter called [`LegalConsent`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#legalconsent) which can have values of `true` or `false`. It's used to indicate whether legal consent is received from visitors or not. The [`LegalConsent`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#legalconsent) parameter determines which data can be included in tracking requests, enabling to adhere to legal and regulatory requirements while responsibly managing visitor data. More information could be found at: https://help.kameleoon.com/consent-management-policy/
* Changed syntax for creation of [`Device`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#device) and [`Browser`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#browser) data:
    - `Device::DESKTOP` is now `Device.desktop()`
    - `Device::TABLET` is now `Device.tablet()`
    - `Device::PHONE` is now `Device.phone()`
    - `Browser::CHROME` is now `Browser.chrome()`
    - `Browser::INTERNET_EXPLORER` is now `Browser.internetExplorer()`
    - `Browser::FIREFOX` is now `Browser.firefox()`
    - `Browser::SAFARI` is now `Browser.safari()`
    - `Browser::OPERA` is now `Browser.opera()`
    - `Browser::OTHER` is now `Browser.other()`

## 3.2.3 - 2023-08-25
### Bug fixes
* Fixed an issue where the SDK couldn't update the data configuration when using the [Real-Time Streaming Architecture](https://developers.kameleoon.com/feature-management-and-experimentation/technical-considerations/#streaming)

## 3.2.2 - 2023-07-20
* Minor improvements

## 3.2.1 - 2023-07-19
* Added new conditions for targeting:
    - `Explicit Trigger`

## 3.2.0 - 2023-07-07
* Added method to fetch remote visitor's data (with an optional capability to add data for a visitor):
    - [`getRemoteVisitorData`](https://developers.kameleoon.com/java-sdk.html#getRemoteVisitorData)
* Removed `enableProxySupport` method.
* Minor changes:
    - [`getRemoteData`](https://developers.kameleoon.com/java-sdk.html#getRemoteData) returns object of `CompletableFuture<JsonObject>` type.
    - [`getRemoteData`](https://developers.kameleoon.com/java-sdk.html#getRemoteData) method does not throw `HttpException` exception anymore.
    - `retrieveDataFromRemoteSource` method does not throw `HttpException` and `IOException` exceptions anymore.
    - `Browser` data class could accept version number of browser
* Added new conditions for targeting:
    - `Visitor Code`
    - `SDK Language`
    - [`Page Title & Page Url`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#pageview)
    - [`Browser`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#browser)
    - [`Device`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#device)
    - [`Conversion`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#trackconversion)

## 3.1.2 - 2023-05-17
* All Kameleoon exceptions are inherited from the KameleoonExceptions class.

## 3.1.1 - 2023-04-28
* Minor improvements

## 3.1.0 - 2023-04-20
* Added a new method which can be used to simplify utilization of hybrid mode:
    - [`getEngineTrackingCode`](https://developers.kameleoon.com/java-sdk.html#getEngineTrackingCode)
* Added possibility for [`CustomData`](https://developers.kameleoon.com/java-sdk.html#customdata) to use variable argument list of values
* Renaming of method:
    - `retrieveDataFromRemoteSource` -> [`getRemoteData`](https://developers.kameleoon.com/java-sdk.html#getRemoteData)

## 3.0.0 - 2023-02-17
* Added support of new feature flag rules:
    - [`getFeatureVariationKey`](https://developers.kameleoon.com/java-sdk.html#getFeatureVariationKey)
    - `obtainFeatureVariable` -> [`getFeatureVariable`](https://developers.kameleoon.com/java-sdk.html#getFeatureVariable)
    - [`getFeatureAllVariables`](https://developers.kameleoon.com/java-sdk.html#getFeatureAllVariables)
    - `activateFeature` -> [`isFeatureActive`](https://developers.kameleoon.com/java-sdk.html#isFeatureActive)
* Renaming of methods (old methods warn you on using and will be removed later)
    - `obtainVisitorCode` -> [`getVisitorCode`](https://developers.kameleoon.com/java-sdk.html#getVisitorCode)
    - `obtainVariationAssociatedData` -> [`getVariationAssociatedData`](https://developers.kameleoon.com/java-sdk.html#getVariationAssociatedData),
    - `obtainFeatureAllVariables` -> [`getFeatureAllVariables`](https://developers.kameleoon.com/java-sdk.html#getFeatureAllVariables),
    - `obtainExperimentList` -> [`getExperimentList`](https://developers.kameleoon.com/java-sdk.html#getExperimentList)
    - `obtainExperimentListForVisitorCode` -> [`getExperimentListForVisitorCode`](https://developers.kameleoon.com/java-sdk.html#getExperimentListForVisitorCode)
    - `obtainFeatureList` -> [`getFeatureList`](https://developers.kameleoon.com/java-sdk.html#getFeatureList)
    - `obtainFeatureListListForVisitorCode` -> [`getActiveFeatureListForVisitorCode`](https://developers.kameleoon.com/java-sdk.html#getActiveFeatureListForVisitorCode)
* Renaming of exceptions:
    - `NotActivated` -> `NotAllocated`
* Changes in Kameleoon Data:
    - Added possibility to set [`UserAgent`](https://developers.kameleoon.com/java-sdk.html#useragent).
* Removed blocking mode of SDK. Related to methods: [`triggerExperiment`](https://developers.kameleoon.com/java-sdk.html#triggerexperiment), [`isFeatureActive`](https://developers.kameleoon.com/java-sdk.html#isFeatureActive)

## 2.0.7 - 2022-08-24
* Fixed crash on initialization with KameleoonConfiguration parameter

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

# Unsupported versions:

## 2.0.5 - 2022-04-12 `[Deprecated]`
* Added method for retrieving data from remote source: [`retrieveDataFromRemoteSource`](https://developers.kameleoon.com/java-sdk.html#retrievedatafromremotesource)
* Removed error notification when configration file is missed

## 2.0.4 - 2022-02-28 `[Deprecated]`
* Added support of multi-environment for feature flags, Related to [`activateFeature`](https://developers.kameleoon.com/java-sdk.html#activatefeature), [`obtainFeatureVariable`](https://developers.kameleoon.com/java-sdk.html#obtainfeaturevariable)
* Added scheduling functionality for [`activateFeature`](https://developers.kameleoon.com/java-sdk.html#activatefeature)
* Adding URI encoding for [`CustomData`](https://developers.kameleoon.com/java-sdk.html#customdata) & [`PageView`](https://developers.kameleoon.com/java-sdk.html#pageview)
* Added VisitorCodeNotValid exception when exceeding the limit of 255 chars for [`activateFeature`](https://developers.kameleoon.com/java-sdk.html#activatefeature) , [`triggerExperiment`](https://developers.kameleoon.com/java-sdk.html#triggerexperiment) , [`trackConversion`](https://developers.kameleoon.com/java-sdk.html#trackConversion) ,
    [`addData`](https://developers.kameleoon.com/java-sdk.html#addData) , [`flush`](https://developers.kameleoon.com/java-sdk.html#flush)
* Added boolean, number and JSON objects to [`obtainFeatureVariable`](https://developers.kameleoon.com/java-sdk.html#obtainfeaturevariable) as a returned values (before it returns only strings)
* Added checking for status of site_code (Enable / Disable). Related to [`activateFeature`](https://developers.kameleoon.com/java-sdk.html#activatefeature) and [`triggerExperiment`](https://developers.kameleoon.com/java-sdk.html#triggerexperiment)

## 2.0.3 - 2021-06-16 `[Deprecated]`
* Added DEVIATED status

## 2.0.2 - 2021-05-24 `[Deprecated]`
* Added Kameleoon-Client header

## 2.0.1 - 2021-02-26 `[Deprecated]`
* Added topLevelDomain

## 2.0.0 - 2021-02-16 `[Deprecated]`
* Updated the configuration file path.
* Added obtainFeatureVariable() method.
