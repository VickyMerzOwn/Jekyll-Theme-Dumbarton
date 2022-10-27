---
layout: post
title:  "A new internet and why we need one..."
description: "Problems with the internet of today, how to fix 'em, what's been done so far, and what's left to do."
date:  2022-10-28 20:30:00 +0530
type: card-img-top
categories: latin text
image: 
caption:
last-updated: 2022-10-28 20:30:00 +0530
categories: SCiON
tag: Scalability, Control, and Isolation
author: Satvik Vemuganti
card: 
---

"Some academics arrive to tell us that (once again) they have fixed the internet and (once again) it runs on top of the current actually working internet and (once again) if you sign up you can connect with as many as twelve other computers".

One can vouch for 2 out of 3 things in the above quote. As for the third, SCiON can connect a whole lot more than a dozen machines with each other.

The internet to me, after a couple of months of formal coursework in computer networks (and a few years of using and informal learning of it), is an abstract world that human beings have invented. It has citizens, infrastructure, resources to compete over, and most importantly some laws. Protocols. Protocols govern the way it essentially works. The division of labor employed in this abstract world would be the TCP / IP stack of layers the internet is divided into. At the network layer, one would find rules such as DHCP and, particularly notable in the context of SCiON, BGP. The problems with the internet of today, as several publications on the scion-architecture website point out, can be attributed to the context over which today's internet was built. The internet was built with a "throw and pray" attitude. It was meant to connect end hosts (without much computing power at the time).

Taking from Prof. Adrian Perrig's talk at CyLab CMU, "the internet is perceived to be a monumental structure that has stood the test of time and as something that cannot be changed". It is more analogous to this structure in the image below. The 4 pillars of today's internet are:
- Control
- Transparency
- Availability
- Trust

<br>
<br>
<div style="text-align: center">
    <embed src="/assets/img/posts/2022-10-28-SCiON/1.png" alt="drawing" height="350" position="center"/><br>
</div>
<br>
<br>

#### Trust, its Scalability, and Isolation Domains

Routing updates, DNS replies, and TLS certificates constitute some of the fundamental entities of today's internet. Unfortunately, these are blindly trusted entities that aren't able to survive the simplest of attacks (to be discussed ahead in this blog post). But then we realize that the internet was never expected to have untrustworthy entities, that are indistinguishable from the trustworthy ones, to be a part of it. It was meant to be a tightly-knit community of computer users who could **connect** with each other. And so the SCiON documents term this problem as that of **non-scalability of trust**.

<br>
<br>
<div style="text-align: center">
    <embed src="/assets/img/posts/2022-10-28-SCiON/2.png" alt="drawing" height="350" position="center"/><br>
</div>
<br>
<br>

Certificates of authentication are provided by entities (roots of trust) that belong to one of two models, Monopoly roots of trust and Oligarchy roots of trust. While monopoly models have issues ranging from that a single point of failure to inefficiency, having multiple roots of trust means bogus roots of trust can pop up as a new certifying authority.

<br>
<br>
<div style="text-align: center">
    <embed src="/assets/img/posts/2022-10-28-SCiON/3.png" alt="drawing" height="350" position="center"/><br>
</div>
<br>
<br>

SCiON proposes that several subsets of the internet can agree on their own roots of trust and form **isolation domains**. These roots of trust would be responsible to authenticate entities within each domain. Users can select which ISD to be a part of depending on the root of trust to which they belong. These roots of trust support Modern log-based Public Key infrastructures for authentication. A prominent challenge would be the global verifiability of users. 

#### Control

Going back to the image, control is another one of the brittle pillars of today's internet. Governments around the world have announced networks including certain countries and leaving out a certain few others. Users have voiced concerns about being able to be reached by users from certain countries. In either case, this would be possible with Isolation Domains. Another aspect to control would be the paths that the datagrams take. The current internet offers minimal control of paths. Of course, ISPs propagate BGP update messages. But there is limited control over these messages after they leave. Other ISPs decide which of these messages propagate. And the destination ISPs can barely decide which of these messages are able to reach that ISP.

