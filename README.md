# Aruka-OptiKernel for Xiaomi Redmi Note 4 / 4X (mido)

Custom Linux 3.18 kernel for Xiaomi Redmi Note 4 / 4X Snapdragon (**mido**, MSM8953) designed for maximum RAM availability, daily battery efficiency, and silky smooth 60 FPS UI performance on Android 10 (Q) ROMs.

---

## 🌿 Branches

* **`main`**: **v1.2 (Standard Stable)** — Proton Clang 13, RAM debloat, BFQ, TCP Westwood, KCAL, WireGuard, 300Hz timer tick.
* **`no-log`**: **v1.3.1 (Debloated & Charging Verified)** — Extensively debloated diagnostics (`SCHED_DEBUG`, `SCHEDSTATS`, `DEBUG_PREEMPT`, `PRINTK_TIME`, `TIMER_STATS`, `MSM_RPM_LOG`, `MSM_SMEM_LOGGING`, `MSM_TZ_LOG`) while maintaining full Qualcomm DWC3 USB controller and battery charging compatibility.

---

## 🌟 Key Features

* **Base Source:** Zeelog LineageOS 17.1 (December 14, 2020)
* **Security Patch:** ASB December 2020 (`ASB-2020-12-05`)
* **CAF Tag:** Qualcomm MSM8953 `LA.UM.8.6.r1-05300-89xx.0`
* **Compiler:** Built with **Proton Clang 13.0.0 (LLVM)** + LLVM Gold Linker
* **RAM Debloated:** Disabled `FTRACE`, `DEBUG_INFO`, `PM_DEBUG`, `CMA_DEBUGFS`, and `MSM_COMMON_LOG`
* **Storage I/O:** Default **BFQ** I/O Scheduler (`slice_idle = 0` non-rotational flash mode)
* **Networking:** Default **TCP Westwood** congestion control for low packet-loss on 4G LTE & Wi-Fi
* **Display Engine:** **KCAL** display calibration controller (`drivers/video/msm/mdss/mdss_mdp_kcal_ctrl.c`)
* **Security & VPN:** **WireGuard** VPN in-tree kernel module (`net/wireguard`)
* **UI Smoothness:** Kernel timer tick `CONFIG_HZ_300=y` perfectly synchronized with 60 FPS Vsync (3.33ms intervals)
* **Power Efficiency:** `CONFIG_WQ_POWER_EFFICIENT_DEFAULT=y` and Boeffla wakelock blocker
* **Hardware Bus Arbiter Safe:** Full `CONFIG_MSM_BUS_SCALING=y` preserved for complete Adreno GPU and MDSS display clock management.
* **Charging Safe:** DWC3 USB subsystem and battery fuel gauge communication verified.

---

## 🛠️ How to Compile

```bash
export ARCH=arm64
export SUBARCH=arm64
export CC=/path/to/clang/bin/clang
export CLANG_TRIPLE=aarch64-linux-gnu-
export CROSS_COMPILE=aarch64-linux-android-
export CROSS_COMPILE_ARM32=arm-linux-androideabi-

make mido_defconfig
make -j$(nproc)
```

The compiled kernel image will be generated at `arch/arm64/boot/Image.gz-dtb`.

---

## 📱 Flashing Instructions

1. Boot into **OrangeFox** or **TWRP Recovery**.
2. Flash the AnyKernel3 zip `Aruka-OptiKernel-v1.3.1-Mido-Q.zip`.
3. Wipe Dalvik & Cache (optional).
4. Reboot System.
