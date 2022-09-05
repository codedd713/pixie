# pixie

Pixie is a DHCP client simulator program

    Author : Codey
    Email  : codedd713@gmail.com

What can pixie do:

- Simulate DHCP client behaviour for DISCOVER, RELEASE and RENEW operations
- Simulate DHCP Relay Agent behaviour
- Target multiple DHCP server
- Send bulk requests in sequence, with multiple MAC addresses
- Use Option 82 common suboptions 1,2,5
- Pixie will generate a random MAC address if not provided

<h2>Examples:</h2>

`$ pixie -e`

<h5>Demo:</h5>

       Def ->             Server              Gateway/Relay        Hostname              FQDN                 MAC address           Vendor Class ID      Parameter Request List
     ----------- ------------------------ --------------------- --------------- ----------------------- ------------------------ --------------------- ---------------------------
      pixie.exe   -server 10.192.116.111   -giaddr 10.192.6.1    -hostname abc   -fqdn pc.domain.local   -mac 66:55:44:33:22:11   -vid "Aruba Client"   -opt55 3,1,6,56,43,89,115

<h5>Use DHCP client identifier:</h5>

       Def ->            Server           DHCP Client Identifier
     ----------- ---------------------- ---------------------------
      pixie.exe   -server 10.192.9.111   -cid 01:00:01:02:a0:bc:03

<h5>Send Discover to multiple servers:</h5>

       Def ->       Servers seperated by comma ( , )
     ----------- ------------------------------------
      pixie.exe   -server 10.192.9.111,172.16.5.9


<h5>Send Discover but DO NOT LEASE:</h5>

       Def ->     Do not request          Servers              Gateway/Relay
     ----------- ---------------- ------------------------ ---------------------
      pixie.exe   -noreq           -server 10.192.116.111   -giaddr 10.192.6.1


<h5>Define Custom options:</h5>

       Def ->            Server             Gateway/Relay              Custom Options (Eg: 18 and 4)
     ----------- ----------------------- -------------------- -----------------------------------------------
      pixie.exe   -server 10.192.11.111   -giaddr 10.192.6.1   -customopt 18=a.b.c,abc 4=5.6.7.8,11.11.11.76


<h5>Renew:</h5>

       Def ->            Server                  Renew
     ----------- ----------------------- ----------------------
      pixie.exe   -server 10.192.11.111   -renew 192.168.5.127

<h5>Release:</h5>

       Def ->            Server                  Release
     ----------- ----------------------- ------------------------
      pixie.exe   -server 10.192.11.111   -release 192.168.5.127

<h5>Option 82 usage:</h5>

       Def ->            Server               Sub-option 1              Sub-option 2              Sub-option 5      Sub-option 151
     ----------- ----------------------- ---------------------- ----------------------------- -------------------- -----------------
      pixie.exe   -server 10.192.11.111   -circuitid junkvalue   -remoteid bb:22:cc:00:dd:ee   -linkid 10.0.0.128    -vss=2,abcd123

<h5>Repeat/Loop DHCP packets:</h5>

       Def ->            Server           Counts to repeat   Sleep between each packet sent(Optional)
     ----------- ----------------------- ------------------ ------------------------------------------
      pixie.exe   -server 10.192.11.111   -repeat 3          -sleep 3


<h2>Infoblox specific options [BETA]</h2>

<h5>Create network and/or range:</h5>

       Def ->            Server           Signal to create    Specify network           Sepcify range                  Specify credentials
     ----------- ----------------------- ------------------  ----------------------   ---------------------------     -----------------------------
      pixie.exe   -server 10.192.11.111   -create             -network 10.0.0.0/24     -range 10.0.0.1-10.0.0.150      -crednetials admin:infoblox


<h3>Logging</h3>

Pixie can display syslogs by setting up your device as a syslog endpoint.

<h5>Configure syslog endpoint on Infoblox pointing to self:</h5>

           Def ->            Server            Specify syslog receiver (own IP)    Specify credentials             Signal to create syslog EndPoint
         ----------- -----------------------  ---------------------------------   -----------------------------   ----------------------------------
          pixie.exe   -server 10.192.11.111   -receiver 10.0.0.55                 -credentials admin:infoblox     -syslogep

<h5>Get syslogs for current call:</h5>

           Def ->            Server             Gateway/Relay      Start logging
         ----------- ----------------------- -------------------- ---------------
          pixie.exe   -server 10.192.11.111   -giaddr 10.192.6.1   -log

Restore syslog endpoint on Infoblox pointing to self:

           Def ->            Server            Restore syslog ep settings   Specify credentials             Signal to create syslog EndPoint
         ----------- -----------------------  ---------------------------  -----------------------------   ----------------------------------
          pixie.exe   -server 10.192.11.111   -restore                     -credentials admin:infoblox     -syslogep
