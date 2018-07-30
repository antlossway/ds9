# ds9
a modern SMPP gateway in go, support SMPPv3.4

# our mission
an ultimate easy-to-use SMPP gateway, which has great scalability and availibility, can run on all unix/linux operating system and windows system.
It includes back office to make configuration, pricing/routing managegment, numbering plan management, monitoring, and billing.

# naming convention
mixedCaps

# preconfigured (upon launch, user can already send SMS, send only)
gateway
- default supplier
- default buying price
- default selling price
- bonus: numbering plan, country, operator

smpp server parameter
- port: tcp 10000
- protocolTimeout=30
- reconnectDelay=5
- addrTon=1
- addrNpi=1
- protocol=SMPP
- notificationType=5
- windowSize=10
- maxThroughput=100


# redis data structure
## incoming (client connect to us)
[customerProfileName] 
 - systemId
 - password
 - systemType
 - protocolTimeout
 - reconnectDelay
 - addrTon
 - addrNpi
 - protocol:  SMPP, HTTP(in future)
 - keepAlive
 - adcOutFilter
 - adcInFilter
 - oadcInFilter
 - oadcOutFilter
 - windowSize
 - maxThroughput
 - maxBinds: how mnay binds can allowed from client
 - clientIps: what IP should be whitelisted
 - customerName: may have multiple profiles for same customer (wholesale, direct, premium ...etc), which can be configured with different routes and selling price, report will provide sum and breakdown statistics for each profile


## outgoing (we connect to supplier)
[supplierProfileName]
- supplierProfileId
- systemId
- systemType
- password
- protocolTimeout
- reconnectDelay
- addrTon
- addrNpi
- notificationType
- keepAlive
- windowSize
- adcOutFilter
- adcInFilter
- oadcInFilter
- oadcOutFilter
- supplierName: may have multiple profiles with same supplier (wholesale,direct,premium,...etc), which will have separate buying price, report will provide sum and breakdown statistics for each profile
- NumOfBinds: create how many binds to this supplier profile

## cdr
[identifier]
- msgId
- tpoa
- msisdn
- dcs
- msg
- pid
- status
- validityPeriod
- receiveTime
- submitTime
- dlrTime


# problems to solve

how to search a message by bnumber/tpoa/msgid?
how to monitor performance?
how to associate price with cdr to make billing?

