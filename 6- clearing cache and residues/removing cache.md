When you stop an installation process using `Ctrl+Z`, the process is suspended, not terminated. This means the temporary files and downloaded data are likely still on your system. To clean up this data, you can follow these steps:

### Step 1: Resume and Properly Terminate the Process

First, resume the suspended process and then terminate it properly:

1. **List Suspended Jobs**:
   - Run the `jobs` command to list suspended jobs.
     ```sh
     jobs
     ```
   - You should see a list of jobs with numbers like `[1]+  Stopped  your_command`.

2. **Resume the Suspended Process in the Foreground**:
   - Use the `fg` command followed by the job number to bring the job back to the foreground.
     ```sh
     fg %1
     ```
   - Replace `1` with the correct job number if it's different.

3. **Terminate the Process Properly**:
   - Once the process is in the foreground, terminate it properly using `Ctrl+C`.

### Step 2: Clean Up Partial Installation Files

After terminating the process, you can remove any partially downloaded or temporary files.

1. **Clear the Package Cache**:
   - Debian-based systems store downloaded package files in `/var/cache/apt/archives/`. To remove these files, run:
     ```sh
     sudo apt-get clean
     ```
   - This command removes all packages from the apt cache, including the ones that were partially downloaded.

2. **Remove Temporary Files**:
   - Temporary files might also be stored in `/tmp` or other locations specific to the installer. You can manually clean the `/tmp` directory:
     ```sh
     sudo rm -rf /tmp/*
     ```
   - Be cautious with this command, as it will delete all files in `/tmp`.

3. **Check for Unused Packages**:
   - If the installation process installed any dependencies before you stopped it, you might want to remove unused packages:
     ```sh
     sudo apt-get autoremove
     ```
   - This command will remove any packages that were installed as dependencies but are no longer needed.

### Step 3: Verify Disk Space

After cleaning up, check your disk space to ensure that the data has been removed:

1. **Check Disk Usage**:
   - Run the following command to see how much disk space is being used:
     ```sh
     df -h
     ```

2. **Check the Cache Directory**:
   - Verify that the package cache is now empty:
     ```sh
     ls /var/cache/apt/archives/
     ```

By following these steps, you should be able to remove the 2GB of data that was partially downloaded during the installation. If you need further assistance, feel free to ask!