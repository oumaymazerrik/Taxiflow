
# 🚕 TaxiFlow
### Real-Time Fleet Analytics and Demand-Aware Taxi Dispatch

**Intelligent Taxi Fleet Management, Demand Forecasting and Repositioning Platform**

**Master Big Data & Internet of Things — ENSAM Casablanca**

**Academic Project | 2026–2027**

---

## 📌 Project Overview

TaxiFlow is an academic project designed to improve urban taxi fleet management in Casablanca, Morocco.

The platform combines real-time taxi tracking, ride management, Big Data processing, demand forecasting, and intelligent vehicle repositioning.

The goal is to reduce passenger waiting times, minimize empty taxi movements, and improve fleet efficiency through data-driven decision-making.

The system will initially be developed and evaluated using simulated taxi fleets and publicly available transportation datasets.

## 🎯 Project Objectives

- Develop a taxi booking and ride management platform.
- Track taxi locations and availability in real time.
- Automatically propose rides to eligible drivers based on estimated pickup time.
- Process and analyze taxi GPS and ride events.
- Forecast taxi demand by geographical zone and time interval.
- Recommend proactive repositioning to available drivers.
- Integrate external road traffic information.
- Compare fleet performance with and without intelligent repositioning.

## 👥 System Actors

### 1. Client

- Register and log in.
- View nearby available taxis.
- Request a ride by specifying pickup and destination.
- Track ride status and driver location.
- Cancel a ride according to the management rules.
- Consult ride history.

### 2. Driver

- Manage availability and online status.
- Receive ride proposals.
- Accept or reject proposed rides.
- Update ride status.
- Share GPS location while online.
- View traffic information and taxi activity.
- Receive and optionally follow repositioning recommendations.

### 3. Administrator

- Manage drivers and vehicles.
- Monitor taxi positions and ride activity.
- Visualize demand distribution and predictions.
- Analyze fleet performance indicators.
- Configure and launch simulation scenarios.
- Compare different dispatch and repositioning strategies.
- Monitor data quality.
- Export reports.

## 🏗️ Proposed System Architecture

The architecture separates operational services from analytical processing.

### Operational Layer

- Client and Driver applications
- Administration dashboard
- REST API and WebSocket communication
- Ride management and dispatch
- GPS tracking
- Real-time notifications
- Routing and traffic integration

### Data Processing Layer

- MQTT for GPS data ingestion
- Apache Kafka for event streaming
- Apache Spark Structured Streaming for processing
- MinIO and Parquet for data storage
- Bronze, Silver and Gold data architecture

### Intelligence Layer

- Taxi demand forecasting
- Supply-demand analysis
- Intelligent repositioning recommendations
- Simulation-based strategy evaluation

### Infrastructure

- Docker Compose
- PostgreSQL/PostGIS
- Redis
- Apache Airflow
- MLflow
- Prometheus and Grafana

The initial development environment contains PostgreSQL/PostGIS, Redis and MQTT. Other components will be integrated progressively.

## 🛠️ Proposed Technology Stack

| Component | Technology |
|---|---|
| Client & Driver Applications | Flutter |
| Administration Dashboard | React, MapLibre GL JS |
| Backend API | Python, FastAPI |
| Relational Database | PostgreSQL, PostGIS |
| Real-Time State Management | Redis |
| IoT Messaging | MQTT, Eclipse Mosquitto |
| Event Streaming | Apache Kafka |
| Stream Processing | Apache Spark |
| Data Lake | MinIO, Parquet |
| Workflow Orchestration | Apache Airflow |
| Machine Learning | Scikit-learn, LightGBM |
| Experiment Tracking | MLflow |
| Geospatial Indexing | H3 |
| Mapping Data | OpenStreetMap |
| Routing | OSRM |
| Simulation | Python, SimPy, OSMnx |
| Monitoring | Prometheus, Grafana |
| Deployment | Docker Compose |
| Version Control | Git, GitHub |

These technologies represent the proposed architecture and will be integrated according to project milestones.

## 📊 Data Sources

TaxiFlow combines multiple data sources:

**1. OpenStreetMap**
- Road network
- Geographical information
- Routing and travel distances

**2. Public Taxi Datasets**
- NYC TLC Trip Record Data
- Chicago Taxi Trips
- Porto Taxi Trajectories

These datasets are candidates for demand forecasting and trajectory analysis. The final selection remains to be validated.

**3. Simulated Taxi Data**
- GPS coordinates
- Taxi availability
- Ride requests
- Ride status
- Driver decisions
- Vehicle movements

**4. External Traffic Data**
- Traffic conditions
- Estimated travel times
- Congestion information

The traffic provider will be selected based on coverage, cost, quotas and usage conditions.

## 🧠 Artificial Intelligence

### 1. Taxi Demand Forecasting

Predict the number of ride requests in each geographical zone.

Proposed configuration:

- Spatial representation: H3 hexagonal zones
- Time interval: 15 minutes
- Forecast horizon: 30 minutes
- Forecast update: every 15 minutes

**Forecasting models:**

- Historical average baseline
- Seasonal naive baseline
- LightGBM — proposed main model
- Spatio-temporal deep learning — optional extension

Forecasting models will be evaluated on public datasets using chronological validation.

Evaluation metrics include:

- MAE
- RMSE
- WAPE

### 2. Automatic Taxi Dispatch

The initial dispatch strategy selects eligible drivers based on the shortest estimated pickup time.

