sequenceDiagram
    participant Attacker
    participant Outsider
    participant BotNet
    participant Firewall
    participant WebServer
    participant Customer
Outsider ->> Attacker: Accesses phishing link or downloads malicious file
destroy Outsider
Attacker ->> Outsider: Infects local machine<br>and hooks it up to a botnet
Customer ->> Firewall: Access request sent
Firewall ->> Customer: Authenticates access request<br>and routes customer<br>to the main site
Customer ->> WebServer: Begins creating user requests
destroy Attacker
Attacker ->> BotNet: Gives instructions to each bot to target a specific IP address
BotNet ->> Firewall: Sends multiple access requests
Firewall -->> BotNet: Fails to recognize DDoS attack and forwards bots to main site
Firewall ->> BotNet: Notices suspicous IP addresses and sudden increase of traffic and blocks origin request as part of DDoS attack procedures
BotNet -->> WebServer: Floods web server with a ton of user requests
WebServer -->> Customer: Unable to process user requests due to high traffic
#### Description 
The first step in a DDoS attack is for the attacker to send a phishing link or a virus to a random person (Outsider). The malware/virus will then infect the outsider's local machine allowing the attacker to gain control and add the machine to a botnet. The attacker's goal is to generate enough user requests with his botnet to cause or even halt traffic on a site.  
Meanwhile, another person (Customer) is trying to log onto a website/server (WebServer). The customer is submitting an access request to the firewall to get to the main site. The firewall checks to see if the IP address of the person is suspicious or if there is already too much traffic on the site. The firewall then determines that the user isn't a threat and that there is no traffic, and forwards the customer to the main site. The customer then starts creating user requests by moving around on the site.  
After completing the botnet, the attacker has now instructed each bot in the botnet to target a specific IP address. The botnets then send multiple access requests to the firewall of the specified site/server.<br>
**_(There are two possible outcomes as to how the firewall will react to the botnet access requests. The "good" outcome is depicted with a solid arrow. The "bad" outcome is depicted with a dotted line.)_**<br>
If the server recognizes that all these access requests came at the same time from different IP addresses in the same region, it can block the origin request to those specific to that region. The firewall could also identify that the sudden influx of traffic at that time of day isn't normal, and choose to block all the access requests from the bots. These two features of web-based firewall protection are called IP blocking and traffic analysis. <br>
If the server fails to recognize that these requests are a part of a DDoS attack, and forwards the bots to the main site, the bots will begin creating tons of user requests causing major traffic issues on the site. The website/server will then fail to keep up with all the user requests and will be unable to process any more of the customer's requests. This will halt all the legitimate customers as well as the bots.