# Wireshark Projects
Documenting different Wireshark uses on both Kali Linux and Mac

https://www.wireshark.org/docs/wsug_html/ 

Statistics > Capture File Properties (overall statistics)
Statistics > Conversations (see the different conversations between Addresses)
    you can right click an IP address to Apply as Filter > Selected > A -> B 
    and it'll automatically set up the filter search

Basic task - Knowing the IP addresses and double checking unknown IP addresses
Mac IP address 192.168.XXX.XXX

Generally Wireshark is something you want to have a goal in mind, a specific issue to troubleshoot
Using Wireshark to double check what's up with a Device not connecting
    or Phishing investigations
    or to tell which devices are constantly communicating and see what can be cut down to increase bandwidth

Insecure/HTTP website traffic
    Search http on the filter cause that's not secure

Right-Click Packet > Follow > HTTP or TCP stream
    gives you the results of all the relevant messages in one message
    if it were in HTTPS, the text would be encrypted and not so readable
    and it would just straight up give you the webpage's HTML in some cases
    That's one way how phishing scams would collect your username and passwords

tcp.port==80 > searches all Packets on port 80
    port 80 data is encrypted so you can't read it without the encryption key

The Plus button next to the filter
    You can create a dedicated button to automatically get to the commonly used filters

View > Coloring Rulres > it explains how each type of packet relates to what color
    TLDR Red and Black is usually a sign to pay attention that something is suspicious

Wireshark > Preference > Appearance > Layout (lets you change teh window layouts, and also  gives you the option to see the Packet Diagram for the structure of the Packet, byte-wise)

Wireshark > Preference > Appearance > Columns ( You can add a new column, and Set up Delta/Delta Time type)

Extra Filter 
    Hide Common Protocols - !(arp or stp or lldp or cdp)
    3-way-handshake SYN flags specifically part 1 - tcp.flags.syn==1
    Show Flagged Packets - tcp.analysis.flags    (usually what you use for finding problems)
    Show Connection Releases - tcp.flags.reset==1 (bunch of red flags)

Malware-traffuc-analysis.net is a website for wireshark practice.

# Freeform Packet Analysis
Dell_5f:ea:0a	Broadcast	ARP	60	Who has 192.168.1.179? Tell 192.168.1.196
    This ARP protocol concerned me because instead of IP addresses it used names and was asking about IP addresses, but turns out this is benign, DNS lookup stuff.

TCP	78	[TCP Dup ACK 957#1] 443 → 54668 [ACK] 
    So turns out that TCP Dup ACK refers to Fast retransmissions stuff and filling in the gaps between packages when some stuff gets lost in transit. I guess it's not just UDP that stuff can get lost in.