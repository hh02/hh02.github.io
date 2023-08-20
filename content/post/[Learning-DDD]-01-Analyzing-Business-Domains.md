---
title: "[Learning DDD] 01 Analyzing Business Domains"
date: 2023-08-20T17:22:21+08:00
draft: false
---

# What Is a Business Domain?

A business domain defines a company's main area of activity. Generally speaking, it's the service the company provides to its clients.

For example:

- FedEx provides courier delivery.
- Starbucks is best known for its coffee.
- Walmart is one of the most widely recognized retail establishments.

# What is a Subdomain?

To achieve its business domain's goals and targets, a company has to operate in multiple *subdomains*. 

A subdomain is a fine-grained area of business activity. All of a company's subdomains form its business domain: the service it provides to its customers.

For example, Starbucks may be most recoginized for its coffee, but building a successful coffeehouse chain requires more than just knowing how to make great coffee. You also have to buy or rent real estate at effective locations, hire personnel, and manage finances, among other activities. 

## Types of Subdomains

### Core subdomains

A *core subdomain* is what a company does differently from its competitors.

A core subdomain that is simple to implement can only provide a short-lived competitive advantage. Therefore, core subdomains are naturally complex.

### Generic subdomains

*Generic subdomains* are business activities that all companies are performing in the same way. 

### Supporting subdomains

*Supporting subdomains* support the company's business.

## Comparing Subdomains

| Subdomain type | Competitive Advantage | Complexity | Volatility | Implementation     | Problem     |
| -------------- | --------------------- | ---------- | ---------- | ------------------ | ----------- |
| Core           | Yes                   | High       | High       | In-house           | Interesting |
| Generic        | No                    | High       | Low        | Buy/adopt          | Solved      |
| Supporting     | No                    | Low        | Low        | In-house/outsource | Obvious     |

## Identifying Subdomain Boundaries

**Coarse-grained subdomains:** A good starting point is the company's departments and other organizational units. 

### Distilling subdomains

Analyzing the inner workings of a suspectedly generic subdomain to find the finer-grained subdomains.

On the other hand, we cannot drill down indefinitely, looking for insights at lower and lower levels of granularity. When should you stop?

### Subdomains as coherent use cases

From a technical perspective, subdomains resemble sets of interrelated, coherent use cases. Such sets of use cases usually involve the same actor, the business entities, and they all manipulate a closely related set of data.

We can use the definition of "subdomains as a set of coherent use cases" as a guiding principle for when to stop looking for finer-grained subdomains. These are the most precise boundaries of the subdomains.

### Focus on the essentials

When looking for subdomains, it's important to identify business functions that are not related to software, acknowledge them as such, and focus on aspects of the business that are relevant to the software system you are working on.

# Who Are the Domain Experts?

Domain experts are subject matter experts who know all the intricacies of the business that we are going to model and implement in code. In other words, domain experts are knowledge authorities in the software's business domain.
