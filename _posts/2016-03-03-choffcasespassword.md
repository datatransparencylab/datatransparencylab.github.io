---
layout: default
title: "The Curious Case of the Exposed Password
"
blurb: "Researchers at Northeastern University identified more than 20 iOS, Android, and Windows Phone apps that exposed users’ credentials, including passwords, to eavesdroppers. Their experience with password vulnerabilities was generally positive in the end, but there’s still room for improvement. They contacted developers to fix these security vulnerabilities, and what they learned was both surprising and enlightening."
date: 2016-03-03 12:00:00 +0100
categories: News
type: blog
author: "David Choffnes"
---

<div class="post-container">
<h3>The Curious Case of the Exposed Password</h3> 

<div class="author">
<a href="mailto: choffnes@ccs.neu.edu"> {{ page.author }} </a>
<p>Northeastern University</p>  
</div>

<div class="post-date">
{{ page.date | date_to_string }}
</div>



<div class="post-body">

<div class="blurb">
{{ page.blurb }}
</div>
 
 



 <h5>Story:</h5>


<p>We started with a simple idea: identify how much of users’ personal information is exposed over the Internet when using mobile apps, and allow users to do something about it. This idea led us to create the <a href="">ReCon project </a>, which hundreds of people worldwide use to understand their privacy when using mobile devices.</p>

<br>

 <h5>On the Internet, Everyone Knows You’re a Dog</h5>

<p>As you use mobile devices with Internet connections, not only are you fetching interesting information (e.g., Facebook posts, tweets, news, and weather), you are probably also sharing personally identifiable information (PII) such as your name, email address, GPS location, gender, sexual orientation, and credentials such as username and passwords for logging into apps. There are many legitimate reasons for apps to send PII over the Internet --- for example, your navigation apps like Google Maps and Waze need to know your location to give you real-time driving directions. Ideally, this information is protected from eavesdroppers using encryption; however, <a href="http://recon.meddle.mobi/app-report.html">we have found substantial information exposed in plaintext.</a> Like the famous New Yorker cartoon about the <a href="https://en.wikipedia.org/wiki/On_the_Internet,_nobody_knows_you%27re_a_dog#/media/File:Internet_dog.jpg">dog using the Internet</a>, <a href="http://newyorker.tumblr.com/post/111446912131/a-cartoon-by-kaamran-hafeez-from-this-weeks">anyone can know who you are </a> based on your mobile device’s Internet traffic (even if you are a dog).</p>

<br>
<div class="row">
	 <div class="col-md-6">
 
	 	 <img class="img-responsive" title="Dogs via New Yorker" src="/images/posts/choff2.jpg"> 
 			 <figcaption>"On the Internet, nobody knows you're a dog." <br>(source:<a href="https://en.wikipedia.org/w/index.php?curid=13627120">Wikipedia</a>)
		  </figcaption>
		  </div>
	
<br>
	<div class="col-md-6"> 
		<img class="img-responsive" title="" src="/images/posts/choff1.jpg"> 
		  <figcaption>"Remember when, on the Internet, nobody knew who you were?" <br>(source: <a href="http://www.newyorker.com/cartoons/issue-cartoons/cartoons-february-23-march-2-2015-issue?mbid=social_tumblr">The New Yorker</a>)
		  </figcaption>
	</div>
 </div>
 <br> 
<br>

<p>Perhaps the most sensitive PII for users is their login credentials, namely usernames and passwords. An eavesdropper who obtains this information can impersonate the user and get access to their online accounts. Further, because users often use the same password to access multiple sites, a single password exposed to an eavesdropper could lead to the compromise of many accounts, from Facebook to online dating and banking sites.</p>


 <h5>An Unexpected Discovery</h5>

<p>Because passwords are so important, we did not expect to find any of them exposed in Internet traffic in our study. Instead, as of this writing we have found 20 apps suffering from this security vulnerability and potentially millions of users, including those we trust with access to our medical records, were affected.</p>


<p>You may be wondering how we did this. Our ReCon project is based on a simple premise: because PII is generally exposed only when it is sent over the Internet, we can identify cases of this by inspecting a mobile device’s network traffic. While it’s easy to find exposed PII if you know exactly what it is (e.g., treat the network traffic like a text file and search for “P@ssw0rd”), it is difficult when you do not know the PII in advance. We developed a system that uses machine learning to identify when PII is exposed without needing to know any specific details about the PII being exposed. In other words, we can tell when your password is exposed without knowing what your password is.</p>

<p>We ran hundreds of apps through ReCon and found passwords exposed by apps ranging from dating to medical reference information, and streaming music to movie ratings. One such app, Match, was used by millions of users. Another, Epocrates, is used by hundreds of thousands of medical professionals.</p>

