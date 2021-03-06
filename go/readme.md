### blockchain based rngs

Disclaimer that this should not be used for anything other than fun and no-funds-attached experimentation!

There's a bunch of ways you can create a randomness beacon from a blockchain,
depending on what adversarial model you're willing to assume (what proportion 
of participants do you expect to behave honestly?) and what communication
overhead you're willing to accept.

#### BLS things

BLS as a randomness beacon assumes that a threshold of parties (which can 
be a tunable parameter, `t`) are willing to participate. This `t`th party will
be able to compute the outcome of the randomness beacon before he decides
whether or not to broadcast his share of the signature, and so we have to 
assume that at least one of the remaining `n - t + 1` parties (for a total
of `n` parties who can possibly participate) are willing to broadcast. 
Equivalently, you can hope that it's in at least one on these people's 
benefit for them to broadcast that final share :)

The randomness beacon can be tuned just like dfinity's (and all credit 
for the idea goes to them, not me).


BLS comes from [this](https://www.iacr.org/archive/asiacrypt2001/22480516.pdf)
2001 paper by Boneh, Lynn, and Shacham. It's been cited ~3000 times and it's
simple enough to read! I promise!

You can also make people commit to their randomness before the actual random 
shares are broadcast (for example by publishing the hash of the randomness 
(and optionally a nonce), and attach some deposit to this commitment, meaning
that parties only won't reveal if they have a huge stake in not revealing, bigger
than their deposit. However, this also might penalise honest users with bad internet 
connections.

#### 'Time lock' things

You can also assume that some computation is really hard to do and produces
a random output that is very quick to verify as honestly generated. An example
of a hard to compute but quick to verify function is repeated modulo spare-rooting.
IDK if this ratio is acceptably bad though.
