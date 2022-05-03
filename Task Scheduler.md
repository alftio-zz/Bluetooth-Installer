
    Install Bluetooth Command Line Tools
    you can use the command line tools to display all device ids by simply running btdiscovery
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
        find an image and remove the background
        convert the transparent png image to a .ico

Adding to start menu

You have two options:

    Move shortcuts to C:\ProgramData\Microsoft\Windows\Start Menu\Programs
    Pin to start menu

other

credit to /u/howheels on reddit
