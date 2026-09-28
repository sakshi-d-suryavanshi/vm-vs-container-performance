# Performance Analysis of Virtual Machines and Containers

## 1. Introduction

This experiment focuses on the performance analysis and comparison of virtual machines and Docker containers under similar workloads.

The experiment uses:

* **VMware Workstation** as the virtualization platform
* **Ubuntu** as the guest operating system
* **Docker** as the container platform
* **Sysbench** for CPU and memory performance benchmarking
* **fio** for disk I/O performance benchmarking
* **iperf3** for network performance benchmarking
* **FastAPI** for application performance testing

The virtual machine and Docker container are configured with comparable resources and workloads so that their performance can be measured and compared.

---

## 2. Objectives

The objectives of this experiment are:

1. To prepare and configure the experimental environment for VM and container performance comparison.
2. To configure a virtual machine using VMware Workstation.
3. To configure a Docker container with controlled CPU, memory, disk and network resources.
4. To verify the CPU, memory, storage and network configurations.
5. To perform baseline performance measurements.
6. To measure CPU performance using Sysbench.
7. To measure memory performance using Sysbench.
8. To measure disk I/O performance using fio.
9. To measure network performance using iperf3.
10. To deploy a FastAPI application for application-level performance testing.
11. To measure API performance under different workloads.
12. To measure VM and container startup time.
13. To study scalability by increasing workload levels.
14. To automate the execution and collection of benchmark results.
15. To process and analyze the collected benchmark data.
16. To perform statistical analysis of the experimental results.
17. To generate graphs and comparison tables.
18. To compare the performance of virtual machines and containers using the collected measurements.
19. To document the complete experiment and publish the results in a GitHub repository.

---

## 3. Experimental Configuration

| Resource               | Configuration      |
| ---------------------- | ------------------ |
| Host Operating System  | Windows            |
| Hypervisor             | VMware Workstation |
| Guest Operating System | Ubuntu 24.04 LTS   |
| Container Platform     | Docker             |
| CPU                    | 4 vCPU             |
| Memory                 | 8 GB               |
| Disk                   | 60 GB              |
| CPU Benchmark          | Sysbench           |
| Memory Benchmark       | Sysbench           |
| Disk Benchmark         | fio                |
| Network Benchmark      | iperf3             |
| Application Framework  | FastAPI            |
| Programming Language   | Python             |

---

# 4. VM Environment

## 4.1 VMware Workstation

VMware Workstation is used to run the Ubuntu virtual machine for the experiment.

The virtual machine is configured with the required CPU, memory, disk and network resources.

| Parameter       | Configuration      |
| --------------- | ------------------ |
| Hypervisor      | VMware Workstation |
| Hypervisor Type | Type-2             |
| Guest OS        | Ubuntu             |
| CPU             | 4 vCPU             |
| Memory          | 8 GB               |
| Disk            | 60 GB              |
| Network         | NAT / Bridged      |

## 4.2 Ubuntu Verification

The Ubuntu virtual machine configuration is verified using:

```bash
hostnamectl
```

The CPU configuration is checked using:

```bash
lscpu
```

Memory information is checked using:

```bash
free -h
```

Disk information is checked using:

```bash
df -h
```

System resource utilization is monitored using:

```bash
top
```

Network configuration is checked using:

```bash
ip addr
```

---

# 5. Docker Environment

## 5.1 Docker

Docker is used as the container platform for the experiment.

Docker installation is verified using:

```bash
docker --version
```

Running containers are checked using:

```bash
docker ps
```

Docker images are checked using:

```bash
docker images
```

## 5.2 Container Configuration

The Docker container is configured with resources comparable to the VM.

| Parameter             | Configuration  |
| --------------------- | -------------- |
| Platform              | Docker         |
| CPU                   | 4 CPUs         |
| Memory                | 8 GB           |
| Network               | Docker Network |
| Operating Environment | Ubuntu Host    |

The same or comparable workloads are executed inside the container for performance comparison.

---

# 6. Baseline Measurement

A baseline measurement is performed before the VM and container performance comparison.

