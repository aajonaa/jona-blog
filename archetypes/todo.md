---
# Basic Information
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
# lastmod: {{ .Date }}
draft: true 

# Task Status
status: "not-started" # Options: not-started, in-progress, completed, blocked
priority: "medium" # Options: low, medium, high, urgent
due_date: "{{ dateFormat "2006-01-02" (now.AddDate 0 0 7) }}" # Default 1 week from now

# Task Details
description: "Detailed description of the task"
category: "general" # e.g., development, design, content, maintenance
tags: ["todo", "{{ .Name | urlize }}"]
weight: 1

# Progress Tracking
# The progress percentage will be calculated automatically based on completed tasks
checklist:
  - task: "Plan the task"
    completed: false
  - task: "Research necessary information"
    completed: false
  - task: "Implement core functionality"
    completed: false
  - task: "Test implementation"
    completed: false
  - task: "Document the process"
    completed: false

# Dependencies
dependencies:
  - "List any related tasks that need to be completed first"

# Notes and Resources
notes: |
  # Additional Notes
  
  Add detailed information, references, or context here.
  You can use full Markdown formatting:
  
  - Bullet points
  - Code blocks
  - Links
  
  ## Background Information
  
  Provide context for why this task is important.

resources:
  - name: "Documentation"
    url: "https://example.com/docs"
    description: "Official documentation for reference"
  - name: "Tutorial"
    url: "https://example.com/tutorial"
    description: "Step-by-step guide"

# Schedule Information
time_estimate: "2h" # Estimated time to complete
scheduled_date: "" # When you plan to work on this

# Display Settings
ShowReadingTime: false
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
comments: true
ShowToc: true

# Edit Link
editPost:
    URL: "https://github.com/yourusername/your-repo/edit/main/content/todos/{{ .Name }}.md"
    Text: "Suggest Changes"
    appendFilePath: true
---

## Task Overview

[Brief overview of the task goes here]

## Implementation Plan

1. First step
2. Second step
3. Third step

## Current Status

**Status**: not-started  
**Priority**: medium  
**Due Date**: {{ dateFormat "2006-01-02" (now.AddDate 0 0 7) }}  
**Time Estimate**: 2h

## Requirements

- Requirement 1
- Requirement 2
- Requirement 3