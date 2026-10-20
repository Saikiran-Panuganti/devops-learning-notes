# devops-learning-notes

**Learn, revise, and build a practical DevOps knowledge base.**

This repository is a personal, course-wise textbook for DevOps concepts and tools. It brings together concise explanations, commands, configuration syntax, practical examples, common pitfalls, and interview questions in one place.

> **Status:** The repository is being built out. The topic map below describes the intended organization; a topic folder or note may not exist until it has been added.

## How to use these notes

1. Choose a topic from the learning map.
2. Start with the fundamentals, then work through the examples and exercises.
3. Run commands in a suitable lab or test environment and adapt them to your system.
4. Use the revision points and interview questions to check your understanding.
5. Add useful discoveries and corrections back to the relevant topic.

The notes are designed for learning and revision. They are not a substitute for official documentation, and commands that change infrastructure should be reviewed before use.

## Learning map

| Area | Topics | What to learn |
| --- | --- | --- |
| Foundations | Linux, Shell Scripting, Git & GitHub | Operating-system basics, command-line workflows, automation, version control, and collaboration |
| Cloud and infrastructure | AWS, Terraform | Cloud fundamentals, infrastructure as code, state, reusable configurations, and safe changes |
| Containers and orchestration | Docker, Kubernetes | Images, containers, networking, storage, workloads, services, configuration, and troubleshooting |
| Continuous delivery and GitOps | Jenkins, Argo CD & Helm | Pipelines, deployment strategies, chart-based releases, and Git-driven operations |
| Observability | Prometheus & Grafana | Metrics, scraping, queries, dashboards, and alerting fundamentals |

### Planned topic layout

```text
devops-learning-notes/
├── shell-scripting/
│   ├── 01-variables.md
│   ├── 02-conditions.md
│   ├── 03-loops.md
│   ├── 04-functions.md
│   ├── 05-arrays.md
│   ├── scripts/
│   └── README.md
├── linux/
├── git-github/
├── aws/
├── terraform/
├── docker/
├── kubernetes/
├── jenkins/
├── argocd-helm/
└── Observability/
etc......
```

Each topic is organized into focused Markdown notes. The Shell Scripting tree shows one example of how a topic can be broken into lessons and practical scripts.

## What each topic covers

- **Shell Scripting:** variables, quoting, input and output, conditions, loops, functions, arrays, exit codes, and reusable scripts.
- **Linux:** files and permissions, processes, users, packages, services, storage, logs, and essential commands.
- **Git & GitHub:** repositories, commits, branches, merging, remotes, pull requests, and everyday collaboration workflows.
- **AWS:** core cloud concepts and commonly used services, identity and access basics, networking, compute, storage, and operational practices.
- **Terraform:** providers, resources, variables, outputs, modules, state, planning, and safe infrastructure changes.
- **Docker:** images, containers, Dockerfiles, volumes, networks, registries, and Compose.
- **Kubernetes:** cluster concepts, Pods, Deployments, Services, configuration, storage, scaling, and troubleshooting.
- **Jenkins:** pipelines, Jenkinsfiles, agents, credentials, build stages, and delivery workflows.
- **Argo CD & Helm:** charts, values, releases, declarative application delivery, and GitOps workflows.
- **Prometheus & Grafana:** metrics, exporters, PromQL fundamentals, dashboards, and alert rules.

## Suggested format for a note

Keep each note focused on one concept or task. Where relevant, use this outline:

1. **Purpose:** What problem does this concept or tool solve?
2. **Core concepts:** Explain the key terms in plain language.
3. **Syntax and commands:** Include short, copyable examples and explain important options.
4. **Practical example:** Show a realistic use case and its expected result.
5. **Common mistakes:** Record pitfalls, troubleshooting hints, and safe practices.
6. **Interview questions:** Add questions with concise answers for revision.
7. **References:** Link to official documentation and other useful sources.

## Learning principles

- Prefer small, runnable examples over long, unexplained command lists.
- Explain what a command changes, its expected output, and any prerequisites.
- Use placeholders for account IDs, credentials, domains, and other environment-specific values.
- Never add real credentials, tokens, private keys, or sensitive infrastructure details to notes.
- Distinguish learning examples from production-ready configurations.
- Keep notes accurate and update examples when tools or command behavior changes.

## Related repositories

- [devops-hands-on-labs](../devops-hands-on-labs/README.md) — practice-oriented labs.
- [devops-real-world-projects](../devops-real-world-projects/README.md) — end-to-end project work.
- [devops-troubleshooting-guides](../devops-troubleshooting-guides/README.md) — symptom-led troubleshooting references.

These repositories complement the notes: learn the concepts here, apply them in labs and projects, and use troubleshooting guides when diagnosing issues.
