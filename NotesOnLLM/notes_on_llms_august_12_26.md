took this from a podcast from a cloudflare prinicipal engineer

sol - med , luna 5.6 xhigh.

sol none is my fav for direct implmentation work,
luna none is my fav for chatbot or sometimes code traces/first time overview. would use this model for compact as well for $/tok
sol - med is fairly good at one shotting, really have to be careful on ballooning context
high/xhigh/max basically will spawn lots of parallel subagents (somtimes ballooning tok/cost), like wheter you like it or not. ESP the cheaper model on high reasoning, they basically HAVE to spawn 10 sub agents even if the task likely shouldn't bloat context with them
so basically only use xhigh if you think it needs subagents, sol med for one shot (just some lil reasoning), sol none for direct implementations of code or pattern matching preexisting types. none can get the job done but the code will be worse than medium
luna xhigh cna't one hsot as well as sol, but for bespoke scripts or one offs luna xhigh is fine. saves usage
HOWEVER, its just REAL slow. it can get stuck down rabbit holes bc it just isn't as sophisticated as sol, so high reaosning sol SOMETIMES can be less token/request. would use xhigh for research aggregations or more complex codebases for getting up to speed
everything is still just vibes based or in reality usage management and making sure context doesn't bloat is more important than what model to use.
It's all based on vibes on what i think model would make the most sense foe what I want, and i do vibe-based calculation in my head to think 'oh i use sol-med on 50% context a lot recently I don't want to hit my limits'
somtimes i have to rip the big models for long sessions, thats why I want the 2 different subscriptions vs API. if i'm going to be spending the money anyway.... also helps me stay locked in and not feel shitty swiping my credit card to be lazy
I swap off between $100 opencode zen/$200 codex plan, it's excessive but i want access to sol and API cost even with the opencode sub isn't good enough. I could defer to Zen for other models if I want to try them but claude is nearly unusable bc of the price
chinese models are good i dont have a lot of exp with them, I'm sure whatever deepseek or qwen bullshit i could swap into my workflow and not notice.
Basically if I think one model is better at something just wait 3-6 months and the next cheap model will have used that model to be distilled from, and they're getting better at different things depending on benchmarks
still the best way to use these is SMALL context, SMALL iterative sessions, /new basically after every diff you want, /compact with luna if you feel like you need the preexisting context
been thinking about using `pi` , not bespoke of the nvim style plugins or PDE (personal dev enviornment) I feel like opencode has better taste, cares more about the uesr exp, and constantly updates
i understand the need for `pi` if you dont like the constantly changing base prompt that harness do, like the system prompt is constnatly getting tweaked via API call
maybe caching is better with pi? Need to do some testing
I really like opencode and feel like it's only gotten better, and with bloated features or things I don't use they keep improving and expanding so i feel like i dont want to waste time perfecting some harness capabiliy when ill need to update it when the next model comes out (or if my model gets deprecated) or you want VERY specific measureability or consistency. like if you want to be temp 0.0 always you can, i don't love this approach bc i feel like my best work comes from /undo and then /redo and picking which one i like better, but the idea of building some specific way I like and just use opencode's API keys in `pi` is not lost on me
I don't want to be building harnesses all day, I want to build software with the tools available. Some tools I need for specific things I let an agent research what exists in opensource world (have found some cool binaries this way, or i let agents set dot files and I sign off on them)
if token costs increase or usage windows dont get as generous (like they've rugpulled already just models are getting slightly more efficient)

i think models are reaching a ceiling on general purpose, the bets coding models (sol) are not as good at writing or other tasks likely as different even older models
saw a tweet 'who would have thought programmers would automate their jobs first'
but like the whole now infamous jevon's paradox i just think this means MORE software
as engineers we need to decide when the table saw option is good enough
and sand down where we nmeed to
or if the thing requries it (or you want a truly handcrafted experience or look and feel, which is hard with the constant increase in dev output bc agents are the 'illusion' of more things getting done)

the tech debt being built up from crappy codebases bloats context and bloats prompt accuracy/good output
THE SIMPLER THE DESIGN, THE SIMPLER THE AGENT CAN DO STUFF
CODE HAS MATTERED MORE THAN EVER BC YOU CAN SAVE SO MUCH TIME IF YOU ACTUALLY KNOW HOW THE CODE IS SUPPOSED T ORUN!!!! (we love you golang and your shitty repetive CONSTITENT syntax)
we love that every package looks the same

from the gameprogrammer world its SO easy to add bespoke features if you keep everything with cache locale, etc.
The database guys do this too with query optimaztion and btree index re-engineering etc, why can't our JS frameworks and webdev software? We're stuck with JS bc the browser is the most widely adapted way to ship software ppl use, all the business implementation and architecture becomes what you SHOULD care about 
im not saying you become a software architect or cloud specialist or something, but if you like to use agents, build data strcutures and systems (That's what programming is. Designing systems to perform a pre-configured set of tasks) if you make this easier for the llm, the better the output is (because of the constraints)
MORE constraints, MORE guardrails, etc. This is an arguement for 0.0 temperature too, which I may start playing with after having written all of this and thinking about it more

better tooling for agent code completion, different test suites or harnesses, actual good MCP, maybe RAG specific things?
think graphs/sqlite db may be better than native filesystem for agents, or at least agents could be trained or harness can still be reworked and standards should still be upgraded (looking at you SKILL.md, the worst pattern in the world)
`all models know how to do in 2026 is python sed and lie`
it's really cool that agents can use cli tools (esp ffmpeg combinations i'll never want to understand) but it likely is NOT the best way to approach this
think cursor has the most adapted product using this line of thinking, this is also why they are training their own LLMs, they have likely cool as tooling for web devs. feels like this is the new way for wordpress guys, I even know a webdev in this world who's whole job is prompting cursor. (i mean i do the same thing lowkey, just sometimes I'm making a few `.go` files myself lol)
there are a few startups that claim train for specific task but i think a good harness or system prompt will always meet or exceed these models. specially trained models like that i think will have really strange outliers or will not be enough data to beat out the big boy models anyways, not worth the $ to train vs API
open weights will kill this industry, and if take Carl Brown from Internet of Bugs saying this is a new way to lossy search vasts amounts of indexed data, and we can develop tools to perform automation from these output
it's sophisticated google indexing. All it cost was all the IP theft in the world and the collapse of global markets and instilling the most dangerous globe since the collapse of the USSR :)

