---
title:  "Exploring Data Streams"
date:   2018-04-13
categories: data streams kafka avro enterprise-architecture
comments: true
---

# Resources

Good read on why data streams should be considered first-class citizens in data infrastructure: [The Future of ETL Isn’t What It Used To Be](https://www.confluent.io/blog/the-future-of-etl-isnt-what-it-used-to-be)

Interesting video on using a streaming platform for ETL: [ETL is Dead! Long Live Streams](https://vimeo.com/220846693/305dfdb663)

# Thoughts

My curiosity was sparked by [Kafka](https://kafka.apache.org) and [Avro](https://avro.apache.org) by listening to [episode 27 of the Drill to Detail podcast](https://www.drilltodetail.com/podcast/2017/5/22/drill-to-detail-ep27-apache-kafka-streaming-data-integration-and-schema-registry-with-special-guest-gwen-shapira). It's a pretty fascinating technology. I got to hello-world with Kafka a few weeks ago but haven't explored further yet. From all I've learned I wonder if it's the technology underlying Ellucian Ethos.

Overall I visualize a bunch of databases as pools, and traditionally when we need to get water from one to another, we would connect a pipe from one to another. With streams, it's like all the pools are pumping into a central stream that can be routed to whatever other pool needs specific water. (Not an amazing analogy, but it helps to visualize a little bit.) If done right, it seems like streams can really enliven an organization.
