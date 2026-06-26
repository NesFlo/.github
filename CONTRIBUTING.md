# Contributing to NesFlo

First and foremost, thank you for your interest in contributing to **NesFlo**.

Whether you're reporting a bug, suggesting an improvement, designing user interfaces, improving documentation, reviewing code, or building new features, your contributions help shape the future of the platform.

NesFlo is more than a software project—it's an effort to redefine how organizations transform operational communication into structured, automated business workflows. We believe that meaningful software is built through collaboration, diverse perspectives, and a shared commitment to engineering excellence.

We welcome contributors of all experience levels. If you're passionate about workflow automation, enterprise software, artificial intelligence, developer tools, or open-source collaboration, there's a place for you in the NesFlo community.

---

# Project Status

> **Current Phase:** Research & Validation

NesFlo is currently in the **Research & Validation** phase.

At this stage, we're focused on understanding real-world operational challenges, validating assumptions, refining the product vision, and designing a scalable architecture capable of supporting enterprise-grade workflow automation.

While production development has not yet begun, this phase is one of the most important in the project's lifecycle. Decisions made now will influence the platform's architecture, extensibility, developer experience, and long-term maintainability.

### Current areas of focus

- Product research and validation
- System architecture and design
- Workflow modelling
- User experience research
- API design
- Integration strategies
- Documentation
- Engineering standards
- Branding and developer experience

As the project progresses, this document will evolve alongside the platform.

---

# Our Engineering Philosophy

NesFlo is built around a few core engineering principles.

## Build for Real Problems

Every feature should solve a genuine operational challenge. We prioritize practical solutions over unnecessary complexity.

## Simplicity Over Complexity

Simple systems are easier to understand, maintain, test, and scale. Whenever multiple solutions exist, we generally prefer the simplest one that satisfies the requirements.

## Documentation is a Feature

Well-written documentation is as valuable as production code. Every significant architectural decision should be documented and understandable by future contributors.

## Developer Experience Matters

Good tooling, clear documentation, consistent code style, and predictable workflows enable contributors to focus on solving problems instead of navigating unnecessary complexity.

## Quality Over Quantity

We value thoughtful, well-designed contributions over rapid feature development. Taking the time to design and review changes carefully leads to a healthier project over the long term.

---

# Ways You Can Contribute

There are many ways to contribute to NesFlo beyond writing code.

## Product Research

Help validate ideas by identifying real-world business workflows, operational pain points, and automation opportunities.

## Documentation

Improve documentation, architecture guides, onboarding material, diagrams, tutorials, examples, and technical references.

## Backend Engineering

Contribute to APIs, workflow orchestration, integrations, automation engines, data processing pipelines, and platform services.

## Frontend Engineering

Help build intuitive and accessible web interfaces that simplify complex business workflows.

## Mobile Development

Contribute to the Flutter application, focusing on cross-platform experiences for Android, iOS, desktop, and future platforms.

## UI/UX Design

Design intuitive user experiences, dashboards, workflow builders, design systems, icons, illustrations, and branding assets.

## DevOps & Infrastructure

Improve deployment pipelines, containerization, CI/CD, monitoring, observability, cloud infrastructure, and development tooling.

## Testing & Quality Assurance

Help improve platform reliability through automated testing, integration testing, performance testing, and quality assurance practices.

## Artificial Intelligence

Research and develop intelligent workflow suggestions, document understanding, message parsing, summarization, anomaly detection, and operational insights.

## Community

Help answer questions, participate in discussions, review pull requests, improve onboarding, and create a welcoming environment for new contributors.

---

# Before You Start

Before contributing, we encourage you to:

- Read the project documentation.
- Review existing issues and discussions.
- Search for duplicate feature requests or bug reports.
- Discuss significant architectural changes before implementation.
- Follow the project's coding standards and contribution guidelines.

Early collaboration helps prevent duplicated effort and leads to better technical decisions.

---

# Development Environment

NesFlo follows a modular, API-first architecture designed for scalability, maintainability, and long-term growth. Before contributing, ensure your local development environment is properly configured.

## Recommended Tools

The following tools are recommended for all contributors.

### General

- Git
- Docker Desktop
- Visual Studio Code (or your preferred IDE)

### Backend

- Python 3.12+
- FastAPI
- uv (preferred) or pip
- PostgreSQL
- Redis

### Frontend

