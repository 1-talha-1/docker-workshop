# 

<div style="text-align: center; margin-top: 25%;">

# Comprehensive Docker & Containerization Workshop Manual

## Technical Training Program

![Workshop Logo](/home/magician/Downloads/image.svg)

*Prepared by:*

**Dr Sohail Khan**

**Talha**

**Shahriyar Choudhry**

</div>



<div style="page-break-after: always;"></div>

<div style="padding: 20px;">

# Table of Contents

<div style="border-left: 4px solid #0078D7; padding-left: 15px;">

#### [1. Workshop Overview](#workshop-overview)

#### [2. Pre-requisites and Setup](#pre-requisites-and-setup)

#### [3. Day 1: Containerization Foundations & Docker Essentials](#day-1-containerization-foundations--docker-essentials)

#### [4. Day 2: Container Customization & Document Analysis System Implementation](#day-2-container-customization--document-analysis-system-implementation)

#### [5. Day 3: Multi-Container Orchestration & Production Deployment](#day-3-multi-container-orchestration--production-deployment)

#### [6. Command Reference](#command-reference)

#### [7. Troubleshooting Guide](#troubleshooting-guide)

#### [8. Best Practices](#best-practices)

#### [9. Additional Resources](#additional-resources)

</div>

</div>

<div style="page-break-after: always;"></div>

## Workshop Overview

This comprehensive Docker & Containerization Workshop is designed to provide IT professionals with the knowledge and skills necessary to effectively implement containerization strategies within enterprise environments. The training program follows a structured learning path that progresses from fundamental containerization concepts to advanced Docker implementation techniques.

### Workshop Focus

The workshop addresses key containerization areas critical for modern IT infrastructure:

- **Containerization Fundamentals**: Understanding the architectural advantages of containers over traditional virtualization, container isolation principles, and the Docker ecosystem architecture.

- **Docker Implementation**: Mastering Docker installation, configuration, container management, image creation, and registry operations in enterprise environments.

- **Multi-Container Applications**: Designing and implementing complex multi-container architectures with appropriate networking, data persistence, and service discovery patterns.

- **Security & Best Practices**: Implementing comprehensive security measures, applying least privilege principles, and following industry best practices for containerized applications.

- **Production Readiness**: Deploying containerized applications in production with proper monitoring, scaling, high availability, and CI/CD integration.

### Learning Outcome

By the conclusion of this workshop, participants will be able to:

- Design and implement efficient containerization strategies
- Create optimized Docker images using best practices
- Manage container lifecycle, networking, and persistent storage
- Orchestrate multi-container applications with Docker Compose
- Implement comprehensive security measures for containers
- Deploy containerized applications in production environments
- Troubleshoot common containerization issues
- Integrate containers with modern CI/CD pipelines

This workshop provides both theoretical knowledge and practical implementation skills, with numerous hands-on exercises reinforcing concepts throughout the training program. Participants will gain expertise applicable to various enterprise containerization scenarios, supporting digital transformation initiatives.

<div style="page-break-after: always;"></div>

## Pre-requisites and Setup

### System Requirements

- Computer with at least 8GB RAM, 4+ CPU cores
- 50GB free disk space
- Administrator/sudo privileges
- Internet connection for downloading Docker and images

### Software Installation

Prior to the workshop, please install:

1. **Docker Installation**
   
   - **Windows**: Docker Desktop for Windows
   - **macOS**: Docker Desktop for Mac
   - **Linux**: Docker Engine
   
   Follow the official installation guide: https://docs.docker.com/engine/install/

2. **Docker Compose Installation**
   
   - Included with Docker Desktop for Windows/Mac
   - Linux: Follow https://docs.docker.com/compose/install/

3. **Code Editor**
   
   - Visual Studio Code (recommended): https://code.visualstudio.com/
   - With Docker extension installed

4. **Git Client**
   
   - https://git-scm.com/downloads

### Verifying Installation

Run these commands to verify your installation:

```bash
docker --version
docker-compose --version
docker run hello-world
```

<br>

### Workshop Repository

Clone the workshop repository:

```bash
git clone https://github.com/1-talha-1/docker-workshop.git
cd docker-workshop
```

<div style="page-break-after: always;"></div>

## Day 1: Containerization Foundations & Docker Essentials

### MODULE 1: VIRTUALIZATION TO CONTAINERIZATION TRANSITION

#### 1.1 Evolution of Infrastructure Virtualization

**Traditional Physical Infrastructure Challenges**

- Hardware provisioning delays and high capital expenditure
- Resource underutilization (typical server utilization: 10-15%)
- Environmental impact and data center costs

**Virtual Machine Architecture**

- Hypervisor types (Type 1 vs Type 2) and their overhead
- Guest OS resource requirements (typical VM overhead: 1-2 GB RAM per instance)
- Limited portability due to hypervisor dependencies
- Hardware-level emulation and its performance implications

**Containerization Breakthrough**

- Kernel-level virtualization fundamentals (cgroups, namespaces, UnionFS)
- Container runtime efficiency (startup time: <1s vs 30-60s for VMs)
- Resource footprint comparison (10-100MB vs 1-10GB for VMs)
- The OCI (Open Container Initiative) standards

**Hands-on Exercise 1.1: VM vs Container Comparison**

1. Start a virtual machine with Ubuntu
2. Start a Docker container with Ubuntu
3. Compare resource usage (RAM, CPU)
4. Compare startup times
5. Run identical workloads and measure performance

#### 1.2 Docker Ecosystem Architecture

**Foundational Components**

