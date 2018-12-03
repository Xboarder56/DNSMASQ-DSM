# DNSMASQ-DSM (Pi-Hole)
DNSMASQ DSM for QRadar

This DSM/Rsyslog config will support sending the following dnsmasq event types "query", "config", "reply", "cached", "forwarded", and "/etc/pihole/gravity.list". If you have any questions you can create an Issue for the github project or open a question/reply on the IBM QRadar CE forms located at: https://ibm.biz/qradarceforums

# Pi-Hole Changes
1. Run the command "sed -i 's/log-facility=\/var\/log\/pihole.log/log-facility=DAEMON/g' /etc/dnsmasq.d/01-pihole.conf"
2. Copy the file "10-dnsmasq-pihole.conf" to the location "/etc/rsyslog.d"
3. Edit the line "@QRadar or @@QRadar" with the IP address of your QRCE instance. Depending on if you will utilize UDP (@) or TCP (@@). 
4. Create the logging file by running the command "touch /var/log/pihole/dnsmasq.pihole.query.log"
5. Set the permissions to write to the log file "chmod 666 /var/log/pihole/dnsmasq.pihole.query.log"
6. Restart the services dnsmasq and rsyslog "systemctl restart pihole-FTL && systemctl restart rsyslog"

# QRCE Changes
1. Create a new custom DSM called (dnsmasq or Pi-Hole) using the DSM editor option under the admin settings window.
2. Once the custom DSM has been created close the window and click the Log Source Extensions option in the admin settings.
3. Click Add near the top right corner
4. Enter a name of "DnsmasqCustom_ext"
5. Select your newly created log source (dnsmasq or Pi-Hole) that you created earlier.
6. Click the upload button and select the file "DnsmasqCustom_ext.xml"
7. Click done and procced to open the DSM menu and select your log source (dnsmasq or Pi-Hole) that you created earlier.
8. You will need to select Event Mappings tab in the DSM editor and create the manual entries located in the file "Event Mappings.txt"
9. Finally, you will need to create a new log source selecting the custom Log source type we just created. 

# References/Sources
- https://discourse.pi-hole.net/t/request-option-to-send-logs-to-a-remote-logserver/1381/8 (User: Fedora-Core)