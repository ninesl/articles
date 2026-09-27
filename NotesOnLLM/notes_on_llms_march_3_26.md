fun quirk i've noticed with the newer models,

opus 4.6 is really good at compaction. it doesn't miss a lot of stuff and generally can figure out how to get started again

codex 5.3 i think is the best at reviewing code/figuring out parts that are connected. This is just my exp and probably is super dependant on codebase patterns.

kimi k2.5 is the fastest and if the servers aren't getting bombarded it is definitely the best $/tok price. 

I'm going to try some of the new qwen 3.5 coder local models that came out I think you can harness opencode up to it pretty easy. Or I have opencode it for me lmao

so I usually plan with 4.6 sonnet, do harder stuff on opus, codex when I'm trying to review/write docs, kimi when I need to iterate and sonnet on impl. 

Basically still think the super high reasoning models are bad at least for coding. You finally get the patterns it needs and htne if it thinks for 10 minutes it'll lose it all. so it's better for a kimi or a sonnet to do straight integration, like here is the specs now implement it based on the patterns of the codebase.

Like my caching thing again is easier for sonnet to do it than opus NGL. Maybe opus can do more complex integrations but atp you should be doing it yourself

I will have max thinking on when I'm trying to figure out the data structures.

number 1 use case for it all is still just rubby ducky chatbot that can sometimes autocomplete if you're lucky

It allows me to work in fields that I otherwise would have been impossible for me to tackle. I can confidently figure out a lot of systems just by banging my head against the wall into the LLM just like I would be if I was googling for 12 hours. I can verify llm's BS on a new topic easier than I can figure out what I need to do. 

SWE is a man-made field where all terminology is nerds arguing SYNTAX literally. There's a million ways to skin a cat and the best way for any system is really 'man it depends.' That's why we get paid so much, that's why the top engineers get paid even MORE money they produce for the company. Like the x value on the best enineers for reveunue likely is a WORSE multiple for entry level devs. Reasoning about a system to reduce costs in cloud compute, whatever it why we get paid the big bucks in the first place. An agent can iterate and iterate and iterate to find best 'perf' but using an analogy from speedrunning, TAS assisted doesn't mean fastest. New ideas, shortcuts or strategies emerge from humans, not AI. I will die on this hill, clanker. 

AI can helps humans get inspired, but arguing about where the muses of engineering to any creative endeavor is not what this discussion is about. The flow-state of figuring out the problems thru your hands is tough for me. I can think about how I want my architecture to look in my brain going into a project, and it's just TOO enticing to 

I've trained myself to go 'eughhh' when I open up my editor for anything other than diffs or to change 2 sections of an LLM-caused error. I hate it. I hate it and since I've done this my speed at programming has plummetteddddd. Down the drain. I don't have the motivation if I'm not in the flow state, but the big red 'do it in one shot' button is to ogood. Or maybe 3-5 times, and I fall into literally what we call gambler's falacy. It's exhausting, truly. I want to code again, but typing out variable after variable in boilerplate code or w/e is tiring... I can make the LLM do this. But if it's wrong and I argue with it for 1.5 hours I could have just typed the whole thing up correctly in 30 minutes compared to what the llm output quality likely is. But sometimes that puts me weeks ahead of schedule and allows me to do more work and responibility at work which is what I want to progress in my career. I don't want to spend my days writing dumb features I want to design auto scaling webapp platform with my own light version of caching so I don't even need redis or anything.

We are reaching the point where you can get sonnet 4 on your laptop. If we can get opus 4.5 or even sonnet 4.5 off of a distilled kimi 3 or w/e is coming it's fucking over.

Literally pewdiepie trained a llm that beat 4o on some benchmarks. now that's a shitty model for real business use cases but the trendline is obvious 

like anything beyond this can't make good software, and it's not getting better. Context engineering is just a new workflow for SWEs. It's abstracting the job to know as the engineer what context is relevant or needed for the problem and developing workflows/patterns to make the autocomplete make your job 'easier'. 

But it all feels like TS type masturbation to a certain level. I still can't think of a reason you'd ever want an MCP because it just feels like it's become unreliable. You're doing all this work have it do some workflow why can't we just fucking send api calls?? Security issues and prompt injection galore. If we're down to it's just for openclaw to grab any context it wants well bye bye security so having agents run production decisions is just a non-starter.

Every week there is some new CVE or vulnerabilty bc the AI just can't design systems the way a smart security researcher would. Then 10x engineer really means 10x the work 10x as fast for 1x the pay and the amount of dev burnout is going to ruin the industry 

I miss coding and being in the flow-state. I can't get flow-state from archietecture work only, but maybe this is the natural progression of things as an engineer.
