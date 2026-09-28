
# Experiment 2 : PERFORMANCE ANALYSIS OF VIRTUAL MACHINES AND CONTAINERS

# Experiment 2: Performance Analysis of Virtual Machines and Containers

# VM vs Container Performance Analysis

## 1. Objective

Measure and compare the performance of Virtual Machines and Docker Containers using CPU, memory, disk, network, and application workloads.

## 2. Technologies Used

* VMware Workstation – Virtual Machine
* Docker – Container
* Ubuntu
* Sysbench – CPU and Memory
* fio – Disk I/O
* iperf3 – Network
* FastAPI – Application
* Python
* Pandas
* Matplotlib

## 3. VM Configuration

| **Resource** | **Configuration** |
| ------------ | ----------------- |
| OS           | Ubuntu            |
| CPU          | 4 vCPU            |
| RAM          | 8 GB              |
| Disk         | 60 GB             |
| Network      | NAT / Bridged     |

# PART A – VIRTUAL MACHINE

## 4. Create VM

1. Open VMware Workstation.
2. Click Create New Virtual Machine.
3. Select Typical.
4. Select Ubuntu ISO.
5. Enter VM name.
6. Set disk = 60 GB.
7. CPU = 4 cores.
8. Memory = 8 GB.
9. Configure network.
10. Finish VM creation.

## 5. Install Ubuntu

1. Start VM.
2. Select language.
3. Install Ubuntu.
4. Configure keyboard.
5. Select disk.
6. Set timezone.
7. Create username/password.
8. Complete installation.
9. Restart VM.

## 6. Verify VM

Run:

```bash
hostnamectl
nproc
free -h
lsblk
df -h
uname -a
```

## 7. Install Required Tools

```bash
sudo apt update
sudo apt install sysbench fio iperf3 htop iotop sysstat python3 python3-pip git -y
```

Check versions:

```bash
sysbench --version
fio --version
iperf3 --version
python3 --version
git --version
```

# PART B – DOCKER CONTAINER

## 8. Install Docker

```bash
sudo apt update
sudo apt install docker.io -y
```

Start Docker:

```bash
sudo systemctl enable docker
sudo systemctl start docker
```

Check Docker:

```bash
docker --version
```

## 9. Test Docker

Run:

```bash
docker run --rm hello-world
```

Expected result:

```text
Hello from Docker!
```

## 10. Create Benchmark Project

```bash
mkdir -p ~/vm-vs-container-performance
cd ~/vm-vs-container-performance
```

Check location:

```bash
pwd
```

## 11. Create Docker Image

Create:

```text
docker/Dockerfile
```

Build image:

```bash
docker build -t vm-container-benchmark -f docker/Dockerfile .
```

Verify:

```bash
docker images
```

# PART C – BASELINE MEASUREMENT

## 12. Run CPU Baseline

Run inside VM:

```bash
sysbench cpu --cpu-max-prime=20000 --threads=4 --time=30 run
```

Record:

* Total time
* Events per second
* CPU time

Run the same test inside the Docker container.

# PART D – CPU PERFORMANCE

## 13. CPU Benchmark

Test different thread counts:

```text
1 thread
2 threads
4 threads
8 threads
```

Example:

```bash
sysbench cpu --cpu-max-prime=20000 --threads=4 --time=30 run
```

Repeat each test 10 times.

Record:

* Execution time
* Events/sec
* CPU performance

## 14. Monitor CPU

Run:

```bash
htop
```

or:

```bash
vmstat 1
```

# PART E – MEMORY PERFORMANCE

## 15. Memory Benchmark

Run:

```bash
sysbench memory --memory-block-size=1M --memory-total-size=10G --threads=4 run
```

Repeat 10 times in:

* Virtual Machine
* Docker Container

Record memory transfer rate and execution time.

# PART F – DISK PERFORMANCE

## 16. Create Test Directory

```bash
mkdir -p ~/fio-test
```

## 17. Sequential Write Test

```bash
fio --name=seqwrite --filename=~/fio-test/testfile \
--size=2G --bs=1M --rw=write --direct=1 \
--iodepth=16 --runtime=30 --time_based
```

## 18. Sequential Read Test

```bash
fio --name=seqread --filename=~/fio-test/testfile \
--size=2G --bs=1M --rw=read --direct=1 \
--iodepth=16 --runtime=30 --time_based
```

## 19. Random Write Test

```bash
fio --name=randwrite --filename=~/fio-test/testfile \
--size=2G --bs=4k --rw=randwrite --direct=1 \
--iodepth=16 --runtime=30 --time_based
```

## 20. Random Read Test

```bash
fio --name=randread --filename=~/fio-test/testfile \
--size=2G --bs=4k --rw=randread --direct=1 \
--iodepth=16 --runtime=30 --time_based
```

Record:

* IOPS
* Bandwidth
* Latency

