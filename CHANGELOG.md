[trackconversion]: https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#trackconversion

# Changelog
## 4.18.0 - 2025-11-21
### Features
* Updated evaluation and tracking logic to comply with GDPR requirements when consent is not given:
    - If behavior is **partially blocked**, the default variation will be returned.
    - If behavior is **completely blocked**, an exception will be thrown.

## 4.17.2 - 2025-10-30
### Bug fixes
* Fixed an issue where [`Conversion`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#conversion)'s metadata initialized with a name was not tracked.
* Changed the **Unexpected TargetingConditionType** log's level to `INFO`.

## 4.17.1 - 2025-09-04
### Bug fixes
* Fixed an issue where a proxy host value was converted incorrectly.

## 4.17.0 - 2025-08-29
### Features
* Added an `overwrite` flag to [`CustomData`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#customdata), used as the `overwrite` parameter during tracking.
* [`CustomData`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#customdata) can now be created using a `name`, in addition to the existing method of using an `index`.
* Added a new property `defaultVariationKey` and a method `getDefaultVariation()` to [`FeatureFlag`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#featureflag). The method returns information about the default variation associated with the feature flag.
* Added a new property `rules` of type [`List<Rule>`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#rule) to [`FeatureFlag`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#featureflag), which defines the targeting rules associated with the feature flag.

## 4.16.0 - 2025-08-20
### Features
* Introduced a new [`getDataFile`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#getdatafile) method. This method returns the current SDK configuration (also known as the **data file**) used for evaluation and targeting. It is **not** intended for production use to fetch variations for every feature flag in the returned list, as it is not optimized for performance. For that purpose, use [`getVariations`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#getvariations) instead. `getDataFile` is mainly useful for debugging or QA, for example to let internal users manually select a variant for a specific feature flag in production.
* Added a new property `name` to [`Variation`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#variation), representing the name of the variation.

## 4.15.0 - 2025-07-23
### Features
* Added the [`evaluateAudiences`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#evaluateaudiences) method. This method iterates over all Audiences Explorer segments, evaluates each one, and tracks the segments for which the visitor is targeted using the [`TARGETINGSEGMENT`](https://developers.kameleoon.com/apis/data-api-rest/all-endpoints/post-visit-events/) event.

## 4.14.1 - 2025-07-01
### Bug fixes
* Stability and performance improvements

## 4.14.0 - 2025-06-27
### Features
* Added support for using a Custom Data value for traffic bucketing instead of the default visitor code. [Learn More](https://help.kameleoon.com/create-feature-flag/#Advanced_Flag_Settings).
* Reduced the number of requests to OAuth service if it has outage.

## 4.13.0 - 2025-05-26
### Features
* Added support for a **New**/**Returning** visitor breakdown filter in reports (requires calling [`getRemoteVisitorData`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#getremotevisitordata)).
* Added support for **304 (Not Modified)** responses from the SDK config service to avoid redundant updates and reduce traffic when the configuration hasn't changed.
### Bug fixes
* Fixed an issue where the value of the `negative` parameter was ignored in the [`trackConversion(String visitorCode, int goalId, boolean negative, float revenue)`][trackconversion] method overload.

All notable changes to this project will be documented in this file.

## 4.12.2 - 2025-04-08
### Bug fixes
* Changed the order in which **conversion** and **experiment** events are sent. This may lead to more accurate **visit**-level experiment reporting.

## 4.12.1 - 2025-03-26
### Bug fixes
* The value of the `revenue` parameter was not accounted for in some overloads of the [`trackConversion`][trackconversion] method.

## 4.12.0 - 2025-03-24
### Features
* Added new optional parameters `negative` and `metadata` to the [`trackConversion`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#trackconversion) method.
* Added new optional parameter `metadata` to the [`Conversion`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#conversion) data constructor.
* Changed the log level for deprecated methods from **WARNING** to **INFO**.

## 4.11.0 - 2025-03-18
### Features
* Added support for Contextual Bandit evaluations. Calling [`getRemoteVisitorData`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#getremotevisitordata) with the `cbs=true` flag is required for this feature to function correctly. Platform-wide release expected in March 2025.

## 4.10.0 - 2025-02-26
### Features
* Added SDK support for **Mutually Exclusive Groups**. When feature flags are grouped into a **Mutually Exclusive Group**, only one flag in the group will be evaluated at a time. All other flags in the group will automatically return their default variation.
* Added new configuration parameter `networkDomain` (`network_domain`) to [`KameleoonClientConfig`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#create) and the [configuration](https://developers.kameleoon.com/java-sdk.html#additional-configuration) file. This parameter allows specifying a custom domain for all outgoing network requests.
* Added support for new conditions:
    - Exclusive Campaign
    - Experiment
    - Personalization

## 4.9.0 - 2025-02-10
### Features
* Added SDK support for **holdout experiments**. Visitors assigned to a holdout experiment are excluded from all other rollouts and experiments, and consistently receive the default variation. For visitors not in a holdout experiment, the standard evaluation process applies, allowing them to be evaluated for all feature flags as usual. Platform-wide release expected in February 2025.

## 4.8.1 - 2024-12-05
### Bug fixes
* Resolved an issue where the SDK could waste memory by creating new connections to the SSE server when utilizing the [Real-Time Streaming Architecture](https://developers.kameleoon.com/feature-management-and-experimentation/technical-considerations/#streaming) if the SSE server was down.
* Fixed an issue where the provided cookie values could not be applied when setting **simulated** variations.

## 4.8.0 - 2024-11-28
### Features
* Added support for **simulated** variations.
* Added the [`setForcedVariation()`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#setforcedvariation) method. This method allows explicitly setting a forced variation for a visitor, which will be applied during experiment evaluation.
### Bug fixes
* Fixed an issue where the [`Variation.isActive()`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk#variation) method returned an incorrect value.

## 4.7.2 - 2024-11-19
### Bug fixes
* Resolved an issue where the validation of [top-level domains](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#additional-configuration) for `localhost` resulted in incorrect failures. The SDK now accepts the provided domain without modification if it is deemed invalid and logs an [error](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#log-levels) to notify you of any issues with the specified domain.

## 4.7.1 - 2024-11-14
### Bug fixes
* Fixed an issue with the [`Page URL`](https://developers.kameleoon.com/feature-management-and-experimentation/using-visit-history-in-feature-flags-and-experiments/#benefits-of-calling-getremotevisitordata) and [`Page Title`](https://developers.kameleoon.com/feature-management-and-experimentation/using-visit-history-in-feature-flags-and-experiments/#benefits-of-calling-getremotevisitordata) targeting conditions, where the condition evaluated all previously visited URLs in the session instead of only the current URL, corresponding to the latest added [`PageView`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#pageview).<br/>
**NOTE**: This change may impact your existing targeting. Please review your targeting conditions to ensure accuracy.

## 4.7.0 - 2024-10-24
### Features
* Introduced a new package with support for [Jakarta EE](https://jakarta.ee/), complementing the existing package for [Java EE](https://www.oracle.com/java/technologies/java-ee-glance.html). The new package is now available in the [Maven repository](https://central.sonatype.com/artifact/com.kameleoon/kameleoon-client-java-jakarta). For more detailed information, please refer to [this documentation](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#install-the-java-client).
* Introduced a new `visitorCode` parameter to [`RemoteVisitorDataFilter`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#using-parameters-in-getremotevisitordata). This parameter determines whether to use the `visitorCode` from the most recent previous visit instead of the current `visitorCode`. When enabled, this feature allows visitor exposure to be based on the retrieved `visitorCode`, facilitating [cross-device reconciliation](https://developers.kameleoon.com/core-concepts/cross-device-experimentation/). Default value of the parameter is `true`.
* Use [`RemoteVisitorDataFilterBuilder`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#using-parameters-in-getremotevisitordata) instead of the deprecated [`RemoteVisitorDataFilter`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#using-parameters-in-getremotevisitordata) constructor.

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
