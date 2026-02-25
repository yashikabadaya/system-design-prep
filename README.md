# system-design-prep


STEPS TO TAKE IN DESIGNING SYSTEM:

1) FEATURE EXPECTATIONS [5 min]

        (1) Use cases -- In terms of what will the user do, what will service do in return, Think about what your users need as features
        (2) Scenarios that will not be covered -- what service should not do 
        (3) Who will use
        (4) How many will use
        (5) Usage patterns -- What facts are applicable? 
        (6) Assumptions - What assumptions would you make for user and the service?
   

Clarify with your interviewer if you should do back-of-the-envelope calculations 

(2) ESTIMATIONS [5 min]

        (1) Throughput (QPS for read and write queries) -- How many requests would we handle per sec? 
        (2) Latency expected from the system (for read and write queries)
        (3) Read/Write ratio
        (4) Traffic estimates
                - Write (QPS, Volume of data)
                - Read  (QPS, Volume of data)
        (5) Storage estimates
        (6) Memory estimates
                - If we are using a cache, what is the kind of data we want to store in cache
                - How much RAM and how many machines do we need for us to achieve this ?
                - Amount of data you want to store in disk/ssd
                
eg. 

    If we 1M reqs/day -> 12 req/s
    
    1B reqs/day ->12k req/s; If each machine can handle 1k req/s then we would need 12 load balancers or web servers. 
    
    15s video -> 10Mb size ; so 1M videos would take 1M * 10Mb -> 1Tb size
    
     5yrs -> 2000 days


(3) DESIGN GOALS OR NON-FUNCTIONAL REQUIREMENTS OR SLA OR SYSTEM GUARANTEES [5 min]

        (1) Latency and Throughput requirements
        
        (2) Consistency vs Availability  [Weak/strong/eventual => consistency | Failover/replication => availability]



(4) HIGH LEVEL DESIGN [5-10 min]

        (1) APIs for Read/Write scenarios for crucial components -- An outline of all the high level components in a flow. Break down the entire system into individual main/key components,  Think about how the services can be broken down as decided in feature expectations
        (2) Database schema
        (3) Basic algorithm
        (4) High level design for Read/Write scenario
 
After SLA, talk about 
1. High level design - high level diagram connecting all components
2. low level design - table schema
3. API design - uploadVideo(userid, filepath, description), REST or gRPC etc
4. how to handle failures -


Design core components
(5) DEEP DIVE [15-20 min]
        (1) Scaling the algorithm
        (2) Scaling individual components: 
                -> Availability, Consistency and Scale story for each component
                -> Consistency and availability patterns
        (3) Think about the following components, how they would fit in and how it would help
                a) DNS
                b) CDN [Push vs Pull]
                c) Load Balancers [Active-Passive, Active-Active, Layer 4, Layer 7]
                d) Reverse Proxy
                e) Application layer scaling [Microservices, Service Discovery]
                f) DB [RDBMS, NoSQL]
                        > RDBMS 
                            >> Master-slave, Master-master, Federation, Sharding, Denormalization, SQL Tuning
                        > NoSQL
                            >> Key-Value, Wide-Column, Graph, Document
                                Fast-lookups:
                                -------------
                                    >>> RAM  [Bounded size] => Redis, Memcached
                                    >>> AP [Unbounded size] => Cassandra, RIAK, Voldemort
                                    >>> CP [Unbounded size] => HBase, MongoDB, Couchbase, DynamoDB
                g) Caches
                        > Client caching, CDN caching, Webserver caching, Database caching, Application caching, Cache @Query level, Cache @Object level
                        > Eviction policies:
                                >> Cache aside
                                >> Write through
                                >> Write behind
                                >> Refresh ahead
                h) Asynchronism
                        > Message queues
                        > Task queues
                        > Back pressure
                i) Communication
                        > TCP
                        > UDP
                        > REST
                        > RPC


(6) JUSTIFY [5 min]
        (1) Throughput of each layer
        (2) Latency caused between each layer
        (3) Overall latency justification

Talk proactively for each design choice - what if it fails, then what to do  etc. Think about error handling throughout
