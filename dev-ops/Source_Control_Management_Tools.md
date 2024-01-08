# Source control management tools
1. Git Basic Operations:
    - `git init`: Initializes a new Git repository.
    - `git clone <repository>`: Creates a copy of a remote repository on your local machine.
    - `git add <file>`: Stages a file, readying it for a commit.
    - `git commit -m "message"`: Commits the staged snapshot with a brief log message.
    - `git status`: Shows the status of changes in the working directory.
    - `git pull`: Fetches the changes from the remote repository and merges it with the local one.
    - `git push`: Pushes the local changes to the remote repository.

2. Branching and Tagging:
    - `git branch <branch-name>`: Creates a new branch.
    - `git checkout <branch-name>`: Switches to the specified branch.
    - `git merge <branch-name>`: Merges the specified branch into the current branch.
    - `git tag <tag-name>`: Creates a new tag, which is a reference to a specific commit.

3. Git(hub) Flow:
    - Git Flow is a branching model for Git. It defines a structured model for branches and merging, making the development process cleaner and easier to manage.
    - The main branches in Git Flow are `master` (or `main`), `develop`, `feature/*`, `release/*`, and `hotfix/*`.
    - `master` (or `main`) is the main branch where the source code always reflects a production-ready state.
    - `develop` is the branch where the source code reflects a state with the latest delivered development changes for the next release.
    - `feature/*` branches are used to develop new features for the upcoming or a distant future release.
    - `release/*` branches are used to prepare for a new production release.
    - `hotfix/*` branches are used to act immediately upon an undesired state of a live production version.
# Questions
1. What are the benefits of VCS?
2. What is the difference between merge and rebase in git?
3. What is pull/merge request lifecycle?
4. How to update your last commit message?
5. How to restore lost commits after reset --hard?
6. What git bisect does?
7. What is Git (Lab/Hub) flow?
8. Compare gitflow and git common flow
# Answers
1. The benefits of Version Control Systems (VCS) include:
    - Collaboration: Multiple developers can work on the same project without overwriting each other's changes.
    - Versioning: You can keep track of changes over time, and revert back to previous versions if needed.
    - Backup: All versions of all files are stored, providing a backup in case of data loss.
    - Accountability: You can see who made each change, when they made it, and why.

2. The difference between merge and rebase in git:
    - Merge takes the contents of a source branch and integrates it with the target branch. A new merge commit is created in the target branch.
    - Rebase moves or combines a sequence of commits to a new base commit. It's like saying "I want to base my changes on what everybody else has already done".

3. Pull/Merge Request Lifecycle:
    - Create the Pull Request: After pushing your branch, create a new pull request in the repository.
    - Review: Other developers review the changes, discuss modifications, and approve the pull request.
    - Test: Automated tests are run to ensure the changes don't break anything.
    - Merge: Once approved and tests pass, the pull request is merged into the target branch.

4. To update your last commit message, you can use the command `git commit --amend -m "New commit message"`.

5. To restore lost commits after `git reset --hard`, you can use the `git reflog` command to find the commit hash, and then use `git cherry-pick <commit-hash>` to restore the commit.

6. `git bisect` is a binary search tool in Git used to find the commit that introduced a bug by using binary search.

7. Git (Lab/Hub) flow is a lightweight, branch-based workflow that supports teams and projects where deployments are made regularly. It's centered around the master branch, feature branches, and pull requests.

8. Gitflow is a specific branching model in Git. It's very structured and great for large projects with several parallel releases. Git common flow (or GitHub flow) is simpler. It's great for projects that deploy often and accept changes quickly.
