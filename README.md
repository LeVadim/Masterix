# Masterix
Message parser for Asterisk - MASTERIX
This plugin is for VoIP Asterisk messaging system.
I have been struggling with storing each data.
Original sms data is like so in extensions.conf ->
`${MESSAGE(from)} ${MESSAGE(to)}  ${MESSAGE(body)}`
 
1. ####### variable ############## output ################### we want
2. ####### `${MESSAGE(from)}` #### `sip:6464852453@192.168.1.12`  ## `6464852453`
3. ####### `${MESSAGE(to)}` ###### `<sip:6464852453@75.9.113.29>` ## `6464852453`
4. ####### `${MESSAGE(body)}` #### `+37126156072 \n Example Message` ######## `+37126156072 AND Example Message` 


# Installation


1. Put masterix.py into /var/lib/asterisk/agi-bin/

2. Install dependencies for python:
`pip install pyCLI`

3. Change in masterix.py sever http URL to which send the data
`http://example.com/sms/{{from}}/{{to}}/{{message}}`

# Usage 

extensions.conf

[example-contest]
 _xx.,1,AGI(masterix.py, -f '${MESSAGE(from)}', -t '${MESSAGE(to)}', -b '${MESSAGE(body)}')


# Comments
For using this app as Command Line Interface take the masterix and put it into /bin directory 
