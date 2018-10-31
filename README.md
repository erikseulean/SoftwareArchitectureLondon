# Software Architecture London

#### Building evolutionary architectures
- Try to keep the performance of your codebase as the architecture evolves. 
- don't think about architecture as a one off thing
- decision changes as new infrastructures or tools appear
What javascript framework will you be using 2 years from now ? 

1. incremental changes
2. guided
3. across multiple dimensions

##### Guided - Fitness functions
- Using a fitness function, you're getting better and better. 
<b>Architectural fitness function</b> objectivity in assessing your architecutre. 
- Fitness function - anything that can be used to assess(a metric) an architectural characteristics

Types of fitness functions: 
- triggered, continuous, atomic, automated, manual, dynamic, domain specific/agnostic

- Use cyclic dependency checker and testing around this
- Pass test ownership to the team that's doing the infrastructure
- Chaos Monkey
- Eg. write a test that doesn't allow to throw generic exception, one that doesn't allow to use certain logging system. No interface starting with I or ending with Interface 
- Use written rulles in documents to make tests and not let people bypass them 
- Test for hashing license files
- Reuse less to reduce coupling (Duplication). Tradeoff.

Domain partitioning vs Technical Partitioning
Usually the changes are regarding a certain domain instead of technical changes. 

Reduce quantum size to soemthing useful (smaller domain). Smaller quantom, more evolutionary architecture. 
You should have a performance fitness function.
- Whenever you tackle a techinical debt, try to add a metric around it and maintain it in time to avoid getting in the same situation again
- Use chaos monkey that is checking for services that aren't used anymore and cleans up automatically.

Check out Microkernel


#### How to build a modular monolith
- How to break ?
- How big ?

##### How big ? 
- Use Bounded Contexts to define the size of the microservice. 
- https://isis.apache.org/ - DDD + Storage options
- Uses isis to focus on domain and let the library take care of the infrastructure and gluing.
- Use DDD Bounded context but not separated in microservices in a nutshell


### Chaos engineering (at DAZN)

- problem is that there's too much emphasis on breaking things
- the goal is to learn about how the systems fail and build confidence
- the goal is not to berak production

#### Steps 
Principles of chaos:

1. define a steady state. If a system is on fire all the time, you're not ready to run chaos testing
2. hypothesise steady state will continue in both control group and experiment group. You should have a degree of confidence that the system is going to behave well.
- Explore in an environment that is not PROD initially. When you're confident, move to production.
- If you know it's going to break your production system anyways, you're not going to gain anything. 
3. Inject cases that are plausible. 
- Check Gremlin
4. Disprove hypothesis
- look for evidence that the steady state was impacted. 
- control your experiments
- communicate what you're doing, make sure that the stakeholders and other teams know what you're doing.
- run experiments during work hours and not during important times to avoid unnecessary risk
- have a rollback plan ready 
- stop the experiment right away
- practices of chaos engineering can be applied at any stage not just to production environments.
- when talking to business don't talk about chaos but talk about testing and continuous integration, to win the business. Your goal is to increase resilence, which has to be communicated to business



What you can fix: 
- chained service failures
- missconfigured timeouts
- regional failovers

##### Latency injection with serverless
- apply same 4 steps. 
- define your metrics: latencies, error count, percentage of requests done, etc.
- hypothesise what is going to happen when you introduce failure. 
- helps you find the right timeout value for your services.

Chained requests - how to split timeouts: 
- equally 
- optimistic, given all the services the same amount close to the total timeout. 
- set timeouts dynamically - check remaining time and give that time to the api call. 
- if you know you'll timeout, you can log everything. 

Where to inject latency ? 
- make sure you control the blast radius so you dont affect too many clients. 

### Architecting for Data driven reliability
- 1956 J von Neumann
- 1986 J Gray - Why do computers stop and what can be done about it ?
- Velocity (engineering, proactive, change) and Reliability (support, reactive, preserve) 
- 1883 - in order to have reliability you need to measure reliability
There are not many tricks in the book:
- redundant resource (extra disk)
- degraded results (tradeoff)
- retry transient failures (trade latency)
Everytime you improve reliability you increase complexity.

1. Research (what are the numbers)
2. Calculate - the % 
3. Design 

Aiming for 100% is not intelectually a righurous objective. 

- 2001 E. Brewer Lessons from Giant Scale Services
- 2009 L Barroso, U Holzle - The datacenter as a computer

- Now - we're trying to break the system to stop it breaking. 
- you have to measure something to be scientific about it 
- Can we iterate towards reliable architecture ? 

##### Measuring reliability
- reliability doesn't necessarily relate to business goals
- not everything that you measure makes sense
- make sure that you are improving based on the correct metrics 
- cut down measurements that don't matter

