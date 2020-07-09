---
layout: post
title: Deterministic Contract Verification
date: '2018-06-16 08:00:00'
tags:
- djvm
---

<figure class="kg-card kg-embed-card kg-card-hascaption"><iframe src="https://player.vimeo.com/video/275577309?app_id=122963" width="740" height="376" frameborder="0" allow="autoplay; fullscreen" allowfullscreen title="Deterministic JVM"></iframe><figcaption>This video demonstrates the <strong>djvm</strong> command line tool that comes with DJVM. The tool can be used to check validation steps and explore transformations made by the deterministic sandbox. It enables the user to quickly build new runnable classes to see whether they pass static analysis and also the dynamic costing constraints imposed on the runtime environment.</figcaption></figure>
#### Why do we need a deterministic sandbox?

It is important that all nodes that process a transaction always agree on whether it is valid or not. Because transaction types in Corda are defined using JVM byte code, this means that the execution of that byte code must be fully deterministic. Out of the box, a standard JVM is not fully deterministic, thus we must make some modifications in order to satisfy our requirements.

So, what does it mean for a piece of code to be fully deterministic? Ultimately, it means that the code, when viewed as a function, is pure. In other words, given the same set of inputs, it will always produce the same set of outputs without inflicting any side-effects that might later affect the computation.

#### What’s the current state of affairs?

In our pursuit of enabling deterministic contract verification in Corda, we have worked on a deterministic sandbox (DJVM) which will provide a safe environment for such verification methods to run in. As part of that work, I have just pushed a pull request for the first iteration of our DJVM work to our Corda repository; see [**corda/corda#3386**](https://github.com/corda/corda/pull/3386). This will form the foundation for the future deterministic sandbox used in Corda. Before we get there though, the code needs thorough review, some further improvements and modifications, etc.

<figure class="kg-card kg-image-card kg-card-hascaption"><img src="https://cdn-images-1.medium.com/max/1600/1*VbYw-mrrVrrZSnqlt9ooNg.png" class="kg-image" alt><figcaption>A high-level view of the design of the deterministic sandbox environment, where a set of rules, definition providers and emitters control the validation, instrumentation and rewriting of loaded byte code.</figcaption></figure>

As you will see from the PR, the code in the top-level DJVM module has not yet been integrated with the rest of the platform. It will eventually become a part of the node and enforce deterministic and secure execution of smart contract code, which is mobile and may propagate around the network without human intervention. However, for now it stands alone as an evaluation version.

#### Preview and request for comments

We want to give developers the ability to start trying it out and get used to developing deterministic code under the set of constraints that we envision will be placed on contract code in the future. For details around the concept, implementation, constraints, scope, etc., please refer to the documentation site. A snapshot of the added documentation can be found on the PR: [docs/source/key-concepts-djvm.rst](https://github.com/corda/corda/blob/9228b5e093f95155d4c3bafa53f96bae8007b446/docs/source/key-concepts-djvm.rst).

**NOTE:** This is quite a meaty piece of work, and the PR is indeed quite large. I expect there to be quite a few comments and rounds of feedback, and for the PR to be up for a while before merging… and this is indeed the reason for my email — it would be great to get this in front of as many of our users as possible (i.e., _you!_), for us to perform a thorough review of the work covered by this PR, but also to start thinking about the follow-up work beyond this initial version of the sandbox. **_This is why I’m calling on anyone interested to take a look and provide feedback._**

#### Related work

It should be mentioned that this work ties in closely with our development efforts on the SGX team, working towards a deterministic sandbox for running contract verification inside an SGX enclave. If you’re curious to learn more about that work, have a look at the following material:

- Mike Hearn’s presentation about SGX and Corda ([**video**](https://vimeo.com/226936471), [blog post](https://www.corda.net/2017/06/corda-sgx-privacy-update/))
- Andras Slemmer’s post on our SGX infrastructure design ([**post**](https://groups.io/g/corda-dev/topic/sgx_design/19247114?p=,,,20,0,0,0::recentpostdate%2Fsticky,,,20,2,0,19247114))
- Chris Rankin’s work on making a deterministic version of our Core module ([pull request](https://github.com/corda/corda/pull/3262)) and [**related documentation**](https://docs.corda.net/head/deterministic-modules.html)
- Note also that there will be **another SGX blog post coming soon** (so stay tuned)!

Have a great weekend! Look forward to hearing your feedback on this.

