# DevOps Engineer Homework

This starter contains three intentional issues. Allow approximately one hour
to troubleshoot them, verify your changes, and submit your work.

## Requirements

- Bash on Linux, macOS, WSL, or Git Bash on Windows.
- Git and a GitHub account with permission to run GitHub Actions.
- No cloud account, credentials, or additional packages are needed.

Run the commands below from the repository root in Bash.

## Task 1: Fix a failing script (15 minutes)

```bash
bash task-1-script/random-data.sh
```

Correct the failure and explain what the script is doing.

## Task 2: Resolve a configuration issue (15 minutes)

```bash
bash task-2-configuration/show-service.sh
```

This script runs from the repository root but fails from another directory.
Make it work regardless of the caller's working directory. Successful runs
must print `Service: sample-worker` and `Environment: test`.

To reproduce the other-directory behavior:

```bash
repo_root="$(pwd)"
(cd .. && bash "$repo_root/task-2-configuration/show-service.sh")
```

Also verify that a missing configuration produces a useful error and a nonzero
exit code. Restore the configuration after testing.

## Task 3: Repair the automated check (20 minutes)

Review `.github/workflows/check-scripts.yml` and the GitHub Actions logs.
Fix the workflow so both corrected scripts run successfully. Keep the push
and pull request triggers, and ensure a script failure fails the workflow.

## Submission (10 minutes)

- Create your own repository from this starter, or fork it if permitted.
- Make your fixes on a branch, commit and push them, and open a pull request
  against your repository's default branch. Leave it open for review.
- Add a short findings section to this README describing each issue, how you
  identified it, your fix, and the commands or checks used to verify it.
- Provide your repository URL, pull request URL, and a successful Actions run
  URL. For private repositories, grant reviewers access.
- Do not include credentials, secrets, or employer information.

Stop after approximately one hour. If anything remains unresolved, submit
your progress, what you tried, and what you would investigate next.
## Findings

### Task 1

The script failed because the first `echo` used an unusual whitespace character. The output also referenced the wrong variable and misspelled `echo`. I noticed that storing binary data in a Bash variable can lose null bytes and that here-strings add a newline. I used a temporary file for the random bytes, fixed the output, and checked the result with `bash task-1-script/random-data.sh` in Git Bash. The script generates 10 random bytes, encodes them as Base64, and prints the counts and their sum.

### Task 2

The configuration path depended on the current working directory. I changed it to resolve `service.conf` relative to the script. I ran the script from the homework directory and its parent, and checked that a missing configuration reports an error and exits with a nonzero status. I restored the configuration afterward.

### Task 3

The starter available in this repository did not include the referenced workflow or its logs. I added a workflow at the repository root that runs both scripts from `junior` on pushes and pull requests. A failing script fails its workflow step.

### AI assistance

I used an AI assistant to help identify the script issues, suggest fixes, run local checks in Git Bash, and prepare the workflow and this findings section. I reviewed the changes and their output as we worked through the tasks.
