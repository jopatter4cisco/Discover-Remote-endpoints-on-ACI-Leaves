# Discover-Remote-endpoints-on-ACI-Leaves
This simple script will pull the remotely learned endpoints from an ACI leaf and produce a list suitable for consumption by an IP scanner such as AngryIP.  This can in turn ping a list of remote nodes in the fabric to ensure they survive the upcoming administrative changes to the fabric.

A high level overview of what YOU WILL NEED is this:
 
1. This Python script – grab a list of unique ip address from ‘show endpoint’ command
2. NetMiko - which elegantly handles the ssh session for the leaf.
3. Python Angry IP Scanner - Take the output from that script (data2.txt) and import into Angry IP Scanner
 a. Angry IP scanner does threading – a huge benefit. (Python can also do threading but I haven’t mastered that yet…)
 b. You can export results from Angry IP Scanner to a CSV if you’d like to do further manipulation of the data
 c. At the end of the scanning, it will give results
 
Here is what the python script actually does.  
 I’ve put many items into functions so it’s reusable and notated where I could.
 - It takes a list of leafs you want to investigate and the credentials
 - Makes connection to that leaf and runs ‘show endpoint’ from the CLI
 - Puts the output into a list
 - Searches each line of the list for the word ‘tunnel’ 
 – remote learned IP addresses have ‘tunnel’ as their interface.  
 - Puts those results in a new list
 - Take the new list and search for an IP address on each line.  
 - If that ip address is unique, it adds to a final list of IP addresses
 - Writes the final list of IP addresses to "OutputFile".
 - This file can be taken to Angry IP scanner to test connectivity to IP addresses


Credit to Justin Thompson at Duke Energy for his contribution and collaboration 
