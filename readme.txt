How to build LineageOS 18.1 for Galaxy Note 3 (SC-01F, hltedcm)

1, Install Ubuntu 22.04.x.

2, Install packages for build.
 sudo apt update && sudo apt upgrade -y
 sudo apt install adb bc bison build-essential ccache curl default-jdk fastboot flex g++-multilib gcc-multilib git git-lfs gnupg gperf imagemagick lib32ncurses5-dev lib32readline-dev lib32z1-dev liblz4-tool libncurses5 libncurses5-dev libsdl1.2-dev libssl-dev libwxgtk3.0-gtk3-dev libxml2 libxml2-utils lzop openjdk-14-jdk pngcrush python3 rsync schedtool squashfs-tools xsltproc zip zlib1g-dev 
 sudo apt install libncurses*

3, Install git-repo.
 wget https://storage.googleapis.com/git-repo-downloads/repo
 sudo chmod 755 repo
 sudo chmod a+x repo
 sudo chown root:root repo
 sudo mv repo /usr/bin/

4, Configure git.
 git config --global user.name "[Your Name]"
 git config --global user.email "[Your Mail Address]"

5, Create folder for download the source code.
 mkdir ~/lineage-18.1
 cd ~/lineage-18.1

6, Download the source code
 repo init -u https://github.com/LineageOS/android.git -b lineage-18.1
 repo sync
 
7, Download device binary.
Download hltedcm.xml from this repository.
Copy hltedcm.xml to "~/lineage-18.1/.repo/local_manifests/hltedcm.xml".
 repo sync

Download hlte-common, msm8974-common from https://github.com/TheMuppets/proprietary_vendor_samsung/tree/lineage-18.1
Copy them to "~/lineage-18.1//vendor/samsung/"

8, Build for mata.
 export LC_ALL=C.UTF-8
 export ALLOW_MISSING_DEPENDENCIES=true
 source build/envsetup.sh
 brunch hltedcm 2>&1 | tee lineage_$(date '+%Y%m%d_%H-%M-%S').log

9, Install
Open the directory "~/lineage-18.1/out/target/product/hltedcm".
You can find "lineage-18.1-[Build Date]-UNOFFICIAL-mata.zip" and "boot.img".
Connect phone to PC using USB.
Reboot phone to Download (Odin).
Flash TWRP using Odin3.
Reboot to Recovery (Power Up + Home + Power)
Select "Advanced".
Select ADB sideload.
 adb sideload ~/lineage-18.1/out/target/product/hltedcm/lineage-18.1-[Build Date]-UNOFFICIAL-hltedcm.zip

(10, Install Magisk)

11, Enjoy LineageOS.
