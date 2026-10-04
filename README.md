# Performance Analysis of Virtual Machines and Containers

## 1. Introduction

This experiment focuses on the performance analysis of a Virtual Machine (VM) and a Docker Container. The experiment compares their performance using CPU, memory, disk I/O, network, and application-level benchmarks.

The experiments were performed on Ubuntu running on VMware Workstation and using Docker containers. Standard benchmarking tools such as Sysbench, FIO, iPerf3, and ApacheBench were used to measure system and application performance.

The main purpose is to understand how a Docker container performs compared with a Virtual Machine when both are used for similar workloads.

---

## 2. Objectives

* To measure CPU performance of a Virtual Machine and a Docker Container.
* To compare memory performance.
* To compare disk I/O performance.
* To measure network throughput.
* To benchmark a FastAPI application running in the environment.
* To observe the performance difference between VM and Container.

---

## 3. Experimental Configuration

| Parameter          | Configuration            |
| ------------------ | ------------------------ |
| Host Platform      | VMware Virtual Platform  |
| Operating System   | Ubuntu 24.04.5 LTS       |
| CPU Cores          | 4                        |
| RAM                | 7.76 GiB                 |
| Disk               | 60 GB                    |
| Docker             | Docker Container         |
| Sysbench           | 1.0.20                   |
| FIO                | 3.36                     |
| iPerf3             | 3.16                     |
| ApacheBench        | 2.3                      |
| Application Server | Uvicorn / FastAPI        |
| Container Image    | `vn-vs-container:latest` |

### System Verification

The VM has 4 CPU cores:

```text
nproc
4
```

Memory:

```text
Total:     7.761 GiB
Used:      1.361 GiB
Free:      4.201 GiB
Available: 6.401 GiB
```

Disk:

```text
/dev/sda2
Size: 59G
Used: 11G
Available: 45G
Usage: 20%
```

---

# 4. Part A - Virtual Machine

## 4.1 Virtual Machine

The Virtual Machine was created and executed using VMware Workstation. Ubuntu 24.04.5 LTS was used as the guest operating system.

The VM was configured with 4 CPU cores and approximately 7.76 GiB RAM.

---

## 4.2 Ubuntu Verification

The Ubuntu environment was verified using:

```bash
nproc
free -h
lsblk
df -h
```

The system contains:

* 4 CPU cores
* 7.76 GiB RAM
* 60 GB virtual disk
* Approximately 45 GB free disk space

---

## 4.3 Benchmark Tools Installation

The following benchmark tools were available in the VM:

```text
Sysbench 1.0.20
FIO 3.36
iPerf3 3.16
```

The FastAPI application was also successfully accessed through Uvicorn.

---

## 4.4 CPU Benchmark

The CPU benchmark was performed using Sysbench with 4 threads and a prime number limit of 2000.

Command:

```bash
sysbench cpu --cpu-max-prime=2000 --threads=4 run
```

### VM CPU Benchmark Output

```text
Number of threads: 4

Prime numbers limit: 2000

CPU speed:
    events per second: 180666.76

General statistics:
    total time: 10.0001s
    total number of events: 1806838
```

### VM CPU Result

| Parameter    |          Value |
| ------------ | -------------: |
| Threads      |              4 |
| Test Time    |      10.0001 s |
| Total Events |      1,806,838 |
| Events/sec   | **180,666.76** |

---

## 4.5 Memory Benchmark

The VM memory benchmark was performed using Sysbench.

Command:

```bash
sysbench memory --memory-block-size=1M --memory-total-size=10G --threads=4 run
```

### VM Memory Result

| Parameter        |                  Value |
| ---------------- | ---------------------: |
| Threads          |                      4 |
| Block Size       |                  1 MiB |
| Total Size       |                 10 GiB |
| Operation        |                  Write |
| Memory Bandwidth | **105,162.73 MiB/sec** |
| Total Operations |                 10,240 |

The VM achieved a memory bandwidth of **105,162.73 MiB/sec**.

---

## 4.6 Disk I/O Benchmark

FIO was used to measure disk write performance.

Command:

```bash
fio --name=vm-disk --filename=/tmp/testfile --size=10G --bs=1M --rw=write --direct=1 --iodepth=16 --runtime=30 --time_based --group_reporting
```

### VM Disk Write Result

| Parameter       |                Value |
| --------------- | -------------------: |
| Operation       |     Sequential Write |
| Block Size      |                1 MiB |
| Runtime         |               30 sec |
| IOPS            |            **1,771** |
| Bandwidth       | **1,771.86 MiB/sec** |
| Bandwidth       |         1,857 MB/sec |
| Average Latency |        **563.74 µs** |
| Maximum Latency |            19,996 µs |

