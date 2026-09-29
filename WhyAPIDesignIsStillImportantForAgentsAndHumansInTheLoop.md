### Code matters more than it ever did

I keep thinking about how [complexity was causing the software crisis of the late 60s](https://en.wikipedia.org/wiki/Software_crisis). We have more tools to make more software than ever, but we are running into the same issues as always. Making code reliable, performant, extensible, testable, provable, accurate.

Complexity was the bottleneck 60 years ago, and I'm willing to bet it will be for the next 60. Back then we wrote COBOL and FORTRAN clusterfucks. Today we generate AI vibe-coded clusterfucks. If we can't wrangle the sheer scale of entropy LLMs create, how are we supposed to make better software?

A well designed API allows your agents to understand your code easier and spend less money on wasted reasoning tokens. Maybe you can bear the [cognitive load of your codebase](https://github.com/zakirullin/cognitive-load/), but there is no way to know what limits your agent has. Context windows change from model to model, and performance of these models can vary drastically between releases and the harness or tooling around it. How can you trust the code being slop-cannoned into your repo?

[CPU thrashing](https://en.wikipedia.org/wiki/Thrashing_(computer_science)), [agent thrashing](https://www.anthropic.com/research/multiagent-systems), and  [constant context-switching](https://pubmed.ncbi.nlm.nih.gov/11518143/) behave in the same way. It’s all wasted work which risk missing flaws in the software we build. Code still runs on a processor with limited registers, people have a limited mental capacity, [agents have limited context and can experience conversation drift](https://arxiv.org/abs/2604.13061).

[Hashimoto's whiteboard defense analogy](https://x.com/mitchellh/status/2100249348345057389?s=20) plays a huge role in my philosophy when designing the implementation or ergonomics of an API. If an agent wrote the code and I ship it, can I explain why the system works, what could break from a change, why this design was picked in the first place? If I can't, is there really any way for me to verify the software does what I say it does? A green checkmark on the PR doesn't mean you know why it works. LLMs will never "know" why it works either.

We all are reading a LOT more code in this new AI age. If we aren't writing code anymore, we still need to [ensure you're not building a spaghetti-tangled mess](https://www.youtube.com/watch?v=tD5NrevFtbU) so your users don't [stop using your app from how slow it is](https://www.youtube.com/watch?v=GC-0tCy4P1U). How the code actually works under the hood still matters even when you are moving abstraction layers up.

### Human-friendly architecture is Agent-friendly architecture 

An easy-to-use interface is an easy-to-infer interface. Clearer contracts and boundaries deter agents from having to guess (or hallucinate) how your system works.

```
Hard-to-use interfaces: 
- agents inspect half the repo ($ on tokens)
- agents infer conventions via reasoning ($ on tokens)
- prompts less likely have desired outcomes (SLOP)
- complexity encourages hack-y glue code (SLOP)
- create restrictive scaffolding tests that over-enforce behavior (SLOP)
```

This is an extremely frustrating situation for a human-in-the-loop. At best you're constantly handholding and correcting your agent which REDUCES productivity. The more slop code in your repo the more money you're spending on tokens. In my experience the tests AI agents, more from models like ChatGPT's Astra or Anthropic's Fable, enforce it's generating the correct code by writing test-scaffolding that feels like scaffolding a skyscraper with a house of cards.

```
Easy-to-use interfaces:
- functions are named in a way so expected behavior is obvious (inferred)
- encourage agents next token is more likely to call the obvious thing (less $$$)
- remove those scaffolding tests without breaking something (trust the code)
```

Obvious interfaces mean less guessing, fewer `/undo`s, fewer tokens, and less slop. [Locality of behavior](https://four.htmx.org/essays/locality-of-behaviour/) and [grug-brained simplicity](https://grugbrain.dev/) help you understand your system without struggling to keep all of its details and edge cases in your head. See [Carson Gross's talk on API design at BSDC 2025](https://www.youtube.com/watch?v=dTstnhS3moc).

> *"Complexity very very bad"*

Agent software factories don't solve problems. Java OOP `AbstractBuilderPatternFactoryDAO()` and C++ `.h` issues or `namespace::` insanity make problems **HARDER TO SOLVE**. You need to avoid redundant or unhelpful abstractions so your agent doesn't see a bunch of slop and want to make more slop. Why make what is already really difficult: creating reliable software, harder than it already is?

### Tools and techniques to consider

If we're never outrunning vibe-coded nonsense, why not invest in implementing scaffolding and pipelines that check the complexity, security risks, "obviousness", or "easy-to-use-ness" of whatever code developers are blindly shipping? Couldn't you just sandbox it and create exhaustive architecture tests? A more [deterministic AI tool like Jev](https://typesafe.ai/blog/introducing-system-one-models-and-jev) with or without MCPs could be the backbone of this kind of CICD pipeline. But how do you write regression tests without locking yourself into a design? A project like [SQLite benefits from its comprehensive testing coverage](https://www.youtube.com/watch?v=V_qzqY1bb7) because its behavior has been defined and shouldn't change.

> ["*A wide and flat architecture is all about planning for growth and change, and then fostering the conditions that make change easy.*" - Evan DeMond](https://www.evandemond.com/programming/wide-and-flat)

Light code duplication or using flatter and wider abstractions are less cumbersome for a developer today versus any other time in history. I want my code to have less of a burden on my cognitive load when I read the code. This way I can have an easier time trusting the code, and [grokking](https://en.wikipedia.org/wiki/Grok#Adoption_and_modern_use) the behavior of code.

I want to design my APIs in such a way that there are no hidden or unexpected behaviors when I call a function. The fewer assumptions the consumer needs to make the better. I want to mitigate being blindsided by how a library works or an agent's implementation in a diff.

An easy-to-infer interface also gives you the added benefit of quickly understanding code you wrote in the past or letting agents figure it out. I want to avoid time debugging and spend more time providing value to my users. I want to solve interesting, new problems instead of fighting glue code and *"whose dumb idea was it to implement it this way"*.

### REDUCE FRICTION ALWAYS

I get more things done when an architecture makes it easy to use. It's also way more fun being able to do everything super simply. It's worth the effort in naming things so we can meaningfully abstract bigger pieces of our systems. Going too far and getting lost in the sauce (look at you JavaScript) isn't being more productive.

Be realistic about your own brain's SIMD lanes and your agent's cognitive load. How much reasoning should either of us need just to figure out which function to call?

Of course business logic scattered everywhere isn't the solution either. Any abstraction is still bad when consumers need to learn or trust secret incantations to use your API. The more complex a system the more incantations the agent has to figure out too. No amount of documentation can explain or fix this. THIS HAS ALWAYS BEEN THE HARD PART. We perpetuate these design patterns and mantras to help "guide" development, but this quickly becomes the blind leading the blind leading the agent.

If you're struggling to understand it, why assume your agent can figure it out reliably? Have the agent HELP YOU UNDERSTAND it. Break down the behavior until you can name the pieces meaningfully yourself. Then those pieces can become useful APIs, repeatable practices, and easy to use [internal developer platforms](https://internaldeveloperplatform.org/what-is-an-internal-developer-platform/) that reduce the cognitive load of getting work done.

REDUCE FRICTION IN ALL AREAS. It gives you the power to abstract more things and spend more time providing unique value to your users. The running gag in dev culture is that extremely hard-to-work-with systems provide job security. Who knows to what extent if you can just throw the slop cannon at it. Complexity does not make products better regardless.

> ["*Start from the call you want people to remember, then make it obvious.*" — Dagger SDK documentation](https://docs.dagger.io/reference/sdks#designing-a-good-api)

We need to define what our system must do and understand the constraints the API will actually be used with before we can make it frictionless to use. Otherwise you're just making assumptions and asking the agent to make more of them.

### API boundaries must be obvious

Once you define the API your contract to the agent and the constraints it's expecting for your system are picked. If your agent wants to add bloat to your interfaces every time you touch an implementation detail, the implementation isn't "obvious" enough for the LLM. Naming is hard, but it's VERY important when determining the proper abstractions you need for easy-to-use interfaces. If I want to reliably prompt the agent to create features in the way I expect, the more obvious the design of my API and libraries used the more likely the next token will be the right one.

Name your functions first. Work backwards from what the most obvious thing the user needs is first. What does the CONSUMER actually care about? The consumer is your agent, the next developer, you in six months, or you actually reading the code for once. If my agent is using your API, I don't have time to debug your magic implementation. [“Don't make me think”](https://sensible.com/dont-make-me-think/) applies to APIs just as much as a UI.

`GetUser` works for a while. Eventually we realize fetching enough users that our `for` loop is making a stupid number of database round trips. What do I actually want to do? The API designer needs to implement `GetUsers`. What does the consumer NOT care about given the name we tell them to use? Caching, validation, maybe we want all users who aren't banned- there are behaviors we are implying we are NOT checking for by this name.

Your implementation should NOT be assuming this when you give it back to them. What is NOT obvious? Ordered users, etc? Instead of reaching for the [strategy pattern](https://en.wikipedia.org/wiki/Strategy_pattern) instantaneously maybe we can be obvious in the function definition by just sorting the users in place? A `SortUsers()` is more obvious than having the cognitive load of strategy patterns...

`GetUsers(Strategy, ids)` is not obvious in what it does. I'd prefer to use an API that looks like

```go
users, _ := GetUsers(ids)
SortUsers(users)
```

A single `SortUsers` could be too vague if we want to add more functionality later. `SortUsersBy(AlphabeticalDesc)` wouldn't be the worst pattern for grokking this abstraction. `FilterUsersBy` could be a feature we want to introduce later. I make it easy to expand the behavior of my library by keeping things as obvious in how they are used as possible. Every piece of functionality available in your system needs to be as obvious in how it's used to you as it is to the agent.

What about caching? Inside of `GetUsers(ids)` we can filter the query input down to the IDs we haven't already fetched earlier and put the results of all of the `ids` back together. This can be REALLY PERFORMANT and save work being done, OR it could cause race locks depending on your system. The original caller of `GetUsers(ids)` doesn't want to know about this, or be responsible for handling it (assuming we call `GetUsers` more than once).

A useful abstraction allows specific implementation details to be hidden so users don't have to be responsible for that work themselves. What matters for your implementations is up to you, the engineer designing it. If we didn't want to use any cache logic, we can split this out to `GetUsersNoCache` and `GetUsers`. You have to understand the needs of your user. You give a user the contract by calling the function `GetUsers`. More features just make you create more functionality. This is better than rewiring the OOP design that you were locked into from some other abstraction.

If you don't tell the LLM what you want, how will it ever create the scalable systems, performant code, the most secure design?

It's on us to make the behavior predictable and be able to rely on not breaking anything else when we check in code. If missing users, ordering, or cache freshness need explaining, a few-line comment above the function is totally fine. `// GetUsers returns []*Users unsorted` is as obvious to you as it is to the agent calling the function. The agent is reading it too, just like you would with your favorite IntelliSense or LSP.

I want my API to compose with ordinary `if` statements and `for` loops so I can simply follow the work, measure it, and change it. The cognitive load of building reliable software is already so complex when you're solving worthwhile problems. Always make your life easier.

### In conclusion

A valuable engineer develops their own heuristics that help them avoid wasting time that is not benefiting their users. We break down big problems into smaller problems, understand what tradeoffs we make as we solve each small problem, and how it affects the greater system. 

No amount of tooling can deterministically tell you what caused the LLM to hallucinate that endpoint to begin with. You can isolate a poorly designed, error prone system perfectly. Unfortunately, it's still a poorly designed, error prone system. 

A module's behavior should be easily inferred from how the API is literally named or used. The developer needs to be able to quickly grok if the LLM is giving decent results as huge vibe-coded diffs scroll in their terminal.

Easy-to-infer APIs are easy-to-use APIs. APIs should be implemented in a way so it's likely the next human, the next agent, and ESPECIALLY the next human using an agent has a chance at a decent PR.
