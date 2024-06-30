Design an Ad Click Aggregator

# Requirement
## Functional
1. Users can click on an ad and be redirected to the advertiser's website
2. Advertisers can query ad click metrics over time with a minimum granularity of 1 minute

## Scale
1. 10m active ad
2. 10k ad click per second

## Non-functional
1. Low latency analytics query, sub-second
2. Fault tolerant and accurant data collection
3. As realtime as possible. Advertisers should be able to query data as soon as possible after the click.
4. Idempotent click tracking. We should not count the same click multiple times.
5. Scalability - 10k cliks per second

# API
getAdMetrics/{adId}

# Dataflow
1. User clicks on an ad on a website.
1. The click is tracked and stored in the system.
1. The user is redirected to the advertiser's website.
1. Advertisers query the system for aggregated click metrics.

# Highlevel designs
1. Users can click on ads and be redirected to the target
Let's start with the easy part, when a user clicks on an ad in their browser, we need to make sure that they're redirected to the advertiser's website. We'll introduce a Ad Placement Service which will be responsible for placing ads on the website and associating them with the correct redirect URL.

When a user clicks on an ad which was placed by the Ad Placement Service, we will send a request to our /click endpoint, which will track the click and then redirect the user to the advertiser's website.

Use real time analytics with stream processing

## Deep dive
1. Scalability - horizontal scaling for click processer, message queue, stream event processer, OLAP db
2. Hot shard - Further partition by adding a randomId after adId
3. How to ensure we don't lose data
4. - message queue retention date of 7 days
   - checkpointing stream processor save states to permenant data store peoriodically
5.  How can we prevent abuse from users clicking on ads multiple times?  Generate a Unique impression ID
6. How can we ensure that advertisers can query metrics at low latency?

# Reference
https://www.hellointerview.com/learn/system-design/answer-keys/ad-click-aggregator
