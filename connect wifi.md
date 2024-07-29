To install `iwctl`, which is part of `iwd` (iNet Wireless Daemon), on a Linux distribution, you generally follow these steps:

1. **Update your package list** to ensure you have the latest information about available packages:
   ```sh
   sudo apt update
   ```

2. **Install `iwd`**, which includes `iwctl`:
   ```sh
   sudo apt install iwd
   ```

3. **Enable and start the iwd service** to make sure it runs automatically:
   ```sh
   sudo systemctl enable iwd
   sudo systemctl start iwd
   ```

To connect to a Wi-Fi network using `iwctl`, follow these steps:

1. **Start `iwctl`:**
   ```sh
   iwctl
   ```

2. **List available devices:**
   ```sh
   device list
   ```

3. **Select the Wi-Fi device (typically `wlan0`):**
   ```sh
   station wlan0 scan
   ```

4. **List available Wi-Fi networks:**
   ```sh
   station wlan0 get-networks
   ```

5. **Connect to a network:**
   ```sh
   station wlan0 connect YOUR_SSID
   ```
   Replace `YOUR_SSID` with the name of your Wi-Fi network. You will be prompted to enter the Wi-Fi password.

6. **Verify the connection:**
   ```sh
   station wlan0 show
   ```

Here's a complete example:

```sh
sudo iwctl
```

Within the `iwctl` interactive prompt:

```sh
device list
station wlan0 scan
station wlan0 get-networks
station wlan0 connect YOUR_SSID
```

Replace `YOUR_SSID` with your network's SSID. Follow the prompts to enter the password, and you should be connected.

If you need further assistance or run into any issues, let me know!


$ nmcli device wifi connect SSID_or_BSSID password password ifname wlan0