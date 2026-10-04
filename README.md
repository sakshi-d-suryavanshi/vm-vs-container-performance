# Performance Analysis of Virtual Machines and Containers

## 1. Introduction

This experiment focuses on the performance analysis of a Virtual Machine and a Docker Container running the same workloads.

The experiment uses:

* **VMware Workstation** for the Virtual Machine
* **Docker** for the Container
* **Ubuntu** as the guest operating system
* **Sysbench** for CPU and memory benchmarking
* **fio** for disk I/O benchmarking
* **iperf3** for network performance benchmarking
* **FastAPI** for application performance testing

Both environments are configured with comparable resources so that their performance can be measured and compared under similar workloads.

---

## 2. Objectives

The objectives of this experiment are:

1. To create and configure a Virtual Machine and Docker Container.
2. To run the same workloads in both environments.
3. To measure CPU, memory, disk, network and application performance.
4. To compare the performance of the Virtual Machine and Docker Container.

---

## 3. Experimental Configuration

| Resource                 | Configuration      |
| ------------------------ | ------------------ |
| Host Operating System    | Windows            |
| Virtual Machine Platform | VMware Workstation |
| Guest Operating System   | Ubuntu             |
| Container Platform       | Docker             |
| CPU                      | 4 vCPU             |
| Memory                   | 8 GB               |
| Disk                     | 60 GB              |
| CPU Benchmark            | Sysbench           |
| Memory Benchmark         | Sysbench           |
| Disk Benchmark           | fio                |
| Network Benchmark        | iperf3             |
| Application              | FastAPI            |

## The experiment uses fixed resources and identical workloads for the VM and container comparison. The lab manual recommends keeping the VM resources fixed and applying controlled CPU and memory limits to the container.

# 4. Part A - Virtual Machine

## 4.1 VMware Workstation

VMware Workstation is used to create the Virtual Machine environment.

The virtual machine is configured with the following resources:

| Parameter | Configuration      |
| --------- | ------------------ |
| Platform  | VMware Workstation |
| Guest OS  | Ubuntu             |
| CPU       | 4 vCPU             |
| Memory    | 8 GB               |
| Disk      | 60 GB              |
| Network   | NAT / Bridged      |

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

System information is checked using:

```bash
uname -a
```

## 4.3 Benchmark Tools Installation

The required benchmark tools are installed using:

```bash
sudo apt update
sudo apt install -y sysbench fio iperf3 htop sysstat python3 python3-pip git
```

The installations are verified using:

```bash
sysbench --version
fio --version
iperf3 --version
python3 --version
git --version
```

## 4.4 CPU Benchmark

CPU performance is measured using Sysbench:

```bash
sysbench cpu --cpu-max-prime=20000 --threads=4 --time=30 run
```

The CPU benchmark is also performed with different thread counts to study scalability.

## 4.5 Memory Benchmark

Memory performance is measured using:

```bash
sysbench memory \
--memory-block-size=1M \
--memory-total-size=10G \
--threads=4 \
run
```

## 4.6 Disk Benchmark

Disk I/O performance is measured using fio.

### Sequential Write

```bash
fio --name=seq-write \
--filename=~/fio-test/testfile \
--size=2G \
--bs=1M \
--rw=write \
--direct=1 \
--iodepth=16 \
--runtime=30 \
--time_based
```

### Sequential Read

```bash
fio --name=seq-read \
--filename=~/fio-test/testfile \
--size=2G \
--bs=1M \
--rw=read \
--direct=1 \
--iodepth=16 \
--runtime=30 \
--time_based
```

### Random Read

```bash
fio --name=random-read \
--filename=~/fio-test/testfile \
--size=2G \
--bs=4k \
--rw=randread \
--direct=1 \
--iodepth=16 \
--runtime=30 \
--time_based
```

### Random Write

```bash
fio --name=random-write \
--filename=~/fio-test/testfile \
--size=2G \
--bs=4k \
--rw=randwrite \
--direct=1 \
--iodepth=16 \
--runtime=30 \
--time_based
```

## 4.7 Network Benchmark

Network performance is measured using iperf3.

Server:

```bash
iperf3 -s
```

Client:

```bash
iperf3 -c <SERVER-IP> -t 30
```

Multiple streams can be tested using:

