### Setup
We need the arm version of the lab setup folder, which is available on the seed website for download. Here is a OneDrive link to the file I used:

[`Labsetup-arm.zip`](https://1drv.ms/u/s!As06ehb0pJGBh_E0dcqNm1YT92bhpw?e=IzMTfC) (Onedrive, 1.62 KB)

Alternatively, you can download it from SEED [here](https://seedsecuritylabs.org/Labs_20.04/Files/Mitnick_Attack/Labsetup-arm.zip)

Assuming docker has already been correctly set up using the steps from my notes on Lab 5 (starting [here](https://github.com/jleesCY/apple-silicon-seed-kali/tree/main/Lab-Notes/CY4310/5%20-%20DNS%20Spoofing#install-the-correct-version-of-docker)), `cd` into `Labsetup-arm` and run

```
dcbuild
sudo docker-compose up --remove-orphans
```

Note that `--remove-orphans` would remove any outstanding containers from Lab 5. If you did not do lab 5, just run

```
dcup
```