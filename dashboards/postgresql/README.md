# n8n Workflow & Execution Analytics Dashboard
A comprehensive Grafana dashboard for monitoring and analyzing n8n workflow automation platform performance, execution metrics, and workflow quality.

## Overview
This dashboard provides deep insights into your n8n workflows and executions, helping you track performance, identify bottlenecks, monitor success rates, and optimize your automation workflows. It connects directly to your n8n PostgreSQL database to provide real-time analytics.

**Perfect companion to the [n8n System Health Overview Dashboard](https://github.com/nluecke/grafana-n8n-dashboards/tree/main/dashboards/prometheus)** - while System Health monitors Node.js runtime metrics, this dashboard focuses on workflow execution analytics and business metrics.

## Features
### Executive Summary
- **Total Workflows**: Complete workflow inventory
- **Active Workflows**: Currently enabled workflows
- **Total Executions**: Execution count in selected time range
- **Success Rate**: Percentage of successful executions with health indicators
- **Failed Executions**: Error and crash tracking
- **Currently Running**: Live execution monitoring

### Execution Performance Trends
- **Executions Over Time by Status**: Visual timeline of success/error/crashed executions
- **Execution Duration Percentiles**: P50, P95, P99 latency tracking over time
- **P95, Max, Avg & Median Duration (24h)**: Performance snapshot metrics

### Workflow Quality Insights
- **Most Executed Workflows**: Top workflows by execution count with success rates
- **Daily Success Rate Trend**: 7-day success rate visualization
- **Workflows with Most Failures**: Identify problematic workflows
- **Slowest Workflows**: Performance bottleneck identification by average duration

### Resource & Queue Management
- **Execution Queue Depth**: Monitor queued and running executions over time
- **Current Execution Queue**: Real-time view of pending workflows
- **Long Running Executions**: Identify potentially stuck workflows
- **Recently Updated Workflows**: Track workflow changes
- **Workflows by Tags**: Category-based workflow organization
- **Recent Execution Errors**: Detailed error log with timing

## Requirements
### Software Requirements
- **Grafana**: v9.0+ (tested with v12.3+)
- **n8n**: Any version with PostgreSQL database backend
- **PostgreSQL**: v12+ (n8n database)

### Grafana Plugins
- PostgreSQL datasource (built-in)

### Database Access
- Read-only access to n8n PostgreSQL database
- Required tables:  
    - `workflow_entity`
    - `execution_entity`
    - `tag_entity`
    - `workflows_tags` (join table)

## Installation
### 1. Configure PostgreSQL Datasource

In Grafana, add a new PostgreSQL datasource:
1. Navigate to **Configuration** → **Data Sources** → **Add data source**
2. Select **PostgreSQL**
3. Configure connection settings:
```
   Host: your-n8n-database-host:5432  
   Database: n8n  
   User: grafana_readonly (or your read-only user)  
   Password: your-password  
   SSL Mode: require (recommended for production)  
   
```
4. Test the connection
5. Save the datasource and note the **UID** (e.g., `bf4plhy8zn8xsd`)

### 2. Import Dashboard

#### Option A: Import from JSON
1. Download or copy content from `n8n-workflow-execution-analytics.json` from this repository
2. In Grafana, navigate to **Dashboards** → **Import**
3. Upload the JSON file or paste the JSON content
4. Select your PostgreSQL datasource
5. Click **Import**

#### Option B: Import from Grafana.com
1. In Grafana, navigate to **Dashboards** → **Import**
2. Enter dashboard ID: `[24475]` 
3. Select your PostgreSQL datasource
4. Click **Import**

### 3. Configure Time Macros

The dashboard uses Grafana's time macros (`$__timeFilter`, `$__timeGroupAlias`) which automatically work with your selected time range. No additional configuration needed.

## Dashboard Sections Explained

### Executive Summary
Provides instant visibility into your n8n instance health with key performance indicators. Color-coded thresholds help quickly identify issues:

- 🔵 Blue: Informational metrics
- 🟢 Green: Healthy state
- 🟡 Yellow: Warning threshold
- 🔴 Red: Critical threshold

### Performance Metrics

Track execution performance over time to identify trends, spikes, or degradation:
- **Duration percentiles** help understand latency distribution
- **P95 tracking** catches outliers that affect user experience
- **Time-series visualization** reveals patterns and anomalies

### Workflow Analysis Tables

Sortable tables provide detailed workflow analytics:
- Click column headers to sort by different metrics
- Use for identifying optimization opportunities
- Export data for further analysis

### Queue Management

Monitor execution queuing and resource utilization:
- Identify backlog buildup
- Detect long-running or stuck executions
- Optimize worker capacity planning
