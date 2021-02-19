The RPI will often place a yellow lighening bolt in the upper right hand corner

This is a low power warning.

Many times, it does not affect the performance.

Turn off the low power warning 
~~~
sudo nano /boot/config.txt
~~~

# Disable under-voltage warning
avoid_warnings=1
#or 
#allows turbo when low-voltage is present
avoid_warnings=2

sudo reboot
