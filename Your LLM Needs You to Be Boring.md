# Your LLM Needs You to Be Boring

#### Lance Nines

#### 9-15-2025

It's not a controversial opinion in September 2025 to say that LLMs are *not* going to be taking your job if you're a software engineer. LLMs cannot literally reason out problems like a human being can. As we all get more accustomed to the output these things have, the magic starts to wear off and the quirks of models are increasingly apparent.

In my experience LLMs are really, really good at understanding patterns. Like, that is all they literally do. The weights of these models can get unbelievably complex and hard to understand, but we generally can assume what patterns (the training data) the LLMs know. Agentic tooling like Claude Code (I'm partial to `sst/opencode`) lets the LLM use `grep`, `find` and a litany  of other Unix tools to help it gather context in an efficient, repeatable way. I've seen some developers share that the underlying model becomes less relevant as long as it's tool calling is good. Anthropic has been leading in this approach for a while now but maybe xAI's Grok v69 will be better next week. The point is that we are reaching (or have reached) diminishing returns when it comes to improvements to the underlying models, AI labs around the world have begun admitting as much. 

If there's one positive thing you can say about LLM's coding ability that likely wouldn't be challenged even by the most anti-LLM developers out there is that it is excellent at making student projects, small static html/css sites (think making a nonfunctional `spotify` clone lookalike in one shot) or solving leetcode problems. The type of code you'd find in Youtube tutorials, online project walkthroughs, student projects or random Github repos. This logically makes sense as it is *literally* the code these LLMs were trained on. The types of things that hiring managers and your coworkers easily gloss over on your resume (TO-DO app, React e-commerce site). Student projects, popular leetcode problems, documentation, the html/css of the sites themselves, online tutorials, college classes are the training data itself.

If you are trying to leverage agentic tooling, aka "viBE cODiNg", you need to understand that the agents can only reliably accomplish very specific, generic tasks. Here's where my logic on this comes from: Boilerplate NEEDS to exist SOMEWHERE in some form. This has been abstracted in 10,000 different ways by the newest JavaScript library (this week), `Spring` in Java, `fastapi` for python, or the `stdlib` in Go just to name a few. Although there are 10,000 different ways to  make boilerplate code, there are definitely a few that are far more popular than the rest. The reasons for this are countless, and arguing over why Spring Boot is the defacto way enterprise does thing vs something else is missing the point. Spring Boot has LOTS of content about how to set up it's annotations, configurations etc online. The amount of example code online that exists is virtually limitless, (compared to something like your own handwritten C HTTP server). Most Golang code is written in a very stylized, opinionated way called "Idiomatic Go." If you're someone who has used Go for some time you'll start to realize that the language almost fights you if you try to force some other paradigm (factory patterns, etc.) that Go was not designed for. Idiomatic Go written by me looks like Idiomatic Go written by you, or at least that's the idea. In practice keeping your codebase idiomatic helps play well with the expansive `stdlib` Go has, making most Go code look the same.

You probably see where I'm going with this by now. **Picking a tech stack that has LOTS of presence online is the only way you'll get anything 'production-worthy' out of an LLM.** You cannot expect Claude Code to be able to use some unknown JS library that came out last week. You just cannot get the same level of output as you would with a popular language or framework. "But Lance" you say, "The code still sucks ass when you want it to do XYZ". Is XYZ something that not everyone already knows how to do? Is it something non-trivial, non boilerplate? It likely will NOT be able to help you.

Here's the final piece of the puzzle to getting the most out of AI agents. **The patterns of your codebase MUST be well established to be able to have the LLM be successful.** What do I mean by this? Let's say we want the LLM to add a endpoint to our Go webserver for gather the JSON data of a given User. A very common outcome in this is for the LLM to just inline the SQL, concatenate every field returned into a string with `{}` appended to the beginning and end. This solution satisfies the prompt, is extremely simple, and likely uses very few lines of code. However, that is definitely not what we want, (at least it shouldn't be). Let's break down what the LLM actually need to be able to do for this basic problem:

```
1. How to get the inputted UserID/read the request
2. How to query the DB for the User
3. How to read the SQL
4. How to modify the SQL into the model
5. How to marshall the User object in JSON
6. How to return the JSON
7. How to name the function
8. Where to put the function
9. How to set up the endpoint
10. Where to put the endpoint
11. What endpoint to use
12. What other content, headers etc. needs to be in the response
```

You need to break down HOW the LLM is supposed to do this.

How does the rest of the codebase usually get the UserID? Middleware? Is it part of the request? Where is this request? Is it part of the function signature? Is this request something we need to account for where it's coming from? 

Simply tell the LLM exactly how you want it to do it.

````
Create a method in @handlers.go that is called HandleGetUserJSON(). This codebase always fetches users by the ID using Get{model}ByID(db, id) in @queries.go. The db will always come from the global Config in @config.go by using GetActiveDB() *sql.DB , that handles race conditions. The userID will always be in the body of the HTTP request as '{ userID: %d }' use the stdlib for this. then return the user with (*model.User) func AsJSON(). In @router.go we are using Chi and it should look like m.Get("/user", HandleGetUserJSON()). put it below the rest of the routes. The status will be 200 if okay, otherwise use LogHTTPError in @logging.go 
````

There are a lot of established patterns in this project as you can tell based on the prompt. We have `chi` routing, custom logging, embedded JSON marshalling/unmarshalling and specific way to do db access. Although very basic, the scope of this prompt has stretched out into various files and expectations about how the data is manipulated that LLM cannot know off the rip without any guidance.  

Every DB function in your code now HAS to look like `Get{Model}ByID(db, _ID) (*model.___`). Your APIs must be explicit. Imagine you pressed `.` on a struct and you're searching your editor for all of it's object level methods. When the LLM uses `grep *Get*ByID*` it will instantly see all the function signatures and the models they return. By keeping CRUD patterns consistent, our function names consistent and OBVIOUS the LLM will be able to search your codebase and understand what context it needs more effectively. Your functions should also have similar behavior because the LLM is going to assume they do. 

Instead of going crazy with MCP servers, standardize the APIs you want the LLM to use. The LLM makes assumptions based on the patterns it's discovering (AND based on patterns of other codebases in it's training data). Make it easy for it! If you want it to get the User, have it ALWAYS use GetUserByID. Keeping data access the same, and being explicit in HOW you want it to access the data will help your LLM stop hallucinating patterns you don't want. Write some documentation (ye olde `AGENTS.md`) that has your patterns and assumptions so the AI produces the code how you want it to with more consistency.

This is a LOT of hand holding you have to give the AI. I'd agree with you that it seems counterproductive, and [some studies are coming out showing that developers may actually be LESS productive when using AI tools](https://arxiv.org/abs/2507.09089). I tell Gemini to make a new feature, follow these patterns and rules, press enter. Now I'm pulling up my phone, I'm firing up a game of TFT, the 2 minutes it takes for the `Thinking...` allows my ADHD ass to get completely distracted. Instead of waiting for code to compile, I'm waiting for the AI to one-shot something I likely would have gotten done faster myself in a lot of cases. If I allow myself too much reliance on the AI tools it's like my brain starts to atrophy and I feel dumber. But I also hate writing CSS (not good at it) and the LLM can iterate through making webcomponents faster that I ever could, following the advice from this article. I fear that this will have a sort of Dark Ages effect on programming as a whole. If LLMs are only good at React because that's all that it knows... We better all start learning React. (or should definitely NOT? idk)

[https://arxiv.org/abs/2507.09089]: https://arxiv.org/abs/2507.09089