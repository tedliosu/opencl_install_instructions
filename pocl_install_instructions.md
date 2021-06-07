# Instructions For Setting Up CPU OpenCL Development On A Linux Distro #

1. `git clone https://github.com/pocl/pocl.git`

2. If using a Debian-type distro that supports the apt package manager, based
   on the latest version of LLVM that the latest version of pocl supports,
   (the version info can be found [here](http://portablecl.org/download.html)
   follow instructions at [here](https://apt.llvm.org/) to add the appropriate
   llvm repositories to your package manager.
       - For example, as of time of writing pocl latest version supports up to LLVM
         12.0, so if you are running an Ubuntu LTS 20.04 focal distro, add 
         > deb http://apt.llvm.org/bionic/ llvm-toolchain-bionic-12 main
         
         to "/etc/apt/sources.list.d/llvm.list" (create the file if it doesn't already
         exist), and run `wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | sudo -H apt-key add -`
         to add the LLVM repository's signature to your apt package manager.
       - If **NOT** running a Debian-type distro, then simply skip to the next step.

3. Follow instructions [here](http://portablecl.org/docs/html/install.html)
   to build and install pocl from the git-cloned repository
       - **NOTE** that the instructions should also include installing
         the following at least as of time of this writing:
         > llvm libclang-cpp10-dev libclang-10-dev

         not sure why this important bit is left out of the instructions.

4. If "/etc/OpenCL/vendors" directory does not exist, then create it on
   your machine. Then run `sudo -H cp /usr/local/etc/OpenCL/vendors/pocl.icd /etc/OpenCL/vendors/`.

5. Run `clinfo -l` to check to make sure that your output looks something like the following:
   <pre>
   Platform #0: Portable Computing Language
    `-- Device #0: pthread-AMD Ryzen 5 2600 Six-Core Processor
   Platform #1: AMD Accelerated Parallel Processing
    `-- Device #0: gfx900:xnack-"
   </pre>

6. Now (if applicable) make sure that your OpenCL host code is able to
   query and retrieve the platform id of the newly installed PoCL OpenCL
   platform.

