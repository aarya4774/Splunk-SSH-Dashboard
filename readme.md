# 🔐 SSH Login Monitoring Dashboard (Splunk)

## Overview

The **SSH Login Monitoring Dashboard** is a Splunk-based security monitoring solution designed to analyze SSH authentication logs and provide actionable insights into login activities. The dashboard helps security analysts quickly identify successful logins, failed authentication attempts, undetermined login events, and potentially suspicious login behavior.

This project demonstrates how Splunk can be used for Security Operations Center (SOC) monitoring by visualizing authentication data collected from SSH logs.

---

## Features

### Authentication Monitoring
- ✅ Successful SSH logins
- ❌ Failed SSH login attempts
- ⚠️ Undetermined/Unknown authentication events

### Suspicious Activity Detection
- Top source IP addresses generating login attempts
- Login attempts by IP address
- Multiple failed login attempts from the same IP
- Brute-force attack indicators
- High-frequency login attempts

### Dashboard Visualizations
- Login status distribution
- Successful vs Failed login trends
- Top attacking IP addresses
- Login count by source IP
- Event timeline
- Authentication statistics

---

## Dashboard Panels

| Panel | Description |
|-------|-------------|
| Successful Logins | Displays all successful SSH authentications |
| Failed Logins | Shows failed login attempts |
| Undetermined Logins | Displays authentication events that could not be classified |
| Login Status Overview | Pie/Bar chart of Success, Failed, and Undetermined logins |
| Top Source IPs | IP addresses with the highest number of login attempts |
| Login Count by IP | Number of authentication attempts from each source IP |
| Suspicious Login Activity | Detects repeated failed logins and abnormal behavior |
| Authentication Timeline | Login events over time |

<img width="2463" height="1299" alt="image" src="https://github.com/user-attachments/assets/3a2b9bb3-8eef-4f4d-a9eb-7b27dc411b86" />








---

## Log Source

The dashboard is built using SSH authentication logs collected from Linux systems.

Example log sources include:

- `/var/log/auth.log`
- `/var/log/secure`
- Syslog forwarded to Splunk
- Universal Forwarder

---

## Technologies Used

- Splunk Enterprise
- SPL (Search Processing Language)
- Linux SSH Authentication Logs
- Syslog
- Dashboard Studio / Classic Dashboards

---

## Sample Use Cases

- Detect brute-force SSH attacks
- Monitor authentication failures
- Identify compromised accounts
- Track login success rates
- Detect unusual login patterns
- Investigate suspicious IP activity
- SOC monitoring and incident response

---

## Example SPL Queries

### Successful Logins

```spl
index=ssh_logs "Accepted password"
```

### Failed Logins

```spl
index=ssh_logs "Failed password"
```

### Undetermined Logins

```spl
index=ssh_logs NOT ("Accepted password" OR "Failed password")
```

### Top Source IP Addresses

```spl
index=ssh_logs
| stats count by src_ip
| sort -count
```

### Suspicious Login Attempts

```spl
index=ssh_logs "Failed password"
| stats count by src_ip
| where count > 10
| sort -count
```

---

## Dashboard Benefits

- Real-time SSH authentication monitoring
- Quick identification of attack patterns
- Improved incident response
- Enhanced visibility into authentication events
- Easy detection of brute-force attempts
- SOC-friendly visualization

---

## Future Improvements

- Geo-location mapping of source IPs
- Threat intelligence integration
- Alerting for brute-force attacks
- User-based login analytics
- Impossible travel detection
- Risk scoring
- MITRE ATT&CK mapping
- Email and Slack alerts
- Machine learning-based anomaly detection

---

## Project Structure

```
SSH-Splunk-Dashboard/
│
├── README.md
├── dashboard.xml
├── savedsearches.conf
├── props.conf
├── transforms.conf
├── sample_logs/
│   └── ssh_logs.log
└── screenshots/
    ├── dashboard.png
    ├── login_summary.png
    └── suspicious_activity.png
```

---

## Dashboard Preview

The dashboard provides a centralized view of SSH authentication activity, enabling analysts to quickly monitor:

- Success vs Failure trends
- Suspicious login sources
- Top attacking IP addresses
- Authentication event distribution
- Login statistics over time

---

## Author

Developed as a cybersecurity monitoring project to demonstrate Splunk-based SSH authentication analysis and security event monitoring.
