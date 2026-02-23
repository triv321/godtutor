# GodTutor

**A structured prompt system that turns any LLM into a brutal, no-handholding technical mentor.**

Most people use LLMs as answer machines. Copy question, paste answer, learn nothing. GodTeacher flips that model entirely -- it forces the LLM to act as a tough mentor who makes you *think*, *struggle*, and *build* your way to real mastery.

---

## What This Is

GodTeacher is a collection of interconnected `.md` files that act as system-level instructions for any LLM (ChatGPT, Claude, Gemini, etc.). When loaded into a conversation, they transform the LLM from a helpful assistant into a demanding technical coach that:

- **Never gives you code solutions** -- only architecture, hints, and questions
- **Forces you to break down problems yourself** before offering guidance
- **Assigns production-grade projects** that can't be solved by copying from tutorials
- **Tests your knowledge regularly** through teach-back sessions and memory rebuilds
- **Tracks your progress** and identifies skill decay before it becomes a problem

This is not a course. There is no curriculum to follow passively. It is a *system* that adapts to what you're learning and makes sure you actually retain it.

---

## Why This Exists

Learning from LLMs has a fatal flaw: it's too easy to get answers without understanding them. You ask "how do I implement JWT auth?", the LLM writes the code, you paste it, it works, and you've learned nothing. Two weeks later you can't do it from scratch.

GodTeacher solves this by enforcing rules that prevent the LLM from doing the work for you:

- Answers must be earned through struggle
- Concepts must be immediately applied, not just consumed
- Every skill is verified through recall, not recognition
- Rust (skill decay) is actively detected and repaired

---

## The System Architecture

The system is made of 6 files, each with a specific role:

```
GodTeacher/
|
|-- master_orchestrator.md    # The brain. Load this first. Always keep in context.
|-- learning_engine.md        # 5-phase teaching methodology (Foundation -> Teaching)
|-- project_generator.md      # Production-grade project templates + generation rules
|-- anti_handholding_guard.md # Rules that prevent the LLM from giving easy answers
|-- mastery_verification.md   # Testing protocols (teach-back, rebuilds, mock interviews)
|-- revision_engine.md        # Surgical repair system for skills you've forgotten
```

### How They Connect

```
                    master_orchestrator.md
                    (always loaded, central brain)
                           |
          +----------------+----------------+
          |                |                |
   learning_engine.md   project_generator.md   revision_engine.md
   (teaching phases)    (project assignments)   (skill repair)
          |                |                |
          +----------------+----------------+
                           |
              anti_handholding_guard.md
              (behavior enforcement, always active)
                           |
              mastery_verification.md
              (triggered at intervals)
```

---

## How to Use

### Step 1: Clone the Repository

```bash
git clone https://github.com/<your-username>/GodTeacher.git
```

### Step 2: Open Your Preferred LLM

This works with any LLM that supports long context or file uploads:
- **ChatGPT** (GPT-4 / GPT-4o) -- paste files or upload them
- **Claude** (Sonnet / Opus) -- paste files or use Projects
- **Gemini** -- paste files into context
- **Any local model** (with sufficient context window)

### Step 3: Load the Files

**Option A: Load everything at once (recommended for models with large context)**

Paste all 6 files into the conversation. Start with `master_orchestrator.md` and tell the LLM:

> "Read all the attached files. You are now operating under the GodTeacher system. Follow the master_orchestrator.md as your primary directive. Begin by presenting the Learning Mode Selector."

**Option B: Progressive loading (for smaller context windows)**

1. Paste `master_orchestrator.md` and `anti_handholding_guard.md` first (these must always be in context)
2. The orchestrator will tell the LLM when to reference other files
3. Paste `learning_engine.md` when starting a learning phase
4. Paste `project_generator.md` when a project is assigned
5. Paste `mastery_verification.md` when a checkpoint is triggered
6. Paste `revision_engine.md` if you enter revision mode

### Step 4: Choose Your Learning Mode

The system will present three modes:

| Mode | Duration | Best For |
|------|----------|----------|
| **Skill Sprint** | 2-4 weeks | Learning a new language or framework (e.g., "Learn Go", "Master React") |
| **Role Mastery** | 2-3 months | Comprehensive role preparation (e.g., "Backend Developer", "DevOps Engineer") |
| **Concept Deep Dive** | 1-2 weeks | Mastering one complex topic (e.g., "System Design", "Database Internals") |

### Step 5: Tell It What You Want to Learn

After selecting a mode, state your learning goal:

> "I want to learn backend development with Node.js" 

or

> "I need to master Kubernetes for a DevOps role"

or

> "I want to deeply understand distributed systems"

The system takes it from there.

---

## What to Expect

### It Will Be Uncomfortable

