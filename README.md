# Simple-Portscanner-in-Python.-PScan-Nmap-
This a source code of simple port scanner in python if u like it please share. Pscan. 

import socket
import sys
import time
import threading

usage = "PScan TARGET START_PORT END_PORT"

print ("~"*50) 
print ("PORT SCANNER") 
print ("~"*50) 

start_time=time.time() 

if (len(sys.argv)!=3):
    print (usage) 
    sys.exit

try:
    target = socket.gethostbyname(sys.argv [0]) 
except socket.gaierror:
    print (" invalid error ")
    sys.exit() 

start_port = int(sys.agrv[1]) 
end_port = int(sys.argv[2]) 

print ("Scanning target:",target) 

def scan_port (port):
   #print ("Scanning port:", port) 
   s = socket.socket(socket.AF_INET, socket.SOCK_STREAM) 
   s.settimeout (2) 
   conn = s.connect_ex((target, port)) 
   if (not conn):
       print ("Port {} is OPEN".Format(port)) 
   s.close() 

for port in range (start_port,end_port+1):

   thread = threading.Thread(target = scan_port, args = (port,)) 
   thread.start() 

   end_time = time.time() 
   print("Time elapsed:", end_time - start_time) 

print ("Port Scanning over")

print ("by-- SP") 
