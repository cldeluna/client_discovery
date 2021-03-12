# Client Discovery Utilities



<img src="images/EIAlogo_OnWhite-01-Transparent.jpg" alt="EIAlogo_OnWhite-01-Transparent" style="zoom:5%;" />

##Synopsis

Commonly used Netmiko utilities for client discovery.



##Installation



```
pip install -r requests.txt
```



##Usage



#### get_showcmds.py

By default, providing the IP or FQDN of a network device with the -d option, executes the associated set of show commands in the show_cmds.yml file on the provided IP or FQDN, and saves the output to a timestamped file with an optional note.  The output is saved, by default,  in a directory under the current working directory named "local".  The ***-o*** or ***--output_subdir*** can be used to save output in a different subdirectory.

By default the script will load credentials as environment variables and with the -m option (for Multi Factor Authentication) concatenate a password with the VIP Access Security Code so as to minimize typing.

The script also supports an option ***-c*** or ***--credentials*** argument which interactively requests the username, password, and enable password to be used.  Passwords are not echoed back and credentials are not saved.

The script has a variety of option to tailor the script execution.

An optional device type can be provided. The default device type cisco_ios.

This script executes show commands either via a single show command provided with the ***-s***  or ***--show_cmd*** option on the CLI when the script is called or via a set of standard show commands loaded from a YAML file based on device type.



##### Executing show commands across multiple devices with the same credentials

The script can take in a list of IPs or FQDNs in a text file using the ***-f*** or ***--file_of_devs*** option.

Example:

In this example the get_showcmds.py file is executed with 

- The -c option so that credentials are provided via the command line interactively
- The -s option is used to only run the "show version" command
- The -f option is used to execute this agains the IPs or FQDNs in the provided text file.

```
(client_discovery) claudia@Claudias-iMac client_discovery % python get_showcmds.py -c -s "show ver" -f example_device_file.txt
===== Date is 2021-03-12 ====
Username [claudia]: cisco
Password and Enable Password will not be echoed to the screen or saved.
*** These credentials will be use for all devices in the file example_device_file.txt***
Password: 
Enable: 

===============  Device 10.1.10.212 ===============
--- Show Command: show ver

Saving show command output to /Users/claudia/Dropbox (Indigo Wire Networks)/scripts/python/2021/client_discovery/local/10.1.10.212_2021-03-12.txt



===============  Device 10.1.10.216 ===============
--- Show Command: show ver

Saving show command output to /Users/claudia/Dropbox (Indigo Wire Networks)/scripts/python/2021/client_discovery/local/10.1.10.216_2021-03-12.txt


(client_discovery) claudia@Claudias-iMac client_discovery % 


```



##### Text File

```
(client_discovery) claudia@Claudias-iMac client_discovery % cat example_device_file.txt 
10.1.10.212
10.1.10.216


```





#### Help

Use the -h option to see the script options.

```
(client_discovery) claudia@Claudias-iMac client_discovery % python get_showcmds.py -h
usage: get_showcmds.py [-h] [-d DEVICE] [-t DEVICE_TYPE] [-p PORT] [-o OUTPUT_SUBDIR] [-s SHOW_CMD] [-n NOTE] [-m] [-c] [-f FILE_OF_DEVS]

Script Description

optional arguments:
  -h, --help            show this help message and exit
  -d DEVICE, --device DEVICE
                        Get show commands from this device (ip or FQDN) and save to file
  -t DEVICE_TYPE, --device_type DEVICE_TYPE
                        Device Types include cisco_nxos, cisco_asa, cisco_wlc Default: cisco_ios
  -p PORT, --port PORT  Port for ssh connection. Default: 22
  -o OUTPUT_SUBDIR, --output_subdir OUTPUT_SUBDIR
                        Name of output subdirectory for show command files
  -s SHOW_CMD, --show_cmd SHOW_CMD
                        Execute a single show command
  -n NOTE, --note NOTE  Short note to distinguish show commands. Ex. -pre or -post
  -m, --mfa             Multi Factor Authentication will prompt for VIP code
  -c, --credentials     Set Credentials via Command Line interactively
  -f FILE_OF_DEVS, --file_of_devs FILE_OF_DEVS
                        Provide the full path to a text file containing an IP or FQDN on each line (see example_device_file.txt) to execute show commands on multiple devices with the same credentials.

Usage: ' python get_showcmds.py -d my_switch_hostname.my.domain'
(client_discovery) claudia@Claudias-iMac client_discovery % 



```





##Licensing

This code is licensed under the BSD 3-Clause License. See [LICENSE](LICENSE) for details.