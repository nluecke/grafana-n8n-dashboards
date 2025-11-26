# grafana-n8n-dashboards

This repository provides two production-ready Grafana dashboards for monitoring self-hosted n8n environments.  
Together they cover system health (Prometheus) and workflow analytics (PostgreSQL).

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
n8n-grafana-dashboards/
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
  - Prometheus dashboard ID: [**24475**](https://grafana.com/grafana/dashboards/24475) 

## License
This project is licensed under the MIT License.
