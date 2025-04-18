# Why DNS
- DNS is the phonebook of the internet. Humans access information online through domain names, like nytimes.com or espn.com. Web browsers interact through Internet Protocol (IP) addresses. DNS translates domain names to IP addresses so browsers can load Internet resources.
- Each device connected to the Internet has a unique IP address which other machines use to find the device. DNS servers eliminate the need for humans to memorize IP addresses.

![Network Image](image/dns-world/1.png) <br>
![Network Image](image/dns-world/2.png) <br>
![Network Image](image/dns-world/3.png) <br>

Thanks to the DNS, we can use domain names to communicate with computers or their services.

![Network Image](image/dns-world/4.png) <br>
Why Can't we Just use IP address instead of domain names?
The simplest reason is that for most humans, it's easier to remember a domain name than remembering an IP address.
![Network Image](image/dns-world/5.png) <br>
But There are a couple of technical reasons behind the importance of DNS:
1. **Infracstructure Migration:** One quick example is infrastructure migration. Imagine you come from work, ready to continue your favorite show on Netflix, but instead of simply typing netflix.com in your browser, you'd have to remember the IP address of the site. Then one day, the Netflix folks perform an infrastructure migration, and the IP address of the infrastructure hosting the site changes, rendering you unable to access Netflix that evening. That is, until you figure out what the correct and updated IP address is. Certainly, it would be a nightmare to keep track of these changing numbers for every website you visit, right? <br>
![Network Image](image/dns-world/6.png) <br>
![Network Image](image/dns-world/7.png) <br>


2. **Internet is Complex:**
The second technical reason is that the `internet is complex`. Often, when learning DNS, you'll hear or read an explanation, such as, the DNS translates a domain name into the IP of a computer hosting a service, but more often than not, there won't be such a thing as having a single IP for a computer hosting a service. This is because the internet relies on complex architectures, such as **content delivery networks** and **DNS systems**, to keep systems performant and well distributed globally, which means there could be dozens or even hundreds of IP addresses that turn out to be the IP address on duty that serves a given service. Just for this reason alone, using IP addresses is definitely not a great idea. And just to keep 
stacking reasons why DNS is so useful and important, we have that IPv6 addresses are even more difficult to remember, Instead of memorizing numbers, we use domain names to access the internet. Lets look at our earlier example, kodekloud.com.

![Network Image](image/dns-world/8.png) <br>
![Network Image](image/dns-world/9.png) <br>
![Network Image](image/dns-world/10.png) <br>
![Network Image](image/dns-world/11.png) <br>
![Network Image](image/dns-world/12.png) <br>
## DNS Queries:

#### DNS Resolution process in two different programs:
1. On Browser:
2. DIG Command:

**On Browser:**
![Network Image](image/dns-world/13.png) <br>
In the above image, I found this one and we see that there's a portion that says **remote address**, and then we have an IPv6 address that is responding on port 443. This IPv6 is what's known as a **AAAA record**. <br>


Let's see how we can match this information that the browser is giving us by going to the terminal and trying to get the same result. So now, I'm going here to my terminal, and then I'm going to type `dig kodekloud.com`, and you can see that we have three different IP addresses. <br>
![Network Image](image/dns-world/14.png) <br>

***This means that any of these three IP addresses is capable of serving KodeKloud.com***. 

Now, as you can see, the IP addresses are *version 4*. So, the response that I'm getting is the same as if I was doing `dig KodeKloud.com A`. <br>
![Network Image](image/dns-world/15.png) <br>

You can see that it's the same thing. <br>
Now, if I happen to do `dig kodekloud.com AAAA`, you'll see that it gives us the IPv6 IP addresses that are the equivalent of the above 3 IP addresses(IPv4) that we got.<br>
![Network Image](image/dns-world/16.png) <br>

we can see that the browser is using the IPv4 `104.26.11.250:443` address to connect to the website and `dig KodeKloud.com A` shows us also `104.26.11.250:443` address. <br>

The gist of this video is to understand that a domain name can be translated into an A record, otherwise known as an IPv4 IP address, or a AAAA record, which is an IPv6 IP address. Now, if you notice, my browser automatically responded to the IP address in an IPv6 format. This is customizable depending on your resolver, your operating system configuration, or your browser configuration. If any of this is confusing, don't worry. We will go over record types and all the other stuff that we saw in this video as we progress with the course. I just thought it would be a good idea to give an early exposure on how the DNS resolution process happens from two different perspectives.


## Terminology:
The purpose is to define some concepts around domain names. Here we will discuss domain names, URLs and email address and how they are related to each other.<br>
![Network Image](image/dns-world/17.png) <br>

First give an analogy to understand that it will help us to understand these concept better:<br><br>
Think of a domain name like a piece of land that you own for a fixed period of time. When you register a domain, like KodeKloud.com, you are essentially buying your own piece of internet real estate for a fixed period of time. <br>
![Network Image](image/dns-world/18.png) <br>

This domain name becomes your base identity on the internet. Now, here's where it gets interesting. When you type KodeKloud.com in your browser, what happens there is that you type a domain name, and given how there's a web server exposing this service, your browser translates this into a URL. <br>
![Network Image](image/dns-world/19.png) <br>

The distinction between a URL and a domain name is important because domain names not only serve web applications, they also serve other types of services like emails, for example. And this is all possible, thanks to the DNS and the existence of domain names. A URL can be identified by the presence of the HTTP prefix and an email by the presence of the @ symbol.<br>
![Network Image](image/dns-world/20.png) <br>



Another interesting perspective on this topic is how, within organizations, such as KodeKloud, for example, servers may be given hostnames, like webserver01.
 ![Network Image](image/dns-world/21.png) <br>

And when you combine this hostname with the organization's domain name, you get what we call a Fully Qualified Domain Name, or FQDN, which in this case will be `webserver01.kodekloud.com`. <br>
![Network Image](image/dns-world/22.png) <br> 

You may also notice that many websites use `www`, like in www.kodekloud.com. This *www* is actually a subdomain that is traditionally used to indicate that a web service is being exposed, though it is not required for websites to work.<br>
![Network Image](image/dns-world/23.png) <br>

So breaking down these concepts, a domain name is your base identity on the Internet. It's like a piece of land that you buy or rent. <br>
![Network Image](image/dns-world/24.png) <br>

From this domain name, you can host multiple different services. All these different services, web, email and other can exist on the same domain name.<br>
![Network Image](image/dns-world/25.png) <br>

So owning a public domain name gives you the ability to create services and expose them where people will be able to use them by referencing your domain name. Just like you build different things, like offices or apartments on the same piece of land, the DNS helps direct traffic to the right service, web, email, and all that, based on how you're trying to use the domain name. And we'll learn more about that as we progress through the course.<br>

## Domain Name Anatomy:
Domain names are written in this particular format of having words separated by dots to create a clear separation of ownership and responsibility. To understand why domain names use this format, we will use the analogy that compares owning a domain name and owning a piece of land. <br>
![Network Image](image/dns-world/26.png) <br>

First let's understand that domain names are read from right to left, with the rightmost part, like `.com`, being the least specific. This means that when you see a domain name like `kodeKloud.com`, you should think of it as KodeKloud being registered on a huge piece of land called com.<br>
![Network Image](image/dns-world/27.png) <br>

In this analogy, com is a large piece of land that can be subdivided into smaller lands. Think of this as if organizations could rent portions of this land to create their own services, just like registering a domain name with the *`.com`* suffix. <br>
![Network Image](image/dns-world/28.png) <br>
The domain registration process also works as a subdivision, where the owners of the com domain effectively say, we will make you responsible for this domain, as long as you are the owner. Think of this as if a piece of land was assigned to a company, individual or organization. <br>
![Network Image](image/dns-world/29.png) <br>

To keep the domain, they need to pay an annual registration fee through a registrar company capable of fixing all the legal documents for both parties. So following the analogy, when `kodekloud.com` was registered, <br>
![Network Image](image/dns-world/30.png) <br>

a subdivision of the `com land` was given to KodeKloud that they now maintain. This maintenance responsibility gives KodeKloud the authority to create services that can be referenced by using the `kodekloud.com` domain. But not all domains are registered under com, though.

Take linuxfoundation.org, for example. In their registration process, they went to a different land altogether, one with the name of org. They requested org to subdivide a portion of its huge landmass so they could be responsible for it and build their services there.<br>
![Network Image](image/dns-world/31.png) <br>

As a matter of fact, the DNS can be represented by looking at it as an inverted tree. 
![Network Image](image/dns-world/32.png) <br>

From now on, I am going to start using this model and hopefully, we can go over the land leasing analogy to try to make sense of it from this tree perspective. <br>

Let's first talk about the DNS tree by starting at the top. At the top of the DNS tree, we have something called the `root zone`. The root zone is like a central real estate agency that keeps track of all of the huge lands out there, in other words, the rightmost part of a domain name. 
![Network Image](image/dns-world/33.png) <br>
These huge territories in our analogy are called top-level domains. This includes common suffixes used for websites such as .com, .org, .net, .io, and others. 
![Network Image](image/dns-world/34.png) <br>
Then, below the top-level domains, we have what's known as a second-level domain, with examples such as `linuxfoundation.org` and `kodekloud.com` <br>
![Network Image](image/dns-world/35.png) <br>

Now, in this analogy, we've mentioned so far how the authority of using `KodeKloud.com` domain was given to KodeKloud as an organization by requesting `com` to create a subdivision of their land, so KodeKloud could own the domain and build the services they wanted on this domain, right? <br>
![Network Image](image/dns-world/36.png) <br>

But now, getting a bit technical here, what happens in reality is that KodeKloud went through a domain registration process and when they picked the domain name `kodekloud.com` They probably registered the domain through a company that offers domain registration services such as godaddy.com, Cloudflare, or others. <br>
![Network Image](image/dns-world/37.png) <br>

The domain registration companies are also known as registrars. So in this example, the registrar checked if the domain was available, which it was, I assume. Since the domain ends with com, then a petition to an organization called `Verisign` is made asking them to hand over the ownership and responsibilities, for `KodeKloud.com`. `Verisign` is the organization responsible for .com, and this process of handing over the ownership is what we call delegation of authority. The delegation of authority creates what’s known as a zone, giving KodeKloud control over their domain. But why exactly is Verisign being requested to delegate the authority to KodeKloud and what does this mean? <br>
![Network Image](image/dns-world/38.png) <br>

Well, without delegation of authority, all domains ending in .com would remain under Verisign’s control. Think about it this way. In our land ownership analogy, there's this huge land called .com. When an organization, individual, or company wants to register a domain name, they're asking for their own piece of this land. Without this subdivision process, the entire land would remain as com, meaning Verisign would maintain control over all the non-subdivided portions. <br>
![Network Image](image/dns-world/39.png) <br>

When these subdivisions happen, they create what you see in the DNS Tree diagram displayed on the screen, where we have multiple levels of ownership. Each level on the tree represents a `zone`. A zone is similar to the land being owned.<br>

![Network Image](image/dns-world/40.png) <br>

The domains and subdomains are similar to erecting buildings with different types of functions such as offices, apartments, and more. <br>
![Network Image](image/dns-world/41.png) <br>

In the case of KodeKloud, a subdomain that you may be familiar with is ``engineer.kodekloud.com``. This subdomain is still part of the kodekloud.com zone. <br>
![Network Image](image/dns-world/42.png) <br>

and because of this, KodeKloud could continue to add more subdomains to it, like `example1.engineer.kodekloud.com` and `example2.engineer.kodekloud.com` while still being the owners.<br>
![Network Image](image/dns-world/43.png) <br>
And similarly, `linuxfoundation.org` has subdomains in this same zone, such as `training.linuxfoundation.org`.<br>
![Network Image](image/dns-world/44.png) <br>

Where I'm trying to go here, is that the same rule applies to the top-level domains. The org top-level domain, which is managed by the Public Interest Registry (PIR), and the com top-level domain, which is managed by VeriSign, could create multiple subdomains such as whatever.com or something.org while still being on the same zone, meaning they'd keep full ownership of these domains. <br>
![Network Image](image/dns-world/45.png) <br>

However, this doesn't generally happen, though, as organizations in charge of top-level domains take their role seriously Instead, their primary focus is probably on maintaining their registries and making domains available for organizations, individuals, or companies that wish to register them through authorized registrars. <br>
![Network Image](image/dns-world/46.png) <br>

But let’s tease our brains a little by thinking about what would happen in the fictitious case that KodeKloud decided to sell the `engineer.kodekloud.com` services to another company, but they chose to keep the same ``engineer.kodekloud.com`` domain name. <br>
![Network Image](image/dns-world/47.png) <br>


kodekloud.com and `engineer.kodekloud.com` both belong to the same zone right now, and this can be proven by using the `dig` command to both kodekloud.com domain and to its subdomain `engineer.kodekloud.com`. We can see in the output shown on the screen how both respond with the same set of `A` records, indicating they're in the same zone. <br>
![Network Image](image/dns-world/48.png) <br>

If KodeKloud wished to split the services into two different companies, what would happen here is that `engineer.kodekloud.com` would go through a delegation of authority process so that it'd begin to exist in a new zone similar to the animation shown on the screen. <br>
![Network Image](image/dns-world/49.png) <br>

We will learn the technicalities behind a delegation of authority in another section. For now, just think about it as the process of how a subdomain would be transferred to a new zone. <br>

Now, I want you to observe how by doing the same dig command to `linuxfoundation.org` and `traning.linuxfoundation.org`, its not immediately visible whether they are in the same zone or not, as both DNS queries may return a different set of `A` records IP Address in the reponse. <br>
 ![Network Image](image/dns-world/50.png) <br>
We will show a demo that how to safely determine if nested subdomains belong to the same zone or not. <br>



## The Root Zone:
We are representing the DNS using a diagram of an inverted tree that starts at the Root Zone.<br>
![Network Image](image/root-zone/1.png) <br>
The Root Zone is shown as a dot(.) in the diagram because every domain name actually ends with a dot, even if you cannot see it. You can test this yourself. Try typing a domain name in your browser with a dot at the end, like `youtube.com.` or `wikipedia.org.` and it should resolve just fine. So the dot that represents the root zone is always implicitly part of the domain names, even when we don’t explicitly type it in.<br>

You can also test this with the dig command. Whether you include the dot or not at the end of a domain name, you will get the same result, as shown in the animation on screen. <br>
![Network Image](image/root-zone/2.png) <br>

The root zone can also be queried by simply typing dig space dot, as demonstrated on the output shown on the screen. 
But what is a root zone and why does it matter? <br>
![Network Image](image/root-zone/3.png) <br>
To understand the root zone, remember what we learned earlier. Domain names are read from right to left, where the rightmost part is the most general. and the leftmost part is the most specific. <br>
![Network Image](image/root-zone/4.png) <br>

DNS queries work the same way. When you look up a domain name, the DNS starts reading from the right side beginning at the Root Zone, then moving to the Top-Level Domain, and so on until it reaches the left-most part of the domain name. Let's use our land analogy to make this clearer. <br>
 
Remember how we said a domain name like `kodeKloud.com` is like a piece of land within the larger territory of .com, and linuxfoundation.org is like a piece of land within .org. So where does the root zone fit in this picture? <br>
![Network Image](image/root-zone/5.png) <br>

Well, you could say that the root zone is planet Earth or something, because all domain names are a subdivision of planet Earth, which means all possible pieces of land have a relationship with the root zone. I hope you can see how saying that domain names go from least specific on the far right to most specific on the far left matches perfectly with our earth analogy. <br>
![Network Image](image/root-zone/6.png) <br> 

For example, looking up facebook.com, a DNS query starts on the Root Zone, then it looks for the Top Level Domain called com, and finally finds a specific area called facebook. <br>
![Network Image](image/root-zone/7.png) <br>
![Network Image](image/root-zone/8.png) <br>
![Network Image](image/root-zone/9.png) <br>

In technical terms, this means that the root zone needs to know how to find any top-level domain in the world. <br>
![Network Image](image/root-zone/10.png) <br>

Remember we've said in previous lectures that zones in the DNS are a way to delegate authority and responsibility of domain names to an organization, individual, or company, and how VeriSign was responsible for the com top-level domain and all that? Well, the root zone is no exception to this rule. The root zone is managed by **IANA**, which is the Internet Assigned Numbers Authority, and it operates under **ICANN**, Internet Corporation for Assigned Names and Numbers.<br>
![Network Image](image/root-zone/11.png) <br>

Think of ICANN like a global organization that makes sure the internet's naming system works smoothly for everyone. Since the root zone is at the very top, it makes sense that it needs a global organization to manage it. IANA’s job is to keep track of all the top-level domains and make sure that the root zone data is accurate and secure. It’s like having a central authority that everyone trusts to maintain Earth’s address book.<br>
![Network Image](image/root-zone/12.png) <br>

Let me show you how this works in a simple way. Just keep in mind that we’ll cover all the technical details about DNS systems and infrastructure in a later section. From this tree-like diagram, you can think about the DNS like a system that assigns servers that act as a database-like system to each zone that exists in the DNS. These servers that act as databases for each zone are called **name servers**. The name is quite literal. They’re servers that contain information about domain names that belong to their zone. <br>
![Network Image](image/root-zone/13.png) <br>

In the animation displayed on the screen, we have a representation of how this database can be thought about, so you create a mental map for this. Think of it as a simple system where each name server `stores key-value pairs` like this a.gtld-servers.net pointing to 192.5.6.30. This same database-like information is copied to all root zone name servers, ensuring they all have the same information. <br>
![Network Image](image/root-zone/14.png) <br>
![Network Image](image/root-zone/15.png) <br>
![Network Image](image/root-zone/16.png) <br>
![Network Image](image/root-zone/17.png) <br>
Now, elaborating more on the purpose of name servers, remember our land analogy? If the root zone is planet Earth, then name servers are like information offices that know about different pieces of land. When you ask a root name server about facebook.com, it's like asking, where can I find information about this land called com? <br>
![Network Image](image/root-zone/18.png) <br>

And the root name server will point you to the specific name servers that know about all the lands within com. <br>
![Network Image](image/root-zone/19.png) <br>

The root zone name servers have key-value pair entries similar to the table displayed on the screen. These entries help resolve any top-level domain by providing the IP address of the name servers for the next domain in the resolution chain. <br>
![Network Image](image/root-zone/20.png) <br>

An IP address is ultimately needed because it gives the exact location. Think of it like providing exact coordinates instead of just a name.<br>
![Network Image](image/root-zone/21.png) <br>

We can see the name servers associated with a zone by using the dig command. When we type `dig . NS`, where NS stands for name servers, we're basically asking, Hey, which name servers are responsible for the root zone? The response shows that there are 13 of these root name servers labeled from A to M. <br>
![Network Image](image/root-zone/22.png) <br>

By the way, the reason why it’s 13 name servers, it's because that was the maximum number of name servers that could fit into a single 512-byte UDP packet. We'll dive deeper into this when we cover the DNS protocol section. <br><br>

So DNS resolution is like a game where you can only ask for information about a zone by consulting its parent zone's name servers.<br>
![Network Image](image/root-zone/23.png) <br>

