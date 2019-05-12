### Table: Computer Geo-Locations

```
// Table: Computer Geo-Locations
Heartbeat
| distinct Computer, ComputerEnvironment, RemoteIPCountry, RemoteIPLatitude, RemoteIPLongitude
| sort by Computer asc
```
