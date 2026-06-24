# AGENTS.md

This file provides project-level guidance to AI agents working in this repository.

## Overview
This repository contains an Ansible deployment for a Glastopf web application honeypot. It provisions and configures the honeypot across multiple environments (Raspberry Pi, Vagrant, EC2).

## Agent Rules
- **No Secrets**: Never write secrets, API keys, or credentials to files. Use environment variables (e.g., `AWS_ACCESS_KEY_ID`).
- **Code Style**:
  - YAML: 2-space indentation. Use FQCN for Ansible tasks (e.g., `ansible.builtin.command`).
  - Playbooks: Keep tasks idempotent.
- **Documentation**: Updates to `README.md` must be command-first, scannable, and avoid machine-specific local tooling.
- **Testing**: Run tests locally using `molecule test` via the `uv` virtual environment before submitting changes.
