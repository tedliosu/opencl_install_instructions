# Instructions For Setting Up GPU OpenCL Development on a Linux Distro #

1. Make sure that your Linux distro AND its kernel is supported by ROCm by
   navigating to [here](https://github.com/RadeonOpenCompute/ROCm#Supported-Operating-Systems).

2. `wget -q -O - https://repo.radeon.com/rocm/rocm.gpg.key | sudo -H apt-key add -`
     or whatever equivalent command for your Linux Distro copied from
     [here](https://rocmdocs.amd.com/en/latest/Installation_Guide/Installation-Guide.html).

3. `echo 'deb [arch=amd64] https://repo.radeon.com/rocm/apt/debian/ xenial main' | sudo -H tee /etc/apt/sources.list.d/rocm.list`
     or whatever equivalent command for your Linux Distro copied from
     [here](https://rocmdocs.amd.com/en/latest/Installation_Guide/Installation-Guide.html).

4. `sudo -H apt update` or whatever equivalent command for your Linux Distro

5. Go to [here](https://www.amd.com/en/support) and download the appropriate graphics drivers for YOUR Linux distro
    and graphics card **FROM THE "Professional Graphics" LIST OF DRIVERS**. **DO NOT DOWNLOAD
    from the "Graphics" only list of drivers**; those drivers unlike the "Professional Graphics"
    drivers tend to not be as stable. Since I have a Vega 56 *which shares the same architecture*
    as a Vega Frontier Edition professional graphics card, I chose > "Professional Graphics" ->
    "AMD Radeon Pro" -> "Radeon Pro Series" -> "Radeon Vega Frontier Edition (Air-cooled)"

    and then clicked the submit button to get my driver to be downloaded and
    installed.  The resulting driver download should be some sort of tar archive
    (e.g. *amdgpu-pro-20.45-1225310-ubuntu-20.04.tar.xz* for Ubuntu 20.04 as of time of
     this writing)

6. Unpack the folder within the archive to your home directory and `cd` into the directory.

7. Run the `amdgpu-pro-install` command but **DO NOT agree to actually installing the
    packages on your Linux distro**; this step is simply to ensure that all of
    the packages within the archive downloaded from [amd.com](amd.com) gets loaded into the
    local */var/opt/amdgpu-pro-local* repository.

8. NOW install the following packages into your machine (or whatever equivalent the
    following packages are for your Linux distro):
   > amdgpu-core amdgpu-dkms amdgpu-dkms-firmware amdgpu-pin amdgpu-pro-core amdgpu-pro-pin
   > libdrm-amdgpu-amdgpu1 libdrm-amdgpu-common libdrm-amdgpu1 libdrm2-amdgpu libllvm${LLVM_VERSION}-amdgpu
   > llvm-amdgpu llvm-amdgpu-${LLVM_VERSION} llvm-amdgpu-${LLVM_VERSION}-dev
   > llvm-amdgpu-${LLVM_VERSION}-runtime llvm-amdgpu-dev llvm-amdgpu-runtime ocl-icd-libopencl1-amdgpu-pro
   > ocl-icd-libopencl1-amdgpu-pro-dev opencl-orca-amdgpu-pro-icd rocm-device-libs-amdgpu-pro
   > xserver-xorg-video-amdgpu rocm-clang-ocl rocm-cmake rocm-dbgapi rocm-debug-agent rocm-dev
   > rocm-device-libs rocm-device-libs-amdgpu-pro rocm-gdb rocm-opencl rocm-opencl-dev rocm-smi-lib
   > rocm-utils rocminfo clinfo

   where ${LLVM_VERSION} is the version of LLVM that the default "llvm" package ships with
   for your Linux distro; as of time of this writing it's "10.0" (for Ubuntu at least
   you may find out this information by executing `sudo -H apt-cache show llvm | grep "Version" | grep -o "[[:digit:]]*\.[[:digit:]]*"` on the
   system CLI.)

9. Reboot your machine

10. Run `clinfo -l` to check to make sure that your output looks something like the following:
    <pre>
    Platform #0: Portable Computing Language
     `-- Device #0: pthread-AMD Ryzen 5 2600 Six-Core Processor
    Platform #1: AMD Accelerated Parallel Processing
     `-- Device #0: gfx900:xnack-
    </pre>

11. Enjoy using your frankensteined AMD OpenCL development install on your Linux distro :)