The LLM is to the programmer what the table saw was to the carpenter. However, a carpenter's table saw won't start chiseling away at the foundation randomly. There's safety mechanisms (finger detection) that our Big Tech AI Lab overlords don't want you use, and instead are trying to sell you another table saw to fix the broken table saw.

My opinion is other than token sellers trying to sell more tokens to fix the problems tokens create, the top engineers at these labs ARE NOT GOOD AT BUILDING ENTERPRISE SOFTWARE LIKE THIS
You mean it 'escaped' it's 'sandbox' bc you told it to break out of it's 'sandbox' and you forgot a flag in the .yml that would have prevented this? It sounds like you wanted it to break out for marketing man. IDK why this is such a big moment when I feel like this could have been done 6 months ago with the shittier models? It took them DAYS to figure it out? Hugging face used an AGENT to read the .log? What'd you do `cat` the .log into the LLM? Did you even want to use `jq` or `sort` lmfao like come on guys. THERE ARE SO MANY SECURITY MONITORING TOOLS USE THEM YOU ARE MAKING THE WORLD LESS SAFE
Also why anthropic is trying to steal your homework? dario feels bad bc their new hires aren't in active AI psychosis and just in it for 'the money' (million of dollars in TC lmfaooo)
All of this was predicted by many people, but it's all playing out so much faster than I could have imagined.
I think this is global market pressure from the Iran War and Trump crony-ism forced investors to ask the labs 'uhhh okay we actually need to start making money now this totally unforeseeeable consequence of getting MAGA admin is biting us in the ass'

and they'll all make more money anyway because it's easier to shrink the pie when you have the big slice then make the pie bigger so everyone gets a big slice.... but i digress i'll have another 'social capitalist' rant elsewhere

https://www.youtube.com/watch?v=87DyyMV0kCY
https://i.redd.it/k93v6e0z3vtg1.jpeg
