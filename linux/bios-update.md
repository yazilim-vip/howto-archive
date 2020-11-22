Updating the BIOS on Lenovo laptops from Linux using a USB flash stick

Aren’t hardware manufacturers funny? They either require an old-fashioned operating system (Windows) or museum hardware (floppy drives) to update a BIOS. Apparently they never learn and are instead busy adding features like DRM and UEFI to make our lives even more miserable.

However updating the BIOS on my Lenovo X230 laptop was surprisingly easy once I learned how to do that (kudos to a G+ post I stumbled upon).

1.  Go to support.lenovo.com (or better use a search engine becaues the Lenovo website is beautiful but technically pretty broken and slow) and search for the BIOS upgrade of your laptop model.
1. Download the most recent ISO file. Look for “BIOS bootable update CD”.
1. Convert the ISO image using the geteltorito utility (if you don’t have it: $`sudo apt-get install genisoimage`).
    - Example:
    - $`geteltorito -o bios.img g2uj18us.iso`
1. Insert any USB stick into your laptop that you have lying around. 
    - The image file is just 50 MB in size so even USB sticks with low capacity will work. 
    - Keep in mind that the stick will be completely overwritten.
1. If you are in a graphical environment then unmount the USB stick again.
1. Find out the device name of the stick. 
    - Enter a terminal window and enter “dmesg | tail”. 
    - You are looking for something like:[ 2101.614860] sd 6:0:0:0: [sdb] Attached SCSI disk
    The “sdb” tells you that your USB stick is available on /dev/sdb. Don’t just assume it’s sdb. If it’s on another device on your laptop then you will destroy your data.
1. Copy the image to the USB stick:
    - $`dd if=bios.img of=/dev/sdb bs=1M`
1. Reboot your laptop.
1. After the Lenovo logo appears press ENTER.
1. Press F12 to make your laptop boot from something else than your harddisk.
1. Select the USB stick.
1. Make sure your laptop has its power supply plugged in. (It will refuse to update otherwise.)
1. Follow the instructions.