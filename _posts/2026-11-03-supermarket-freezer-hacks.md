---
layout: post
title: "Hackers Heated Europe's Supermarket Freezers to 50°C. Why Is a Fridge So Easy to Break Into?"
date: 2026-11-03 10:01:12 +0200
categories: [Explainers]
summary: "Two waves of attacks have spoiled food in hundreds of European shops without a single piece of malware. The weak point is a box most people never see: the refrigeration controller that technicians reach over the internet. Here is how it works, who might be behind it, and why fixing it is harder than it sounds."
image: /assets/img/2026-11-03-supermarket-freezer-hacks.jpg
image_alt: "A dark, empty supermarket freezer aisle at night, its fogged glass doors glowing warm orange inside, with a small control panel showing a red light on the wall"
sources:
  - title: "The Record: Second wave of suspected cyberattacks hits supermarket freezers across Europe (2 November 2026)"
    url: "https://therecord.media/cyberattack-grocery-freezers-europe"
  - title: "The Guardian: Who is hacking Europe's supermarket fridges and freezers, and why? (2 November 2026)"
    url: "https://www.theguardian.com/technology/2026/nov/02/europe-supermarket-fridges-freezers-who-hacking-why"
  - title: "AP: Supermarket freezers across Europe hit by suspected cyberattack"
    url: "https://apnews.com/article/europe-supermarkets-freezers-cyberattacks-a8ea5b30d67da47957769f29101fe686"
  - title: "ERR News: Hackers raised freezer temperature at Estonian supermarket chain to +50°C"
    url: "https://news.err.ee/1610183296/hackers-raised-freezer-temperature-at-estonian-supermarket-chain-to-50-c"
  - title: "Censys: European refrigerator controller redux, a new wave of refrigeration attacks"
    url: "https://censys.com/blog/european-refrigerator-controller-redux-a-new-wave-of-refrigeration-attacks/"
  - title: "CERT-FR alert CERTFR-2026-ALE-012: attacks on remote controllers of refrigeration installations"
    url: "https://www.cert.cyber.gouv.fr/alerte/CERTFR-2026-ALE-012/"
  - title: "SecurityWeek: Supermarket refrigeration attack widens to Copeland, Dixell controllers"
    url: "https://www.securityweek.com/supermarket-refrigeration-attack-widens-to-copeland-dixell-controllers/"
  - title: "AP: Cyberattack disrupts supermarkets in France, raises food supply security fears"
    url: "https://apnews.com/article/france-supermarkets-hacked-cybercrime-81c2d5721f4df77f601f71741ef7c291"
  - title: "CNN: What to know about the cyberattack that targeted supermarket refrigeration systems in France"
    url: "https://www.cnn.com/2026/10/14/europe/france-cyberattack-supermarket-fridges-intl"
  - title: "FortiGuard Labs: OT refrigeration control systems attack (threat signal)"
    url: "https://www.fortiguard.com/threat-signal-report/6553/ot-refrigeration-control-systems-attack"
  - title: "Forescout Vedere Labs: Cold chain, open control, exposed refrigeration systems reveal global risk"
    url: "https://www.forescout.com/blog/cold-chain-open-control-exposed-refrigeration-systems-reveal-global-risk/"
  - title: "Kaspersky ICS CERT: H1 2022, a brief overview of the main incidents in industrial cybersecurity"
    url: "https://ics-media.kasperskycontenthub.com/uploads/2022/09/kaspersky-ics-cert-h1-2022-a-brief-overview-of-the-main-incidents-in-industrial-cybersecurity-eng.pdf"
  - title: "CISA: IRGC-affiliated cyber actors exploit PLCs in multiple sectors, including US water facilities (AA23-335A)"
    url: "https://www.cisa.gov/news-events/cybersecurity-advisories/aa23-335a"
  - title: "Krebs on Security: Target hackers broke in via HVAC company (2014)"
    url: "https://krebsonsecurity.com/2014/02/target-hackers-broke-in-via-hvac-company/"
  - title: "European Commission: Cyber Resilience Act"
    url: "https://digital-strategy.ec.europa.eu/en/policies/cyber-resilience-act"
  - title: "European Commission: Cyber Resilience Act reporting obligations"
    url: "https://digital-strategy.ec.europa.eu/en/policies/cra-reporting"
  - title: "Finnish Food Authority: the NIS2 cybersecurity directive in the food sector"
    url: "https://www.ruokavirasto.fi/en/foodstuffs/food-sector/setting-up-a-food-business/kyberturvallisuusdirektiivi-nis2-elintarviketoimialalla/"
  - title: "Danfoss: 5 ways connected monitoring and management systems can save food retailers money"
    url: "https://www.danfoss.com/en/service-and-support/articles/dcs/5-ways-connected-monitoring-and-management-systems-can-save-food-retailers-money-right-now/"
---

