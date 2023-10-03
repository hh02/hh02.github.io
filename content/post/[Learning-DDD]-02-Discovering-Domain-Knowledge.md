---
title: "[Learning DDD] 02 Discovering Domain Knowledge"
date: 2023-08-20T22:17:15+08:00
draft: false
---

Chapter 01: business subdomains' boundaries and types.

This chapter continues the topic of business domain analysis but in a different dimension: depth. It focuses on what happens inside a subdomain: its business function and logic.

# Business Problems

Business problems appear both at the business domain and subdomain levels. 

# Knowledge Discovery

To be effective, the software has to mimic the domain experts' way of thinking about the problem—their mental models.

# Communication

During the traditional software development lifecycle, the domain knowledge is "translated" into an engineer-friendly form known as an *analysis model*, which is a description of the system's requirements rather than an understanding of the business domain behind it. While the intentions may be good, such mediation is hazardous to knowledge sharing. In any translation, information is lost;

信息随着传递环节的增多，会变得不可信。

减少信息的翻译，让 PM, RD 等所有参与者使用同一套语言。

# What Is a Ubiquitous Language

Using a ubiquitous language is the cornerstone practice of domain-driven design. The idea is simple and straightforward: if parties need to communicate efficiently, instead of relying on translations, they have to speak the same language. （书同文）

The traditional software development lifecycle implies the following translations:

- Domain knowledge into an analysis model
- Analysis model into requirements
- Requirements into system design
- System design into source code

Instead of continuously translating domain knowledge, domain-driven design calls for cultivating a single language for describe the business domain: the ubiquitous language.

All project-related stakeholders—software engineers, product owners, domain experts, UI/UX designers—should use the ubiquitous language when describing the business domain.

# Language of the Business

The ubiquitous language is the language of the business. As such, it should consist of business domain—related terms only. No technical jargon!

## Consistency

The ubiquitous language must be precise and consistent. It should eliminate the need for assumptions and should make the business domain's logic explicit.

### Ambiguous terms

The term *policy* has multiple meanings: it can mean a regulatory rule or an insurance contract. The exact meaning can be worked out in human-to-human interaction, depending on the context. Software, however doesn't cope well with ambiguity, and it can be cumbersome and challenging to model the "policy" entity in code.

Ubiquitous language demands a single meaning for each term, so "policy" should be modeled explicitly using the two terms *regulatory rule* and *insurance contract*.

### Synonymous terms

It is preferable to use each term explicitly in its specific context. Understanding the differences between the terms in use allows for building simpler and clearer models and implementations of the business domain's entities.

# Model of the business Domain

## What Is a Model?

> A model is a simplified representation of a thing or phenomenon that intentionally emphasizes certain aspects while ignoring others. Abstraction with a specific use in mind. —Rebecca Wirfs-Brock

## Effective Modeling

A useful is not a copy of the real world, instead a model is intended to solve a problem, and it should provide just enough information for that purpose.

> All models are wrong, but some are useful.

## Continuous Effort

Cultivation of a ubiquitous language is an ongoing process. It should be constantly validated and evolved.

## Tools

A wiki can be used as a *glossary* to capture and document the ubiquitous language. It's important to make glossary maintenance a shared effort (not centralized).

Glossaries work best for "nouns": names of entities, processes, roles, and so on. Behavior is also important. The behavior is not a mere list of verbs associated with nouns, but the actual business logic, with its rules, assumptions, and invariants. Such concepts are much harder to document in a glossary. 

Hence, glossaries are best used in tandem with other tools that are better suited to capture the behavior; for example, use cases or Gherkin tests.

Automated tests written in the Gherkin language are not only great tools for capturing the ubiquitous language but also act as an additional tool for bridging the gap between domain experts and software engineers.

Finally, there are even static code analysis tools that can verify the usage of a ubiquitous language's terms. A notable example for such a tool is NDepend.

## Challenges

Finally, the question about the ubiquitous language that I an asked often at conferences is what language should we use if the company is not an English-speaking country. My advice is to at least use English nouns for naming the business domain's entities. This will alleviate using the same terminology in code.





 

