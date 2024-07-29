The document contains useful information regarding setting up screen brightness control in Hyprland using `brightnessctl`. Here are the relevant excerpts and steps to set it up:

### Using `brightnessctl` in Hyprland

1. **Install `brightnessctl`:**

   Ensure you have `brightnessctl` installed on your system:

   ```sh
   sudo apt install brightnessctl
   ```

2. **Configure Key Bindings in Hyprland:**

   Add the following binds to your Hyprland configuration file (usually `~/.config/hypr/hyprland.conf` or similar):

   ```ini
   # Screen brightness
   bind = XF86MonBrightnessUp,exec,brightnessctl s +5%
   bind = XF86MonBrightnessDown,exec,brightnessctl s 5%-
   ```

   This setup binds the `XF86MonBrightnessUp` and `XF86MonBrightnessDown` keys to increase and decrease the screen brightness by 5%.

3. **Create a Script for Syncing Multiple Monitors:**

   If you have multiple monitors and want to sync their brightness, you can use a script similar to the one provided earlier. Here is an enhanced version that incorporates the `brightnessctl` commands:

   ```sh
   #!/bin/bash

   # Define the backlight interfaces for your monitors
   monitor1="intel_backlight"
   monitor2="acpi_video0"

   # Get the current brightness level of the primary monitor
   current_brightness=$(brightnessctl -d $monitor1 get)
   max_brightness=$(brightnessctl -d $monitor1 max)
   current_percentage=$(echo "$current_brightness * 100 / $max_brightness" | bc)

   # Adjust the brightness based on the argument (up or down)
   if [ "$1" == "up" ]; then
       new_percentage=$(echo "$current_percentage + 5" | bc)
   elif [ "$1" == "down" ]; then
       new_percentage=$(echo "$current_percentage - 5" | bc)
   fi

   # Ensure the new percentage is within the range 0-100
   if [ "$new_percentage" -gt 100 ]; then
       new_percentage=100
   elif [ "$new_percentage" -lt 0 ]; then
       new_percentage=0
   fi

   # Set the new brightness level for both monitors
   brightnessctl -d $monitor1 set ${new_percentage}%
   brightnessctl -d $monitor2 set ${new_percentage}%
   ```

   Make the script executable:

   ```sh
   chmod +x ~/.config/hypr/sync_brightness.sh
   ```

4. **Bind the Script to Key Combinations in Hyprland:**

   Add the following lines to your Hyprland configuration file to bind the brightness control script to the `XF86MonBrightnessUp` and `XF86MonBrightnessDown` keys:

   ```ini
   bind = XF86MonBrightnessUp,exec,~/.config/hypr/sync_brightness.sh up
   bind = XF86MonBrightnessDown,exec,~/.config/hypr/sync_brightness.sh down
   ```

5. **Reload Hyprland Configuration:**

   After updating your configuration, reload Hyprland to apply the changes:

   ```sh
   hyprctl reload
   ```

These steps will enable you to control and sync the brightness of your monitors using the `XF86MonBrightnessUp` and `XF86MonBrightnessDown` keys in Hyprland. Adjust the script and configuration as necessary to fit your specific setup.