This is why all DNS queries begin from the root zone. You have to start at the top and work your way down, one zone at a time. So this explains the importance of the root zone. Its name servers know how to direct you to any top-level domain in the world. They don’t need to know about facebook.com specifically. They just need to know which name servers are responsible for the com domains in this example.
![Network Image](image/root-zone/24.png) <br>

## Top-Level Domain:
Now that we understand the Root Zone better, let's talk about another fundamental part of the DNS, Top-Level Domains, or TLDs for short.<br>

We have been comparing top-level domains as big territories on earth; however, top-level domains also have different classifications within themselves that are worth talking about so you understand the DNS better. <br>
![Network Image](image/tld/1.png) <br>

I want to focus on **two** of what I believe are the most important top-level domain classifications.

First, we have what we call *generic top-level domains*, or **gTLDs**, such as com, io, net, org, ai, etc. Think of this like international territories that anyone from any country can use.<br>
![Network Image](image/tld/2.png) <br>

Then we have *country-code top-level domains*, often abbreviated as **ccTLDs**. These are the two-letter-long labels I'm sure you've seen, which are used to represent specific countries, making it possible to create country-specific versions of services and websites. For example, Amazon has `amazon.com.mx` for its Mexican service.
![Network Image](image/tld/3.png) <br>
![Network Image](image/tld/4.png) <br>

Government agencies use their country codes for official websites, and many local services choose their country code domains to indicate they operate specifically in that country.

#### Generic TLDs (gTLDs)
Ok, so let's begin talking about generic top-level domains. Unlike country-code top-level domains that are used for country-specific services, generic top-level domains are commonly used to serve users globally. The best examples are services like youtube.com, google.com, netflix.com, and of course, kodeKloud.com, which use their .com domains to reach users worldwide, regardless of what country they’re in.<br>
![Network Image](image/tld/5.png) <br>

The most popular generic TLD is `com`, which was originally meant for commercial organizations, but is now used by pretty much anyone who wants a broad presence on the internet. Others like `org`, which was originally for non-profit organizations, and `net`, for network providers are also widely used. Although these days, the original purpose of each TLD isn't strictly enforced. However, <br> 
![Network Image](image/tld/6.png) <br>


There is an interesting exception that applies to many United states based Services. Some organzations that originated in the United States often use .com for their US-specific services rather than using .us. Amazon is a perfect example.<br>
![Network Image](image/tld/7.png) <br>

Amazon.com primarily serves US customers, while they create specific domains for other countries as is the example I talked about of `amazon.com.mx` for Mexico.<br>
![Network Image](image/tld/8.png) <br>

This is partly because historically, many US organizations didn't adopt the US domain like other countries did with their country codes.

The United States is also unique in that they use the `.gov` Top-Level Domain exclusively for its government, while most other countries use their country code TLD for government services which we'll talk about more when we cover country code TLDs.<br> 

The list of generic top-level domains isn't short of just the samples we have displayed on screen. As of 2024, there are over 1,500 of them. Now, we have talked about how registering a domain name, such as kodekloud.com, is like subdividing a piece of the `com` land and how this is a process that happens when a registrar, in other words, a company in charge of providing domain registration services, checks if the desired domain is available for registration, and then it requests com to delegate the authority of `kodekloud.com` to KodeKloud, right? <br>
![Network Image](image/tld/9.png) <br>
![Network Image](image/tld/10.png) <br>

And then we talked about how the Root Zone is the highest level of the DNS hierarchy, containing information about all Top-Level Domains, which is crucial for the DNS resolution process. <br>
![Network Image](image/tld/11.png) <br>

Well, theoretically, the generic top-level domains are also domains. So can we just create a domain directly as a subdomain of the root zone, such as `somedomain.`?
![Network Image](image/tld/12.png) <br>

Well, *the truth is that this is not possible*. First off, because registering a generic top-level domain requires a specific process, you have to pay an application fee of about $185,000 to apply for creating a new top-level domain. And these applications go through IANA, which oversees the approval process. These processes happen in rounds, with the last one being in 2012, according to the information from the website displayed on the screen.<br>
![Network Image](image/tld/13.png) <br>
One interesting thing about top-level domains is that some of them support what we call internationalized domain names, or IDNs.

Ever wondered why domain names seem limited in their characters? Well, original DNS was designed to work strictly with ASCII characters, which means standard English alphabet letters. So by default, a domain name only allows characters from A to Z, numbers from 0 to 9, and hyphens.But the hyphen can't be used at the start or end of a label. Domain names are case insensitive, by the way.Now each label in a domain name can be up to 63 characters long, with the total domain name limited to 253 characters. <br>
![Network Image](image/tld/14.png) <br>

But the internet is global, right? That's where IDNs come in. Today many top-level domains like com, org, and info allow registration using different writing systems like Arabic, Chinese, or Japanese characters. These get converted into ASCII using a special encoding called Punycode, as in the animation displayed on the screen.<br>
![Network Image](image/tld/15.png) <br>

 On screen we have a sample of a German U with two dots above it, and how it gets converted into regular ASCII characters on the right.<br>
 ![Network Image](image/tld/16.png) <br> <br><br>
 

 **ccTLDs**
 Now let’s talk about country code top-level domains. Unlike generic top-level domains that require a complex application process that happens very infrequently and costs hundreds of thousands of dollars, creating a country code top-level domain, otherwise known as ccTLD, would require you to create your own country and get it officially recognized by some global organization.<br>
 
 
Living hypothetical scenarios aside, country code top-level domains are always two characters long and each country gets to decide how their country code top-level domain works and where people can register domain names within it. Now understanding country code top-level domains is very important when adhering to the idea that a zone represents authority and responsibility, because they actually make this concept more complex. <br>
![Network Image](image/tld/17.png) <br>

With generic top-level domains like com, org, or io, it's straightforward. Domains with a simple top-level domain like kodekloud.com can be easily represented in its own zone under the com zone, because it is very straightforward that the com top-level domain had to be subdivided as in the land analogy. But with country code top-level domains, things get trickier. <br>
![Network Image](image/tld/18.png) <br>

To explain this, let’s look at a portion of the public suffix list at publicsuffix.org, which is, in other words, a list that documents how different TLDs structure their domain names and where public registration is allowed.

Let’s examine Hong Kong’s country code top-level domain as an example. Their country code is HK, and all these domains below HK, such as com.hk, edu.hk, and gov.hk belong to the same zone, even though they have different labels to their left. <br>
![Network Image](image/tld/19.png) <br>

This example shows how a country can organize its namespaces as each country gets to make its own rules. 
![Network Image](image/tld/20.png) <br>

Some may allow direct registration under their ccTLD, while others may only allow registration after, say for example, `com.hk`.
<br>
![Network Image](image/tld/21.png) <br>

For example, Hong Kong allows registration both directly under the HK label, as we can see when querying domain.hk, which, at the moment of recording this video, resolves to an existing domain. But we also have `amazon.com.hk`, for which `com.hk` is represented in the same hk zone, with `amazon.com.hk` being only a zone below hk, as seen in the diagram shown on the screen.
![Network Image](image/tld/22.png) <br>

So public suffixes are essentially like a checkpoint in a domain where public registration begins to be allowed. It helps define where one registrant's control ends, and another's begins. The public suffix list documents these registration boundaries for different generic top-level domains and country code top-level domains around the world.<br>
![Network Image](image/tld/23.png) <br>
The United Kingdom follows a similar pattern with its ccTLD, but with a key difference. While Hong Kong allows registration of domains directly under their two-character label, and the majority of the countries do, I believe, the UK doesn't allow registration directly under UK. Instead, domains must be registered under specific categories that are all part of the UK zone, such as co.uk for companies, ac.uk for academic institutions, and org.uk for organizations. <br>
![Network Image](image/tld/24.png) <br>

Now, country code top-level domains can be queried using dig. A quick example is dig.jp, which will display information about Japan’s country code top-level domain.<br>
![Network Image](image/tld/25.png) <br>

Some specific cases like Mexico's MX or India's in require you to add a dot at the end. Why? Because without the dot, dig might interpret this differently. For example, MX by itself looks like you're asking about email servers or MX records, and IN is interpreted as the Internet class of DNS records, in both cases resulting in a query to the root zone instead of the intended ccTLD. <br>
![Network Image](image/tld/26.png) <br>

Adding the dot explicitly tells dig that you're querying a country code top-level domain and not just a DNS record type. We will learn more about these and other record types throughout the course. Remember that we've already seen the NS record type when learning about the Root Zone when we used `dig . NS`. Keep this in mind when trying the examples of querying MX and IN TLDs to understand what I'm talking about. <br>
![Network Image](image/tld/27.png) <br>
 
All these top-level domains, whether generic or country code, need someone to manage them. Remember how we talked about IANA managing the Root Zone? Well, each Top-Level Domain has its own manager too. For example, Verisign manages .com, and each country typically has an organization that manages their country code Top-Level Domain.<br>
![Network Image](image/tld/28.png) <br>

Each top-level domain gets to set their own rules and prices for registering domain names. For example, some top-level domains might be really cheap, like .com domains costing around $10 to $15 a year, while others might be super expensive, costing hundreds or even thousands of dollars. It all depends on what that top-level domain's manager decides.<br> 


Now besides generic and country code top-level domains, there are some special categories of top-level domains that serve specific purposes. <br>
![Network Image](image/tld/29.png) <br>


*First we have infrastructure top-level domains. The main example is .ARPA, which is used for managing Internet infrastructure. You won't register domains under ARPA. It's reserved for technical purposes that help the internet work. We'll see more about ARPA when we talk about reverse DNS lookups later in this course.* <br>

But to give a quick overview, when you see something like this `1.0.0.127.in-addr.arpa`, you can assume that this domain name is used for what we call *reverse DNS lookups*.<br>
![Network Image](image/tld/30.png) <br>

You can also do the opposite. You can try this by using dig and the -x flag, followed by an IP address.

For example, the command on the screen will perform a reverse DNS lookup for that IP address. What's interesting is that behind the scenes, this command actually queries the in-addr.ARPA zone. But why do we need the ARPA for this? Well, IP addresses and domain names work in opposite directions. <br>
![Network Image](image/tld/31.png) <br>

Domain names are read from right to left, like we learned earlier. But IP addresses are typically read from left to right. To make reverse DNS lookups work within the DNS system, IP addresses need to be reversed and have the in-addr.ARPA added at the end. <br>
![Network Image](image/tld/32.png) <br>

So when you do dig -x 127.0.0.1, dig automatically converts this into a query for 1.0.0.127.in-addr.arpa. Each number in the IP becomes a label in this special domain name, but in reverse order.<br>
![Network Image](image/tld/33.png) <br>

This way, the DNS system can handle IP lookups just like it handles regular domain name queries. This is just one way .ARPA helps manage internet infrastructure. And we will dive deeper into reverse DNS lookups and see exactly how these queries work in another section. But I wanted to give you this overview to understand why infrastructure top-level domains like ARPA are important. Then we have restricted top-level domains, also called generic restricted top-level domains or gTLDs. These are like regular generic top-level domains but with strict rules about who can register domains under them. For example, edu was originally restricted to US educational institutions and mil is exclusively for the United States military. <br>
![Network Image](image/tld/34.png) <br>

We also have sponsored TLDs and these are specialized TLDs that have sponsored communities, for example .museum for museums or .post for postal services. <br>
![Network Image](image/tld/35.png) <br>

Finally we have test top-level domains which are specifically reserved for testing purposes. The main one you might see is .test which is never used in the real DNS system but it's reserved so developers can safely test DNS-related software without risking conflicts with real domain names.

## Domain and Zones
Before we progress further in the course, I want to make sure that everyone watching can confidently determine if two or more domains belong to the same zone or if they are in different zones.<br>
![Network Image](image/domain_zones/1.png) <br>

So far in this course, we've used some analogies comparing domains to pieces of land. We've talked about how registering a new domain name such as KodeKloud.com is similar to getting a piece of land that's part of a larger territory named com.

It's important to highlight that the name of your piece of land will always include in its name, the name of the larger territory that it's part of.<br>
![Network Image](image/domain_zones/2.png) <br>

That's why we say kodekloud.com. When you own this piece of land, in other words, your domain, you can build different things in it, like how KodeKloud has built their website, their lab service, and the KodeKloud engineer platform.<br>
![Network Image](image/domain_zones/3.png) <br>

It's like having a piece of land where you can build different offices, classrooms, apartments, etc. What I want you to imagine is that, in this analogy, paying for this piece of land that you divide from .com is akin to the act of creating a new zone, in other words, a space where you have the authority over what gets built in there. <br>
![Network Image](image/domain_zones/4.png) <br>

Remember that zones are meant to represent authority or ownership that an organization, company, or individual has over a domain name. At first glance, the zone concept may seem pretty straightforward. <br>
![Network Image](image/domain_zones/5.png) <br>

You may look at a domain name like `mail.google.com`, separate each label, and quickly assume that each label represents a zone.<br>

Following this intuition, you might think that this domain name involves these zones, the Root Zone, com zone, and google zone, with mail being part of google.com zone. With this particular example, you'd be correct, but there's a problem with this approach. We're basically relying on our familiarity with Google as a company to guess that google.com is a main domain, and therefore mail must be part of the Google zone. But what happens when we don't know the company, or when the structure isn’t so obvious? This becomes even trickier when we look at country code top-level domains which we learned about in our previous lecture. <br>

![Network Image](image/domain_zones/6.png) <br>

Remember how we discussed that some country codes can actually use two labels? Let's look at the example shown on screen.<br>
![Network Image](image/domain_zones/7.png) <br>

In Hong Kong's case, the hk country code TLD can also use com.hk, edu.hk, and other public suffixes. How can we represent a zone structure for a domain like yahoo.com.hk? <br>

Looking at this domain name, we might be tempted to think that the zone structure is formed simply by going from right to left, where we would have the root zone,<br>
![Network Image](image/domain_zones/8.png) <br>
and then the HK zone,<br>
![Network Image](image/domain_zones/9.png) <br>
and then com.hk zone,<br>
![Network Image](image/domain_zones/10.png) <br>
and finally the yahoo.com.hk zone.<br>
![Network Image](image/domain_zones/11.png) <br>
But this is incorrect.<br>
![Network Image](image/domain_zones/12.png) <br>

Remember from our previous lecture that com.hk together forms a single zone. So, to help us solve this problem properly, we first have to be very clear about the different ways we can refer to parts of a domain name. In this course, we've used terms like top-level domain, second-level domain, third- and fourth-level domains, and also subdomains, and so on.<br>
![Network Image](image/domain_zones/13.png) <br>

And I want to explain these as I feel, this would make the process of understanding zones much easier. Let's look at this from two different perspectives, what I call the **absolute perspective** and the **relative perspective**.

In the absolute perspective, we always count from right to left, starting from the Root Zone. In the domain name shown on the screen, moving from right to left, we have the Top-Level Domain, the second-level domain, the third-level domain, and so on. <br>
![Network Image](image/domain_zones/14.png) <br>

But there's also a relative perspective, which changes depending on where we're looking from. In the animation shown on the screen, if we start from example.com, then `test.example.com` would be the subdomain of `example.com`. And if we move our position to `test.example.com`, then `dev.test.example.com` would be the subdomain of `test.example.com`. So from this relative perspective, we also have the *domain apex*, or what some people call the naked domain. <br>
![Network Image](image/domain_zones/15.png) <br>
This is the actual domain name that was registered and represents the start of a zone. Think of it as a main domain that everything else in the zone branches off from.

So going to the `yahoo.com.hk` zone structure, in the tree diagram shown on the screen, I'm showing what many would assume the zones look like. Where we started the Root Zone, then we have an hk zone, then a com zone, and finally, what would be the domain apex of yahoo.com.hk. <br>

But this assumption about how the zones are structured would be incorrect, like we mentioned previously. This second diagram shows how these zones are actually structured.<br>

Notice how com.hk global top-level domain is treated as a single unit in the zone hierarchy, with yahoo.com.hk being the domain apex of its zone.

The difference between these two diagrams highlights why we can't just rely on counting labels from right to left to understand zone structures. <br>
![Network Image](image/domain_zones/16.png) <br>

This can be proven by using a `dig` command with a +trace option against the yahoo.com.hk domain.<br>
![Network Image](image/domain_zones/17.png) <br>

Okay, so running the dig command with the +trace option to a domain name, like I'm doing here, will give you a simulation of what happens in the DNS resolution process.
Open Terminal and type `dig +trace yahoo.com.hk` and hit enter. <br>

we will get lots of information from here. <br>
we will get the Root Zone name servers:<br>
![Network Image](image/domain_zones/18.png) <br>

Then we will get Top level Domain Name server:<br>
![Network Image](image/domain_zones/19.png) <br>

Then we have who gave us the information:<br>
![Network Image](image/domain_zones/20.png) <br>
![Network Image](image/domain_zones/21.png) <br>

So this essentially proves that `com.hk` is basically a subdomain of the hk top-level domain. Now, I just mentioned that the `dig + trace` command is a simulation of what happens in the DNS resolution process. And I’m saving this explanation for the next section when we are talking about the DNS infrastructure and its intricacies.<br>

Okay, so moving on, I’m going to show you a domain that I own that I registered on Route 53 on where I actually registered a subdomain. And then I hosted the subdomain in a different zone. So you can see how it looks like in the cloud and also in `dig`. I have my primary AWS account. So if I go to Route 53, you can see that I have one hosted zone. And this is my domain name, jcroyolaun.io. When I click on this, you can see that I have the NS Records for the apex of the domain, which is jcroyolaun.io. And then I have the Start of Authority record, which indicates that this is the beginning of a zone. And then I also have a subdomain. <br>
![Network Image](image/domain_zones/22.png) <br>

But you can see that the name servers are different, right? <br> 
![Network Image](image/domain_zones/23.png) <br>

These ones are like 171.9. And we don't have that one right here. And so, yeah, you can do the work and see that they're actually different. So `jcroyolaun.io` and `staging.jcroyolaun.io` are different.<br>
![Network Image](image/domain_zones/24.png) <br>
And this is actually the other account where I have the staging hosted zone. And so what I did was that I created this zone.<br>
![Network Image](image/domain_zones/25.png) <br>

 And then it has different name servers, as you can see, and also a different start of authority. So you can see that this start of authority (SOA) indicates that there is a primary name server for resolving DNS requests for this particular domain. Now, if any of this is a little confusing, this is one of those things that we are going to explain more in depth in the next section. So just follow along and hopefully everything will be clear by then. All right, so I'm going to go back to the terminal. And then I'm going to show you that if I do `dig +trace jcroyolaun.io`, and you'll see that in this case we have the Root Zone and then the IO zone.

![Network Image](image/domain_zones/26.png) <br>