- Docker Engine internal architecture (daemon, containerd, runc)
- Docker client-server communication model
- Registry infrastructure (Docker Hub, private registries)
- BuildKit and image creation pipeline

**Core Technical Concepts**

- Image layering and the Copy-on-Write mechanism
- Container lifecycle and state management
- Isolation boundaries and security considerations
- Docker's networking subsystem overview

**Docker vs. Alternative Container Runtimes**

- Comparison with Podman, LXC, containerd
- Kubernetes container runtime interface (CRI)
- Selection criteria for production environments

#### 1.3 Enterprise Adoption Case Study: Financial Services Sector

**Containerization Impact Metrics**

- Deployment frequency increases (case study: from biweekly to daily)
- Resource utilization improvements (50-70% reduction in infrastructure costs)
- Application startup time reductions (minutes to seconds)

**Architecture Transformation Journey**

- Monolith to microservices transition methodology
- Incremental containerization strategies
- Cultural and organizational challenges

**NADRA-Specific Applications**

- Document processing pipeline opportunities
- Identity verification system modernization
- Database services containerization strategy

<div style="page-break-after: always;"></div>

### MODULE 2: DOCKER INSTALLATION & CONFIGURATION DEEP DIVE

#### 2.1 Docker Deployment Architecture Options

**Docker Desktop vs. Engine Comparison**

- Component analysis: Docker Engine, CLI, Buildx, Compose
- Platform-specific internals (LinuxKit/HyperV/Hyperkit)
- Resource allocation and performance tuning

**Production Installation Planning**

- Operating system selection criteria (RHEL, Ubuntu, Windows Server)
- Docker Enterprise Edition features and licensing
- High-availability Docker daemon configuration

**Infrastructure Prerequisites**

- Kernel version requirements and compatibility
- Storage driver selection guidelines
- Network prerequisites and considerations

<div style="page-break-after: always;"></div>

#### 2.2 Step-by-Step Enterprise Installation

**Linux-based Installation**

```bash
# Add Docker's official GPG key
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker Engine
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

**Windows Server Deployment**

- Windows container vs Linux container modes
- Feature activation requirements
- Integration with Windows authentication systems

**Configuration Best Practices**

- daemon.json configuration deep dive
- Log rotation and storage setup
- Proxy and registry configuration
- Resource constraint implementation

<div style="page-break-after: always;"></div>

#### 2.3 Docker Architecture Validation & Troubleshooting

**Installation Verification Procedure**

```bash
# Verify Docker is running
sudo systemctl status docker

# Run test container
sudo docker run hello-world

# Check Docker info
sudo docker info
```

**Common Installation Issues**

- Permission and user group configuration
- Kernel parameter requirements
- Firewall and SELinux/AppArmor configuration

**Performance Tuning**

- Storage driver optimization (overlay2 vs devicemapper)
- Daemon thread and connection settings
- Resource control with cgroups

**Hands-on Exercise 2.1: Enterprise Docker Installation**

1. Install Docker CE on lab environment
2. Configure non-root user access
3. Set up custom daemon.json configuration
4. Implement log rotation
5. Test installation with hello-world container

**Hands-on Exercise 2.2: Docker Environment Validation**

1. Run container runtime verification tests
2. Test registry connectivity
3. Measure baseline performance

### 

<div style="page-break-after: always;"></div>

### MODULE 3: DOCKER CONTAINER FUNDAMENTALS

#### 3.1 Container Lifecycle Deep Dive

**Container States and Transitions**

- Created, Running, Paused, Stopped, Deleted states
- Exit codes and troubleshooting implications
- Container restart policies and their applications

**Essential Container Operations**

```bash
# Create and start a container
docker run -d --name webserver nginx

# List running containers
docker ps

# Stop a container
docker stop webserver

# Start a stopped container
docker start webserver

# Remove a container
docker rm webserver
```

**Container Resource Management**

```bash
# Set memory limits
docker run -d --name db --memory=1g --memory-reservation=750m postgres

# Set CPU limits
docker run -d --name app --cpus=0.5 --cpu-shares=512 nginx

# Set I/O limits
docker run -d --name backup --device-write-bps /dev/sda:10mb ubuntu
```

<div style="page-break-after: always;"></div>

#### 3.2 Container Shell Interaction Techniques

**Interactive Container Management**

```bash
# Attach to container's main process
docker attach container_name

# Execute a command in a running container
docker exec -it container_name bash

# Send a signal to a container
docker kill --signal=SIGTERM container_name
```

**Environment Configuration**

```bash
# Set environment variables
docker run -e VAR1=value1 -e VAR2=value2 image_name

# Use environment file
docker run --env-file=config.env image_name
```

**Debugging Techniques**

```bash
# Check processes in container
docker top container_name

# Inspect container details
docker inspect container_name

# View container logs
docker logs -f container_name
```

<div style="page-break-after: always;"></div>

#### 3.3 Container Monitoring and Health Management

**Built-in Monitoring Tools**

```bash
# View real-time container stats
docker stats

# View container events
docker events

# Configure health checks
docker run --health-cmd="curl -f http://localhost/ || exit 1" \
          --health-interval=30s \
          --health-timeout=3s \
          --health-retries=3 \
          --health-start-period=5s \
          nginx
