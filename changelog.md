0.7.1
* Various documentation updates.
* Add stepping combinator for manual retries.
* Add applyPolicy and applyAndDelay
* Add Read instance for RetryStatus
* Fix logic bug in rsPreviousDelay in first retry

0.7.0.1
* Officially drop support for GHC < 7.6 due to usage of Generics.

0.7
* RetryPolicy has become RetryPolicyM, allowing for policy logic to
  consult the monad context.
* RetryPolicyM now takes a RetryStatus value. Use the function
  rsIterNum to preserve existing behavior of RetryPolicy only
  receiving the number.
* The monadic action now gets the RetryStatus on each try. Use const
  if you don't need it.
* recoverAll explicitly does not handle the standard async
  exceptions. Users are encouraged to do the same when using
  recovering, as catching async exceptions can be hazardous.
* We no longer re-export (<>) from Monoid.
* Utility functions simulatePolicy and simulatePolicyPP have been
  added which help predict how a policy will behave on each iteration.

0.6

* Actions are now retried in the original masking state, while
  handlers continue to run in `MaskedInterruptible` (@maoe)
* Added several tests confirming exception hierarchy semantics under
  `recovering` (@ozataman)

0.5

* Mitsutoshi's backoff work inspired a complete redo of the
  RetryPolicy interface, replacing it with a monoidal RetryPolicy. The
  result is a much thinner API that actually provides much more power
  to the end user.
* Now using microseconds in all premade policies. PLEASE TAKE CARE
  WHEN UPGRADING. It was a bad idea to use miliseconds and deviate
  from norms in the first place.

0.4

* Transitioned to using Edward Kmett's exceptions package instead of
  monad-control. Use 0.3 series if you still need monad-control
  support.

0.3

Thanks to John Wiegley and Michael Snoyman for their contributions:

* Now using monad-control instead of MonadCatchIO, which is widely
  agreed to be broken.
* Now using transformers instead of mtl, which was a broader than
  needed dependency.