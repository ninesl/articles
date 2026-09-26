## 

The more I learn about API design I find that best architecture for a human is exactly the same way we want to design our APIs for agents.

A simpler designed API makes agent performance better, therefore less $ on tokens and wasted reasoning. Maybe you can bear the cognitive load, but how do you know what details your AI keeps in it's context window? 

How do you make it MORE likely for your stochastic parrot to create the code you want? [Straightfoward, grug-brained](https://grugbrain.dev/) interfaces help models generate the correct code just as much as they help you understand what the code is actually doing. Cheaper models (your code wont need the same capabilities to understand convoluted monstrosities) becomes more appealing and you get the benefit of more reliable software.

API design benefits the agent just as much as you, if not more so. The AI writes the code, right? Let's design software architecture that can benefit the agent the same way we think about our own mental load. This generally is going to still be the same mantra as all performance aware code should be, because YOU YOURSELF live in reality where your code runs on a processor.

 CPU thrashing, constant context-switching, and [agent thrashing](https://www.anthropic.com/research/multiagent-systems), behave in the same way. It’s all wasted work which can risk missing flaws in the software we build. Experienced software engineers can recognize wasteful abstractions because their wisdom allows them to avoid footguns. We should design our APIs to make it HARD to have a footgun. Users implementation your API should encouraged to use patterns that AVOID potential footguns. This in my opinion has always been the job. Code still runs on a processor with limited registers, people have limited mental load/capacity, [agents have limited context experience long conversation drift](https://arxiv.org/abs/2604.13061). A simple API makes what already is really hard (building good software) easier to do. 


## Human-friendly architecture is Agent-friendly architecture 

The point is not “fewer lines of code.” The point is explicit, easy-to-use interfaces. clear contracts and boundaries/defined constraint,, the agent doesn’t have to guess or hallucinate how the system works. Agent Software factories don't solve problems the same way that Java OOP AbstractBuilderPatternFactoryDAO() don't solve problems the same way that C++ inherited header files and `namespace::` insanity makes problems **HARDER TO SOLVE**, not easier.

Bad interfaces make agents: 
1. inspect half the repo ($$$)
2. forced to infer conventions via reasoning ($$$)
3. prompts less likely to get desired outcomes (SLOP)
4. complexity encourages hack-y glue code (SLOP)
5. (some agents do this) makes restrictive test scaffolding 

This is an extremely frustrating human-in-the-loop. At best you're constantly handholding which can REDUCE productivity.

What does a easy to use interface look like?
- functions are named in a way so expected behavior is obvious
- agents likely next token is to call the obvious thing (less $$$)
- easily remove those scaffolding tests without breaking something

Obvious interfaces mean less guessing, less slop, fewer retries and tokens. They can make cheaper models useful by have defined API constraints and expectations. Jev or other tooling looks promising for these types of situations for correctness. This is all to services less hallucinations/hacky agent slop code.

We all are reading a LOT of code in this new AI age. The more I trust my system's behaviors and APIs the more I trust the agent's output and when I need to understand when I need to dive into a specific implemenation. API ergonomics matter for reading too. If we aren't writing code anymore, [we still need to ensure we don't have a spaghetti tangled mess, just for our end user's sake](https://www.youtube.com/watch?v=tD5NrevFtbU). Your module's behaviors should be easily inferred from how the API itself is implemented. This makes reading huge vibed-coded diffs easier. You can quickly grok if the AI is giving you decent results as it's scrolling by.

[Locality of behavior](https://four.htmx.org/essays/locality-of-behaviour/), grug-brained simplicity, and how your easily inferred your interfaces help you understand without struggling to keep the whole system in your head. See [Carson Gross's talk on API design at BSDC 2025](https://www.youtube.com/watch?v=dTstnhS3moc). "Complexity very very bad"

### The current mess

I keep thinking about how all feels very similar to the 60s software crisis. We have all these new tools for making more software but there is a bottleneck with reliability, scabilitiy, testability ESP with agents introduced. It's the same underlying issue: we are producing complexity faster than we can understand it.

Back then everyone was writing assembly clusterfucks; now we're generating AI clusterfucks at 100x speed. More tokens won't fix interfaces nobody understands. Simplify the system so the next human AND the next agent and ESPECIALLY the next human using an agent has at a chance of writing the proper code.

### What are the types of tools and techniques we should adapt

If we're never outrunning vibe-coded nonsense, why not invest in implementing scaffolding that checks the complexity, explicitiness, wide/flat easy to user interfaces, security risks and expectations to whatever people are blindly shipping? Couldnt't you just sandbox it and do pen tests? A more [determinstic AI tool like Jev](https://typesafe.ai/blog/introducing-system-one-models-and-jev) or more useful MCPs could be the backbone of this kind of CICD pipeline.

> How do you even write regression tests without instantly locking yourself into a specific design? [SQLite's reliability and it's extremely comprehensive testing coverage](https://www.youtube.com/watch?v=V_qzqY1bb7) works because its behavior has been defined. 

Once you define the API your contract to the user and the constraints for your system are picked. You can be more confident when rewriting the guts and still test reliably test the contracts. If your agent changes or adds bloat to your interfaces every time you touch an implementation detail, the implementation isn't "obvious" enough for the LLM. And more than likely if you don't know what the code is supposed to look like.

Make it OBVIOUS what your functions do. Naming is hard, but it's VERY important when determining the proper abstractions we need for easy to user interfaces. If I want to reliably prompt the agent to create features in the way I expect, the more obvious the design of my API and librarires used the more likely the next token will be the right one.

> In my experience the tests AI agents (esp something like ChatGPT's Astra) want to make will make your entire architecture be enforced by skyscraper-scafolding built with a house of cards.

I've been using this ergonomics-focused tool called [Dagger](https://dagger.io) for my CICD pipelines recently. The Dagger API is designed in a way that your entire development pipeline becomes obvious from it's actual programmatic implementation. You and especially your agents have the ability to understand it's behaviors clearly. The deployment of your app could live in the repo itself or the specific deployment environment's job to handle your repo's runtime instead of putting out fires in `Dockerfile` and `compose.yml` scripts. Every building block you're given has a usually very obvious job and agents can easily understand what it needs to know because every API function just does what it says it does.

I believe that no amount of tooling can determinsitcally tell you what caused the LLM to hallucinate that endpoint to begin with. You can isolate a poorly designed, error prone system perfectly. Unfortunately it's still a poorly designed, error prone system. 

## 

> [_A wide and flat architecture is all about planning for growth and change, and then fostering the conditions that make change easy._ - Evan DeMond's article on wide and flat architectures.](https://www.evandemond.com/programming/wide-and-flat)

Code duplication or a flatter and wider abstraction is less cumbersome for a developer than it was ever before. Especially if they are not writing the code themselves. Reading the code, trusting the code, and grokking the behavior of your code becomes less on your cognitive load because there are no secretly inherited behaviors of the APIs you are using.

You are not blindsided by how a library works or an agent's implementation in a diff. I want to stress again how this makes it SO much easier on your cognitie load.

You also get the added benefit of more quickly understanding your old code or let agents figure out your old code. I want to avoid time debugging and more time providing value to my users. I want to solve interesting, new problems instead of fighting glue code and *"who's dumb idea was it to implement it this way"*.

Hashimoto's [whiteboard defense](https://x.com/mitchellh/status/2100249348345057389?s=20) analogy plays a huge role into my philosphy from desigining the implementaiton ergonmics of an API. If an agent wrote the code and I ship it, can I explain why the system works, what could break from a change, why this design was picked in the first place? If I can't, is there really anyway to verify the software does what you say it does? A green checkmark on the PR doesn't mean you know why it works. LLMs will never "know" why it works either.

A valuable engineer should have development practices and develop their own hueristics that help them avoid anything that isnt't solving business problems or benefiting users. We break down big problems into smaller problems, understand what tradeoffs we make as we solve each small problem as it tradeoffs in the greater system. The less complexity on your cognitive load the better you can modify parts of your system. And guess what, this is best thing for your agents too.

Who knew the best things for agents has always been what was best for humans too...

> something esoteric and anthromorphozing to the lossy search stocastic parrot

