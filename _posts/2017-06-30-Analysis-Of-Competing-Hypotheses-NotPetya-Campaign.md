---
layout: post
title: Analysis of Competing Hypotheses - NotPetya (Ransomware) Campaign
published: true
date: 2017-06-30 18:45:35
categories: [Ransomware, Wiper, Petya, NotPetya, Malware, Campaign, ACH]
---

{% assign imagedir = "/images/" | prepend: site.baseurl | prepend: site.url   %}


After *Wannacry* spreading around the world looking to use NSA exploit known as *EternalBlue*, a variant of the *Petya* family of ransomware came out. This new variant has been called *NotPetya* (not to mix with the first Petya campaign) by Kaspersky.

According to numerous researches and evidences, this campaign might not be just a ransomware ... but *a wiper* ... 
 
Having said that, I wanted to prove this theory following the well-known methodology (["Analysis of Competing Hypotheses" (ACH)](http://competinghypotheses.org/docs/The_ACH_Methodology_and_Its_Purpose).

So, this post is not about technical evidences, fancy decompilation, but instead will try to follow this method and conclude on which hypotheses is the most plausible.
 
In *Threat Intelligence*, an analyst will have/need to perform assessments with incomplete information and/or inaccurate details. Thus, hypotheses will be needed and formed, and evidences supporting them will be drafted unconscientiously. This type of approach does not take into account alternate hypotheses or others evidences.
 
ACH methodology is supposed to correct this issue and help analysts to understand what is most likely.
 
The first step is to come up with hypotheses (they don't cover 100% of all possibilities but they are a good start):
* H1 - A sophisticated financially motivated cybercriminal (group)
* H2 - An unsophisticated financially motivated cybercriminal (group)
* H3 - A nation state or state affiliated organisation crime tending to cause a disruption in Ukraine
* H4 - A nation state or state affiliated organisation crime tending to cause a worldwide disruption
 
Next, high and medium level evidences need to be collected for and against those hypotheses:
 
**Initial infection vector**
* Petya was deployed to machines by hacking "MeDoc" Ukranian software company and using the update feature
* No evidence (yet) Petya was deployed using phishing email
 
**Installation-Propagation**
* Exploitation of SMB vulnerability to propagate
* Use of Psexec, Wmic to propagate
* Use of DHCP service to identify known hosts
* Use of Mimikatz for authentication reuse
* Use of EternalBlue and EternalRomance exploit
* No operator input needed for encryption
* Petya only spread by scanning the company internal network where it is deployed
 
**Activity**
* The Killswitch used prevent the malware to be executed on the system but not to spread on the internal company network
* The malware delete any logs on the system and then, proceeds so that the system will not record any further changes on the system
* The malware encrypt the Master Boot Record if running with administrative privileges
* The malware encrypt the user-space if running without administrative privileges
* The malware does not keep a copy of the old Master Boot Record encrypted and replace by malicious code displaying ransom note
* The hard drive encryption only starts 1h after the infection and the system rebooted
 
**Ransom**
* Email address that was used to contact for the recovery key was suspended rapidly
* Only one email address was used for the recovery key
* Only one BTC wallet used
* Victims who paid did not receive decryption keys
* Ransom demand 300 USD per machine rather than against individual organisation
 
**Activity in the wild - (Geo) localisation**
* Majority of victims are in the Ukraine
* This campaign has touched crucial infrastructure included central bank, airport, metro transport, etc.
* This wide ransomware campaign are not financially profitable (vs Wannacry)
 
**Other**
* Media narrative around this campaign
 
 
Then, a matrix needs to be created analysing each evidence against every hypotheses by defining whether they is correlation or contradiction. If the evidence is not relevant to any hypotheses, they will need to be removed (grey) from the matrix.
 
For this purpose, we will use this scoring:

![ACH-scoring-petya.jpg]({{ "ACH-scoring-petya.jpg" | prepend: imagedir}} | width=100))  

And the matrix is ...

![ACH-matrix-petya.jpg]({{ "ACH-matrix-petya.jpg" | prepend: imagedir}}) 


### Conclusion

Plenty of other hypotheses can be used to enhance this model and increase confidence. This methodology is not widely used worldwide yet even if it shows good result without using too many biases.
 
According to this result and the **data-information-knowledge available at this time**, we can see that a nation state or state affiliated organisation crime tending to cause a disruption in Ukraine is the most plausible scenario.
 
If any disagreement about the result, or any feedback regarding the scoring-workflow, I would be happy to exchange about it.

*References*
* https://sroberts.github.io/2016/12/12/rnc-hack/
* https://www.digitalshadows.com/blog-and-research/wannacry-an-analysis-of-competing-hypotheses/
* https://www.digitalshadows.com/blog-and-research/leak-on-aisle-12-an-analysis-of-competing-hypotheses-for-the-tesco-bank-incident/