Example:<br>
![Network Image](image/domain_zones/27.png) <br>
KodeKloud.com decided to migrate the engineering service to a different company, but they want to keep the same domain. What they would do is basically do this process of delegation of authority so that the `engineer.kodekloud.com` would end up being in its own separate zone.<br>
![Network Image](image/domain_zones/28.png) <br>
So you can see here, if I type it in, it is not in a different zone, right? It’s in the same zone as KodeKloud.com, same as labs and so on and so forth. For them to be in different zones, just to finalize this demo lecture, I want to show you what the process would be, at least from the Route 53 perspective. What they would need to do is like right now, they probably have the `engineer.kodekloud.com` as a subdomain record. And then they’ll probably have some A records pointing to it. Yeah, so it’ll be something similar to this just to play around with it. They’ll have something like engineer@kodekloud.com. I’m obviously not going to save this right now, but it’ll be like adding an A record and then they’ll be basically pointing.<br>

# DNS as a System:


## DNS - System or Protocol?
DNS is not only a System but also a Protocol. Translating domain names into IP addresses happens through a complex process involving servers placed around the world working together in a hierarchical structure. The DNS as a protocol is about the rules for making a DNS query. It covers the format of the DNS request and the format of the response as well, and it relies on the DNS infrastructure to be in place. <br>
![Network Image](image/dns-as-system/1.png) <br>


## DNS - a Distributed System

A system can be defined as a collection of interconnected elements working together with a purpose. An example of a system is an ecosystem, where living and non-living things interact. Nature maintains balance and life persists.<br>
![Network Image](image/dns-as-system/2.png) <br>

In the domain name system, we have different types of servers and infrastructure pieces interacting, thanks to which the translation of domain names into IP addresses happens.<br>
![Network Image](image/dns-as-system/3.png) <br>

Now let's take a look at the DNS design. For me, personally, it's remarkable how a system designed in the 80s remains so relevant, even after the exponential internet growth in recent years.

The DNS was designed by smart people that seemed to have predicted that the internet was going to grow. Therefore, the DNS was architected as a distributed system. As a distributed system, the DNS is designed to spread the responsibilities of its various operations in different server types across multiple locations worldwide. It's not just one big computer somewhere that knows all the domain names and IP addresses. Thanks to its design, the DNS is fast, reliable, and scalable. <br>
![Network Image](image/dns-as-system/4.png) <br>

We want to have speed, as a slow DNS would be a huge bottleneck for internet communication. We want to have reliability, as the DNS needs to be always available. This is achieved by fault tolerance, in other words, the ability of a system to keep operating, even on failure.

Imagine a world where sometimes the DNS is down, so you gotta type the Netflix or YouTube IP address in your browser.

We want to have scalability, because the internet grows, and despite its growth rate, there shouldn’t be a concern for losing speed, or reliability as more people adopt the internet. Let’s talk about how the DNS design helps achieve the performance, reliability, and scalability that it is known for.

For this, we’ll define a simplified way to look into **two major components** in the domain name system. We have a type of server called the **1. recursive resolver**, which will be responsible for asking other servers for information.<br>
![Network Image](image/dns-as-system/5.png) <br>

Then we have a **2. name server**, which is responsible for storing the information of which domain name points to which IP address. <br>
![Network Image](image/dns-as-system/6.png) <br>


I like to imagine these two components as detectives, so let's use that analogy to explain the whole process.<br>
![Network Image](image/dns-as-system/7.png) <br>

The recursive resolver is like a seasoned detective who knows how to navigate the complex world of DNS. This detective is skilled at quickly finding the right sources of information and remembering previous cases. The name server acts as a specialized agent with access to the source of truth. <br>
![Network Image](image/dns-as-system/8.png) <br>

These agents are strategically positioned around the world, each safeguarding crucial information about domain names and their corresponding IP addresses. <br>
![Network Image](image/dns-as-system/9.png) <br>

This speed of DNS is achieves by having multiple detectives and agents working together. When a DNS request comes in, the recursive resolver detective will often attempt to solve the case by referring to notes from previous investigations. This is known as caching, and it's often the first place where the investigation begins. <br>
![Network Image](image/dns-as-system/10.png) <br>

Later in the course, we will learn about different caching layers that play a role in the speed of the DNS. If the detectives can find anything in cache, AKA their notes, they’ll know exactly which name server agents to contact for the most up-to-date information. <br>

The reliability of DNS comes from having a vast network of resolvers and agents. If one resolver or agent is unavailable, there are always others ready to take on the case. This redundancy ensures that the DNS investigation process continues smoothly, even if some team members are temporarily out of action. <br>
![Network Image](image/dns-as-system/11.png) <br>

As for scalability, the DNS is designed to grow its directory as needed. As the Internet expands with more domains and users, new records and agents can be easily added to the network. This flexibility allows the DNS to handle an ever-increasing number of requests without ever compromising on speed or accuracy. <br>
![Network Image](image/dns-as-system/12.png) <br>

I want to emphasize the distributed system concept one more time. Why? First, because DNS, as one of the foundations of the Internet, being a distributed system, is why the DNS works so well. But being distributed is also why the DNS is hard for us, engineers, to learn and troubleshoot, because there’s no longer a single point of failure to look for. Second, because building the muscle of defining system designs in a correct category is a very important part of learning, and improving as an engineer, as it gives the ability to see patterns and correlations in other system designs as well. <br><br>

## DNS Resolvers
Personally, I find the concept of resolvers as one of those that are simple on the surface but can be very complex when going deeper, and it's no surprise, as we're talking about one of the core mechanisms that make the internet work.<br>

Because of this complexity, I'm trying to simplify the concept by comparing DNS resolvers to detectives that know their way around the complex DNS world, so they can help us, the end users, browse the World Wide Web using simple domain names we can remember. Remember that the role of DNS resolvers is to receive a DNS query and look for an answer by doing something that people usually refer to as walking the DNS Tree. <br>
![Network Image](image/dns-resolvers/1.png) <br>

I'll explain this in detail later in this section, but it basically refers to the act of starting the DNS resolution process at the root of the DNS tree and asking a root zone nameserver for the location of a top-level domain. Then you request the top-level domain for the location of a second-level or third-level domain.<br>
![Network Image](image/dns-resolvers/2.png) <br>

Domain depending on the zone hierarchy, and so on. We went over nameservers in the previous section. To put it simply, let's say you have a Python application and you want to deploy it so others can access it. You might use DigitalOcean, where you can create a Linux virtual machine, which they call a droplet, and deploy your code there. DigitalOcean will give you a public IP address that anyone can use to reach your application through the Internet. <br>
![Network Image](image/dns-resolvers/3.png) <br>

Now, if you want people to access it using a friendly domain name like `myawesomepythonapp.xyz` instead of that IP address, you just need to add an A record pointing to your application's IP address on the nameservers assigned to your domain. These nameservers are owned by different organizations responsible for each zone.<br>
![Network Image](image/dns-resolvers/4.png) <br>

IANA manages the root zone nameservers, various companies manage TLD zones like COM, being managed by VeriSign, and your domain's nameservers will be managed by whoever you choose as your provider. But who owns the resolvers, which are our DNS detectives? <br>
![Network Image](image/dns-resolvers/5.png) <br>

Well, there are several players in this game. Some big companies provide public resolvers worldwide, like Google, Cloudflare, or others.

Internet providers also run their own resolvers. For example, I'm from Mexico, and when I connect to the Internet, my resolver is automatically assigned to Telmex, which is a major ISP here. <br>
![Network Image](image/dns-resolvers/6.png) <br>

Looking at this analogy, we can see how there are multiple types of detectives. Some of them are deemed to be faster or slower than others, and this can be benchmarked by using tools like `dnsperf.com`. <br>

Resolvers can be configured in several ways. Your laptop or phone typically uses the resolver provided by your Internet Service Provider by default, but you can change this in your operating system's network settings to use other resolvers you choose.<br>
![Network Image](image/dns-resolvers/7.png) <br>

On Linux systems, for example, these resolver settings live in the `/etc/resolv.conf` file, where you can specify which nameserver to use by adding or modifying the nameserver line. But what if you want to test different resolvers without modifying your system settings?<br>
![Network Image](image/dns-resolvers/8.png) <br>

You can use dig, for example. By using the at symbol, followed by an IP address,<br> 
![Network Image](image/dns-resolvers/9.png) <br>

It's like walking past your neighborhood's assigned detective and asking a different detective to help you instead.
![Network Image](image/dns-resolvers/10.png) <br>
![Network Image](image/dns-resolvers/11.png) <br>
![Network Image](image/dns-resolvers/12.png) <br>
This way, you can compare how different resolvers respond to the same query,

which can be useful for troubleshooting DNS issues or testing resolver performance.<br>
![Network Image](image/dns-resolvers/13.png) <br>
![Network Image](image/dns-resolvers/14.png) <br>
![Network Image](image/dns-resolvers/15.png) <br>

The purpose of resolvers is to help the DNS be fast. Think of them as detective agencies that help distribute the workload. If every single question about a domain name had to go directly to the authoritative nameservers, these nameservers would be overwhelmed with millions of repeated queries.<br>
![Network Image](image/dns-resolvers/16.png) <br>

The resolvers use caching mechanisms to help with DNS speed. Think about this as if the detectives used a notebook where they write common mysteries. When someone asks, where is google.com, and the detective just solved that case 5 minutes ago, they don't need to start a new investigation, they just check their notebook and give you the answer right away.<br>
![Network Image](image/dns-resolvers/17.png) <br>
In technical terms, this means the resolver has cached the DNS record and can respond without querying the authoritative nameservers again. This caching mechanism is crucial because it reduces the load on nameservers across the internet while making responses much faster for users.<br>


## Nameserver

In our previous lecture, we talked about DNS resolvers working like detectives trying to track down IP addresses. These detectives often need help from special agents who have access to the source of truth about specific domains.
The special agents in this analogy are the authoritative nameservers.<br>
![Network Image](image/nameserver/1.png) <br>

Remember that the DNS is all about finding the IP address for the infrastructure providing a service by using a friendlier domain name. Without the DNS, the Internet would require the use of IP addresses for everything. <br>
![Network Image](image/nameserver/2.png) <br>

The nameservers are responsible for maintaining this up-to-date information of a domain name and the IP address of the infrastructure providing the service. <br>
![Network Image](image/nameserver/3.png) <br>

When we perform a DNS query, for example, by typing a domain name in our browser, the resolver, a.k.a. the detective, begins an investigation to find the IP address associated with that domain name.  <br>

To get accurate information, the detective needs to find and talk to the special agents, or authoritative nameservers, who have the official records for that domain. <br>
![Network Image](image/nameserver/4.png) <br>

We previously established that nameservers act similarly to a database. They store and manage all the information about domain names and their IP addresses. This setup follows some important principles we see in database system design principles.<br>
![Network Image](image/nameserver/5.png) <br>

In the world of databases, when we deal with massive amounts of data, we often need ways to handle it efficiently.
One key concept in database design is called sharding, in other words, splitting up a huge database into smaller pieces that different servers can handle. <br>
![Network Image](image/nameserver/6.png) <br>

This makes everything faster and more reliable because each server only needs to deal with its own piece of the data.<br>

In the DNS, nameservers are designed with these principles in mind. Instead of having one massive server trying to handle the entire Internet's worth of domain names,<br>
![Network Image](image/nameserver/7.png) <br>

Different nameservers are responsible for different zones. Some handle com domains, others handle org domains, and some handle country domains like UK. This distributed system approach means that if one part has problems, the rest of the system can still function. <br>
![Network Image](image/nameserver/8.png) <br>

Each nameserver maintains zone files containing records that follow a specific format. Let me show you what a basic zone file looks like. <br>
![Network Image](image/nameserver/9.png) <br>

This zone file contains different types of records. Each line represents a resource record that tells us important information about the domain. <br>
![Network Image](image/nameserver/10.png) <br>

The A records point to IPv4 addresses, while NS records indicate which nameservers are authoritative for this domain. Every domain must have at least two nameservers for redundancy.<br>
![Network Image](image/nameserver/11.png) <br>

Looking at a real-world example, let me run a dig command to show you Google's nameservers. On screen, I'm running a dig command to see how many nameservers Google has. Looking at this output, we can see that Google maintains four nameservers. This is quite common for large organizations, though the minimum requirement is two nameservers. <br>
![Network Image](image/nameserver/12.png) <br>

This redundancy **ensures that DNS queries can always be answered**, even if one or more nameservers become unavailable. <br> Something important to talk about is that, among these nameservers, one is designated as the primary nameserver.

Imagine the primary nameserver as a lead agent who gets the information first, and then it distributes the source of truth among its peers.

We can identify the primary nameserver by looking at something called the SOA record, or **Start of Authority record**. Let me show you what this looks like. On screen, I'm running another dig command, this time by requesting the SOA record by typing `dig google.com SOA`. <br>

Looking at this SOA record, we can see that `ns1.google.com` is the primary nameserver. This means that this nameserver holds the master copy of all the zone data <br>
![Network Image](image/nameserver/13.png) <br>
but, as we've learned, the DNS was designed as a fault-tolerant distributed system.

If there was only one nameserver and it failed, the entire domain would become unreachable. That's why having multiple nameservers is essential for the Internet to run smoothly.<br>
![Network Image](image/nameserver/14.png) <br>

The primary nameserver, `ns1.google.com` in this case, shares its data through a replication process with all the other nameservers listed in the NS Records. <br>
![Network Image](image/nameserver/15.png) <br>
This distributed database approach ensures that no matter which nameserver our resolver contacts, it will receive the same accurate information from the zone's official records.

There's another lecture dedicated to explaining the concept of zone transfers, in other words, the mechanism that keeps all nameservers synchronized with the same records, which is crucial for keeping the distributed nature of DNS by copying zone data from the primary nameserver to all other nameservers in the zone.

## Walking the DNS Tree
Here is a list of Topics that we will cover in this section:<br>
![Network Image](image/walking-dns-tree/1.png) <br>

First, we are going to go over example of the steps that happen when a domain name gets translated into an IP by the DNS, which is often known as walking the DNS tree. <br>
![Network Image](image/walking-dns-tree/2.png) <br>

Then we'll talk about delegation of authority, how DNS zones can delegate control of their subdomains to other name servers, which is a fundamental part of how DNS works as a distributed system. <br>
![Network Image](image/walking-dns-tree/3.png) <br>

This will lead us to an interesting problem. If name servers are identified by domain names, how do we resolve these domain names if we need DNS to resolve names in the first place? <br>
![Network Image](image/walking-dns-tree/4.png) <br>

And even more basic, how do we even reach the root name servers when we don't have any IP addresses to start with?This is what we call the chicken and egg problem in DNS.<br>
![Network Image](image/walking-dns-tree/5.png) <br>

Finally, we'll learn about glue records, a special type of record that helps solve this circular dependency and makes the whole DNS system possible. <br>
![Network Image](image/walking-dns-tree/6.png) <br>
Alright, so let's get started. Finding an IP address from a domain name works like a detective game with strict rules.<br>
![Network Image](image/walking-dns-tree/7.png) <br>

Domain names have labels separated by dots, and the recursive resolver must start by asking the root zone name servers. <br>
![Network Image](image/walking-dns-tree/8.png) <br>
We always begin at the root zone. Here, we ask for information about the domain name formed by the first immediate label to the left <br>
![Network Image](image/walking-dns-tree/9.png) <br>

which, relative to our current position in the DNS hierarchy, represents a subdomain of where we are.

For example, from root, com is a subdomain of root, <br>
![Network Image](image/walking-dns-tree/10.png) <br>
and from com, example would be a subdomain of com.<br>
![Network Image](image/walking-dns-tree/11.png) <br>
If the name servers are not the owners of this subdomain, they'll respond with, I don't own this domain, but here are the name servers that do, and by definition, this means we are moving forward to a different zone since ownership determines zone boundaries. <br>
![Network Image](image/walking-dns-tree/12.png) <br>
Then we ask these new name servers about the next label to the left, repeating this process of either getting direct information if they own the domain formed by that label, or being directed to different name servers if they don't, which means crossing another zone boundary.
![Network Image](image/walking-dns-tree/13.png) <br>

This traversal through zones, determined by domain ownership and authority, is why understanding delegation of authority in glue records becomes crucial, which we are going to cover next.<br>
![Network Image](image/walking-dns-tree/14.png) <br>
![Network Image](image/walking-dns-tree/15.png) <br>

But first, let's go over a few exercises of walking the DNS tree together to reinforce these concepts. Let's start with `engineer.kodekloud.com` since we are already familiarized with it.

Starting at the root zone, we ask for information about the domain name formed by the first immediate label to the left, which is `com`.<br>
![Network Image](image/walking-dns-tree/16.png) <br>

The root name servers are not the owners of this subdomain, so they respond with, I don't own this domain, but here are the name servers that do, and by definition, this means we are moving to a different zone. <br>
![Network Image](image/walking-dns-tree/17.png) <br>

Now we are at the com zone, and we ask for information about the domain name formed by the first immediate label to the left, which is `KodeKloud`. The com name servers are not the owners of this subdomain, so they respond with, I don't own this domain, but here are the name servers that do, and by definition, we are moving to a different zone.<br>
![Network Image](image/walking-dns-tree/18.png) <br>
![Network Image](image/walking-dns-tree/19.png) <br>

Now we are at the kodekloud.com zone, and we ask for information about the domain name formed by the first immediate label to the left, which is engineer. Since this is a subdomain that's part of their zone, they own it, they directly provide us with the IP address with no further zone transitions needed. <br>
![Network Image](image/walking-dns-tree/20.png) <br>

Now let's walk through `museum.co.uk`. Starting at the root zone, we ask for information about the domain name formed by the first immediate label to the left, which is uk. The root name servers are not the owners of this domain, so they respond with, I don't own this domain, but here are the name servers that do<br>
![Network Image](image/walking-dns-tree/21.png) <br>
and by definition, this means we are moving to a different zone. <br>
Now we are at the uk zone, and we ask for information about the domain name formed by the first immediate label to the left, which is co. Since co.uk is actually a subdomain that's part of the uk zone, they own it, we continue in the same zone. When we ask about museum, the uk name servers are not the owners of this subdomain, so they respond with, I don't own this domain, but here are the name servers that do. <br>
![Network Image](image/walking-dns-tree/22.png) <br>
and by definition, this means we are now moving to a different zone. Now we are at the museum.co.uk zone, and since we've reached our destination and they own it, they directly provide us with the IP address.<br>
![Network Image](image/walking-dns-tree/23.png) <br>

Finally, let's examine a domain I created. For this course called `jcroyowaun.io`. Keep in mind that depending on when you are taking this course, the domain may exist or not, but assume the explanations and command outputs were true at the moment of recording this video. For this exercise, we are going to use a subdomain of jcroyowaun.io called `staging.jcroyowaun.io`. <br>
![Network Image](image/walking-dns-tree/24.png) <br>

Starting at the root zone, we ask for information about the domain name formed by the first immediate label to the left, which is io. The root name servers are not the owners of this subdomain, so they respond with, I don't own this domain, but here are the name servers that do, and by definition, <br>
![Network Image](image/walking-dns-tree/25.png) <br>
this means we are moving to a different zone. <br>
![Network Image](image/walking-dns-tree/26.png) <br>
Now we are at the `jcroyowaun.io` zone, and we ask for information about the domain name formed by the first immediate label to the left, which is staging. The `jcroyowaun.io` name servers are not the owners of this subdomain, so they respond with, I don't own this domain, but here are the name servers that do,
![Network Image](image/walking-dns-tree/27.png) <br>

