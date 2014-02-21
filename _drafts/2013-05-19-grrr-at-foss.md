---
layout: post
title: "Response to a grumble regarding FOSS"
excerpt: "Virtual Dedicated Servers are wonderful things; th"
tags: 
- development
- rant
published: true
---

<p>Virtual Dedicated Servers are wonderful things; they're cheap, fill a gap, can be recycled or upgraded, and when no longer needed can be cancelled. I've been using them for years with various providers including <a href="//mediatemple.com">media temple</a> and <a href="//bytemark.co.uk">bytemark</a>. However, they usually suffer from the same problem as hardware servers - they have one location, and when the connectivity goes down for that location, your box is not only virtual but virtually useless. This bit hard recently at the office &#8213; and worse it bit twice in the same month; with one provider the load-balancer to two hardware servers had its plug pulled, and another provider lost connectivity to their datacenter due to some routing issues. These are just two of the 6 downtime events in the last year, all out of our control, with providers who are asking a lot of money for "guaranteed" up-time.</p> 

<p>The recent advances in cloud-computing from Amazon tout solutions to the problems we've experienced, so I spent a little time getting-to-grips with Amazon's EC2. As with all these excursions into the unfamiliar parts of the internet and it's technologies I soon became perplexed by the amount of semi-ambiguous buzz-words.</p>

<p>As far as I understood EC2 before reading the docs it was a cloud in which your virtual server/servers lived, with advanced options for storage and routing domains, and that's still my understanding having played with the service, but the Amazon docs served only to confuse me.</p>

<p>After reviewing the Wikipedia article in search of a higher-level explanation, the flow of information pulled me to this screen: <a href="//open.eucalyptus.com/">http://open.eucalyptus.com/</a></p>

<p>Here is the opening paragraph:</p>
<blockquote>Eucalyptus - Elastic Utility Computing Architecture for Linking Your Programs To Useful Systems - is an open-source software infrastructure for implementing "cloud computing" on clusters. The current interface to Eucalyptus is compatible with Amazon's EC2, S3, and EBS interfaces, but the infrastructure is designed to support multiple client-side interfaces. Eucalyptus is implemented using commonly available Linux tools and basic Web-service technologies making it easy to install and maintain.</blockquote>

<p>From that paragraph all I could glean was that it was called "Eucalyptus", which was an acronym, and that it is compatible with EC2. I've been using open-source tech for 10 years, I've been using virtual servers for 5 years, and I'd just set up an EC2 instance, but for the life of me I couldn't grok what Eucalyptus is. That's probably due to my poor grip of the terms they use than my understanding of the technologies they build upon or the techniques they employ.</p>

<p>I've seen it a lot with open-source projects; the very clever guys who design and build these libraries obviously have years on me and my peers in terms of development, and it shows in the descriptions they write for these projects. They're developers - they're used to writing terse copy to describe what they're doing for other developers. There's nothing wrong with that.</p>

<p>Except that they often forget not everyone who would like to be use their code is at their level.</p>

<p>The Eucalyptus website annoyed me as I couldn't at a glance grep whether the project was going to be useful to me. And what does any self-respecting geek do when they're annoyed?</p>

<a href="//twitter.com/digitala/status/1835091159"><img style="border: 0" src="//static.digita.la/2009/05/19/Tweet.png" alt="Original Tweet: All opensource projects should treat visitors to their homepage as though they've never heard of the project, or even computers, before." /></a>

<p>Frustration satiated, I moved on to breaking my amazon instance via incorrectly formed iptable rules, and thought nothing more of the subject.</p>

<p>Twitter is a remarkable thing. You post a random thought and happy with it out in the world you forget that other people can see them. And respond.</p>

<a href="//twitter.com/kamaelian/status/1835997226"><img style="border: 0" src="//static.digita.la/2009/05/19/TweetResponse.png" alt="Response tweet: @digitala Concrete suggestions as to how to apply that maxim to the kamaeila website very welcome :-)" /></a>

<p>The <a href="//www.kamaelia.org/">kamaelia project</a> is a great example of the <em>correct</em> way to do it. The intro paragraph gives me a basic understanding of what it is, and the code examples help to illustrate the ease with which it can be used.</p>

<p>Sticking to the concept of my tweet, however, there could be some changes made:</p>
<blockquote>In Kamaelia you build systems from simple <del>components</del> <ins>chunks of code</ins> that talk to each other. This speeds development, massively aids maintenance and also means you build <del>naturally concurrent software</del> <ins>software which naturally follows some of the more advanced programming techniques, such as concurrency (or running multiple tasks simultaneously)</ins>. It's intended to be accessible by any developer, including novices. It also makes it fun!</blockquote>

<p>I'm not a copywriter, and I'm sure they'd be able to enhance it further, but I just want to illustrate the point - sometimes the words you use when describing a technology are just too ambiguous for the people reading it.</p>

<p>Thankfully the fix is simple: <strong>Imagine all your visitors are on the first day of a CS course, and that english is their second language.</strong></p>
