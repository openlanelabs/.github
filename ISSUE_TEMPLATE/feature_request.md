name: Feature request
description: Propose a new capability or improvement
labels: ["enhancement", "triage"]
body:
  - type: markdown
    attributes:
      value: |
        Tell us the *job* you're trying to get done — not just the feature. We build for outcomes.
  - type: textarea
    id: problem
    attributes:
      label: What problem does this solve?
      description: Who is blocked, and what does it cost them?
      placeholder: As an implementation manager, I chase 12 customers over email and lose 60% of my week.
    validations:
      required: true
  - type: textarea
    id: solution
    attributes:
      label: What solution would you like?
    validations:
      required: true
  - type: textarea
    id: alternatives
    attributes:
      label: Alternatives you've considered
      description: Spreadsheets, Rocketlane, GUIDEcx, Asana, duct tape — anything.
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
        - ui/ux
        - other
    validations:
      required: true
  - type: checkboxes
    id: self-serve
    attributes:
      label: Are you willing to contribute this?
      options:
        - label: I might submit a PR for this
          required: false
