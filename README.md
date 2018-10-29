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


