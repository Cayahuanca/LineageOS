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
 mkdir ~/lineage-18.0
 cd ~/lineage-18.0

6, Download the source code
 repo init -u https://github.com/LineageOS/android.git -b lineage-18.0"
 repo sync
 
7, Download device binary.
Download mata.xml from this repository.
Copy mata.xml to "~/lineage-18.0/.repo/local_manifests".
 repo sync

8, Build for mata.
 export LC_ALL=C.UTF-8
 export ALLOW_MISSING_DEPENDENCIES=true
 export WITH_SU=true
 source build/envsetup.sh
 brunch mata 2>&1 | tee lineage_$(date '+%Y%m%d_%H-%M-%S').log

9, Install
Open the directory "~/lineage-18.0/out/target/product/mata".
You can find "lineage-18.0-[Build Date]-UNOFFICIAL-mata.zip" and "boot.img".
Connect phone to PC using USB.
Reboot phone to bootloader.
 fastboot flash boot_a ~/lineage-18.0/out/target/product/mata/boot.img
 fastboot --set-active=a
Reboot phone to recovery.
Select "Apply update" using Volume Down button and push Power button.
Select "Apply from ADB".
 adb sideload ~/lineage-18.0/out/target/product/mata/lineage-18.0-[Build Date]-UNOFFICIAL-mata.zip
Select "← " using Volume Up button and push Power button.
Select "Reboot system now" and push Power button.

(10, Install Magisk using ADB sideload)

11, Enjoy LineageOS.
