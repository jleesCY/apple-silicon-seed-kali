### Part 3 Setup
I did not have to switch the UTM network adapter mode ot "host only" to get SSH-ing and port scanning to work. In fact, switching to "host only" was not working for me. I kept the default UTM network settings for the SEED VM and it worked just fine

### Part 4 Setup
I had to find a Nessus version compatible with ARM64, since that is what architecture the VMs were running. i followed the same URL provided in the lab, but selected `aarch64` instead of the default.

<p align="center">
  <image src="../../../images/lab3-nessus.png"></image>
</p>

### Part 5 Setup
I had to stop the snort service by running `sudo systemctl stop snort`

On the lab instructions it says to run `sudo systemctl snort stop`, which did not work for me

### Part 5c (SYN Scan)
I had to create the `/home/seed` directory manually for this step, since it is not created by default by the seed setup scripts.

`sudo mkdir /home/seed`

`sudo touch /home/seed/alert.log`
