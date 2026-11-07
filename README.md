# Roadmap Progress Cheatsheets

This repository contains my personal progress cheatsheets for a 24-month dual-track roadmap:

- **Path A — Red Team / Offensive Security**
- **Path B — AI Red Team / AI Security**

The goal is to build practical skills through structured learning, hands-on labs, projects, documentation, and continuous review.

## Current progress

I am currently in **Month 3** of the roadmap.

My current focus is:

- **Path A:** Windows internals, Active Directory basics, PowerShell, and Windows enumeration.
- **Path B:** HTTP, REST APIs, JSON, API authentication, rate limiting, and AI API testing.

I am also beginning light CTF practice with picoCTF.

## Repository structure

```text
roadmap-stages/
├── Stage01-Linux-Basics-and-Python-for-AI/
│   ├── pathA/
│   │   ├── 01-linux-command-line/
│   │   │   └── cheatsheet.md
│   │   └── ...
│   └── pathB/
│       ├── 01-python-fundamentals/
│       │   └── cheatsheet.md
│       └── ...
├── Stage02-Python-for-Security-and-Data-Science/
├── Stage03-Windows-Internals-and-API-Fundamentals/
├── ...
└── Stage24-Capstone-AI-Red-Team-Operation/
```

## Folder meaning

| Folder | Purpose |
|---|---|
| `pathA` | Red team, offensive security, networking, web security, Active Directory, privilege escalation, cloud, phishing, malware, CTF, and red-team operations |
| `pathB` | AI security, machine learning, transformers, MLOps, adversarial ML, model attacks, LLM security, and AI infrastructure |
| `cheatsheet.md` | My personal notes, commands, tools, mistakes, fixes, and progress for one specific topic |
| `README.md` | Short overview of the stage or path |

## How I use this repository

1. Open the current stage folder.
2. Choose either `pathA` or `pathB`.
3. Open the topic folder I am studying.
4. Fill in `cheatsheet.md` with:
   - Key concepts
   - Commands and code
   - Labs and practice notes
   - Errors and solutions
   - Project progress
   - What I can explain from memory
5. Commit regularly so my progress is visible and version-controlled.

## Current stage: Month 3

### Path A — Red Team

Topics I am working through:

- Windows processes
- Windows services
- Windows registry
- Windows event logs
- PowerShell basics
- Active Directory structure
- Windows enumeration scripting

Project:

- Build a Windows enumeration script that collects system information, users, groups, services, scheduled tasks, network connections, and running processes into a timestamped log.

### Path B — AI Red Team

Topics I am working through:

- HTTP methods
- REST API principles
- JSON
- API authentication
- API keys and OAuth basics
- Rate limiting
- AI API testing

Project:

- Build an AI API tester that checks rate limits, error handling, input validation, and endpoint behavior for AI APIs.

## Learning rules

- No calendar pressure: months are stages, not strict deadlines.
- Understanding matters more than completion.
- A project is finished only when I can rebuild and explain it from memory.
- Learn the concept first, build a basic version, then improve it step by step.
- Search narrowly only after attempting the problem myself.
- Document commands, errors, fixes, and lessons while working.
- Verify every tool, repository, Docker image, and GitHub link before using it.
- Only test systems I own or have explicit written permission to test.

## Progress tracking

I will update each cheatsheet as I learn.

For every topic, I aim to reach this level:

- [ ] Understand the core concept
- [ ] Complete practical exercises
- [ ] Build or complete the related project
- [ ] Document commands, errors, and fixes
- [ ] Explain the topic without notes
- [ ] Add useful artifacts to GitHub

## Commit style

I will use clear commit messages such as:

```text
docs: add Windows processes cheatsheet
progress: complete PowerShell basics checklist
project: start Windows enumeration script
fix: document API rate-limit error
review: update Month 3 progress
```

## Security notice

This repository is for learning and authorized security testing only.

I will not test, attack, scan, exploit, or access any system, website, API, model, or network without explicit permission. All labs and projects are performed in isolated, controlled environments.