The process includes:

1. Receive a ride request.
2. Identify available nearby drivers.
3. Estimate travel times.
4. Rank eligible drivers.
5. Send a proposal to the selected driver.
6. Handle acceptance, rejection or expiration.
7. Retry when necessary.

Drivers remain free to accept or reject proposed rides.

Initial parameters, subject to validation:

- Response timeout: 15 seconds
- Maximum attempts: 3
- Search timeout: 2 minutes
- Initial search radius: 3 km
- Extended search radius: 5 km

### 3. Intelligent Taxi Repositioning

The system identifies zones where predicted demand exceeds expected taxi supply.

Available drivers may receive recommendations to move toward those zones.

The proposed method uses minimum-cost assignment, with the Hungarian algorithm, to minimize estimated repositioning travel time.

Repositioning recommendations are optional for drivers.

**Evaluation strategies:**

- S0: No repositioning
- S1: Simple heuristic repositioning
- S2: Proposed optimization-based repositioning

The evaluation compares waiting times, service rates and empty travel distances across reproducible simulations.

## 📈 Key Performance Indicators

TaxiFlow will evaluate:

- Average passenger waiting time
- Ride search time
- Ride service rate
- Driver acceptance rate
- Empty travel distance and time
- Demand forecasting accuracy
- Estimated versus observed travel times
- Data quality indicators
- System response latency

## 🗂️ Repository Structure

```text
taxiflow/
│
├── apps/
│   ├── mobile/          # Client and Driver applications
│   └── admin-web/       # Administration dashboard
│
├── backend/             # FastAPI backend services
│
├── core/                # Shared business logic and rules
│
├── simulator/           # Fleet and demand simulation
│
├── pipelines/           # Streaming and batch data pipelines
│
├── ml/                  # Demand forecasting models
│
├── schemas/             # Event schemas
│
├── experiments/         # Simulation experiments
│
├── infra/               # Docker and infrastructure
│
├── scripts/             # Setup and utility scripts
│
├── docs/                # Project documentation
│
├── .github/             # CI and collaboration templates
│
├── CONTRIBUTING.md
├── requirements-dev.txt
└── README.md
```

## 🚀 Getting Started

### Prerequisites

- Git
- Python 3.12
- Docker Desktop
- VS Code or another IDE

### Clone the Repository

```bash
git clone https://github.com/oumaymazerrik/Taxiflow.git
cd Taxiflow
```

### Configure Environment

Create a local `.env` file from the example:

```bash
cp .env.example .env
```

For Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

### Start Initial Services

```bash
docker compose -f infra/docker-compose.yml --env-file .env up -d
```

The starter configuration includes:

- PostgreSQL/PostGIS
- Redis
- Eclipse Mosquitto

### Install Python Dependencies

```bash
python -m venv .venv
```

Activate the environment.

Linux/macOS:

```bash
source .venv/bin/activate
```

Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Install dependencies:

```bash
pip install -r requirements-dev.txt
```

### Run Tests

```bash
pytest
```

The starter project includes 22 tests covering initial business rules, course states and event schemas.

## 📅 Project Roadmap

| Phase | Period | Deliverable |
|---|---|---|
| 1. Project Scoping | Weeks 1–2 | Validated requirements and initial design |
| 2. Core Implementation | Weeks 3–6 | Simulated ride demonstration |
| 3. Real-Time Data | Weeks 6–9 | GPS tracking and historical data |
| 4. Demand Forecasting | Weeks 9–11 | Evaluated forecasting models |
| 5. Repositioning | Weeks 11–13 | Comparative simulation results |
| 6. Final Integration | Weeks 13–16 | Traffic integration, testing and final report |

The schedule is provisional and will be adapted to the academic calendar.

## 🤝 Collaboration Workflow

Development follows an issue-based GitHub workflow.

1. Create or assign an issue.
2. Create a dedicated feature branch.
3. Implement and test the feature.
4. Open a Pull Request.
5. Request code review.
6. Merge after approval and successful CI checks.

Direct commits to the `main` branch are not permitted under the proposed workflow.

Detailed guidelines are available in [CONTRIBUTING.md](CONTRIBUTING.md).

## 📚 Reference Documents

The `docs/` directory contains the official project reference documents:

- TaxiFlow Cahier des Charges V2
- TaxiFlow Conception Fonctionnelle V2
- TaxiFlow Dossier de Conception
- TaxiFlow Organisation GitHub
- Project Decision Log

The functional design V2 is the reference for expected system behavior, while the technical design provides the proposed implementation architecture.

## 🔒 Privacy and Data Protection

TaxiFlow is initially an academic prototype using simulated and publicly available data.

Any future processing of real personal data must respect Moroccan Law 09-08 and applicable CNDP requirements.

## 📌 Project Status

**Current phase: Project setup and initial implementation**

The repository starts from the project skeleton provided by the academic supervisor.

The complete platform, AI modules and advanced real-time pipelines remain under development.

## 🎓 Academic Context

**Project:** TaxiFlow

**Program:** Master Big Data & Internet of Things

**Institution:** ENSAM Casablanca, Morocco

**Academic Year:** 2026–2027

**Project Type:** Projet Métier M2

**Academic Supervisor:** Prof. Aissam Jadli

**Development Team:** Oumayma Zerrik & Hala

---

*TaxiFlow — Data-driven urban mobility through Big Data, IoT and Artificial Intelligence.*
