#### Wireless security
###### Common security protocols
1. WEP
2. WPA
3. WPA2

WEP - Early security standard version, WEP passwords can be cracked in minutes.

###### WPA
Improvement over WEP:
1. A cryptographic message integrity check to protect packets.
2. An initialization-vector sequencing mechanism that includes hashing, as opposed to WEP's plain text transmission.
3. A per-packet key-mixing function to increase cryptographic strength
4. A re-keying mechanism to provide key generation every 10000 packets

###### WPA V.S WPA2
1. The mandatory use of AES algorithms
2. The introduction of CCMP

###### The primary security vulnerability to the actual WPA2 system
- Requires the attacker to already have access to the secured WI-FI network in order to gain access to certain keys and then perpetuate an attack against other devices on the network.

###### The biggest hole in the WPA armor
Attack vector through the WPS

It allows a remote attacker to recover the WPS PIN in a few hours with a brute-force attack and, with the WPS PIN, the network's WPA/WPA2 pre-shared key.