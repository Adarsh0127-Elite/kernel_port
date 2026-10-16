# OPPO MT6896 Kernel Building (Linux 6.12.23)

Guide to building the Linux 6.12.23 Android GKI kernel and device modules for OPPO MediaTek MT6896 devices.

---

## Getting Started

### 1. Prerequisites
Ensure you have the required source control and build tools installed. Refer to the [Android Source Control Setup](https://source.android.com/setup/develop) for details.

### 2. Initialize Local Workspace
Initialize the repository using Google's Android 16 (Kernel 6.12) manifest:

```bash
repo init -u https://android.googlesource.com/kernel/manifest.git -b common-android16-6.12-lts --depth=1
```

> **Note:** You can also use `-b common-android16-6.12-lts` if preferred.

### 3. Add Local Manifest
Clone this local manifest repository into `.repo/local_manifests`:

```bash
git clone https://github.com/Adarsh0127-Elite/kernel_port.git -b lineage-23.2 .repo/local_manifests
```

### 4. Synchronize Sources
Sync the tree (adjust `-j` to match your CPU cores):

```bash
repo sync -c -j$(nproc --all) --no-tags
```

---

## Building the Kernel

### Option 1: Using Kleaf Device Modules Build Script (Recommended)

From the root of your local repository, run:

```bash
PROJECT=mgk_64_k612 ./kernel_device_modules-6.12/build.sh
```

Or from the `kernel/` directory:

```bash
cd kernel
PROJECT=mgk_64_k612 ./kernel_device_modules-6.12/build.sh
```

For debug build variants:
```bash
PROJECT=mgk_64_k612 MODE=userdebug ./kernel_device_modules-6.12/build.sh
```

### Option 2: Using OPlus Kernel Build Script

From the root of your local repository, execute:

```bash
# For user build:
./kernel/oplus/build/oplus_build_kernel.sh mt6993 user

# For userdebug build:
./kernel/oplus/build/oplus_build_kernel.sh mt6993 userdebug
```

---

## Build Artifacts

Once the build finishes successfully, all generated artifacts (`Image`, `Image.lz4`, `vmlinux`, `dtbo.img`, and loadable kernel modules `.ko`) will be available in:

```bash
out/dist/
```
*(or under `out_krn/target/product/mgk_64_k612/obj/KLEAF_OBJ/dist/` when building via OPlus scripts)*
