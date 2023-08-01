# DNS

Azure DNS is a hosting service for DNS domains that provides name resolution by using Microsoft Azure infrastructure. By hosting your domains in Azure, you can manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services.

!!! tip "How it ensures relability?"
    DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers, providing resiliency and high availability. Azure DNS uses `anycast networking`, so each DNS query is answered by the closest available DNS server to provide fast performance and high availability for your domain.

!!! questions "Can I use my own domain name?"
    Azure DNS also supports private DNS domains. This feature allows you to use your own custom domain names in your private virtual networks, rather than being stuck with the Azure-provided names.

## CNAME

### What is CNAME?
The ‘canonical name’ (CNAME) record is used in lieu of an A record, when a domain or subdomain is an alias of another domain. All CNAME records must point to a domain, never to an IP address. Imagine a scavenger hunt where each clue points to another clue, and the final clue points to the treasure. A domain with a CNAME record is like a clue that can point you to another clue (another domain with a CNAME record) or to the treasure (a domain with an A record).

## Example
Suppose `blog.example.com` has a CNAME record with a value of `example.com` (without the ‘blog’). This means when a DNS server hits the DNS records for `blog.example.com`, it actually triggers another DNS lookup to `example.com`, returning example.com’s IP address via its A record. In this case we would say that example.com is the canonical name (or true name) of `blog.example.com`

!!! tip "IP update scenario"
    Oftentimes, when sites have subdomains such as `blog.example.com` or `shop.example.com`, those subdomains will have CNAME records that point to a root domain (`example.com`). This way if the IP address of the host changes, only the DNS `A record` for the root domain needs to be updated and all the `CNAME records` will follow along with whatever changes are made to the root.


## MX record
A DNS `mail exchange` (MX) record directs email to a mail server. The `MX record` indicates how email messages should be routed in accordance with the Simple Mail Transfer Protocol (SMTP, the standard protocol for all email). Like `CNAME records`, an MX record must always point to another domain.

## NS record
NS stands for ‘nameserver,’ and the nameserver record indicates which DNS server is authoritative for that domain (i.e. which server contains the actual DNS records). Basically, NS records tell the Internet where to go to find out a domain's IP address. A domain often has multiple NS records which can indicate primary and secondary nameservers for that domain.

!!! warning
    Without properly configured NS records, users will be unable to load a website or application.

## A record

The "A" stands for "address" and this is the most fundamental type of DNS record: it indicates the IP address of a given domain. For example, if you pull the DNS records of cloudflare.com, the A record currently returns an IP address of: 104.17.210.9.

A records only hold IPv4 addresses. If a website has an IPv6 address, it will instead use an "AAAA" record.

## AAAA record
DNS `AAAA records` match a domain name to an IPv6 address. DNS `AAAA records` are exactly like DNS `A records`, except that they store a domain's IPv6 address instead of its IPv4 address.


