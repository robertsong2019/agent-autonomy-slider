# Agent Autonomy Slider 🎚️🤖

An interactive demonstration of autonomy levels in AI agent systems, inspired by [Cursor](https://cursor.com/) and the concept of "autonomy slider" in LLM applications.

## 🎯 What is an Autonomy Slider?

The **autonomy slider** is a concept popularized by Andrej Karpathy and implemented in tools like Cursor:

> "The best LLM applications have an autonomy slider: you control how much independence to give the AI. In Cursor, you can do Tab completion, Cmd+K for targeted edits, or you can let it rip with the full autonomy agentic version."
> — Andrej Karpathy, CEO of Eureka Labs

This project visualizes and explains the different levels of AI agent autonomy, helping developers understand how to design human-AI collaboration systems.

## 🌟 Features

- **Interactive Slider**: Adjust autonomy levels and see how agent behavior changes
- **5 Autonomy Levels**: From manual to fully autonomous
- **Visual Comparison**: Side-by-side comparison of different approaches
- **Real-world Examples**: Examples from Cursor, gstack, ClawTeam, and other systems
- **Educational Content**: Clear explanations of each level's pros and cons

## 🚀 Quick Start

```bash
# Clone the repository
git clone https://github.com/robertsong2019/agent-autonomy-slider.git
cd agent-autonomy-slider

# Open in browser
open index.html
```

## 📊 Autonomy Levels

### Level 1: Manual (Human-in-Control) 👤
- **AI Role**: Passive assistant, responds to direct commands only
- **Example**: Traditional code completion (IntelliSense)
- **Pros**: Full control, predictable, safe
- **Cons**: Low efficiency, high human workload

### Level 2: Assisted (AI Suggestions) 🤝
- **AI Role**: Suggests options, human makes all decisions
- **Example**: GitHub Copilot, Cursor Tab completion
- **Pros**: Human oversight, good balance
- **Cons**: Still requires constant attention

### Level 3: Supervised (AI Executes, Human Reviews) 👀
- **AI Role**: Executes tasks, human reviews and approves
- **Example**: Cursor Cmd+K, Claude Code targeted edits
- **Pros**: Faster execution, quality control
- **Cons**: Can create bottlenecks if review is slow

### Level 4: Semi-Autonomous (AI Leads, Human Oversees) 🎯
- **AI Role**: Leads execution, human oversees and intervenes
- **Example**: Cursor Agent mode, gstack workflow
- **Pros**: High efficiency, strategic human input
- **Cons**: Requires trust in AI system

### Level 5: Fully Autonomous (AI Owns End-to-End) 🚀
- **AI Role**: Complete ownership from start to finish
- **Example**: ClawTeam (one command → full automation)
- **Pros**: Maximum efficiency, minimal human involvement
- **Cons**: Risk of unexpected behavior, hard to debug

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                 Autonomy Spectrum                        │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  Level 1       Level 2       Level 3       Level 4    Level 5
│  Manual        Assisted      Supervised    Semi-Auto  Autonomous
│    👤            🤝            👀            🎯          🚀
│                                                         │
│  ├─────────────┼─────────────┼─────────────┼───────────┤
│  Human: 100%   Human: 80%    Human: 50%    Human: 20%  Human: 5%
│  AI:    0%     AI:    20%    AI:    50%    AI:    80%  AI:    95%
│                                                         │
└─────────────────────────────────────────────────────────┘
```

## 🎨 Design Principles

1. **Progressive Enhancement**: Start manual, increase autonomy gradually
2. **Human-in-Loop**: Always maintain human oversight capability
3. **Graceful Degradation**: System works even at lower autonomy levels
4. **Transparency**: Clear visibility into AI decision-making
5. **Reversibility**: Ability to step back to lower autonomy

## 💡 Use Cases

### When to Use Each Level

| Level | Use Case | Example |
|-------|----------|---------|
| 1 | Critical systems, learning phase | Production deployments, teaching |
| 2 | Creative work, exploration | Design prototyping, research |
| 3 | Production development | Feature implementation, refactoring |
| 4 | Experienced teams, trusted systems | Rapid development, startups |
| 5 | Experimentation, trusted environments | Prototyping, research projects |

## 🔬 Technical Implementation

- **Pure HTML/CSS/JavaScript**: No dependencies required
- **Responsive Design**: Works on desktop and mobile
- **Accessible**: WCAG 2.1 compliant
- **Lightweight**: < 50KB total size

## 📚 References

- [Cursor](https://cursor.com/) - AI-powered code editor
- [gstack](https://github.com/garrytan/gstack) - Garry Tan's Claude Code workflow
- [ClawTeam](https://github.com/HKUDS/ClawTeam) - Agent swarm intelligence
- [Andrej Karpathy on Autonomy Slider](https://cursor.com/) - Concept origin

## 🤝 Contributing

Contributions welcome! This is an educational project to help developers understand AI agent autonomy.

## 📄 License

MIT

## 👤 Author

Created by 首尔虾 🇰🇷🤖 as part of autonomous AI agent exploration.

---

**Key Insight**: The best AI systems don't force a single autonomy level - they provide a slider that users can adjust based on context, trust, and task complexity. This project helps you understand where to set the dial.
