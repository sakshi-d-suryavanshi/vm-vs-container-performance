# Performance Analysis of Virtual Machines and Containers

## 1. Introduction

This experiment focuses on the performance analysis of virtual machines and containers.

The experiment uses:

* **VMware** as the virtualization platform
* **Docker** as the containerization platform
* **Ubuntu 24.04.5 LTS** as the operating system
* **Sysbench** for CPU and memory performance benchmarking
* **fio** for disk I/O benchmarking
* **iperf3** for network performance benchmarking
* **FastAPI** for application performance testing

Both environments are configured with comparable system resources so that their CPU, memory, disk, network and application performance can be compared.

---

## 2. Objectives

The objectives of this experiment are:

1. To configure and verify a virtual machine environment.
2. To create and configure a Docker container environment.
3. To verify CPU, memory and disk configurations.
4. To perform CPU and memory benchmarking using Sysbench.
5. To measure disk I/O performance using fio.
6. To measure network performance using iperf3.
7. To evaluate FastAPI application performance.
8. To record the benchmark results.
9. To compare the performance of virtual machines and containers.

---

## 3. Experimental Configuration

| Resource          | Configuration      |
| ----------------- | ------------------ |
| Operating System  | Ubuntu 24.04.5 LTS |
| CPU               | 4 vCPU             |
| Memory            | 7.761 GiB          |
| Disk              | 60 GB              |
| Container Runtime | Docker             |
| CPU Benchmark     | Sysbench 1.0.20    |
| Memory Benchmark  | Sysbench 1.0.20    |
| Disk Benchmark    | fio 3.36           |
| Network Benchmark | iperf3 3.16        |
| Application       | FastAPI            |
| API Benchmark     | ApacheBench / wrk  |

---

# 4. Part A - Virtual Machine

## 4.1 VMware Virtual Machine

VMware is used to provide the virtual machine environment for the first part of the experiment.

The virtual machine is configured with the following resources:

| Parameter               | Configuration      |
| ----------------------- | ------------------ |
| Virtualization Platform | VMware             |
| Guest OS                | Ubuntu 24.04.5 LTS |
| CPU                     | 4 vCPU             |
| Memory                  | 7.761 GiB          |
| Disk                    | 60 GB              |
| Available Disk Space    | 45 GB              |

## 4.2 Ubuntu Verification

The CPU configuration is checked using:

```bash
nproc
```

This command is used to check the number of available CPU processing units.

Memory information is checked using:

```bash
free -h
```

This command is used to check the total, used, free and available memory.

Disk information is checked using:

```bash
lsblk
```

This command is used to identify the available storage devices and their partitions.

The available disk space is checked using:

```bash
df -h
```

This command is used to check the disk space available on the mounted file systems.

---

## 4.3 Benchmark Tools Verification

The benchmark tools are verified using:

```bash
sysbench --version
```

```bash
fio --version
```

```bash
iperf3 --version
```

These commands are used to verify that Sysbench, fio and iperf3 are installed and available for the experiments.

---

## 4.4 CPU Benchmark

The CPU benchmark is executed using different numbers of threads.

The 1-thread benchmark is executed using:

```bash
sysbench cpu --cpu-max-prime=20000 --threads=1 --time=30 run
```

The 2-thread benchmark is executed using:

```bash
sysbench cpu --cpu-max-prime=20000 --threads=2 --time=30 run
```

The 4-thread benchmark is executed using:

```bash
sysbench cpu --cpu-max-prime=20000 --threads=4 --time=30 run
```

The 8-thread benchmark is executed using:

```bash
sysbench cpu --cpu-max-prime=20000 --threads=8 --time=30 run
```

These commands are used to measure CPU performance at different levels of parallelism.

## 4.5 Memory Benchmark

The memory benchmark is executed using:

```bash
sysbench memory --memory-block-size=1M --memory-total-size=10G --threads=4 run
```

This command is used to measure the memory write throughput of the virtual machine.

### Type of Operation

* Block size: 1 MiB
* Total size: 10 GiB
* Threads: 4
* Operation: Write

## 4.6 Disk I/O Benchmark

The disk benchmark is executed using:

```bash
fio --name=vm-disk --filename=/tmp/testfile --size=10G --bs=1M --rw=write --direct=1 --iodepth=16 --runtime=30 --time_based --group_reporting
```

This command is used to measure sequential disk write performance using fio.

The test measures:

* IOPS
* Bandwidth
* Latency

## 4.7 Network Benchmark

The IP address of the virtual machine is checked using:

```bash
hostname -I
```

This command is used to identify the IP address required for the network performance test.

The iperf3 network benchmark is executed using:

```bash
iperf3 -c 192.168.234.130 -t 10
```

This command is used to measure network throughput between the VM and the iperf3 server for 10 seconds.

## 4.8 VM Results

### CPU Results

| Threads | VM Events/sec |
| ------: | ------------: |
|       1 |       1668.83 |
|       2 |       3357.85 |
|       4 |       6623.18 |
|       8 |       6368.62 |

### Memory Result

| Metric            |                VM |
| ----------------- | ----------------: |
| Memory Throughput | 105162.73 MiB/sec |

### Disk Result

| Metric    |           VM |
| --------- | -----------: |
| IOPS      |         1771 |
| Bandwidth | 1771 MiB/sec |

### Network Result

| Metric    |             VM |
| --------- | -------------: |
| Transfer  |        75.8 GB |
| Bandwidth | 65.1 Gbits/sec |

---

# 5. Part B - Docker Container

## 5.1 Docker Container

Docker is used as the containerization platform for the second part of the experiment.

A benchmark container is created using the Docker image:

```bash
sudo docker run -it --name benchmark-container vn-vs-container
```

The container is used to execute the same benchmark tools and workloads used for the virtual machine.

| Parameter         | Configuration          |
| ----------------- | ---------------------- |
| Container Runtime | Docker                 |
| Base Image        | Ubuntu 24.04           |
| Container Image   | vn-vs-container:latest |
| CPU               | Host resources         |
| Memory            | Host resources         |
| Benchmark Tools   | Sysbench, fio, iperf3  |

## 5.2 Container Verification

The container is started using:

```bash
sudo docker start benchmark-container
```

The container is entered using:

```bash
sudo docker exec -it benchmark-container bash
```

These commands are used to start the benchmark container and access its terminal for executing the experiments.

The installed benchmark tools are checked using:

```bash
sysbench --version
```

```bash
fio --version
```

```bash
iperf3 --version
```

---

## 5.3 CPU Benchmark

The CPU benchmark is executed using:

```bash
sysbench cpu --cpu-max-prime=20000 --threads=1 --time=30 run
```

```bash
sysbench cpu --cpu-max-prime=20000 --threads=2 --time=30 run
```

```bash
sysbench cpu --cpu-max-prime=20000 --threads=4 --time=30 run
```

```bash
sysbench cpu --cpu-max-prime=20000 --threads=8 --time=30 run
```

These commands are used to measure container CPU performance at different thread levels.

## 5.4 Memory Benchmark

The memory benchmark is executed using:

```bash
sysbench memory --memory-block-size=1M --memory-total-size=10G --threads=4
```
