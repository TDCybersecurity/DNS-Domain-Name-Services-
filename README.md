# DNS-Domain-Name-Services-

# **DNS Domain Names Services| System**
DNS, or Domain Name System, is like the phone book of the Internet.  When you want to visit a website, you type in its name like (www.examplewebsite.com) into the browser.
DNS translates that name into the numerical IP Address like (192.1.2.1) that computers use to find each other on the internet.
This way, you don't have to remember a string of numbers; you just need to know the website's name, and DNS takes care of the rest, guiding your browser to the right place.



















**DNS** is the acronym for **Domain Name Services**, which acts like a directory that translates **human-readable domain names** into **IP addresses**.

**Understanding DNS**

- DNS converts computer names (such as client-1.mydomain.com or [**www.google.com**](http://www.google.com/) ) to IP addresses which can be used by the computer to locate resources.
- DNS is integrated with Active Directory and automatically installed on DC-B in the last lab.
- In this lab we will use **Client-B** and **DC-B** to do a few exercises for the sake of understanding DNS a bit better.
![DNS Google](https://github.com/TDCybersecurity/DNS-Domain-Name-Services-/assets/142702123/fc377657-cddb-445a-9187-9503639e8223)

**Overview (What we are going to do)**

- Inspect **DNS A-Records** on the server (hostname to IP address mappings).
- Create some of our own **A-Records** on the server and observe them from the client.
- Delete records from the server and inspect/clear the **client DNS cache** to gain a better understanding.
- Touch on **"CNAME"** records (mapping one name to another name).
- **Discuss Root Hints**: If we're using our local DNS server to resolve names into IP addresses, how can we still access sites like Google and others on the internet? Does our local DNS server know about these sites?

<h1>1 A-Record Exercise</h1>

1. Connect/log into **DC-B** as your Domain Admin Account (mydomain.com\jane\_admin).
2. Connect/log into **Client-B** as an admin (mydomain\Joe\_Admin).
3. From **Client-B** try to ping "mainframe" and notice that it **FAILS**.
4. **nslookup**"mainframe" notice that it FAILS (no DNS record)
5. Create a DNS A-record on **DC-B** for "mainframe" and have it point to **DC-B**'s Private IP address.
![DNSa 2 Log into](https://github.com/TDCybersecurity/DNS-Domain-Name-Services-/assets/142702123/0651208e-989a-4327-be33-356c06107284)
![](RackMultipart20240523-1-1v9tlt_html_7cb153d3e035cca.png)

![](RackMultipart20240523-1-1v9tlt_html_3a1db3865af05a21.png)

a.Log into both **Client-B** and DC-B using mydomain.com\Joe\_Admin |Password1

b.Go back to **Client-B** and try to ping it. Observe that it works.

c. Go to **Client-B** virtual desktop\>Command Line\> ping **mainframe**\>

Error message: Ping request could not find host mainframe. Please check the name and try again.

d. Create an A-Record for **mainframe.** Go to **DB-B Server Manager****.** Go to Tools\>DNS\>click DC-B and expand the folder.![DNS A record C error](https://github.com/TDCybersecurity/DNS-Domain-Name-Services-/assets/142702123/4ebbb864-03a4-4b64-81e6-529013a2e96a)![DNS1 d Create 1](https://github.com/TDCybersecurity/DNS-Domain-Name-Services-/assets/142702123/26b05a70-c8fe-4bb5-b039-94e9599ebbcb)[DNS 1d Create 2](https://github.com/TDCybersecurity/DNS-Domain-Name-Services-/assets/142702123/b54f5454-2a20-4cad-a62d-99b9fd3ca836)![DNS 1e2](https://github.com/TDCybersecurity/DNS-Domain-Name-Services-/assets/142702123/2f0ae85a-52ea-45ae-af1c-b44cd76d9962)

e. Open and Expand Forward Lookup Zones\> click on mydomain.com. These are the A-Records that we have.![DNS 1e1](https://github.com/TDCybersecurity/DNS-Domain-Name-Services-/assets/142702123/9347bae3-be71-4490-a03f-467d4eebc649)![DNS e Open and Expand](https://github.com/TDCybersecurity/DNS-Domain-Name-Services-/assets/142702123/8f3f9fae-bbd1-4036-8054-310013698afa)

f. Manually create **mainframe** as a New Host (A or AAA Record)\>Entry\>Created\>Add Host. ![DNS f manually](https://github.com/TDCybersecurity/DNS-Domain-Name-Services-/assets/142702123/0cf2a75d-b4d6-48c5-a0b5-2d0adfb59485)

g. **ping mainframe** for **Client-B**, the ping was successful. Enter **nslookup** for mainframe to return IP 10.1.0.4.![DNS g ping nslookup](https://github.com/TDCybersecurity/DNS-Domain-Name-Services-/assets/142702123/949a695f-3d65-4a6b-bd4b-82c0c8e5ef32)

h. Mainframe will now be in the local cache.

i.Go back to **DC-B**\>DNS\>mainframe\>change DNS to 8.8.8.8\>OK\>Apply\>OK

j. Go back to **Client-B** and ping **8.8.8.8** or **mainframe**. It works for both.![DNS 1j](https://github.com/TDCybersecurity/DNS-Domain-Name-Services-/assets/142702123/b785cb1e-86bb-49d6-9f2c-d1007b3c43f1)

k. **Client-B** go to Command Prompt\>Run as Administrator\>ipconfig /flushdnsip

m.dnsflush

<h1>2 Local DNS Cache Exercise</h1>

1. Go back to **DC-B** and change the **mainframe's** record address to **8.8.8.8**.![DNS j ping 8888 and mainframe](https://github.com/TDCybersecurity/DNS-Domain-Name-Services-/assets/142702123/fa4b375c-b873-41a4-9e83-e104150b61f9)
2. Go back to **Client-B** and ping " **mainframe**" again. Observe that it still pings the old address.![DNS Local a](https://github.com/TDCybersecurity/DNS-Domain-Name-Services-/assets/142702123/9540efac-be06-46d6-abb9-2b8a9e34978a)
3. Observe the local DNS cache (ipconfig/ **displaydns**).
   
![DNS Local displaydns](https://github.com/TDCybersecurity/DNS-Domain-Name-Services-/assets/142702123/78015247-62ab-4dd1-8a03-dac8bf61885b)

4. Flush the DNS cache (ipconfig/ **flushdns**). Observe that the cache is empty.
![DNS Local d flushdns](https://github.com/TDCybersecurity/DNS-Domain-Name-Services-/assets/142702123/bc89ea92-ffaf-4453-87be-018cda880389)

5. Attempt to ping " **mainframe**" again. Observe the address of the new record showing up.

<h1>3 CNAME Record Exercise</h1>

Go back to ~~**DC-B**~~ and create a **CNAME** record that points the host " **search**" to [www.google.com](http://www.google.com/).

Go back to **Client-B** and attempt to ping " **search**", observe the results of the CNAME record.

On **Client-B**, nslookup " **search**", observe the results of the CNAME record.

97Go to **Client-B** and **ping search**. No hits.
![DNS 97 ping search fails](https://github.com/TDCybersecurity/DNS-Domain-Name-Services-/assets/142702123/f54aca17-aa39-4156-9efe-7fce7ee5510d)

98Go to **DC-B**\>mydomain.com\>New Alias (CNAME)\>add search to Alias (CNAME) and [www.google.com](http://www.google.com/) as FQDN
![DNS 98 CNAME](https://github.com/TDCybersecurity/DNS-Domain-Name-Services-/assets/142702123/a50bfd47-ede0-4d42-b39e-4f2cf1f0e232)

Go to **Client-B** and **ping search**.
![DNS 99 ping search](https://github.com/TDCybersecurity/DNS-Domain-Name-Services-/assets/142702123/2dcf4819-afc2-4a2e-9b50-e6fd278230a3)

Go to **DC-B**\> **Root Hints**
![DNS 100 Root Hint](https://github.com/TDCybersecurity/DNS-Domain-Name-Services-/assets/142702123/65e4ed55-39a3-4295-aa33-b27dc05ce107)

<h2>Thank you for reviewing my Github IT Project, which highlights my hands-on experience with DNS.</h2>
