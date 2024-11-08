Yes, disabling some CPU cores can reduce power consumption and potentially extend battery life, especially during light tasks where not all cores are needed. However, there are some considerations and methods to do this.

### How Disabling CPU Cores Saves Battery
Modern CPUs save power by reducing active cores and frequencies when idle, but manually disabling cores can help by further reducing power usage on battery, especially if your workload is light (like browsing or document editing). However, doing this may reduce system performance, so it’s best to test if it suits your needs.

### Methods to Disable CPU Cores on Linux

1. **Using `maxcpus` Kernel Parameter (Permanent)**  
   You can limit the number of active cores by modifying the kernel boot parameters. This is a more permanent method and is effective immediately on boot.

   - Open the GRUB configuration file:

     ```bash
     sudo nano /etc/default/grub
     ```

   - Find the line starting with `GRUB_CMDLINE_LINUX_DEFAULT` and add `maxcpus=X` (replace `X` with the number of cores you want to keep active). For example, to keep only 4 cores active, you would modify it like this:

     ```plaintext
     GRUB_CMDLINE_LINUX_DEFAULT="quiet splash maxcpus=4"
     ```

   - Save the file, then update GRUB:

     ```bash
     sudo update-grub
     ```

   - Reboot your system for the changes to take effect.

2. **Disabling Cores Dynamically Using `echo` Commands (Temporary)**  
   This method is less permanent and only affects the current session, so it’s useful if you want to test how core disabling affects battery life.

   - To disable a specific CPU core, write `0` to its `online` file. For example, to disable CPU core 3:

     ```bash
     echo 0 | sudo tee /sys/devices/system/cpu/cpu3/online
     ```

   - To re-enable it, write `1` to the same file:

     ```bash
     echo 1 | sudo tee /sys/devices/system/cpu/cpu3/online
     ```

   - You can repeat this for other cores (e.g., `cpu4`, `cpu5`, etc.), but avoid disabling `cpu0`, as it’s required for system stability.

3. **Automating with a Script**  
   To automate this process when on battery power, you can create a script and add it to TLP’s hooks or set it to run on startup.

   - Create a script, for example `disable_cores.sh`:

     ```bash
     sudo nano /usr/local/bin/disable_cores.sh
     ```

   - Add commands to disable specific cores:

     ```bash
     #!/bin/bash
     echo 0 | tee /sys/devices/system/cpu/cpu3/online
     echo 0 | tee /sys/devices/system/cpu/cpu4/online
     ```

   - Make the script executable:

     ```bash
     sudo chmod +x /usr/local/bin/disable_cores.sh
     ```

   - Add the script to TLP's hooks to run it when on battery power by placing it in the `/etc/tlp.d` directory or configuring it to run as part of the startup sequence.

### Considerations
- **Performance Impact**: Disabling cores will reduce the ability to handle multitasking and high-performance tasks.
- **Dynamic Power Management**: Modern CPUs often manage cores dynamically, so disabling cores manually may interfere with the CPU’s built-in power management.
- **Testing**: It’s a good idea to test how battery life and performance are impacted before making it permanent.