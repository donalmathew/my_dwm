To uninstall Dolphin from your Linux system, you can use the package manager that you used to install it. Here’s how you can uninstall Dolphin using `apt` on Debian-based distributions (such as Ubuntu):

### Uninstall Dolphin

1. **Open a Terminal**:
   - You can open a terminal from your applications menu or by pressing `Ctrl+Alt+T`.

2. **Uninstall Dolphin**:
   - Run the following command to uninstall Dolphin:
     ```sh
     sudo apt remove dolphin
     ```

3. **Remove Unnecessary Packages**:
   - To remove any dependencies that were installed with Dolphin but are no longer needed, you can run:
     ```sh
     sudo apt autoremove
     ```

This will remove Dolphin from your system along with any unnecessary dependencies. If you have any configuration files or user settings related to Dolphin that you want to remove as well, you can use the `purge` command:

### Uninstall and Purge Dolphin

1. **Uninstall and Purge Dolphin**:
   - Run the following command to completely remove Dolphin along with its configuration files:
     ```sh
     sudo apt purge dolphin
     ```

2. **Remove Unnecessary Packages**:
   - Run the autoremove command again to clean up any remaining dependencies:
     ```sh
     sudo apt autoremove
     ```

## Cleaning the build directory to avoid issues with the previous failed build:
```sh
rm -rf build
```