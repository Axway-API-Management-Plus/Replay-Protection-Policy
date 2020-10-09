# Replay-Protection-Policy
Here is a replay attack protection policy that we have in place for our customers that could be used to identify the Replay Attack by use of Ehcache

Replay Attack are always a concern for our clients and Replay Attack are hard to detect in case they can penetrate using a policy/Api published. Here is a replay attack protection policy that we have in place for our customers that could be used to identify the Replay Attack by use of Ehcache (in non-HA environment local cache & in case of HA env use distributed cache). The policy that we have created can be directly imported as a sub Replay protection policy in your development.

### What is Replay Attack?

Definition - A replay attack is a form of network attack in which a valid data transmission is maliciously or fraudulently repeated or delayed. This is carried out either by the originator or by an adversary who intercepts the data and re-transmits it, possibly as part of a masquerade attack by IP packet substitution. This is one of the lower tier versions of a "Man-in-the-middle attack".


Solution - The solution that we are using is to use of ehcache using the cache and throttling filter using message and IP hash key.

![PolicyIMG]( https://github.com/Axway-API-Management-Plus/Replay-Protection-Policy/blob/main/IMG/Capture.PNG ) 

Steps involved on Replay Protection (RP) policy check -

    We first check the IP is not yet "Replay_Protection_IP_Blacklist " (violated the RP before) cache.
    If the message hash is not already in the "Replay_Protection_Messages" then allow the first hit and then store the message as the hash key in the "Replay_Protection_Messages" cache.
    If the message hash is already in the "Replay_Protection_Messages" then use throttling filter to check how many number of times the partner is allowed to make the POST call.
    In case partner violate the throttling filter quota (using cache "Replay_Protection_Invalid_Attempts") then put its IP in the "Replay_Protection_IP_Blacklist " cache or else pass the message in case throttling filter quota is not yet breached.

 

Hence using the 3 different cache we are currently able to stop all Replay attack.

![Axwaylogo]( https://github.com/Axway-API-Management/Common/blob/master/img/AxwayLogoSmall.png ) 
### Axway Team
Altaf Hossain
