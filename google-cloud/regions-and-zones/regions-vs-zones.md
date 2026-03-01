# Regions vs Zones

## Region

- **Definition**: A separate geographic area (e.g. London, Mumbai)
- **Distance**: Regions are separated by large geographic distances
- **Failure Scope**: Deploying in multiple regions protects against massive disasters (earthquakes, floods) affecting a whole region
- **Primary Goal**: Disaster Recovery, Data Residency, Low Latency for global users

## Zone/AZ

- **Definition**: An isolated location within a region
- **Distance**: Zones are connected by ultra-low latency links within the same region
- **Failure Scope**: Deploying in multiple zones in a region protects against local failures (power outage, fire) in a specific building
- **Primary Goal**: High Availability within the same region
