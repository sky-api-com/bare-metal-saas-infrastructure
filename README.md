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
- Nomad workers for scheduling docker containers

### Certificates
Generate certificates with Letsencrypt using Cloudflare DNS chalenge and put them into Hashicorp vault.

### Logs storage
WIP

### Instance manager
Adds, stops, resumes and removes instances on workers cluster. 

### MySQL Database
WIP
Candidates: database for every 10 instances or vitess.

## Hardware

- Bare metal cluster for worker nodes. 
- A set of vm's as master nodes

## Roadmap

1) Generate and store certificates in Vault. Apply certificates on existing API.
2) Run workloads on nomad servers, including persistance on bare-metal. Deploy and update cluster automatically. 