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