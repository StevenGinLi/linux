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
6. `lsmod | grep kvm` to check if KVM modules are mounted. Skip to step 9. if no output
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
   
![image](https://user-images.githubusercontent.com/78942886/142806022-ac4bd3e5-099c-4368-91e8-2562206b28b9.png)


# Assignment 3

## Questions
### 1. For each member in your team, provide 1 paragraph detailing what parts of the lab that member implemented / researched. (You may skip this question if you are doing the lab by yourself).

Just me, Steven Li.

### 2. Describe in detail the steps you used to complete the assignment. Consider your reader to be someone skilled in software development but otherwise unfamiliar with the assignment. Good answers to this question will be recipes that someone can follow to reproduce your development steps.Note: I may decide to follow these instructions for random assignments, so you should make sure they are accurate.

1. Continung from assignment 2, already installed Linux and loaded the kernel. Made changes to cpuid.c and vmx.c to have case 1 & 2 of recording number of exits and cycles taken to complete them.
2. Make changes to cpuid.c and vmx.c to include case 3 & 4, to display # of exits and timings per each exit number #0-69, some numbers are invalid and some are disabled.
3. Run `make -j <number_of_cores> modules`
4. Run `sudo make INSTALL_MOD_STRIP=1 modules_install`
5. Run `sudo make install`
6. `lsmod | grep kvm` to check if KVM modules are mounted. Skip to step 9. if no output
7. `sudo rmmod kvm_intel`
8. `sudo rmmod kvm`
9. Reinput the mods `sudo modprobe kvm` and `sudo modprobe kvm_intel`
10. Run the nested VM either through apps or `sudo virt-manager`
11. Run CPUID command such `cpuid -l 0x4ffffffd -s <exit number>` in the nested VM. I ran exit number from 0-69 to see exit from each exit number.
12. run `dmesg` on host VM to check outputs 

![image](https://user-images.githubusercontent.com/78942886/143743396-7c9a0dd3-666d-4602-b5f5-d2f1ae237740.png)


### 3. Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there more exits performed during certain VM operations? Approximately how many exits does a full VM boot entail?

The frequency of exit does not increase at a stable rate, each CPUID call results in a different amount of exits. a Full VM boot takes roughly ~1m exits. (Should be lower but I let the VM sit idle for a little bit)

![image](https://user-images.githubusercontent.com/78942886/143753695-3bf14d1d-2c9c-48e1-8ac2-d0109dc9b0c3.png)


### 4. Of the exit types defined in the SDM, which are the most frequent? Least?

Most Frequent:
- 12: HLT
- 30: I/O instruction
- 32: WRMSR
- 48: EPT violation

Least Frequent:
- 0: Exception or non-maskable interrupt (NMI)
- 29: MOV DR
- 31: RDMSR

# Assignment 4
## Questions
### 1. For each member in your team, provide 1 paragraph detailing what parts of the lab that member 
implemented / researched. (You may skip this question if you are doing the lab by yourself).
Just me.
### 2. Include a sample of your print of exit count output from dmesg from “with ept” and “without ept”.

with ept:

![image](https://user-images.githubusercontent.com/78942886/144952787-1dd9735d-94d5-4d4c-971a-2498b812d3b9.png)
![image](https://user-images.githubusercontent.com/78942886/144955205-fec48752-39b7-4033-9798-33a31a273419.png)



without ept:

![image](https://user-images.githubusercontent.com/78942886/144953740-bd0dac92-2c36-4dd8-80fe-d220d97b1fd9.png)

![image](https://user-images.githubusercontent.com/78942886/144954645-a860695b-cc29-40ec-8f2c-267e69f51d15.png)



### 3. What did you learn from the count of exits? Was the count what you expected? If not, why not?
The amount of counts went up without ept as expected because without nested paging there would be more exits even though there is less ept exits. 

### 4. What changed between the two runs (ept vs no-ept)
The number of exits, there was more total exits in no-ept than ept. I believe the increase comes from the increase need to read and write the cr3 register which triggers additional VM exits. Also there needs to be more table flushes to be done in shadow paging. Essentially more cr3 read and write exits, table flushes and page faults (not from ept) makes up for the difference in amount of VM exits between ept vs. no-ept.