- Node.js (LTS)
- pnpm (preferred)
- Next.js
- TypeScript

### Mobile

- Flutter (Stable)
- Dart SDK
- Android Studio / Xcode (where applicable)

### Database

- PostgreSQL
- Supabase (Development)

---

# Repository Structure

The NesFlo organization is organized into independent repositories, each with a clear responsibility.

```text
nesflo/

.github/
docs/
branding/

backend/
frontend/
mobile/

website/

sdk-python/
sdk-javascript/
sdk-flutter/

cli/
examples/
```

Each repository contains its own documentation, dependencies, and development instructions.

Contributors should only make changes within repositories relevant to their work unless a coordinated cross-repository change has been discussed.

---

# Development Workflow

We follow a feature-branch workflow.

Never develop directly on the `main` branch.

The typical workflow is:

1. Fork the repository (if required).
2. Create a new branch.
3. Implement your changes.
4. Test your changes.
5. Update documentation where necessary.
6. Submit a Pull Request.

---

# Branch Naming Convention

Use descriptive branch names.

Preferred format:

```text
feature/short-description
fix/short-description
docs/short-description
refactor/short-description
test/short-description
ci/short-description
chore/short-description
```

Examples:

```text
feature/workflow-parser
feature/mobile-authentication

fix/email-template-validation

docs/update-api-reference

refactor/report-engine

test/parser-unit-tests

ci/github-actions

chore/dependency-updates
```

Avoid branch names like:

```text
new
testing
branch1
fixes
random
```

Branch names should clearly communicate their purpose.

---

# Commit Message Convention

NesFlo follows the **Conventional Commits Specification**.

Format:

```text
<type>: <description>
```

Common commit types include:

```text
feat
fix
docs
style
refactor
perf
test
build
ci
chore
revert
```

Examples:

```text
feat: implement workflow parsing engine

fix: resolve duplicate webhook processing

docs: update architecture documentation

refactor: simplify message parser

test: add API integration tests

ci: improve GitHub Actions pipeline

chore: update project dependencies
```

Keep commit messages:

- concise
- descriptive
- written in the imperative mood

Good:

```text
feat: add Supabase authentication
```

Poor:

```text
updated stuff

fixed bug

changes

working now
```

---

# Keeping Changes Focused

Every Pull Request should solve **one logical problem**.

Instead of combining multiple unrelated changes:

❌

- Authentication
- Dashboard redesign
- Documentation updates
- Database migration

Prefer:

✅

One PR = One feature

Examples:

- Add authentication middleware
- Improve workflow editor
- Update deployment documentation

Focused Pull Requests are easier to review, test, and maintain.

---

# Synchronizing with the Main Branch

Before opening a Pull Request:

- Pull the latest changes from `main`
- Resolve merge conflicts locally
- Ensure your branch is up to date
- Re-run tests after rebasing or merging

Keeping your branch synchronized reduces integration issues and simplifies code review.

---

# Pull Request Guidelines

Thank you for taking the time to contribute to NesFlo.

Every Pull Request (PR) should represent a well-defined, tested, and documented improvement to the project. Our review process focuses not only on whether code works, but also on maintainability, readability, scalability, and alignment with the project's architecture.

## Before Opening a Pull Request

Please ensure that:

- Your branch is up to date with the latest `main` branch.
- Your changes solve a single logical problem.
- Your code follows the project's coding standards.
- All relevant tests pass.
- Documentation has been updated where applicable.
- There are no unnecessary files or commits.

Before submitting, ask yourself:

> Would another contributor understand this change six months from now?

If the answer is "no," consider improving your implementation or documentation.

---

# Pull Request Checklist

Before requesting a review, verify the following:

- [ ] My code follows the project's coding standards.
- [ ] I have tested my changes.
- [ ] Existing tests continue to pass.
- [ ] I updated documentation where necessary.
- [ ] My Pull Request addresses a single concern.
- [ ] My commit history is clean.
- [ ] My branch is based on the latest `main`.

---

# Code Review Process

Every Pull Request is reviewed for:

## Correctness

Does the implementation solve the intended problem?

## Readability

Can another engineer easily understand the code?

## Maintainability

Will this be easy to maintain as the project grows?

## Performance

Does the implementation introduce unnecessary complexity or resource usage?

## Security

Does the change introduce potential vulnerabilities?

## Consistency

Does the implementation follow existing project conventions?

