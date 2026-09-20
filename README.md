# Embedded Linux Kernel Optimization - Boot Time Reduction and Performance Tuning

Analysis and optimization of Linux boot time using `systemd-analyze` and a
service-tuning shell script.

**Result:** userspace startup reduced from **22.287 s to 7.527 s** (about 66% faster).

## Project Overview
Embedded Linux systems (routers, IoT devices, automotive and industrial controllers)
need fast startup. This project measures the boot time, finds slow services with
`systemd-analyze blame`, disables non-essential services (Bluetooth, CUPS, Avahi)
using a Bash script, then reboots and measures again.

## Repository Structure
| File / Folder | Description |
|---------------|-------------|
| `README.pdf` | Project overview (PDF) |
| `docs/Project_Report.pdf` | Full report with screenshots and results |
| `docs/Scripts_and_Commands.pdf` | All commands and scripts, explained line by line |
| `scripts/optimize_services.sh` | Disables bluetooth, cups and avahi-daemon |
| `scripts/boot_analysis.sh` | Prints boot time, slow services, memory and kernel log |
| `screenshots/` | Terminal screenshots (before and after) |

## Requirements
- Ubuntu Linux (native, VM, or WSL with systemd enabled)
- systemd, Bash and sudo access

## How to Run
```bash
git clone https://github.com/praveenmanne09/Embedded-Linux-Kernel-Optimization.git
cd Embedded-Linux-Kernel-Optimization
chmod +x scripts/*.sh

systemd-analyze                    # baseline boot time
systemd-analyze blame | head -10   # slowest services
./scripts/optimize_services.sh     # disable unneeded services
sudo reboot
systemd-analyze                    # measure again and compare
```

## Results
| Metric | Before | After |
|--------|--------|-------|
| Startup finished (userspace) | 22.287 s | 7.527 s |
| graphical.target reached | 21.861 s | 7.381 s |
| Slowest unit | dev-sdd.device (4.242 s) | landscape-client.service (3.007 s) |

> Note: measured on Ubuntu under WSL, so only the userspace phase is reported.
> Results vary between runs; see the report for details.

## Author
**Praveen Manne**  
GitHub: [praveenmanne09](https://github.com/praveenmanne09)  
LinkedIn: [praveen-manne](https://linkedin.com/in/praveen-manne-1b8902269)