```

**External Monitoring Integration**

- Prometheus metrics exposure
- cAdvisor deployment for detailed metrics
- Log aggregation strategies (fluentd, logstash)

**Proactive Container Management**

- Automated restart strategies
- Resource utilization alerting
- Container garbage collection policies

**Hands-on Exercise 3.1: Container Lifecycle Management**

1. Create containers with different configurations
2. Explore lifecycle states and transitions
3. Implement restart policies
4. Test volume data persistence

**Hands-on Exercise 3.2: Container Resource Management**

1. Set memory and CPU constraints
2. Monitor resource usage under load
3. Implement and test I/O throttling
4. Observe and resolve resource constraint issues

### 

<div style="page-break-after: always;"></div>

### MODULE 4: DOCKER IMAGES & REGISTRIES

#### 4.1 Docker Image Architecture

**Image Internals**

- Layer structure and content-addressable storage
- Manifest and config file specifications
- Tag versioning strategies (semantic versioning, immutable tags)

**Image Size Optimization**

- Base image selection criteria
- Multi-stage build introduction
- Layer optimization techniques

**Image Inspection and Analysis**

```bash
# View image history
docker history image_name

# Inspect image details
docker inspect image_name

# Scan image for vulnerabilities
docker scout cves image_name
```

#### 4.2 Docker Registry Ecosystem

**Registry Types and Selection**

- Public registries (Docker Hub, Amazon ECR, Google GCR)
- Private registry deployment options
- Air-gapped environments strategy

**Docker Hub Deep Dive**

- Official images vs community images
- Automated builds and webhooks
- Rate limits and pull policies

**Registry Security Best Practices**

- Authentication methods (basic auth, LDAP, OAuth)
- Transport layer security implementation
- Content trust and image signing

#### 4.3 Image Management Workflow

**Enterprise Image Strategy**

- Base image standardization
- Tagging conventions and policies
- Promotion workflows across environments

**Image Cleanup and Maintenance**

```bash
# Remove unused images
docker image prune

# Remove all unused objects
docker system prune -a

# Remove dangling images
docker image prune -f
```

**Hands-on Exercise 4.1: Registry Management**

1. Authenticate with Docker Hub
2. Pull and tag images
3. Push to your repository
4. Configure and test image signing with Docker Content Trust

**Hands-on Exercise 4.2: Image Analysis**

1. Analyze image layers with docker history
2. Scan images for vulnerabilities
3. Identify optimization opportunities

<div style="page-break-after: always;"></div>

## Day 2: Container Customization & Document Analysis System Implementation

### MODULE 5: DOCKERFILE MASTERY & IMAGE CREATION

#### 5.1 Dockerfile Instruction Set Deep Dive

**Base Instructions Analysis**

```dockerfile
FROM ubuntu:22.04
LABEL maintainer="example@nadra.gov.pk"
ARG VERSION=latest
ENV APP_HOME=/app
```

**Filesystem Instructions**

```dockerfile
WORKDIR /app
COPY src/ /app/src/
ADD http://example.com/file.tar.gz /tmp/
VOLUME /data
```

**Execution Instructions**

```dockerfile
RUN apt-get update && apt-get install -y package
CMD ["executable", "param1", "param2"]
ENTRYPOINT ["nginx", "-g", "daemon off;"]
HEALTHCHECK --interval=30s --timeout=3s CMD curl -f http://localhost/ || exit 1
USER appuser
```

<div style="page-break-after: always;"></div>

#### 5.2 Multi-Stage Build Optimization

**Multi-Stage Architecture Design**

```dockerfile
# Build stage
FROM node:14 AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Runtime stage
FROM node:14-alpine
WORKDIR /app
COPY --from=build /app/dist /app
CMD ["node", "server.js"]
```

**Language-Specific Optimizations**

- Java application optimization patterns
- Python dependency management
- Node.js module optimization
- C/C++ compilation strategies

**Advanced Multi-Stage Techniques**

```dockerfile
# Using distroless base image
FROM gcr.io/distroless/java:11
COPY --from=build /app/target/app.jar /app.jar
CMD ["app.jar"]
```

#### 5.3 Dockerfile Best Practices for Enterprise Applications

**Security Optimization**

```dockerfile
RUN groupadd -r appuser && useradd -r -g appuser appuser
USER appuser
```

<div style="page-break-after: always;"></div>

**Build Performance Enhancement**

```bash
# Use BuildKit for faster builds
export DOCKER_BUILDKIT=1
docker build -t myapp .
```

**Image Standardization**

```dockerfile
LABEL org.opencontainers.image.vendor="NADRA" \
      org.opencontainers.image.title="Document Analysis API" \
      org.opencontainers.image.version="1.0.0"
```

**Hands-on Exercise 5.1: Creating Efficient Dockerfiles**

1. Create a multi-stage Dockerfile for a Java application
2. Optimize layer structure
3. Implement security best practices
4. Measure image size before and after optimization

**Hands-on Exercise 5.2: Dockerfile Analysis**

1. Review sample Dockerfiles
2. Identify security and efficiency issues
3. Apply best practices to improve them 

<div style="page-break-after: always;"></div>

### MODULE 6: DOCUMENT ANALYSIS SYSTEM ARCHITECTURE

#### 6.1 Document Analysis System Requirements & Architecture

**Business Requirements Analysis**

- Document processing volume and throughput requirements
- OCR accuracy and reliability metrics
- NLP analysis capabilities and integration

**System Architecture Overview**

```
Document Ingestion → OCR Processing → NLP Analysis → Results Storage
      ↓                   ↓                ↓               ↓