<p>The implication of this revelation was troublesome at best. If you’ve used the popular Match dating app, someone else could have learned your credentials.<em>Did you reuse that password anywhere else? And what about your medical professional? If their password was exposed, what other medical systems could be accessed using this password?</em></p>

<p>Importantly, not a single user had any idea this was happening. We wanted to tell the world, let everyone know about this problem. But therein lies a problem: if we tell the world, then every bad guy will also know about the problem and might try to exploit it. This is a common problem in the security research community, one solved by <em>responsible disclosure.</em></p>


 <h5>Responsibly Disclosing Irresponsible Behavior</h5>

<p>Security vulnerabilities put users at risk, and ethics dictates that we should minimize and/or eliminate this risk as quickly as possible. Therein lies a tension. On the one hand, we could tell users as quickly as possible so they can stop using affected software. However, any users who don’t hear the news would be at risk from attack from bad guys who learn about the problem. </p>

<p>On the other hand, we can privately work with developers to fix the problem as quickly as possible, but users would still be at risk until the fix is released. Responsible disclosure balances these two concerns.</p>

<p>While there is no standard for how to conduct responsible disclosure, it generally works as follows: tell the developer, give them some time to fix the vulnerability, then notify users after the problem is fixed. If the developer does not respond or does not fix the problem in a timely manner, then notify the public after a reasonable waiting period. We followed this approach, and gave developers three months to fix the password vulnerabilities.</p>
<p>In all of the cases we discovered, there is a trivially easy fix: use standard encryption software to transmit user credentials. If you’ve ever seen a padlock in the location bar of your browser, this is what we are talking about.  There is standard, free, and easy-to-use software that does this. For many apps, this requires changing one line of code. In other cases, it may require a small change to their servers as well.</p>

<p>In short, the time required to fix the password vulnerabilities we discovered should have been short (an hour or two of labor) for every app. We began the process of disclosure in November, 2015. At the time of this writing --- nearly four months later --- many apps are still vulnerable. What follows is the story of how various developers reacted – and did not react – to our disclosures.</p>



<h5>Responsive, Confused, Indignant, and Silent</h5>

<p>Our disclosure emails were straightforward. To paraphrase, we wrote: we found that your app is exposing passwords in plaintext; please acknowledge this message and fix this as soon as possible. If we did not get a reply the first time, we sent two more emails over three months to give developers a chance to respond. If they did not fix the problem at that time, we disclosed the vulnerability publicly.</p>
<p>The reactions we received from developers and security teams were scattered across the spectrum from professional and prompt to indignant, confused, and silent. There are lessons to be learned in the responses to our disclosures, ones that will hopefully help us move to a more secure mobile ecosystem. Below, we provide vignettes describing our disclosure process, highlighting challenges that include difficulty reaching developers, explaining the risks when exposure was downplayed, and deciding to go with public disclosure when we received no response.</p>

<div class="blog-subsection">
<h6 style="font-style: oblique; text-decoration: underline;">Epocrates</h6>
<p>The Epocrates iOS app is a digital reference for medical professionals, the equivalent of a pocket reference book for diseases, treatments, and medication. We notified the team of the vulnerability in November, 2015. After a couple of weeks of silence, we received an email from their security team, where they asked to schedule a phone call to discuss.</p>
<p>It ends up that the delayed response was because we had contacted their support@ email address, and not security@. The former is meant for issues affecting app functionality (e.g., the app crashes), and the latter for security issues like exposed passwords. We learned that most companies have a security@ email address (for example, security disclosures for foo.com should be sent to security@foo.com) meant specifically for such issues, and we should include this for any future disclosures.</p>
<p>The Epocrates team reacted swiftly to our disclosure and kept us in the loop along the way. First, they immediately patched the app and released it to the public. In addition, they identified the software development process that led to the problem and put in place measures to prevent this from ever happening again. But they didn’t stop there.</p>
<p>To minimize the risk to their users, they asked us to hold off on public disclosure. The reason is that releasing a new app doesn’t mean that users will install it. And those who haven’t updated are still at risk once the vulnerability is disclosed publicly.</p>
<p>We agreed to postpone while they reached out to users via different communication channels to encourage updates. After two months of outreach, the Epocrates team determined that they had exhausted all reasonable strategies to encourage upgrades to app software, and publicly disclosed the vulnerability and their remediative actions.</p>
<p>Among all app developers we contacted, the Epocrates team was the most responsive, and was the most transparent in terms of keeping us (and eventually their users) in the loop with respect to their actions.</p>


