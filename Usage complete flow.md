Install Bluetooth Command Line Tools

Create a Connect batch script:

btcom -r -b aa:bb:cc:dd:ee:ff -s110b
btcom -c -b aa:bb:cc:dd:ee:ff -s110b

Create a Disconnect batch script:

btcom -r -b aa:bb:cc:dd:ee:ff -s110b

    Open Task Scheduler and Create Task

    Select Run whether user is logged on or not and Hidden (This will launch the script in the background so you don't see a command window pop up, or in your taskbar)

    Select Run with the highest privileges

    From Actions tab, select your Connect batch script

    Save and enter your password

Do the same as above for Disconnect, but Run with the highest privileges is not required.

    Now create a new shortcut for Connect and Disconnect

    For Target enter C:\Windows\System32\schtasks.exe /run /tn "Name of your Connect/Disconnect Task"

    Add custom icons to the shortcuts if you like

If you wish:

    Move shortcuts to "C:\ProgramData\Microsoft\Windows\Start Menu\Programs"

    Pin to start menu

Now you have a 2-click solution (Open start menu, click pinned icon).
