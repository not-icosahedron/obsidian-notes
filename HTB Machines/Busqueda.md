# Initial Enumeration

For this machine I decided to try the `autorecon <ip-address>` command.
Soon I received the output that port 80/tcp and 22/tcp were open, so I went to check out the website on port 80 (HTTP).
The website redirected to `searcher.htb` so I added it to the hosts file with `echo '<ip-address> searcher.htb | sudo tee -a /etc/hosts` command.
After this I started a Fuzz with `ffuf` against the website, with no findings.
## Web Page
The Web Page presents a website that generates a url for a search parameter; selecting the search engine, and inputting the search parameter we get the link to the search result page, that we can navigate to.
Further enumeration of the web page reveals that the website uses 2 main components to achieve this; 