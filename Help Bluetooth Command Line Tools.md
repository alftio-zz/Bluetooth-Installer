Currently there are following utilities in the suite:

## btinfo

  Displays information about installed bluetooth adapter. Output format can be customized.

  usage:

    btinfo [-n] [-a] [-t] [-s] [-b] [-m] [-d] [-c] [-f{FormatString}]

     -n  Print friendly name
     -a  Print bluetooth address
     -t  Print class-of-device (CoD)
     -s  Print subversion
     -b  Print manufacturer name (decoded from bluetooth address)
     -m  Print chip namufacturer name
     -d  Print discovery state
     -c  Print connectable state
     -f  Print information using provided format string.
     -h  Print help screen.

     When run without switches full local radio information is printed.

     The -f switch supports the following format specifiers:

       %n% - friendly name
       %a% - bluetooth address
       %t% - class-of-device (CoD)
       %s% - subversion
       %b% - manufacturer name
       %m% - chip namufacturer name
       %d% - discovery state
       %c% - connectable state
       \n  - new line
       \t  - tab
       \\  - backslash
       All other characters are displayed as-is.

----------------------------------------------------------------------------------------------------------

## btconfig

  Modifies friendly name and class-of-device (desktop, laptop, server) of the local bluetooth radio.     Turns discovery on or off. Ebables or disables incoming bluetooth connections.

  usage:

    btconfig [-n[NewName]] [-t[desktop|server|laptop]] [-d{0|1}] [-c{0|1}]
             [-a{0|1}] [-i{0|1}]

     -n  Changes fiendly name of the local bluetooth radio.
         Resets friendly name to default(computer name) if NewName is not provided.
     -t  Changes class-of-device (CoD) for the local bluetooth radio. 
         Valid values are "desktop", "server" or "laptop".
     -d  Turns discovery on or off. if necessary makes local radio connectable.
     -c  Changes connectable state of local bluetooth radio. Discovery is turned
         off when incoming connections are disabled.
     -i  Enables or disables bluetooth icon in the windows notification area.
     -a  Enables or disables alerts when a remote Bluetooth device wants to connect.
     -h  Prints help screen.

     Notes: -n and -t switches require administrative privileges.
            -d1 and -c0 are mutually exclusive.

----------------------------------------------------------------------------------------------------------

## btdiscovery

  Discovers remote blueotooth devices and services.

  usage:

    btdiscovery [-iSeconds] [-bBluetoothAddress | -nFriendlyName] [-dFormat] [-s[Format]]

     -i  Set the length of inquiry to the specified number of seconds.
     -b  Bluetooth address of remote device in (XX:XX:XX:XX:XX:XX) format.
     -n  Friendly name of temote device.
     -d  Set output format for the list of discovered devices.
     -s  Make service discovery. Optionally set output format for the list of services.
     -h  Prints help screen.

    Notes: if -n or -b are set, btdiscovery returns data obtained from that device only.

     The -d switch supports the following format specifiers:

       %n% - friendly name
       %a% - bluetooth address
       %t% - class-of-device (CoD)
       %r% - remembered
       %p% - authenticated
       %c% - connected
       %s% - lastseen
       %u% - lastused
       %b% - manufacturer name
       \n  - new line
       \t  - tab
       \\  - backslash
       All other characters are displayed as-is.

     The -s switch supports the following format specifiers:

       %sn% - service name
       %su% - UUID
       %si% - short UUID
       %sc% - RFCOMM channel
       \n  - new line
       \t  - tab
       \\  - backslash
       All other characters are displayed as-is.


    Samples:
      1. Discover all devices and thier services, display information in default format:
      
         btdiscovery -s

      2. Discover all devices and return display addresses only:

         btdiscovery -d"%a%"

      2. Discover services from the device named "Nokia 6630" and display names and channels:

         btdiscovery -n"Nokia 6630" -s"%sc% - %sn%"

----------------------------------------------------------------------------------------------------------
## btpair

  Bluetooth device pairing utility


  usage:

    btpair {-p[PIN] | -u} [-bBluetoothAddress | -nFriendlyName]

       -p  Pair your computer with remote device using specified PIN code.
           If no pin specified, the default ('0000') is used.
       -u  Unpair remote device.
       -b  Bluetooth address of remote device in (XX:XX:XX:XX:XX:XX) format.
       -n  Friendly name of remote device.
       -h  Prints this help screen.

  Note:
    Usually pairing is not enough for the remote bluetooth device to function properly.
    One ore more remote bluetooth services should be enabled using "btcom" utility.

  samples:

    1. Pair your computer and device named "Nokia 6300" using PIN code 1234 :

	    btpair -n"Nokia 6300" -p1234

    2. Unpair all remembered devices: 

            btpair -u

