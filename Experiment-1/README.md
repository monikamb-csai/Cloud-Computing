# Experiment 1: Performance Analysis of Type-1 and Type-2 Hypervisors


# TITLE:
Hypervisor Performance Analysis


# 1. OBJECTIVES

• To understand the concept of virtualization and hypervisors.
• To study Type-1 and Type-2 hypervisors.
• To understand the working of Proxmox VE and VMware Workstation.
• To perform CPU benchmarking using Sysbench.
• To study different CPU performance metrics.
• To compare virtual machine performance.
• To understand the basic difference between virtual machines and containers.


# 2. SYSTEM ARCHITECTURE

#TYPE-1 HYPERVISOR – PROXMOX VE
```

Physical Hardware
        ↓
    Proxmox VE
        ↓
Ubuntu Virtual Machine
        ↓
Sysbench CPU Benchmark
        ↓
Performance Result

```

# TYPE-2 HYPERVISOR – VMWARE WORKSTATION
```

Physical Hardware
        ↓
    Windows OS
        ↓
VMware Workstation
        ↓
Ubuntu Virtual Machine
        ↓
Sysbench CPU Benchmark
        ↓
Performance Result

```

# 3. TYPE-1 HYPERVISOR – PROXMOX VE

Configuration:

Hypervisor       : Proxmox VE
Hypervisor Type  : Type-1
Guest OS         : Ubuntu
CPU              : 2 vCPU
Memory           : 2 GB RAM
Disk             : 20 GB
Benchmark        : Sysbench CPU

Proxmox VE operates directly on the physical hardware and is used to create and manage the Ubuntu virtual machine.


# 4. TYPE-2 HYPERVISOR – VMWARE WORKSTATION

Configuration:

Hypervisor       : VMware Workstation
Hypervisor Type  : Type-2
Host OS          : Windows
Guest OS         : Ubuntu
CPU              : 2 vCPU
Memory           : 2 GB RAM
Disk             : 20 GB
Network          : NAT
Benchmark        : Sysbench CPU

VMware Workstation runs on top of the Windows operating system and provides a virtual environment for running Ubuntu.


# 5. EXECUTION

STEP 1:
Create and start the Ubuntu virtual machine.

STEP 2:
Configure the virtual machine with 2 vCPU, 2 GB RAM and 20 GB disk.

STEP 3:
Open the Ubuntu terminal.

STEP 4:
Update the package information.

Command:

sudo apt update

STEP 5:
Install Sysbench.

Command:

sudo apt install sysbench -y

STEP 6:
Check the installed Sysbench version.

Command:

sysbench --version

STEP 7:
Run the CPU benchmark.

Command:

sysbench cpu --cpu-max-prime=20000 run

STEP 8:
Record the following performance parameters:

• Total execution time
• Total events
• Events per second
• Average latency
• Maximum latency
• 95th percentile latency


# 6. RESULTS

The following VMware values are taken from the supplied reference experiment.

Metric                         VMware Workstation
--------------------------------------------------
Sysbench Version               1.0.20
Benchmark                      CPU
Prime Number Limit             20,000
Threads                        1
Total Execution Time           10.0006 s
Total Events                   24,366
Events Per Second              2,436.05
Minimum Latency                0.40 ms
Average Latency                0.41 ms
Maximum Latency                4.39 ms
95th Percentile Latency        0.42 ms
Latency Sum                    9992.75 ms

Proxmox numerical benchmark values were not available in the supplied reference material, so they are not filled with fabricated values.


# 7. RESULT OBSERVATION

The reference VMware benchmark completed in approximately 10 seconds.

The system processed 24,366 total events and achieved approximately 2,436.05 events per second.

The average latency was 0.41 ms, while the maximum observed latency was 4.39 ms.

These values indicate the CPU performance observed during the reference Sysbench execution.


# 8. PERFORMANCE GRAPH

The graph can be created using the available VMware benchmark values.

Metrics used for the graph:

• Total Events
• Events Per Second
• Average Latency
• Maximum Latency


# 9. VM VS CONTAINER

VIRTUAL MACHINE:

A virtual machine provides a complete virtualized environment with its own guest operating system.
```
Physical Hardware
        ↓
Hypervisor
        ↓
Guest Operating System
        ↓
Application
```

CONTAINER:

A container shares the host operating system kernel while keeping the application and its dependencies isolated.
```
Physical Hardware
        ↓
Host Operating System
        ↓
Container Runtime
        ↓
Container
        ↓
Application
```

# COMPARISON:

Feature              Virtual Machine        Container
------------------------------------------------------------
Operating System     Separate guest OS      Shares host OS
Startup              Generally slower       Generally faster
Resource Usage       Higher                 Lower
Isolation            Strong                 Process-level
Usage                Full OS environment    Applications


# 10. TYPE-1 VS TYPE-2 COMPARISON

Feature                     Type-1              Type-2
------------------------------------------------------------
Example                     Proxmox VE           VMware Workstation
Runs on                     Physical hardware    Host OS
Host OS required            No                   Yes
Guest OS                    Ubuntu               Ubuntu
CPU                         2 vCPU               2 vCPU
Memory                      2 GB                 2 GB
Disk                        20 GB                20 GB
Virtualization layer        Direct hardware      Above host OS


# 11. CONCLUSION

This experiment helped in understanding virtualization and the working of Type-1 and Type-2 hypervisors.

Proxmox VE represents a Type-1 hypervisor because it operates directly on physical hardware. VMware Workstation represents a Type-2 hypervisor because it runs on top of a host operating system.

Sysbench was used to study CPU performance using parameters such as execution time, total events, events per second and latency.

The experiment also helped in understanding the difference between virtual machines and containers. Virtual machines require a separate guest operating system, whereas containers share the host operating system kernel and generally require fewer resources.


# 12. AUTHOR

Monika M. Bhandari



K.L.E. Technological University, Hubballi
