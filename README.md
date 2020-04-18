# Check Saved Wifi Password in Windows or Linux Using CMD Terminal or Simply Python3

## Python3


> **Prerequisites**<br>
* Have Python installed in Windows (or Unix)
* Pyhton version and Packages
* Here I am using Python 3.6.6 version<br>

```py
    import subprocess

    a = subprocess.check_output(['netsh', 'wlan', 'show', 'profiles']).decode('utf-8').split('\n')
    a = [i.split(":")[1][1:-1] for i in a if "All User Profile" in i]
    for i in a:
        results = subprocess.check_output(['netsh', 'wlan', 'show', 'profile', i, 'key=clear']).decode('utf-8').split('\n')
        results = [b.split(":")[1][1:-1] for b in results if "Key Content" in b]
        try:
            print ("{:<30}|  {:<}".format(i, results[0]))
        except IndexError:
            print ("{:<30}|  {:<}".format(i, ""))
```
<br>

> Subprocess Module <br>

We have first imported the required module subprocess. The subprocess module allows you to spawn new processes, connect to input/output/error pipes, and obtain their return codes.<br>

> Additional Command <br>

We have used command ***netsh wlan show profiles*** in our Python script to retrieve the stored key from profiles. It will retrieve all keys stored for all profiles in your system. If you have only one profile then it will retrieve for only one profile.

**Netsh** is a command-line scripting utility that allows you to display or modify the network configuration of a computer that is currently running.

**WLAN** commands that allow you to access the Wi-Fi profiles.

**Show** the list of wireless **profiles**.<br>

Source and Credit : https://www.roytuts.com/check-saved-password-in-wifi-network/
<br>





## WINDOWS

Whenever we connect to a Wi-Fi network and enter the password, Windows creates a WLAN profile of that Wi-Fi network. These WLAN profiles are stored in the computer alongside other required details of the Wi-Fi profile.<br>

We can uncover these WLAN profiles later by simply using Windows CMD. You can find out all the connected networks and their passwords by using simple commands. These commands can also uncover the Wi-Fi passwords of the networks which are not connected at the moment but were connected before. So it works even when you are offline or when you are connected to any other networks.

> **NOTE: Following command will only be executed by administrator** <br>

1. Open command prompt and run it as administrator.
2. Type **“netsh wlan show profile”** – It will show all profile of Wi-Fi which were earlier connected to the computer.

![img1](https://github.com/ishusagar/Check-Saved-Wifi-Password-in-Windows-or-Linux-Using-CMD-Terminal-or-Simply-Python3/blob/master/Images/img1.png)

3. Type this command without quotes ***“netsh wlan show profile fsociety key=clear”***<br>

![img2](https://github.com/ishusagar/Check-Saved-Wifi-Password-in-Windows-or-Linux-Using-CMD-Terminal-or-Simply-Python3/blob/master/Images/img2.png)

> Precaution which should be taken :<br>

1. Type netsh wlan show profiles (It will show different wi-fi which were connected)
2. Type netsh wlan delete profile name=”ProfileName” (Delete the desired profile)




## LINUX


To find the saved wifi password via command line, follow these steps: Login into Ubuntu and open up the “Terminal”” and enter these commands.

1. Type **cd /etc/NetworkManager/system-connections/** – It contains profile of Wi-Fis
2. Type **ls -a**

Now you will get name of the wifi networks saved on your pc. Now enter the following command with the name of your wifi network you want to find the password. You can find your password at “psk”=”PASSWORD”.

3. **sudo cat WIFI_SSID_Name**<br>

![img3](https://github.com/ishusagar/Check-Saved-Wifi-Password-in-Windows-or-Linux-Using-CMD-Terminal-or-Simply-Python3/blob/master/Images/img3.png)

> Precaution which should be taken : <br>

1. sudo ls -l /etc/NetworkManager/system-connections/<br>
To list all the files, after you have found the network that you want to delete, remove them with the command:<br>
2. sudo rm /etc/NetworkManager/system-connections/NETWORK_NAME <br>



Credit : Akash Sharan<br>
Source : https://www.geeksforgeeks.org/wi-fi-password-connected-networks-windowslinux/
