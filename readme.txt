How to build LineageOS for Essential Phone (PH-1, mata)

1, Install Ubuntu 20.04.x.

2, Install packages for build.
 sudo apt update && sudo apt upgrade
 sudo apt install bc bison build-essential ccache curl flex g++-multilib gcc-multilib git gnupg gperf imagemagick lib32ncurses5-dev lib32readline-dev lib32z1-dev liblz4-tool libncurses5 libncurses5-dev libsdl1.2-dev libssl-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev libwxgtk3.0-gtk3-dev openjdk-14-jdk python3 git-lfs adb fastboot
 sudo apt-get install libncurses*

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
 mkdir ~/lineage-17.1
 cd ~/lineage-17.1

6, Download the source code
 repo init -u https://github.com/LineageOS/android.git -b lineage-17.1
 repo sync
 
7, Download device binary.
Download hltedcm.xml from this repository.
Copy hltedcm.xml to "~/lineage-17.1/.repo/local_manifests".
 repo sync

8, Build for mata.
 export LC_ALL=C.UTF-8
 export ALLOW_MISSING_DEPENDENCIES=true
 export WITH_SU=true
 source build/envsetup.sh
 brunch hltedcm 2>&1 | tee lineage_$(date '+%Y%m%d_%H-%M-%S').log

9, Install
Open the directory "~/lineage-17.1/out/target/product/hltedcm".
You can find "lineage-17.1-[Build Date]-UNOFFICIAL-mata.zip" and "boot.img".
Connect phone to PC using USB.
Reboot phone to Download (Odin).
Flash TWRP using Odin3.
Reboot to Recovery (Power Up + Home + Power)
Select "Advanced".
Select ADB sideload.
 adb sideload ~/lineage-17.1/out/target/product/hltedcm/lineage-17.1-[Build Date]-UNOFFICIAL-mata.zip

(10, Install Magisk using ADB sideload)

11, Enjoy LineageOS.
