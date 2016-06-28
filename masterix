#!/usr/bin/python
# -*- coding: utf-8 -*-
import sys,requests,cli.app

class bcolors:
    HEADER = '\033[95m'
    OKBLUE = '\033[94m'
    OKGREEN = '\033[92m'
    WARNING = '\033[93m'
    FAIL = '\033[91m'
    ENDC = '\033[0m'
    BOLD = '\033[1m'
    UNDERLINE = '\033[4m'


class Parser:

        def __init__(self,message_from,message_to,message_body,url):
                self.base_url = url
                self.message_to = message_to
                self.message_from = message_from
                self.message_body = message_body

        def parse_message_to(self):    #### sip:6464852453@192.168.1.12
                parse1 = self.message_to.split("@")
                parse2 = parse1[0].split(":")
                message_to_number = parse2[1]
                return message_to_number

        def parse_message_from(self):  #### 6464852453 <sip:6464852453@75.9.113.29>
                parsedString = self.message_body.split('\n')
		#print(parsedString)
                return parsedString[0]

        def parse_message_body(self):
		#print(self.message_body)
                parsedString2 = self.message_body.split('\n') 
                return parsedString2[1]

        def parse_url(self):
                return str(self.base_url+str(self.parse_message_from())+'/'+str(self.parse_message_to())+'/'+str(self.parse_message_body()))
 


@cli.app.CommandLineApp()
def masterix(app):
	if app.params.mfrom == None or app.params.to == None or app.params.body == None:
		print(bcolors.BOLD + bcolors.FAIL + "Missing required params! \n"+ bcolors.OKBLUE + "Type masterix -h or masterix --help")
	else:
		try:
			print(bcolors.BOLD + bcolors.HEADER + "Parsing input")
			ParserObj = Parser(app.params.mfrom,app.params.to,app.params.body,'http://example.com/sms/')
                	REQUEST_URL = ParserObj.parse_url()
			print(bcolors.BOLD + bcolors.HEADER + "Sending request")
                	r = requests.post(REQUEST_URL)
			print(REQUEST_URL)
                	print(bcolors.BOLD + bcolors.OKGREEN + str(r))
                        print(bcolors.BOLD + bcolors.OKBLUE+'Everythink completed. OK!')
		except Exception:
			print(bcolors.BOLD + bcolors.FAIL + "An error occured! \n"+bcolors.OKBLUE+'Please try again later')

		

masterix.add_param('-f','--mfrom',help='parse from number from which message has sent',default=None)
masterix.add_param('-t','--to',help='parse to number',default=None)
masterix.add_param('-b','--body',help='parse message body',default=None)


if __name__ == "__main__":
	masterix.run()



