# lib4ai_rules_skills

## INTENT
what does this repository have?

1. collection of pointers/ refernces for agents.md; skills; workflows
2. definition / description of what is what when using AI Code Assistants.
3. idea is as/when you start a new project, working with AI tools, 
  - SDLC with Agentic AI is different
  - how should you setup your machine/ environment
  - how should you structure your project
  - how should you plan your project
  - how should you design your project
  - which skill-set you must always have for your typical profile.
  - what are the commands, their sequence, and when to use them.
  - how to make yourself fast as well as productive and efficient.


## some definitions to clarify
* Project = a temporary, structured endeavor to create, maintain, or enhance a software product or system
* SDLC = Software Development Lifecycle
* Activity = a specific, actionable task within the SDLC that contributes to the creation, modification, or maintenance of a software product
* Task = a sufficiently defined, complete unit of work that delivers a specific, tangible change, typically designed to be accomplished by one person within one day
* Workflow = a structured, step-by-step methodology, or plan, used by teams to build, test, and deploy applications, often referred to as SDLC
* Skill = a technical or professional capability—ranging from programming languages to problem-solving—used to design, build, test, and maintain computer applications and systems
* Rules = set of explicit or understood regulations or principles governing conduct within a particular activity or group of activities
* Memory = the part of a computer in which data or program instructions can be stored for retrieval
* Constitution = a body of fundamental principles or established precedents according to which a software program/code is acknowledged to be governed


## SPECS, SDD, Specifications Driven Development
* there is no hard/ fast directions / guidelines on which workflows are best -- you can develop your own
* industry standard is missing; different companies have different techniques to address SDD
* SpecKit (https://github.com/github/spec-kit): a good starting point for using readily available workflows; 
  * workflow: **spec > constitution > specify  > clarify > plan > tasks > implement**
  * SpecKit runs as standalone tool; runs from CLI; 
  * SpecKit provides its templates to different AI Agents.
* RIPER-5 from Cursor (https://github.com/johnpeterman72/CursorRIPER); 
  * workflow: **research > innovate > plan > execute > review**
* Agent-Skills https://github.com/addyosmani/agent-skills
  * workflow: **spec > plan > build > test > review > ship**
* so what is a typical developer workflow ?
  * you start with specifications, 
  * clarify the specs and ideate on these specs, refine specs if possible, 
  * then create a plan for your project, 
  * then break down the plan into tasks, 
  * then have AI Agent implement the tasks; 
  * and finally verify/ validate the output of AI Agent;


## AGENTS, CONSTITUTION, RULES
* these are overarchiing rules that the AI Agent must follow
* these can be re-used across multiple projects
* We can have one AGENTS.md file for each type of Software Developer: Java, Python, Java-Springboot, React, etc.
* You can hand craft an AGENTS.md or even have AI-Agent generate it for you.
* AI Coding Agents like Windsurf/ Cascade refer to AGENTS.md as Constitution
* AI Coding Agents like Claude Code refer to AGENTS.md as CLAUDE.md
* scopes: Global (<user-home>/.claude/...), Project, Task


## SKILLS, WORKFLOWS
* Reference points to begin with
  * https://agentskills.io/home
  * https://skills.sh
  * https://skillzwave.ai/browse/development/
* A Skill relates to a specific task that the AI Agent must perform as a software developer.
* like any other tool -- **RTFM: please read the docs to understand how to use each skill.**
* Claude specific
  * https://claude.com/plugins
  * https://claudemarketplaces.com/skills
  * https://github.com/addyosmani/agent-skills
  * https://github.com/JuliusBrussee/caveman
* AI Coding Agents like Windsurf/ Cascade refer to Skills as Workflows.
* install Skills under different scopes: Global (<user-home>/.claude/skills/...), Project




