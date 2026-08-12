# 🚀 Custom Diet CachyOS Kernel (AMD Zen 3 / Lenovo IdeaPad 5 Pro)

Automated, high-performance CachyOS kernel builds optimized for **AMD Zen 3** laptops and tailored via `modprobed-db` for minimal binary bloat and maximum responsiveness.

---

## 🎯 Target Hardware & System Specifications

| Parameter | Targeted Specification |
| :--- | :--- |
| **Architecture** | `x86_64` (AMD Zen 3 / `znver3`) |
| **Tested Laptop Model** | **Lenovo IdeaPad 5 Pro 14ACN6** |
| **CPU Family** | AMD Ryzen 5000 Series Mobile (e.g., Ryzen 7 5800U / 5600U) |
| **GPU Support** | Integrated AMD Radeon Graphics (Cezanne / Vega) |
| **Target Distribution** | Arch Linux / CachyOS / Arch-based distributions |

---

## ⚙️ Kernel Configuration & Optimizations

This kernel is compiled using **Clang/LLVM** with the following optimized flags:

```ini
### CPU Scheduler
_cpusched="bore"
# Burst-Oriented Response Enhancer (BORE) scheduler tuned for smooth desktop responsiveness under high CPU loads.

### Microarchitecture Optimizations
_processor_opt="znver3"
# Compiler targeting znver3 flags (AVX2, FMA, BMI2, SHA) specifically for AMD Zen 3 cores.

### Link-Time Optimization (LTO)
_use_llvm_lto="full"
# Full Link-Time Optimization via LLVM/LLD for maximum inter-module inlining and performance.

### Compiler Flags
_cc_harder="yes"
# Enables KBUILD_CFLAGS -O3 optimization level.

### Hardware-Tailored Module Selection ("Diet Kernel")
_localmodcfg="yes"
_localmodcfg_path="./modprobed.db"
# Only modules actively required by the Lenovo IdeaPad 5 Pro hardware are compiled, 
# drastically reducing kernel footprint and boot memory overhead.

### Tick Rate & Preemption
_HZ_ticks="1000"
_tickrate="full"
_preempt="full"
# 1000Hz tick rate with full tickless preemptive kernel tuning for low latency.

### Memory Tuning
_hugepage="madvise"
# Transparent Hugepages set to madvise to prevent memory fragmentation and bloat.

### Network Congestion Control
_tcp_bbr3="yes"
# TCP BBRv3 congestion control enabled by default.
```

---

## 📦 Pacman Repository Configuration

To use these pre-built packages via `pacman`, add the following custom repository to `/etc/pacman.conf`:

```ini
[custom_repo]
SigLevel = Optional TrustAll
Server = https://github.com/sreepadmarat/CachyOS-KernelBuilder/releases/download/latest
```

Then synchronize and install:

```bash
sudo pacman -Sy linux-cachyos-ideapad-bore-lto-diet linux-cachyos-ideapad-bore-lto-diet-headers
```