While it seems from the above argument that end-points (sources and destinations) need to have control over which path the packets take, this too would be sub-optimal. ISPs constitute a fundamental and important piece to the puzzle of the internet without which it wouldn't function. And so they require some path control to implement their own policies. SCiON helps in this regard by allowing ISPs some control over the path but more importantly empowering end-points to have a say over the path of datagrams. How is this done?

#### Transparency

Once again, how would we define transparency? We would like sending entities to have information about where their packet would go while traversing the internet. Simply downloading the BGP updates wouldn't give the path. Downloading the state of routing tables (of which there are lots) would be enough to determine this information, that too only probabilistically. One could put the forwarding information in the datagrams to solve this issue. And this wouldn't mean that end-points are being given a full say in the route control since the network would still define the possible forwarding information that could go into these packets.

Also under transparency falls the transparency of trust roots. Which entities does a user trust for any particular authentication, say a TLS connection to a server? Isolation Domains offer a fix by just reducing the number of roots to trust.

###### Source routing? 
Source routing allows a sender of a packet to partially or completely specify the route the packet takes through the network. This is in contrast to conventional routing, where routers in the network determine the path incrementally based on the packet's destination. There does exist some source routing in today's internet. However, this doesn't scale to inter-domain networks, as a source would require to know the network topology to determine paths. In order to be able to scale path control, SCiON lets sources select amongst a relatively small set of paths. This way, SCiON relies on source-selected paths and packet-carried forwarding-state instead of full-fledged source routing.

#### Availability

Availability is defined today in terms of *9s* (99.9% would be 3 *9s* of availability). A very interesting (and meticulously documented) paper by Katz-Bassett et al. from SIGCOMM 2012 showed how the general internet achieved 3 *9s* of availability (4 *9s* for an Amazon data center) which is equivalent to about 86 seconds (or 8.6 seconds) of unavailability each day. There are numerous short-lived outages due to BGP route changes. There are outages due to misconfigurations, route convergences, and attacks such as DDoS and prefix hijacking. 

But is it worth working so hard to devise solutions to make sure the internet is not unavailable for those extra 8.6 (or 86) seconds a day? The internet has, as I point out once again, grown far beyond what it was meant to be. It is used for the flow of sensitive mission-critical information. It has applications varying from air traffic control to remote, robot-operated surgical exercises. And then there are the services running 24 x 7. 

The only way (seemingly) to solve it? Replace BGP...
BGPSEC is an extension of BGP that fixes some of the above issues brought by BGP rather inefficiently by bringing new issues. Traffic hijacking is still a problem with BGPSec. There is no security guarantee for inter-domain routing. Essentially, extensions and scaffolding has been going on since the internet was introduced. This has brought everyone to believe that the internet has stood the test of time where in reality, it has been patched up and patched up again just to keep it working. Not the way any great engineering product should be.

#### Other Future Internet Architectures

SCiON is neither the first nor only attempt towards redefining the internet. Here's a table showing some other attempts and where their focus lies.

|Architecture|Focus|
| --- | --- |
| NIMROD | New internet routing and addressing | 
| eXpressive Internet Architecture (XIA) | Addresses the growing diversity of network use models, need for trustworthy communication, and the growing set of stakeholders who coordinate their activities to provide Internet services |
| MobilityFirst | Adopts a clean separation between identity and network location |
| Nebula | Cloud Computing |
| NewArch | Tolerance of evolving requirements, DARPA funded |
<br>

#### SCiON

And just before diving into the architecture of SCiON and the several protocols it offers, we look at the design goals for the SCiON future internet architecture. 

- High Availability: We'd like to be able to use a path as long as an attacker-free path exists. In today's internet, a compromised entity can prevent communication with surrounding entities. As long as adversaries can't have access to the management plane of a sequence of routers these sequences of routers should be able to be used for packet forwarding.

- Secure entity authentication that scales to a globally distrusted environment.

- Flexible Trust: We can operate in a heterogenous trust environment and enable end users or domains to make decisions about which entities they want to trust for entity authentication.