Reviews are collaborative discussions, not personal criticism. Feedback should always remain constructive and respectful.

---

# Coding Standards

We value clean, readable, and maintainable code over clever or overly complex implementations.

## General Principles

Write code that is:

- Simple
- Predictable
- Testable
- Modular
- Reusable
- Well documented

Avoid unnecessary abstraction or premature optimization.

---

## Naming

Use meaningful names.

Good:

```text
workflowParser
reportGenerator
fuelRequestService
```

Avoid:

```text
temp
test
abc
data1
newObject
```

Names should clearly communicate purpose.

---

## Functions

Functions should perform one responsibility.

Prefer:

- Small functions
- Clear parameters
- Minimal side effects

Avoid functions that perform multiple unrelated operations.

---

## Comments

Comments should explain **why**, not **what**.

Good:

```text
// Retry because upstream services may temporarily reject requests.
```

Avoid:

```text
// Increment i
i++
```

If code requires extensive comments to explain what it does, consider simplifying the implementation.

---

## Error Handling

Handle errors explicitly.

Provide meaningful error messages.

Never silently ignore failures.

Prefer graceful recovery over unexpected crashes whenever appropriate.

---

# Documentation Standards

Documentation is considered part of the product.

Contributors are encouraged to document:

- New features
- Public APIs
- Configuration options
- Architectural decisions
- Breaking changes

Whenever practical, documentation should accompany the same Pull Request as the implementation.

---

# Testing

Reliable software requires reliable testing.

Contributors should include appropriate tests for new functionality whenever possible.

Testing may include:

- Unit Tests
- Integration Tests
- End-to-End Tests
- API Tests
- Performance Tests

Bug fixes should include regression tests whenever practical to prevent future reoccurrence.

---

# Code Quality

Before submitting code, ask yourself:

- Is this the simplest solution?
- Is the code readable?
- Can another contributor maintain this?
- Does it introduce unnecessary complexity?
- Is it documented?
- Is it tested?

If improvements can still be made, consider refining the implementation before opening a Pull Request.

---

# Breaking Changes

Breaking changes should be discussed before implementation.

When introducing a breaking change:

- Explain the motivation.
- Describe affected components.
- Provide migration guidance.
- Update relevant documentation.

Large architectural changes should begin as a discussion or proposal before development starts.

---

# Reporting Issues

If you've discovered a bug, we'd love to hear about it.

Before opening a new issue, please:

- Search existing issues to avoid duplicates.
- Ensure the issue hasn't already been reported.
- Gather enough information to reproduce the problem.

When reporting a bug, please include:

- A clear and descriptive title.
- Steps to reproduce the issue.
- Expected behavior.
- Actual behavior.
- Screenshots or recordings (if applicable).
- Environment information (Operating System, Browser, Device, etc.).
- Relevant logs or error messages.

The more information you provide, the easier it is for maintainers to investigate and resolve the issue.

---

# Feature Requests

Great products evolve through great ideas.

If you'd like to propose a new feature:

- Clearly describe the problem you're trying to solve.
- Explain why the feature would be valuable.
- Suggest a possible solution (optional).
- Consider alternative approaches.

Feature requests should focus on solving real-world problems rather than introducing unnecessary complexity.

Remember:

> Every feature adds long-term maintenance cost.

Our goal is to build a focused, scalable, and maintainable platform.

---

# Discussions

Not every idea belongs in an Issue.

Use GitHub Discussions for:

- Questions
- Brainstorming
- Product ideas
- Architecture conversations
- Design feedback
- Community discussions
- Workflow proposals

Issues should represent actionable work.

Discussions are for collaborative thinking.

---

# Request for Comments (RFC)

Significant features should begin as an RFC before implementation.

Examples include:

- New platform modules
- Major integrations
- Breaking API changes
- Workflow engine enhancements
- Authentication changes
- Database architecture
- Large UI redesigns

A typical RFC should include:

## Summary

Brief overview of the proposal.

## Motivation

Why is this needed?

## Proposed Solution

Describe the implementation.

## Alternatives Considered

Explain why other approaches were not chosen.

## Drawbacks

Identify potential disadvantages or trade-offs.

## Open Questions

Highlight areas requiring further discussion.

RFCs allow contributors to collaborate before development begins, reducing wasted effort and encouraging better technical decisions.

---

# Architecture Decision Records (ADRs)

Major engineering decisions should be documented as Architecture Decision Records (ADRs).

