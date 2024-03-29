# Connect/Disconnect Bluetooth Audio Device 

## Instructions

1. Install  [Bluetooth command line tools](https://bluetoothinstaller.com/bluetooth-command-line-tools/BluetoothCLTools-1.2.0.56.exe)
2. Open a cmd window
3. Get the Bluetooth MAC Ids for the current bluetooth devices by executing the next command

```
btdiscovery
```

4. Create a Connect Batch (.bat) script with the next lines
   - Note: Replace the Bluetooth Media Access Control address, (XX:XX:XX:XX:XX:XX) format.
   
   ```
    btcom -r -b 1c:e6:1d:33:e9:09 -s110b
    btcom -c -b 1c:e6:1d:33:e9:09 -s110b
   ```
   
5. Create a Disconnect Batch (.bat) script with the next lines
   
    ```
    btcom -r -b 1c:e6:1d:33:e9:09 -s110b
    ```
6. Get previously created batch (.bat) files and execute them to test the behavior.

7. Create the Shortcut from Windows
   7.1 Right click on the desktop area.
   7.2 Select, "New" → "Shortcut"
   7.3 Type the location of the  batch (.bat) file. I.E.:  batch (.bat)
   7.4 Type a name for the shortcut