and by definition, this means we are moving to a different zone, <br>
![Network Image](image/walking-dns-tree/28.png) <br>
showing us that even subdomains can be delegated to different zones. Now we are at the staging.jcroyowaun.io zone, and since we've reached our destination, and they own it, they directly provide us with the IP address. <br>
![Network Image](image/walking-dns-tree/29.png) <br>

To illustrate these DNS tree traversal exercises, we used an online tool called `dnszones.dev`.<br>
![Network Image](image/walking-dns-tree/30.png) <br>
For general use cases, I would recommend using the command line. Running `dig +trace` will produce standard output of the DNS tree walking process. As seen in the animation on screen, running `dig + trace kodekloud.com`,<bt>
![Network Image](image/walking-dns-tree/31.png) <br>
the query starts by making a request to the root name servers. Our first response comes from `a.root-servers.net`, giving us the list of com name servers.<br>
![Network Image](image/walking-dns-tree/32.png) <br>
Then jtld-servers.net from the com zone responds with Cloudflare's name servers for kodekloud.com.<br>
![Network Image](image/walking-dns-tree/33.png) <br>
And finally, cheryl.ns.cloudflare.com provides us the actual IP addresses. We can see each response and who provided it right here in the output as we walk through the DNS tree.<br>
![Network Image](image/walking-dns-tree/34.png) <br>
**Please run this command multiple times to examine the output.**
![Network Image](image/walking-dns-tree/35.png) <br>
We may notice that we  get the answers from different name server each time, This is because DNS uses multiple servers at each level for redundancy and load balancing. Picking a different server each time makes sense for spreading the load more evenly to avoid overloading the infrastructure. <br>
![Network Image](image/walking-dns-tree/36.png) <br>
![Network Image](image/walking-dns-tree/37.png) <br>
![Network Image](image/walking-dns-tree/38.png) <br>

This exercise that we just went over is called walking the DNS tree. By walking the DNS tree, we reinforce the concept of how domain names are separated by an ownership and authority model called DNS zones. <br>
![Network Image](image/walking-dns-tree/39.png) <br>

When we see a subdomain with different NS records than its parent domain, we've found a delegation of authority. <br>
![Network Image](image/walking-dns-tree/40.png) <br>

Think of the delegation of authority like a ceremony where a subdomain is transferred to its own zone. This process is carried out by assigning new name servers to the subdomain.<br>
![Network Image](image/walking-dns-tree/41.png) <br>
while ensuring the parent domain keeps an identical copy of the subdomain NS records.<br>
![Network Image](image/walking-dns-tree/42.png) <br>
So we end up with identical NS records in both the parent and child zones.<br>
![Network Image](image/walking-dns-tree/43.png) <br>
But wait, this brings up an interesting question. **How can the DNS resolution process involve traversing through zones, when the zones use nameserver records which are formed of domain name?** <br>
![Network Image](image/walking-dns-tree/44.png) <br>
Remember that we mentioned earlier how resolving an IP address from a domain name is like a detective game with strict rules? Well, every actor in the DNS must adhere to these rules.<br>
![Network Image](image/walking-dns-tree/45.png) <br>

**How do we reach the root name servers in the first place?** <br>
**How do name servers find each other?** <br>

This is what we call the chicken-and-egg problem in DNS because it feels that we need DNS to use DNS. To resolve the chicken-and-egg problem, we have two solutions in place, each at a different level of the DNS system. <br>
![Network Image](image/walking-dns-tree/46.png) <br>

**Number one**, every recursive resolver comes pre-configured with a list of IP addresses for all the root name servers called root hints.<br>
![Network Image](image/walking-dns-tree/47.png) <br>

Since recursive resolvers are publicly accessible on the internet via their IP addresses, any client can send a query to a recursive resolver.<br>
![Network Image](image/walking-dns-tree/48.png) <br>

The recursive resolver then uses the root hints to contact the appropriate root name server and begin traversing the DNS hierarchy to resolve the requested domain name. <br>
![Network Image](image/walking-dns-tree/49.png) <br>

Number two, name servers from a parent zone may point to the exact location of the delegated child zone's name servers using a special record type called `glue records`.<br>
![Network Image](image/walking-dns-tree/50.png) <br>

Glue records are A or quad A records added to the parent zone's zone file to provide the IP addresses of the child zone's name servers.<br>
![Network Image](image/walking-dns-tree/51.png) <br>

For example, during the delegation of authority, when we're assigning new name servers to a child zone, we need to ensure that the parent zone maintains a copy of the child zone's NS records.<br>
![Network Image](image/walking-dns-tree/52.png) <br> 
![Network Image](image/walking-dns-tree/53.png) <br> 
 
We may also include glue records in the parent zone's zone file, providing the IPv4 and/or IPv6 addresses of the child zone's name servers. <br>
![Network Image](image/walking-dns-tree/54.png) <br>
This is an example of how the NS records and glue records for KodeKloud.com would look in the com zone file.<br>



All com name servers must have a copy of these records in their zone files. Now, as end users, we probably have multiple options to check the glue records, but the one that I'm comfortable with is using the dig command by querying an authoritative nameserver directly using the @ symbol and then adding then + additional flag as shown in the output display on screen.<br>
![Network Image](image/walking-dns-tree/55.png) <br>

In this command, we're directly querying the a.gtld-servers.net nameserver for the kodekloud.com domain. By using the +additional flag, we can see the additional section highlighted on screen, which shows all the A and AAAA records for the nameservers. These are what we call glue records.<br>
![Network Image](image/walking-dns-tree/56.png) <br>

Observe how we can modify dig's behavior and output by using different flags and even querying name servers directly using the @ symbol, basically ignoring the recursive resolver by talking directly to the name server. <br>
![Network Image](image/walking-dns-tree/57.png) <br>

I find it interesting to highlight that since we are querying the authoritative name server directly instead of letting the recursive resolver handle the query for us, we have a warning message saying recursion requested but not available. <br>
![Network Image](image/walking-dns-tree/58.png) <br>
This is because, as we'll learn in the DNS as a protocol section, DNS requests have a question section with flags and bits enabled that modify its behavior.

There's a recursion bit that's usually enabled, which means please follow the entire chain of DNS queries needed to resolve the name if you don't have the asewer. 
![Network Image](image/walking-dns-tree/59.png) <br>

But we are querying a nameserver directly. And nameservers are configured to not allow recursion even when asked. <br> 
![Network Image](image/walking-dns-tree/60.png) <br>
This is a safety measure to prevent the nameservers from being overwhelmed by recursive queries that would force them to perform lookups on behalf of any client that asks, which could lead to resource exhaustion and potential denial of service.<br>
![Network Image](image/walking-dns-tree/61.png) <br>
But wait, there is more information I want to give you because we’ve just started the happy path of walking the DNS tree where nameservers have glue records of the delegated nameservers to quickly point their locations.

Sometimes the nameservers of a parent domain won’t have the glue records with the IP addresses of the delegated child domain’s nameservers, as is the case in the command shown on screen.<br>
![Network Image](image/walking-dns-tree/62.png) <br>
In these cases, where glue records are not present to point the exact location of the delegated zone nameservers, <br>
![Network Image](image/walking-dns-tree/63.png) <br>
the only option to resolve the domain name is to walk the DNS tree all over again, which is a warranted way to complete the domain resolution process.<br>
![Network Image](image/walking-dns-tree/64.png) <br>

In a previous lecture, I think I called dig +trace as being a simulation of walking the DNS tree. <br>
![Network Image](image/walking-dns-tree/65.png) <br>

And while it may not be entirely accurate to call it a simulation, it's true that DIG + trace will omit some steps when dealing with out-of-the-ordinary circumstances, and the resolver will rely on its cached knowledge to resolve certain DNS queries.<br>
![Network Image](image/walking-dns-tree/66.png) <br>
I was very curious and I wanted to demonstrate this in the course when creating these lectures, so I tried using a trace command to examine the system calls made, when using the DIG + trace command.<br>
![Network Image](image/walking-dns-tree/67.png) <br>
![Network Image](image/walking-dns-tree/68.png) <br>
![Network Image](image/walking-dns-tree/69.png) <br>
![Network Image](image/walking-dns-tree/70.png) <br>
![Network Image](image/walking-dns-tree/71.png) <br>
![Network Image](image/walking-dns-tree/72.png) <br>
![Network Image](image/walking-dns-tree/73.png) <br>
![Network Image](image/walking-dns-tree/74.png) <br>
![Network Image](image/walking-dns-tree/75.png) <br>
This is the exact command that I used. Now, the output of this command is very detailed and verbose, but for simplicity, in this lecture, I'm placing the pieces that matter.

We see that after getting the AWS name server records from IO's name servers, instead of walking the DNS Tree again, the resolver, which is configured as the IP address 8.8.8.8, directly returns the IP address for these name servers from its cache.<br>
![Network Image](image/walking-dns-tree/76.png) <br>
From this output, we can infer that the normal DNS Tree walk, starting from the Root Zone and to dot IO name servers, uses the connect function. <br>
![Network Image](image/walking-dns-tree/77.png) <br>

This represents a true walk in the tree, where we request information from nameservers. But, When We need AWS name server IPs, it suddenly switches to the send to function, where it directly requests the resolver 8.8.8.8 for information. This shows we're abandoning the tree walk and relying on the resolver's cache, and that DIG plus trace isn't really doing the complete resolution process, as it relies on the resolver's cached knowledge when encountering certain circumstances. This caching mechanism is crucial for DNS performance, as we've learned in the previous lecture. <br>
![Network Image](image/walking-dns-tree/78.png) <br>

If you have a Linux machine, you can try this command. I would advise you to look for the connect and receive message and send to system calls when looking at the huge output.<br>
![Network Image](image/walking-dns-tree/79.png) <br>
All these command line techniques showcased in this lecture, including the use of the add symbol to communicate directly with the name servers instead of going through the resolvers, are especially useful when debugging and to compare if DNS records match between different name servers.<br>
![Network Image](image/walking-dns-tree/80.png) <br>
Because, as we’ll learn in the zone transfer lecture, name servers must maintain exact copies of DNS records.<br>
![Network Image](image/walking-dns-tree/81.png) <br>
Replication mechanisms built into DNS handle this synchronization, but common DNS issues can arise when name servers have different records due to failed updates or outdated information.<br>

So, to finish this lecture, let's close the last subtopic by stating that the A and AAAA records in name servers are called glue records because they're the glue that holds the DNS system together, breaking circular dependencies and making the whole system work. <br>
![Network Image](image/walking-dns-tree/82.png) <br>

These concepts, delegation of authority, and glue records are what make DNS a truly distributed system, where no single entity needs to manage the entire namespace and different organizations can manage their zones independently while still maintaining a cohesive global DNS system.<br>
![Network Image](image/walking-dns-tree/83.png) <br>

## Time to Live - TTL

One of the design goals of the DNS is that it needs to be fast. But how can it be fast when we have so many systems interacting with each other through network calls? <br>
![Network Image](image/ttl/1.png) <br>
The answer is that the **DNS uses caching mechanisms** to help with speed. I want to make a quick mention since we haven’t discussed RFCs yet. <br>
![Network Image](image/ttl/2.png) <br>

RFC 1034 Section 2.2, Design Goals, is where all this foundational information was documented since the 1980s. RFCs, which stands for Requests for Comments, are numbered documents that outline specifications, standards, and best practices related to Internet protocols and technologies. <br>

![Network Image](image/ttl/3.png) <br>
![Network Image](image/ttl/4.png) <br>

Since DNS is both a distributed system and a protocol, it has its own dedicated RFC.<br>
![Network Image](image/ttl/5.png) <br>

