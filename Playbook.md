# Playbooks

## Table of Content

- [Playbooks](#playbooks)
  - [Table of Content](#table-of-content)
  - [Writing tasks, plays, and playbooks](#writing-tasks-plays-and-playbooks)
    - [Working with inventory](#working-with-inventory)
    - [Interacting with data](#interacting-with-data)
    - [Executing playbooks](#executing-playbooks)
  - [Execution orders](#execution-orders)
  - [Import vs Include](#import-vs-include)
    - [**Includes: dynamic re-use**](#includes-dynamic-re-use)
    - [**Imports: static re-use**](#imports-static-re-use)
  - [Debugging](#debugging)
  - [Keywords](#keywords)

## Writing tasks, plays, and playbooks

- I have a specific use case for a task or play:

  - Executing tasks with elevated privileges or as a different user with become

  - [Repeating a task once for each item in a list with loops](https://docs.ansible.com/ansible/latest/user_guide/playbooks_loops.html#playbooks-loops)

  - Executing tasks on a different machine with delegation

  - [Running tasks only when certain conditions apply with conditionals and evaluating conditions with tests](https://docs.ansible.com/ansible/latest/user_guide/playbooks_conditionals.html)

  - Grouping a set of tasks together with blocks

  - Running tasks only when something has changed with handlers

  - Changing the way Ansible handles failures

  - Setting remote environment values

- I want to leverage the power of re-usable Ansible artifacts. How do I create re-usable files and roles?

- I need to incorporate one file or playbook inside another. What is the difference between including and importing?

- I want to run selected parts of my playbook. How do I add and use tags?

### Working with inventory

- I have a list of servers and devices I want to automate. How do I create inventory to track them?

- I use cloud services and constantly have servers and devices starting and stopping. How do I track them using dynamic inventory?

- I want to automate specific sub-sets of my inventory. How do I use patterns?

### Interacting with data

- [I want to use a single playbook against multiple systems with different attributes. How do I use variables to handle the differences?](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#playbooks-variables)

- I want to retrieve data about my systems. How do I access Ansible facts?

- I need to access sensitive data like passwords with Ansible. How can I protect that data with Ansible vault?

- I want to change the data I have, so I can use it in a task. How do I use filters to transform my data?

- I need to retrieve data from an external datastore. How do I use lookups to access databases and APIs?

- I want to ask playbook users to supply data. How do I get user input with prompts?

- I use certain modules frequently. How do I streamline my inventory and playbooks by setting default values for module parameters?

### Executing playbooks

Once your playbook is ready to run, you may need to use these topics:

- Executing “dry run” playbooks with check mode and diff

- Running playbooks while troubleshooting with start and step

- [Correcting tasks during execution with the Ansible debugger](https://docs.ansible.com/ansible/latest/user_guide/playbooks_debugger.html#playbook-debugger)


- Controlling how my playbook executes with strategies and more

- Running tasks, plays, and playbooks asynchronously

## Execution orders

1. Pre-tasks
2. Roles
3. Tasks
4. Post-tasks

## [Import vs Include](https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse.html#playbooks-reuse)

### **Includes: dynamic re-use**

Including roles, tasks, or variables adds them to a playbook dynamically. Ansible processes included files and roles as they come up in a playbook, so included tasks can be affected by the results of earlier tasks within the top-level playbook. Included roles and tasks are similar to handlers - they may or may not run, depending on the results of other tasks in the top-level playbook.

The primary advantage of using include_* statements is looping. When a loop is used with an include, the included tasks or role will be executed once for each item in the loop.

You can pass variables into includes. See Variable precedence: Where should I put a variable? for more details on variable inheritance and precedence.

### **Imports: static re-use**

Importing roles, tasks, or playbooks adds them to a playbook statically. Ansible pre-processes imported files and roles before it runs any tasks in a playbook, so imported content is never affected by other tasks within the top-level playbook.

You can pass variables to imports. You must pass variables if you want to run an imported file more than once in a playbook. For example:

```yaml
tasks:
- import_tasks: wordpress.yml
  vars:
    wp_user: timmy

- import_tasks: wordpress.yml
  vars:
    wp_user: alice

- import_tasks: wordpress.yml
  vars:
    wp_user: bob
```

## Debugging

- [Executing playbooks for troubleshooting](https://docs.ansible.com/ansible/latest/user_guide/playbooks_startnstep.html )
- [Debugging Tasks](https://docs.ansible.com/ansible/latest/user_guide/playbooks_debugger.html)

## [Keywords](https://docs.ansible.com/ansible/latest/reference_appendices/playbooks_keywords.html)
