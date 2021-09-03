---
layout: post
title:  "APIs & Abstract Entities"
categories: engineering
---

Today at work there was an interesting problem. My team owns System C, which is going to integrate with Service S, owned by another team. A colleague designed the integration but something was off. Our system has a concept of a collection of items, while Service S only deals with denormalized items, with each item containing all the information related to it. Based on that, Service S was only exposing APIs to work at the item level. There was no concept whatsoever of managing a collection of items. If you wanted to create a collection of items, you'd have to tag all items with something to indicate they belong to the same collection. The Service S team even suggested introducing a Batch API to support the collection use-case, where we could make requests to bulk edit multiple items. That didn't seem semantic, efficient nor client-friendly. So we setup a call to evaluate the trade-offs of introducing the concept of a collection in their system.

The resistance in introducing the new concept was that it would add complexity, make the system inefficient, because the system only served information at the item-level. Despite considering that this was not necessarily the obvious best implementation (for instance, the denormalization could happen in-memory instead of in the datastore where it is harder to manage large collections at the item level), the discussion became a lot more productive once we identified that there were two sides to be evaluated, and that they can be evaluated independently: what is exposed to the client (API) and what is the internal implementation.

You see, the team was thinking in terms of what made more sense for the internal implementation, and I was coming with the perspective of the client, mostly caring about the API. However, I phrased it wrongly: I mentioned I would like to evaluate the introduction of the collection concept in their system. I should have said "in the API" instead. Once this was identified, I explained how they could opt for any way of implementing things internally, regardless of the API exposing this concept. I.e., the concept of normalized collections did not necessarily have to exist internally in their service, but it was very beneficial to expose it to the clients. In fact, even for the Service S itself. If the abstract entity is not exposed with its own APIs, coupling arises with the internal implementation of the system, removing the freedom for the service to modify its internal implementation without impacting clients.

Here are the takeaways:
1. Remember that the API does not have to reflect the internal implementation. You can expose "abstract entities" that aren't modeled in the same way internally. The focus of the API is to a) serve the client; b) encapsulate the internal implementation, enabling it to evolve independently.
2. When bringing a new concept to a team's service, make sure to be clear about the above: you're bringing a new concept to the API, which doesn't dictate how things are implemented internally.

Cheers!

Igor