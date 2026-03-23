---
name: code-simplifier
description: Use when simplifying, cleaning up, or refactoring existing code without changing behavior, especially after recent edits or when polishing touched files for clarity, consistency, and maintainability.
---

# Code Simplifier

## Overview

Simplify and refine code for clarity, consistency, and maintainability while preserving exact behavior. Default to recently modified code unless the user asks for a broader scope.

## Core Rules

### 1. Preserve Functionality

Do not change what the code does. Keep the same features, outputs, side effects, and externally visible behavior.

When a simplification could alter behavior, stop and treat it as a separate change rather than folding it into cleanup work.

### 2. Apply Project Standards

Read and follow the active project instructions first, including repository guidance such as `AGENTS.md`, `CLAUDE.md`, linters, formatters, and existing code patterns.

If the repository does not define a rule, prefer:

- the dominant style already used in the touched area
- explicit, readable code over compressed cleverness
- naming and structure that match nearby code

### 3. Enhance Clarity

Look for opportunities to:

- reduce unnecessary complexity and nesting
- remove redundant code, branches, and abstractions
- improve variable, function, and type names when that improves readability
- consolidate related logic that is currently scattered
- remove comments that restate obvious code
- replace dense or hard-to-scan constructs with clearer control flow

Prefer code that is easy to read, debug, and extend.

### 4. Maintain Balance

Do not over-simplify. Avoid changes that:

- trade readability for fewer lines
- combine unrelated concerns into one function, class, or component
- remove abstractions that still serve a useful organizational purpose
- introduce clever patterns that are harder to understand than the original code
- make future debugging or extension harder

### 5. Focus Scope

By default, refine only code that was recently modified, is in the current diff, or is directly adjacent to the requested change.

Expand scope only when:

- the user asks for broader cleanup
- a nearby issue blocks a clean simplification
- a small supporting cleanup is necessary to keep the result coherent

## Refinement Process

1. Identify the recently modified or requested code.
2. Check project instructions and local patterns before changing style.
3. Find the highest-value simplifications that preserve behavior.
4. Apply the smallest maintainable changes that improve clarity.
5. Verify behavior is unchanged with the narrowest meaningful checks.
6. Summarize only the material simplifications and any residual risk.

## Verification

After simplification, run the most relevant lightweight verification available for the touched code, such as targeted tests, lint, typecheck, or other local validation commands.

If no meaningful verification is available, say so explicitly instead of implying certainty.
