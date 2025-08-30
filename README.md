# Lab1
Elicit and Document Requirements
1. Target users
U1 — Everyday Drivers: private car owners looking for nearby, affordable parking.
U2 — EV Drivers: need chargers and charger availability.
U3 — Visitors/Travellers: unfamiliar with area; need guidance and payment info.
Functional Requirements (FR)
FR-01 Search carparks
1 The system must allow a user to search for carpark(s).
1.1 The system must have a search bar for the user to search for carpark(s).
1.1.1 The search bar must display placeholder text to give the user a hint about the expected input.
1.1.2 The placeholder text must disappear when the user clicks on the search bar.
1.2 When a user searches for carpark(s), the user must provide the carpark name in the search bar.
1.2.1 The carpark name must be text of length greater than 0 and less than 50 characters.




1.2.4 The system must normalise queries to be case-insensitive and handle Unicode normalisation.


1.5 The system must display an error message if no carparks match the search text.




1.3 The system must filter carparks based on the text given by the user.
1.3.1 The filtering must be case-insensitive.
1.3.2 The filtering must support substring matches.
1.3.3 The filtering must support fuzzy matching for typos.
1.3.4 The system must rank filtered results by a default filter setting.
1.3.4.1 The default user setting must prioritise carparks by distance from the user’s location.


Display according to fr3


FR-02 Filter and sort carparks
1.3.6 The system must allow filtering of results by lot type, open hours, or coverage.
1.6 The system must filter the list of carparks within 100 milliseconds for inputs.
Display according to fr3


FR-03 Carpark list display
1.4 The system must display the list of filtered carparks.
1.4.1 The system must display the carpark name for each carpark.
1.4.2 The system must display the distance from the user’s current position to each carpark.
1.4.3 The system must display the number of available lots for each carpark.
1.4.4 The system must display the parking rate for each carpark.
1.4.5 The system must display the last updated timestamp for availability and rates.

FR-02 Show nearest carparks
The system must display a list of nearest carparks by default.
 2.1 When a user opens the system, the system must accept the user’s current GPS location as input.
 2.2 The system must compute distances from the user’s location to each carpark
The system must sort the list of carparks based on their distance in descending order by default.



FR-03 Live availability
The system must provide live availability information for carparks.
 3.1 The system must accept carpark IDs as input.
 3.2 The system must call the live availability API and cache results for 60 seconds.
 3.3 The system must output the number of available lots, including breakdown by type if provided.
 3.4 The system’s availability data must match the provider’s values at poll time.



FR-04 Parking rate calculation
The system must provide parking rate estimates.
 4.1 The system must accept as input a carpark ID and a time window.
 4.2 The system must compute estimated fees using tariff rules.
 4.3 The system must output a price estimate and a detailed tariff breakdown.
 4.4 The computed price must be within ±$0.10 of the official authority calculator for test cases.



FR-05 Distance and walking time calculation
The system must provide distance and walking time information for carparks.
 5.1 The system must accept as input a carpark location and a destination.
 5.2 The system must compute the driving distance from the destination to the carpark.
 5.3 The system must compute the walking time from the carpark to the destination.
 5.4 The system must output driving distance (in meters) and walking time (in minutes).
 5.5 The computed values must be consistent with a mapping SDK within ±10%.



FR-06 Save favourites
The system must allow users to save carparks as favourites.
 6.1 When a user inputs a nickname, the system must accept it along with its carpark ID
 6.2 When a user presses the add to favourites button, the system must store favourites locally or in the cloud.

 6.3 After the user saves favourites, the system must output confirmation and display the updated favourites list.
6.4 The favourites list must stay along with the user ID  across user sessions.



FR-07 Filters
The system must allow users to apply filters when searching for carparks.
 7.1 The system must accept filter parameters for:
Lot type (e.g., EV charging lot, accessible/disabled lot, motorcycle lot).
Maximum height limit (numerical input, e.g., 1.8m, 2.1m).
Opening hours (must check against carpark operating times, and allow filtering for currently open vs closed).
Payment type (e.g., cash, card, app payment, season parking).

 7.2 The system must apply filters on the client or server side.

 7.3 The system must output a filtered list of carparks that satisfy the applied filters.

 7.4 The filtered results must exclude carparks that do not meet constraints and must include only those that do, partial matches must not be shown.



FR-08 Accessibility info
The system must provide accessibility information for carparks.
 8.1 The system must accept a carpark ID as input when accessing carpark information
.
 8.2 The system must fetch accessibility data for selected carparks, including accessible lots and lift/ramp flags (if available).

 8.3 The system must display the accessibility in the form of badges/icons
.
 8.4 The presence or absence of accessibility features must match the dataset.



FR-09 EV charger info
The system must provide EV charger information for carparks.
 9.1 The system must accept a carpark ID as input when requesting charger information.

 9.2 The system must fetch EV charging data for the given carpark, including:
