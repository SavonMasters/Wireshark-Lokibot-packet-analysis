# Wireshark-Lokibot-packet-analysis


Title: Wireshark LokiBot packet analysis 

Analyst: Savon Masters 

Date: February 28th, 2026


                                                        Summary
                                                        
LokiBot uses a credential and information stealing malware, often sent as a malicious attachment, email, website, text or file. LokiBot also known as Lokibot, Loki PWS, and Loki-bot extends Trojan malware to steal sensitive information of the following usernames, passwords, cryptocurrency wallets, and other credentials. Inside of the investigation I searched a packet of the malware to learn the IOCs, actions and patterns, and its effects when used successfully. 


                                                        Investigation 


![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/68f29c4d1dc95425ac88dae9154b27ffe900ee5d/Screenshot%20from%202026-03-02%2015-34-30.png)
First, I like to see what all the packet contains by looking at the capture file properties. This one started at “2021-09-14”at “10:32:16”, elapsed for “09:44” minutes and consisted of 3679 packets. 


![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/ce679bd8686bd2f7ac30946510989f8758c17e30/Screenshot%20from%202026-03-02%2015-46-21.png)
Second, I clicked on the protocol hierarchy statistics to see the most frequent protocol. You can see there is not a lot of UDP traffic but a big amount of TCP with HTTP and ARP traffic being high. 


![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/8983a549f2b749856763c23ddb3758b6fc816569/Screenshot%20from%202026-03-02%2015-56-06.png)
Thirdly, I see if I can see the source IP address of the client and who he was communicating with the most with the conversations feature. The source IP address of the client might be “10[.]0[.]0[.]168” and interesting IP addresses to look into would be “103[.]232[.]55[.]148 and 204[.]79[.]197[.]200” due to their high packets. 