The baseline measurement provides a reference for the performance experiments.

The actual baseline results will be recorded below.

| Metric               |       Baseline |
| -------------------- | -------------: |
| Total Execution Time | To be recorded |
| Total Events         | To be recorded |
| Events per Second    | To be recorded |
| Average Latency      | To be recorded |

The raw baseline results are stored in:

```text
results/raw/baseline/
```

---

# 7. CPU Performance

## 7.1 Sysbench Installation

Sysbench is installed using:

```bash
sudo apt update
sudo apt install sysbench -y
```

The installation is verified using:

```bash
sysbench --version
```

## 7.2 CPU Benchmark

The CPU benchmark is executed using:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

The same benchmark workload is executed in both the VM and Docker container.

The benchmark measures:

* Total execution time
* Total events
* Events per second
* Minimum latency
* Average latency
* Maximum latency
* Percentile latency

## 7.3 CPU Results

### VM Results

| Metric               |             VM |
| -------------------- | -------------: |
| Total Execution Time | To be recorded |
| Total Events         | To be recorded |
| Events per Second    | To be recorded |
| Minimum Latency      | To be recorded |
| Average Latency      | To be recorded |
| Maximum Latency      | To be recorded |
| 95th Percentile      | To be recorded |

### Docker Container Results

| Metric               | Docker Container |
| -------------------- | ---------------: |
| Total Execution Time |   To be recorded |
| Total Events         |   To be recorded |
| Events per Second    |   To be recorded |
| Minimum Latency      |   To be recorded |
| Average Latency      |   To be recorded |
| Maximum Latency      |   To be recorded |
| 95th Percentile      |   To be recorded |

The raw CPU results are stored in:

```text
results/raw/cpu/
```

---

# 8. Memory Performance

## 8.1 Memory Benchmark

Memory performance is measured using Sysbench.

The memory workload uses:

* Block size: 1 MB
* Total memory operation: 10 GB
* Threads: 4

The same workload is used for the VM and Docker container.

## 8.2 Memory Results

### VM Results

| Metric               |             VM |
| -------------------- | -------------: |
| Total Execution Time | To be recorded |
| Total Operations     | To be recorded |
| Throughput           | To be recorded |
| Average Latency      | To be recorded |

### Docker Container Results

| Metric               | Docker Container |
| -------------------- | ---------------: |
| Total Execution Time |   To be recorded |
| Total Operations     |   To be recorded |
| Throughput           |   To be recorded |
| Average Latency      |   To be recorded |

The raw memory results are stored in:

```text
results/raw/memory/
```

---

# 9. Disk I/O Performance

## 9.1 fio Installation

The disk benchmarking tool is installed using:

```bash
sudo apt update
sudo apt install fio -y
```

The installation is verified using:

```bash
fio --version
```

## 9.2 Disk Benchmark

Disk performance is measured using fio.

The experiment includes:

* Sequential write
* Sequential read
* Random write
* Random read

The benchmark measures:

* Throughput
* IOPS
* Latency

## 9.3 Disk Results

### VM Results

| Test             |     Throughput |           IOPS | Average Latency |
| ---------------- | -------------: | -------------: | --------------: |
| Sequential Write | To be recorded | To be recorded |  To be recorded |
| Sequential Read  | To be recorded | To be recorded |  To be recorded |
| Random Write     | To be recorded | To be recorded |  To be recorded |
| Random Read      | To be recorded | To be recorded |  To be recorded |

### Docker Container Results

| Test             |     Throughput |           IOPS | Average Latency |
| ---------------- | -------------: | -------------: | --------------: |
| Sequential Write | To be recorded | To be recorded |  To be recorded |
| Sequential Read  | To be recorded | To be recorded |  To be recorded |
| Random Write     | To be recorded | To be recorded |  To be recorded |
| Random Read      | To be recorded | To be recorded |  To be recorded |

The raw disk results are stored in:

```text
results/raw/disk/
```

---

# 10. Network Performance

## 10.1 iperf3 Installation

The network benchmarking tool is installed using:

```bash
sudo apt update
sudo apt install iperf3 -y
```

