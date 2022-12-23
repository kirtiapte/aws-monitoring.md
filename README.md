# aws-monitoring.md
## Cloud Trail
- track events, api calls, changes made to resources
- multiregion trail, single region trail
- log files - automatically encrypted, amazon s3 SSE
- you can configure s3 lifecycle rules to delete or archiecve log f
iles
- who made calls?

## AWS Config
- auditing- inventory of aws resources, resources history and change tracking, config reules for governance,
sns notifications
- group config packs and remediation
- example - 80 + rules present.  alb-http-to-https-redirection-check, ec2-instance-no-public-ip
- resource timeline, non compliant reports
- what does my resource look like?

## Cloud Watch
- monitoring and observability
logs, metrics, events, alarms, visualization, automated actions
- integrate with 70+ services
- cloudwatch events - resources
- Servicelens - unified access to monitor, logs, trail
- container insights- observe metrics for containers, servicemesh
- logs - 
- memoru utilization metric not tracked by default, by default does not track
operation system metrics - like memory consuption

## Async models
- Pull model - producers -> queue -> consumers.  only one cumer pulls and process the message
  - decoupling, scalability, availability, reliability
- push model - subscriber subscripes to a topic, producer send notication to the topic

## SQS 
- simple queing service 
- low cost - pay per use
- standard - unlimited throughput, choose standard if throughput is important
best-effort ordering, at-least once deliver, some messages may be processed twice
- FIFO - first in first out, exactly once processing, choose when order is important,
low throughput, 300 messages
- processing - 1. producer puts message on the queue (get message id back) 
2. consumer polls for the message - gets message + receipt handle
3. message remains on the queue until consumer processes it
4. consumer responsibility to delete the message with receiot handle
- delay queue, visibility timeout, max number  , message retention period, dead queue
- SQS autoscaling - sqs ->cloudwatch alarm ->autoscaling -> ec2 instances
   - use target tracking scaling policy
   - ApproximateNumberof Messages sqs metrics to trigger alarm
- configurations -
  1. visibility timeout - default
  2. delaysecond
  3. message retention period - default 4 days
  4. maxreceivecount 
- security - iamroles to give access to SQS for other AWS resources
           - other AWS accounts for access to SQS , SQS Queue Access Policy
 - Review 301 - scenarios, reduce api calls - long polling
 
 ## SNS
 - simple notification service
 - publish subscribe , create topic, one topic mumtiple subscribers
 - monitoring apps, workflow, mobile apps
 - SNS does not need SQS or a queue, queue can be one of the subscribers
 - bulk emails -use SES , for notification email use SNS
 
 ## Amazon MQ
 - Active MQ - combination sqs + SNS
 - scale is not good
 - JMS, AMQP, MQTT, Openwire, STOMP
 - start with it and migrate to SQS, SNS
 
 # Routing and Content Deliver
 - CDN - distribute content globally publish the content to edge locations
 - improve availability and scalability
 - configure time to live
 
 ## Cloudfront
 - serves users from nearest edge location
 - sources - s3, ec2, elb, external websites
 - if content is not available at the edge location go to origin and then cache
 - static webapps, audio/video software downloads, dynamic webapps
 - integrates with Amazon shield - prevents DDos attacks, Amazon WAF- sql injection and cross site scripting
 - zero caost s3 to cloudfront data transfer
 - reduce compute workload
 - Process - create cloudfront distribution, need domain name, source, cache-control
 - cache-control default is 24 hours but configurable, ttl, min, max
 - path patterns - configure different values 
 - Private content - signed url (access id, , signed cookies, 
 OAI origin Access identities- create OAI user 
 - signed urls - distribution with stream contents, individal file download,
 single object, cookies are not supported
 - signed cookies - multiple urls, subscriber urls, app urls don't need to be changed
 - OAI - only cloudfront can access s3 - create special OAI user
       - associate oai with cloudfront, create s3 bucket policy allowing access to OAI
- default root object configuration - to make it index.html as first page
- TTL - content expires from the edge locations
- invalidation api - remove from caches
- versions - larger expiration
- don't use - all requests origins from single location, single vpn corporate 
- retrict users from specific countries - geo restrction - whitelist and black list

# Route 53
- byuing domain name - domain registar
- set up website content - ec2 server, website hosting
- route requests to website - DNS 
- route 53 - domain registration and DNS
## DNS
- configure records - different ruting , ttl time to live - caching at the router and hosts
- hosted zone - private or public
- Arecord - name to ipv4
- AAAA - name to ipv6
- NS - name server containing DNS records - go dady to route 53 domain
- MX - mail exchange
- CNAME - name1 to name2
- Alias - route selected AWS resources, root route, or nonroot domains
- cname - <b>only for nonroot records</b>

## Routing
- route diff regions, routing policies
- simple - map domain to ip addresses - round robin
- weighted - canary deployment 
- latency based - provide min latency
- failover - active-passive failover
- geoproximity - nearest physical distance
- multivalue answer - healthcheck multiple healthj records
- geolocation - choose based on location of the user, recordset for smallest geographical region wins
       - configure default policy



 