Examples include:

- Choosing FastAPI over another backend framework.
- Selecting PostgreSQL as the primary database.
- Introducing a new workflow engine.
- Changing deployment architecture.
- Adopting a messaging broker.

Each ADR should document:

- Context
- Decision
- Alternatives
- Consequences

This helps future contributors understand not only *what* decisions were made, but also *why* they were made.

---

# Release Process

NesFlo follows a structured release process to maintain stability and predictability.

General release stages include:

1. Development
2. Internal Testing
3. Quality Assurance
4. Release Candidate
5. Production Release

Every release should include:

- Updated documentation
- Release notes
- Version tagging
- Migration guidance (if required)

Breaking changes must be clearly documented.

---

# Semantic Versioning

NesFlo follows Semantic Versioning (SemVer):

```
MAJOR.MINOR.PATCH
```

Example:

```
2.4.1
```

Where:

- **MAJOR** — Breaking changes
- **MINOR** — New backward-compatible features
- **PATCH** — Bug fixes and maintenance updates

This versioning strategy provides predictable upgrades for developers and users.

---

# Project Roadmap

The long-term direction of NesFlo is documented in the project's roadmap.

Contributors are encouraged to review the roadmap before proposing large features to ensure alignment with the project's vision and priorities.

While we welcome new ideas, not every feature request will align with the current roadmap.

---

# Decision-Making

Engineering decisions are guided by the following principles:

- Solve real-world problems.
- Prioritize maintainability.
- Prefer simplicity over unnecessary complexity.
- Optimize for long-term scalability.
- Maintain a consistent developer experience.
- Preserve backward compatibility whenever practical.

Every contribution should strengthen the platform without compromising its long-term vision.

---

# Communication

Healthy communication is essential to building great software.

We encourage contributors to:

- Ask questions when unsure.
- Share ideas openly and respectfully.
- Provide constructive feedback.
- Be open to learning and mentorship.
- Respect differing technical opinions.

Remember that every contributor brings unique experiences and perspectives that strengthen the project.

---

# Community Expectations

As a member of the NesFlo community, you agree to:

- Be respectful and professional.
- Follow the project's Code of Conduct.
- Welcome newcomers.
- Encourage constructive discussions.
- Focus on solving problems collaboratively.
- Respect maintainers' decisions.
- Help maintain a positive and inclusive environment.

Open source is built on collaboration, trust, and mutual respect.

---

# Recognition

Every contribution matters.

Whether you've:

- Fixed a bug
- Improved documentation
- Suggested a feature
- Reviewed code
- Reported an issue
- Designed an interface
- Improved accessibility
- Shared feedback
- Answered community questions

you have helped move NesFlo forward.

We sincerely appreciate every contribution, regardless of size.

---

# Becoming a Maintainer

As the project grows, contributors who consistently demonstrate technical excellence, collaboration, and alignment with the project's vision may be invited to become maintainers.

Maintainers are expected to:

- Review Pull Requests
- Guide technical discussions
- Help shape the project's architecture
- Mentor contributors
- Uphold community standards
- Help maintain project quality

Maintainer status is earned through consistent contribution and community involvement.

---

# Contributor License

By submitting a contribution to NesFlo, you agree that your contribution may be incorporated into the project under its applicable license.

You confirm that:

- You have the right to submit the contribution.
- Your contribution is your own original work or you have the necessary rights to contribute it.
- You understand that contributions may become part of the project's public history.

---

# Security

If you discover a security vulnerability, **please do not disclose it publicly**.

Instead, follow the instructions in the project's **SECURITY.md** document so the issue can be investigated and resolved responsibly before public disclosure.

Responsible disclosure helps protect both the project and its users.

---

# Questions?

If you have any questions about contributing, feel free to:

- Open a GitHub Discussion.
- Start a conversation in the appropriate community channel.
- Contact the maintainers.

We're always happy to help new contributors get started.

---

# Thank You

Thank you for taking the time to contribute to **NesFlo**.

NesFlo began with a simple vision:

> Transform operational conversations into intelligent workflows.

Every contribution—whether it's code, documentation, design, research, testing, or simply sharing ideas—helps bring that vision closer to reality.

We're excited to build the future of workflow intelligence together.

---

<div align="center">

### **NesFlo**

**Turning Conversations Into Workflows.**

Made with love by contributors around the world.

</div>

