# Experiment 1: Performance Analysis of Type-1 and Type-2 Hypervisors

# Hypervisor Performance Analysis

## 1. Objective
Short explanation of what the experiment measures.

## 2. Technologies Used
- Proxmox VE – Type-1 Hypervisor
- VMware Workstation – Type-2 Hypervisor
- Ubuntu
- Sysbench

## 3. VM Configuration
| Resource | Configuration |
|---|---|
| OS | Ubuntu |
| CPU | 2 vCPU |
| RAM | 2 GB |
| Disk | 20 GB |

# PART A – PROXMOX VE

## 4. Access Proxmox
1. Connect to the network.
2. Open browser.
3. Open:
   https://<PROXMOX_IP>:8006
4. Accept certificate warning.
5. Enter username/password.
6. Click Login.

## 5. Create VM
1. Datacenter → Node
2. Click Create VM.
3. Enter VM name.
4. Select Ubuntu ISO.
5. Keep default System settings.
6. Set disk = 20 GB.
7. CPU = 2 cores.
8. Memory = 2048 MB.
9. Network = vmbr0.
10. Review → Finish.

## 6. Install Ubuntu
1. Start VM.
2. Open Console.
3. Select language.
4. Install Ubuntu.
5. Configure keyboard.
6. Select disk.
7. Set timezone.
8. Create username/password.
9. Complete installation.
10. Restart VM.

### Type-1 Hypervisor — Proxmox VE

**Execution Steps**

1. Access Proxmox Web Interface
2. Login to Proxmox
3. Create Virtual Machine
4. Configure OS
5. Configure CPU — 2 vCPU
6. Configure Memory — 2 GB
7. Configure Disk — 20 GB
8. Configure Network
9. Start VM
10. Install Ubuntu
11. Verify VM using `hostnamectl`, `lscpu`, `free -h`, `df -h`
12. Install Sysbench
13. Run CPU benchmark
14. Record results
15. Monitor VM resources
16. Shut down VM

### Type-2 Hypervisor — VMware Workstation

**Execution Steps**

1. Open VMware Workstation
2. Create New Virtual Machine
3. Select Typical Configuration
4. Select Ubuntu ISO
5. Configure VM Name
6. Configure Disk — 20 GB
7. Customize Hardware
8. Configure CPU — 2 vCPU
9. Configure Memory — 2 GB
10. Configure Network — NAT
11. Start VM
12. Install Ubuntu
13. Verify VM using `hostnamectl`, `lscpu`, `free -h`, `df -h`
14. Install Sysbench
15. Run CPU benchmark
16. Record results
17. Monitor VM resources
18. Shut down VM

## 7. Verify VM

Run:

hostnamectl
lscpu
free -h
df -h
top

Press `q` to exit `top`.

## 8. Install Sysbench

```bash
sudo apt update
sudo apt install sysbench -y
sysbench --version
