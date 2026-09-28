# Performance Analysis of Virtual Machines and Containers

## 1. Introduction

This experiment focuses on the performance analysis of virtual machines and Docker containers under similar workloads.

The experiment uses:

* **VMware Workstation** as the virtualization platform
* **Ubuntu** as the guest operating system
* **Docker** as the container platform
* **Sysbench** for CPU and memory performance benchmarking
* **fio** for disk I/O performance benchmarking
* **iperf3** for network performance benchmarking

The experiments are performed using comparable resources and workloads so that the performance of the virtual machine and container can be measured and compared.

---

## 2. Objectives

The objectives of this experiment are:

1. To configure a virtual machine using VMware Workstation.
2. To configure Docker containers for performance testing.
3. To verify CPU, memory, disk and network configurations.
4. To perform CPU performance benchmarking.
5. To perform memory performance benchmarking.
6. To perform disk I/O benchmarking.
7. To perform network performance benchmarking.
8. To record the benchmark results.
9. To compare the measured performance of the VM and container.

---

## 3. Experimental Configuration

| Resource               | Configuration      |
| ---------------------- | ------------------ |
| Host Operating System  | Windows            |
| Hypervisor             | VMware Workstation |
| Guest Operating System | Ubuntu             |
| Container Platform     | Docker             |
| CPU                    | 4 vCPU             |
| Memory                 | 8 GB               |
| Disk                   | 60 GB              |
| CPU Benchmark          | Sysbench           |
| Memory Benchmark       | Sysbench           |
| Disk Benchmark         | fio                |
| Network Benchmark      | iperf3             |

---

# 4. VM Environment

## 4.1 VMware Workstation

VMware Workstation is used to run the Ubuntu virtual machine for the experiment.

The virtual machine is configured with the required CPU, memory, storage and network resources.

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

---

# 5. Docker Environment

## 5.1 Docker

Docker is used as the container platform for the experiment.

Docker version is verified using:

```bash
docker --version
```

Running containers can be checked using:

```bash
docker ps
```

Docker images can be checked using:

```bash
docker images
```

## 5.2 Container Configuration

The Docker container is used to perform the same or comparable workloads used for the VM measurements.

The container environment is configured and tested using the Ubuntu host system.

---

# 6. Baseline Measurement

Before performing the VM and container comparison, a baseline measurement is obtained from the environment.

The baseline measurement is used as a reference for the later performance comparison.

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

The CPU benchmark measures the processing performance of the environment.

The experiment records:

* Total execution time
* Total events
* Events per second
* Average latency
* Other latency measurements provided by Sysbench

## 7.3 CPU Results

The actual benchmark values obtained during the experiment are stored under:

```text
results/raw/cpu/
```

The VM and container results are kept separately for comparison.

---

# 8. Memory Performance

## 8.1 Memory Benchmark

Memory performance is measured using Sysbench.

The memory workload uses:

* Block size: 1 MB
* Total memory operation: 10 GB
* Threads: 4

The benchmark is used to measure memory operation performance between the VM and container environments.

## 8.2 Memory Results

The actual benchmark results obtained during the experiment are stored under:

```text
results/raw/memory/
```

The results are maintained separately for the VM and container.

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

Disk performance is tested using `fio`.

The experiment includes:

* Sequential write
* Sequential read
* Random read
* Random write

The benchmark records:

* Throughput
* IOPS
* Latency

## 9.3 Disk Results

The actual disk benchmark results are stored under:

```text
results/raw/disk/
```

The VM and container measurements are maintained separately.

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

The network performance is measured using an iperf3 client-server setup.

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

The actual network benchmark results are stored under:

```text
results/raw/network/
```

The measured results are used for the VM and container comparison.

---

# 11. Performance Comparison

The benchmark results obtained from the VM and Docker container will be compared using the following parameters:

| Performance Metric |                   VM |     Docker Container |
| ------------------ | -------------------: | -------------------: |
| CPU                | Recorded measurement | Recorded measurement |
| Memory             | Recorded measurement | Recorded measurement |
| Disk Throughput    | Recorded measurement | Recorded measurement |
| Disk IOPS          | Recorded measurement | Recorded measurement |
| Disk Latency       | Recorded measurement | Recorded measurement |
| Network Throughput | Recorded measurement | Recorded measurement |
| Retransmissions    | Recorded measurement | Recorded measurement |

The comparison will be based on the actual measurements obtained during the experiments.

Detailed processed results will be added later in:

```text
results/processed/
```

Graphs will be added in:

```text
results/figures/
```

---

# 12. Current Progress

| Experiment               | Status    |
| ------------------------ | --------- |
| VM setup                 | Completed |
| Docker setup             | Completed |
| Baseline measurement     | Completed |
| CPU benchmark            | Completed |
| Memory benchmark         | Completed |
| Disk I/O benchmark       | Completed |
| Network benchmark        | Completed |
| FastAPI application      | Pending   |
| API performance          | Pending   |
| Startup-time measurement | Pending   |
| Scalability testing      | Pending   |
| Final analysis           | Pending   |

---

# 13. Project Structure

```text
vm-vs-container-performance/
│
├── README.md
│
├── docs/
│
├── docker/
│
├── scripts/
│
├── workloads/
│
└── results/
    ├── raw/
    │   ├── baseline/
    │   ├── cpu/
    │   ├── memory/
    │   ├── disk/
    │   └── network/
    │
    ├── processed/
    └── figures/
```

---

# 14. Conclusion

The experiment measures the performance of a virtual machine and Docker container using CPU, memory, disk I/O and network workloads.

The measurements obtained from Sysbench, fio and iperf3 are recorded and organized for comparison.

The remaining FastAPI, startup-time and scalability experiments will be performed in the next stages of the project.

The final analysis will be based on the actual experimental measurements collected during the complete experiment.