In the early hours of Monday, 2 November, supermarket managers in Sweden, Belgium, Ireland, Estonia, the Netherlands, Luxembourg and Finland came in to find their freezers blowing hot air. "We can't adjust the temperatures, we can't change them. Heat is blowing into the freezers. Everything is ruined," one store manager in southern Sweden [told TV4](https://therecord.media/cyberattack-grocery-freezers-europe). Some units had been set remotely to 50°C.

It was the second wave in three weeks. On 11–12 October, attackers did the same to about 700 of France's roughly 10,000 supermarkets, according to the French finance minister, [as reported by SecurityWeek](https://www.securityweek.com/supermarket-refrigeration-attack-widens-to-copeland-dixell-controllers/). At Intermarché, units ran at 50°C for six hours and all the food was thrown away; the chain spoke of losses of ["tens of millions of euros"](https://apnews.com/article/france-supermarkets-hacked-cybercrime-81c2d5721f4df77f601f71741ef7c291) in a single day. The EU called the November wave "a deliberate attempt to disrupt our food supply chain", [according to the Guardian](https://www.theguardian.com/technology/2026/nov/02/europe-supermarket-fridges-freezers-who-hacking-why).

No one has claimed either wave. But how it was done is much clearer than who did it, and that is the part worth understanding.

## The box behind the freezer aisle

A supermarket's chilled cabinets are not run one by one. A supervisory controller, a small computer in a back room, watches every unit, sets temperatures and schedules the defrost cycles that stop ice building up. Refrigeration contractors usually maintain these systems for many shops at once, so the controllers are built to be reached remotely. That is not an accident of careless shops: Forescout, a security firm, found that the manufacturers' own installation guides [describe opening the router](https://www.forescout.com/blog/cold-chain-open-control-exposed-refrigeration-systems-reveal-global-risk/) so the controller can be reached from outside.

France's national cyber-emergency team, CERT-FR, [named the affected products](https://www.cert.cyber.gouv.fr/alerte/CERTFR-2026-ALE-012/): Danfoss AK-SM and AK-SC controllers and Copeland and Dixell XWEB systems. Danfoss and Copeland both said most hit devices were [discontinued products](https://www.cnn.com/2026/10/14/europe/france-cyberattack-supermarket-fridges-intl) that no longer received security updates. Researchers had published flaws in these controllers, including an [authentication bypass](https://www.fortiguard.com/threat-signal-report/6553/ot-refrigeration-control-systems-attack), before the attacks, although French authorities have not said which weakness, if any, was used.

The striking thing is that no malware was needed. The attackers used the controllers' normal functions: change the setpoint, start a defrost, and wait. A Sophos researcher compared it to ["wearing rubber gloves and messing with the switches"](https://www.theguardian.com/technology/2026/nov/02/europe-supermarket-fridges-freezers-who-hacking-why). The timing, in the middle of the night, meant staff were least likely to notice before the food was lost.

## How many are exposed?

Scanning the public internet, Forescout counted 6,017 addresses in 99 countries and territories showing refrigeration management interfaces, from Danfoss, Copeland, Carel and others. For one Danfoss model, 80% of the visible interfaces ran firmware older than the patched version. Several European countries beyond France, including Italy, Greece and Belgium, have [many exposed systems](https://www.theguardian.com/technology/2026/nov/02/europe-supermarket-fridges-freezers-who-hacking-why), Forescout told the Guardian.

There is some good news. Before the French attack, the search engine Censys saw 1,825 exposed Danfoss StoreView systems in France; three weeks later it saw 220. In Belgium [68% of the remaining ones](https://censys.com/blog/european-refrigerator-controller-redux-a-new-wave-of-refrigeration-attacks/) looked patched. A Belgian installer, Sabcobel, said damage on 2 November would have been far worse had it not started patching after the French attack, but also that some units needed physical changes, not just a software update.

## This is not new

Attacks through building systems have a long history. In 2013, thieves got into the American retailer Target's network using credentials stolen from a [refrigeration and air-conditioning contractor](https://krebsonsecurity.com/2014/02/target-hackers-broke-in-via-hvac-company/) and went on to steal around 40 million card records. The contractor said its link to Target was only for billing and project work, not for controlling equipment, but the lesson stuck: whoever maintains the cooling also holds a key to the building. In late 2023, a group linked to Iran's Revolutionary Guards, called CyberAv3ngers, took over at least 75 industrial controllers in the United States, many in water utilities, often [because the default password had never been changed](https://www.cisa.gov/news-events/cybersecurity-advisories/aa23-335a).

Refrigeration specifically has been hit before, and from more than one side. On 26 February 2022, two days after Russia invaded Ukraine, an intruder calling themselves "Supervisor" got into the refrigeration monitoring network of a frozen-food hub near Moscow and changed the settings from −24°C to +30°C in a store holding 40 tons of meat and fish, according to a [Kaspersky industrial-security review](https://ics-media.kasperskycontenthub.com/uploads/2022/09/kaspersky-ics-cert-h1-2022-a-brief-overview-of-the-main-incidents-in-industrial-cybersecurity-eng.pdf). Danfoss later said 16 Russian supermarkets and 40 Israeli stores had been hit that year. And since January 2026, Forescout has logged more than 20 claimed attacks on refrigeration in Europe, mostly by the pro-Russian hacktivist groups Z-Pentest Alliance and NoName057(16), aimed at fruit stores, wineries and supermarkets in Spain, Italy and elsewhere.

## Who could be behind it?

There are several plausible scenarios, and the evidence does not yet pick one.

- **A state, or a group working for one, demonstrating capability.** Sophos's Rafe Pilling named state signalling as one of his two most plausible explanations. The Guardian notes that Western intelligence chiefs say Russia is running a sabotage campaign in Europe, and that Chinese-linked hackers are also in the frame. Empty freezers are frightening in a way that a stolen database is not.
- **Hacktivists.** Pro-Russian groups have been doing smaller versions of exactly this all year, and we know about those attacks because they claimed them. The silence this time is, to my reading, unusual for such groups.
- **A lone or criminal hacker.** Pilling's other main scenario. The attack is simple enough for one skilled person. Criminals seem less likely, because there was no ransom demand, and the damage is done before anyone could pay.
- **Copycats.** The second wave may not even be the same people as the first. No authority has linked them.

Belgium's cyber agency put it bluntly: "It is not known who is behind this attack, and it may never be possible to identify them." Its spokesperson also said the agency was worried about a rise in vulnerabilities found and used with the help of AI, while adding that it did not know whether AI was used here. Pointing at Moscow may feel natural in today's Europe, but the 2022 attacks on Russian food stores are a reminder that this tool is available to anyone with a grudge.

## Why the fix is harder than "just patch it"

The obvious advice, which CERT-FR and others give, is to take the controllers off the open internet, use a secure gateway or VPN for remote work, change passwords and replace devices that can't be patched. All true. But the people running the system have real reasons for doing things the way they do.

**Remote access saves money and food.** Danfoss [reportedly claims](https://www.danfoss.com/en/service-and-support/articles/dcs/5-ways-connected-monitoring-and-management-systems-can-save-food-retailers-money-right-now/) that connected monitoring can cut food waste by up to 30% and refrigeration energy by up to 15%. These are unconfirmed: they are a vendor's own figures, I could not open the page to check them, and I found no independent study. The logic is sound, though: a contractor who can see a failing compressor at 3am saves a lot of stock. Pulling every controller offline would bring back the waste the connection was meant to stop.

**Responsibility is split.** The contractor manages the controller, the shop owns the hardware, and someone else runs the network. Forescout notes that unless roles are written down, nobody sees the whole path.

**Replacement costs money, and the law had an odd side effect.** In 2025 Danfoss announced a "hard End of Service" for legacy products, [citing new European cybersecurity laws](https://therecord.media/cyberattack-grocery-freezers-europe): keeping old products supported would have placed it under legal duties to keep shipping security updates. A law meant to make products safer pushed a manufacturer to stop supporting the older ones. From a firm's point of view this is rational; from a corner shop's, it means a working controller suddenly needs replacing.

**The rules arrive late and cover little.** The EU's [Cyber Resilience Act](https://digital-strategy.ec.europa.eu/en/policies/cyber-resilience-act) has required manufacturers since 11 September 2026 to [report actively exploited vulnerabilities](https://digital-strategy.ec.europa.eu/en/policies/cra-reporting) within 24 hours. Its main duties, including a support period matching a product's expected lifetime, only apply from December 2027, and mostly to new products. The other big EU law, NIS2, covers food wholesale and industrial processing but [not retail shops](https://www.ruokavirasto.fi/en/foodstuffs/food-sector/setting-up-a-food-business/kyberturvallisuusdirektiivi-nis2-elintarviketoimialalla/). So the supermarket itself, where the freezers are, falls between the two.

## Why it matters beyond Europe

The same controllers sit in shops, warehouses and, Forescout warns, hospital and farm cold stores across 99 countries. The Guardian reports that the Pentagon is investigating suspected hacking after fridge failures at commissaries on at least six US military bases in August. Retailers in places with fewer IT staff and older equipment are likely to be more exposed, not less, though I found no data measuring that.

So far the damage has been money and wasted food, not shortages. The quieter risk is safety: an Estonian contractor [warned](https://news.err.ee/1610183296/hackers-raised-freezer-temperature-at-estonian-supermarket-chain-to-50-c) that tampering with these systems can directly affect food safety, for example if a warm-up goes unnoticed. The bigger lesson is about trust. A fridge that a technician can reach from anywhere can be reached by anyone who finds the door. Until shops know who holds the keys, and manufacturers stop leaving old doors unlocked, the cheapest attack on a food system may be a change of a few degrees in the middle of the night.