The installation is verified using:

```bash
iperf3 --version
```

## 10.2 Network Benchmark

The network performance is measured using an iperf3 client-server arrangement.

The server is started using:

```bash
iperf3 -s
```

The client is run using:

```bash
iperf3 -c <server-ip> -t 10
```

The experiment records:

* Network throughput
* Retransmissions

## 10.3 Network Results

### VM Results

| Run   |     Throughput | Retransmissions |
| ----- | -------------: | --------------: |
| Run 1 | To be recorded |  To be recorded |
| Run 2 | To be recorded |  To be recorded |
| Run 3 | To be recorded |  To be recorded |

### Docker Container Results

| Run   |     Throughput | Retransmissions |
| ----- | -------------: | --------------: |
| Run 1 | To be recorded |  To be recorded |
| Run 2 | To be recorded |  To be recorded |
| Run 3 | To be recorded |  To be recorded |

The raw network results are stored in:

```text
results/raw/network/
```

---

# 11. FastAPI Application Performance

## 11.1 FastAPI Application

A FastAPI application is created to measure application-level performance.

The application provides the following endpoints:

```text
/health
/compute
/memory
```

The FastAPI application is started using:

```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```

## 11.2 API Workloads

The following API endpoints are tested:

### Health Endpoint

```text
/health
```

This endpoint is used to measure basic API response performance.

### CPU Workload

```text
/compute
```

This endpoint performs a CPU-intensive operation.

### Memory Workload

```text
/memory
```

This endpoint performs a memory-intensive operation.

The same application and workloads are used for the VM and Docker container.

## 11.3 API Performance Results

### VM Results

| Endpoint |   Requests/sec | Average Latency |         Errors |
| -------- | -------------: | --------------: | -------------: |
| /health  | To be recorded |  To be recorded | To be recorded |
| /compute | To be recorded |  To be recorded | To be recorded |
| /memory  | To be recorded |  To be recorded | To be recorded |

### Docker Container Results

| Endpoint |   Requests/sec | Average Latency |         Errors |
| -------- | -------------: | --------------: | -------------: |
| /health  | To be recorded |  To be recorded | To be recorded |
| /compute | To be recorded |  To be recorded | To be recorded |
| /memory  | To be recorded |  To be recorded | To be recorded |

---

# 12. Startup Time

Startup performance is measured for both the virtual machine and Docker container.

The experiment measures:

* VM startup time
* Container startup time
* Application startup time
* Application ready time

## 12.1 Startup Results

| Measurement              |             VM | Docker Container |
| ------------------------ | -------------: | ---------------: |
| Environment Startup Time | To be recorded |   To be recorded |
| Application Startup Time | To be recorded |   To be recorded |
| Application Ready Time   | To be recorded |   To be recorded |

The raw startup results are stored in:

```text
results/raw/startup/
```

---

# 13. Scalability

Scalability is tested by increasing workload levels and observing the performance of the VM and Docker container.

## 13.1 CPU Scalability

CPU performance is tested using increasing thread counts.

Example:

```text
1 → 2 → 4 → 8 threads
```

The performance is recorded for each workload level.

## 13.2 API Scalability

API performance is tested using increasing numbers of clients and connections.

The measurements include:

* Requests per second
* Latency
* Errors
* Throughput

## 13.3 Scalability Results

| Workload Level |             VM | Docker Container |
| -------------- | -------------: | ---------------: |
| Level 1        | To be recorded |   To be recorded |
| Level 2        | To be recorded |   To be recorded |
| Level 3        | To be recorded |   To be recorded |
| Level 4        | To be recorded |   To be recorded |

The raw scalability results are stored in:

```text
results/raw/scalability/
```

---

# 14. Automated Benchmark Execution

Benchmark scripts are used to automate the execution of experiments and collection of results.

The scripts are used to:

* Execute repeated benchmark runs
* Maintain consistent benchmark parameters
* Save raw results
* Reduce manual errors
* Organize benchmark outputs

The scripts are stored in:

```text
scripts/
```

---

# 15. Result Processing

The collected benchmark results are processed using Python.

