# DNS-Domain-Name-Services-
A brief walk through of DNS Domain Name Services
# **CC Lab 6 DNS Domain Names Services**

**DNS** is the acronym for **Domain Name System**, which acts like a directory that translates **human-readable domain names** into **IP addresses**.

**Understanding DNS**

- DNS converts computer names (such as client-1.mydomain.com or [**www.google.com**](http://www.google.com/) ) to IP addresses which can be used by the computer to locate resources.
- DNS is integrated with Active Directory and automatically installed on DC-B in the last lab.
- In this lab we will use **Client-B** and **DC-B** to do a few exercises for the sake of understanding DNS a bit better.


# **www.google.com**
(http://www.google.com/)

#

# ****

# **206.58.199.228**

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

![](RackMultipart20240523-1-1v9tlt_html_7cb153d3e035cca.png)

![](RackMultipart20240523-1-1v9tlt_html_3a1db3865af05a21.png)

a.Log into both **Client-B** and DC-B using mydomain.com\Joe\_Admin |Password1

b.Go back to **Client-B** and try to ping it. Observe that it works.

c. Go to **Client-B** virtual desktop\>Command Line\> ping **mainframe**\>

Error message: Ping request could not find host mainframe. Please check the name and try again.

d. Create an A-Record for **mainframe.** Go to **DB-B Server Manager****.** Go to Tools\>DNS\>click DC-B and expand the folder.

e. Open and Expand Forward Lookup Zones\> click on mydomain.com. These are the A-Records that we have.

f. Manually create **mainframe** as a New Host (A or AAA Record)\>Entry\>Created\>Add Host

g. **ping mainframe** for **Client-B**, the ping was successful. Enter **nslookup** for mainframe to return IP 10.1.0.4.

h. Mainframe will now be in the local cache.

i.Go back to **DC-B**\>DNS\>mainframe\>change DNS to 8.8.8.8\>OK\>Apply\>OK

j. Go back to **Client-B** and ping **8.8.8.8** or **mainframe**. It works for both.

k. **Client-B** go to Command Prompt\>Run as Administrator\>ipconfig /flushdnsip

m.dnsflush

<h1>2 Local DNS Cache Exercise</h1>

1. Go back to **DC-B** and change the **mainframe's** record address to **8.8.8.8**.
2. Go back to **Client-B** and ping " **mainframe**" again. Observe that it still pings the old address.
3. Observe the local DNS cache (ipconfig/ **displaydns**).
4. Flush the DNS cache (ipconfig/ **flushdns**). Observe that the cache is empty.
5. Attempt to ping " **mainframe**" again. Observe the address of the new record showing up.

<h1>3 CNAME Record Exercise</h1>

Go back to ~~**DC-B**~~ and create a **CNAME** record that points the host " **search**" to [www.google.com](http://www.google.com/).

Go back to **Client-B** and attempt to ping " **search**", observe the results of the CNAME record.

On **Client-B**, nslookup " **search**", observe the results of the CNAME record.

97Go to **Client-B** and **ping search**. No hits.

98Go to **DC-B**\>mydomain.com\>New Alias (CNAME)\>add search to Alias (CNAME) and [www.google.com](http://www.google.com/) as FQDN

99Go to **Client-B** and **ping search**.

100Go to **DC-B**\> **Root Hints**

Thank you for reviewing my lab. I hope it has provided a clearer understanding of (DNS) Domain Name Service.
