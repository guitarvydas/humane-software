This is a _very_ simple example of a hierarchical state-machine and actor system.

All consideration of critical regions has been removed - for clarity.  I assume that once the principle(s) is understood, the code for critical regions will become "obvious" (queue access and busy-bit access).

To facilitate clarity, the scheduler (dispatcher) is not correct (SEND should cause dispatching).

This simple example demonstrates:

1. How simple actors can be (I claim that any programming problem can be solved this way, when the dispatcher is correct).

2. Hierarchical state machines - the Intensity mode of the example is actually a state machine on its own (with state variable "intensity").

3. Parent machine vs. child submachine event anti-inheritance (the parent ALWAYS sees and (and gets to react to) the :power event before the child does (this characteristic is no specified by Harel State Machines ; this characteristic makes all diagrams of states "meaningful" - nothing can be hidden).

4. In FBP-like terms - the lamp is a Component and the inner state machine (intensity) is another Component.

5. The Concurrent Design Paradigm (see Rob Pike's talk "Concurrency is not Parallelism")

This example _does not_ demonstrate:

1. The semantic property that children of the same parent cannot talk to one another directly.

2. Deferred SENDs.  When a machine SENDs an event, the event is acutally queued on the output-queue of the machine, to be released only when the machine as finished processing a single event to completion (this property allows one to calculate the through-time for a Component and prevents priority-inversion-like behaviour in certain circumstances).

3. Outputs to multiple Components from a single output pin.

4. Input and Output API's

5. Input and Output pins (:power and :intensity should be "pins" attached to their respective Components ; a full-blown event is a tuple {self, pin, event-data-on-specifed-pin}).

6. How to convert the digram 

