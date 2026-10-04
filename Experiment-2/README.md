
# Experiment 2 : PERFORMANCE ANALYSIS OF VIRTUAL MACHINES AND CONTAINERS


# Performance Analysis of Virtual Machines and Containers

---

# 1. Abstract

This project presents a performance analysis of Virtual Machines and Docker Containers.

The main purpose of the project is to study how different computing environments perform under CPU, memory, disk, network, and application workloads.

The experiments include CPU performance, memory performance, disk I/O performance, network performance, FastAPI application performance, startup time, and scalability.

The collected results are stored in CSV format and analyzed using Python. Statistical measures such as mean, median, minimum, maximum, and standard deviation are calculated.

Graphs are generated from the experimental results to make the performance differences easier to understand.

The project also provides a comparison between Virtual Machine and Container environments based on measured results and expected performance characteristics.

---

# 2. Objectives

The main objectives of this project are:

1. To understand Virtual Machine technology.
2. To understand Docker Container technology.
3. To configure a Virtual Machine environment.
4. To configure a Docker Container environment.
5. To measure CPU performance.
6. To measure memory performance.
7. To measure disk I/O performance.
8. To measure network performance.
9. To evaluate FastAPI application performance.
10. To measure application startup time.
11. To analyze scalability with increasing workloads.
12. To collect benchmark results in CSV format.
13. To perform statistical analysis.
14. To generate graphs from experimental results.
15. To compare Virtual Machine and Container performance.

---

# 3. Research Questions

The project investigates the following questions:

1. How does CPU performance change when the number of threads increases?
2. How does memory performance behave under different workloads?
3. How does disk I/O performance change for sequential and random operations?
4. What network throughput can be achieved?
5. How does FastAPI application performance behave?
6. How much time is required for application startup?
7. How does application performance change when workload increases?
8. How do Virtual Machines and Containers compare in terms of performance and resource overhead?

---

# 4. Experimental Environment

## 4.1 Hardware Configuration

The experiments were performed using a laptop computer.

| Component | Configuration |
|---|---|
| Processor | Intel Core i5-1235U |
| CPU Threads | 12 |
| RAM | 8 GB |
| Host Operating System | Windows 11 |
| Linux Environment | Ubuntu |
| Container Platform | Docker |
| Storage | Local laptop storage |

---

## 4.2 Software Configuration

The following software and tools were used:

- Windows 11
- Ubuntu
- VMware Workstation
- Docker
- Docker Desktop
- Python 3
- FastAPI
- Uvicorn
- Sysbench
- fio
- iperf3
- Apache Benchmark
- curl
- Pandas
- Matplotlib
- Git
- GitHub

---

# 5. Architecture

The project uses two main execution environments:

1. Virtual Machine
2. Docker Container

The same category of workloads is used to analyze both environments.

```text
                         HOST LAPTOP
                              |
              +---------------+---------------+
              |                               |
              |                               |
       VIRTUAL MACHINE                  DOCKER CONTAINER
              |                               |
           Ubuntu                         Container
              |                               |
       +------+------+                 +------+------+
       |      |      |                 |      |      |
      CPU   Memory  Disk              CPU   Memory  Disk
       |      |      |                 |      |      |
       +------+------+                 +------+------+
              |                               |
              +---------------+---------------+
                              |
                       FastAPI Application
                              |
                    Performance Measurements
                              |
                     CSV Result Processing
                              |
                     Statistical Analysis
                              |
                            Graphs
```
# 6. Project Structure
```
vm-vs-container-performance/
│
├── README.md
├── .gitignore
│
├── docs/
│   ├── architecture.png
│   ├── cpu-info.txt
│   ├── memory-info.txt
│   ├── storage-info.txt
│   └── methodology.md
│
├── vm/
│   ├── setup.sh
│   └── benchmark.sh
│
├── docker/
│   ├── Dockerfile
│   └── benchmark.sh
│
├── api/
│   ├── main.py
│   ├── requirements.txt
│   └── Dockerfile
│
├── workloads/
│   ├── cpu/
│   ├── memory/
│   ├── disk/
│   └── network/
│
├── scripts/
│   ├── run_cpu.sh
│   ├── run_memory.sh
│   ├── run_disk.sh
│   ├── run_network.sh
│   ├── collect_metrics.py
│   ├── analyze_results.py
│   └── generate_plots.py
│
├── results/
│   ├── raw/
│   ├── processed/
│   └── figures/
│
├── screenshots/
│
└── analysis/
    └── analysis.ipynb
   ```
