# Windows Network Sessions & Firewall Security Lab

## Overview
In this exercise, I used a Windows computer and Windows Command Prompt to run `netstat`, `tasklist`, and `netsh advfirewall`. My goal was to identify active network sessions, investigate port 445, and verify firewall protection.

## Tools Used
- Windows Command Prompt
- `netstat`
- `tasklist`
- `netsh advfirewall`

- ## Commands and Findings
- ### 1. View Active Connections

```text
netstat -a
![Active connections output](01-netstat-active-connections-redacted.png)

### 2. Identify the Process Using Port 445

```text
netstat -ano | findstr :445
```

Port 445 was listening on both IPv4 and IPv6. The command identified process ID (PID) `4` as the process associated with this port.
![Port 445 and PID](02-port-445-pid-redacted.png)

### 3. Confirm the Process Name

```text
tasklist /fi "PID eq 4"
```

The command confirmed that PID `4` belongs to the Windows `System` process.
![PID 4 System process confirmation](03-pid-4-system-process-redacted.png)

### 4. Check Windows Firewall Profiles

```text
netsh advfirewall show allprofiles
```

The Domain, Private, and Public firewall profiles were enabled. Each profile used the `BlockInbound,AllowOutbound` policy.
![Windows Firewall profile status](04-windows-firewall-profiles-redacted.png)

## Security Takeaways

- Port 445 is commonly used by Windows SMB file and printer sharing.
- A listening port should be reviewed to confirm that the related service is necessary.
- A listening port does not automatically mean that the device is exposed to the internet.
- In this lab, Windows Firewall was enabled for all profiles and configured to block inbound connections by default.
- Keeping Windows updated and reviewing unnecessary sharing services helps reduce network risk.

- ## Skills Demonstrated

- Command-line troubleshooting
- Basic network session analysis
- Port and PID identification
- Windows Firewall verification
- Basic security risk assessment
