Multi-Threaded-Web-Server
=========================

The goal of the project is to provide a basic web server that should be shielded from all of the details of network connections and the HTTP (Hypertext Transfer Protocol) protocol.

Multi-thread Web Server
Date : November-23-2013

**************************

This File Contains :
==========================
  * Compilation of Program
  * Options
  * Test Procedure
  * Protocol
  * Logging 
	  
****************************	  


How to compile the program ?
===========================
type a simple command "make" as below,

$ make
The will create a binary executable as, "myhttpd"

$ ls -al myhttpd

ls -al myhttpd
-rwxrwxr-x 1 user user 38960 Oct 16 19:32 myhttpd

To run this program with default values, use simple, 

$ ./myhttpd

Above command will start a http server and listen on port 8080, with default run directory as,
from where you are starting the myhttpd server, i.e. may be your current working directory.


OPTIONS
===========================
To run this program with custom values as defined from command line, use following parameters:

    ./myhttpd [-d] [-h] [-l file] [-p port] [-r dir] [-t time] [-n threadnum] [-s sched]
where,
    -d : Enter debugging mode. Without this option, the web server should run as a daemon process in the background.
    -h : Print a usage summary with all options and exit.
    -l file : Log all requests to the given file. See LOGGING for details.
    -p port : Listen on the given port. If not provided, myhttpd will listen on port 8080.
    -r dir : Set the root directory for the http server to dir.
    -t time : Set the queuing time to time seconds. The default is 60 seconds.
    -n threadnum : Set number of threads waiting ready in the execution thread pool to threadnum. The default should is 4 execution threads.
    -s sched : Set the scheduling policy. It can be either FCFS or SJF. The default will be FCFS.

	
Test Procedure
===========================
1) open a web browser, and type as, http://localhost:port_num/filename to verify if things are working as expected.
   you can replace "localhost" if you are trying to get data from remote server with the IP of remote server as,
   http://ip_address_server:port_num/filename

2) using test shell scripts, copy testcode folder from this package to the client machine,
   $ cd testcode
   
   To test HEAD request and get response to it, modify reqhead.sh with proper port_num, server & file name and then run the script as
   $ sh reqhead.sh

   To test GET request and get response to it, modify reqget.sh with proper port_num, server & file name and then run the script as
   $ sh reqget.sh

   Verify you are getting expected responses to it.

   
Protocol
===========================

myhttpd supports HTTP/1.0 version: 
it will subsequently respond to GET and HEAD requests according to RFC1945.

the following are the headers which HTTP/1.0 will respond:

    Date : The current timestamps in GMT.
    Server : A string identifying this server and version.
    Last-Modified : The timestamps in GMT of the file’s last modification date.
    Content-Type : text/html
    Content-Length : The size in bytes of the data returned.

	* GET : it will the data of the requested file.
	* HEAD: This will only only return the meta-data but not actual content.

If the request was for a directory and the directory does not contain a file named "index.html", then myhttpd will generate a directory index, listing the 
contents of the directory in alphanumeric order.


Logging 
===========================

The Program will log:

    %a : The remote IP address.
    %t : The time the request was received by the queuing thread (in GMT).
    %t : The time the request was assigned to an execution thread by the scheduler (in GMT).
    %r : The (quoted) first line of the request.
    %s : The status of the request.
    %b : Size of the response in bytes. i.e, "Content-Length".
