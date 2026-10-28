# [Hackbots | DEF CON 34 | BBV Masterclass with Jason Haddix](https://youtu.be/cRKToFkZMvk?si=3roB0XRweI3Ye_x1)

## 00:04 Introduction and Overview

### 00:06 What is a Hackbot?

- Offensive security agents using LLMs or traditional ML
  
- Automation to scale offensive security tasks
  
- Offload just-in-time coding and expand testing capabilities
  
- Repeatability and methodology adherence in security testing
  
- Intuition aid for bug bounty hunters, focus on scale and automation
  
## 00:38 Hackbot Types and Focus

### 00:42 Dynamic Testing Focus

- Primarily web hacking and bug bounty context
  
- Different hackbots exist for other domains like hardware, source code, fuzzing
  
- Example output: Armada system's vulnerability report with critical to low findings
  
## 03:12 Agent Frameworks Introduction

### 03:20 Popular Frameworks

- Cloud Code, Codeex, Open Code as main agent harnesses
  
- Functions include spawning tasks, scheduling, CLI tool integration
  
- Emphasis on human-in-the-loop design to review and validate AI results
  
- Issues like false positives and chaining vulnerabilities need human oversight
  
- Challenges: agents may behave unpredictably or cause unwanted destructive actions
  
## 05:43 Preferred Agent Frameworks and Features

### 05:55 Details on Frameworks

- Cloud Code preferred; Codeex secondary; Open Code popular for local models
  
- Maestro framework for command chaining and task breakdown
  
- Agent framework architecture includes tools such as web fetch, shell access, APIs, sandboxing
  
- New features: loops, scheduling, goal prompting, autoskill generation
  
## 08:04 Building Skills in Agent Frameworks

### 08:16 Skills Defined in Markdown

- Skills standardized since 2025 with markdown files defining agent identity, instructions
  
- Low barrier for building agents: no Python programming needed, supports voice/typing input
  
- Skill components: name, description, arguments, model choice, context inheritance, supporting scripts & workflows
  
- Avoid "fable classifier" bans caused by cyber terminology in skill descriptions or context
  
## 11:11 Skill Engineering Approach

### 11:23 From High-Level Commands to Methodology

- "Bitter pill engineering": direct commands to AI work with top models but less effective for deep testing
  
- Preferred approach: domain knowledge embedded step-by-step methodology
  
- Example: JS Analyze skill for parsing JavaScript from websites, finding API endpoints and secrets
  
## 13:10 JS Analyze Skill Architecture

### 13:19 Key Design Requirements for JS Analyze

- Capture live and historical endpoints (including Wayback Machine sources)
  
- Parse all JS files and inline JS, including lazy-loaded scripts
  
- Detect source maps, secrets, outdated libraries, framework identification
  
- Overcome bot protections and anti-automation via specialized spidering tools (Interceptor)
  
- Output comprehensive reports with endpoints and curl commands
  
## 15:19 Deep JS Analysis Challenges

### 15:27 Handling Complex Scenarios

- Differentiate inline vs file-based JS
  
- Manage lazy-loaded scripts from user actions or authenticated sessions
  
- Crawl multiple domains for source maps
  
- Use interceptor to avoid bot detection and blocking
  
- Unobfuscate/minify code for better analysis
  
- Extract parameters, dangerous functions, and sensitive comments
  
## 17:32 Splitting Skills and Completion Bias

### 17:41 Modular Methodology

- Splitting large skills into smaller micro-skills (e.g., discover and download JS, then analyze)
  
- Combat AI's completion bias (skipping parts of long methodologies) by limiting task size
  
- Content discovery skill example: creating both generic and framework-specific brute force wordlists
  
- Use AI dictation/jamming techniques to build skills interactively (Andrej Karpathy style)
  
## 21:07 Vulnerability Specific Skills

### 21:15 Example: Cross-Site Scripting (XSS)

- Separate agents for reflected XSS, stored XSS, DOM XSS, blind XSS
  
- Enhances focus and completion on discrete vulnerabilities
  
- Gadget gathering as key secret sauce (requires full class training to learn)
  
## 21:33 Context and Harness Engineering Lessons

### 21:41 Model Access and Refusals

