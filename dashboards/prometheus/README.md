# n8n System Health Overview Dashboard
Monitor your n8n workflow automation platform with this comprehensive Node.js runtime and application health dashboard for Grafana.

## Overview
This dashboard provides real-time monitoring of your n8n instance's health and performance metrics. It tracks CPU usage, memory consumption, heap allocation, garbage collection, event loop performance, and cluster status using n8n's native Prometheus metrics.
Perfect for production environments running self-hosted n8n instances.

![Dashboard Preview](./n8n-system-health-overview.png)

## Features
### Process & Instance Information
- **n8n Version** - Current n8n version running
- **Node.js Version** - Runtime version information
- **Instance Uptime** - Time since process started (with color-coded thresholds)
- **Leader Status** - Cluster role indicator (Leader/Follower)
- **Active Workflows** - Count of currently active workflows
### CPU & Event Loop Health
- **CPU Usage** - Total, user, and system CPU utilization breakdown
- **Event Loop Latency** - p50, p90, p99 percentiles for event loop lag detection
### Memory & Heap Usage
- **Memory (RSS)** - Resident set size memory usage
- **Heap Memory** - Dynamic heap allocation (used vs total)
- **Heap Percentage** - Current heap utilization gauge
### GC & Runtime Resources
- **GC Duration** - Minor and major garbage collection time
- **File Descriptors** - Open vs maximum file descriptor limits
## Prerequisites
- Grafana 8.0 or higher
- Prometheus datasource configured in Grafana
- n8n instance with Prometheus metrics endpoint enabled

## Installation
### 1. Enable n8n Metrics
Ensure your n8n instance has Prometheus metrics enabled. Add these environment variables:
```
N8N_METRICS=true  
```
Metrics will be available at `http://your-n8n-instance:5678/metrics`

### 2. Configure Prometheus
Add n8n as a scrape target in your `prometheus.yml`:
```
scrape_configs:  
  - job_name: 'n8n'  
    static_configs:  
      - targets: ['your-n8n-instance:5678']  
    metrics_path: '/metrics'  
    scrape_interval: 15s  
```

### 3. Import Dashboard
1. Download `n8n-system-health-overview.json` or Copy the dashboard JSON or use dashboard id `24474`
2. In Grafana, go to **Dashboards** → **Import**
3. Paste the JSON, upload the file or insert dashboard id
4. Select your Prometheus datasource
5. Click **Import**

## Metrics Used
This dashboard relies on these n8n Prometheus metrics:

|Metric|Description|
|---|---|
|`n8n_version_info`|Version information labels|
|`n8n_nodejs_version_info`|Node.js version labels|
|`n8n_process_start_time_seconds`|Process start timestamp|
|`n8n_instance_role_leader`|Cluster leader status (0/1)|
|`n8n_active_workflow_count`|Number of active workflows|
|`n8n_process_cpu_seconds_total`|Total CPU time|
|`n8n_process_cpu_user_seconds_total`|User CPU time|
|`n8n_process_cpu_system_seconds_total`|System CPU time|
|`n8n_nodejs_eventloop_lag_p*_seconds`|Event loop lag percentiles|
|`n8n_process_resident_memory_bytes`|RSS memory usage|
|`n8n_nodejs_heap_size_used_bytes`|Heap memory used|
|`n8n_nodejs_heap_size_total_bytes`|Total heap size|
|`n8n_nodejs_gc_duration_seconds_sum`|GC duration by type|
|`n8n_process_open_fds`|Open file descriptors|
|`n8n_process_max_fds`|Maximum file descriptors|

## Understanding the Metrics
### Heap Memory Behavior
**Important:** High heap percentage (80-95%) is **NORMAL** for Node.js applications! The Node.js V8 engine dynamically manages heap size and will expand it as needed.

⚠️ **Watch for these warning signs instead:**
- Heap total continuously growing over time
- Excessive garbage collection activity
- Sustained high memory (RSS) growth

### Event Loop Latency Thresholds
- **Green** (< 50ms) - Healthy
- **Yellow** (50-100ms) - Monitor
- **Orange** (100-150ms) - Investigate
- **Red** (> 150ms) - Action required

### CPU Usage Thresholds
- **Green** (< 70%) - Normal operation
- **Yellow** (70-85%) - Elevated
- **Orange** (85-95%) - High load
- **Red** (> 95%) - Critical

