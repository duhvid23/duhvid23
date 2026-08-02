# David

I am building one thing. Everything public here fell out of building it.

## Escrova

**Buy anything, anywhere, with crypto. Non custodial.**

You search Amazon, eBay and Walmart in one place, or buy from another person.
You pay in crypto. The money sits in escrow on Solana until your order arrives,
and Escrova cannot spend it while it waits.

Live at **[escrova.io](https://escrova.io)**.

Honest state: it runs on Solana devnet today and mainnet is next. The escrow
program, the retail buying, the disputes and the refunds all work end to end.
The chain it runs on is the part that has not moved yet.

## What came out of it

Both of these were written for Escrova, then pulled out and cut loose from it.
Zero dependencies each, because a security tool with a package tree is a set of
keys other people hold.

**[solana-agent-402](https://github.com/duhvid23/solana-agent-402)**
An AI agent with a wallet has no session. You cannot give it a cookie and there
is nobody to click Approve, so it signs something instead, and a signature over
a static string is a bearer token that never expires. This binds the signature
to the actual request, adds an HTTP 402 challenge for paying in USDC, and makes
sure one payment can only ever buy one thing.
142 tests: replay, expiry, tampered body, forged signature, two agents
presenting the same proof at the same moment.

**[prisma-deploy-guard](https://github.com/duhvid23/prisma-deploy-guard)**
Plenty of projects deploy with `prisma db push --accept-data-loss`. That flag
says: if the schema does not match, drop whatever is in the way. Every deploy.
Nobody watching. Mine said it too. This reads the plan first, refuses anything
that can delete, and only approves one specific change at a time so an old
approval cannot wave through a new one.
86 tests over real Prisma output. Writing them found a bug in my own version:
it would have blocked the first deploy after a database restore, which is
exactly when you need it least.

**[legal-version-guard](https://github.com/duhvid23/legal-version-guard)**
Your terms of service say a customer has 14 days to cancel. A constant in your
code says 21. Both were right the day they were written, and now the contract is
wrong and nobody will notice until a customer quotes it back. This fails the
build instead. It also refuses to let you edit a document somebody already
accepted, because they agreed to specific bytes and editing those destroys the
record of what was agreed.
147 tests. Two of them are the real times it caught me: once when I moved a
number and left the contract behind, and once when I fixed that document and a
second one still said the old number.

## How I work

Every fix here says what broke and what it cost, not what the code does. If I
cannot explain the failure, I do not understand the fix yet.

Anything I have not proven, I say so. Both READMEs above have a section for it.

## Stack

Solana, Anchor, Rust. Node, React, Postgres, Prisma. Vercel.

Reach me at **david.guedesact@gmail.com**.
