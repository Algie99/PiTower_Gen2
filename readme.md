The instructions below do not work. There are missing files, dependencies, and copy instructions. They are a work in progress not a finished release.

Elecrow have provided a Bookworm image that functions (https://drive.google.com/file/d/11cD6NDc93rNiuJtBJ9wSB34deXeKxy-h/view?usp=sharing). Use raspi-config to reset unknown password. Only SSD1 displays and it is labelled 'ROM'. This image cannot be successfully upgraded to Trixie.

If you would like to get the front display working whilst Elecrow locate or finish their Trixie install the extra steps are below. Use the files and instructions in this archive as I have not confirmed the files on Bookworm image desktop are the same. There is an interesting Chinese readme amongst the Bookworm files that when translated details a completely different set of files with an installer. Please be aware that the final installation may be totally different. 

**Extra Steps**

These steps should work pre or post Elecrow's instructions.

Copy /PiTower_Gen2-master/PiTowerGen2/LCD_Module_RPI_code/RaspberryPi/python/pic/LCD_2inch8.png to /home/pi/Pictures

<img width="240" height="320" alt="bj-03" src="https://github.com/user-attachments/assets/b2b377f1-2e7e-4eb8-9cf3-1fa5d78edd5a" /> 

Copy the above image, save as bj-03.png and copy to /home/pi/Pictures

Open lcd_display.py in a text editor and change line 131 disk_title_text = f"ROM:" to  disk_title_text = f"SSD:"

Wherever you are told to move to the python3.11 folder on Trixie it will be python3.13

Now proceed with below and your front screen should work


**Before configuration, please download the entire PiTowerGen2 file to your local system and place it on your desktop.**

Pi5 Configuration Steps:

step 1:

Move /home/pi/Desktop/PiTowerGen2/LCD_Module_RPI_code/RaspberryPi/python/lib/LCD_2inch8.py to /usr/local/lib/python3.11/dist-packages/

Move /home/pi/Desktop/PiTowerGen2/LCD_Module_RPI_code/RaspberryPi/python/lib/lcdconfig.py to /usr/local/lib/python3.11/dist-packages/

Move /home/pi/Desktop/PiTowerGen2/lcd_display.py to /home/pi/elecrow/

Move /home/pi/Desktop/PiTowerGen2/cfg/lcd_script.service to /etc/systemd/system/

sudo chmod +x /home/pi/elecrow/lcd_display.py

step 2:

Move /home/pi/Desktop/PiTowerGen2/RGB_Module_RPI_code/rpi5_ws2812 to /usr/local/lib/python3.11/dist-packages

Move /home/pi/Desktop/PiTowerGen2/RGB_Module_RPI_code/rpi5_ws2812-0.1.2.dist-info to /usr/local/lib/python3.11/dist-packages

Move /home/pi/Desktop/PiTowerGen2/rgb_control.py to /home/pi/elecrow/

Move /home/pi/Desktop/PiTowerGen2/cfg/rgb_control.service to /etc/systemd/system/

sudo chmod +x /home/pi/elecrow/rgb_control.py

step 3:

Move /home/pi/Desktop/PiTowerGen2/cfg/rc.shutdown to /etc

Move /home/pi/Desktop/PiTowerGen2/cfg/rcshutdown.service to /etc/systemd/system/

Move /home/pi/Desktop/PiTowerGen2/cfg/shutdown.py to /usr/local/bin/

step 4:

Move /home/pi/Desktop/PiTowerGen2/cfg/shutdown.service to /etc/systemd/system/

Move /home/pi/Desktop/PiTowerGen2/cfg/shutdownsignal.py to /usr/local/bin/

Step 5:

sudo apt-get update

sudo apt-get install python3-psutil python3-smbus

sudo systemctl enable lcd_script.service

sudo systemctl start lcd_script.service

sudo systemctl enable rgb_control.service

sudo systemctl start rgb_control.service

sudo systemctl enable rcshutdown.service

sudo systemctl start rcshutdown.service

sudo systemctl enable shutdown.service

sudo systemctl start shutdown.service

Step 6:

Add "dtoverlay=i2c0" to the last line of /boot/firmware/config.txt and then restart the board.

