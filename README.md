SDV Middleware & Telemetry Simulator

A full-stack Software-Defined Vehicle (SDV) middleware and telemetry simulator built with C++, Python, MQTT, SQLite, Supabase, Docker, and Streamlit.

## Architecture

```
+--------------------------------------------------+
|  C++ Sensor Simulator                            |
|  - Vehicle physics model                         |
|  - 10 sensor types (speed, RPM, temp, GPS, etc.) |
|  - Publishes JSON telemetry frames via MQTT      |
+--------------------------------------------------+
                          |
                          v
+--------------------------------------------------+
|  Eclipse Mosquitto (MQTT Broker)                 |
+--------------------------------------------------+
                          |
                          v
+--------------------------------------------------+
|  Python Telemetry Collector                      |
|  - Subscribes to MQTT topics                     |
|  - Stores data in SQLite (edge)                  |
|  - Forwards to Supabase (cloud)                  |
+--------------------------------------------------+
                          |
          +---------------+---------------+
          |                               |
          v                               v
+--------------------------------------------------+
|  SQLite (Local)                       |  Supabase |
|  - telemetry_frames                   |  (Cloud)  |
|  - sensor_readings                    |           |
+--------------------------------------------------+
                          |
                          v
+--------------------------------------------------+
|  Streamlit Dashboard                             |
|  - Real-time gauges and charts                   |
|  - Historical analytics                          |
|  - Vehicle health metrics                        |
+--------------------------------------------------+
```

## Quick Start

### Prerequisites
- Docker & Docker Compose

### Run All Services

```bash
docker-compose up --build
```

Services:
- MQTT Broker: `localhost:1883`
- Streamlit Dashboard: `http://localhost:8501`

### Components

| Service | Tech | Description |
|---------|------|-------------|
| Sensor Simulator | C++17 | Generates realistic vehicle sensor data |
| MQTT Broker | Mosquitto | Message pub/sub backbone |
| Telemetry Collector | Python 3.11 | Ingests, stores, forwards data |
| Edge Storage | SQLite | Local persistent cache |
| Cloud Storage | Supabase | Remote telemetry warehouse |
| Dashboard | Streamlit | Real-time visualization |

### Sensor Types
- Speed (km/h)
- Engine RPM
- Engine Temperature (C)
- Battery Voltage (V)
- Battery SOC (%)
- Fuel Level (%)
- GPS (lat, lon)
- Accelerometer (g)
- Brake Status
- Gear Position

## Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `MQTT_BROKER` | `localhost` | MQTT broker hostname |
| `MQTT_PORT` | `1883` | MQTT broker port |
| `VEHICLE_ID` | `VEH-001` | Simulated vehicle identifier |
| `SIMULATION_RATE_HZ` | `10` | Telemetry publish frequency |
| `SQLITE_DB` | `/data/telemetry.db` | SQLite database path |
| `SUPABASE_URL` | - | Supabase project URL |
| `SUPABASE_ANON_KEY` | - | Supabase anon key |