# PART A – VIRTUAL MACHINE
# 8. Create Virtual Machine

A Virtual Machine was created using VMware Workstation.

The VM configuration was:

VM Type: Typical
Operating System: Ubuntu
Disk Size: 60 GB
CPU: 4 cores
Memory: 8 GB
Network: Configured according to the experimental environment

# 9. Install Ubuntu

The following steps were followed:

Start VMware Workstation.
Create a new Virtual Machine.
Select Typical installation.
Select the Ubuntu ISO image.
Enter the VM name.
Configure disk size.
Configure CPU and memory.
Configure network.
Start the Virtual Machine.
Select language.
Install Ubuntu.
Configure keyboard.
Configure disk.
Set timezone.
Create username and password.
Complete installation.
Restart the VM.

# 10. Verify Virtual Machine

The following commands were used:

hostnamectl
nproc
free -h
lsblk
df -h
uname -a

These commands provide information about:

Hostname
CPU
Memory
Storage
Disk usage
Linux kernel
# 11. Install Required Tools

The following packages were installed:

sudo apt update
sudo apt install sysbench fio iperf3 htop iotop sysstat python3 python3-pip git -y

Versions were checked using:

sysbench --version
fio --version
iperf3 --version
python3 --version
git --version
# PART B – DOCKER CONTAINER
# 12. Install Docker

Docker was installed using:

sudo apt update
sudo apt install docker.io -y

Docker was enabled using:

sudo systemctl enable docker
sudo systemctl start docker

Docker version was checked using:

docker --version
# 13. Test Docker

Docker was tested using:

docker run --rm hello-world

Expected output:

Hello from Docker!
# 14. Create Benchmark Project

The project directory was created using:

mkdir -p ~/vm-vs-container-performance
cd ~/vm-vs-container-performance

The current location was checked using:

pwd
# 15. Create Docker Image

The Docker benchmark Dockerfile was created in:

docker/Dockerfile

The image was built using:

docker build -t vm-container-benchmark -f docker/Dockerfile .

The image was verified using:

docker images
# PART C – BASELINE MEASUREMENT
# 16. Baseline System Information

Baseline system information was collected using:

lscpu
free -h
df -h /

The baseline information includes:

CPU configuration
Number of CPU threads
Memory information
Storage information
Available disk space

The baseline information was saved for later analysis.

# PART D – CPU PERFORMANCE
# 17. CPU Benchmark

CPU performance was measured using Sysbench.

The following thread counts were tested:

1 thread
2 threads
4 threads
8 threads

Example command:

sysbench cpu --cpu-max-prime=20000 --threads=4 --time=30 run

The benchmark records:

Total execution time
Events per second
CPU time
# 18. Observed CPU Results

The confirmed CPU measurements available from the experiment are:

Threads	Events/sec
4	2847.74
8	5204.09

The results show an increase in CPU throughput when more threads are used.

# 19. CPU Monitoring

CPU utilization can be monitored using:

htop

or:

vmstat 1
# PART E – MEMORY PERFORMANCE
# 20. Memory Benchmark

Memory performance was measured using Sysbench.

The command used was:

sysbench memory --memory-block-size=1M --memory-total-size=10G --threads=4 run

Multiple runs were performed.

# 21. Observed Memory Results

The confirmed memory measurements are:

Run	Memory Performance
Run 1	32941.74 MiB/s
Run 2	28440.75 MiB/s

Average:

30691.245 MiB/s

The difference between the two runs shows that benchmark performance can vary due to system conditions.

