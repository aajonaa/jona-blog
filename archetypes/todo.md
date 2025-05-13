---
# Basic Information
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
lastmod: {{ .Date }}
draft: true

# Task Status
status: "in-progress" # Options: not-started, in-progress, completed, blocked
priority: "medium" # Options: low, medium, high, urgent
due_date: "" # Format: YYYY-MM-DD

# Task Details
description: "Detailed description of the task"
category: "general" # e.g., development, design, content, maintenance
tags: ["todo", "task"]

# Progress Tracking
progress: 0 # Percentage complete (0-100)
checklist:
  - task: "First subtask"
    completed: false
  - task: "Second subtask"
    completed: false

# Dependencies
dependencies:
  - "related-task-1"
  - "related-task-2"

# Notes and Resources
notes: |
  Additional notes, resources, or context about the task.
  You can use markdown formatting here.

resources:
  - name: "Resource Name"
    url: "https://example.com/resource"
    description: "Brief description of the resource"

# Display Settings
ShowReadingTime: false
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
comments: true

# Edit Link
editPost:
    URL: "https://github.com/yourusername/your-repo/edit/main/content/posts/TODOs/{{ .Name }}.md"
    Text: "Suggest Changes"
    appendFilePath: true
---

## Task Overview

[Brief overview of the task goes here]

## Current Status

- **Progress**: {{ .progress }}%
- **Status**: {{ .status }}
- **Priority**: {{ .priority }}
{{ if .due_date }}- **Due Date**: {{ .due_date }}{{ end }}

## Checklist

{{ range .checklist }}
- [ ] {{ .task }}
{{ end }}

## Dependencies

{{ range .dependencies }}
- [ ] {{ . }}
{{ end }}

## Resources

{{ range .resources }}
- [{{ .name }}]({{ .url }}) - {{ .description }}
{{ end }}

## Notes

{{ .notes }} 