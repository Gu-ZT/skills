<div align="center">

# Codex Skills

**A personal collection of Codex skills for commits, Minecraft modding, README polish, and multi-platform CI scaffolding.**

English | [简体中文](README.zh_CN.md)

</div>

## Overview

This repository contains reusable Codex skills. Each skill is stored in its own directory and is described by a `SKILL.md` file with front matter metadata and workflow instructions.

The skills are written for agent-assisted development workflows where a user can invoke a focused capability with a prompt such as `$conventional-commits` or `$write-readme-header`.

## Skills

| Skill | Purpose |
| --- | --- |
| `conventional-commits` | Creates Git commits using Conventional Commits with a scoped Chinese subject and a concise bullet-list body. |
| `minecraft-modder-neoforge` | Guides Minecraft mod development with NeoForge, including items, blocks, entities, recipes, datagen, mixins, testing, and crash investigation. |
| `scaffold-multiplatform-ci` | Designs GitHub Actions workflows for quality checks, integration tests, release preparation, platform packaging, and release notes. |
| `write-readme-header` | Creates compact bilingual README mastheads and complete Simplified Chinese README counterparts. |

## Repository Layout

```text
.
|-- conventional-commits/
|   |-- SKILL.md
|   `-- agents/openai.yaml
|-- minecraft-modder-neoforge/
|   `-- SKILL.md
|-- scaffold-multiplatform-ci/
|   |-- SKILL.md
|   |-- agents/openai.yaml
|   `-- references/
`-- write-readme-header/
    |-- SKILL.md
    `-- agents/openai.yaml
```

## Usage

Place this repository's skill directories under your Codex skills directory, then invoke a skill by name in a Codex session:

```text
$conventional-commits
$minecraft-modder-neoforge
$scaffold-multiplatform-ci
$write-readme-header
```

Each `SKILL.md` is the canonical source of behavior. The optional `agents/openai.yaml` files provide interface metadata such as display names, descriptions, and default prompts.

## Maintenance

When adding or changing a skill:

- Keep the `name` field in `SKILL.md` aligned with the directory name.
- Write a concrete `description` that explains when the skill should be used.
- Put large reusable templates, examples, or checklists in a `references/` directory instead of expanding the main instructions indefinitely.
- Update both README files when the skill list, layout, or usage model changes.

## License

No repository-level license file is currently present. Check individual skill metadata before redistributing or reusing a skill outside this repository.