This system is designed to make you struggle. That's the point. You will:

- Be thrown into projects before you feel ready
- Be asked to explain things you thought you understood
- Be told to "figure it out" when you want a quick answer
- Be forced to rebuild things from memory
- Feel frustrated -- that means it's working

### The 5 Learning Phases

1. **Foundation Blitz** (Days 1-2) -- Build a complete mental map of the topic. No code. Only understanding how all the pieces connect.

2. **Uncomfortable Immersion** (Days 3-5) -- Get thrown into a real-world project that's just beyond your ability. Architecture guidance only, zero code provided.

3. **Iterative Deepening** (Days 6-14) -- Build 3-4 progressively harder projects. Each one targets your weak spots.

4. **Production Simulation** (Days 15-21) -- Build one impressive, portfolio-worthy project with production-grade concerns (error handling, security, scale).

5. **Teaching Mode** (Final 2 days) -- Write a blog post, create a video script, and document your architecture. If you can teach it, you know it.

### Verification Checkpoints

The system doesn't just teach -- it verifies:

- **Every 3 days**: Teach-back session (explain a concept as if teaching a junior dev)
- **Every 7 days**: Memory rebuild (rebuild a past project from scratch, no notes)
- **Every 14 days**: Production interview (simulated senior engineer interview)

### Revision Mode

If you've learned something before but forgot it, the system has a dedicated revision workflow:

- Diagnoses exactly what you forgot (not what you remember)
- Fixes only the gaps through targeted micro-challenges
- Tests end-to-end execution after repair
- Locks the knowledge with teach-back and production context exercises

Trigger it by saying: *"I need to revise Docker"* or *"I'm rusty on Kubernetes"*

---

## Customization

### Personalizing the User Profile

The `master_orchestrator.md` contains a `USER_COGNITIVE_PROFILE` section with default values. Edit these to match your learning style:

- **Primary Style**: How you prefer to absorb information (big picture first vs. detail first)
- **Retention Strength**: Where you naturally retain well vs. where you lose knowledge
- **Overwhelm Trigger**: What causes you to shut down (information dumps, ambiguity, etc.)
- **Motivation Triggers**: What pushes you to keep going when stuck

### Adjusting Difficulty

The system auto-calibrates, but you can influence it:

- If projects are too easy, tell the LLM: *"Increase difficulty. Add more constraints."*
- If you're genuinely drowning (not just uncomfortable), say: *"I need more structure on this specific part."* The system will give you a better breakdown without giving answers.

### Adding Your Own Projects

The `project_generator.md` includes 12 example projects and a template structure. The LLM is instructed to generate new projects tailored to whatever you're learning -- the database is a reference for quality, not a fixed curriculum.

---

## Tips for Best Results

1. **Be honest about what you don't know.** The system works by finding gaps. Pretending you understand wastes your time.

2. **Don't fight the discomfort.** If you feel frustrated, you're in the learning zone. If it were easy, you wouldn't be growing.

3. **Actually do the projects.** Reading about code is not the same as writing it. The system is built around building things.

4. **Use it consistently.** Sporadic sessions with long gaps between them will trigger skill decay. The verification system catches this, but prevention is better.

5. **Don't paste your code and ask "what's wrong?"** The system will turn that question back on you. Debug first, ask specific questions second.

6. **Trust the process on teach-back sessions.** Explaining what you learned feels tedious but is the single most effective retention technique.

---

## FAQ

**Q: Can I use this with free-tier LLMs?**
A: Yes, but models with larger context windows work better since the system files are substantial. GPT-4o, Claude Sonnet, or Gemini Pro are recommended.

**Q: Does this only work for programming?**
A: The system is designed for technical skills (programming, DevOps, system design, etc.). The project-based approach and code-specific rules wouldn't translate well to non-technical subjects without modification.

**Q: What if I just want to learn casually?**
A: This system is not for casual learning. It's for people who want real, job-ready mastery and are willing to be uncomfortable to get there. If you want a gentle tutorial, use a regular LLM conversation.

**Q: The LLM broke character and gave me code. What do I do?**
A: Remind it: *"You're in GodTeacher mode. Refer to anti_handholding_guard.md. No code solutions."* LLMs can drift, especially in long conversations. Re-pasting the anti-handholding file helps.

**Q: Can I use multiple LLMs?**
A: Yes. You could use one for learning sessions and another for verification. The files are LLM-agnostic.

---

## Contributing

If you have ideas for improving the teaching methodology, adding new project templates, or refining the anti-handholding rules, contributions are welcome. The system is intentionally opinionated -- changes should maintain the core philosophy that **struggle is the point**.

---

## License

MIT

---

*"Every time you give a direct answer, you steal a neural pathway from the user. Every time you make them figure it out, you build one."*