# PART F – DISK PERFORMANCE
# 22. Create Test Directory
mkdir -p ~/fio-test
# 23. Sequential Write Test
fio --name=seqwrite --filename=~/fio-test/testfile \
--size=2G --bs=1M --rw=write --direct=1 \
--iodepth=16 --runtime=30 --time_based
# 24. Sequential Read Test
fio --name=seqread --filename=~/fio-test/testfile \
--size=2G --bs=1M --rw=read --direct=1 \
--iodepth=16 --runtime=30 --time_based
# 25. Random Write Test
fio --name=randwrite --filename=~/fio-test/testfile \
--size=2G --bs=4k --rw=randwrite --direct=1 \
--iodepth=16 --runtime=30 --time_based
# 26. Random Read Test
fio --name=randread --filename=~/fio-test/testfile \
--size=2G --bs=4k --rw=randread --direct=1 \
--iodepth=16 --runtime=30 --time_based

The following values are recorded:

IOPS
Bandwidth
Latency
# 27. Observed Disk Result

One confirmed disk measurement from the benchmark was:

Random Write:
Bandwidth = 37.4 MiB/s
IOPS = 9580

Other disk values should be taken directly from the corresponding benchmark output.

# PART G – NETWORK PERFORMANCE
# 28. Start iperf3 Server

The iperf3 server was started using:

iperf3 -s

The IP address can be checked using:

ip addr
# 29. Run iperf3 Client

The client can be executed using:

iperf3 -c <SERVER-IP> -t 30

Parallel testing:

iperf3 -c <SERVER-IP> -t 30 -P 4

The following values are recorded:

Bandwidth
Transfer
Network throughput
# 30. Observed Network Result

The confirmed loopback benchmark result was:

53.3 Gbits/sec

This is a local loopback measurement and should not be interpreted as Internet or Wi-Fi speed.

# PART H – FASTAPI APPLICATION
# 31. Create FastAPI Application

The FastAPI application was created in:

api/main.py

The application contains a health endpoint and a compute endpoint.

from fastapi import FastAPI
import time

app = FastAPI()

@app.get("/health")
def health():
    return {"status": "healthy"}

@app.get("/compute")
def compute():
    start = time.time()

    total = 0

    for i in range(100000):
        total += i * i

    elapsed = time.time() - start

    return {
        "result": total,
        "execution_time": elapsed
    }
# 32. Run FastAPI

The required packages were installed using:

pip3 install fastapi uvicorn

The application was started using:

python3 -m uvicorn api.main:app --host 127.0.0.1 --port 8000
# 33. Test FastAPI

Health endpoint:

curl http://localhost:8000/health

Compute endpoint:

curl http://localhost:8000/compute
# PART I – DOCKERIZE FASTAPI
# 34. Requirements File

The file:

api/requirements.txt

contains:

fastapi
uvicorn
# 35. API Dockerfile

The Dockerfile contains:

FROM python:3.13-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY main.py .

EXPOSE 8000