I highly suggest spending time to get comfortable with these documents or, at the very least, make a habit of fact-checking against these primary resources when learning or researching anything related to DNS or even other protocols with RFC document specifications.
[RFC Link](https://datatracker.ietf.org/doc/rfc1034#section-2.2)<br>

For those that are not very familiar with the concept of cache and caching, let’s think about it using our previous detective analogy.<br>

Imagine that every time one of the detectives resolves a case, he writes all the clues in his notebook. So, next time someone hires a detective to resolve a case he has already resolved, a.k.a. resolving a DNS query,<br>
![Network Image](image/ttl/6.png) <br>
The detective will have readily available information to provide an answer, without having to go through the whole process of walking the DNS Tree, asking the authoritative nameservers for answers. As you can imagine, accessing information from cache significantly reduces the load and traffic that the DNS infrastructure would otherwise go through, which contributes to making the DNS fast.<br>

Looking at the diagram presented on screen, we have a more accurate technical representation of many of the actors that play a role in the DNS resolution process, which is a way to evolve or elaborate further on our simple detective analogy that we’ve been using so far.<br>
![Network Image](image/ttl/7.png) <br>

This takes us towards a more technical mental model of how the DNS resolution process actually works. Going over the diagram, from the inside out, and I want you to pay attention to this as **this is very important**.<br>

Everything starts on our personal device, on the far left. Whether it's our computer, phone, smart TV, etc., any device capable of connecting to the internet will inherently be able to perform DNS queries and get responses. <br>

Going from left to right, you can see that an application or program within the device will make a DNS request, and then there's a stub resolver, which is a DNS client program that's built into most operating systems. In Linux systems, the stub resolvers can be traced by using the getaddrInfo() system call.<br>

Its main responsibility is to forward the request to a recursive resolver as it can't perform queries to the name servers directly.

But moving to the right, we have that before talking to any public recursive resolvers, we go through our router's resolver, which is often known as a forwarding resolver. <br>
![Network Image](image/ttl/8.png) <br>

After leaving our home network towards the internet, we then talk to a recursive resolver, a.k.a. the agents we've been using as examples throughout this section.<br>
![Network Image](image/ttl/9.png) <br>

And finally, we get to ask questions to the name servers, starting on the Root Zone and then to the Top-Level Domain, and then finally on the second, third, fourth-level domain, or whatever corresponds to the DNS query we are performing. <br>
![Network Image](image/ttl/10.png) <br>


The DNS is a concept called TTL, or Time-to-Live, which is a number that specifies how long a domain record will remain in cache before checking if there's been any update to the domain name.

A change can be anything from adding records like CNAME records, A records. changing the start of authority information, changing name servers, or even deleting the domain name.

Using a dig command to KodeKloud.com, we can observe a 300 number in the answer section next to the domain name.<br>
![Network Image](image/ttl/11.png) <br>

That 300 is the number of seconds that the DNS record is meant to be cached. Think about it like an expiration timer on a detective's notebook.

After 300 seconds, which is 5 minutes, the information is considered expired, and the detective needs to go through the process of asking the authoritative nameservers again.<br>
![Network Image](image/ttl/12.png) <br>
To get current information about the domain name. This TTL mechanism is important because if the TTL is too long, changes to the DNS records might take too long to propagate across the Internet. If it's too short, we may lose the performance benefits of caching, since resolvers need to query the authoritative nameservers more frequently.<br>
![Network Image](image/ttl/13.png) <br>

In our KodeKloud.com example, all three A records have the same TTL of 300 seconds, but different records for the same domain could have different TTL values, depending on how frequently the administrators expect those records to change. <br>
![Network Image](image/ttl/14.png) <br>

Now, in previous lectures, we've focused only on what happens on the public side of the DNS, meaning the recursive resolvers and nameservers. Now, we are evolving our mental model of this design by introducing some of the levels of detail of what happens in our private networks when we need to resolve DNS queries. <br>
![Network Image](image/ttl/15.png) <br>

The reason why we are introducing this evolved design in this lecture is because sometimes the TTL value specified in the DNS records is not honored by some applications.<br>
![Network Image](image/ttl/14.png) <br>

Caching is a relatively simple concept on the surface, but it can be complex when thinking about how multiple clients that participate in the DNS resolution process have different rules and cache implementations. <br>
![Network Image](image/ttl/16.png) <br>

Observing the diagram shown on the screen, you can see that within the device section, we have the operating system and then multiple soft classifications of entities, including applications, programs, or services running at the operating system level,<br>
![Network Image](image/ttl/17.png) <br>

meaning some programs or applications handle their cache independently to the TTL value from a DNS record. If you've ever been through a situation where you're pointing a domain name, for example, while also trying to access the same domain name through a browser and you get different responses, for example, ping response correctly or successfully, but the browser won’t resolve the domain name. This is why they both have their own timing for cache to expire. In one of the last lectures in this course, we discuss more on clearing DNS cache when resolving DNS issues

## Zone Transfer
In this video, I want to talk about a concept known as zone transfer, which is the mechanism that nameservers use to stay in sync. <br>
![Network Image](image/zone-transfer/1.png) <br>

Throughout this course, we've compared authoritative nameservers to a database in the sense that nameservers store data that can be queried, for which they will return a response.<br>
![Network Image](image/zone-transfer/2.png) <br>

Turns out that nameservers also follow system design philosophies similar to databases.<br>

The following concepts are all tied to the DNS design goals of being fast, reliable, fault-tolerant, and scalable.<br>
![Network Image](image/zone-transfer/3.png) <br>
In database system design, there's a concept called sharding, which can be explained as a way to split a large amount of data across multiple servers.<br>
![Network Image](image/zone-transfer/4.png) <br>
Instead of having one huge server trying to handle everything, we break the data into smaller pieces, and each server handles its own piece.

In DNS, this means splitting domain records across different zones.<br>
![Network Image](image/zone-transfer/5.png) <br>
Instead of one server holding all domain records for the entire Internet, the DNS splits domains into zones.<br>
![Network Image](image/zone-transfer/6.png) <br>
Each zone is managed by different nameservers.<br>
![Network Image](image/zone-transfer/7.png) <br>
For example, some nameservers only need to know about com domains.

while org nameservers handle org domains.<br>
![Network Image](image/zone-transfer/8.png) <br>
This sharding continues down. Amazon.com nameservers only need to handle amazon.com records, not walmart.com records.<br>
![Network Image](image/zone-transfer/9.png) <br>

This way, no single server needs to handle the entire internet's DNS traffic. So in other words, nameservers borrow from databases, not only from their purpose of providing answers to queries, but in their design as well.<br>
![Network Image](image/zone-transfer/10.png) <br>

When the datasets grow too large, it’s better if we split the data across multiple servers, as we do in the DNS.
![Network Image](image/zone-transfer/11.png) <br>
Each server handles just a portion of the data, making the system more manageable and faster. DNS works the same way, by sharding the domain namespace into zones, each managed by different nameservers.

Also, as we've mentioned earlier, in the DNS, there should be at least two or more nameservers assigned to a zone. This is for redundancy and availability.<br>
![Network Image](image/zone-transfer/12.png) <br>

Each zone has multiple nameservers, because if there were only one, and it failed, the entire domain would become unreachable.<br>
![Network Image](image/zone-transfer/13.png) <br>

By having nameservers in different networks and locations, the domain stays available even if an entire network region goes down.

Every zone must have multiple nameservers for redundancy. When a record needs to be updated, it first goes to the primary nameserver.<br>

Then, a replication mechanism called zone transfer ensures all other nameservers receive these updates.<br>
![Network Image](image/zone-transfer/14.png) <br>

A quick parenthesis, I recommend taking notes on what zone transfer means, as there is also something called domain transfer, and there’s another concept called delegation of authority, and they all mean different things.<br>
![Network Image](image/zone-transfer/15.png) <br>

Take notes on each, to keep their meanings well categorized.<br>
![Network Image](image/zone-transfer/16.png) <br>

Anyway, the nameservers follow a leader-follower architecture, and we can find out which one is the primary nameserver for a zone by checking the start of authority record. Using dig and requesting the NS records reveals all of the nameservers designated for that zone.<br>
![Network Image](image/zone-transfer/17.png) <br>

When we update a record in our zone, say for example, we change the A records to point our domain to a new IP address,
the data first goes into the primary nameserver. Then, the process of zone transfer will ensure the rest of the secondary nameservers stay in sync.<br>
![Network Image](image/zone-transfer/18.png) <br>

Modern DNS providers like Cloudflare and AWS Route 53 handle the zone transfer through their own proprietary mechanisms.
<br>
![Network Image](image/zone-transfer/19.png) <br>
When you update a DNS record, the nameservers quickly get the updated information, usually within seconds, and I would say, nowadays it’s just a given that this mechanism will work fine.

However, many DNS operators, especially those managing top-level domains like .com or .net, use traditional replication methods called AXFR and IXFR.

AXFR copies all zone data to a secondary nameserver. Think of it as the special agents sharing the full authoritative data, <br>
![Network Image](image/zone-transfer/20.png) <br>

like the complete case files, with other agents in their organization. When a new nameserver is added to the zone, it knows nothing. It needs a complete copy of all records. That’s when AXFR is used.

 In IXFR, the secondary nameserver actively checks with the primary nameserver. to see if anything has changed. It does this by looking at the zone's version number, called a serial number.

If the primary has a higher number, the secondary requests just the changes that happened since its last update. So it's a pull system.

The secondary nameserver requests the changes. The primary doesn't push them automatically. This is more efficient because each secondary can request updates on its own schedule, and only when it needs them. This is similar to how database replicas work. They periodically check the primary database for changes rather than pushing updates to every replica. <br>
![Network Image](image/zone-transfer/21.png) <br>
This course won't contain more details of AXFR and IXFR for now. But as a summary, remember that zone transfer refers to the process of replicating DNS records across nameservers. First, the records originate on the primary nameserver, and then the data is replicated to the others.

## Root Servers and Anycast

So far in this course, we've established that the domain resolution process starts on the root zone. Another detail we've uncovered through commands like dig +trace is that there are only 13 root name servers.<br>
![Network Image](image/root-server-anycast/1.png) <br>
 I promise you that we will explore why there are 13 root name servers later in the course, <br>
 ![Network Image](image/root-server-anycast/2.png) <br>
 but the focus of this demo is on understanding how these 13 servers manage to handle the entire Internet's DNS traffic without becoming overwhelmed. 

Think about this, 13 servers handling DNS queries from every single device connected to the Internet worldwide.<br>
![Network Image](image/root-server-anycast/3.png) <br>
 The numbers are massive when you think about all the queries happening every second. So how is it possible that only 13 root name servers are capable of handling so much load? The answer is that this is possible thanks to a network design called **Anycast**. What Anycast does is it allows multiple physical servers to share the same IP address. To show you exactly what I mean, I am going to open `rootservers.org` website


and then I'm going to zoom into a random location in the map. Probably Mexico because I'm from Mexico. And so in the central region, we have two locations with root servers, one in Mexico City and the other in Querétaro. If we click on Querétaro, we see that this geographical place hosts root name servers E, C, K, D, and F in a data center.

Clicking on Mexico City, we have E, E, I, F, and D. This is interesting that the E server appears twice in this region, right? Let's click on the server here and check that the IPv4 address begins with 192 and ends with 230.10. The other one over here is the same, and the one in Querétaro has the same exact IP address. If we compare the IPv6, we can see it matches as well. Same is true for the F server, and so on. If we zoom out, we can see that there are many data centers announced in this map. There are many more in the United States, and there are regions with more than a few root servers like this place here close to Washington.


If we check the IPs from any of the A records, they're all the same. Take a look. Now, to understand Anycast, think about it as a distributed system that allows multiple machines with the same IP addresses to share compute resources to help with a huge traffic load by strategically positioning the servers in multiple locations to also help find the nearest location.

We get to interact with a root nameserver based on proximity thanks to a network protocol called BGP, or Border Gateway Protocol, which uses an algorithm to decide the fastest route to an internet location based on multiple considerations. I highly suggest you go check on YouTube.

There are some very interesting videos on BGP that are worth checking as BGP is a very important concept. Anyway, that's it for this demo. In the next lecture, we will take a look at another DNS distributed design called GeoDNS. I want to put forward that Anycast and GeoDNS are different.

Anycast uses the closest proximity method through network routing, while GeoDNS makes routing decisions by looking at information like our subnet location to figure out where you are connceting from.





## GeoDNS
Throughout this section, we've explored the DNS resolution process, from nameservers managing different zones to resolvers acting as our DNS detectives caching results. But being that the Internet is a worldwide system serving billions of users, we're missing a crucial piece known as GeoDNS. GeoDNS is a technology that helps analyze the origin IP address of a DNS request to determine the user's location and route the request to the most appropriate server.

This service is provided by modern DNS providers like Cloudflare or Amazon's Route 53. GeoDNS implementations consider multiple factors, like geographical proximity,but also the status of the service you're being directed to. Let's examine these factors one by one. First, let's talk about geographical distribution. In global distributed systems, there's something called CDN, which means content delivery network. Think of a content delivery network as a McDonald's restaurant chain for a moment.



McDonald's doesn't have just one restaurant serving the entire world from one location. Instead, they have thousands of restaurants worldwide, each serving their local community. Similarly, companies like Akamai provide these content delivery network services, maintaining servers across the globe that store cached copies of frequently accessed content.

This infrastructure enables faster access to popular websites, applications, and services, regardless of where users are located. The second factor is server health and operational status.When you type an address like KodeKloud.com, GeoDNS ensures you won't be directed to a server that's down or malfunctioning, because it constantly performs health checks on all available servers. Even if you have a server physically close to the user, that server might be experiencing issues or could be under heavy load. In these cases, GeoDNS will route traffic to the next best available option.

It's like if your nearest McDonald's is temporarily closed for maintenance, you'd rather drive a bit further to get your meal than arrive at a closed restaurant. This ensures users are always directed to servers that are actually capable of handling their requests, maintaining service reliability and performance. Remember at the beginning of this section we explained that DNS is both a distributed system and a protocol. When we talk about the format of a DNS request or its response,

we're talking about the DNS protocol, and GeoDNS uses the structure of the DNS request to understand how to direct the traffic to the nearest infrastructure thanks to a special value that's included in the DNS requests. I want to make a parenthesis to say that, when DNS was created back in the day, the internet wasn't what it is today, but the people in charge of creating the DNS

decided it may be a good idea to keep some unused bits in its request-response structure in case things evolved. As the internet grew, an extension for the DNS protocol, known as EDNS, was created, and within these extensions, there's a value or field with information about something called the client subnet that tells nameservers where requests are coming from. This is crucial. Without this subnet information, a user in Thailand, for example,

might end up talking to resolvers from someplace in America, thus getting responses that aren’t optimized for his location. We'll examine DNS requests and responses in detail in the next section, but for now, understand that this extension was fundamental in making GeoDNS work effectively. It gives nameservers visibility into where queries truly originate, not just which resolver is asking. We have a lecture that talks about EDNS in the next section, but for now,


Let's imagine a person from Sweden wants to watch Netflix, so they type netflix.com. What happens here is that this request first hits their DNS resolver, which might be their ISP’s resolver, or possibly Google’s resolver, at 8.8.8.8. Thanks to that special value we talked about earlier in the DNS request,

Netflix’s nameservers can see this request is coming from a Swedish network. Now, Netflix has multiple servers across Europe. They might have some in Stockholm, some in Amsterdam, and others in Frankfurt. When their GeoDNS system sees this request coming from Sweden, it doesn’t just automatically pick the Stockholm servers because they’re closest. Instead, it looks at several things. First, it checks which of these European servers currently have capacity to handle more streaming.

Then it looks at which ones have good network conditions. Maybe the Stockholm servers are having some network congestion right now. It also checks which servers already have the most popular Swedish content cached and ready to serve. GeoDNS uses a load balancing strategy to make these decisions of which server may give the best streaming experience at the moment. I wanted to make sure we covered GeoDNS as Its very Import in todays internet.


# DNS as a Protocol

## DNS as a Protocol
DNS as a protocol is about understanding the format of the requests, the responses, and other rules and nuances around the way DNS behaves. A good mental model to learn these concepts is that DNS is a network protocol. As you may know, the word protocol is used to define rules and contracts for an entity to follow. In computer networking, we have multiple protocols like TCP or UDP, which help define standards of how a device should communicate with another device.

It's like establishing a mutual set of rules so network-connected devices can know what type of data to expect and how to respond to said data. For me, it was a big help to understand that. In DNS, everything runs either in TCP or UDP, so keep this in mind when thinking about DNS. Now, in relation to network protocols, in case you’re not very familiar with it, I want to establish that protocols have hierarchies, meaning some can be a lower level


and others can use the previous rules set by another protocol to add an additional functionality or behavior to the communication contract. These higher-level protocols build upon the basic transport mechanisms to provide specialized services for specific use cases. To better understand these protocol hierarchies, let's start with the basics. At the foundation, we have IP for routing data across the Internet. This means that for any Internet communication to happen,

IP addresses need to be involved to know where to send data. IP works with transport protocols like TCP and UDP for actually sending that data. Think of it like different delivery methods. TCP is like sending packets where the delivery service waits for the recipient to sign and confirm they got each packet before sending the next one, whereas UDP is more like throwing all the packets into the recipient's yard at once, not caring if they actually got them all. It's crucial to understand the differences between TCP and UDP, as both are foundational protocols for network communication,

so I’ll elaborate more on the explanation before moving on. The TCP way of doing things is achieved through packet IDs and acknowledgments.

When sending data over the Internet, if the data is larger than what can fit in a single packet, TCP divides it into smaller packets, each with an ID so they can be put back together in the right order. While TCP packets can theoretically be up to 65,535 bytes, in practice they’re usually limited to around 1,500 bytes because of something called MTU, Maximum Transmission Unit, which is basically how much data Ethernet networks can handle in a single frame. If the data is small enough to fit in one packet, it’ll just send it as is, but TCP still uses what we call an ACK, or acknowledgment, to confirm the data made it to its destination. This acknowledgment system is what makes TCP reliable. The sender knows for sure if their data arrived.

Otherwise, the file won't open, as bits of its data may be missing or incorrect. UDP, on the other hand, just sends data packets

without waiting for any confirmation that they arrived. The receiver just processes packets as they arrive, in whatever order they come in.

This makes UDP much faster than TCP but less reliable. UDP is used for live streaming and gaming, for example,

where speed matters more than perfect delivery. If you miss a few frames in a video call or a game, the stream just continues and you might see a brief freeze. But as the transmission is live, it can't really wait for things to be acknowledged. Originally, DNS was designed to use UDP with a strict 512-byte limit for its packets. This limit wasn't random. It was chosen because the IPv4 standard specified that


every host must be able to handle packets of 576 bytes or less. Since IP headers could be up to 60 bytes and UDP headers were 8 bytes, staying under 512 bytes for the actual DNS data meant the total packet would always fit. Remember how in a previous lecture we talked about DNS having exactly 13 root servers? Well, this is exactly why. It's the maximum number that could fit in a single 512-byte response. This is because the server name itself would add about 20 bytes, times 13.

This means 260 bytes just for the names. So considering the rest of the fields displayed on the screen, this makes up for about a total of 512 bytes. These days we have something called extended DNS, which we will cover in another video. But this extended DNS capability enables handling much larger UDP packets, which makes sense since modern networks and computers can easily handle bigger packets now. We're not in the 1980s anymore.

Plus, we needed this capability because of other newer features like DNSSEC, which have been included in the DNS protocol in an attempt to make the DNS more secure. These security features add more information to DNS responses, making them naturally bigger than 512 bytes. We'll go over the basics of DNSSEC in another video in this section.

The only downside is that this ability to send larger responses has made DNS servers attractive for amplification attacks, where bad actors can use DNS to generate a lot of traffic.

But anyway, the key point here is that these basic protocols provide different ways to move information, and other protocols can build on top of them to add their own rules and features. Now, when talking about how protocols stack, or sit on top of each other, think about the following. We just defined that TCP and UDP are two protocols that use IP addressing and routing to operate. As technologies evolve, new requirements emerge for how devices and software need to communicate. I'm going to use HTTP as an example since we interact with it everyday and I'm sure you've seen a 404 error when a page doesn't exist, or a 504 when a server is too busy.

These status codes are part of how HTTP standardizes communication, which will help us understand how DNS also standardizes its own way of handling requests and responses. So, HTTP is a protocol that builds on top of TCP. This means it has all the reliable delivery features of TCP, but adds its own specific rules about how to make requests and receive responses. Think about this as a way to solve new challenges that came up as the web evolved.

For example, a basic TCP packet requires source and destination ports, sequence numbers, and checksums for verification. The response includes acknowledgment numbers and flags to indicate the status of the connection.
HTTP adds more guidelines to follow on top of the existing TCP/IP. For example, it requires headers in the request to tell the server important information.

like what website you're trying to reach, what type of content you'll accept as a response, or what browser you're using.
It also has standardized response codes like the 404 and 504 we talked about earlier. These codes are part of HTTP's standard way of communicating,
so applications, devices, or people using the service know how to send requests and how to interpret a response. DNS works similarly in this hierarchy.

It's also a protocol with its own standards for requests and responses, though, as we mentioned before, it typically uses UDP instead of TCP.
This is because DNS was designed for quick, simple lookups where speed matters more than guaranteed delivery. DNS uses port 53 by default.
There's also port 853, which is used for DNS over TLS. TLS, or Transport Layer Security, is a protocol that adds encryption to network communication.


Think of it like a secure tunnel where data can't be seen or modified by others while it's traveling through the Internet. This is the same technology used when you see HTTPS in your browser, but applied to DNS queries to keep them private and secure. There are actually a couple of ways to do secure DNS.

 DNS over TLS, otherwise known as DoT, and DNS over HTTPS, known as DoH. They both encrypt DNS traffic, but work a bit differently, for which we have a video in this section. So, when using DoT or DoH, DNS uses the TCP protocol. In most other cases, it uses UDP by default, but DNS also falls back to TCP in a couple of interesting situations.

 Remember how we talked about that 512 byte UDP limit? Well, when a DNS response is bigger than that limit, and the client hasn't told the server it can handle bigger responses through extended DNS capabilities in its request, which is done by setting a flag in the DNS query options, the server will send back a truncated response indicating that the answer is too big for UDP. When this happens, the client knows it needs to try again, using TCP instead.
 
  DNS also uses TCP for zone transfers, which we learned in the previous section when explaining how DNS nameservers use a leader-follower architecture, where a primary nameserver replicates domain name updates to secondary servers. If some of these concepts like extended DNS capabilities and flags seem a bit complex right now, don't worry, we're just getting a high-level view. We'll dive into the specifics of DNS requests and responses, their flags, and options later in this section. Now that we're going over DNS as a protocol, and we also talked in the previous section about DNS from a distributed system perspective, I hope you see why DNS is probably more complex than, say, HTTP. DNS is a protocol that requires a complex global distributed system to be in place to operate. It's not just about learning networking basics.

  there's also the system design aspect, global internet routing, and concepts from high-performance databases like sharding to spread data across multiple servers, which is similar to how DNS uses multiple nameservers to distribute the load efficiently. So I hope you feel proud of making it this far in the course, and I hope you're learning a lot from this experience. Quick note about where DNS sits in the OSI model. It operates in layer 7, the application layer, while TCP and UDP are down in layer 4, the transport layer. We won't really go into the OSI model in this course, but thought it was an interesting mention in case you're already familiar. In our next video, we're going to look at how a DNS request and response is formed so we can understand dig outputs better.


  ## DNS Request and Response
  Every time we attempt to resolve a domain name, a DNS request with a query is initiated. We get an answer to the query from one of the components of the DNS system, either from the caching layer or, if needed, by an authoritative nameserver which, as we've learned in previous lectures, is reached by walking the DNS tree, starting at the root zone. The communication around resolving a domain name involves a two-way process. A request with a question initiated by the client. A response with an answer from a DNS system component. Both the question and the response are carried in a standard format called a message, as defined in RFC 1035 section 4.1. The message in the DNS is divided into five sections. The message has the same sections and resource records in both the DNS request and the DNS response. Each will interact with specific sections of the message. For example, a DNS request will populate fields in the question section with information about the desired operation.

  An example of data populated in the question section by a request is a domain name that we are looking to resolve. The DNS response may populate fields in the answer and authority section. The header section and the additional section may be populated by the request and the response to reflect different aspects of the operation and its outcome. Depending on how we perform a DNS query, the message may be transported by UDP, TCP, HTTP, or other protocols. The protocol used to send a query may change how the message is transported to the system responsible for handling the response, but the message will keep the same resource record structure intact regardless. For example, a traditional query using dig may use UDP or TCP to transmit the data in plain text. In most cases, a single UDP packet can fit the entire message containing both the request and response data. A fallback to TCP occurs when the message exceeds the capacity of a single UDP packet.


A large response is the most common cause of this. When the message travels through HTTPS or TLS, it encrypts the data in transit. The data is decrypted by the DoH-DoT resolver to perform the DNS lookup with traditional unencrypted DNS servers. Then it’s re-encrypted for the return trip to the client, where it is finally decrypted back to plaintext. Let's examine the message format starting on the header. Since we're familiarized with dig command's output from the lab exercises, I’m going to have a simple dig output to match each section of the DNS message with the corresponding part of the output when appropriate. The DNS message header is 12 bytes long, comprising the following fields. The ID field is an integer number in the DNS header used to track which response matches to which query. When a client sends a DNS query, it generates this ID, and the server copies the same ID in a response.

This matching mechanism exists because DNS uses UDP primarily, which has no built-in way to track related packets, and messages were meant to fit in a single packet. While TCP and HTTP have their own packet tracking capabilities, DNS continues to use this ID field regardless, since it works effectively and it maintains backwards compatibility with the original design. The row below is known as the flags row. Like other command-line programs, the flags section stores information that modifies how the query will be performed. In the flags row, we first have the QR that indicates whether the DNS request is a query with a number 0 or a response with a number 1. The output of a dig command will have a 1, as this field gets populated last by a response. Opcode is a value that specifies what type of query is included in this message. This value is set by the originator of a query. There are different values that can go in this flag, but the only important one to learn is 0 for standard query.

Number 1 and number 2 are either deprecated or never implemented. Numbers 3 to 15 are reserved for a future use case if someone comes up with a good use case for them. AA stands for authoritative answer. This flag will be populated if the response is sent by an authoritative nameserver. For example, when using dig and the ADD symbol to send a query to a nameserver directly, the flag will be present in the header like the sample shown on screen. TC is a flag that indicates when a DNS message had to be truncated due to its length not fitting in a single UDP packet. When a DNS response is too large for UDP, the server cuts off the response, essentially sending an incomplete answer. Then it sets the TC flag to 1. The client sees that TC equals 1 and knows, hey, I didn’t get a full answer. So the client then makes the exact same query again, but using TCP instead of UDP. Next we have the RD and RA bits, which stand for recursion desired and recursion available.

The client sends a query with a recursion desired to indicate that it wants the resolver to get back to it until it has a response. The client disengages from having to deal with walking the DNS Tree, making multiple queries, handling referrals, or talking to different authoritative nameservers. The resolvers are called recursive resolvers as they're able to perform the entire DNS resolution process on behalf of the client. The resolver first checks its own cache, and if it can't find the answer, it will begin walking the DNS Tree. This process is called an iterative query because the resolver iterates through the DNS hierarchy, making a series of independent queries to different nameservers, similar to a for loop in programming. The RA, or recursion available, is a bit set by the response, and it indicates if performing a recursive query is possible or not. When using the dig command with an add symbol to query an authoritative nameserver directly, the recursion available bit is set to false.


This is a safety measure to prevent the nameservers from being overwhelmed by recursive queries that would force them to perform lookups on behalf of any client that asks, which could lead to resource exhaustion and potential denial of service. The Z flag is reserved for future use. Lastly, the R code is a response code which indicates if the query was successful or not. I think the most important ones to mention are that 0 means success, and 3 is for a non-existent domain. The R code can have a value from 0 to 15. On screen we have samples of why the rest may appear. Now moving down in the header section we have Qd count, which means question count, and it indicates how many questions are in the request section. In most common DNS queries the value will be 1. At first it was thought that the DNS protocol would be able to query multiple domain names in a single request.

For example, in KodeKloud.com we get 3 A records, so the AN count is 3. NS count is a field populated by a response, with a number of nameserver records in the authority section, which we will talk about in a second. This value cannot be seen directly using dig, which shows authority instead. To see the raw NS count value you would need a packet capture tool like TCPDump or Wireshark, which we will learn more about in a future lecture. R count is the additional count, showing how many records are in the additional section. This section often contains supplementary information like Glue Records. The next section of the DNS message is the question section. This section contains data about the query we are sending in a DNS message.

In the resource record structure we first have a QName, which means a query name. When performing a DNS query, the domain name we are requesting to get resolved will be added in the QName field. The QType field indicates what type of DNS records we are querying for. When using dig without specifying a record type, it defaults to querying for an A record, but it can be CNAME, AAAA record, MX record, etc. The QClass field specifies the class for the query, which will almost always be of type 1 or IN for Internet class, which is why when querying for India's top-level domain record, we need to use a fully qualified domain name by including the dot at the end. Moving down to the answer section. The answer section is populated in the message by the component of the DNS system responsible for sending the response. The first resource record we have is a name. This is a domain name that was queried in the question section.

Then we have the type, and the type indicates what type of record has been sent to the response, for example an A record, AAAA record, and so on.

RDLength means resource data length, and it will be different depending on the records contained in the response. For example, an A record will have an RDLength of 4 bytes, and a AAAA record of 16 bytes, because they're longer. TTL is a time-to-live value in seconds that indicates how long this record can be cached. In the class record, we will almost always have type 1 for IN, or Internet class.

It will have the same values in the QClass record from the question section. The authority section contains resource records with the same structure that's in the answer section. We have name, type, class, TTL, RDLength, and RData. This section is typically populated when asking a nameserver to resolve a domain name that they can have a final authoritative answer for, for example, asking root nameservers about the top-level domain, or asking the com nameservers about cultglan.com second-level domain. The additional section contains the same resource record structure as the answer and authority sections.

Despite having the same structure, the additional section populates data differently. As the Internet grew larger, new requirements for the DNS protocol emerged, and the additional section was found to be useful because it had some free bytes capable of storing more data in a DNS message while keeping its structure the same. So, OPT records that help add new functionality to DNS without breaking backwards compatibility were added here. For example, fields like name, type, class, and TTL are already present in the authoritative sections. At first, having them in the additional section seemed like a good idea, but then it was found to be redundant since it didn’t really provide any additional value. In consequence, the designers of the DNS cleverly reused the existing fields for new purposes. Think about this as how you might repurpose a drawer in your closet. While all drawers were originally designed to store folded clothes in the same way, you might realize one drawer could be better used by adding dividers or labels to store socks and accessories differently.

The additional section does provide certain types of records with supplementary information that might be helpful in a DNS response. For example, you may use the +additional flag to see additional records that may be omitted in the default output.

For example, when checking for Glue Records or when querying NS records outside of your current resolution chain. Therefore, the additional section still has basic use cases for the RDATA and RDLENGTH fields. The rdata will contain the key value pairs with data from an additional response, and rdlength will be the length of the data provided in the rdata record.

In the next section, we will elaborate more on the additional section and the OPT records that offer extended DNS capabilities.

## Extended DNS (EDNS)

When EDNS was first created in the 1980s, the original specifications were thought out to work well with the hardware limitations of the era. Some of the limitations were UDP message size limited to 512 bytes, limited response codes, only 4 bits were allocated for this, allowing responses with values from 0 to 15. DNS clients and servers had no way of communicating if either side was operating on their newer capabilities or not. As networks and computers evolved, it made sense to make DNS evolve along to stay relevant. Unfortunately, changing a protocol that’s essentially the backbone of the Internet offers significant challenges, as it risks breaking compatibility with existing systems. This challenge was solved by repurposing the additional section in the DNS message resource record structure by providing a space to store new functionality. The additional section has these resource record types name, type, class, TTL, RD length, RData. To enable extension mechanisms while maintaining compatibility with standard resource records, a new concept called pseudo resource records was introduced, allowing different interpretations of these fields while using the same structure. Taking a look at the additional section of a DNS response, I'll explain how the resource record fields are repurposed despite having the same names. The name field has an empty root domain, whereas in the answer section it contains a domain name that was included in the original request. On the type, this is where the OPT record goes. Its value is 41 and its presence in a DNS request indicates that extended capabilities are being requested. The class field is used to indicate UDP payload size. Now UDP packets can be larger in size, thanks to this part, which I'll explain in a moment.

The TTL field is now repurposed with an EDNS flag and version made to extend DNS functionality. The current version is 0 and it's the only stable version that’s been widely adopted. Higher version numbers are reserved for future use. Extended response codes, numbers 16 and upwards. 
 
Remember we said that R codes are from 0 to 5 and then 6 to 15 are unused. Now we have numbers from 16 and upwards in case they’re ever needed for something. There’s a do bit for DNSSEC, which we’ll talk about in the next video. The R data field contains EDNS options and it will also contain the key value per data if there are records in the additional section of the response. The RD length that contains the length of a response contained in the additional section. By using OPT records, we signal EDNS capabilities. This way DNS can evolve and add new features while staying backwards compatible, all without needing to create a DNS 2.0. Since 2013, EDNS support by the DNS Infrastructure, such as resolvers and nameservers, is now mandatory. So if an OPT record is present in a received request, a compliant responder must include an OPT record in their respective responses. The OPT pseudo section can be spotted in the dig command. When you see additional 1 in the header, this is often the OPT record indicating EDNS support. Some other things that EDNS enables are extended response codes, starting from 16 and upwards. DNS security extensions, such as DNSSEC, which is covered in this section. Client subnet information for CDN optimization. 
 
Remember we talked about this in the GeoDNS section, where we mentioned how there are architectures like content delivery networks that offer multiple edge locations, serving cached data from a service, such as Netflix, with the purpose of helping performance and how these decisions will be made based on a location. Larger UDP.

Messages, up to 4096 bytes commonly. Thanks to EDNS, the UDP packet size limit of 512 bytes can now be negotiated to avoid TCP fallback. In the original DNS implementation, if the server response was larger than the 512 bytes, the DNS message had to be truncated by setting the TC flag to 1, which would force it to retry the exact same query one more time, but the second time using TCP instead of UDP. When EDNS is enabled, the client can say, I support bigger UDP sizes, like 4096 for example, so the server can send bigger UDP responses without TCP fallback, and it will only fall back into TCP if the response exceeds the 4096 size. For instance, when preparing the lab exercises for the core section, I tried looking for a sample where a response would be bigger than the 4096 byte limit to give an example of a TCP fallback, but I couldn't find a reliable option suitable for the lab environment. Something technical to keep in mind is that, for performance reasons, RFC 6891 specifies that the UDP payload size, with values over 512 bytes, must be treated as 512. The 4096 limit is recommended as a good compromise between size and reliability, as allowing higher values could create opportunities for malicious attacks.


 ## DoH, DoT and DNSSEC

DNS queries will carry a message transported through the network, generally with UDP or TCP, but other protocols are available too, such as HTTP. By default, UDP and TCP use port 53 for transporting the message, and both UDP and TCP transmit the data unencrypted. Other common and important DNS transfer protocols are DoH, which is DNS over HTTPS, and DoT, which stands for DNS over TLS.
 
Both these protocols offer mechanisms to encrypt the DNS queries in transit. A DoT or DoH query needs to be sent to a resolver capable of understanding the request in this format. The data is decrypted by the resolver to perform the DNS lookup with traditional, unencrypted DNS servers, then re-encrypted for the return trip to the client, where it is finally decrypted back to plain text. For example, Cloudflare offers a DoH endpoint shown on screen. DNSzones.dev, the web application we use in the Walking the DNS Tree lecture, uses this Cloudflare's resolver endpoint. If we make queries over DoH in the command line, we may use a command line program capable of making HTTP requests, such as cURL.
 
This would be the equivalent of using dig but for DNS over HTTPS instead of plain UDP or TCP. Now, besides the transfer protocols, I want to cover DNSSEC in this lecture as well. DNSSEC stands for Domain Name System Security Extensions, and, while it also incorporates cryptographic mechanisms in the DNS, it's actually a completely different thing than DoT or DoH. When talking about DoT and DoH, we are talking about the transport protocol that will be used to send DNS queries and get the responses across the network. We just saw an example of how DoH use HTTPS, and therefore, it requires HTTP headers in the request.

It will also use HTTPS encryption mechanisms like SSL or TLS to secure the data in transit between the client and the DNS resolver. DNSSEC is about including additional security records in the DNS responses that can only be cryptographically signed by legitimate components in the DNS system, such as a recursive resolver or an authoritative nameserver with the appropriate cryptographic keys. The process goes as follows. A client initiates a DNS query, and the query may include an OPT record in the additional section. The OPT record signals a request for DNSSEC data. If the query domain has DNSSEC enabled, the client sets the DNSSEC OK bits in the OPT record to indicate that it wants DNSSEC data in the response.

The resolvers involved in the query resolution process must have the appropriate public keys to validate DNS signatures in the response. Then, we also have the root and top-level domain key signing ceremonies as part of the process. The public key is used to validate that root and the TLD DNSSEC signatures are managed through a key signing ceremony. These ceremonies are performed by a group of trusted experts who follow strict security measures to generate and store the keys securely. The ceremonies are often recorded and published for transparency. you can find videos of DNS key signing ceremonies on YouTube. 

The purpose of DNSSEC is to prevent attacks where a malicious actor would spoof DNS responses and provide fake or misleading information. This type of attack is known as DNS spoofing or cache poisoning. By implementing DNSSEC, we have a higher level of assurance that the authoritative answer of the query can only be provided by legitimate servers with the appropriate cryptographic keys. DNS messages with DNSSEC enabled will have a larger size due to the extra data involving the keys. When using the DIG command, you can include the PLUS DNSSEC flag. This flag sets a DNSSEC OK bit in the OPT record of the DNS query, indicating that the client is interested in receiving DNSSEC-related records. The flag has a negotiation mechanism. PLOS Node DNSSEC, for example, will perform the query without requesting the DNSSEC records. In AWS Route 53, for example, there is an option to create a hosted zone with DNSSEC enabled when registering a domain.

This feature automates the process of generating and managing DNSSEC keys for your domain. The process of adding DNSSEC keys to your domain involves the following steps. The first thing is key generation. DNSSEC keys are generated for your domain, and these keys are used to digitally sign your DNS data. The second is the key publication, so the public part of the key is published in your DNS zone as a DNS key record. This allows other DNS servers to verify the signatures of your DNS data. Then you have the data signing, so your DNS data, or the resource records, are digitally signed using the zone signing key. The signatures are published in your DNS zone using RRSIG records. Then you have the parent zone interaction, so your domain's parent zone, or the top-level domain, is notified of your DNSSEC keys. This establishes a chain of trust from the roots to your domain. When DNSSEC is enabled for your domain, DNS responses from your domain will include the RRSIG records, which are the digital signatures that authenticate the DNS data.

Resolvers that support DNSSEC will validate these signatures to ensure that the data hasn't been tampered with, and that it originates from a legitimate resource. If the validation succeeds, the resolver knows it can trust the DNS data. If the validation fails, the resolver will treat the response as untrusted and may not return the data back to the client. The DNSSEC topic is vast and would require significant time to get into explaining depth, especially when you get into the technical aspects like the key management and the cryptographic algorithms. I would encourage you to request more information on this topic to be included in the course if it’s within your interests. A summary of this lecture is that the DoT and DoH are protocols used to securely transport DNS messages, and that DNSSEC, on the other hand, is an extension of the DNS protocol that incorporates cryptographic signatures to ensure the authenticity and integrity of DNS responses, protecting against DNS spoofing attacks.

# Record Types
## DNS Record Types- Introduction
This part of the course is, for the most part, a practical learn-by-doing section where we will learn some of the common DNS records by actually implementing them in a BIND9 server.

For the demo videos, we are going to have two machines, Node-01 and Node-02. On Node-01, we will set up and configure our BIND9 DNS server.

On Node-02, we will install a web server that we'll use to demonstrate how DNS resolution works in practice. This two-machine setup will help us understand how DNS servers and services work together in the real world. The DNS server we are configuring locally will be able to answer DNS queries but it will not be exposed to the internet. The fundamentals of DNS are the same, minus the distributed system remote communications, but I think having a local server to experiment freely without worrying about breaking anything in production helps a lot.

Alright, let's jump into installing and configuring our DNS server. First thing we need to do is get BIND9 up and running. So I'm going to run this: <br>
`sudo apt update && sudo apt install bind9 bind9utils bind9-doc -y`<br
command. Ok, so it’s installed. Let’s check if the service is running. The service is not running, so let’s start it. Checking the status again. Perfect, now the service is running.

## SOA and NS Records
Now that we have our DNS service running, we want to create a zone called my.kodekloudlab.com, and here’s where things get interesting. To create a zone, we first need to modify a BIND9 configuration file to let our service know how many zones we are going to have configured in this server, and where to find each zone file. For this demo, we are configuring just one zone file and the configuration file to indicate this zone file is in the etc BIND9 directory, and the file name is named.conf.local. So I’m going to edit this file using vim. See that it has some comments pre-populated by default? I’m going to get rid of the contents of the file by entering vim command mode by typing a colon, and then the following command. One, and then a comma, and then dollar symbol, then D, and then I’m going to press enter, and the contents are gone. Now, first thing I’m going to do is I’m going to type the zone name, which will be `my.kodekloud.com`.

Inside of the curly braces, there will be two arguments here. The type and the location of the zone file we will be configuring next. The type we are picking indicates that this is a primary DNS server for this zone. Remember, in DNS, there should always be two nameservers for redundancy, but for simplicity in this exercise, we are configuring just one. Okay, so we have the file. Let's save it. Okay, now that it's saved, let's create the zone file.

The zone file is also in the etc bind directory, but the name of the zone file, by convention, will start with DB, and then dot, and then our domain apex that indicates the start of the zone. In this case, my.kodekloudlab.com. We will populate our zone file with some mandatory values first. The TTL 300 sets the default time to live in seconds for every record in the zone, telling resolvers how long to cache responses.

Now on to the start of authority record, or SOA. This at symbol to the left of the SOA record represents the zone's apex domain in the syntax, so we are saying that my.kodekloudlab.com has an SOA record of ns1.my.kodekloudlab.com. So this line defines the start of authority record, specifying that ns1.kodekloudlab.com is the primary name server for this zone. The second field, admin.my.kodekloudlab.com, is actually an email address with the at symbol replaced by a dot, so if it were a normal email, it would be admin@my.kodekloudlab.com. That's how SOA records store contact information in the zone files.

The numbers in parentheses are the serial number which increments with each zone file change. Hopefully, I'll remember to increment the number every time we make a change to the zone file during this demo. The refresh interval means how often secondary DNS servers will check for updates. The retry interval is how long they wait to try again if the refresh fails.

The expire interval is when secondary servers should discard the data if no successful refresh occurs. And the negative caching TTL is for how long resolvers will cache a nonexistent domain or other negative responses.

So for example, if there's a domain that didn't exist and this value is set for, let's say, 5 hours, and then you register that domain just 5 minutes after, it may take the full 5 hours until a resolver will attempt to check if this domain exists again.

And we have a lecture about negative caching in TTL where we explain this more in depth. So this whole block is the SOA record.

Now we need the NS records. For this, we use the add symbol again to indicate the APEX domain again, followed by the IN NS and the hostname of the nameserver. This tells resolvers that ns1.kodekloudlab.com is the authoritative name server for this zone. This is meant to help queries arrive at the correct destination, which is the name server, with the authority to give answers for this zone's domain name.

This NS record in combination with the SOA completes the definition of which server holds the authoritative data for my.kodekloudlab.com.

So this SOA and NS records along with the TTL gives us the basic framework for our DNS zone file.

So now we save the file and exit. Now, even though this gives us the basic framework for our DNS zone file, if we query the domain,

for example using dig pointing to the localhost because here's where the nameserver is, and then my.kodekloudlab.com, it won't respond fine because the nameserver we declared doesn't yet have a glue record pointing to an actual IP.

This causes a query to get lost since it doesn't know where to find the ns1.kodekloudlab.com name server. In the next lecture, we'll see how to add the glue record ensuring the name server can be found and our local DNS server will respond correctly after this.

## Glue Records
Ok, so we are trying to reach our nameserver but the query is getting lost. We need a glue record to give our dig command the nameserver's IP address so it knows exactly where to go and how to find the nameserver.

Let's edit the zone file again. So we are going to add this line. This line tells DNS that our nameserver, which is ns1.microcloudlab.com, is at 127.0.0.1.

Remember, this only works if we query from node-01 because 127.0.0.1 is the local loopback IP address. In a real setup, you'd need to use a valid IP address for your nameserver.

We should also increment the SOA Serial to 2, or any higher number than what it currently has since we changed the zone file, ok?

Let's see if we keep remembering this as we keep adding changes. Ok, so we are going to reload by 9.

Now let's run our query. This time it returns no error instead of the NXDOMAIN, proving the Glue Records is working.

## A and AAAA Records
Okay, so this video is about the A and AAAA records. In this demo, we are just going to configure the A records.

AAAA records is essentially the same, but with an IPv6 IP address. As covered earlier, an A record maps domain names to IPv4 addresses, while the AAAA record maps domain names to IPv6 addresses. In DNS packets, an A record's address field is 4 bytes long, whereas a Quad A record's address field is 16 bytes, and the packet's header includes flags identifying each record type. Okay, so let's find the IP address for node 02, so that we can add the A record.

So I'm pinging node 02 to see what the IP address is, it's going to be different for each playground session.

Okay, so this is the IPv4 address, I'm copying it, and now I'm going to edit the zone file again.

Let's add this line at the bottom that maps the node 02 host to its IP address. Now let's restart BIND9.

Let's try it out like this, since we are specifying that the A record belongs to a node 02, it has been taken as a subdomain, we can see that it's working. However, thinking about it, I think we shouldn't create this in a subdomain format.

Ideally, we want our Apex domain, in this case, my.kodekloudlab.com, to have a mapping to node 02 host, because next we intend on deploying a web server there, and it'll be nice if we can just hit the domain Apex and be able to consume the service exposed by the web server.

To do this, we use the at symbol instead of the node 02 to indicate that we want our Apex domain to respond with the A record when queried. Ok, so we are going to restart by BIND9 again, and let's try the query to the Apex domain.

Ok, so it's working. Configuring the AAAA record involves the same exact steps, but I'll skip it due to virtual environment constraints.

Now we have a clear mental map of how a nameserver resolves the IP address of a machine by resolving its domain name, Next we are going to configure the CNAME record.


## CNAME Records

Okay, so this is my favorite part. We are going to configure a CNAME record in this video. And so, basically, CNAMEs are short for canonical name.

And they're a type of record that points to another domain name. Meaning, CNAMEs cannot point to other IP addresses, for example.

Also, CNAMEs cannot be used to point to the apex domain. It needs to be something different. CNAMEs are often used for www prefixes to indicate that the IP address that the domain name is pointing to is exposing a web service. And that's exactly what we are going to do.

To configure these records, we are going to install Nginx in Node-02 to have a service exposed from there. So I'm going to ssh into Node-02.

And then I'm going to run this apt install nginx. Okay, so we start Nginx. And from here, I should be able to do curl to localhost.

And we should see the HTML page. Okay, it seems that it's working. Now I'm going to SSH back into Node-01.


And from here, I'm going to edit the zone file again. And this time, I'm going to add the CNAME record, just like this.

On the left, we have the www, which means that if we hit www.my.kodekloudlab.com, it will be equivalent of getting to the IP address of my.kodekloudlab.com, basically.

Let's not forget to increase the serial number in the SOA record, by the way. Okay, now that we have saved the file,

what I want to do is curl the Nginx service simply by using curl and then www.my.kodekloudlab.com. To make it work, what I'm going to need to do is edit the resolv.conf file.

If you're following along or you do this in any of the KodeKloud playgrounds, make sure you keep a copy of the nameserver that's originally in this file

in case you need to roll back for some reason to redo any of the steps if you made a mistake or something.


Because otherwise, you'll have to restart your lab all over because it’s going to be messed up with a nameserver pointing to a localhost IP address.

Okay, so now that I did this, I'm going to restart BIND9 again just to make sure everything’s working. Now, this indicates that we successfully configured our nameserver to resolve the main names in the my.kodekloudlab.com zone.

Another thing I wanted to mention about CNAMEs before I close the video is that in Amazon Route 53, CNAMEs have some unique characteristics as they can point directly to AWS resources like S3 buckets or load balancers through alias records, even at the root of the domain level, which regular CNAMEs can't do.

But I thought it was worth mentioning as it threw me off the first time I saw it. Okay, that’s it for this demo. I hope you enjoyed the walkthrough. Thank you so much.

## Other Recors: TXT, PTR and SRV
DNS supports other record types with different specific purposes that we haven't covered in the course yet. So in this video, I want to cover the following DNS record types.

We are going to talk about TXT records for storing text information, SRV records for service discovery, and PTR records for reverse DNS lookups.

For TXT records, or text records, we have that they were originally designed to hold human-readable notes in DNS. However, they've evolved to serve many machine-readable purposes too.

To request a text record for a domain, simply use dig and include the TXT record in the request, like the command shown on screen.

Think of TXT records like digital sticky notes that say, Yes, the owner of this domain approves this service. So TXT records will generally be used as a digital badge that proves a domain is authorized to use a certain service, such as 1Password, Google Site Verification, or ensuring that only Google’s mail servers and mail.k8s.io can send emails using the @kubernetes.io addresses.

Here's a high-level explanation of the TXT records returned by kubernetes.io. For the 1Password verification, what this is telling us is that, if an organization like kubernetes.io wants to use a password manager like 1Password, they need to prove they own kubernetes.io.

Think of 1Password like a secure digital vault where organizations store all their passwords, API keys, and other sensitive data. 1Password says, put this specific TXT record on your domain to prove you control it. It's like showing your ID to open a bank account.

You are proving ownership. Now we have two Google verification records here. They were likely generated at different times and for different purposes.

It's like having multiple keys for the same house. One of the keys might be for Google Workspace or Gmail, and the other one for another Google service. It proves domain ownership to Google, which may give kubernetes.io the authority of using this domain name for certain services.

A good example on using a domain name in other services is email. We have this SPF record, which is like saying, only Google mail servers and mail.kubernetes.io can send emails from

at kubernetes.io addresses. SPF means Sender Policy Framework, by the way. The point is that, if a scammer tries to send email pretending to be from kubernetes.io,

but uses their own server, receiving mail servers will check the kubernetes.io DNS and see that this server is not authorized,

making it more likely that the email is placed in the spam folder or something. Without these text records, kubernetes.io couldn’t use these services securely.

They’re like digital ID cards proving domain ownership to each of these services. Moving to SRV records. SRV stands for Service,

and these are DNS records that help with service discovery. By associating SRV records to a domain, other services running on this domain can see them.

and finding them will help them get information on how to find certain machines or applications in the DNS. I see this has been similar to placing pins on your favorite restaurants in Google Maps, for example,

which helps you track and get information on where the restaurant is, when it's open, what kind of food they serve, etc.

SRV records are like digital pins that help systems track where services are running and how to connect to them.

Kubernetes uses SRV records to help pods find and connect to other services across a cluster. When you deploy microservices in Kubernetes,

CoreDNS, which is a cluster's DNS server, will automatically create SRV records. These records are stored in CoreDNS's internal DNS zone files,

which get updated whenever services are created, modified, or deleted through the Kubernetes API server. This is how an SRV record looks like.

Let us know if you'd like us to explore the details of Kubernetes service discovery with SRV records more deeply in another lecture.

Now we have PTR records, which are called pointer records, and these are used for reverse DNS lookups. As we may know, in a regular DNS query,

we are looking to find which IP address is associated with a domain name by passing the domain name in the DNS query.

In a reverse DNS lookup, we look to find the domain name associated with an IP, so we use the -x flag to indicate we are requesting a reverse DNS lookup.

And then we pass an IP address in the query instead of a domain name as we would normally do.

When performing a reverse DNS lookup, the IP address gets automatically reversed and appended to an PTR top-level domain. In the top-level domains lecture,

we explained that there's an RPA top-level domain that exists with the purpose of making reverse DNS lookups possible. So in this video, I want to elaborate more on that thought so that we make it clear how it actually operates.


I must begin by reminding you that domain names are read from left to right. The concept of reading the domain names from left to right is what enables walking the DNS tree starting on the Root Zone.

IP addresses, on the other hand, are read from right to left. So to be able to use an IP address to perform a reverse DNS lookup,

we first need to reverse the IP address to make sure the DNS system will be able to read it from right to left.

Then we append the reverse IP address to an RPAT top-level domain and to a root zone by consequence to make the domain name adhere to DNS standards.

So by reversing the IP and appending it to the .arpa top-level domain, we can use the standard DNS walking process which reads the domain names from right to left as we've already explained.

This will help us find the corresponding domain name associated to an IP address. Let's see what happens when we walk the DNS Tree for a reverse DNS lookup.
In the query, we are performing a reverse DNS lookup to 8.8.8.8. The IP gets reversed and then appended to the PTR top-level domain,

so the domain resolution can be attempted by walking the DNS tree to the address 8.8.8.8.in-addr.arpa and then the dot at the end to symbolize the root zone.

So we begin by asking the root zone for the RPAT top-level domain name servers. We figure that the IN address is a subdomain of RPAT, but they're in the same zone.

We then move to the 8 third-level domain, where we ask for information about this domain name, and this is where we get an authoritative answer.

The authoritative answer includes a PTR record with the value of dns.google. This means that the domain name associated with the 8.8.8.8 IP address is dns.google.

We can prove this by asking dns.google.com for its A records. PTR records are created just like any other DNS record with your hosted zone,

whether you're using a service like Route 53, Cloudflare, or another registrar. It's important to mention that you must own the IP address for which you are creating the record.

In most cases, you'll only want a PTR record for a service that involves using a static IP address. For many common use cases involving web applications, using PTR records may not be the best idea, given how web apps benefit from dynamic IP addresses more so than from a static IP address.


## MX Records
When I was planning this course curriculum, I communicated back and forth with KodeKloud project managers through email, using my personal Gmail account, which I operate directly from a browser.

I want you to imagine that every time I hit reply to an email, because the email I'm replying to has a cochla.com domain,

the following things would happen in the background. Since my email is hosted in Gmail, Google would pick a Gmail mail server to try to deliver the email using SMTP.

The designated Gmail mail server will now be responsible for finding a recipient for the email, which is another mail server somewhere else.

To find the recipient, the Gmail mail server performs a DNS query to cochla.com domain, requesting its MX records. The DNS query returns multiple mail servers,

and one of these servers is chosen to receive the email. The email server then requests its A record. Finally, an IP address for the actual mail servers is retrieved, and this is where the email will be delivered. In the domain name system, MX records are used to point to mail servers

to help an email message reach its destination. The anatomy of an MX record goes as follows. First is a domain name.

This must be a domain you own and control. 300 is a TTL, which means that these records will be cached by DNS servers for 300 seconds or 5 minutes

before they need to check for updates. IN is for Internet Class. This is the standard class for all modern DNS records.

MX is a record type that indicates this is a mail exchange record. In other words, this record will tell DNS which mail servers are responsible

for receiving email for this domain. The numbers like the 10, 5, and 1 show priority level, which I’ll explain soon.

Last is the name of the mail server that will receive the email. While DNS will let you save an MX record pointing to any valid hostname, that hostname must be a real mail server configured with SMTP to receive emails. If not, any messages sent to your domain will fail to deliver and bounce back to the sender.

When adding an MX record to your domain zone file, you would write it like this. This tells email systems that mail.kodekloud.com is a mail server

that will receive email for the kodekloud.com domain. The mail server itself needs its own A record, so other servers can find its IP address.

In practice, most of us will work with MX records directly from a domain registrar's web interface. Most, if not all of them, will have the option to configure MX records.

For example, in Cloudflare, Route 53, or GoDaddy, you simply go to the DNS settings, click Add Record, select MX type, and fill in the priority and the mail server hostname.

Email needs to be reliable, so domains typically have multiple mail servers for backup. This is why MX records use a priority system to direct emails to the best available server.


Looking at the kodekloud.com example, we see priorities of 10, 10, 5, and 1. What this means is that the mail server with the lowest number will be tried first, as it has the highest priority. So mail servers will first try to deliver to smtp.l.google.com, which has a priority 1.

If that fails, they’ll try the priority 5 servers. If those fail, they’ll try the priority 10 servers last. When MX records are configured with the same priority,

mail servers will pick one of them in a load-balanced fashion. Some rules around MX records are MX records cannot point to CNAME records.

They must point to hostnames with A or AAAA records. Having no MX records for a domain means email will attempt delivery using the A record,

which is called implicit MX. Each MX record must have a priority value. Of course, there are security considerations around email.

For example, malicious actors could intercept an email while it travels through the Internet or send emails pretending they are coming from your domain by spoofing the sender address.

To protect against these threats, modern email systems use a combination of three main security protocols. First, we have SPF, or Sender Policy Framework.

As mentioned before, these are TXT records that list which mail servers are authorized to send emails from your domain.

When someone receives an email claiming to be from your domain, the mail server checks these SPF records to verify if the sending server is legitimate.

We also have DKIM, or DomainKeys Identified Mail. This adds a digital signature to every email sent from your domain.

The signature is created using a private key that only your mail server knows, and the public key is published in your domain's DNS TXT records.

Receiving mail servers can verify this signature to ensure the email wasn’t tampered with during transit and if it really came from your domain.

We also have DMARC, or Domain-Based Message Authentication Reporting and Conformance. This protocol ties SPF and DKIM together and tells receiving mail servers what to do if an email fails these authentication checks.

DMARC policies, which are also stored in TXT records, can instruct servers to reject suspicious emails outright, quarantine them in spam folders, or just monitor and report failures back to the domain owner. Together, these three protocols form a comprehensive email security framework that helps ensure emails are legitimate and haven't been tampered with. When properly configured, they make it much harder for attackers to successfully spoof emails or conduct phishing attacks using your domain.


# Domain Name Lifecycle

## Domain Registration Process
Throughout the course, we've talked about registering domains and how DNS works in general. In this video, I want to talk about the domain registration process more in-depth.

To make it enjoyable, I'm going to explain the process with three different actors that play crucial roles in this process. First, we have the registrar. This is the company that offers

domain registration services, companies like GoDaddy, Namecheap, or Google Domains. They're like the real estate agents of the internet. Next up is the registrant. That's you, me,

or anyone wanting to register a domain name. If we continue with our real estate analogy from previous lectures, we're the ones looking to get our piece of digital land. And finally,

we have the registry. The registry is the organization that maintains all records for a particular top-level domain. VeriSign, for example, takes care of all .com domains.

They keep the main list of who owns which domain in their territory. One day, our friend the registrant wakes up and decides he needs something special. He's tired of living in his parents domain. Every day, he has to put up with WordPress.com, Medium.com, or GitHub.io as his address. No more, he says. I need my own domain name where I can be independent.

The registrant starts researching. He discovers there's this whole huge business dedicated to selling domain names, and the people that make it possible are called the registrars.

These registrars are like real estate agents of the internet, each with their own special way of doing business. As he digs deeper into this domain world, he learns about the real

powers behind the Domain Name System, the registries. These aren’t your regular businesses. They’re more like territory bosses, each controlling their own piece of the internet.

There’s VeriSign, the biggest boss of them all, controlling the massive .com territory. They process millions of domain transactions daily, keeping their books clean and their

territory under strict control. No domain gets registered in .com without VeriSign knowing about it. Then there's the Public Interest Registry running the .org territory. They're like the more community-focused family, preferring to deal with non-profits and organizations that help people. They run a tight ship too, but with different rules than VeriSign's territory.

Over in the .io territory, you've got the Internet Computer Bureau. They’re the new kids on the block who made it big when tech startups started flooding into their territory. They saw an

opportunity and turned their small island domain into prime internet real estate. In his exploration, he also learns about this huge underground world of domain trading. Some sketchy registrars hide

in the dark corners of the internet, specializing in something called domain snatching. They grab domains the moment they expire, then sell them for huge profits. That's not what I want, thinks the

registrant. I want something legitimate. What the registrant just discovered is a real practice in the domain industry. Companies like DropCatch.com and SnapNames operate vast networks of registrars

specifically to catch expiring domains. They use automated systems to monitor expiration dates and and instantly register valuable domains the moment they become available. Some companies even control hundreds of registrar accreditations just to increase their chances of catching valuable domains. This process of domain snatching is called domain drop catching,

and it happens when domains aren't renewed by their owners. The registries created a system to prevent chaos in their territories. When a domain expires, it goes into something called a redemption

period, a sort of domain name purgatory. Without it, you'd have domain snatchers camping outside their digital offices, waiting to grab expired domains like vultures. In the actual domain name

system, when a domain expires, it goes through several stages. First, a 30-day grace period where the owner can renew normally. Then, a 30-day redemption period where renewal is possible but

costs much more. Finally, a five-day waiting period before it becomes available to anyone. Some other registrars, like GoDaddy and Namecheap, are more like traditional real estate offices.


providing straightforward domain registration services. They work directly with the registries, but here's the thing. The registries don't deal with regular people. No, they only deal with

authorized registrars. It's just business, they say. We keep the records. You handle the customers. He notices the prices are different between registrars, so he starts asking himself why.

Now I understand, thinks the registrant. Each registry charges registrars a different protection fee for their territory. Verisign charges more for .com because they can. Everyone wants to live

in their neighborhood. The .io registry saw this and raised their prices too when they became popular with tech companies. In the domain name industry, these price differences are significant.

Verisign charges registrars about $8 to $20 yearly for a .com domain, while the .io registry charges around $60. Registrars then add their markup,

which is why you might pay $15 for a .com but $80 or more for a .io domain. Ready to start his journey to independence, he first tries to get bestcode.com,

The registrant doesn't give up. That's it, he exclaims after some more research. All the cool tech companies are using .io these days, so he asks his registrar to check with the

Internet Computer Bureau about getting bestcode.io. Good news, says the registrar. bestcode.io is available, but you better act fast. Domain names in trendy territories like .io don't stay available

for long. The registrar reaches out through their special connections. Let me talk to the registry, they say. Only authorized registrars like us can communicate with them directly.

The conversation with the Internet Computer Bureau's registry goes something like this. Registrar, hey, I've got a potential new registrant for your territory.

Registry, ah, one of your customers wants to establish themselves in our namespace. Registrar, yes, they're interested in bestcode.io. I've already collected their information and payment. Registry, let me check our records. Yes, that name is available in our territory. You're an authorized registrar, so we can proceed. Send over the technical details.

This conversation happens through the EPP protocol, where the registrar sends standardized commands like check domain, create domain, and the registry responds with specific status codes.

The registry continues. Once we add this to our zone, here's how the delegation will work. We already control .io. The Root Servers have been pointing to our Nameservers for that.

We'll add bestcode.io to our zone file along with its nameservers. This tells everyone that these specific nameservers are authoritative for bestcode.io.

The delegation hierarchy is already established. Root servers have NS records pointing to the .io registry's nameservers. When registering a new domain, we're just adding a new entry to the .io zone,

not changing anything at the root level. The registry adds NS records for bestcode.io, and those specific nameservers will need matching records to complete the delegation chain.

Your customer will need to set up their name servers, the registry adds, and make sure they have matching NS records on their side. That's how the internet will know where to find these

domain services. Understood, says the registrar. We'll handle the payment and make sure the registrant understands their responsibilities. The registry updates their master database,

the ultimate source of truth for who owns what in their territory. With this update, the delegation chain is clear. The root servers already trust the registry's name servers for all

.io domains, and now the registry zone will show that bestcode.io belongs to our registrant. Next, the registrant will need to make sure their nameservers have matching records to

complete the chain. But the story doesn't end here. The registrar asks, now, what nameservers do you want to use? The registrant looks confused. What do you mean?

Well, explains the registrar, owning a domain is like owning land, but to actually use it, you need to build something on it. The nameservers are like the building permits, they tell the internet what you're going to do with your domain. You see, continues the registrar, you can either use our nameservers, or if you're hosting your website somewhere else,

you can use theirs. Most people starting out just use whatever their web hosting company gives them. The registrant thinks about it. So even though I own the domain through you,

I can use it with any hosting company I want? Exactly, says the registrar. That's the beauty of how domains work. We're just the ones who handle the paperwork with the registry.

What you build on your domain, and where you build it, that's entirely up to you. This separation between domain registration and hosting is a fundamental principle of the

internet. It's why you can register a domain with GoDaddy, but host your website on AWS, or use Cloudflare for DNS while keeping your domain registered somewhere else.

The registrant decides to use a popular hosting company's nameservers. The registrar types them in, ns1.hostcompany.com, ns2.hostcompany.com. Now watch what happens, says the registrar. I'm telling the registry, the Internet Corporation for Assigned Names and Numbers, that these are the name servers responsible for your domain. From now on, when anyone anywhere in the world types bestcode.io into their browser,

the Internet will know to check these nameservers to find your website. This process updates what’s called the zone file at the registry level.

Every TLD registry maintains a zone file, essentially a massive directory telling the Internet which nameservers are authoritative for each domain in their territory.

The registrant beams with pride. Finally, after all this research into registrars and registries, after learning about domain hijacking and redemption periods,

after understanding why different territories cost different amounts, he finally has his own piece of the Internet. No more living at WordPress.com or Medium.com, he thinks.

Bestcode.io is all mine. Time to build something great on it.

## Negative Caching
In the domain registration story, we had our friend the registrant, who was tired of living at WordPress.com and Medium.com, wanting to register his own domain. Let’s use this same scenario to understand how negative caching works. When someone tries to access a domain that hasn’t been registered yet, in other words, when the registrant was checking if bestcode.io was available, the DNS resolver needs to figure out if this domain exists.

Now, keep in mind that the code samples I'm going to show are for illustration purposes only, with the purpose of enhancing the explanation.

Using the following commands most likely result in different outputs. With that in mind, let’s talk about how using a dig command against a domain that hasn’t been registered yet returns an NXDOMAIN response. In this output, the Negative Caching field corresponds to the 3600 number as highlighted on screen.

Let's understand what’s happening here with negative caching. When a resolver gets an NXDomain response like this one, it also receives the SOA record of the parent zone, in the case, io.

Looking at this SOA record, the last number, 3600, is actually a suggestion from the zone operator about how long resolvers should remember this domain doesn't exist response.

But here's the interesting part. Resolvers aren't actually required to follow this suggestion. Some might cache for the full suggested time,

others might use shorter periods, and some might even ignore it completely and use their own rules. This is entirely up to each resolver's configuration and policies.

This becomes really important when our registrant finally registers their domain. Even though the top-level domain operator now knows about it,

some resolvers might still have that old this-domain-doesn't-exist information cached. That's why, when you register a new domain, you might find that some people can access it right away,

while others get errors saying the domain doesn't exist. These differences happen because different resolvers around the world have different cached information and different caching mechanisms.
The same thing happens in reverse when a domain expires. Remember how in our story we talked about domain snatchers waiting to grab expired domains?

When a domain enters that redemption period, resolvers start getting NXDOMAIN responses again, like in the output displayed on screen.

Notice how VeriSign suggests a negative caching time of 900 seconds, or 15 minutes, for expired .com domains. This shorter time makes sense because

so resolvers shouldn't cache the non-existent response for too long. This caching system exists because having every resolver check with each registry

every single time someone tries to access a non-existent domain would overwhelm their systems. It's also helpful against attacks, where someone might try to overload the DNS system

by repeatedly querying for domains that don't exist.

## Domain Transfer != Zone Transfer
In a previous lecture, we explained that zone transfer is the process where nameservers sync data between each other. The DNS follows a leader-follower architecture, where the primary nameserver receives the

updated records in a hosted zone file, and the other ones get the data replicated through various mechanisms. In this lecture, we're talking about domain transfer.

A domain transfer can mean either changing the registrar that manages your domain, or changing who owns the domain. In other words, the registrant, or both at the same time.

Let's use KodeKloud.com as an example, which, as we've seen before, uses Cloudflare nameservers. If Mumshad Mannambeth wanted to keep ownership but move KodeKloud.com from Cloudflare to

AWS Route 53, that would be a registrar transfer. If he wanted to give ownership to someone else, that would be a registrant transfer.

And he could do both simultaneously, transferring ownership to someone else who uses a different registrar. However, domain transfers can also happen through attacks. 

Domain hijacking is a form of DNS attack, where someone will attempt to take control of your domain by trying to impersonate you, for example by sending an email on your behalf.

This is particularly dangerous because ICANN considers email as an acceptable method for assessing validity. To defend against domain hijacking, there are several important measures you can take.

First, always keep your domain locked. Domain locking is a feature offered by domain registrars that prevents unauthorized transfers of your domain name without your explicit permission.

Most registrars have this option set by default. This is called the domain transfer lock or registrar lock, and it prevents unauthorized transfers. Second, keep your SOA records updated. Third, enable auto-renewal on your domain to prevent expiration. And finally, use strong authentication methods whenever possible.

To conclude this lecture, remember that while domain transfers are a legitimate process, they can be exploited through domain hijacking attacks.

Now, for example, if you were subject to a domain hijacking without your authorization, you can file a dispute with ICANN to investigate and potentially reverse the transfer.

## $WHOIS
In our previous lectures, we covered how DNS helps us locate services on the internet by translating domain names into IP addresses,

and how nameservers act as authoritative sources for this information. While DNS SOA records provide some administrative information like the primary nameserver and zone administrator's email,

they don't give us the complete picture of domain ownership and registration details. WHOIS is a protocol standardized to give information related to domains being registered,

providing information about domains such as registrar information, registration dates, expiration dates, and various contact details, while DNS focuses on service location and basic administrative details.

Though still in use today, WHOIS is gradually being replaced by RDAP, which is the newer Registration Data Access Protocol offering more structured data responses.

Let’s look at how WHOIS works in practice. On screen, we have a basic WHOIS query. Similar to how DNS uses a hierarchy of servers, WHOIS queries follow a path through different servers to get informations.

On screen, we can see this process. One important aspect of WHOIS is privacy. Many registrars now offer WHOIS privacy services that replace personal contact information with proxy details.

On screen, we can see a privacy-protected record. Today, most domain management happens through modern cloud providers and their APIs.

These providers still maintain WHOIS records as required, but they're moving toward RDAP. On screen, we have a snippet of how an RDAP query looks like.

RDAP solves several WHOIS limitations, for example WHOIS returns text-based responses, which resulted in responses being structured differently. RDAP provides structured JSON responses instead of free text, supports internationalized domain names better,

and includes standardized status codes. Most importantly, it’s built on HTTP, making it easier to integrate with modern web services and APIs.

When working with domains today, you'll encounter both systems. WHOIS remains widely used for basic domain lookups and verification, while RDAP is becoming the standard for automated domain management and integration with modern cloud services.

Both serve the same basic purpose, providing information about domain registration and ownership that complements the technical data available through DNS.

Using both may come in handy when debugging or troubleshooting the DNS or simply for understanding more about a domain name.

# Miscellaneous
## Setting up DNS Monitoring Tool
Monitoring DNS is an exciting, vast topic, but I want to quickly go over some of the techniques that I use to encourage you to start digging more into this. First, because I’m on macOS, I’ll show you this Docker image called netshoot that comes with a bunch of networking tools, which I commonly use for troubleshooting network issues inside Kubernetes and other containerized workspaces. Using this will allow me to run strace commands to trace Linux system calls. I want to show you a few interesting techniques to learn how to read network system calls related to DNS. Here, I'm running an strace command to monitor the network-related system calls during a DNS lookup. The "-f" flag tells strace to follow any child processes that might be created during execution, so I don't miss any activity, even if the process spawns others. Meanwhile, the "-e trace=network" option restricts the output to only those system calls related to networking, such as when it opens a socket or makes a connection.


On the other side, the dig command is performing a DNS query with several options. For example, the plus trace makes dig follow the DNS delegation chain from the root servers down to the authoritative nameservers until we get the final answer. If I control F and search for the connect word, you'll see that it's often followed back-to-back by send message and receive message functions. This often indicates which server is giving the answer.

So if I go to the very top, and then we find who gave the answer for their root name servers, you can see that the answer was given by this IP address. I believe this belongs to the resolver configured in this Docker environment. Every recursive resolver comes pre-configured with a list of IP addresses for all their root name servers called root hints, which helps us reach root name servers to start walking the DNS tree. Following down the path, we can see that the second answer was given by this IP.

If we do our reverse DNS lookup, we can see that this belongs to this nameserver, and so we can continue following their resolution chain. This gives information not provided by simply doing dig +trace. For example, right here, we can see that to resolve the AWS nameservers' IP addresses, instead of resolving this by following conventional DNS processes, the recursive resolver had the records in cache, so it returned the answer, as indicated by this line.

Another great tool to use is Wireshark. I have Wireshark installed on my macOS, and I'm going to show you a basic configuration that I use to monitor DNS traffic. So if you open Wireshark, the first thing you may be asked is which network interface you want to monitor. I'm selecting EN0, as that's the one my computer used to connect to my internet router. So I double-click on it, and now I see a lot of traffic showing on the dashboard.

To shortlist the data to only DNS, you can use a filter such as this one, where you indicate that you want UDP and TCP traffic comming from port 53.
If you have a browser open or any internet application running, you'll be surprised at how many DNS requests happen, even on standby.

Here I'm using the command against gocloud.com really quickly so we can inspect the traffic. You can see that there's a query and a response message here.

If we click on the response, we can analyze it, remembering all we've learned in the DNS as a protocol section, and even how many bytes each part of the response is taking. Another tool I use is tcpdump. You can see that by running this command on my terminal, because we are monitoring port 53, which is the default one that DNS uses, I start to get on standard output some of the activity by my ISP's DNS resolver.

For understanding very large outputs for these types of logs and system traces, a great learning resource may be to use an AI chatbot to get help interpreting the information. This can help you get used to navigating through these verbose logs. Just be careful of not sharing any sensitive data.

## Troubleshooting DNS
Troubleshooting DNS is difficult, as it involves a wide number of systems interacting with each other, starting from your machine, all the way to the authoritative nameserver, then again, on the trip of the response coming back to the initiator. Additionally, we've learned that different applications or platforms have different caching life cycles.

For example, if you've encountered an issue where a DNS command successfully resolves a domain name, but the browser doesn't, it's probably because the operating system caches records for a certain period, while the browser caches them for a different duration. Let's quickly go over some of the basic categories of DNS issues, along with an initial guideline, and how to start troubleshooting. First, we have that the different systems may be unable to communicate due to network.

Another issue could be that maybe they can communicate, but one of the resolvers or nameservers is overloaded, resulting in slow DNS.

Another issue could be that we get the wrong DNS responses by the nameserver, for some reason. Let's break down each category and explore basic troubleshooting approaches for each.

For the networking aspects, we have that, when dealing with networking-related DNS issues, we have to start with basic connectivity checks. We may try pinging the resolvers first. We may also check if the network interface is properly configured, and if this is an issue with DNS or with connectivity to the internet in general. We may want to check if there are some firewalls blocking port 53 for UDP or TCP. This can be checked by using Telnet, for example.

Often, VPN configurations may be the cause of DNS issues, so disconnecting from a VPN can also help. For slow DNS, it's usually because one of the servers in the chain is slow to respond. You may notice this when new websites take ages to start loading, but they work fine once they do load. The best way to find a slow link is using the dig and trace option. This walks through the entire DNS resolution chain.

Watch the timing on each step. If one nameserver takes several seconds while others respond quickly, you've found your bottleneck.

There are some ways to test the speed of a DNS resolution by using the time command and the dig command, like the example shown on screen, where you may direct your query directly to your resolver by using the @ symbol, and then the IP address of the resolver. There are some online tools that benchmark resolvers' performance. Another type of DNS issue is having the wrong DNS response.

Wrong DNS responses usually mean either caching issues or that the authoritative nameservers are not properly synced. I'd say this is one of the most common types of DNS issues, and one of the most difficult to debug.

I learned from **Ruijan Paul**, an engineer that creates a bunch of DNS learning resources, that when working with caching issues, it's better to start with the outside components and work inwards.


As he explains, that clearing the cache, for example, in your operating system first, if the DNS issue happens to be with stale cache in one of the external resources, your operating system will just repopulate the same faulty records from an external resource, whereas if you start on the outside and work inwards, you make sure that you'll be following a path that ensures better results. So we'll generally start with the public resources until we end up clearing the cache in our local machines.

Some public resolvers have a web tool that you can use to clear the DNS cache, like the links displayed on screen. Some companies that provide content delivery network resources, like Akamai, may provide tools to either invalidate or delete the cache. This is an interesting reading, and I'm providing a link resource so you can learn more about this concept. Remember that the resolver that you communicate with depends on the configuration on your machine.

Some devices are configured to talk to a resolver from your internet service provider first, so deleting the cache on public resolvers like Cloudflare or Google will do nothing if you're communicating to a resolver from your internet service provider. However, if this is the case, some of the cached records may be cleared when you reset your router.

Moving into the operating system, we have that, if we're on Windows, we can use these commands to clear the DNS cache in the operating system.

For Linux, we generally use systemd-resolved, which is the default in most modern Linux distributions. If you're running your own DNS server like BIND9, you'll be working with two important components.

The name server, this is your actual DNS server, so you can do systemctl start, stop, or restart named, depending on the operation you want to perform.

For BIND9, we also have the rndc tool, which is a tool that lets you manage your records in your DNS server without restarting the entire service.

The commands for macOS will be different depending on the operating system version. For example, for Ventura and higher, we have the dns-cache-util.

For older versions, there is a discovery-util tool that you can use to flush the cache. So now that we are getting into the operating system, we'll get to the application level.

Specifically about browsers, most modern browsers will have a URL that you can type in the browser where you can select clear host cache or clear DNS cache.

The URLs are displayed on screen and will be different depending on the browser that you're using. Now, keep in mind that if the DNS issue you're encountering is specific to an application, for example, a desktop application or a web application that you're running locally, so restarting the application will probably clear them as well.

Wrong DNS responses, however, may also be caused by synchronization issues, not only by cache. Remember that the DNS uses a leader-follower architecture.

and if the records are not synchronized between the leader and follower authoritative nameservers, they’ll be responding with different DNS records.

I would recommend you to check this by doing DNS lookups against the different nameservers directly. You can use the dig command or nslookup to query specific nameservers, like in the sample shown on screen. If you get different answers from different nameservers, you likely have a zone transfer or synchronization issue.

This is particularly common after DNS changes, when the TTL hasn’t expired or not all nameservers have updated their records yet.

You can also check the SOA serial numbers to see if all of the authoritative nameservers for a zone display the same serial number ID.

If the serial numbers don’t match, that’s a clear indicator of a synchronization issue between your nameservers.


# Final Project
## Setting Up DNS Server 

In this demo, we are going to demonstrate a multi-node DNS setup. We are going to have two nameservers. The primary nameserver will be node-01, and the secondary nameserver will be node-02.

We will have a webserver with an application running on node-03, which we are going to use as a client as well.

So first, let's install BIND9 on node-01, which is going to be our primary nameserver. Ok, so let's start BIND9, and then we are going to declare where our zone file is going to be by modifying the name.com.local file. Our zone will be multinode.kodecloud.lab. So we add the type here to indicate that this will be our primary nameserver.

And we are declaring that our zone file will be in the etc bind directory. If this was created on the public internet, this zone file would represent that we are intending to make the multinode.kodecloud.lab as a domain apex for a zone called multinode.kodecloud.lab. Let's save and exit. Now, to create the zone file, I want to find our node-01 and node-02 IP addresses first.


because we are going to need them for the zone file. Ok, so I'm going to copy the IP addresses.

Now let's create the zone file. The zone file by default will be on the etc bind directory, and by convention, it's going to have the db prefix followed by the domain apex, in this case multinode.kodekloud.lab. To begin with, we have to start by declaring the SOA records, the NS records, which are going to be node-01 and node-02, and then the Glue Records at the bottom. So let's save the file. And then we restart BIND9.

And then we are going to try to resolve multinode.kodekloud.lab domain by querying directly our authoritative nameserver node-01 by using the at localhost notation.

Seems like it's working. In the lab exercise, we may have you configure the zone file and then the named.conf.local file in a different order. The important thing is to remember what each one does. The named.conf.local file indicates the purpose of this server, stating that it is a primary nameserver, and it also indicates where our zone file is going to be located at. The zone file has records for our domain.

So we are going to configure the secondary nameserver, node-02, so let's ssh into it, and then we are going to install BIND9 again using the same commands we used moments ago.

Ok, so we start by 9. Now let's check node-01's IP address again, because it will be needed for this step.

Ok, so I'm copying node-01's IP address, and then we are going to modify the named.conf.local file for node-02. This file will indicate that node-02 is our secondary nameserver, which means that this

will be a follower of the leader, which is a primary nameserver. We are specifying that the leader is node-01, and we are giving its IP address on line 4 to point to it. So we save the file, and then reload BIND9. Now let's SSH into node-01 again. So here, we are going to modify another file called named.conf.options.

This file controls configurations for how our nameservers will behave. For example, here we declare whether recursion will be allowed or not, which some nameservers don't allow to prevent being overloaded with requests. In this case, we are specifying that we want to allow zone transfer from node-02.

Zone transfer means that a secondary nameserver will be able to request a copy of the DNS records, so both nameservers stay in sync, creating a more reliable DNS system.

Now if we restart BIND9 again, and then we ssh into node-02, here we will try to make node-02 use itself as a nameserver to answer queries for multinode.kodekloud.lab, and it should work fine. We can also use node-02's IP address, and it should work fine as well. Ok, so although the following exercise won't come up in the upcoming lab, it's worth noting that you can request a primary nameserver to sync records using the AXFR to transfer the entire zone, or IXFR to transfer only incremental values.
However, as we learned in the zone transfer lecture, most modern cloud DNS providers won't use these replication mechanisms, since they would probably have their own proprietary replication mechanisms of their own. If you're a DNS administrator, and you require your nameservers to be in sync on demand, this is what you do. Anyway, let's log in to node-03 now. Here we are going to install nginx, then we are going to start nginx, and we check the installation using curl. Ok, so it's working. Now we are going to add a CNAME record pointing to this service on our primary nameserver.

So let's SSH into node-01, then we are going to modify our zone file. Here we are adding the CNAME record pointing to the web service, so that whenever we do curl www.multinode.cococlub, it should respond just fine. So we restart by 9 again, and then we SSH into node-03. And here we are going to modify the etc/resolve.conf file by adding the IP address of node-01 of  the nameserver. We save the file, and now we should be able to do curl www.multinode.coconutlab, and we can see the output produced by the Hello World nginx web service running, which means that

we've successfully configured a 2-node DNS nameserver setup.