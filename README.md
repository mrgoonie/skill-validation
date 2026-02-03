# Skills vs Commands Benchmark

Experimental framework for comparing **Skill** vs **Slash Command** prompt adherence in Claude Code.

## Metrics

1. **Accuracy**: Steps completed correctly / total steps
2. **Token Efficiency**: Tokens consumed for same task
3. **Consistency**: Variance between runs

## Structure

```
skill-validation/
├── .claude/
│   ├── skills/benchmark-fileops/     # Skill implementation
│   ├── commands/benchmark-fileops.md # Command implementation
│   ├── hooks/                        # Logging hooks
│   └── settings.json                 # Hook configuration
├── scripts/
│   ├── verify-steps.py               # Step verification
│   ├── analyze-benchmark-results.py  # Results aggregation
│   └── run-benchmark.sh              # Automation script
└── plans/reports/                    # Benchmark reports
```

## Usage

### Automated Runs

```bash
# Sequential (default)
./scripts/run-benchmark.sh all 3

# Parallel execution (6 runs simultaneously)
./scripts/run-benchmark.sh all 3 --parallel

# Specific model
./scripts/run-benchmark.sh all 3 --model haiku
./scripts/run-benchmark.sh all 3 --model sonnet
./scripts/run-benchmark.sh all 3 --model opus

# Combined flags
./scripts/run-benchmark.sh all 3 --parallel --model haiku

# Run only skills or commands
./scripts/run-benchmark.sh skill 3
./scripts/run-benchmark.sh command 3
```

### Options

| Flag | Description |
|------|-------------|
| `all\|skill\|command` | Method to benchmark (default: all) |
| `[runs]` | Number of runs per method (default: 3) |
| `--parallel` | Run all tests simultaneously |
| `--model <name>` | Model: haiku, sonnet, opus (default: account default) |

### Analysis

```bash
~/.claude/skills/.venv/bin/python3 scripts/analyze-benchmark-results.py
```

## Test Task

21-step file operations workflow:
- Phase 1: Directory setup (steps 1-4)
- Phase 2: File creation (steps 5-10)
- Phase 3: Read operations (steps 11-13)
- Phase 4: Modify operations (steps 14-17)
- Phase 5: Verification (steps 18-21)

## Reports

Generated reports saved to `plans/reports/benchmark-YYMMDD-HHMM-fileops.md`
