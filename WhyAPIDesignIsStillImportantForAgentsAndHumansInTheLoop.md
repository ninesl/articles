The more I learn about API design I find that the best architecture for a human is exactly the same way we want to design our APIs for agents.

A well designed API allows your agents to understand your code easier, therefore less $ spent on wasted reasoning tokens. Maybe you can bear the [cognitive load of your codebase](https://github.com/zakirullin/cognitive-load/), but there is no way to know what limits your agent has. Context windows change from model to model, and performance of these models can vary drastically between releases and the harness/tooling around it.

[CPU thrashing](https://en.wikipedia.org/wiki/Thrashing_(computer_science)), [agent thrashing](https://www.anthropic.com/research/multiagent-systems), and  [constant context-switching](https://pubmed.ncbi.nlm.nih.gov/11518143/) behave in the same way. It’s all wasted work which risk missing flaws in the software we build. Code still runs on a processor with limited registers, people have limited mental load/capacity, [agents have limited context and can experience conversation drift](https://arxiv.org/abs/2604.13061).

### Code matters more than it ever did

I keep thinking about how all this feels very similar to the how [complexity caused the software crisis in the late 60s](https://en.wikipedia.org/wiki/Software_crisis). There are more tools to create more software than ever. The bottleneck is creating reliabile, performant, extensible, testable, provable code. What it has been for the last 60 years. I'm willing to bet this will be the same for the next 60.

Back then everyone was writing COBOL and FORTRAN clusterfucks; now we're generating AI vibe-coded clusterfucks. We cannot make better software without being able to wrangle the sheer scale of entropy caused by LLMs. 

[Hashimoto's whiteboard defense analogy](https://x.com/mitchellh/status/2100249348345057389?s=20) plays a huge role in my philosophy when designing the implementation or ergonomics of an API. If an agent wrote the code and I ship it, can I explain why the system works, what could break from a change, why this design was picked in the first place? If I can't, is there really any way for me to verify the software does what I say it does? A green checkmark on the PR doesn't mean you know why it works. LLMs will never "know" why it works either.

We all are reading a LOT more code in this new AI age. If we aren't writing code anymore, [we still need to ensure you're not building a spaghetti-tangled mess so your users don't stop using your app from how slow it is](https://www.youtube.com/watch?v=tD5NrevFtbU). How the code actually works under the hood still matter even when you are moving abstraction layers up.

### Human-friendly architecture is Agent-friendly architecture 

An easy-to-use interface is an easy-to-infer interface. Clearer contracts and boundaries deter agents from having to guess (or hallucinate) how your system works.

```
Hard-to-use interfaces: 
- agents inspect half the repo ($ on tokens)
- agents infer conventions via reasoning ($ on tokens)
- prompts less likely have desired outcomes (SLOP)
- complexity encourages hack-y glue code (SLOP)
- create restrivice scaffolding tests that over-enforce behavior (SLOP)
```

This is an extremely frustrating situation for a human-in-the-loop. At best you're constantly handholding and correcting your agent which REDUCES productivity. The more slop code in your repo the more money you're spending on tokens. In my experience the tests AI agents, more from models like ChatGPT's Astra or Anthrophic's Fable, enforce it's generating the correct code by writing test-scaffolding that feels like scafoldding a skyscraper with a house of cards.

```
Easy-to-use interfaces:
- functions are named in a way so expected behavior is obvious (inferred)
- encourage agents next token is more likely to call the obvious thing (less $$$)
- remove those scaffolding tests without breaking something (trust the code)
```

Obvious interfaces mean less guessing, fewer `/undo`s, less tokens, and less slop. [Locality of behavior](https://four.htmx.org/essays/locality-of-behaviour/) and [grug-brained simplicity](https://grugbrain.dev/) help you understand your system without struggling to keep all of it's details and edgecases in your head. See [Carson Gross's talk on API design at BSDC 2025](https://www.youtube.com/watch?v=dTstnhS3moc). 

> *"Complexity very very bad"*

Agent software factories don't solve problems. Java OOP `AbstractBuilderPatternFactoryDAO()` and C++ `.h` issues/`namespace::` insanity make problems **HARDER TO SOLVE**. You need to avoid redundant or unuseful abstractions so your agent doesn't see a bunch of slop and want to make more slop. Why make what is already really difficult: creating reliable software, harder than it already is?

### Tools and techniques to consider

Once you define the API your contract to the agent and the constraints it's expecting for your system are picked. If your agent changes or wants to add bloat to your interfaces every time you touch an implementation detail, the implementation isn't "obvious" enough for the LLM. Naming is hard, but it's VERY important when determining the proper abstractions you need for easy-to-use interfaces. If I want to reliably prompt the agent to create features in the way I expect, the more obvious the design of my API and libraries used the more likely the next token will be the right one.

If we're never outrunning vibe-coded nonsense, why not invest in implementing scaffolding and pipelines that check the complexity, security risks, "obviousness", or "easy-to-use-ness" of whatever code developers are blindly shipping? Couldn't you just sandbox it and create exhaustive architecture tests? A more [deterministic AI tool like Jev](https://typesafe.ai/blog/introducing-system-one-models-and-jev) with or without MCPs could be the backbone of this kind of CICD pipeline.

How do you even write regression tests without instantly locking yourself into a specific design? A project like [SQLite benefits from its extremely comprehensive testing coverage](https://www.youtube.com/watch?v=V_qzqY1bb7) because its behavior has been defined and shouldn't change.

> ["*A wide and flat architecture is all about planning for growth and change, and then fostering the conditions that make change easy.*" - Evan DeMond's article on architectures](https://www.evandemond.com/programming/wide-and-flat)

Light code duplication or using flatter and wider abstractions are less cumbersome for a developer today versus any other time in history. We want to have less of a burden on our cognitive load when reading the code, trusting the code, and [grokking](https://en.wikipedia.org/wiki/Grok#Adoption_and_modern_use) the behavior of code. You want to avoid secretly inherited behaviors int the APIs you are using. We want to mitgate being blindsided by how a library works or an agent's implementation in a diff.

You also get the added benefit of quickly understanding code you wrote in the past or letting agents figure it out. I want to avoid time debugging and spend more time providing value to my users. I want to solve interesting, new problems instead of fighting glue code and *"who's dumb idea was it to implement it this way"*.

I've been using this ergonomics-focused tool called [Dagger](https://dagger.io) for my CICD pipelines recently. The Dagger API is designed in a way that your entire development pipeline becomes obvious from its actual programmatic implementation. The deployment of your app could live in the repo itself or the specific deployment environment's job to handle your repo's runtime instead of putting out fires in `Dockerfile` and `compose.yml` scripts. Every building block you're given has a usually very obvious job because every API function just does what it says it does.

Dagger is a good example of an API that can be both easy-to-use for humans *and* agents.

### In conclusion

I believe that no amount of tooling can deterministically tell you what caused the LLM to hallucinate that endpoint to begin with. You can isolate a poorly designed, error prone system perfectly, unfortunately it's still a poorly designed, error prone system. A valuable engineer should develop their own heuristics that help them avoid wasting time not solving business problems or benefiting users. We break down big problems into smaller problems, understand what tradeoffs we make as we solve each small problem in the greater system. A module's behavior should be easily inferred from how the API is literally implemented. You need to be able to quickly grok if the LLM model is giving decent results as huge vibed-coded diffs scroll by. Simplifying a complex system should be priority #0 so the next human, the next agent, and ESPECAILLY the next human using an agent have a chance of writing the correct implementation. 