- Operation Transparency for clarity to sender and receiver about what is happening to their packets.

- Balance of control among ISPs and sender/receiver.

- Scalability, efficiency, and Flexibility.

#### Isolation Domains

A trust domain means to have a region in which the entities of the region can agree on who authenticates trust in that region. This region should also agree on a set of ISPs to manage the ISD core. How exactly to partition the internet into ISDs is a problem that is still being worked upon and it's possibly going to be along geographical lines. From the SCiON book, "an AS (Autonomous System) is a self-contained network administered by a single entity". An Isolation Domain (ISD) constitutes a logical clustering of such ASes. 

One problem that this solves is that faced by monopolistic and oligopolistic architectures for authentication. Both these models have in common that the scope of the key is unrestricted. The compromise of a single point (protected by modern cryptography's security guarantees) can lead to compromising billions of hosts around the world. Isolation can diminish the attack vector of these large-scale attacks by structuring entities into isolation domains. Each isolation domain has its own authorities for managing keys, limiting the scope of attacks. With SCiON, clients are enabled to choose Trust Root Configurations (TRCs) they'd like to use.

Another property such ISDs provide helps in isolation for the propagation of routing attacks. This shall be discussed in more detail while going through some attacks on BGP.

#### Beaconing for Route Discovery

The ASes in the ISD core initiate route construction beacons. Path Construction Beacons (PCBs) are a scalable and secure way of disseminating topological information. Uses a k-wise multi-path flood to provide each autonomous domain with multiple entities. How is this implemented?

The ISD core maintains a path server. Destination domains can choose paths under which they'd like to be reached and upload this to the path server in the ISD core. Consider the image shown below. If a host within the blue autonomous domain would like to reach a host in the red autonomous domain, it'll fetch the red paths from the server and combine it with the blue paths. 

<br>
<br>
<div style="text-align: center">
    <embed src="/assets/img/posts/2022-10-28-SCiON/domain-logo.png" alt="drawing" height="350" position="center"/><br>
</div>
<br>
<br>

This technique allows for a balanced route control between the endpoints and the ISPs. ISPs have control over which beacons are forwarded and which paths are being announced. Destination hosts have control over the paths they'd like to be reached under. These are the paths that they upload to a node server in the ISD core. Source hosts have control over the paths they'd like to use by means of getting to select which of the paths from the path server to use. This way, all parties have equal control over the path of packets and no single party has complete control. 

Interestingly, this also helps to separate the routing and forwarding process. Once the packet creates its black path, the control plane routing protocol can no longer influence the packet from traversing by that path. Even if there are attacks on the routing protocol, the actual data path can no longer be influenced by these attacks.

Such a system also provides transparency in forwarding. The source node knows exactly which path the packet will take. Routers no longer need to store forwarding information for the bordering routers.

Inter-ISD communication is also possible. (Please refer to the image below) End hosts can combine up-paths, inter-ISD-core paths, and down-paths for inter-ISD communication. The image on the right shows how peering links can be strategically placed to make the system more efficient.  But what happens if and when a link fails? 

<br>
<br>
<div style="text-align: center">
    <embed src="/assets/img/posts/2022-10-28-SCiON/4.jpg" alt="drawing" height="350" position="center"/>
    <embed src="/assets/img/posts/2022-10-28-SCiON/10.png" alt="drawing" height="350" position="center"/>
</div>
<br>
<br>

#### Link Failures

If the link inside an AD fails, we assume there is a separate routing protocol inside this AD that'll help the packet reach its destination. SCiON only dictates the ingress and egress within an AD. It doesn't matter how the packet traverses within an AD.

What if a border router fails? SCiON uses multi-path forwarding by default. For every socket that is created, several paths are used at the same time. For any path that fails, there is thus an alternative path to be taken. Anyways, the Path Construction Beacons (PCBs) are constantly being sent. So even if the links fail, the sender continues to receive a number of functioning beacons. When a link fails, a message is sent to the ISD core to delete all paths containing the particular link. 

#### SCiON Header

<br>
<br>
<div style="text-align: center">
    <embed src="/assets/img/posts/2022-10-28-SCiON/5.png" alt="drawing" height="350" position="center"/><br>
</div>
<br>
<br>

#### Security Applications

SCiON places more emphasis on security against other FIAs. It has a number of security applications that are built into the protocol. In order to focus on some examples, I'll just list the security applications and a link to the point where they're discussed in Prof. Perrig's 2014 talk at the CMU-CyLab.

- [Trust](https://www.youtube.com/watch?v=jpLHDw5gkbU&t=2424s)
    - Trust Root Configuration file creation
    - TRC Updation
- [Transparency](https://www.youtube.com/watch?v=jpLHDw5gkbU&t=2701s)
    - [Source Authentication](https://www.youtube.com/watch?v=jpLHDw5gkbU&t=2789s)
    - [Path Validation](https://www.youtube.com/watch?v=jpLHDw5gkbU&t=2856s)
- Availability 

#### Border Gateway Protocol (BGP)

In the article so far, we must've come across the abbreviation BGP quite a few times already (10 to be exact 🤷). This protocol (routing protocol) is essentially the postal service of the internet. When a user from Hyderabad, India loads a website with origin servers in Zurich, Switzerland, BGP is the protocol that enables that communication to happen quickly and efficiently. Before diving into BGP, let's take a briefing on Autonomous Systems (ASes). The Internet is a network of networks. It is broken up into hundreds of thousands of smaller networks known as autonomous systems (ASes). Each of these networks is essentially a large pool of routers run by a single organization. If we continue to think of BGP as the Postal Service of the Internet, ASes are like individual post office branches.

In BGP, peers are created manually between routers to initiate a TCP session on port 179. Every 30 seconds (protocol default value, adjustable), a BGP speaker delivers 19-byte keep-alive messages to sustain the connection. BGP stands out from other routing protocols in that it uses TCP as its transport protocol. Internal BGP is the term used to describe BGP between two peers within the same autonomous system (AS) (iBGP or Interior Border Gateway Protocol). It is known as External BGP when it operates between various autonomous systems (eBGP or Exterior Border Gateway Protocol). While iBGP peers can be interconnected through other intermediate routers, border or edge routers, sometimes known as eBGP peers, are routers on the edge of one AS that are exchanging information with another AS. Other deployment topologies are also feasible, such as eBGP peering inside a VPN tunnel, which enables the secure and isolated exchange of routing data between two remote locations. 

The way routes received from one peer are often propagated by default to other peers is the primary distinction between iBGP and eBGP peering:

- All iBGP and eBGP peers receive a new route announcement when it is learned from an eBGP peer. 
- Only all eBGP peers receive new routes that have been learned from an iBGP peer. 
- These route-propagation rules essentially demand a full mesh of iBGP connections between all iBGP peers inside an AS. 

The route-maps method allows for fine-grained control over how routes spread. These rules make up the mechanism. Each rule specifies what should be done when a route meets a certain set of requirements. The step could involve dropping the route or altering some of its attributes before adding it to the routing table.

#### BGP Tales

In 2004, a Turkish ISP called TTNet **accidentally** advertised incorrect BGP routes to its neighbors. These routes claimed that TTNet itself was the best destination for all traffic on the Internet. As these routes spread further and further to more autonomous systems, a massive disruption occurred, creating a one-day crisis where many people across the world were not able to access some or all of the Internet.

Similarly, in 2008, a Pakistani ISP **attempted** to use a BGP route to block Pakistani users from visiting YouTube. The ISP then accidentally advertised these routes with its neighboring ASes and the route quickly spread across the Internet’s BGP network. This route sent users trying to access YouTube to a dead end, which resulted in YouTube being inaccessible for several hours.

In 2017, a major BGP routing "incident" routes traffic for big-name sites through Russia. 80 prefixes normally announced by organizations such as Google, Apple, Facebook, Microsoft, Twitch, NTT Communications, and Riot Games were now detected in the global BGP routing tables with a previously unknown Origin AS of 39523 (DV-LINK-AS), originating in Russia. This incident was one of almost 5000 route leaks and hijacks in 2017.

All of the above attacks fall under a subset of cyberattacks on the internet that one can call BGP Hijacking. BGP hijacking is when attackers maliciously reroute Internet traffic. Attackers accomplish this by falsely announcing ownership of groups of IP addresses, called IP prefixes, that they do not actually own, control, or route to. A BGP hijack is much like if someone were to change out all the signs on a stretch of freeway and reroute automobile traffic onto incorrect exits. Here's an interesting image from a blog post by Cloudflare about BGP Hijacking that spells it out nicely.

<br>
<br>
<div style="text-align: center">
    <embed src="/assets/img/posts/2022-10-28-SCiON/6.png" alt="drawing" height="350" position="center"/><br>
</div>
<br>
<br>

While there have been security mechanisms like RPKI (Resource Public Key Infrastructure) and BGPSEC (BGP Security) bootstrapped over BGP to prevent such attacks, the folks at SCiON argue that these are just not enough and convincingly so. SCiON makes the Internet more secure through path-aware networking and preventing BGP route leaks and prefix hijacking attacks. SCiON solves both scalability and network sovereignty by organizing ASes into isolation domains based on shared jurisdictions or other criteria. The routing process is hierarchically divided into an intra-ISD (discovering paths within an ISD) and an inter-ISD procedure rather than discovering paths between any two ASes (discovering paths between ISDs). As a result, fewer pathways must be found, and fewer routing messages are thus needed. Additionally, since each ISD is able to establish its own foundation of trust (instead of relying on a single international organization like ICANN), its public-key infrastructure (PKI), which gives keys and certificates to the ASes, is immune to bad actions of outside parties.

As discussed in earlier sections, such an adaptable PKI is used by SCiON to cryptographically authenticate all routing packets, thwarting hijacking attempts. Finally, no cyclic dependencies between the PKI and the routing process can develop thanks to the integration of certificate distribution with routing.

In 2020, SIDN Labs connected to the global SCiONLab testbed, through BGP-free connections by SURF and GEANT. There's also a cool [<span style="color:red"> practical demonstration of a video-chat application on a SCION architecture <span>](https://www.youtube.com/watch?v=4KO-YP7rkHA&t=1s) that you can check out.

#### DNS vs SCiON

DNS is the directory of the internet that resolves domain names to IP addresses. DNSSEC provides authentication for DNS. Like BGPsec, DNSSEC relies on a single or very small number of roots of trust (oligopolistic trust model). As of recent, DDoS attacks have been widely used to prevent access to servers or network resources. For example, a very large attack with an unprecedented amount of attack traffic — exceeding 1 Tbps — on DNS infrastructure maintained by a company called Dyn that provides core Internet services for Twitter, SoundCloud, Spotify, and Reddit among others. SCiON recognizes the importance of scaling the authentication of entities of the internet such as ASes for routing, domains for TLS, and name servers for DNS.

SCiON's name servers are analogous to DNS servers on the current internet. SCiON proposes the RAINS system for translating a human-understandable name into a SCiON address. The system uses the (ISD, AS) tuple to look up and construct end-to-end paths. As described above, the end host as well as the end-to-end path are then placed in the SCiON packet header to enable delivery to a given destination. Path servers store mappings from AS identifiers to sets of announced path segments, which are arranged in a hierarchical caching system similar to DNS. Overall, SCiON provides 3 basic mechanisms to shield against DDoS attacks:
- Non-registered (hidden) path segments
- Short-lived paths
- Multipath communication

Here's an image showing an example Assertion space in RAINS (a cool recursive acronym for RAINS Another Internet Naming Service).

<br>
<br>
<div style="text-align: center">
    <embed src="/assets/img/posts/2022-10-28-SCiON/7.png" alt="drawing" height="350" position="center"/><br>
</div>
<br>
<br>

#### SIBRA (Anti DDoS)

Typical defenses to DDoS attacks perform traffic scrubbing in upstream ASes or the cloud, but greater bandwidth attacks. Some other defense systems/mechanisms include Quality of Service architectures at different granularities, improved network capabilities, fair resource reservation mechanisms, and a botnet-size independence property. All these have drawbacks that don't scale to the bandwidth of more recently demonstrated DDoS attacks. SIBRA (Scalable Internet Bandwidth Reservation Architecture) provides a novel bandwidth allocation system resolving these drawbacks and operating at the scale of the internet.

SIBRA provides inter-domain bandwidth allocations that let an AS guarantee a minimal amount of bandwidth to its end hosts by limiting the possible paths in end-to-end communication. An important property of SIBRA is the **per-flow** *stateless* **fast-path operation** on transit routers for renewing reservations, policing, and monitoring. This provides the efficiently scalable router operation SCiON is looking for. 

Here's a sample topology from the SCiON book showing briefly how SIBRA works in geographically divided ISDs.

<br>
<br>
<div style="text-align: center">
    <embed src="/assets/img/posts/2022-10-28-SCiON/8.png" alt="drawing" height="350" position="center"/><br>
</div>
<br>
<br>

Hidden COBRA is the North Korean botnet infrastructure being used to target critical infrastructure in the US and around the globe. SCiON claims to ensure communication despite the attacks.

#### Secure Swiss Finance Network

The Swiss National Bank (SNB) wants to open its infrastructure to innovative fintech and has developed ideas on how the Swiss financial center could benefit more from the new possibilities. The Secure Swiss Financial Network is one of the possibilities which uses SCiON to provide safety against cyber risks. The SSFN is a controlled and secure network launched by the Swiss National Bank and SIX (the Swiss Exchange). The SSFN allows all connected users in the Swiss financial center to communicate securely with SIX, among other financial market infrastructures, and also with each other.

Here's a visualization to bring into perspective how the SSFN is organized from the talk by William Boye and Fritz Steinmann on SCiON Day 2022.

<br>
<br>
<div style="text-align: center">
    <embed src="/assets/img/posts/2022-10-28-SCiON/9.png" alt="drawing" height="350" position="center"/><br>
</div>
<br>
<br>

#### Remarks

It now feels appropriate to end this blog. Don't get me wrong. A lot of topics are yet to be discussed but here I am, a few weeks into exploring this future internet architecture and its possibilities. Some questions for future blogs may be understanding how SCiON counters censorship on the internet, flaws with HTTP, and how SCiON deals with them. A crucial part of the SCiON project would be the research on path-aware networking by the recently formed PANRG of the IETF. Another paper by SCiON researchers at NDSS'22 shows how most popular VPN implementations are vulnerable to DoS attacks. SCiON packet filtering and authentication mechanisms can help mitigate this. There is also the work on Secure Backbone Autonomous Systems (SBAS) that's going to be presented in Usenix '22.

Innovations that drive mankind forward start in the imagination of visionaries. Once the visionaries figure out what it's meant to be, it's their job to show everyone the world as they see it. SCiON is a vision of a future internet that is secure, scalable, and sovereign. This vision is being made a reality by the team at Anapaya Systems. 

India, being a developing nation, is witnessing a huge demand for indigenous innovations to problems faced by the common man in the day-to-day. An example of innovation would be the hugely successful, state-developed Unified Payment Interface (UPI). An interesting problem to think about would be figuring out how this UPI could be engineered to leverage the security features provided by a SCiON internet. These are the sort of problems whose innovative solutions catapult a developing country into becoming a first-world nation. And these are exactly the sort of things that I'm excited to work on, contribute to, and simply be a part of. 

<!-- FAQ page
The SCION book (https://scion-architecture.net/pdf/SCION-book.pdf)
FOSDEM (by Mateusz Kowalski)
SCION Stories from the field
https://www.cloudflare.com/en-in/learning/security/glossary/what-is-bgp/
https://www.us-cert.gov/ncas/alerts/TA17-164A
https://www.nzz.ch/finanzen/snb-oeffnet-zahlungsverkehr-fuer-fintechs-spricht-ueber-blockchain-ld.1470845 -->