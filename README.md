mmmf, multi-master mysql failover
====

Explained in details
====
You can watch me explaining the thing here: http://www.youtube.com/watch?v=Qzht1B7p0yQ

Overview
====
mmmf is an algorithm and a tool which turns a simple and popular mysql installation
with master and several slaves replicating from it into a powerful mysql cluster
with some properties of complex multi-master solutions:
  * ability to lose the current master and continue right away
  * choose any of the slaves as a new master
  * no data loss (with semi-synchronous replication)

The important difference with the real multi-master solutions is that the time needed to recove
from master failure is not zero, though it is sane for the majority of the projects (see speed section below).

Limitations
====
Currently the tool has the following limitations:
  * nothing should modify slaves except the replication
  * all the slaves should replicate directly from master
  * statement-based replication
  * log-slave-updates turned on on all of the slaves
 
Algorithm
====
Algorithm consists of two phases: finding the Best Slave and Equalization phase.

Speed
====
Algorithm speed depends on the number of slaves and the difference between
Best Slave and other slaves. With the use of parallel synchronization
the time to execute the algorithm is approximated by the time needed
to synchronize the Best slave with the "worst" slave which in turn
can be approximated by an average lag of all of your slaves
during production work.

petya@kohts.ru, 2011
