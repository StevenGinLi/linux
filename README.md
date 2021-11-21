# Assignment 1

## Questions
### 1. For each member in your team, provide 1 paragraph detailing what parts of the lab that member implemented / researched. (You may skip this question if you are doing the lab by yourself).

Just me, Steven Li.


### 2. Describe in detail the steps you used to complete the assignment. Consider your reader to be someone skilled in software development but otherwise unfamiliar with the assignment. Good answers to this question will be recipes that someone can follow to reproduce your development steps.Note: I may decide to follow these instructions for random assignments, so you should make sure they are accurate.
   

1. Configured Ubuntu VM on VMware Workstation Player
2. Fork Linux repo on Github
3. Clone that repo on VM
4. `cd Linux/`
5. Make Linux kernel (Using make oldconfig -> make modules -> make wait..)
6. Reboot VM
7. Run `make`
8. `cd Linux/`
9. `mkdir CMPE283/`
10. `cd CMPE283/`
11. Download provided Make & CMPE283-1.c files and put it into dir
12. run `make`
13. run `sudo insmod cmpe283-1.ko`
14. run `dmesg` and save output to something
15. run `sudo rmmod cmpe283_1` 
16. edit CMPE283-1.c for the other MSR & repeat step 12-15 until done. (Or edit CMPE283-1.c to do all the ctrl reads at once, which I did)
17. submit output

# Assignment 2

## Questions
### 1. For each member in your team, provide 1 paragraph detailing what parts of the lab that member implemented / researched. (You may skip this question if you are doing the lab by yourself).

Just me, Steven Li.

### 2. Describe in detail the steps you used to complete the assignment. Consider your reader to be someone skilled in software development but otherwise unfamiliar with the assignment. Good answers to this question will be recipes that someone can follow to reproduce your development steps.Note: I may decide to follow these instructions for random assignments, so you should make sure they are accurate.


1. Continung from assignment 1, already installed Linux and loaded the kernel
2. Go into Linux/arch/x86/kvm to edit cpuid.c and linux/arch/x86/kvm/vmx to edit vmx.c to add the new functionalities (case 1 & 2, # of exits & total cycles of those exits)
3. Run `make -j <number_of_cores> modules`
4. Run `sudo make INSTALL_MOD_STRIP=1 modules_install`
5. Run `sudo make install`
6. `lsmod | grep kvm` to check if KVM modules are mounted. Skip to step 6 if no output
7. `sudo rmmod kvm_intel`
8. `sudo rmmod kvm`
9. Reinput the mods `sudo modprobe kvm` and `sudo modprobe kvm_intel`
10. Install the nested VM using Virt, `sudo apt-get install virt-manager`
11. `sudo virt-manager` to start the VMM and create a VM
12. Download Ubuntu .iso from website
13. Follow installation steps and finish installing VM and Run it 
14. Go to Terminal in nested VM and `sudo apt-get install cpuid`
15. Run CPUID command such `cpuid -l 0x4fffffff` in the nested VM
16. run `dmesg` on host VM to check outputs 
   
