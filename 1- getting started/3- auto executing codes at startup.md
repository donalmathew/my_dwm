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
xinput set-prop 11 "libinput Accel Speed" 0.5 &
xinput set-prop 10 "libinput Accel Speed" 0.5 &
#screen timeout
xset s 120 &

#change refresh rate
xrandr --output eDP-1 --mode 2880x1800 --rate 60 &
```

3. during each startup, execute startup.sh file
```sh
sh startup.sh
```