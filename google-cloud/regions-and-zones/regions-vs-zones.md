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

## Common misconceptions

> [!NOTE]
> **Misconception**: Regions are only for large enterprises
>
> **Reality**: Cloud makes regions accessible even to startups

> [!NOTE]
> **Misconception**: All regions cost the same
>
> **Reality**: Costs vary from region to region - based on local taxes and costs of running a data center in that specific region

> [!NOTE]
> **Misconception**: Using one zone is enough for high availability
>
> **Reality**: Zone failure can still bring apps down

> [!NOTE]
> **Misconception**: All regions have same number of zones
>
> **Reality**: Number of zones can vary by region

> [!NOTE]
> **Misconception**: All zones have just one data center
>
> **Reality**: No - Some zones can have more than one data centers
