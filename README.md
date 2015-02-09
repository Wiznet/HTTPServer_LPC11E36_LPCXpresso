# HTTP Server Example for W5500-EVB
Common to Any MCU, Easy to Add-on. Internet Offload co-Processor, HW TCP/IP chip, 
best fits for low-end Non-OS devices connecting to Ethernet for the Internet of Things. These will be updated continuously.

<!-- W5500 EVB pic -->
<p align="center">
  <img width="50%" src="http://wizwiki.net/wiki/lib/exe/fetch.php?media=products:w5500:w5500_evb:w5500-evb_side.png" />
</p>

## How to Use
The HTTP server library is roughly composed of the following functions.
- httpServer_init(): Handler the HTTP server initialization (user's buffer, H/W sockets for HTTP)
- reg_httpServer_webContent(): Function for example web page registration 
  - webpages, javascript function pages, images and etc.
- httpServer_run(): HTTP server process handler in main routine.

** web page examples are located in 'webpages.h' file.

W5500-EVB uses AJAX method and pre-defined CGI function to configure the network or monitor and control the I/O.
<p align="center">
  <img width="70%" src="http://wizwiki.net/wiki/lib/exe/fetch.php?media=products:w5500:w5500_evb:w5500-evb_cgi.png" />
</p>
CGI for W5500-EVB consists the 'Request name + .cgi' using HTTP GET/POST request method. The CGI for each HTTP methods are handled as below.

<p align="center">
  <img width="90%" src="http://wizwiki.net/wiki/lib/exe/fetch.php?media=products:w5500:w5500_evb:w5500-evb_cgi_processes.png" />
</p>

### GET
- The method for getting the values from web server
- Passed in the form of a JavaScript callback function parameters
  - Same structures as JSON
  - The function name in the HTTP response body must be the same on the Web page's JavaScript Callback function name
  - e.g., If the 'function IoStatusCallback' is Javascript function name in the Web page, web server must pass the data as next; DioCallback({"dio_p" : "0"}, {"dio_s" : "0"}, {"dio_d" : "2"})

### POST
- The method for putting the changed values to web server
- Values are passing by the Web form element
- Key-value pairs; Each pair is separated by '&' and the Key/value of a pair is represented by '='
  - e.g., 'Pin : 1, Val : 1' ⇒ 'Pin=1&Val=1'

### Pre-defined GET/POST CGI Name Example
- GET (Get)
  - get_netinfo.cgi (Network information, Return MAC/IP/GW/SN/DNS/DHCPen)
  - get_dio0.cgi ~ get_dio15.cgi (Digital I/O D0 ~ D15, Return Pin/Status/Direction)
  - get_ain0.cgi ~ get_ain6.cgi (Analog Input A0 ~ A5 and A6 for on-board temp.sensor+Potentiometer)

- POST (Set)
  - set_diostate.cgi (Setting the Digital I/O status, Post requset have to includes 'pin=x&val=y', 0(low) or 1(high))
  - set_diodir.cgi (Setting the Digital I/O direction, Post requset have to includes 'pin=x&val=y' 0(notused) or 1(input) or 2(output))


## Related Project GitHub Repositories
- [W5500-EVB Main](https://github.com/Wiznet/W5500_EVB)
- [Loopback Test](https://github.com/Wiznet/Loopback_LPC11E36_LPCXpresso): Loopback test example project (TCP server / TCP client / UDP)
- [FTP Server](https://github.com/Wiznet/FTP_LPC11E36_LPCXpresso): FTP server example project
- [SNMPv1 Agent](https://github.com/Wiznet/SNMP_LPC11E36_LPCXpresso): SNMPv1 agent example project (Get/Set/Trap)


## How to add a submodule of ioLibrary in project
- $ git submodule add git@github.com:Wiznet/ioLibrary_Driver.git project_src/ioLibrary
- $ git commit -m "description"
- $ git push

## How to clone a submodule of ioLibrary
- $ git clone git@github.com:Wiznet/HTTPServer_LPC11E36_LPCXpresso.git
- $ git submodule init
- $ git submodule update

## Revision History
Last release : Feb. 2015
