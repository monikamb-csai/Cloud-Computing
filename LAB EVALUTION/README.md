# Containerized Microservice Performance Analysis

## 📌 Project Overview

This project demonstrates the development, containerization, deployment,
communication, and performance analysis of a microservice-based application.

The application consists of three independent Flask microservices:

- Order Service
- Product Service
- User Service

Docker Compose is used to deploy and connect the services.

---

## 🏗️ System Architecture

User
  ↓
Order Service
  ↓
 ┌──────────────────┐
 ↓                  ↓
User Service    Product Service

---

## 🛠️ Technologies Used

- Python
- Flask
- Docker
- Docker Compose
- REST API
- Pandas
- Matplotlib
- PowerShell

---

## 🚀 Microservices

### 1. Order Service
Port: 5000

Handles order requests and communicates with the
User Service and Product Service.

### 2. Product Service
Port: 5001

Provides product information.

### 3. User Service
Port: 5002

Provides user information.

---

## 🐳 Containerization

Each microservice is packaged into its own Docker container.

Docker Compose creates a common network that allows
the services to communicate using service names.

---

## 🔗 Microservice Communication

The Order Service communicates with:

- User Service
- Product Service

Communication is performed using REST APIs over the
Docker Compose network.

---

## 🧪 Workload Testing

The application was tested using the following concurrency levels:

1
2
4
8
16

100 requests were generated for each concurrency level.

The following metrics were measured:

- Average Response Time
- Throughput
- Failed Requests
- CPU Usage
- Memory Usage

---

## 📊 Performance Results

### Response Time

![Response Time](performance-analysis/01_response_time.png)

### Throughput

![Throughput](performance-analysis/02_throughput.png)

### CPU Usage

![CPU Usage](performance-analysis/03_cpu_usage.png)

### Memory Usage

![Memory Usage](performance-analysis/04_memory_usage.png)

---

## 📈 Analysis

As concurrency increased, response time increased significantly
at higher workloads.

Throughput initially increased and reached its highest observed
value at concurrency 4, after which it became less consistent.

No failed requests were observed during the tested workloads.

The Order Service showed the highest observed memory usage.

---

## 📋 Observation

| Concurrency | Response Time (ms) | Throughput (req/s) | Failed |
|-------------|--------------------|--------------------|--------|
| 1 | 31.78 | 31.32 | 0 |
| 2 | 33.99 | 58.29 | 0 |
| 4 | 33.05 | 118.92 | 0 |
| 8 | 109.12 | 71.78 | 0 |
| 16 | 164.93 | 90.18 | 0 |

---

## ✅ Conclusion

The experiment demonstrates how workload intensity affects the
performance of a containerized microservice application.

The application successfully handled all tested workloads without
request failures. Higher concurrency resulted in increased response
time, while throughput did not increase proportionally at higher
workloads.

---

## 👩‍💻 Author

Monika M. Bhandari
B.E. Computer Science and AI Engineering
KLE Technological University
