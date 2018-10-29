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