Message Queue ←───────────────────────────────────────────┘
```

**Containerization Strategy**

- Component service boundaries
- State management approach
- Scalability and redundancy design

#### 6.2 OCR Subsystem Design

**OCR Engine Selection**

- Tesseract OCR architecture and capabilities
- Google Vision API integration options
- OCR preprocessing requirements

**Technical Implementation Requirements**

- PDF and image preprocessing pipeline
- Text extraction workflow
- Output standardization and validation

**Containerization Considerations**

- Base image selection for OCR workloads
- Resource requirements analysis
- Performance optimization opportunities

<div style="page-break-after: always;"></div>

#### 6.3 NLP Processing Pipeline Design

**NLP Technology Selection**

- spaCy vs. NLTK comparison for document analysis
- Named Entity Recognition requirements
- Language model selection criteria

**Processing Pipeline Architecture**

- Text normalization and preprocessing
- Entity extraction and classification
- Sentiment and intent analysis

**Containerization Strategy**

- Model packaging and distribution
- Inference optimization techniques
- Scaling and resource allocation

**Hands-on Exercise 6.1: Document Analysis System Architecture Design**

1. Design component interaction diagram
2. Create container specifications for each component
3. Document resource requirements and scaling strategy

**Hands-on Exercise 6.2: OCR Subsystem Prototyping**

1. Set up Tesseract OCR container
2. Test with sample NADRA documents
3. Measure accuracy and performance

<div style="page-break-after: always;"></div>

### MODULE 7: DOCKER NETWORKING DEEP DIVE

#### 7.1 Docker Network Architecture & Drivers

**Core Network Driver Types**

```bash
# Create bridge network
docker network create --driver bridge my_bridge

# Create overlay network
docker network create --driver overlay my_overlay

# Create macvlan network
docker network create --driver macvlan \
  --subnet=192.168.50.0/24 \
  --gateway=192.168.50.1 \
  -o parent=eth0 my_macvlan
```

**Network Creation and Management**

```bash
# List networks
docker network ls

# Inspect network
docker network inspect my_network

# Connect container to network
docker network connect my_network container_name
```

**Container Network Interface (CNI)**

- Docker network plugin architecture
- Third-party network plugin integration
- Performance comparisons across drivers

<div style="page-break-after: always;"></div>

#### 7.2 Container Communication Patterns

**Service Discovery Methods**

```bash
# DNS-based service discovery (automatic in user-defined networks)
docker run --network my_network --name db mysql
docker run --network my_network --name app myapp
# Now 'app' container can connect to 'db' using hostname 'db'
```

**Port Management Strategies**

```bash
# Publish port to host
docker run -p 8080:80 nginx

# Bind to specific interface
docker run -p 127.0.0.1:8080:80 nginx

# Publish all exposed ports
docker run -P nginx
```

**Network Segmentation**

```bash
# Create frontend and backend networks
docker network create frontend
docker network create backend

# Connect container to multiple networks
docker run --name app --network frontend nginx
docker network connect backend app
```

#### 7.3 Network Security & Troubleshooting

**Network Security Best Practices**

- Exposed port minimization
- Network policy implementation
- Traffic encryption strategies

**Advanced Network Features**

- User-defined IP addressing
- Custom bridge setup for isolation
- iptables integration and customization

**Network Troubleshooting Methodology**

```bash
# Test container connectivity
docker exec container_name ping othercontainer

# Check DNS resolution
docker exec container_name nslookup servicehost

# Network packet inspection
docker exec container_name tcpdump -i eth0 -n
```

**Hands-on Exercise 7.1: Container Network Configuration**

1. Create custom bridge networks
2. Deploy containers across networks
3. Implement service discovery
4. Test inter-network communication

**Hands-on Exercise 7.2: Network Troubleshooting**

1. Diagnose network connectivity issues
2. Implement network security policies
3. Measure performance across network drivers

<div style="page-break-after: always;"></div>

### MODULE 8: DOCKERFILE IMPLEMENTATION FOR DOCUMENT ANALYSIS SYSTEM

#### 8.1 OCR Component Dockerfile Implementation

**Base Image Selection**

```dockerfile
# Ubuntu base for Tesseract OCR
FROM ubuntu:22.04

