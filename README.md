# grafana-n8n-dashboards

This repository provides two production-ready Grafana dashboards for monitoring self-hosted n8n environments.  
Together they cover system health (Prometheus) and workflow analytics (PostgreSQL).

## n8n Cloud or no Prometheus/database access?

Both dashboards need direct access to n8n's `/metrics` endpoint or its PostgreSQL database. n8n Cloud offers
neither. For n8n Cloud, or for self-hosted n8n without extra infrastructure, use the
[n8n data source plugin](https://grafana.com/grafana/plugins/nluecke-n8n-datasource/) instead:
it reads workflows, executions and Insights from the n8n public API with only a URL and an API key, and ships its own dashboard "n8n Workflow Executions (API)".

| Setup | Use |
| --- | --- |
| n8n Cloud | [n8n data source](https://grafana.com/grafana/plugins/nluecke-n8n-datasource/) |
| Self-hosted n8n, URL and API key only | [n8n data source](https://grafana.com/grafana/plugins/nluecke-n8n-datasource/) |
| Self-hosted n8n with Prometheus and/or PostgreSQL | The dashboards in this repository, optionally together with the plugin |

## Dashboards Included

### 1. n8n System Health Overview  
**Location:** `dashboards/prometheus/`  
**Datasource:** Prometheus  
Monitors Node.js runtime, CPU, memory, event loop performance, GC, and instance metadata.

### 2. n8n Workflow & Execution Analytics  
**Location:** `dashboards/postgresql/`  
**Datasource:** PostgreSQL  
Provides execution statistics, workflow quality insights, latency trends, queue depth, and error analysis.

## Structure
```
grafana-n8n-dashboards/
├── dashboards/
│   ├── prometheus/
│   │   ├── README.md
│   │   ├── n8n-system-health-overview.json
│   │   └── n8n-system-health-overview.png
│   └── postgresql/
│       ├── README.md
│       ├── n8n-workflow-execution-analytics.json
│       ├── n8n-workflow-execution-analytics-1.png
│       └── n8n-workflow-execution-analytics-2.png
├── provisioning/
│   ├── dashboards-prometheus.yaml
│   └── dashboards-db.yaml
└── LICENSE
```

## Import Options
Both dashboards can be imported via:
- JSON files (included in this repo)
- Grafana.com  
  - Prometheus dashboard ID: [**24474**](https://grafana.com/grafana/dashboards/24474)   
  - PostgreSQL dashboard ID: [**24475**](https://grafana.com/grafana/dashboards/24475) 

## License
This project is licensed under the MIT License.
