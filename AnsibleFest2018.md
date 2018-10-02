# Overall Notes
  Splunk

# Best Practices - Organizing Playbooks
##  Opening
  Ansible for DevOps - Jeff Geerling (book)
  Docker -> Kubernetes
  Mac Dev Playbook
## Notes
Start with a repo
Start a playbook, main.yml
Commit it (first working build)
git reset --head
Playbooks awys run from a build server
"If it's important, it will be forgotten"  - Jeff Geerling

## README
  Purpose
  Links (CI, docs, issue tracking)
  Instructions for local testing

## Small Files
  < 100 lines per file
  Start by splitting out related tasks with include_*
  Progress to single-responsibility roles

## Roles
  Make roles generic
  Share roles among projects
  Contribute to / use from Galaxy?
  Split roles by software package
  Include version with requirements.yml

## Value (Increasing complexity)
  yamllint
  ansible-playbook --syntax-check
  ansible-lint
  molecule test (integration)
  ansible-playbook --check (against prod)
  Parallel infrastructure (blue/green)

## Testing
  Heed [DEPRECATION WARING]s
  Read through porting guides
  Disable annoying WARN messages
  Target latest Ansible release
  Keep CI environment updated

## Best Practices
  Prefer simple, flat variables over dicts
  NO:
  apache:
    startservers: 2
    maxservers: 2
  YES:
    apache_startservers:2
    apache_maxservers:250

## SPEED
  CI is useless if slow
  Disable gather_facts if not needed
  forks config - fully utilize resources
  package - pass list to name instead of a loop
  copy - only for single files or small dirs
  lineinfile - try to switch to template instead of looping on one file
  (ansible callback plugins! - try YAML) callback_whitelist = profile_roles, profile_tasks, timer

  END