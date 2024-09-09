there are 2 ways that worked for me.
there are also other methods like creating **.xinitc** file (refer. chatgpt).



## 1.making a .sh-file in home directory and executing it at every startup

1. create startup.sh file in home directory
```sh
sudo nano startup.sh
```

2. add all the codes to be executed to the file
eg:
>place & at end of each line to parallelly execute them(mistake in a particular line will not affect others)
```sh
# Enable tap-to-click
xinput set-prop 10 "libinput Tapping Enabled" 1 &
xinput set-prop 11 "libinput Tapping Enabled" 1 &
xinput set-prop 10 "libinput Natural Scrolling Enabled" 1 &
xinput set-prop 11 "libinput Natural Scrolling Enabled" 1 &
xinput set-prop 11 "libinput Accel Speed" 0.77 &
xinput set-prop 10 "libinput Accel Speed" 0.77 &
#screen timeout
xset s 120 &

#change refresh rate
xrandr --output eDP-1 --mode 2880x1800 --rate 60 &

#battery saver
sudo tlp start &
```

3. during each startup, execute startup.sh file
```sh
sh startup.sh
```


## (not verified as working by me)2. adding the script file to autostart in `config file`

### an example case(read and you will understand)
To display the battery charge percentage in the **dwm** top bar (status bar), you can modify the status string using a script that retrieves the battery status and updates it regularly. This is done by setting the **status text** in `dwm` using the `xsetroot` command, which updates the root window's name, and thus the status bar.

Here are the steps:

### Step 1: Create a Script to Fetch Battery Percentage

1. Open a terminal and create a new script:
   ```bash
   nano ~/battery-status.sh
   ```

2. Add the following script to fetch the battery percentage and update the dwm status bar:
   ```bash
   #!/bin/bash

   while true; do
       # Get battery percentage (for systems with UPower)
       battery=$(upower -i $(upower -e | grep BAT) | grep -E "percentage" | awk '{print $2}')

       # Set the battery status in dwm's status bar
       xsetroot -name "Battery: $battery"

       # Update every 60 seconds
       sleep 60
   done
   ```

3. Save the file and exit.

### Step 2: Make the Script Executable

You need to make the script executable:
```bash
chmod +x ~/battery-status.sh
```

### Step 3: Add the Script to Autostart in dwm

To ensure that the battery status updates every time you log in to dwm, you can make the script run automatically at startup.

1. If you already have a startup script (like `autostart.sh`), add this line to it. If you don't have one, create the file `autostart.sh` in the same directory as dwm's configuration.

   ```bash
   nano ~/dwm/autostart.sh
   ```

2. Add the following lines:
   ```bash
   #!/bin/bash
   ~/battery-status.sh &
   ```

3. Make the autostart script executable:
   ```bash
   chmod +x ~/dwm/autostart.sh
   ```

4. Modify `config.h` to run the autostart script when dwm starts. Add this line at the bottom of your `config.h` (just before the keybindings):
   ```c
   static void autostart(void) {
       system("~/dwm/autostart.sh");
   }
   ```

5. In your `config.h`, after `setup();` in the `main` function, add the following line:
   ```c
   autostart();
   ```

### Step 4: Recompile dwm

To apply the changes, recompile dwm:

1. In the directory where your `dwm` source code is located:
    ```bash
   cd ~/dwm
   sudo make clean install
   ```

2.  restart dwm:
    ```sh
    killall dwm
    ```