<h6 style="font-style: oblique; text-decoration: underline;">Gaana</h6>
<p>This iOS/Andriod app is popular for streaming music in India, much like Spotify is popular in Western countries. When we tried to contact Gaana, we found that the only way to submit our message was via a Web form that limited text length to a couple hundred characters. We reformatted our standard disclosure text into a tweet-like missive and fired it off. To their credit, after a few weeks Gaana had responded to the disclosure, and they fixed the vulnerability soon after that. Unfortunately, this was not enough to protect users – Gaana was <a href="http://thehackernews.com/2015/05/gaanacom-hacked-10-million-users.html">famously hacked</a> and their entire database of user information was compromised.</p>

<h6 style="font-style: oblique; text-decoration: underline;">Match</h6>
<p>Match.com, the popular dating website, received much negative publicity for <a href="http://www.esecurityplanet.com/network-security/researcher-uncovers-match.com-security-flaw.html">exposing user passwords on laptop/desktop Web browsers in early 2015</a> and quickly moved to fix that vulnerability. However, we discovered in November, 2015 that their Android app was still affected by the same problem. We notified Match.com and received no response for a month. At that point, a member of the security team emailed to say that they are looking into the reported problem. After another few weeks, we contacted Match for a status update and they replied that they were still looking into the problem but it would take extra time due to the Christmas holiday. We received no further update from Match but noticed in late January that a new version of the app had fixed the vulnerability, at which point we went public.</p>
<p>
Interestingly, the security team reached out to us in February after public disclosure to schedule a phone call to discuss the vulnerability we reported to them. (Note that we found it is common to discuss any details over phone instead of email, presumably to reduce the “paper trail” that would provide evidence of the vulnerability.) We asked them why they wanted to meet now, especially since they had already fixed the problem, and we never heard from them again.
</p>

<h6 style="font-style: oblique; text-decoration: underline;">MocoSpace</h6>
<p>This iOS/Android chat app was not only exposing user login information, but also the contents of their instant messages, to any potential eavesdropper. We notified the developer, who within two weeks released a new version of the app that protected credentials. However, the developer <em>did not secure the contents of the instant messages,</em> which remain exposed to eavesdroppers today, because they “do not claim to be a secure messaging app.”</p>
 
<h6 style="font-style: oblique; text-decoration: underline;">AirG</h6>
<p>This Android app exposed passwords in plaintext, and the developer has since addressed this vulnerability. Interestingly, the developer noted that logins for their website were to remain exposed -- if they use encryption to protect passwords, then users accessing their site from feature phones (i.e., phones that are not “smart” and do not have full-fledged Web browsers) will not be able to access the content. This was first instance where a developer indicated that exposing credentials <em>was intentional.</em></p> 

 
<h6 style="font-style: oblique; text-decoration: underline;">TriviaCrack</h6>
<p>This Windows Phone app currently exposes users’ passwords during login. The developers have fixed this issue with iOS and Android apps, but are <em>currently unable to fix it on Windows Phone</em> because they used a third-party vendor to develop the app and that vendor will not give them an ETA for remediation. If anything, this demonstrates the danger of relying on outside services to manage software that might have critical security vulnerabilities.</p> 

<h6 style="font-style: oblique; text-decoration: underline;">The Silent</h6>
<p>We contacted WapLog, RV Parks, TalkBox, and Qunyou to notify them of password vulnerabilities more than three months ago. <em>To this day we have yet to receive a single response.</em> We decided to go public with these vulnerabilities because it was clear that the developers were not protecting users’ credentials, and the best/only way to mitigate their risk of exposure was to announce it publicly to dissuade use of the apps (and encourage users to change their passwords).</p> 
</div>

<h5>The Way Forward: Continuous Transparency</h5>

<p>Our experience with password vulnerabilities was generally positive: most of the cases are now fixed and developers in general took corrective action within reasonable time frames. However, our study highlights an important issue --- password vulnerabilities will not all disappear overnight, and it is likely that more will appear over time. </p>

<p>We were able to find these vulnerabilities because we started to look in places where most users and researchers previously could not. We have been, metaphorically, turning over rocks in the soil to expose the creatures and bugs that hide out of plain sight. We believe that for a more secure mobile Internet experience, the only way forward to is to continue this approach of improving transparency for users and for the developers of apps who unknowingly put users’ privacy and security at risk. </p>

<p>To that end, we have made our ReCon system available to the public, and plan to continue growing this project to support more users and more network environments (e.g., in home networks to control PII leaked by “Internet of Things” devices). To learn more, visit <a href="http://recon.meddle.mobi">http://recon.meddle.mobi</a>, or contact the author at <a href="mailto:choffnes@ccs.neu.edu">choffnes@ccs.neu.edu</a>.</p>
 

 

<!-- close post body -->
</div>
</div>
