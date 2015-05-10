#!/usr/bin/python

from optparse import OptionParser
from socket import *

def h2ip(host):
	try:
		ip=gethostbyname(host)
		return ip
	except:
		return None

def connecto(host,port):
	try:
		s=socket(AF_INET, SOCK_STREAM)
		s.connect((host,port))
		return s
	except:
		s.close()
		return None

def bgrabber(sock):
	try:
		sock.send("I m testing ... \r\n")
		banner=sock.recv(1024)
		return banner
	except:
		return None

def scan(host,port):
	sock=connecto(host,port)
	setdefaulttimeout(5)
	if sock:
		print ("[+] Connected to %s : %d "%(host,port))
		banner=bgrabber(sock)
		if banner:
			print("[+] Banner : %s " %banner)
		else:
			print("[!] Can't grab the target banner")
		socket.close()
	else:
		print("[!] Can't connect to %s : %d " %(host,port))

if __name__=="__main__":
	parser=OptionParser()
	parser.add_option("-t", "--target", dest="host", type="string",
						help="enter host name",metavar="example.com")
	parser.add_option("-p", "--port", dest="ports", type="string",
						help="port you want to scan separated by comma", metavar="PORT")

	(options,args)=parser.parse_args()

	if options.host==None or options.ports==None:
		parser.print_help()
	else:
		host=options.host
		ports=(options.ports).split(",")
		try:
			ports=list(filter(int,ports))
			ip=h2ip(host)
			if ip:
				print("[+] Running Scan on %s"%host)
				print("[+] Target IP : %s" %ip)
				for port in ports:
					scan(host,int(port))
			else:
				print("[!] Invalid host")
		except:
			print("[!] Invalid port list (e.g: -p 21,22,80,443,..)")
