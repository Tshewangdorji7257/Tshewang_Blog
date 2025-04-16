---
title: Nmap Performance
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Nmap
draft: false
---

# Nmap Performance Optimization

## Key Performance Parameters
| Parameter | Description | Example |
|-----------|-------------|---------|
| `-T<0-5>` | Timing template (0=slowest, 5=fastest) | `-T4` |
| `--min-parallelism` | Minimum parallel probes | `--min-parallelism 50` |
| `--max-rtt-timeout` | Maximum round-trip time | `--max-rtt-timeout 100ms` |
| `--min-rate` | Minimum packets per second | `--min-rate 300` |
| `--max-retries` | Maximum port scan retries | `--max-retries 2` |

## Timing Templates
| Level | Name | Description |
|-------|------|-------------|
| 0 | Paranoid | Very slow, IDS evasion |
| 1 | Sneaky | Slow, stealthy |
| 2 | Polite | Slower, less intrusive |
| 3 | Normal | Default balanced speed |
| 4 | Aggressive | Faster, more intrusive |
| 5 | Insane | Very fast, likely to be detected |

## Optimization Examples

### RTT Timeout Adjustment
```bash
# Default scan (100ms timeout)
nmap 10.129.2.0/24 -F  # 39.44 seconds

# Optimized timeout
nmap 10.129.2.0/24 -F --initial-rtt-timeout 50ms --max-rtt-timeout 100ms  # 12.29 seconds
```
**Trade-off:** Faster scans may miss some hosts/ports

### Retry Reduction
```bash
nmap 10.129.2.0/24 -F --max-retries 0
```
**Effect:** Reduces accuracy but significantly speeds up scans

### Packet Rate Control
```bash
nmap 10.129.2.0/24 -F --min-rate 300  # Completes in 8.67s vs default 29.83s
```
**Best for:** Whitelisted environments with known bandwidth

### Timing Template Usage
```bash
nmap 10.129.2.0/24 -F -T5  # "Insane" template completes in 18.07s
```

## Performance vs Accuracy
| Optimization | Speed Gain | Accuracy Impact |
|--------------|-----------|-----------------|
| Reduced RTT | +++ | May miss slow hosts |
| Zero retries | ++ | May miss filtered ports |
| High min-rate | ++++ | Minimal if bandwidth available |
| Aggressive timing | ++ | May trigger IDS |

## Best Practices
1. Start with default (`-T3`) for unknown networks
2. Use aggressive (`-T4`) for internal/whitelisted scans
3. Adjust timeouts based on observed network latency
4. Balance speed with accuracy needs
5. Log results (`-oN`) to compare different approaches
