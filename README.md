# Check Saved Wifi Password in Windows or Linux Using CMD Terminal or Simply Python3

### Python 3

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