The VM achieved an average disk write bandwidth of **1,771.86 MiB/sec**.

---

## 4.7 Network Benchmark

iPerf3 was used to measure network throughput.

Command:

```bash
iperf3 -c 192.168.234.130 -t 10
```

### VM Network Result

```text
0.00-10.00 sec
Transfer: 75.8 GBytes
Bitrate: 65.1 Gbits/sec
Retransmissions: 2
```

| Parameter       |              Value |
| --------------- | -----------------: |
| Test Duration   |             10 sec |
| Transfer        |            75.8 GB |
| Throughput      | **65.1 Gbits/sec** |
| Retransmissions |                  2 |

The VM achieved a network throughput of **65.1 Gbits/sec**.

---

## 4.8 FastAPI Application

The FastAPI application was tested using the following endpoints:

```text
/health
/compute
/memory
```

### Health Check

```bash
curl http://localhost:8000/health
```

Output:

```text
{"status": "healthy"}
```

### Compute Test

```bash
curl http://localhost:8000/compute
```

Output:

```text
{"result": 333332833333500000}
```

The FastAPI application was successfully running and responding to requests.

---

## 4.9 API Benchmark - `/health`

ApacheBench was used with 10,000 requests and 100 concurrent requests.

Command:

```bash
ab -n 10000 -c 100 http://127.0.0.1:8000/health
```

### Benchmark Output

| Parameter            |                 Value |
| -------------------- | --------------------: |
| Requests             |                10,000 |
| Concurrency          |                   100 |
| Test Time            |         **3.767 sec** |
| Failed Requests      |                 **0** |
| Requests/sec         |          **2,654.45** |
| Average Time/request |         **37.673 ms** |
| Transfer Rate        | **425.13 Kbytes/sec** |
| Longest Request      |             **77 ms** |

The `/health` endpoint successfully completed all **10,000 requests without failure**.

---

## 4.10 API Benchmark - `/compute`

ApacheBench was used to test the compute endpoint.

Command:

```bash
ab -n 10000 -c 100 http://127.0.0.1:8000/compute
```

### Benchmark Output

| Parameter            |                Value |
| -------------------- | -------------------: |
| Requests             |               10,000 |
| Concurrency          |                  100 |
| Test Time            |       **35.970 sec** |
| Failed Requests      |                **0** |
| Requests/sec         |           **278.01** |
| Average Time/request |       **359.705 ms** |
| Transfer Rate        | **46.15 Kbytes/sec** |
| Longest Request      |           **490 ms** |

The `/compute` endpoint successfully completed all **10,000 requests without failure**.

---

# 5. Part B - Docker Container

## 5.1 Docker Container

A Docker image named:

```text
vn-vs-container:latest
```

was successfully built.

The image was created for running the benchmarking environment.

```text
Successfully tagged vn-vs-container:latest
```

The container environment was verified using Sysbench, FIO, and iPerf3.

---

## 5.2 Container Verification

Inside the container, the following tools were verified:

```text
sysbench 1.0.20
fio-3.36
iperf3 3.16
```

The container was running on:

```text
Linux x86_64
Ubuntu 24.04 based environment
```

---

## 5.3 CPU Benchmark

Command:

```bash
sysbench cpu --cpu-max-prime=2000 --threads=4 run
```

### Container CPU Result

```text
Number of threads: 4

CPU speed:
    events per second: 180495.09
```

The container achieved approximately:

**180,495.09 events/sec**

A second recorded run gave:

**180,666.76 events/sec**

The CPU results are very close to the VM results, showing similar CPU performance.

---

## 5.4 Memory Benchmark

Command:

```bash
sysbench memory --memory-block-size=1M --memory-total-size=10G --threads=4 run
```

### Container Memory Result

| Parameter        |                  Value |
| ---------------- | ---------------------: |
| Threads          |                      4 |
| Block Size       |                  1 MiB |
| Total Size       |                 10 GiB |
| Operation        |                  Write |
| Memory Bandwidth | **119,741.15 MiB/sec** |
| Total Operations |                 10,240 |

The container achieved a memory bandwidth of **119,741.15 MiB/sec**.

---

## 5.5 Disk I/O Benchmark

FIO was used to measure container disk write performance.

Command:

```bash
fio --name=container-disk --filename=/tmp/testfile --size=10G --bs=1M --rw=write --direct=1 --iodepth=16 --runtime=30 --time_based --group_reporting
```

### Container Disk Write Result

