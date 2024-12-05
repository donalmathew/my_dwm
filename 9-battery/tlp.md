To change the setting `CPU_ENERGY_PERF_POLICY_ON_BAT="balance_power"` in TLP, you need to modify the TLP configuration file. Here’s how you can do it:

## Steps to Change CPU Energy/Performance Policy on Battery

1. **Open the TLP Configuration File**:
   The TLP configuration file is typically located at `/etc/tlp.conf`. You can open it using a text editor with root permissions. For example, using `nano`:

   ```bash
   sudo nano /etc/tlp.conf
   ```
----------------------------
## note: ensure that TLP_ENABLE=1
-----------------

2. **Locate the Setting**:
   Search for the line that contains `CPU_ENERGY_PERF_POLICY_ON_BAT`. It may look like this:

   ```bash
   CPU_ENERGY_PERF_POLICY_ON_BAT="balance_power"
   ```

3. **Change the Value**:
   Modify the value to your desired setting. The available options are:
   - `performance`
   - `balance_performance`
   - `default`
   - `balance_power`
   - `power`

   For example, if you want to change it to `default`, you would edit the line to:

   ```bash
   CPU_ENERGY_PERF_POLICY_ON_BAT="default"
   ```

4. **Save and Exit**:
   After making your changes, save the file and exit the text editor. In `nano`, you can do this by pressing `CTRL + X`, then `Y` to confirm changes, and `Enter` to exit.

5. **Restart TLP**:
   To apply the changes, restart TLP with the following command:

   ```bash
   sudo tlp restart
   ```

## Summary of Options

Here’s a quick overview of what each policy does:

| Policy                | Description                                           |
|----------------------|-------------------------------------------------------|
| **performance**      | Maximizes performance without regard for energy efficiency. |
| **balance_performance** | Prioritizes performance while allowing some energy savings. |
| **default**          | A standard balance between performance and energy efficiency. |
| **balance_power**    | Focuses more on energy savings than performance.     |
| **power**            | Maximizes energy efficiency at a significant cost to performance. |

By following these steps, you can effectively change your CPU energy/performance policy while on battery power in TLP.




### chat-gpt
Yes, you can make these power-saving settings permanent by configuring them in the TLP configuration file. Here’s how:

1. **Edit the TLP Configuration File**

   Open the TLP configuration file at `/etc/tlp.conf`:

   ```bash
   sudo nano /etc/tlp.conf
   ```

2. **Configure CPU Scaling and Power Preferences**

   To reduce power usage permanently, you can set the CPU governor, disable Turbo Boost, and adjust energy performance preferences specifically for battery mode. Find or add these lines to the file:

   ```plaintext
   # Set CPU governor to powersave on battery mode
   CPU_SCALING_GOVERNOR_ON_BAT=powersave

   # Set maximum CPU performance on battery
   CPU_MAX_PERF_ON_BAT=50

   # Disable Turbo Boost on battery mode to save power
   CPU_BOOST_ON_BAT=0

   # Use energy-efficient profile when on battery
   CPU_ENERGY_PERF_POLICY_ON_BAT=power
   ```

3. **Optimize Workqueues and USB Autosuspend**

   Set the power-efficient workqueues and enable USB autosuspend to save power. Add these lines if they’re not already set:

   ```plaintext
   # Enable power-efficient workqueues on battery
   POWER_SUPPLY_WORKQUEUE_ON_BAT=Y

   # Enable USB autosuspend for power savings
   USB_AUTOSUSPEND=1
   ```

4. **Adjust Other Power-Saving Options**

   Consider disabling unused features like Wi-Fi power and sound power saving on battery:

   ```plaintext
   # Power-saving options for Wi-Fi, Bluetooth, and sound
   WIFI_PWR_ON_BAT=5
   SOUND_POWER_SAVE_ON_BAT=1
   ```

5. **Save and Exit**

   After making these changes, save the file and exit the editor.

6. **Restart TLP to Apply Changes**

   To activate the new settings without rebooting, restart TLP:

   ```bash
   sudo tlp start
   ```

7. **Verify the Configuration**

   To check if the settings are applied correctly, you can use:

   ```bash
   sudo tlp-stat -p
   ```

These settings will now be applied automatically every time you boot into battery mode. If you need to adjust any settings later, you can simply edit `/etc/tlp.conf` again and restart TLP.


### bluetooth not turning on after this:

5. **Unblock Bluetooth with `rfkill`**

   In some cases, the Bluetooth device may be soft-blocked (disabled by software). Check and unblock it with `rfkill`:

   ```bash
   rfkill list all
   ```

   If Bluetooth is listed as "Soft blocked: yes," unblock it with:

   ```bash
   sudo rfkill unblock bluetooth
   ```

These methods should help you enable Bluetooth on Debian even if TLP has restricted its power usage.
