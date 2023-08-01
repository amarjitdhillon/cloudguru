

Route 53 offers a number of different routing policies: 
- Simple
- Failover
- Geolocation
- Geo proximity
- Latency-based
- Multivalue answer 
- Weighted

Route 53 supports up to 50 domain names by default, but this limit can be raised if requested.

A naked domain is a domain name server (DNS) name that can't be a canonical name record (CNAME). An example is hello.com, without the www subdomain

----
!!! important

    - The A record maps a name to one or more IP addresses when the IP is known and stable.
    - The CNAME record maps a name to another name. It should only be used when there are no other records on that name.
    - The ALIAS record maps a name to another name but can coexist with other records on that name.
    - The URL record redirects the name to the target name using the HTTP 301 status code.



Important rules:

- The A, CNAME, and ALIAS records cause a name to resolve to an IP. Conversely, the URL record redirects the name to a destination. The URL record is a simple and effective way to apply a redirect for one name to another name, for example redirecting www.example.com to example.com.
- The A name must resolve to an IP. The CNAME and ALIAS records must point to a name.



!!! hint "Some imp records are"

    - `A`: They are the most basic type of DNS record and are used to point a domain or subdomain to an IP address.
    - `CNAME`
    - `Alias`
    - `MX`: A mail exchanger record specifies the mail server responsible for accepting email messages on behalf of a domain name.
    - `SOA`: it means Start Of Authority
    - `PTR`: Getting reverse DNS going is done by finding the PTR records in use by a DNS server. 
    - `NS`: NS stands for 'name server' and this record indicates which DNS server is authoritative for that domain (which server contains the actual DNS records). A domain will often have multiple NS records which can indicate primary and backup name servers for that domain.