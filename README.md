# Local Speedtest
A turnkey speed test and connectivity check utility that uses `iperf`. It runs on macOS and Linux.

Run it as a listener/server on one system, then run it as a client on another. Automatically probes available connectivity and provides the commands to use to test connectivity and speed.

Supports TCP and UDP, and will check for available Tailscale tailnet connections.

## Suggestions
Copy `local-speedtest` to a folder in your path such as `/usr/local/bin` and call via the comamnd line. On the initial run it will start an `iperf` daemon in the background as a listener.

If you wish to shut down the daemon:

```bash
pkill iperf3
```

### Run the `iperf` listener daemon automatically after a reboot

On Linux:
```bash
crontab -e
```

Add a line like:
```cron
@reboot		chronic iperf3 -D -i1 -s -p 25002
```

On a Synology DSM and other POSIX-like systems:
```bash
sudo nano /etc/crontab
```

Add a line like:
```cron
@reboot					root	iperf3 -D -i1 -s -p 25002 > /dev/null
```
Make sure to keep *tabs* intact on Synology DSM, using spaces can fully break `cron`!