# PART G – NETWORK PERFORMANCE

## 21. Start iperf3 Server

On server:

```bash
iperf3 -s
```

Find IP:

```bash
ip addr
```

## 22. Run iperf3 Client

On client:

```bash
iperf3 -c <SERVER-IP> -t 30
```

Parallel test:

```bash
iperf3 -c <SERVER-IP> -t 30 -P 4
```

Record:

* Bandwidth
* Transfer
* Network performance

# PART H – FASTAPI APPLICATION

## 23. Create FastAPI Application

Create:

```text
api/main.py
```

Run:

```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```

## 24. Test Application

Open another terminal:

```bash
curl http://localhost:8000/health
```

Test compute endpoint:

```bash
curl http://localhost:8000/compute
```

# PART I – DOCKERIZE FASTAPI

## 25. Create Requirements File

Create:

```text
api/requirements.txt
```

Add:

```text
fastapi
uvicorn
```

## 26. Create API Dockerfile

Create:

```text
api/Dockerfile
```

Build image:

```bash
docker build -t performance-api -f api/Dockerfile api
```

## 27. Run FastAPI Container

```bash
docker run --rm --cpus=4 --memory=8g -p 8000:8000 performance-api
```

Test:

```bash
curl http://localhost:8000/health
```

# PART J – APPLICATION PERFORMANCE

## 28. Install Apache Benchmark

```bash
sudo apt install apache2-utils -y
```

## 29. Test Health API

```bash
ab -n 10000 -c 100 http://127.0.0.1:8000/health
```

## 30. Test Compute API

```bash
ab -n 1000 -c 10 http://127.0.0.1:8000/compute
```

Record:

* Requests/sec
* Latency
* Failed requests
* Connection time

# PART K – STARTUP TIME

## 31. Measure Container Startup

```bash
time docker run --rm performance-api
```

Record:

* Container startup time
* Application ready time

# PART L – SCALABILITY

## 32. CPU Scalability

Run CPU tests with:

```text
1 thread
2 threads
4 threads
8 threads
```

Compare VM and container performance.

## 33. API Scalability

Run different workloads:

```bash
wrk -t1 -c10 -d30s http://127.0.0.1:8000/health
```

```bash
wrk -t2 -c50 -d30s http://127.0.0.1:8000/health
```

```bash
wrk -t4 -c100 -d30s http://127.0.0.1:8000/health
```

```bash
wrk -t4 -c200 -d30s http://127.0.0.1:8000/health
```

# PART M – AUTOMATION

## 34. Create Benchmark Scripts

Create:

```text
scripts/run_cpu.sh
scripts/run_memory.sh
scripts/run_disk.sh
scripts/run_network.sh
```

Make executable:

```bash
chmod +x scripts/*.sh
```

Run:

```bash
./scripts/run_cpu.sh
```

# PART N – RESULTS

## 35. Store Raw Results

Save results in:

```text
results/raw/
```

Store:

* CPU results
* Memory results
* Disk results
* Network results
* Application results
* Startup results

## 36. Process Results

Save processed CSV files in:

```text
results/processed/
```

Use Pandas to calculate:

* Mean
* Median
* Minimum
* Maximum
* Standard deviation

## 37. Generate Graphs

Save graphs in:

```text
results/figures/
```

Generate graphs for:

* CPU
* Memory
* Disk
* Network
* Application
* Startup
* Scalability

# PART O – COMPARISON

## 38. Compare VM and Container

Compare:

| **Metric**         | **VM**         | **Container**  |
| ------------------ | -------------- | -------------- |
| CPU Performance    | Measured value | Measured value |
| Memory Performance | Measured value | Measured value |
| Disk Read          | Measured value | Measured value |
| Disk Write         | Measured value | Measured value |
| Network            | Measured value | Measured value |
| API Requests/sec   | Measured value | Measured value |
| API Latency        | Measured value | Measured value |
| Startup Time       | Measured value | Measured value |

Use only measured experimental values.

# PART P – GITHUB

## 39. Organize Project

```text
vm-vs-container-performance/
│
├── docs/
├── vm/
├── docker/
├── api/
├── workloads/
├── scripts/
├── results/
│   ├── raw/
│   ├── processed/
│   └── figures/
├── analysis/
├── README.md
└── .gitignore
```

## 40. Initialize Git

```bash
git init
git add .
git commit -m "Add VM vs Container performance analysis"
```

## 41. Set Main Branch

```bash
git branch -M main
```

## 42. Connect GitHub

```bash
git remote add origin <GITHUB-REPOSITORY-URL>
```

## 43. Push Project

```bash
git push -u origin main
```

## 44. Verify GitHub

1. Open GitHub repository.
2. Check README.md.
3. Check experiment files.
4. Check results.
5. Check graphs.
6. Verify all files are uploaded.