Things to do:
1. focus on the user
2. keep it simple
3. mean it - actually use it
4. be honest


##### Measuring UIs:
- application load
- navigation
- instant
- animation
- captive
- notification

Pareto FTW:
20% matter - 80% just extra stuff.

Thinking about availability in large service infrastructures. J Mogul, R Isaacs, B Welch - Google
Measure the system end to end. 

Does your business have a problem with availability?
Do you have a good idea of your users reliability ?
What should your signal -> collect -> aggregate pipeline look like ?
How would you net the biggest metric improvement ? 
What direct indicators of user harm you have and do they register on your metrics ? How would you make measuremets broader/truer ? 

### Ethics in tech - a psychological perspective on behaviour and organisations

- 75% of people conform to something that they are being told to do. Because we don't want to be different. 
- in ambiguous situations conformity increases
- be courageous and speak up
- Courage is persistence in the face of fear (Aristotle)
- Impression management - we like to be in charge how people see us. 
- Look for psychological safety. The shared belief that one will not be punished or humiliated for speaking up with ideas, questions, concerns or mistakes. The less psychological safe is, the more mistakes people do and less inovation happens.
- Number one spot that makes teams effective is psychological safety. 
"In google's fast-paced highly demanding environment our success hinges on the ability to take risks and be vulnerable in front of peers"
- High demand and no psychological safety = anxiety zone


psychological safety low and high demand company = anxiety zone
psychological safety low and low demand company = apathy zone
psychological safety high and low demand company = comfort zone
psychological safety high and high demand company = learning zone


### Event streaming as a source of truth
- check out formula 1 realtime event streaming 
- apply projection into a view using CQRS
- have the events cached
- anti-corruption layer
- create aggregate event

### Scaling CQRS in Theory, Practice and Reality

Microservices - seen as noun driven design.
CQRS - helps to achieve you the microservice architecture by enforcing services

### Communicating your architectural decisions

#### The illusion of communication
Phrases that are covering us, protecting us, trying to save us from later:
- I told them
- They were in the room
- It's on the wiki
- It was in an email
- It's in the code


Communication is a 2 way process. 

- Understanding difference between stakeholders and how to communicate with them
- learn conflict management and antipatterns

#### Selling: 
- we sell our solutions internally and externally
- help your clients (workmates, stakeholders) to succed in a way they feel good about it
- a good sales process starts in mind 
- a good sales person understands 
- a good sales person is about listening and understanding

Sometimes sales is being seen as doing something <b>to</b> people instead of <b>for</b> or <b>with</b> people.

Don't try to convince people to do the way YOU want but make sure they are part of the entire thought process.

#### Buying:
- percived value is worth the perceived cost

Why talk about tech ? All decisions are emotional. Reusability, clean code, security, etc. 

#### Developers as Stakeholders
- knowledege of existing implementation
- deeper hands on language/platform knowledge
- sounding board
- technical constraints

Everytime you communicate or do something make sure you're including the developers in the equation. Make sure they know everything they have to know and <b>WHY</b> you're building what you're building. What are the assumptions and the constrains. 

Explain what are the goals and time constraints, make sure htey understand the direction and they have <b>independence</b>. Eg "this is what we're doing in the next 3 months, this is the direction"
Motivation is the sense of autonomy. 

Friction: passive-aggressive resistance, ongoing skepticism. 

#### Project managers as stakeholders:
- they need to know how are we building this thing, in a broad sense. Not as technical jargon as talking with developers. Impact on time,scope and cost. 

Assure that the solution is meeting all the constraints we have and we're not making the incorrect assumptions. 

Friction: no time for meetings, armchair solutioning, lack of support

#### Client / Business
- What are we doing ? How are the short term and long term goals. What's the direction, are there any tradeoffs ? 
- If business are part of your daily process, they know when you don't meet the deadlines and they can understand the reasoning. 
They need to have confidence in the team, and the costs are justified. 

Friction - "I've heard that x is a great technology why don't we use that?", misalignment.

#### Shaping and communicating a solution:
1. research 
2. qualify
3. solve
4. present (close)

<b>Research</b> - understand what exactly we're solving and what's the problem the stakeholders are presenting.
- Listen to understand not to intrerrupt! 
- Find the actual problem statement. 
- Remember what's the real problem and don't microfocus. 
- The solution is valuable only if stakeholders understand that you're solving a real problem. 

<b> Qualify </b> 
- listen to people
- build trust by demonstrating listening skills and understanding of needs
- verify key assumptions and constraints before diving into the solution
- you own the understanding of what you've heard in a 2 way communication

<b>To make sure you understand use:</b> <i>"What i hear you saying is ..." , "Ok so my understanding is ...", "To summarize you want to do 3 things..."</i>

