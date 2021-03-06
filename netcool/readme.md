Boundary-Netcool-Feed
=====================

This integration is instrumented as a combination of:
- 1 Netcool objectserver temporal trigger `bluebridge_trigger`
- 1 Netcool objectserver external procedure `bluebridge_proc`
- 1 BASH script `bluebridge.sh` which uses the [Event REST API](https://app.boundary.com/docs/events_api) to create events in [Boundary](https://app.boundary.com).

`bluebridge_trigger` executes on a configured interval (typically every 1-5 minutes), identifies new alerts which haven't been sent to Boundary yet and passes the core alert fields to the `bluebridge_proc` external procedure which calls the `bluebridge.sh` script.

`bluebridge.sh` currently processes only the core alerts.status fields of:
Summary, Severity, Node, Identifier, Serial, ServerName

The Netcool code is manually defined in the objectserver but may be imported via confpack in an upcoming release. `bluebridge.sh` can reside in any directory but would most commonly be stored in `$OMNIHOME/utils`.

