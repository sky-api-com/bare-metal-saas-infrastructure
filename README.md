# Bare metal SaaS service infrastructure

For those who can't afford to pay $100k/month AWS bill.

## Components

### Service discovery
Consul for service discovery. Standalone 3-node master cluster and worker on every machine.

### API Geteway and router
Every request comes to an API router. API Router is a docker container, with access to consul worker. It redirects every request into apropriate host and port. API router source code is side-loaded.

### Worker nodes
Bare metal servers. Consists of: 
- Consul worker for registering containers
- 

### Certificates
Generate certificates with Letsencrypt using Cloudflare DNS chalenge and put them into Hashicorp vault.

### Logs storage
WIP

### MySQL Database
WIP
Candidates: database for every 10 instances or vitess.

## Hardware

Everything runs on Hetzner cloud except for Worker nodes. Worker nodes run bare metal.