# Install Tesseract and dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    tesseract-ocr \
    tesseract-ocr-eng \
    tesseract-ocr-urd \
    python3-pip \
    && rm -rf /var/lib/apt/lists/*
```

**Dockerfile Implementation**

```dockerfile
# Multi-stage build for OCR component
FROM ubuntu:22.04 AS builder

# Install dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    tesseract-ocr \
    python3-pip \
    python3-dev \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app
COPY requirements.txt .
RUN pip3 install --no-cache-dir -r requirements.txt

FROM ubuntu:22.04

# Install runtime dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    tesseract-ocr \
    python3 \
    python3-pip \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app
COPY --from=builder /usr/local/lib/python3.10/dist-packages /usr/local/lib/python3.10/dist-packages
COPY . .

EXPOSE 5000
HEALTHCHECK --interval=30s --timeout=10s CMD curl -f http://localhost:5000/health || exit 1
CMD ["python3", "ocr_service.py"]
```

**OCR Performance Optimization**

- Runtime configuration for OCR engine
- Thread and process management
- Memory optimization techniques

#### 8.2 NLP Component Dockerfile Implementation

**NLP Model Containerization**

```dockerfile
FROM python:3.10-slim AS builder

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app
COPY requirements.txt .
RUN pip wheel --no-cache-dir --wheel-dir /app/wheels -r requirements.txt

FROM python:3.10-slim

WORKDIR /app
COPY --from=builder /app/wheels /app/wheels
RUN pip install --no-cache-dir /app/wheels/*

# Download language models
RUN python -m spacy download en_core_web_sm && \
    python -m spacy download ur_core_news_sm

COPY . .
EXPOSE 5001
HEALTHCHECK --interval=30s --timeout=10s CMD curl -f http://localhost:5001/health || exit 1
CMD ["python", "nlp_service.py"]
```

**Performance Considerations**

- GPU support configuration
- Memory optimization for NLP models
- Threading and concurrency management

#### 8.3 Component Testing and Validation

**Testing Methodology**

- Component isolation testing
- Resource utilization analysis
- Performance benchmarking

**Validation Criteria**

- OCR accuracy metrics
- NLP model performance verification
- Throughput and latency measurement

**Hands-on Exercise 8.1: OCR Component Dockerfile Creation**

1. Create multi-stage Dockerfile for OCR component
2. Build and test the container
3. Optimize for performance and resource usage

**Hands-on Exercise 8.2: NLP Component Dockerfile Creation**

1. Create multi-stage Dockerfile for NLP component
2. Include model loading optimization
3. Test with sample OCR output

<div style="page-break-after: always;"></div>

## Day 3: Multi-Container Orchestration & Production Deployment

### MODULE 9: DOCKER VOLUME MANAGEMENT & DATA PERSISTENCE

#### 9.1 Docker Storage Architecture

**Storage Driver Architecture**

- Storage driver types (overlay2, devicemapper, btrfs, zfs)
- Performance characteristics comparison
- Use case optimization guidelines

**Volume Types and Use Cases**

```bash
# Create named volume
docker volume create data-volume

# Use named volume
docker run -v data-volume:/app/data nginx

# Use bind mount
docker run -v /host/path:/container/path nginx

# Use tmpfs mount
docker run --tmpfs /app/temp nginx
```

**Data Persistence Patterns**

- Stateful vs. stateless container design
- State externalization strategies
- Transaction consistency guarantees

<div style="page-break-after: always;"></div>

#### 9.2 Volume Management for Enterprise Applications

**Volume Creation and Configuration**

```bash
# Create volume with labels
docker volume create --label project=nadra --label env=prod doc-data

# Create volume with specific driver
docker volume create --driver local \
  --opt type=nfs \
  --opt o=addr=192.168.1.1,rw \
  --opt device=:/path/to/dir \
  nfs-volume
```

**Enterprise Storage Integration**

- NFS volume configuration
- SAN/block storage integration
- Cloud provider volume drivers (AWS EBS, Azure Disk)

**Performance Optimization**

- I/O performance benchmarking
- Volume caching strategies
- Read/write optimization techniques

#### 9.3 Backup, Recovery, and Migration

**Volume Backup Strategies**

```bash
# Backup volume to tar file
docker run --rm -v my-volume:/source -v $(pwd):/backup \
  alpine tar czf /backup/volume-backup.tar.gz -C /source .
```

**Disaster Recovery Planning**

```bash
# Restore volume from backup
docker run --rm -v my-volume:/target -v $(pwd):/backup \
  alpine sh -c "rm -rf /target/* && tar xzf /backup/volume-backup.tar.gz -C /target"
```

<div style="page-break-after: always;"></div>

**Volume Migration Techniques**

- Cross-host volume migration
- Environment migration strategy
- Upgrade and rollback procedures

**Hands-on Exercise 9.1: Volume Management for Document Analysis**

1. Create volumes for document storage
2. Configure persistence for OCR and NLP models
3. Test data persistence across container restarts

**Hands-on Exercise 9.2: Backup and Recovery Implementation**

1. Create backup scripts for document volumes
2. Test recovery procedures
3. Implement automated backup solution

<div style="page-break-after: always;"></div>

### MODULE 10: DOCKER COMPOSE FOR MULTI-CONTAINER APPLICATIONS

#### 10.1 Docker Compose Architecture and Concepts

**Compose File Structure**

```yaml
version: '3.8'
services:
  webapp:
    image: nginx:latest
    ports:
      - "80:80"
    volumes:
      - ./www:/usr/share/nginx/html
    depends_on:
      - api
  api:
    build: ./api
    environment:
      - DB_HOST=db
    depends_on:
      - db
  db:
    image: postgres:13
    volumes:
      - db-data:/var/lib/postgresql/data
    environment:
      - POSTGRES_PASSWORD=secret
volumes:
  db-data:
```

**Compose vs. Swarm vs. Kubernetes**

- Capability comparison
- Use case differentiation
- Migration paths between orchestrators

<div style="page-break-after: always;"></div>

**Compose Command Architecture**

```bash
# Start services
docker compose up -d

# View logs
docker compose logs -f

# Stop services
docker compose down
```

#### 10.2 Compose File Deep Dive

**Service Configuration Options**

```yaml
services:
  app:
    build:
      context: ./app
      dockerfile: Dockerfile.prod
      args:
        VERSION: 1.0
    restart: always
    deploy:
      resources:
        limits:
          cpus: '0.5'
          memory: 512M
```

**Networking Configuration**

```yaml
networks:
  frontend:
    driver: bridge
  backend:
    internal: true

services:
  app:
    networks:
      - frontend
      - backend
    ports:
      - "8080:80"
```

**Volume and Secret Management**

```yaml
volumes:
  data:
    driver: local
    driver_opts:
      type: nfs
      o: addr=192.168.1.1,rw

secrets:
  db_password:
    file: ./secrets/db_password.txt

services:
  app:
    volumes:
      - data:/app/data
    secrets:
      - db_password
```

#### 

<div style="page-break-after: always;"></div>

#### 10.3 Document Analysis System Compose Implementation

**System Architecture in Compose**

```yaml
services:
  ingestion:
    image: doc-ingestion:latest
    depends_on:
      - rabbitmq
    volumes:
      - document-storage:/data/documents
  ocr:
    image: doc-ocr:latest
    deploy:
      replicas: 3
    depends_on:
      - rabbitmq
    volumes:
      - document-storage:/data/documents
  nlp:
    image: doc-nlp:latest
    depends_on:
      - rabbitmq
    volumes:
      - document-storage:/data/documents
      - nlp-models:/app/models
  storage:
    image: doc-storage:latest
    depends_on:
      - postgres
      - elasticsearch
    volumes:
      - document-storage:/data/documents
  rabbitmq:
    image: rabbitmq:3-management
    volumes:
      - rabbitmq-data:/var/lib/rabbitmq
  postgres:
    image: postgres:13
    volumes:
      - postgres-data:/var/lib/postgresql/data
  elasticsearch:
    image: elasticsearch:7.14.0
    volumes:
      - es-data:/usr/share/elasticsearch/data
```

**Integration Configuration**

- Service communication setup
- Environment variables management
- Health checks implementation

**Environment Configuration**

- Development vs. production settings
- Secret management in production
- Configuration overrides

**Hands-on Exercise 10.1: Docker Compose for Document Analysis System**

1. Create complete docker-compose.yml
2. Configure service dependencies
3. Set up volumes and networks

**Hands-on Exercise 10.2: Testing and Debugging with Compose**

1. Start complete system
2. Test document processing workflow
3. Troubleshoot integration issues

<div style="page-break-after: always;"></div>

### MODULE 11: DOCKER SECURITY DEEP DIVE

#### 11.1 Container Security Fundamentals

**Container Isolation Architecture**

- Linux security mechanisms (namespaces, cgroups, capabilities)
- Isolation guarantee analysis
- Docker security defaults and their limitations

**Attack Surface Analysis**

- Common attack vectors in container environments
- Privilege escalation pathways
- Container escape vulnerabilities

**Security Benchmark Standards**

- CIS Docker Benchmark overview
- Docker security scanning tools
- Compliance automation techniques

#### 11.2 Least Privilege Implementation

**Non-Root Container Configuration**

```dockerfile
# Create non-root user in Dockerfile
RUN groupadd -r appuser && useradd -r -g appuser appuser
USER appuser
```

**Capability Management**

```bash
# Drop all capabilities and add only necessary ones
docker run --cap-drop=ALL --cap-add=NET_BIND_SERVICE nginx
```

**Read-Only Filesystem Implementation**

```bash
# Run with read-only filesystem
docker run --read-only \
  --tmpfs /run:rw,noexec \
  --tmpfs /tmp:rw,noexec \
  nginx
```

#### 11.3 Image Security & Supply Chain

**Image Vulnerability Management**

```bash
# Scan image with Trivy
trivy image nginx:latest

# Scan with Docker Scout
docker scout cves nginx:latest
```

**Image Signing and Verification**

```bash
# Enable content trust
export DOCKER_CONTENT_TRUST=1

# Push signed image
docker push myregistry/myimage:latest
```

**Base Image Security Strategy**

- Minimal base images (Alpine, distroless)
- Patch management strategy
- Image lifecycle management

#### 11.4 Runtime Security Monitoring

**Runtime Security Tools**

```bash
# Run Falco container
docker run -d --name falco \
  --privileged \
  -v /var/run/docker.sock:/var/run/docker.sock \
  falcosecurity/falco
```

**Security Monitoring Integration**

- SIEM integration approaches
- Alert generation and management
- Incident response automation

**Secure Deployment Pipeline**

- Security gate implementation
- Vulnerability policy enforcement
- Compliance reporting automation

**Hands-on Exercise 11.1: Container Security Hardening**

1. Implement non-root containers
2. Configure capability restrictions
3. Set up read-only filesystem
4. Test security controls

**Hands-on Exercise 11.2: Runtime Security Implementation**

1. Set up Falco monitoring
2. Create security profiles
3. Test with security scenarios

<div style="page-break-after: always;"></div>

### MODULE 12: PRODUCTION DEPLOYMENT & ADVANCED TOPICS

#### 12.1 Production Deployment Strategy

**Environment Configuration Management**

```yaml
# docker-compose.prod.yml
services:
  app:
    image: ${APP_IMAGE}:${APP_VERSION}
    environment:
      - NODE_ENV=production
      - LOG_LEVEL=warn
    deploy:
      replicas: 3
      resources:
        limits:
          cpus: '0.5'
          memory: 512M
```

**High Availability Implementation**

- Service replication strategies
- Load balancing configuration
- Failover and recovery automation

**CI/CD Pipeline Integration**

- Container-based CI/CD workflow
- Automated testing strategies
- Deployment automation best practices

<div style="page-break-after: always;"></div>

#### 12.2 Monitoring and Observability

**Monitoring Stack Implementation**

```yaml
# docker-compose.monitoring.yml
services:
  prometheus:
    image: prom/prometheus
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    ports:
      - "9090:9090"

  grafana:
    image: grafana/grafana
    ports:
      - "3000:3000"
    depends_on:
      - prometheus

  cadvisor:
    image: gcr.io/cadvisor/cadvisor
    volumes:
      - /:/rootfs:ro
      - /var/run:/var/run:ro
      - /sys:/sys:ro
      - /var/lib/docker/:/var/lib/docker:ro
    ports:
      - "8080:8080"
```

<div style="page-break-after: always;"></div>

**Logging Architecture**

```yaml
# ELK stack for centralized logging
services:
  elasticsearch:
    image: elasticsearch:7
    environment:
      - discovery.type=single-node
    volumes:
      - es-data:/usr/share/elasticsearch/data

  logstash:
    image: logstash:7
    volumes:
      - ./logstash/pipeline:/usr/share/logstash/pipeline
    depends_on:
      - elasticsearch

  kibana:
    image: kibana:7
    ports:
      - "5601:5601"
    depends_on:
      - elasticsearch
```

**Performance Optimization**

- Resource utilization analysis
- Bottleneck identification methodology
- Scaling decision metrics

#### 12.3 Advanced Docker Ecosystem

**Docker Swarm Introduction**

```bash
# Initialize swarm
docker swarm init

# Create service
docker service create --name web --replicas 3 -p 80:80 nginx

# Scale service
docker service scale web=5
```

**Kubernetes Migration Path**

```bash
# Convert docker-compose.yml to Kubernetes manifests
kompose convert -f docker-compose.yml
```

**Emerging Container Technologies**

- BuildKit and BuildX advances
- WASM and containerd innovations
- Docker roadmap and future directions

#### 12.4 Workshop Conclusion

**Implementation Review**

- Document analysis system architecture review
- Production readiness assessment
- Implementation challenges and solutions

**Continuous Learning Resources**

- Recommended learning paths
- Community and support resources
- Advanced certification options

**Final Assessment and Feedback**

- Knowledge assessment completion
- Skill validation certification
- Workshop feedback collection

**Hands-on Exercise 12.1: Production Deployment**

1. Configure production docker-compose.yml
2. Implement monitoring and logging
3. Test with load and performance validation

**Hands-on Exercise 12.2: System Demonstration**

1. Process sample documents end-to-end
2. Demonstrate scaling and resilience
3. Show monitoring and performance metrics

<div style="page-break-after: always;"></div>

## Command Reference

### Docker Basics

```bash
# Docker information
docker version
docker info

# Container lifecycle
docker run [OPTIONS] IMAGE [COMMAND]
docker start CONTAINER
docker stop CONTAINER
docker restart CONTAINER
docker pause CONTAINER
docker unpause CONTAINER
docker rm CONTAINER

# Container management
docker ps [OPTIONS]
docker logs [OPTIONS] CONTAINER
docker exec [OPTIONS] CONTAINER COMMAND
docker attach CONTAINER
docker inspect CONTAINER
docker top CONTAINER
docker stats [CONTAINER...]

# Image management
docker images [OPTIONS]
docker pull [OPTIONS] IMAGE
docker push [OPTIONS] IMAGE
docker build [OPTIONS] PATH
docker rmi [OPTIONS] IMAGE
docker history IMAGE
docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
```

<div style="page-break-after: always;"></div>

### Docker Compose

```bash
# Compose lifecycle
docker compose up [OPTIONS]
docker compose down [OPTIONS]
docker compose start
docker compose stop
docker compose restart

# Compose management
docker compose ps
docker compose logs [SERVICE...]
docker compose exec SERVICE COMMAND
docker compose config
docker compose top
docker compose build

# Compose scaling
docker compose up -d --scale SERVICE=NUM
```

### Docker Volume Management

```bash
# Volume operations
docker volume create [OPTIONS] [VOLUME]
docker volume ls [OPTIONS]
docker volume inspect [OPTIONS] VOLUME
docker volume rm [OPTIONS] VOLUME
docker volume prune [OPTIONS]

# Volume backup
docker run --rm -v VOLUME_NAME:/source -v $(pwd):/backup \
  alpine tar czf /backup/volume-backup.tar.gz -C /source .

# Volume restore
docker run --rm -v VOLUME_NAME:/target -v $(pwd):/backup \
  alpine sh -c "rm -rf /target/* && tar xzf /backup/volume-backup.tar.gz -C /target"
```

<div style="page-break-after: always;"></div>

### Docker Network Management

```bash
# Network operations
docker network create [OPTIONS] NETWORK
docker network ls [OPTIONS]
docker network inspect [OPTIONS] NETWORK
docker network connect [OPTIONS] NETWORK CONTAINER
docker network disconnect [OPTIONS] NETWORK CONTAINER
docker network rm NETWORK
docker network prune [OPTIONS]
```

### Docker Security

```bash
# User and capabilities
docker run --user 1000:1000 IMAGE
docker run --cap-drop=ALL --cap-add=NET_BIND_SERVICE IMAGE

# Security options
docker run --security-opt=no-new-privileges IMAGE
docker run --read-only IMAGE
docker run --tmpfs /tmp IMAGE

# Content trust
export DOCKER_CONTENT_TRUST=1
docker push USER/IMAGE:TAG
```

### Docker System Management

```bash
# System information
docker system info
docker system df
docker system events

# Cleanup operations
docker system prune [OPTIONS]
docker container prune [OPTIONS]
docker image prune [OPTIONS]
docker volume prune [OPTIONS]
docker network prune [OPTIONS]
```

<div style="page-break-after: always;"></div>

## Troubleshooting Guide

### Installation Issues

| Problem                        | Possible Cause             | Solution                                                 |
| ------------------------------ | -------------------------- | -------------------------------------------------------- |
| Docker daemon won't start      | Missing dependencies       | Check system requirements and install dependencies       |
| Permission denied              | User not in docker group   | `sudo usermod -aG docker $USER` then log out and back in |
| Error connecting to daemon     | Docker service not running | `sudo systemctl start docker`                            |
| Network timeout during install | Network issues             | Check proxy settings and connectivity                    |

### Container Issues

| Problem                        | Possible Cause                | Solution                                                 |
| ------------------------------ | ----------------------------- | -------------------------------------------------------- |
| Container exits immediately    | Command completes             | Use a blocking command or add `--restart=unless-stopped` |
| Container can't access network | Network configuration         | Check network settings with `docker network inspect`     |
| Container fails with OOMKilled | Not enough memory             | Increase memory limit with `--memory` option             |
| Port binding fails             | Port already in use           | Change host port or stop competing service               |
| Volume mount fails             | Incorrect path or permissions | Check path exists and has correct permissions            |

### Image Issues

| Problem                   | Possible Cause        | Solution                                    |
| ------------------------- | --------------------- | ------------------------------------------- |
| Build fails               | Error in Dockerfile   | Check Dockerfile syntax and dependencies    |
| Pull fails                | Rate limiting         | Log in to Docker Hub or use mirror registry |
| Image too large           | Unnecessary files     | Use multi-stage build and .dockerignore     |
| Layer caching not working | Invalidated cache     | Reorder Dockerfile instructions             |
| Push fails                | Authentication issues | Check credentials with `docker login`       |

<div style="page-break-after: always;"></div>

### Docker Compose Issues

| Problem                   | Possible Cause       | Solution                                        |
| ------------------------- | -------------------- | ----------------------------------------------- |
| Service won't start       | Dependency issue     | Check `depends_on` configuration                |
| Configuration error       | YAML syntax          | Validate with `docker compose config`           |
| Volume persistence issues | Incorrect path       | Check volume configuration and paths            |
| Network connectivity      | Service discovery    | Ensure services on same network                 |
| Environment variables     | Missing or incorrect | Check `.env` file and environment configuration |

### Performance Issues

| Problem                 | Possible Cause         | Solution                                    |
| ----------------------- | ---------------------- | ------------------------------------------- |
| Container slow          | Resource contention    | Check with `docker stats` and adjust limits |
| High disk usage         | Unused images/volumes  | Run `docker system prune`                   |
| Network bottlenecks     | Default network driver | Consider macvlan or host networking         |
| Build performance       | Inefficient Dockerfile | Use BuildKit and optimize caching           |
| Slow volume performance | Storage driver         | Consider different volume driver            |

<div style="page-break-after: always;"></div>

## Best Practices

### Docker Image Best Practices

1. **Use Official Base Images**
   
   - Verified, maintained, and secure
   - Regular security updates
   - Well-documented behavior

2. **Optimize Layers**
   
   - Combine related commands
   - Remove unnecessary files in same layer
   - Order instructions from least to most frequently changed

3. **Use Multi-Stage Builds**
   
   - Separate build and runtime environments
   - Include only necessary artifacts
   - Significantly reduce final image size

4. **Implement Security Measures**
   
   - Run as non-root user
   - Use minimal base images
   - Scan images for vulnerabilities

5. **Document with Labels**
   
   - Maintainer information
   - Version details
   - Build information
   - Usage instructions

### Docker Container Best Practices

1. **Resource Management**
   
   - Define appropriate memory and CPU limits
   - Monitor resource usage
   - Implement proper restart policies

2. **Data Management**
   
   - Use named volumes for persistent data
   - Implement backup strategies
   - Use tmpfs for sensitive temporary data

3. **Logging Practices**
   
   - Configure appropriate log drivers
   - Implement log rotation
   - Centralize logs for analysis

4. **Security Hardening**
   
   - Implement least privilege principle
   - Use read-only filesystems where possible
   - Drop unnecessary capabilities

5. **Health Monitoring**
   
   - Implement container health checks
   - Monitor container state
   - Set up alerting for failures

### Docker Compose Best Practices

1. **Project Organization**
   
   - Modular service definitions
   - Environment-specific overrides
   - Consistent naming conventions

2. **Configuration Management**
   
   - Use .env files for variables
   - Separate secrets from configuration
   - Document required variables

3. **Service Dependencies**
   
   - Implement proper depends_on
   - Define healthchecks for critical services
   - Handle startup order correctly

4. **Network Design**
   
   - Create separate networks for tiers
   - Limit exposed ports
   - Implement proper service discovery

5. **Volume Management**
   
   - Define explicit volume configurations
   - Use named volumes for persistence
   - Document volume purposes

### Production Deployment Best Practices

1. **High Availability**
   
   - Replicate critical services
   - Implement load balancing
   - Design for failover

2. **Monitoring and Observability**
   
   - Implement comprehensive monitoring
   - Centralize logs
   - Set up alerts for key metrics

3. **Security Measures**
   
   - Regular vulnerability scanning
   - Content trust for images
   - Network isolation

4. **CI/CD Integration**
   
   - Automated testing
   - Deployment verification
   - Rollback capability

5. **Disaster Recovery**
   
   - Regular backups
   - Documented recovery procedures
   - Tested recovery scenarios

<div style="page-break-after: always;"></div>

## Additional Resources

### Official Documentation

- [Docker Documentation](https://docs.docker.com/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)
- [Docker Hub](https://hub.docker.com/)
- [Open Container Initiative](https://opencontainers.org/)

### Books

- "Docker Deep Dive" by Nigel Poulton
- "Docker: Up & Running" by Sean P. Kane & Karl Matthias
- "Docker in Practice" by Ian Miell & Aidan Hobson Sayers
- "Container Security" by Liz Rice

### Online Courses

- Docker Mastery (Udemy)
- Docker and Kubernetes: The Complete Guide (Udemy)
- Docker for the Absolute Beginner (Udemy)
- Docker Certified Associate Preparation Course

### Blogs and Websites

- Docker Blog: https://www.docker.com/blog/
- Container Journal: https://containerjournal.com/
- The New Stack: https://thenewstack.io/
- Medium Docker Topics: https://medium.com/tag/docker

### Tools

- Docker Scout: Security scanning for Docker images
- Portainer: UI for Docker management
- cAdvisor: Container monitoring
- Docker Bench for Security: Security auditing tool
- Hadolint: Dockerfile linter
