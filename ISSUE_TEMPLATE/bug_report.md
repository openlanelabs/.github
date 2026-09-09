name: Bug report
description: Something is broken or behaving incorrectly
labels: ["bug", "triage"]
body:
  - type: markdown
    attributes:
      value: |
        Thanks for taking the time to report a bug. Please fill in as much as you can.
  - type: textarea
    id: what-happened
    attributes:
      label: What happened?
      description: A clear description of the bug. If applicable, add screenshots.
      placeholder: The task completion button did nothing.
    validations:
      required: true
  - type: textarea
    id: expected
    attributes:
      label: What did you expect to happen?
    validations:
      required: true
  - type: textarea
    id: steps
    attributes:
      label: Steps to reproduce
      description: Minimal reproduction — the smaller, the faster we fix it.
      placeholder: |
        1. Create project from template
        2. Click complete on customer task
        3. Nothing happens
    validations:
      required: true
  - type: dropdown
    id: area
    attributes:
      label: Area
      options:
        - projects
        - customer-portal
        - tasks
        - docs-files-forms
        - resources
        - time
        - money
        - integrations
        - agents
        - api
        - auth/security
        - infra
        - ui/ux
        - other
    validations:
      required: true
  - type: input
    id: version
    attributes:
      label: Version / commit
      description: Self-hosted: `git rev-parse HEAD` or docker tag. Cloud: workspace + approximate time.
      placeholder: v0.1.0 / commit sha
  - type: textarea
    id: logs
    attributes:
      label: Relevant logs
      description: Output from `apps/api` or `apps/worker`. Redact secrets and PII.
      render: shell
