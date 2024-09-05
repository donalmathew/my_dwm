> config file is usually located in the same folder where the installation files are located

### **Restart dwm**:
    You can either log out and back in, or restart dwm by killing and restarting it:
    ```bash
    killall dwm
    ```

## 1. ensure git is installed

changes to config file must be tracked.

## 2. know your desktop session
>codes to be executed in the startup has to be in different files according to sessions

```sh
echo $DESKTOP_SESSION
```

## 3. create an autostart script
>this has to be inside the installation folder where you type: "sudo make clean install"

```sh
touch ~/.dwm/autostart.sh
chmod +x ~/.dwm/autostart.sh
```

example:

```sh
#!/bin/sh
xsetroot -name "dwm" &
```
