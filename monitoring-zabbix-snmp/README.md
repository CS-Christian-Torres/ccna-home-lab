
1. Stop the Annoying "Translating... Domain Server" HangIf you misspell a command (like typing clera instead of clear), the CLI will freeze for 30 seconds trying to look it up on the internet. Turn this off globally:textRouter(config)# no ip domain-lookup

Use code with caution.2. Stop Log Messages from Cutting Your Sentences in HalfWhen an interface goes up or down, the status message prints directly over what you are currently typing. This command pushes the alert messages to a new line, keeping your typed command completely clean:textRouter(config)# line console 0
Router(config-line)# logging synchronous
Router(config-line)# exit
Use code with caution.3. Prevent the CLI Session from Timing OutBy default, the CLI will kick you out if you don't type anything for a few minutes. Set the timeout to zero so your session stays open forever while you study:textRouter(config)# line console 0
Router(config-line)# exec-timeout 0 0

SSH CONFIG
The Quick Template for the Rest of Your DevicesTo avoid this error on your other routers and switches, simply add a custom name to the top of your paste script for each device:For Router 1:texthostname R1
ip domain-name lab.com
crypto key generate rsa general-keys modulus 1024
username a privilege 15 secret a
line vty 0 4
transport input ssh
login local
exit

SWITCH SSH CONFIG
