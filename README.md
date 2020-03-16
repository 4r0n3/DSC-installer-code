# DSC-installer-code
Brute force script to be ran in Firefox developer console. Pre-requisites:
* denvera's kernel driver module to enable the Raspberry to communicate key presses into the DSC Keybus. (https://github.com/denvera/dscmod)
* denvera's dsc-node repository to control to feed keypresses from the browser to the dscmod kernel driver. (https://github.com/denvera/dsc-node)
Follow all the inscructions included in the denvera's repositories and after you get both of those modules up and running, only then come back to this repository.

This script was used successfully to brute force the installer's code of a DSC PC1616 home alarm system. Will work with many other DSC models. Most likely at least with PC1864.

Components needed are listed in the denvera's repositories, but here are some additional comments:
Raspberry Pi.
      Preferably with as much RAM as possible. The script was consuming a lot of RAM and the old Raspberry Pi 2, that I used for the brute forcing,  ran out of RAM in approximately 1 hour and required a reboot. Might be that there was a memory leak in the very old version of Firefox ESR that was used. Or I did not implement the proper garbage collection into the script.
Well, anyway, the script did what it was supposed to, so I did not develop it further.

