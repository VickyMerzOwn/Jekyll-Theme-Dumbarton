---
layout: post
title:  "Software Heritage"
description: "About Software Heritage, what we stand for, and where we are headed"
date:  2022-05-25 19:30:00 +0100
type: card-img-top
categories: latin text
image: 
caption:
last-updated: 2022-05-25 11:05:00 +0100
categories: Project Blog
tag: GSoC'22
author:
card: card-1
---

Mankind is currently voyaging through the age of information. This age of information has been fuelled by the internet, which is nothing but a vast network that connects computers all around the world.[^1] The web is nothing but a subset of the internet. Over time, the web has evolved and is currently in its fourth phase. Putting it in a single sentence, "`Web 1.0` was a web of internet connections, `web 2.0` was a web of people connections, `web 3.0` was a web of knowledge connections and `web 4.0`, also known as symbiotic web in which human mind and machines can interact in symbiosis, is a web of intelligence connections".[^2]

[^1]: Michael Aaron Dennis, "Internet", April 7, 2022, accessed May 25, 2022, https://www.britannica.com/technology/Internet
[^2]: Aghaei et.al, "EVOLUTION OF THE WORLD WIDE WEB: FROM WEB 1.0 TO WEB 4.0", January, 2012, accessed May 25, 2022, http://www.cbpp.uaa.alaska.edu/afef/web%20evolution%201-4.htm

The transition from `web 1.0` (worldwide accessible knowledge source) being only readable to `web 2.0` as a web of connections made it possible for people from different parts of the globe to collaborate on building software. In a way, `web 3.0` was enabled by foundations laid by `web 2.0`, and Open Source Projects flourished in `web 3.0`. So much that a 2021 estimate puts the number of open source projects on [github](https://github.com/) in 2020 at 54.21 million.[^3] One has to realize that the power of these projects, these software lies not in the executable binaries that perform tasks but in the code that resulted in the executables. To be able to build on existing source code, the source code files themselves are necessary.

[^3]: Xue (Xander) Wu, "Open Source Insights – What We Learned from 860 Million GitHub Event Logs", April 9, 2021, accessed May 25, 2022, https://www.freecodecamp.org/news/open-source-insights-what-we-learned-from-860-million-github-event-logs/


Born at the advent of `web 4.0`, <span style="color:red">Software Heritage</span> is an ambitious project whose mission is to "collect, organize, preserve, and make easily accessible all publicly available source code, independently of where and how it is being developed or distributed".[^4] Software, i.e code, controls several aspects of our day-to-day life and more. So its importance has never been felt more. SWH aims to collect, index, preserve and make easily accessible the source code of this software. All contributors to the project share this vision and believe that "Preserving software is essential for preserving our cultural heritage".

[^4]: Roberto Di Cosmo, Stefano Zacchiroli. <span style="color:red">Software Heritage</span>: Why and How to Preserve Software Source Code. iPRES 2017 - 14th International Conference on Digital Preservation, Sep 2017, Kyoto, Japan. pp.1-10. hal-01590958

The page on <span style="color:red">Software Heritage's</span> mission in the industry presents a very unique analogy. It compares the process of building a universal software archive to drawing a map of the stars. SWH tracks software origin, history, and evolution and gives unique software identifiers to various software components. So far, we have looked at what is <span style="color:red">Software Heritage</span> and why there is a need for a project like <span style="color:red">Software Heritage</span>. Now, I'd like to dive deeper into the how. How does <span style="color:red">Software Heritage</span> accomplish its goals of software source code archival.

<div style="width:50%;height:0;padding-bottom:56%;position:relative;" align = center><iframe src="https://giphy.com/embed/2A4AuksVMmWXKfJjGl" width="100%" height="100%" style="position:absolute" frameBorder="0" class="giphy-embed" allowFullScreen></iframe></div><p><a href="https://giphy.com/gifs/internet-cyberspace-surfing-the-net-2A4AuksVMmWXKfJjGl"></a></p>

The major components are data storage, the journal, source-code scraping, and the scheduler. Storage's role is to provide a means by which elements of the graph can be stored or retrieved. The journal does essentially what human beings do with journals: it logs every change in the archive, with publish-subscribe support using `Kafka`. For example, the storage publishes a Kafka message in the journal every time a new object is added to the archive. The source code scraping carousel consists of listers, loaders, scheduler's generic task management, scheduler's listing, and visit stats, and the scheduler's origin visit scheduling. While listers scrape a website like a forge and gather all source code repositories, loaders are responsible for importing source code from these repositories. The scheduler can be explained as the choreographer of jobs in SWH.

<img src="/assets/img/posts/2022-05-26-Software-Heritage/img2.png" alt="drawing" width="600"/>

Additionally, <span style="color:red">Software Heritage</span> has the archive website and API (known as swh-web), indexers, and the vault. It also provides tools such as `swh-search`, `swh-graph`, `swh-counter`, `swh-deposit`, and `swh-auth`. To access the archive via API, SWH provides the:
- [SWH Web Client](https://docs.softwareheritage.org/devel/swh-web-client/index.html#swh-web-client)
- [SWH Filesystem - FUSE](https://docs.softwareheritage.org/devel/swh-fuse/index.html#swh-fuse)
- [SWH Code Scanner](https://docs.softwareheritage.org/devel/swh-scanner/index.html#swh-scanner)

My project in <span style="color:red">Software Heritage</span> for GSoC 2022, titled "Mine information from Archived Content", extends the functionality of the indexer. There are two parts to the project. In the first part, I will work on mining intrinsic metadata from archived repositories. The second part focuses on extrinsic metadata. This link contains a description of the metadata workflow and architecture. The CodeMeta initiative’s crosswalk table provides a framework for translating software metadata into a convenient and common vocabulary. Once some filename-based heuristics indicate a file to be a metadata file, it is fetched and translated into `CodeMeta` metadata (JSON) format. The figure below is an example sequence that follows in obtaining metadata of NPM-managed projects in the archive.

<img src="/assets/img/posts/2022-05-26-Software-Heritage/img1.png" alt="drawing" width="600"/>

<span style="color:red">Software Heritage</span> is the first open source project that I shall contribute to after the projects hosted openly in our university. I am fortunate to have been given this opportunity. Looking forward to contribute to the <span style="color:red">Software Heritage</span> project!
<br>
<br>
<br>
### Sources


<!-- ![alt text for screen readers]( "Text to show on mouseover") -->