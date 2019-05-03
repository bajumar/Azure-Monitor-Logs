# Server Asset Inventory Queries Prerequisites & Comments

**Heartbeat-based Query Examples**

Heartbeat logs for Windows Servers do not log the full operating system release name (e.g. Windows Server 2019), so the full release name must be derived from the operating system Major and Minor version numbers. Windows operating system version numbers are identical for Windows Servers and Windows Dekstops from the same release cycle (e.g. Windows 10 version is identified as "10.0", and Windows Server 2016 version is also identified as "10.0").

The relevant queries in this repo assume that the logged version numbers are for Windows Server oprating systems, and use the Log Analytics Query Language "datatable" operator to construct the lookup table to map the version numbers to the full release name.

*Reference: https://docs.microsoft.com/en-us/windows/desktop/SysInfo/operating-system-version*