```bash
iperf3 -c <SERVER-IP> -t 30 -P 4
```

## 4.8 FastAPI Application

A FastAPI application is used to test application performance.

The application provides:

* `/health`
* `/compute`
* `/memory`

The application is started using:

```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```

The health endpoint is tested using:

```bash
curl http://localhost:8000/health
```

Expected output:

```text
{"status":"healthy"}
```

---

# 5. Part B - Docker Container

## 5.1 Docker Container

Docker is used to create the Container environment for the second part of the experiment.

The container is configured with comparable resources.

| Parameter    | Configuration               |
| ------------ | --------------------------- |
| Platform     | Docker                      |
| Base Image   | Ubuntu 24.04                |
| CPU Limit    | 4 CPUs                      |
| Memory Limit | 8 GB                        |
| Storage      | Benchmark directory         |
| Network      | Fixed network configuration |

## 5.2 Docker Image

The benchmark Docker image is created using a Dockerfile containing the required benchmarking tools.

The image is built using:

```bash
docker build -t vm-container-benchmark -f docker/Dockerfile .
```

The image is verified using:

```bash
docker images
```

## 5.3 CPU Benchmark

The same CPU benchmark used in the VM is executed inside the container:

```bash
docker run --rm \
--cpus=4 \
--memory=8g \
vm-container-benchmark \
sysbench cpu \
--cpu-max-prime=20000 \
--threads=4 \
--time=30 \
run
```

## 5.4 Memory Benchmark

The same memory workload is executed inside the container:

```bash
docker run --rm \
vm-container-benchmark \
sysbench memory \
--memory-block-size=1M \
--memory-total-size=10G \
--threads=4 \
run
```

## 5.5 Disk Benchmark

The benchmark directory is mounted into the container:

```bash
docker run --rm \
-v ~/fio-test:/fio-test \
vm-container-benchmark \
fio --name=seq-write \
--filename=/fio-test/testfile \
--size=2G \
--bs=1M \
--rw=write \
--direct=1 \
--iodepth=16 \
--runtime=30 \
--time_based
```

The same sequential and random disk tests are performed inside the container.

## 5.6 Network Benchmark

Network performance is tested using iperf3:

```bash
iperf3 -c <SERVER-IP> -t 30
```

Multiple parallel streams can be tested using:

```bash
iperf3 -c <SERVER-IP> -t 30 -P 4
```

## 5.7 FastAPI Application

The same FastAPI application is containerized using Docker.

The image is built using:

```bash
docker build -t performance-api -f api/Dockerfile api
```

The container is started using:

```bash
docker run --rm \
--cpus=4 \
--memory=8g \
-p 8000:8000 \
performance-api
```

The API is tested using:

```bash
curl http://127.0.0.1:8000/health
```

## 5.8 API Benchmark

Apache Benchmark is used to test the FastAPI application.

Health endpoint:

```bash
ab -n 10000 -c 100 http://127.0.0.1:8000/health
```

Compute endpoint:

```bash
ab -n 1000 -c 10 http://127.0.0.1:8000/compute
```

---

# 6. Performance Comparison

The performance results obtained from both environments are compared using the following parameters:

| Performance Metric | Virtual Machine | Docker Container |
| ------------------ | --------------: | ---------------: |
| CPU Performance    |   Actual Result |    Actual Result |
| Memory Performance |   Actual Result |    Actual Result |
| Sequential Read    |   Actual Result |    Actual Result |
| Sequential Write   |   Actual Result |    Actual Result |
| Random Read        |   Actual Result |    Actual Result |
| Random Write       |   Actual Result |    Actual Result |
| Network Throughput |   Actual Result |    Actual Result |
| API Requests/sec   |   Actual Result |    Actual Result |
| API Latency        |   Actual Result |    Actual Result |
| Startup Time       |   Actual Result |    Actual Result |

The comparison is based on the actual benchmark measurements obtained during the experiment.

---

# 7. Conclusion

The performance of a Virtual Machine and a Docker Container is compared using the same workloads and benchmark tools.

CPU, memory, disk I/O, network, and application performance are measured in both environments. Startup time and scalability are also evaluated.

The collected benchmark results are used to compare the performance of Virtual Machines and Containers under similar workloads.

The final conclusion is based on the actual measurements obtained during the experiment.
