# Useful Queries

These are a few common KQL queries I've had customers ask about.

* **[CVE Last Seen](./CVEsLastSeen.kql)**: Reports when the CVE was last seen per device and gives an idea of when the CVE was most recently detected on that device.
* **[Device State](./DeviceState.kql) and [Device State 2](./DeviceState2.kql)**: Reports the Device's state including Defender versions, AV scan date/results, and other various pieces of information.
* **[Last Seen Alert](./LastSeenAlert.kql)**: Using the TVM table, which is generally updated every day, this query identifies machines where the TVM data was not updated and therefore may not be communicating with the service any more.
* **[OnboardOffboard](./OnboardOffboard.kql)**: The goal is to detect when a device is onboarded to or offboarded from MDE. Unforunately, there are no current events that record this in the system, so this query doesn't work today.
