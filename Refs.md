## Refs

> **Refs:** Update the state of more than one identity simultaneously.

Refs are Clojure’s coordinated reference type. You can ensure that you will be able to safely update multiple identities with multiple operations. This is most likely something you have seen before with database transactions. This sort of safety guarantees several things for your multi threaded programs:

* No possibility of the involved refs ever being in an observable inconsistent state
* No possibility of race conditions among the involved refs
* No manual use of locks, monitors, or other low-level synchronization primitives
* No possibility of deadlocks

### Using a Ref

We can create a Ref called Sansa.  Sansa keeps track of all of her siblings.  So far she only has one.

~~~clojure
    (def sansa (ref {:siblings #{"Rob"}}))
~~~

We can create a transaction with `dosync` that will add more siblings to Sansa :

~~~clojure
    (dosync (alter sansa update-in [:siblings] conj "Bran" "Jon" "Rickon"))
~~~

Since Refs are known for safely updating multiple items in a single transaction, lets implement a safe way to transfer money from one account to another. Fix out program `lib/refs.clj`.

> _TIP: skip ahead to an implementation of using delays with `git checkout refs-solved`_