----------------------------------------------------------------------------------------------------------

## btobex

  Sends files to remote OBEX capable devices (computers, mobile phones, etc).

  usage:

    btobex {-bBluetoothAddress | -nFriendlyName} [-cChannel] [-pPIN [-e]] 
           [-rRetries] [-fFileName] [file1 [file2 [...]]] 

      -b  Bluetooth address of target device in (XX:XX:XX:XX:XX:XX) format. 
      -n  Friendly name of target device.
      -c  RFCOMM channel (1-30). If specified, service lookup is not performed. 
      -p  PIN code for authenticating with remote device.
      -e  Use encrypted connection (only if PIN authentication is used)
      -r  Make specified number of attempts is case of error
      -f  Use this file name for the data from STDIN (standard input)
      -h  Prints help screen.

  samples:

    1. Send file "picture.jpg" from the current folder to the device named "Nokia 6300" :

	    btobex -n"Nokia 6300" picture.jpg

    2. Send all text files from the current folder to the device with known address : 

            btobex -b(11:11:22:22:33:33) *.txt

    3. Send output of other program as a file named "message.txt" :

            echo This is a test | btobex -b(11:11:22:22:33:33) -f"message.txt"


----------------------------------------------------------------------------------------------------------

## btftp 

  Exchanges files with remote bluetooth device using OBEX file transfer profile

  Usage:

    btftp {-bBluetoothAddress | -nFriendlyName} [-cChannel] [-pPIN [-e]] 
          [-dRemoteFolder] [-a{get|put|list|delete}] file1 file2 ... 

     -b  Bluetooth address of target device in (XX:XX:XX:XX:XX:XX) format. 
     -n  Friendly name of target device.
     -c  RFCOMM channel (1-30). If specified, service lookup is not performed. 
     -a  Action to be performed. 
     -p  PIN code for authenticating with remote device.
     -e  Use encrypted connection (only if PIN authentication is used)
     -h  Prints this help screen.


  Notes:
    1. Using OBEX FTP profile usually requires authentification. Use -p switch with a PIN code or pair 
       the remote device before using btftp.
    2. Wildcards in remote file specifications are not supported in the current release of btftp.

  samples:

    1. List contents of root folder of the device named "Nokia 6630" :

	    btftp -n"Nokia 6630" -alist

    2. Get the file "e:\images\img001.jpg" from the device named "Nokia 6630" :

	    btftp -n"Nokia 6630" -aget -d"e:\images" img001.jpg

    2. Copy all text files from the current folder to the "e:\data" folder of the remote device with known address : 

            btftp -b(11:11:22:22:33:33) -aput -d"e:\data" *.txt

----------------------------------------------------------------------------------------------------------

## btcom 
  
   Enables or disables remote bluetooth services, manipulates bluetooth COM ports.

  
  Usage:

    btcom {-c|-r} {-bBluetoothAddress | -nFriendlyName} [-s{sp|dun|GUID|UUID}]

     -c  Create association between COM port and a remote service (Enable non-COM service).
     -r  Remove association between COM port and a remote service (Disable non-COM service).
     -s  Remote service to use (Default is Serial Port Service)
     -b  Bluetooth address of remote device in (XX:XX:XX:XX:XX:XX) format. 
     -n  Friendly name of remote device.
     -h  Prints this help screen.

  Notes: 
    1. Service can be specified as a GUID (e.g. {00001124-0000-1000-8000-00805F9B34FB}) or short UUID (e.g. 1124).
    2. Im most cases the remote device should be paired first before using "btcom" utility.

  samples:

    1. Associate Dialup Networking service of the device named "Nokia 6630" with local COM port:

	    btcom -n"Nokia 6630" -c -sdun

    2. Enable HID service of the Bluetooth mouse

            btcom -b"00:01:02:03:FF:FF" -c -s1124



All utilities maintain the ERRORLEVEL environment variable. Zero means successful execution, any other value - error.
Detailed error description is printed to the standard error output.