| Parameter       |                Value |
| --------------- | -------------------: |
| Operation       |     Sequential Write |
| Block Size      |                1 MiB |
| Runtime         |               30 sec |
| IOPS            |            **1,805** |
| Bandwidth       | **1,806.31 MiB/sec** |
| Bandwidth       |         1,893 MB/sec |
| Average Latency |        **553.31 µs** |
| Maximum Latency |             5,579 µs |

The container achieved an average disk write bandwidth of **1,806.31 MiB/sec**.

---

## 5.6 Network Benchmark

The container was tested using iPerf3 against the VM network endpoint.

Command:

```bash
iperf3 -c 192.168.234.130 -t 10
```

### Container Network Result

```text
0.00-10.00 sec
Transfer: 60.2 GBytes
Bitrate: 60.2 Gbits/sec
Retransmissions: 2
```

| Parameter       |              Value |
| --------------- | -----------------: |
| Test Duration   |             10 sec |
| Transfer        |            60.2 GB |
| Throughput      | **60.2 Gbits/sec** |
| Retransmissions |                  2 |

The container achieved a network throughput of **60.2 Gbits/sec**.

---

## 5.7 FastAPI Application

The FastAPI application was successfully accessed through the container environment.

### Health Check

```bash
curl http://localhost:8000/health
```

Output:

```text
{"status": "healthy"}
```

### Compute Test

```bash
curl http://localhost:8000/compute
```

Output:

```text
{"result": 333332833333500000}
```

---

## 5.8 API Benchmark - `/health`

ApacheBench was used with 10,000 requests and 100 concurrent requests.

```bash
ab -n 10000 -c 100 http://127.0.0.1:8000/health
```

### Result

| Parameter            |                 Value |
| -------------------- | --------------------: |
| Requests             |                10,000 |
| Concurrency          |                   100 |
| Test Time            |         **3.767 sec** |
| Failed Requests      |                 **0** |
| Requests/sec         |          **2,654.45** |
| Average Time/request |         **37.673 ms** |
| Transfer Rate        | **425.13 Kbytes/sec** |
| Longest Request      |             **77 ms** |

---

## 5.9 API Benchmark - `/compute`

```bash
ab -n 10000 -c 100 http://127.0.0.1:8000/compute
```

### Result

| Parameter            |                Value |
| -------------------- | -------------------: |
| Requests             |               10,000 |
| Concurrency          |                  100 |
| Test Time            |       **35.970 sec** |
| Failed Requests      |                **0** |
| Requests/sec         |           **278.01** |
| Average Time/request |       **359.705 ms** |
| Transfer Rate        | **46.15 Kbytes/sec** |
| Longest Request      |           **490 ms** |

---

# 6. Performance Comparison

The measured results are summarized below.

| Benchmark                   |                 VM |          Container |
| --------------------------- | -----------------: | -----------------: |
| CPU Events/sec              |         180,666.76 |         180,495.09 |
| Memory Bandwidth            | 105,162.73 MiB/sec | 119,741.15 MiB/sec |
| Disk Write Bandwidth        |   1,771.86 MiB/sec |   1,806.31 MiB/sec |
| Disk Write IOPS             |              1,771 |              1,805 |
| Disk Write Avg. Latency     |          563.74 µs |          553.31 µs |
| Network Throughput          |     65.1 Gbits/sec |     60.2 Gbits/sec |
| API `/health` Requests/sec  |           2,654.45 |           2,654.45 |
| API `/health` Avg. Latency  |          37.673 ms |          37.673 ms |
| API `/compute` Requests/sec |             278.01 |             278.01 |
| API `/compute` Avg. Latency |         359.705 ms |         359.705 ms |

### Observations

* **CPU:** VM and Container show almost the same CPU performance.
* **Memory:** Container achieved higher measured memory bandwidth than the VM.
* **Disk Write:** Container achieved slightly higher write bandwidth and IOPS, with slightly lower average latency.
* **Network:** VM achieved higher network throughput than the container.
* **FastAPI `/health`:** All 10,000 requests completed successfully with no failures.
* **FastAPI `/compute`:** All 10,000 requests completed successfully with no failures.
* Overall, the container provides performance close to the VM for the tested workloads.

---

# 7. Conclusion

The experiment compared the performance of a Virtual Machine and a Docker Container using CPU, memory, disk I/O, network, and FastAPI application benchmarks.

The CPU results show that the VM and container provide very similar processing performance. The container showed higher measured memory bandwidth and slightly higher disk write performance. The VM achieved higher network throughput in the iPerf3 test.

The FastAPI application successfully responded to both `/health` and `/compute` requests, and ApacheBench completed 10,000 requests without failures.

Overall, the experimental results show that **Docker containers can provide performance close to a Virtual Machine while maintaining efficient resource usage**. The actual performance difference depends on the type of workload and the resource being measured.
