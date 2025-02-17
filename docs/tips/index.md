---
hide:
  - navigation
icon: material/lightbulb
title: Tips
---

#:material-lightbulb: Tips

This section lists various tips for beginning pivoters. If you'd like to learn more about pivoting in particular and threat intel research in general, be sure to check out the references mentioned in the [FAQ](/#where-can-i-learn-more-about-pivoting).

## Focus on rarity

As a rule, queries that return more results are less helpful than those that return less results, since the former requires a lot of manual sifting. To be more specific, we should strive to run queries that return a set of results in which many are relevant to our investigation. The technical term for this quality of results is called [**precision**](https://en.wikipedia.org/wiki/Precision_and_recall).

For this reason, it makes sense to pivot on **rare** (low-prevalence) properties of artifacts, since these are most likely to return precise results, and thereby more easily surface new information.

For example, if a suspicious server has many properties which are shared by thousands of other servers (such as listening on port 80), but its IP address is located in a small ASN with only a few dozen other addresses, then you should probably prioritize the ASN for further investigation before pursuing other avenues of exploration.

One way of identifying rare properties is [frequency analysis](https://en.wikipedia.org/wiki/Frequency_analysis), which involves calculating the prevalence of every property of a given artifact in order to identify outliers of interest. Some platforms perform these calculations for you, such as the "Guided Pivots" feature of [DomainTools](https://domaintools.com/). This process can be especially helpful if an investigation has so far only surfaced a small number of artifacts, by highlighting which aspects of those artifacts are the most pivotable. However, frequency analysis can also be useful when a pivot surfaces too many artifacts, as it can be used to prioritize artifacts with the rarest properties, which are usually most likely to be interesting and therefore worth pursuing further.

## Use both inclusion and exclusion

In order to build high-precision queries, it can often be helpful to use a mix of inclusions (`X AND Y`) and exclusions (`X AND NOT Y`). Exclusions can compensate for situations where the things we're searching for have mostly non-unique features. Let's say we encounter a malicious Python script and set out looking for other similar scripts. Merely being written in Python is hardly unique, and while there are many possible inclusions we could use, such as specific lines of code which we might expect to appear in other variants, we can also consider incorporating exclusions in our query in order to further improve precision. For example, we could try ruling out the usage of certain common imports that are unlikely to be used in malware; any sort of licensing information; or comments.

To learn more about querying strategies, check out [this blogpost](https://amitaico.substack.com/p/querying-in-research).

## Combine multiple pivots

Having considered the significance of rarity, during your investigations you may yet encounter artifacts with properties that don't stand out among the rest in any significant way. However, sometimes you can identify rarity by filtering on multiple properties at once.

For instance, let's say a phishing website is hosted on a server that listens on port 80, uses a TLS certificate issued by GlobalSign, contains placeholder HTML content that can be found on thousands of other websites, and its domain was registered on May the 4th, 2024. While each of these properties in and of themselves isn't rare enough to be significant (querying for each of them separately would yield anywhere between thousands and millions of results), in combination they are probably unique enough to surface only a dozen or so other servers with the exact same combination of properties, which may all be associated with the same phishing campaign.

## Check multiple databases and tools

Pivot between different databases, and avoid fixating on a single database. Adjust your querying strategy according to the characteristics of each database.

## Cross-reference between different types of databases

If you have access to open-source, commercial and private data (generated by you or the company you work for), it's always a good idea to cross-reference between these various databases, especially between your private data and data available to others. This raises the likelihood of reaching conclusions unique to your own visibility. In other words, it allows you to reveal information that you are in a unique position to uncover, meaning that your discoveries are more likely to be novel.

## Always search for prior art

Before diving deep into an investigation, be sure to query for the artifacts and fingerprints in threat intelligence databases. Additionally, consider that others may have recorded and organized the information you seek in ways that seem counterintuitive.

## Don't be afraid of manual sifting

As a rule, quantity is more important than quality. It’s okay to compromise on low precision and sift through many results, as long as we’re quite confident in our recall (otherwise we’re at greater risk of wasting our time). While we should hope to find “holy grails” in our data (as in a single piece of information that answers our research questions), it’s more feasible to discover lots of smaller bits of information that we can piece together to reach an important conclusion - we must not let this discourage us.

## Invest in documentation

Record the information you discover while including the exact source (so you can return to reexamine it later and also use it as a reference in your research products), as well as any notes on ideas or possible connections to other pieces of information you’ve encountered so far. Additionally, you should tag the information so that you can more easily retrieve it from your corpus at a later point in time.

For this purpose, you can use dedicated threat intel platforms such as [Yeti](https://yeti-platform.io/), [Synapse](https://github.com/vertexproject/synapse), or others described in the [tools section](/tools). Alternatively, you might want to look into general knowledge management software such as [Notion](https://notion.so/) or [Obsidian](https://obsidian.md/).