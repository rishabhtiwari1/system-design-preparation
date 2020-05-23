# System Design Interview Preparation
Prep for the system design interview. Includes system design concepts and FAQ's on System Design

> I originally started with learning ad-hoc concepts related to system design. But soon came to understand this will not work > for a long term. So i am creating this to start as a to-do list for system design interview preparation.
>
> The items listed here will prepare you well for in an interview at just about any software company,
> including the giants: Amazon, Facebook, Google or Microsoft.

This is meant for **new software engineers** who have 3+ years of experience. If you have
many years of experience and are claiming many years of software engineering experience, expect a harder interview.

## Table of Contents

- [System Design Concepts](#system-design-concepts)
    - [Caching](#caching)
    
    
    
    
    
## System Design Concepts

- ### Caching

      > In computing, a cache is a hardware or software component that stores data so that future requests for that data can         > be served faster; the data stored in a cache might be the result of an earlier computation or a copy of data stored         > elsewhere.
      
      > Caching consists of: precalculating results (e.g. the number of visits from each referring domain for the previous 
      > day), pre-generating expensive indexes (e.g. suggested stories based on a user's click history), and storing copies 
      > of frequently accessed data in a faster backend (e.g. Memcache instead of PostgreSQL).
      
     # Application vs. database caching

      > There are two primary approaches to caching: application caching and database caching (most systems rely heavily on         > both).
      > Application caching requires explicit integration in the application code itself. Usually it will check if a value is       > in the cache; if not, retrieve the value from the database; then write that value into the cache (this value is             > especially common if you are using a cache which observes the least recently used caching algorithm). The code               > typically looks like (specifically this is a read-through cache, as it reads the value from the database into the           > cache if it is missing from the cache)
        
      > The other side of the coin is database caching.
      > When you flip your database on, you're going to get some level of default configuration which will provide some degree       > of caching and performance. Those initial settings will be optimized for a generic usecase, and by tweaking them to         > your system's access patterns you can generally squeeze a great deal of performance improvement.
      > The beauty of database caching is that your application code gets faster "for free", and a talented DBA or operational       > engineer can uncover quite a bit of performance without your code changing a whit (my colleague Rob Coli spent some         > time recently optimizing our configuration for Cassandra row caches, and was succcessful to the extent that he spent a       > week harassing us with graphs showing the I/O load dropping dramatically and request latencies improving substantially       > as well).

     # In-memory caches
      
      > The most potent–in terms of raw performance–caches you'll encounter are those which store their entire set of data in       > memory. Memcached and Redis are both examples of in-memory caches (caveat: Redis can be configured to store some data       > to disk). This is because accesses to RAM are orders of magnitude faster than those to disk.
        
      > On the other hand, you'll generally have far less RAM available than disk space, so you'll need a strategy for only         > keeping the hot subset of your data in your memory cache. The most straightforward strategy is least recently used,         > and is employed by Memcache (and Redis as of 2.2 can be configured to employ it as well). LRU works by evicting less         > commonly used data in preference of more frequently used data, and is almost always an appropriate caching strategy.

      
      Some Important links related to caching
      - [ ] [Caching Basics](https://en.wikipedia.org/wiki/Cache_(computing))
      - [ ] [Locality of reference](https://en.wikipedia.org/wiki/Locality_of_reference)
      - [ ] [Cache Basics (video)](https://www.youtube.com/watch?v=chnhnxWIjgw&list=PLbtzT1TYeoMgJ4NcWFuXpnF24fsiaOdGq)
