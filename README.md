# Automated-Network-IP-Monitoring-Downtime-Logging-System.

🔍 Key Functional Insights
Purpose:

The script monitors the network connectivity of multiple IP addresses.

Logs their status (Up/Down) and downtime duration.

Helps IT teams to proactively handle outages and maintain system reliability.

Monitoring Process:

Uses Python’s subprocess to ping each IP every 1 second for a total of 60 seconds.

Captures response status (Reply from) and response time (time=).

If an IP is down, calculates how long it's been down based on historical logs.

Data Storage:

Writes results to two SQL Server tables:

ip_ping_status → detailed logs.

live_ping_status → current live status.

PingResponse table logs timestamped response time for each IP.

Downtime Calculation:

Looks back into the last "Up" record or first "Down" record to calculate downtime.

Converts it into human-readable format (e.g., 0 days 00:03:22).

Alert Mechanism:

If the script fails, it sends an error email via Outlook to the IT team (NVTI.IT@nvtpower.com).

DataFrame Usage:

Uses Pandas extensively for reading/writing SQL data, transforming logs, and creating cumulative downtime metrics.

📊 Operational Insights
Live Downtime Counter:

Maintains a cumulative count of 'Down' events per IP using cumsum() logic.

Provides a quick metric to identify which IPs are most frequently down.

Dynamic Column Handling:

Automatically adds new IP columns to the PingResponse table if they don't exist.

Makes the system scalable for more IPs without manual schema updates.

System Feedback:

Status logs, downtime, and counters give a complete picture of network health.

⚠️ Potential Areas for Improvement
Scalability:

Hardcoded running_time = 60 and interval = 1. Could be configurable.

May not scale well with hundreds of IPs due to performance.

Ping Optimization:

Each IP is pinged twice per loop (once for Up/Down, once for response time). You can optimize to ping only once and parse both data from the same result.

Security:

Database credentials are hardcoded (though redacted here). It's better to use environment variables or a secrets manager.

Logging:

Consider logging all events (success/failure) into a log file using the logging module for better debugging.

🧠 Possible Use Cases
Real-time IP/device uptime monitoring dashboard.

Network health reports for IT infrastructure teams.

Automated alerting system for downtime escalation.

Useful for SMEs and internal IT departments in industries relying on local infrastructure (e.g., manufacturing, logistics).
