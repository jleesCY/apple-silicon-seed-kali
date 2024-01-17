# Setting up SEED and Kali Linux VMs on Apple silicon using UTM
As of Spring 2024

## Contents

[Download UTM](#download-utm)

[Download VMs](#download-the-vms)

[Set Up the VMs](#set-up-the-vms)

&nbsp;&nbsp;&nbsp;[SEED Labs](#seed-labs)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Ubuntu 22.04](#ubuntu-2204)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Installing SEED Tools](#installing-seed-tools)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Final Steps](#final-steps)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Disable Automatic Updates](#disable-automatic-updates)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Fix "internal error" problem](#fix-internal-error-problem)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Fix Firefox not opening](#fix-firefox-not-opening)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Install the "HTTP Header Live" Firefox extension](#install-the-http-header-live-firefox-extension)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Disable DNS over HTTPS](#disable-dns-over-https)

&nbsp;&nbsp;&nbsp;[Kali Linux](#kali-linux)

[Final Notes](#final-notes)


## Download UTM
A link to the free version of UTM can be found [here](https://mac.getutm.app/). There is a paid version on the mac appstore ($9.99 USD). The only difference between these versions is the fact that the paid version gets automatic updates. The free download needs to be manually updated.

## Download the VMs
The necessary UTM files can be downloaded here:

[`Ubuntu 22.04 ARM64 UTM.zip`](https://1drv.ms/u/s!As06ehb0pJGBh-dfzYzdChnJhK6RUg?e=yTgODR) (OneDrive, 3.61GB)

[`Kali Linux 2023 ARM64 UTM.zip`](https://1drv.ms/u/s!As06ehb0pJGBh-deUz1P8yrWaRpo7g?e=hotwXl) (OneDrive, 4.51GB)

> **NOTE**: These exact files are available for download from the UTM site. However, they are quite slow to download, taking around 1 - 2 hours a piece. The provided links are the identical files provided by UTM, just serviced by OneDrive, which is far quicker. 

---
## Set Up the VMs

### SEED Labs

#### Ubuntu 22.04

The `.vdi` file available for download from the SEED Labs site is incompatible with UTM. We need to build the SEED Labs VM manually.

Unzip `Ubuntu 22.04 ARM64 UTM.zip` and save the `.utm` file somewhere you can find it.

From the UTM starting screen, select `Create a New Virtual Machine`, or select the `+` in the upper left corner
<p align="center">
  <image src="images/starting-screen.png" style="width:85vw"></image>
</p>

Select `open`
<p align="center">
  <image src="images/open-existing.png" style="width:40vw"></image>
</p>

Find and select `Ubuntu 22.04.utm`.

The machine should now automatically be added to your sidebar. Running the machine should be no problem. Login credentials are as follows:

Username: ```ubuntu```

Password: ```ubuntu```

Be sure to update the system before proceeding:

```sudo apt update```

```sudo apt upgrade```

At this point, you can customize your machine to your liking.

#### Installing SEED Tools

> **NOTE**: The steps I followed were from SEED Labs' documentation found [here](https://github.com/seed-labs/seed-labs/blob/master/manuals/vm/seedvm-from-scratch.md#4-installing-software-packages)

First, ensure git is installed

```sudo apt install git```

Clone the SEED Labs setup repository

```git clone https://github.com/seed-labs/seed-labs.git```

This should have created a directory called 
`seed-labs`.

Navigate to the directory containing the necessary setup scripts

```cd seed-labs/lab-setup/ubuntu20.04-vm/src-vm```

Run `main.sh` and all of the necessary tools should begin to install.

```./main.sh```

> **NOTE**: during the installation of Wireshark, you will be asked whether a non-superuser should be able to capture packets. Choose `no`.

#### Final Steps
##### Disable automatic updates
We do not want the system to automatically update. Open `Software and Updates`

<p align="center">
  <image src="images/software-and-updates.png" style="width:50vw"></image>
</p>

Under the `Updates` tab, change the settings for "automatically check for updates" and "notify me of a new Ubuntu version" to `Never`

<p align="center">
  <image src="images/updates-settings.png" style="width:75vw"></image>
</p>

##### Fix "internal error" problem
You may have seen a notification several times from Ubuntu saying that there was an internal error. In this case, it is really nothing serious. To disable the notification, we need to do two steps:

1. Go to `Settings` --> `Privacy` --> `Diagnostics`, and change "Send error report to Canonical" to `Never`.

<p align="center">
  <image src="images/error-reports.png" style="width:75vw"></image>
</p>

2. Ensure that in `/etc/default/apport`, `enabled=0`

##### Fix Firefox not opening

For some reason Firefox was not opening on my UTM virtual machine. To fix this, simply enable and start the `snapd.apparmor` service

```sudo systemctl enable snapd.apparmor```

```sudo systemctl start snapd.apparmor```

##### Install the "HTTP Header Live" Firefox extension

This extension is nescessary for some of the SEED labs. It can be added to firefox using [this](https://addons.mozilla.org/en-US/firefox/addon/http-header-live/) link:
```https://addons.mozilla.org/en-US/firefox/addon/http-header-live/```

##### Disable DNS over HTTPS

To ensure DNS over HTTPS is disabled in firefox, click the menu button and select `Settings`. Search for "DNS over HTTPS", and make sure the `Status` is `Off`

---
### Kali Linux

Unzip `Kali Linux 2023 ARM64 UTM.zip` and save the `.utm` file somewhere you can find it.

From the UTM starting screen, select `Create a New Virtual Machine`, or select the `+` in the upper left corner
<p align="center">
  <image src="images/starting-screen.png" style="width:85vw"></image>
</p>

Select `open`
<p align="center">
  <image src="images/open-existing.png" style="width:40vw"></image>
</p>

Find and select `Kali Linux 2023.utm`.

The machine should now automatically be added to your sidebar. Running the machine should be no problem. Login credentials are as follows:

Username: `kali`

Password: `kali`

---

### Final Notes
I have only done a few SEED labs using this virtual machine. I also have yet to dive deep into the Kali Linux machine. *There may be things I missed in this setup*. If I do happen to find issues, I will be sure to document them on this page.