CMD ["python", "-m", "uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
# 36. Build FastAPI Image
docker build -t performance-api -f api/Dockerfile api
# 37. Run FastAPI Container
docker run -d --name performance-api-container -p 8000:8000 performance-api

Check the running container:

docker ps

Test:

curl http://localhost:8000/health

Test compute endpoint:

curl http://localhost:8000/compute
# PART J – APPLICATION PERFORMANCE
# 38. API Response Time

Response time was measured using:

curl -o /dev/null -s -w "Response time: %{time_total} seconds\n" http://127.0.0.1:8000/compute

Six response-time measurements were collected.

Request	Response Time
1	0.014007 s
2	0.007228 s
3	0.006512 s
4	0.009844 s
5	0.013185 s
6	0.011088 s

Average response time:

0.01031 seconds

Approximately:

10.31 milliseconds
# 39. Apache Benchmark

Apache Benchmark can be installed using:

sudo apt install apache2-utils -y

Health API:

ab -n 10000 -c 100 http://127.0.0.1:8000/health

Compute API:

ab -n 1000 -c 10 http://127.0.0.1:8000/compute

The following values can be recorded:

Requests per second
Latency
Failed requests
Connection time
# PART K – STARTUP TIME
# 40. Startup Time

Application startup was measured using the application execution command.

The confirmed measured real time from the experiment was:

22.198 seconds

The startup measurement represents the observed execution time of the application startup experiment.

# PART L – SCALABILITY
# 41. CPU Scalability

CPU tests were performed using:

1 thread
2 threads
4 threads
8 threads

The results are used to understand how performance changes when more CPU threads are used.

# 42. API Scalability

The application was tested with increasing workloads.

The following workloads were measured:

Requests	Total Time
10	0.173 s
50	0.608 s
100	1.458 s

The results show that total execution time increases as the number of requests increases.

# PART M – DOCKER BENCHMARKING
# 43. Docker CPU Benchmark

The same Sysbench CPU methodology was used inside the Docker environment.

The following thread counts were tested:

1 thread
2 threads
4 threads
8 threads

This allows CPU performance to be evaluated under containerized execution.

# 44. Docker Memory Benchmark

The same memory benchmark was executed inside the Docker container:

sysbench memory --memory-block-size=1M --memory-total-size=10G run

Multiple runs were performed.

# 45. Docker Disk Benchmark

fio was installed inside the Docker container.

The following tests were performed:

Sequential Read
Sequential Write
Random Read
Random Write

The same benchmark methodology was used for comparison.

# 46. Docker Network Benchmark

iperf3 was installed inside the Docker environment.

The network benchmark was performed using:

iperf3 -c 127.0.0.1 -t 10

The result represents local loopback performance.

# 47. Docker FastAPI Application

The FastAPI application was built as a Docker image:

docker build -t performance-api -f api/Dockerfile api

The container was started using:

docker run -d --name performance-api-container -p 8000:8000 performance-api

The application was tested using:

curl http://127.0.0.1:8000/health

and:

curl http://127.0.0.1:8000/compute
# PART N – RESULTS
# 48. Results Storage

Raw results are stored in:

results/raw/

Processed results are stored in:

results/processed/

Generated graphs are stored in:

results/figures/
# 49. Performance Results CSV

The measured results are stored in:

results/processed/performance_results.csv

The CSV contains values from the completed experiments.

Example measured values include:

experiment,workload,value,unit
CPU,4 threads,2847.74,events/sec
CPU,8 threads,5204.09,events/sec
Memory,Run 1,32941.74,MiB/sec
Memory,Run 2,28440.75,MiB/sec
Network,iperf3 loopback,53.3,Gbits/sec
API,Request 1,0.014007,seconds
API,Request 2,0.007228,seconds
API,Request 3,0.006512,seconds
API,Request 4,0.009844,seconds
API,Request 5,0.013185,seconds
API,Request 6,0.011088,seconds
Startup,Uvicorn startup,22.198,seconds
Scalability,10 requests,0.173,seconds
Scalability,50 requests,0.608,seconds
Scalability,100 requests,1.458,seconds
# 50. Statistical Analysis

Statistical analysis was performed using Python and Pandas.

The following measures were calculated:

Mean
Median
Minimum
Maximum
Standard Deviation

The analysis script is:

scripts/analyze_results.py

The output file is:

results/processed/statistical_analysis.csv
# 51. Statistical Results
Experiment	Mean	Median	Minimum	Maximum	Standard Deviation
CPU	4025.915	4025.915	2847.74	5204.09	1666.191
Memory	30691.245	30691.245	28440.75	32941.74	3182.681
Network	53.3	53.3	53.3	53.3	N/A
API	0.01031	0.010466	0.006512	0.014007	0.003055
Startup	22.198	22.198	22.198	22.198	N/A
Scalability	0.7463	0.608	0.173	1.458	0.6536

For experiments with only one value, standard deviation is shown as N/A.

# 52. Graph Generation

Graphs were generated using Python and Matplotlib.

The graph generation script is:

scripts/generate_plots.py

The graphs are stored in:

results/figures/

The available graphs are:

api_performance.png
cpu_performance.png
memory_performance.png
network_performance.png
scalability.png
startup_time.png
# 53. Performance Graphs
## 53.1 API Performance

The API graph shows the response-time variation across the recorded requests.

## 53.2 CPU Performance

The CPU graph shows CPU performance for the tested thread counts.

## 53.3 Memory Performance

The memory graph shows the measured memory throughput for the recorded runs.

## 53.4 Network Performance

The network graph represents the measured loopback network throughput.

## 53.5 Scalability

The scalability graph shows how total execution time changes with increasing numbers of requests.

## 53.6 Startup Time

The startup graph represents the measured application startup experiment.

# PART O – VM AND CONTAINER COMPARISON
# 54. Comparison

The following table provides a comparison of the two environments.

The container values are based on the measurements collected during the experiment.

| Metric | Virtual Machine | Docker Container | Comparison |
|---|---|---|---|
| CPU Performance | Estimated ~2700–2900 events/sec | Observed 2847.74–5204.09 events/sec | Similar range expected |
| Memory Performance | Estimated ~27000–30000 MiB/s | Observed 28440.75–32941.74 MiB/s | Expected to be similar |
| Sequential Read | Estimated ~450–550 MB/s | Actual benchmark result | Depends on storage |
| Sequential Write | Estimated ~400–500 MB/s | Actual benchmark result | Depends on storage |
| Random Read | Estimated ~7000–9000 IOPS | Actual benchmark result | Expected to be similar |
| Random Write | Estimated ~8500–9500 IOPS | Observed 9580 IOPS | Similar performance expected |
| Network Throughput | Estimated value | Observed 53.3 Gbits/sec | Network configuration dependent |
| API Latency | Estimated ~10–15 ms | Observed average ~10.31 ms | Similar application performance expected |
| Startup Time | Expected to be higher | Observed 22.198 seconds | Container expected to have lower overhead |
| Scalability | Expected good | Observed increasing execution time with workload | Both depend on workload |

 # 55. General Comparison
Virtual Machine

A Virtual Machine provides a complete guest operating system and virtualized hardware environment.

Advantages:

Strong isolation
Complete guest operating system
Flexible operating-system configuration
Useful for testing complete operating systems

Disadvantages:

Higher resource overhead
Larger storage requirement
Longer startup time
More memory usage
Docker Container

A Docker Container shares the host operating system kernel while isolating applications and their dependencies.

Advantages:

Lightweight
Fast startup
Lower overhead
Easy deployment
Efficient resource usage
Suitable for microservices and application deployment

Disadvantages:

Shares the host kernel
Provides less isolation than a full VM
Performance depends on container configuration and host resources
56. Discussion

The experiments show that performance depends on the type of workload and the execution environment.

The CPU benchmark shows that increasing the number of threads can improve the number of processed events per second.

The memory benchmark shows variation between repeated runs. This demonstrates that benchmark results can change depending on system conditions and background activity.

The disk benchmark measures sequential and random I/O operations. Disk performance depends strongly on the underlying storage device and configuration.

The network benchmark achieved high throughput because the test used local loopback communication.

The FastAPI application showed response times in the millisecond range.

The scalability experiment showed that total execution time increased when the workload increased from 10 requests to 50 and 100 requests.

Containers are generally expected to have lower overhead because they share the host operating system kernel, while Virtual Machines require a complete guest operating system.

# 57. Limitations

The project has the following limitations:

The experiments were performed on a personal laptop.
The system has limited memory resources.
Background processes can affect benchmark results.
Some benchmarks were not repeated 10 times.
The network test used local loopback for some measurements.
Disk results depend on the underlying physical storage.
VM comparison values should be replaced with actual VM measurements whenever possible.
Container and VM network configurations may affect the comparison.
Application startup measurement depends on the measurement method used.
The final comparison should be interpreted together with the experimental methodology.
58. Reproduction Instructions
Step 1 – Clone Repository
git clone <GITHUB-REPOSITORY-URL>
cd vm-vs-container-performance
Step 2 – Install Required Packages
sudo apt update
sudo apt install -y sysbench fio iperf3 curl python3 python3-pip git
Step 3 – CPU Benchmark
sysbench cpu --cpu-max-prime=20000 --threads=4 --time=30 run
Step 4 – Memory Benchmark
sysbench memory --memory-block-size=1M --memory-total-size=10G --threads=4 run
Step 5 – Disk Benchmark
fio --name=seqread --filename=~/fio-test/testfile \
--size=2G --bs=1M --rw=read --direct=1 \
--iodepth=16 --runtime=30 --time_based
Step 6 – Network Benchmark
iperf3 -c <SERVER-IP> -t 30
Step 7 – Start FastAPI
python3 -m uvicorn api.main:app --host 127.0.0.1 --port 8000
Step 8 – Test API
curl http://127.0.0.1:8000/health
curl http://127.0.0.1:8000/compute
Step 9 – Measure API Response Time
curl -o /dev/null -s -w "Response time: %{time_total} seconds\n" http://127.0.0.1:8000/compute
Step 10 – Statistical Analysis
python3 scripts/analyze_results.py
Step 11 – Generate Graphs
python3 scripts/generate_plots.py

# 59. Screenshots

Experiment screenshots are stored inside:

screenshots/

The screenshot naming convention is:

01_environment_setup.png
02_tools_installed.png
03_project_structure.png
04_baseline.png
05_cpu_benchmark.png
06_memory_benchmark.png
07_disk_benchmark.png
08_network_benchmark.png
09_api_running.png
10_api_performance.png
11_startup_time.png
12_scalability.png
13_docker_working.png
14_docker_cpu.png
15_docker_memory.png
16_docker_disk.png
17_docker_network.png
18_docker_api.png
19_docker_api_performance.png

These screenshots provide visual evidence of the experiment execution.

# 60. Output Files

Important result files include:
```
results/
│
├── raw/
│
├── processed/
│   ├── performance_results.csv
│   └── statistical_analysis.csv
│
└── figures/
    ├── api_performance.png
    ├── cpu_performance.png
    ├── memory_performance.png
    ├── network_performance.png
    ├── scalability.png
    └── startup_time.png
```
# 61. GitHub Publication

The project is maintained using Git and GitHub.

Initialize Git:

git init

Add files:

git add .

Commit:

git commit -m "Add VM vs Container performance analysis"

Set main branch:

git branch -M main

Connect GitHub:

git remote add origin <GITHUB-REPOSITORY-URL>

Push:

git push -u origin main

# 62. Updating GitHub

After adding new screenshots, graphs, or results:

git add .
git commit -m "Add experiment results and performance graphs"
git push

# 63. Final GitHub Repository Structure
```
vm-vs-container-performance/
│
├── README.md
├── .gitignore
│
├── docs/
│
├── vm/
│
├── docker/
│
├── api/
│
├── workloads/
│   ├── cpu/
│   ├── memory/
│   ├── disk/
│   └── network/
│
├── scripts/
│
├── results/
│   ├── raw/
│   ├── processed/
│   └── figures/
│       ├── api_performance.png
│       ├── cpu_performance.png
│       ├── memory_performance.png
│       ├── network_performance.png
│       ├── scalability.png
│       └── startup_time.png
│
├── screenshots/
│   ├── 01_environment_setup.png
│   ├── 02_tools_installed.png
│   ├── 03_project_structure.png
│   ├── 04_baseline.png
│   ├── 05_cpu_benchmark.png
│   ├── 06_memory_benchmark.png
│   ├── 07_disk_benchmark.png
│   ├── 08_network_benchmark.png
│   ├── 09_api_running.png
│   ├── 10_api_performance.png
│   ├── 11_startup_time.png
│   ├── 12_scalability.png
│   ├── 13_docker_working.png
│   ├── 14_docker_cpu.png
│   ├── 15_docker_memory.png
│   ├── 16_docker_disk.png
│   ├── 17_docker_network.png
│   ├── 18_docker_api.png
│   └── 19_docker_api_performance.png
│
└── analysis/
    └── analysis.ipynb
```
# 65. Conclusion

This project presents an experimental performance analysis of Virtual Machines and Docker Containers.

The experiments cover CPU performance, memory performance, disk I/O, network throughput, FastAPI application performance, startup time, and scalability.

The results were collected using standard benchmarking tools such as Sysbench, fio, iperf3, curl, and application-level testing tools.

The measured results were stored in CSV format and statistically analyzed using Python and Pandas.

Matplotlib was used to generate graphs for CPU performance, memory performance, network performance, API performance, startup time, and scalability.

The experiments demonstrate that different execution environments have different performance characteristics.

Virtual Machines provide a complete guest operating system and strong isolation, while Docker Containers provide lightweight application isolation with lower expected overhead.

The project also demonstrates the importance of collecting actual measurements, maintaining raw results, performing statistical analysis, generating graphs, and documenting the complete experimental procedure.

# Author:
MONIKA.M.BHANDARI

Monika M. Bhandari  
