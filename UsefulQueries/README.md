# Useful Queries

These are a few common KQL queries I've had customers ask about.

* **[Device State](./DeviceState.kql) and [Device State 2](./DeviceState2.kql)**: Reports the Device's state including Defender versions, AV scan date/results, and other various pieces of information.
* **[Last Seen Alert](./LastSeenAlert.kql)**: Using the TVM table, which is generally updated every day, this query identifies machines where the TVM data was not updated and therefore may not be communicating with the service any more.
* **[Heartbeat](./Heartbeat.kql)**: Using the Sentinel integration and the Heartbeat table which records a communication from a device, typically at least once per 5 minutes, this query finds devices that have not sent a heartbeat in over 1 hour.
* **[OnboardOffboard](./OnboardOffboard.kql)**: The goal is to detect when a device is onboarded to or offboarded from MDE. Unforunately, there are no current events that record this in the system, so this query doesn't work today.
* **[Connectivity Type](./Connectivity.kql)**: This query shows the connectivity method used by each endpoint communicating with MDE. There are three potential values: `blank`,`Standard`,`Streamlined`. *Standard* is the original legacy method of connecting with the service while *Streamlined* is the latest/modern approach.