<b> Don't afraid to be wrong. </b>You're not being paid to be right, you're paid to solve problems. Admit that you made a mistake. If you show humility you're going to earn more confidence from your team. 

<b> Questions are a sign of strength </b> - a sign that you care to understand. 
Ask questions to disprove your theory. 
What's the probability of that happening ? How often that happens, etc ?

<b>Solve</b>
- knowing all the details make you have a very inflexible design. System are constantly changing and you can't know all the details upfront. Although make sure that the problem is well stated. 
<hr>
Make sure that you're stating a problem not a <b> USE </b> of technology. Eg
"We need multithreading"  better "We need to support more concurrent customers"
"We're not closing enough new business" 

Let the team dismiss or approve your solution. 
<i>"We need an architecture that enables offline tablet usage but can get content updates when wifi is available" </i>

Your architecture doesn't have to be just technical buzzwords. 
Solving is basically mapping from needs/goals to solution while honoring constraints. 

<b> Present </b>
- Start with the problem statement. <i> Here's what are we solving </i>
- Walk people into your solution
- Pave the way with understanding of needs
- Show how you're addressing constraints
- On board people as you go

Provide Solution Details tailored for your specific stakeholders. Continue to map values, needs, constraints. 
Be confident, and if you made your homework you shouldn't have problems. Listen, don't just talk. Communication is a process.
Make sure that the people understand that you have the best interest in mind. 

<hr>
Means of comunication:

<b>Storytelling</b>
- understand the conclusion of your story.
- provides cohesion, reasons to listen
- set people up to predict ending which can often garner support.

<b> Newspaper approach </b>
- builds a framework to absorb complex information

<b> Teaching method </b>
- first tell them what you're going to tell them 
- tell them
- then explain them what you told them
- always wrap up and make sure you outline the key things

#### Conflict:
- Conflict of idea (good)
- Conflict of people (bad)

1. Good team members will question what they don't understand and challenge assumptions.

2. Bad team members will not ask questions, will be comfortable. People will take the floor and talk about things that aren't important. 

<b>The detail</b>
- sometimes we have visibility to too many details and can make the honest mistake of giving equal weight to details
- don't prioritize minutiae at the expense of a good solution.
The conflict is (usually) not about the solution but about the problem we're trying to solve. 

Inquiry vs Advocacy:
- make sure that people are heard. Don't say <i>"I don have time to hear all of you" </i>
- engineers should speak as one voice with managers/stakeholders. This means you need to get to a consensus. Smaller the team the easier it is. 

<b>When dealing with conflict...</b>
- ask questions to guide rather than confront.
- depends regionally and culturally. Eg in NY it's very common to be agressive and don't have hard 
feelings about it. 

<hr>
Use the "5 whys" to get to the root of the problem.
Drill into something gradually by zooming in on the previous question.

We can learn something from anybody, if we're willing to do it. 

#### Communication antipatterns:
- I'm really busy
- As i've said before
- I told them
- That's just common sense
- Because I've said so

This ones are shutting down conversations and make people avoid conversating with you. 

#### Communication styles:
- Dominant/Direct
- Influence/Inspire
- Conscientious/Cautious
- Steady/Supportive

Some people are more people oriented others are more task oriented. Task oriented people seem to be direct and dominant, cautious and conscientious. [Disc model](
https://www.discprofile.com/what-is-disc/overview/)

<b> Dominant/Direct people </b>
- they don't like to flower things
- but they get upset when they are being told that they are wrong. 
- <i>"facts are facts"</i> but they are taking everything very personally 

<b> Task focused people: </b>
- can be controlling, micromanaging
- rejecting suggestions that aren't theirs
- appears impatient
- won't want to admit being wrong
- too deep in implementation details
- quick thinking - not taking all the details in consideration. 
- considers they have the flash of briliance 
- reactive thinking

<b> People focused people: </b>
- too vague
- not hands on enough
- moves on too soon
- can appear in over their head
- lets bad decision run rather than confront
- assumes good intentions are enough
- needs all information to make a decision
- disrupting status quo requires work

Becoming an effective architect
- provide decision and guidance to help dev teams make good choices NOT enforcing choices.
- ensure teams have everything they need to succeed.
- get feedback on your architecture, people are working on it.
- desplay emotional intelligence. Sometimes listening is what you need to do. 
- Don't assault other ideas. 
- walk back to assumptions, constraints and expected outcomes.
- Don't get sidetrack by "cool technology" or "new things" your goal is to solve problems.

#### Final thoughts:
- remove ambiguity
- words have meaning :-) communication antipattern 
- stating the obvious is not bad, because sometimes the obvious is not that obvious
- 