- Importance of joining trusted access programs (e.g. Anthropic CVP) to reduce refusals on offensive security tasks
  
- Engineering workarounds: document scope of work as artifacts, context overload techniques
  
- Exploit features like Cloud Code's /BBTW flag in models like Fable during limited-time access
  
## 23:40 Markdown Checklists and Review Skills

### 24:40 Ensuring Completion and Quality

- Use markdown checklists to track methodology steps and enforce completeness
  
- Review skill (e.g. built with Gemini model) checks missing steps and output artifacts
  
- Nudge prompts reinjected automatically to fix missing work based on review results
  
- Define success criteria via exemplar output directory structures
  
## 28:30 Prompting and Tool Syntax

### 28:44 Defining Explicit Tool Calls

- Avoid vague prompts for tool execution (e.g., specifying full HTTPX syntax for port scanning)
  
- Prevents lazy or incomplete tool usage by agents
  
## 29:21 Multiple Models, Multiple Runs

### 29:33 Ensemble Approach

- Use multiple models (Opus 4.6, 4.8, Chat GPT 5.6, Gemini, GLM, custom tuned) and run multiple times
  
- Non-deterministic LLM outputs require broad inference resources
  
- Use higher-level models for direct hacking commands and lower-level models for methodical vulnerability discovery
  
## 31:37 Output and File Management

### 31:39 Managing Output Location

- Never store output inside skill folders to avoid bloating and errors
  
- Always reference tools and output files with full absolute paths
  
- Prevents tool miss-identification and accidental task skipping
  
## 32:25 Retuning Skills for New Model Generations

### 32:34 Safe Mode Testing

- Run new models in safe mode (no identity or skill files) to benchmark innate abilities
  
- Remove redundant instructions from skill if model performs well unaided
  
- Keeps skills lean and efficient
  
## 33:25 New Features - Workflows

### 33:37 Classifier Challenges

- Workflows enable splitting methodologies across agents running in parallel
  
- However, tool call classifiers can aggressively block suspicious-looking workflow steps
  
- Silent failures common; users should inspect failed agents mid-run
  
## 34:05 Interceptor Tool for Browser Automation

### 34:23 Capturing Dynamic Web Traffic

- Interceptor browser extension drives full crawl of site with AI automation
  
- Executes all links and buttons, intercepts all requests
  
- Ported to Windows, added dash spider feature for thorough JS detection
  
- Replaces need for Burp, Kaido for AI-driven web crawling
  
## 35:15 War Stories and Special Cases

### 35:24 Example 1: Admin Password Reset Bug

- Two forgot password pages; AI missed second hidden admin password setter
  
- Human-in-the-loop identified it during live interception
  
- Resulted in discovered admin takeover vulnerability
  
- Inspired creation of standalone skill for login-related bugs and parameter brute forcing
  
### 37:49 Example 2: IDP Race Condition Testing

- Captured redirect timing to IDP providers (e.g. Octa)
  
- Built skill to stop redirects and analyze vulnerable API calls before authentication kicks in
  
- Led to discovery of serious data leak affecting major energy company
  
### 39:26 Example 3: SSRF Post-Exploitation Expansion

- Beyond classical SSRF AWS metadata focus, agent scanned localhost ports
  
- Found exposed Kubernetes Envoy admin panel with config dump access
  
- Allowed access to tenant API keys, escalating impact
  
- Led to SSRF skill split into identification and post-exploitation phases
  
## 42:12 Q&A Highlights

### 42:31 Skill-Based Review vs Model-Orchestrated Review

- No explicit benchmarks; Gemini chosen for critical vulnerability reviewing
  
- Multiple-model orchestration used to cover different strengths in workflows
  
- Lower level models used for easier tasks; high-level ones for vulnerability discovery
  
## Summary

### Hackbots combine modern agent harnesses and LLMs to automate offensive security testing

### Building effective hackbots requires domain knowledge, modular skills, robust prompting, and human-in-the-loop review

### Use multiple agent frameworks and ensemble model runs to overcome AI non-determinism and classifier challenges

### Tools like Interceptor and markdown checklists dramatically improve dynamic testing and workflow completion

### Continual retuning with new models essential to maintain bot effectiveness and efficiency