Pandas is used for reading and processing the collected CSV data.

Matplotlib is used to generate graphs from the processed results.

Processed results are stored in:

```text
results/processed/
```

---

# 16. Statistical Analysis

The collected benchmark results are analyzed using repeated measurements.

The analysis includes:

* Mean
* Minimum
* Maximum
* Standard deviation
* Variation between runs

The statistical analysis is performed using the actual experimental measurements.

---

# 17. Performance Comparison

The final performance comparison includes all completed experiments.

| Performance Metric      |             VM | Docker Container |
| ----------------------- | -------------: | ---------------: |
| CPU Events per Second   | To be recorded |   To be recorded |
| CPU Execution Time      | To be recorded |   To be recorded |
| CPU Average Latency     | To be recorded |   To be recorded |
| Memory Throughput       | To be recorded |   To be recorded |
| Disk Read Throughput    | To be recorded |   To be recorded |
| Disk Write Throughput   | To be recorded |   To be recorded |
| Disk Read IOPS          | To be recorded |   To be recorded |
| Disk Write IOPS         | To be recorded |   To be recorded |
| Disk Latency            | To be recorded |   To be recorded |
| Network Throughput      | To be recorded |   To be recorded |
| Network Retransmissions | To be recorded |   To be recorded |
| API Requests/sec        | To be recorded |   To be recorded |
| API Average Latency     | To be recorded |   To be recorded |
| Startup Time            | To be recorded |   To be recorded |
| Scalability Performance | To be recorded |   To be recorded |

The comparison is based on the actual benchmark measurements obtained during the experiments.

---

# 18. Graphs and Visualization

Graphs are generated from the processed experimental results.

The planned graphs include:

* CPU performance comparison
* Memory performance comparison
* Disk throughput comparison
* Disk IOPS comparison
* Disk latency comparison
* Network throughput comparison
* API performance comparison
* Startup-time comparison
* CPU scalability comparison
* API scalability comparison

The graphs are stored in:

```text
results/figures/
```

---

# 19. Current Progress

| Experiment                    | Status      |
| ----------------------------- | ----------- |
| VM setup                      | Completed   |
| Docker setup                  | Completed   |
| Baseline measurement          | Completed   |
| CPU benchmark                 | Completed   |
| Memory benchmark              | Completed   |
| Disk I/O benchmark            | Completed   |
| Network benchmark             | Completed   |
| FastAPI application           | Pending     |
| API performance benchmark     | Pending     |
| Startup-time measurement      | Pending     |
| Scalability testing           | Pending     |
| Automated benchmark execution | Pending     |
| Result processing             | Pending     |
| Statistical analysis          | Pending     |
| Graph generation              | Pending     |
| Final performance comparison  | Pending     |
| Documentation                 | In Progress |

---

# 20. Project Structure

```text
vm-vs-container-performance/
│
├── README.md
│
├── docs/
│   ├── cpu-info.txt
│   ├── memory-info.txt
│   ├── storage-info.txt
│   ├── kernel-info.txt
│   └── vm-configuration.txt
│
├── api/
│   └── main.py
│
├── docker/
│   └── Dockerfile
│
├── scripts/
│
├── workloads/
│
└── results/
    │
    ├── raw/
    │   ├── baseline/
    │   ├── cpu/
    │   ├── memory/
    │   ├── disk/
    │   ├── network/
    │   ├── startup/
    │   └── scalability/
    │
    ├── processed/
    │
    └── figures/
```

---

# 21. Conclusion

This experiment focuses on the performance analysis and comparison of virtual machines and Docker containers using controlled and comparable workloads.

The experiment includes CPU, memory, disk I/O, network, application performance, startup time and scalability measurements.

Sysbench is used for CPU and memory benchmarking, fio is used for disk I/O benchmarking, iperf3 is used for network benchmarking, and FastAPI is used for application-level performance testing.

The collected benchmark results are processed and statistically analyzed to compare the measured performance of the VM and Docker container.

Graphs and comparison tables are generated from the experimental results.

The final conclusion will be based on the actual measurements obtained after completing all experiments.