Number of chargers available.
Charger type(s) (e.g., Type 2, CCS, CHAdeMO).
Live status (e.g., available, occupied, out of service), if such data is provided by the API.


 9.3 The system must display an EV charger availability panel containing the above details. The panel must be formatted clearly (e.g., “4 chargers – Type 2 – 2 available”).

 9.4 All EV charger information must match the provider API exactly. If the provider API reports unavailable or stale data, the system must clearly indicate that status to the user.



FR-10 Alerts
The system must provide carpark alerts to users.
 10.1Alerts must be triggered under the following conditions:
When a favourite carpark is nearing full capacity (e.g., fewer than N lots available, where N is user-defined).
When a cheap rate period begins (based on pricing schedule).

 	10.2 The system must allow users to set thresholds for triggering alerts.
The system must perform background data fetches at regular intervals to evaluate these conditions.

 	10.3 The system must evaluate alert rules every N minutes, where N is configurable in the system configuration.

 	10.4 When an alert condition is met,  the system must output push notifications using the platform’s notification system.

	 10.5 Alerts must fire within 5 minutes of the triggering condition, ensuring notifications are timely.



FR-11 Offline fallback
The system must provide offline fallback functionality.
 11.1 Offline fallback must be triggered when no network connection is available.

 11.2 The system must present last-known availability data clearly labeled as “stale.”

 11.3 The system must output the cached data with a timestamp showing when the data was last fetched.
.
 11.4 While offline, the app must remain usable, must not crash, and must clearly display the stale badge to let users know the data is outdated .



FR-12 Carpark details
The system must provide detailed carpark information.
 12.1 The system must accept a carpark selection as input(e.g., tap on a carpark from the list or map).

 12.2 The system must fetch and display carpark detail fields, including:
Entrances and exits (addresses or map points).
Operating hours.
Accepted payment methods.
Maximum vehicle height limit.

 12.3 The system must output a detailed view of the carpark, separate from the main listing.

 12.4 All detail fields must populate according to the dataset. If a field is missing or unavailable, the system must indicate “not available” instead of leaving it blank.



Non-Functional Requirements (NFR)
NFR-01 Performance: 
The system shall return search results (FR-01) within 2.0 seconds (95th percentile) on a 4G connection.
Live availability refreshes (FR-03) shall complete within 1.0 second from cache or 1.5 seconds from the network. 
Carpark detail views (FR-12) shall load within 1.0 second at the 95th percentile.


NFR-02 Availability: 
The backend services shall maintain at least 99.5% uptime per month, and the alerts subsystem shall maintain at least 99% uptime.
 In the event of upstream API failure, the system shall fall back to cached data and display a clear “Data temporarily unavailable” banner with a freshness timestamp, rather than failing silently or crashing.


NFR-03 Reliability: 
The system shall ensure no loss of user data, including favourites and settings, across app updates or reinstalls. 
The mobile app shall maintain a crash-free session rate of at least 99.8%.


NFR-04 Usability: 
The system shall allow users to complete the core task of finding and navigating to a carpark within three taps. 
The user interface shall comply with WCAG 2.1 AA standards, including text contrast, and support text scaling up to 200% without cutting off content.


NFR-05 Security/Privacy: 
All communication shall be secured with TLS 1.2 or higher, and user favourites shall be encrypted at rest with AES-256. 
Location data shall be processed locally on the device where possible
All logs containing personal data shall be retained for no longer than 180 days in compliance with PDPA.


NFR-06 Compatibility: 
The mobile application shall support at least the last two major versions of iOS and Android (minimum: iOS 15+ and Android 10+). 
The user interface shall function correctly on screens ranging from 4.7″ to 12.9″, and shall support both light and dark mode.


NFR-07 Maintainability: 
The codebase shall maintain at least 80% unit test coverage of domain logic, and continuous integration builds shall complete within 10 minutes. 
The system shall use feature flags to toggle external API integrations, ensuring that changes can be tested safely without code redeployment.


NFR-08 Localization: 
The system shall launch with support for English (en-SG)
All user-visible strings shall be externalized so that additional locales can be added in the future through an internationalization framework.


NFR-09 Scalability:
The system shall be able to handle at least three times the normal request load for 30 minutes during peak events (e.g., concerts or national holidays) without exceeding the response-time targets defined in NFR-01.


NFR-10 Data Freshness:
The system shall ensure that all live availability data is no more than 15 minutes old
The system shall clearly display a freshness indicator such as “Updated X minutes ago” in the user interface.


NFR-11 Observability:
The system shall provide end-to-end observability, including correlated logs, metrics, and traces with request IDs. 
The system shall trigger alerts when service level objectives are at risk, and maintain audit logs of significant state changes for debugging and compliance.


NFR-12 Offline and Robustness:
When no network connection is available, the system shall continue to present the last-known data, clearly marked as stale with a timestamp. 
The system shall handle API timeouts, errors, or malformed responses by showing a user-friendly message and retrying gracefully, without application crashes.
