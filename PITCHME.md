## Moving away from a Monolith

Datasets at SoundCloud

---

### Problem that we see
* Working with data and multiple teams is hard          |
* Bugs in data production go undetected for a long time |
* Changes are hard to make, coordination required       |

---

### How did we get here?

+++

#### Open access

With a monolith codebase, everything had access to the same data

* one message bus, everyone throws messages on there, reads from it
* common access to MySQL tables. Just connect, read
  * not to the extent that it was a single database for everything, but treated in a similar way

+++

#### Easy-to-use tools

With locally-useful tools, it's easy to lose global control of data flow

* Data Warehouse is great for analytics
* Devs want to explore data, and it's easy to set up regular exports of data -> Redshift
  * MySQL tables
  * Event-stream dumps
* Production schemas are coupled to analytics workloads

---

### This causes problems

* lack of visibility of data flow
* making changes can cause bugs at a distance
* making changes causes coordination between teams, slow
* duplicated work, consumer has to understand all semantics

---

### Even worse
* these costs are difficult to see
* lack of visibility in data, but also in work

---

### Why?
    * this data is available to all, but should not be consumed
    * accidental publication
    * Public vs published (Martin Fowler)

---

### How do we deal with this?
* Address the costs -- make things explicit
* Ownership needs to be in the right place
* Think about your datasets as an API
    * this requirement, approach is familiar from services
    * ad-hoc producer-consumer relationships means hidden costs

---

### Who should own a dataset?
    * Two things to think about
    * Semantics
        * Producer of a dataset should ...
    * Encapsulation
        * Don't use data stores from elsewhere

---

### What does it mean to own a dataset?