![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/66bc232ce97c499c95b070111086cee12cacaf04/Screenshot%20from%202026-03-02%2016-24-12.png)
![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/66e98437c8f452cbd5783695950c21b4245d7de1/Screenshot%20from%202026-03-02%2016-26-27.png)
Fourthly, I chose to look at the HTTP traffic first since it had the most traffic and its unsecure for possible attacks to take place. The client made a GET request to the website “hxxp[://]103[.]232[.]55[.]148/service” and got the response of line-text based data sending “/icons/blank/gif” and “/icons/back/gif” from the server “Apache/2.4.47 (Win64) OpenSSL/1.1.1k PHP/7.3.28\r\n”.


![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/d18b3678f6da5c55ab42e2d55886ce5d6c92dc74/Wireshark%20Lokibot%201.png)
![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/202b106c21550d97033969dd1b9ea3308bbae3bb/Wireshark%20Lokibot%202.png)
Fifthly, I researched the IP address that was included in the query and learned that it has been flagged 7/90 times for being malicious. I looked up the server as well and learned that it is using unsecured versions that all have separate vulnerabilities making the server easy to base attacks. 


![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/48042d22ed62b50266bca2329f98c244011f1205/Screenshot%20from%202026-03-02%2017-32-25.png)
![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/847bd7e71c058148a3d30519bda67af874544cd1/Screenshot%20from%202026-03-02%2017-33-26.png)
Sixly, two items were requested from the domain “/icons/blank.gifs” and “/icons/back.gifs”. I believe the attacker is using the gifs to mask malware that can be downloaded. 


![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/fc82273ecce9fa1d875562ef2f7ecfeb4a5aa365/Screenshot%20from%202026-03-02%2018-18-00.png)
![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/2b631fa25d714902c9cec6c84b6ef14e767cbed8/Wireshark%20Lokibot%203.png)
SeventhIy, I went through to the next HTTP request and saw that it was for a “favicon[.]ico” from the attacker’s domain. I looked up what a “favicon[.]ico” is and gathered that it can be used to impersonate a known recognizable website image which would allow an attacker to download malware behind an image. 


![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/cab6e1244a54ad7eace887d41fde7b24f214c66e/Wireshark%20Lokibot%204.png)
![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/36ba606699cfa1ebd708dd299713c1d3b476219b/Screenshot%20from%202026-03-02%2018-33-36.png)
Eightly, I continued on to a new HTTP request and saw it was for “hxxp[://]ctldl[.]windowsupdate[.]com/msdownload/update/v3/static/trustedr/en/disallowedcertstl[.]cab?3027e92ff72bd024]”, this is a legitimate service that allows the Microsoft system to allow untrusted digital certificates to the system. The vulnerability is an attacker can use this service to allow an untrustworthy digital certificate that they own and avoid detection by Microsoft's defenses. 


![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/6498a1c6a6533cec3a20402afadf12af1523aef9/Wireshark%20Lokibot%205.png)
![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/b3929b0487eb2ff7481c215f609a91ec3d4e1307/Screenshot%20from%202026-03-02%2019-11-47.png)
![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/c8eeb3d63044b8e21cf7adf1332012170038eeb6/Wireshark%20Lokibot%206.png)
Ninthly, in relation to the last HTTP request the client made a request for an online certificate status protocol “hxxp[://]ocsp[.]digicert[.]com/MFEwTzBNMEswSTAJBgUrDgMCGgUABBSAUQYBMq2awn1Rh6Doh%2FsBYgFV7gQUA95QNVbRTLtm8KPiGxvDl7I90VUCEAJ0LqoXyo4hxxe7H%2Fz9DKA%3D”. Viewing information online about this digital certificate you can see it has been flagged for being malicious with the possibility of it being a ransomware attack which would give evidence for the prior indicators. The client made this request for a new IP address “93[.]184[.]220[.]29”, the information about this one IP address is not malicious but the site can be wrongfully used to host malware.


![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/fc388ebdd9345d0bfb55ca946e90cd93c06ff71f/Screenshot%20from%202026-03-03%2017-34-25.png)
![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/574c8bbca194ad78a38ec8ba8a962bf3b8be42ea/Wireshark%20Lokibot%207.png)
![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/25623af1786edd06758ab1de9804270392228c68/Screenshot%20from%202026-03-03%2017-36-51.png)
Tenthly, another GET request was made this time it was towards the website “ hxxp[://]microsoft[.]com/pkiops/certs/MicSecSercA2011_2011-10-18[.]crt”. I looked at information about this website on Any Run and learned it was malicious with behaviors including messing with certificates settings on a system. If you look at the packet bytes you can see there's also another HTTP website with the words “Root Certificate” it’s an likely indicator of changes to the certificates settings. 


![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/cae0730bd94c50418369241820719cdc912f9309/Screenshot%20from%202026-03-03%2017-57-33.png)
![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/1e66bcf12475a611338eb2fb024103756d93f456/Wireshark%20Lokibot%208.png)
![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/441406eb1185fefed02901404837eb304fb80e80/Screenshot%20from%202026-03-03%2018-07-59.png)
Eleventhly, moving on a GET request was made to the attacker’s domain adding on “dasboard/stylesheets/normalize.css”. “Dashboard/stylesheets/normalize.css” is used to alter the appearance of a website. The next few GET requests all ask for this domain’s available appearance features to change different parts of the website. I have a strong suspicion that the attacker is starting to build a popular well known looking website for an impersonation attack to make unnoticeable malware linked. 


![image alt](https://github.com/SavonMasters/Wireshark-Lokibot-packet-analysis/blob/d69a60490bdd792be8ca17c2fab4eac3d0bc6c53/Screenshot%20from%202026-03-03%2018-40-09.png)
Twlevely, by using the “hxxp[://]connect[.]facebook[.]net/en_US/all[.]js” the attacker was able to get the rights to a FaceBook software license giving fact the attacker is initiating an impersonation attack with a fake FaceBook website. 



Thirteenthly, from this point the attacker is trying to pull the actual malware file from his domain, “http%3A%2F%2F103.232.55.148%2Fservice%2F[.]au&maxwidth=32765&rowheight=20&sectionHeight=160&FORM=IESS02&market=en-US HTTP/1.1\r\n”. To hide the true location of the malware file on his domain the attacker is using percent encoding “%3A,%2F, %2F” and url spoofing. Using a few GET request to the url the attacker is pulling parts of the malware each time he requests, you can see below query in the XML section an “.” for the first GET request response and “.audiodg.exe” for the last GET request response.

 

Fourteenlthy, keeping going the attacker has fully downloaded the malware onto the system. The malware is called “.audiodg.exe” and has been categorized as Trojan, Rat and Stealer. The malware will be unseeable until it uses the command line to leave an executable on the device that interacts with it, which at that point it will start to steal the devices data, information and credentials. 



Fifthteenly, the attacker then makes a POST request for “hxxp[://]136[.]243[.]159[.]53/~element/page[.]php?id=484” for the last part of his attack. The POST request is making it look as an error message after a person clicked on the link on the malicious page. The message features data like “404 Not Found”, “The requested URL was not found on this server”, and “error was encountered while trying to use an ErrorDocument to handle the request”. Tying together the built fake Facebook page and the last message to mimic a real error message the attacker can now download the malware without any trouble. 


                                                        Conclusion 

After conducting the investigation of the LokiBot malware I learned it operated on the HTTP protocol, it queried for a untrusted domain for malicious content, it used the malicious content in the presentation of a Facebook page to host the malware, exporting the malware from the domain to leave on the Facebook as an attack vector to have the ability to gain login credentials, host information, and different metadata. I have a more thorough understanding of the malware techniques and the advancing threats and dangers to cybersecurity safety. 


                                                          IOCs

An extra amount of HTTP traffic which is a unsecure protocol. 
The attackers IP address “103[.]232[.]55[.]148”.
The attacker's domain “hxxp[://]103[.]232[.]55[.]148/service”.
Malicious items from the domain to create an impersonation attack such as “/icons/blank.gifs”, “/icons/back.gifs”. “Favicon[.]ico”, “dasboard/stylesheets/normalize.css”, and “hxxp[://]connect[.]facebook[.]net/en_US/all[.]js” 
Accessing “hxxp[://]ctldl[.]windowsupdate[.]com/msdownload/update/v3/static/trustedr/en/disallowedcertstl[.]cab?3027e92ff72bd024]” to change certificate status with “hxxp[://]ocsp[.]digicert[.]com/MFEwTzBNMEswSTAJBgUrDgMCGgUABBSAUQYBMq2awn1Rh6Doh%2FsBYgFV7gQUA95QNVbRTLtm8KPiGxvDl7I90VUCEAJ0LqoXyo4hxxe7H%2Fz9DKA%3D”, and “hxxp[://]microsoft[.]com/pkiops/certs/MicSecSercA2011_2011-10-18[.]crt”
The obfuscated location of the malware on the attacker’s domian “http%3A%2F%2F103.232.55.148%2Fservice%2F[.]au&maxwidth=32765&rowheight=20&sectionHeight=160&FORM=IESS02&market=en-US HTTP/1.1\r\n”.\”.
The malware called “.audiodg.exe” and its SHA256 hash 7714997ED1B2E2C56ED953288242AE8BEC057E1561E8191E12E9EBA13DC1D74D
A put together error message page from “hxxp[://]136[.]243[.]159[.]53/~element/page[.]php?id=484” to behave the same as a FaceBook page.
The malware displayed the MITRE techniques of “Obfuscated Files or Information [T1027], Application Layer Protocol: Web Protocols [T1071.001], Credentials from Password Stores: Credentials from Web Browsers [T1555.003]”, and User Execution: Malicious File [T1204.002].


                                                        Recommendations

Block the attacker’s IP address “103[.]232[.]55[.]148” and domain “hxxp[://]103[.]232[.]55[.]148/service”
Install a firewall or proxy to block websites that were made by an untrustworthy service. 
Create alerts for changes to certificates that are allowed or blocked from your server. 
If not possible to block HTTP traffic, monitor regularly due to the unprotectedness of the protocol. 
Review links that you click on are the right links to the webpage. 
Add the malware to the Anti Virus signature software to be on top of the attack.
Block the link to the malware “http%3A%2F%2F103.232.55.148%2Fservice%2F[.]au&maxwidth=32765&rowheight=20&sectionHeight=160&FORM=IESS02&market=en-US HTTP/1.1\r\n”.\” and delete the malware “.audiodg.exe” and run checks on the computer afterwards to reassure no artifacts were left from the attack. 


                                                        Things I learned  

The LokiBot malware actions during an attack. 
An improved understanding of MITRE attack techniques that are always used. 
A new strategy to investigate IOCs of packets. 
A group of helpful links to perform Open source intelligence (OSINT) on threats of malicious files, links, and executables. 
How WireShark guides an investigation details. 

