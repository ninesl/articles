The more I learn about API design I find that the best architecture for a human is exactly the same way we want to design our APIs for agents.

A well designed API allows your agents to understand your code easier, therefore less $ spent on wasted reasoning tokens. Maybe you can bear the [cognitive load of your codebase](https://github.com/zakirullin/cognitive-load/), but there is no way to know what limits your agent has. Context windows change from model to model, and performance of these models can vary drastically between releases and the harness/tooling around it.

[CPU thrashing](https://en.wikipedia.org/wiki/Thrashing_(computer_science)), [constant context-switching](https://pubmed.ncbi.nlm.nih.gov/11518143/), and [agent thrashing](https://www.anthropic.com/research/multiagent-systems) behave in the same way. It’s all wasted work which risk missing flaws in the software we build. Code still runs on a processor with limited registers, people have limited mental load/capacity, [agents have limited context and experience long conversation drift](https://arxiv.org/abs/2604.13061).

## Human-friendly architecture is Agent-friendly architecture 

An easy-to-use interface is an easy-to-infer interface. Clearer contracts and boundaries deters your agent from having to guess or hallucinate how the system works. 

Bad interfaces make agents: 
1. inspect half the repo ($$$)
2. forced to infer conventions via reasoning ($$$)
3. prompts less likely to get desired outcomes (SLOP)
4. complexity encourages hack-y glue code (SLOP)
5. (some agents do this) makes restrictive test scaffolding 

This is an extremely frustrating human-in-the-loop. At best you're constantly handholding which can REDUCE productivity.

What does an easy to use interface look like?
- functions are named in a way so expected behavior is obvious
- agents likely next token is to call the obvious thing (less $$$)
- easily remove those scaffolding tests without breaking something

Obvious interfaces mean less guessing, less slop, fewer retries and tokens. They can make cheaper models useful by having defined API constraints and expectations.

We all are reading a LOT of code in this new AI age. If we aren't writing code anymore, [we still need to ensure we don't have a spaghetti tangled mess, just for our end user's sake](https://www.youtube.com/watch?v=tD5NrevFtbU). Your module's behaviors should be easily inferred from how the API itself is implemented. You can quickly grok if the AI is giving you decent results as huge vibed-coded diffs scroll by.

[Locality of behavior](https://four.htmx.org/essays/locality-of-behaviour/), grug-brained simplicity, and easily inferred interfaces help you understand without struggling to keep the whole system in your head. See [Carson Gross's talk on API design at BSDC 2025](https://www.youtube.com/watch?v=dTstnhS3moc). "Complexity very very bad"

Agent software factories don't solve problems. Java OOP `AbstractBuilderPatternFactoryDAO()` and C++ `.h` issues/`namespace::` insanity make problems **HARDER TO SOLVE**. You need to avoid redundant abstractions so your agent doesn't see a bunch of slop and want to make more slop.

### The current mess

I keep thinking about how all this feels very similar to the 60s software crisis. We have all these new tools for making more software but there is a bottleneck with reliability, scalability, testability ESP with agents introduced. It's the same underlying issue: we are producing complexity faster than we can understand it.

Back then everyone was writing assembly clusterfucks; now we're generating AI clusterfucks at 100x speed. Simplify the system so the next human AND the next agent and ESPECIALLY the next human using an agent has a chance of writing the proper code.

### What are the types of tools and techniques we should adapt

If we're never outrunning vibe-coded nonsense, why not invest in implementing scaffolding that checks the complexity, explicitness, wide/flat easy to use interfaces, security risks and expectations of whatever people are blindly shipping? Couldn't you just sandbox it and do pen tests? A more [deterministic AI tool like Jev](https://typesafe.ai/blog/introducing-system-one-models-and-jev) or more useful MCPs could be the backbone of this kind of CICD pipeline.

> How do you even write regression tests without instantly locking yourself into a specific design? [SQLite's reliability and its extremely comprehensive testing coverage](https://www.youtube.com/watch?v=V_qzqY1bb7) works because its behavior has been defined.

Once you define the API your contract to the user and the constraints for your system are picked. You can be more confident when rewriting the guts and still reliably test the contracts. If your agent changes or adds bloat to your interfaces every time you touch an implementation detail, the implementation isn't "obvious" enough for the LLM. And more than likely you don't know what the code is supposed to look like.

Naming is hard, but it's VERY important when determining the proper abstractions we need for easy to use interfaces. If I want to reliably prompt the agent to create features in the way I expect, the more obvious the design of my API and libraries used the more likely the next token will be the right one.

> In my experience the tests AI agents (esp something like ChatGPT's Astra) want to make will make your entire architecture be enforced by skyscraper-scaffolding built with a house of cards.

I've been using this ergonomics-focused tool called [Dagger](https://dagger.io) for my CICD pipelines recently. The Dagger API is designed in a way that your entire development pipeline becomes obvious from its actual programmatic implementation. The deployment of your app could live in the repo itself or the specific deployment environment's job to handle your repo's runtime instead of putting out fires in `Dockerfile` and `compose.yml` scripts. Every building block you're given has a usually very obvious job because every API function just does what it says it does.

I believe that no amount of tooling can deterministically tell you what caused the LLM to hallucinate that endpoint to begin with. You can isolate a poorly designed, error prone system perfectly. Unfortunately it's still a poorly designed, error prone system.

## Wide and flat

> [_A wide and flat architecture is all about planning for growth and change, and then fostering the conditions that make change easy._ - Evan DeMond's article on wide and flat architectures.](https://www.evandemond.com/programming/wide-and-flat)

Code duplication or a flatter and wider abstraction is less cumbersome for a developer than it was ever before. Especially if they are not writing the code themselves. Reading the code, trusting the code, and grokking the behavior of your code becomes less on your cognitive load because there are no secretly inherited behaviors of the APIs you are using. You are not blindsided by how a library works or an agent's implementation in a diff.

You also get the added benefit of more quickly understanding your old code or letting agents figure it out. I want to avoid time debugging and spend more time providing value to my users. I want to solve interesting, new problems instead of fighting glue code and *"who's dumb idea was it to implement it this way"*.

Hashimoto's [whiteboard defense](https://x.com/mitchellh/status/2100249348345057389?s=20) analogy plays a huge role in my philosophy of designing the implementation ergonomics of an API. If an agent wrote the code and I ship it, can I explain why the system works, what could break from a change, why this design was picked in the first place? If I can't, is there really any way to verify the software does what you say it does? A green checkmark on the PR doesn't mean you know why it works. LLMs will never "know" why it works either.

A valuable engineer should develop their own heuristics that help them avoid anything that isn't solving business problems or benefiting users. We break down big problems into smaller problems, understand what tradeoffs we make as we solve each small problem in the greater system.

> something esoteric and anthromorphozing to the lossy search stocastic parrot
