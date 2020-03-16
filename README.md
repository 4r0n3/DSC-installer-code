# DSC-installer-code

Brute force script to be run in Firefox developer console. Below pre-requisites need to be installed successfully first:
* denvera's kernel driver module to enable the Raspberry to communicate key presses into the DSC Keybus. (https://github.com/denvera/dscmod)
* denvera's dsc-node repository to control to feed keypresses from the browser to the dscmod kernel driver. (https://github.com/denvera/dsc-node)

Follow all the inscructions included in the denvera's repositories and after you get both of those modules up and running, only then come back to this repository.

# Background information

This script was used successfully to brute force the installer's code of a DSC PC1616 home alarm system. Will work with many other DSC models. Most likely at least with PC1864.

Components needed are listed in the denvera's repositories.

Preferably get a Raspberry or similar with as much RAM as possible. The script was consuming a lot of RAM and the old Raspberry Pi 2, that I used for the brute forcing, ran out of RAM in approximately 1 hour and required a reboot. Might be that there is a memory leak in the old version of Firefox ESR that I used. Or I did not implement the proper garbage collection into the script.
Anyhow, the script did what it was supposed to, so I have not fine tuned it any further.

I used the SparkFun logic level converter (part number BOB-12009) as suggested by denvera in the dscmod repository. It worked perfectly.

# SETUP INSTRUCTIONS

First disarm the DSC alarm system before you begin to work on the system.

IMPORTANT:

Make sure you have at least one open zone in your DSC alarm system.

Having an open zone / open loop will make sure that no nuisance arming can happen by this script during the brute forcing.

For example keep open the door of control cabinet, where the DSC main circuit board is located. This is usually a zone.

FIRST READ THE MANUAL IN denvera's repositories: dscmod and dsc-node and do as there is told.

Then perform these additional modifications.

Edit line 303 in file dscmod.c as shown below (folder dscmod):

FROM:

ret = copy_from_user(kbuf, buff, copy_max);

TO:

ret = raw_copy_from_user(kbuf, buff, copy_max);

Compile the dscmod kernel driver using make. Ignore the warnings.

In the Node.js server config folder (dsc-node/src/)
comment out lines 141 & 142 in the file "dscserver.js", as shown below:

					//status.zones = msg.readUInt8(6);
					
					//status.msgText = '. . .';
					
Edit file dsc-node/config/default.json by changing in that file the word "socket" to "dev"

Create the missing folder /dsc-node/log/

Build assets with 'brunch build' in folder "dsc-node"

# Daily usage routine

Load the kernel driver into Linux with command (folder dscmod):

insmod dscmod.ko

Start up the dsc-node server instance by instantiating the following command (folder dsc-node):

sudo yarn start > /dev/null 2>&1

Copy-paste the script from file
*installerCodeBruteForce.txt
into the Firefox developer console and hit Enter. In Firefox you can open the dev console by key F12.

The brute force will now commence. See the Firefox developer console output for possible troubleshooting details.
