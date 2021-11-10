Questions
1. For each member in your team, provide 1 paragraph detailing what parts of the lab that member 
   implemented / researched. (You may skip this question if you are doing the lab by yourself).
  
   ```
   Just me, Steven Li.
   ```

2. Describe in detail the steps you used to complete the assignment. Consider your reader to be someone 
   skilled in software development but otherwise unfamiliar with the assignment. Good answers to this 
   question will be recipes that someone can follow to reproduce your development steps.
   Note: I may decide to follow these instructions for random assignments, so you should make sure 
   they are accurate.
   
  ```
  1. Configured Ubuntu VM on VMware Workstation Player
  2. Fork Linux repo on Github
  3. Clone that repo on VM
  4. CD to Linux/
  5. Make Linux kernel (Using make oldconfig -> make modules -> make wait..)
  6. Reboot VM
  7. Run make
  8. cd Linux/ 
  9. mkdir CMPE283/ 
  10. cd CMPE283/ 
  11. Download provided Make & CMPE283-1.c files and put it into dir
  12. run make 
  13. run sudo insmod cmpe283-1.ko 
  14. run dmesg
  15. read and save output to something
  16. edit CMPE283-1.c for the other MSR & repeat step 13-14 until done. (Or edit CMPE283-1.c to do all the ctl reads at once, which I did)
  17. submit output```
