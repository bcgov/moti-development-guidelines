# Code Review Guidelines

These guidelines apply to MOTI GitHub project repositories or Subversion project code.
Code Review aims in reviewing the software code and examining for any errors in that. 
The goal of the reviews is to improve the code quality by having several pairs of eyes on the code, for the benefit of all. It helps in reducing the ratio of defect multiplication and avoids later-stage error detection by simplifying all the initial error detection processes. This code review should come under the review process of any application.

There are some principles should be considered before conducting code review:

- Understand the code's purpose: Make sure you understand the purpose of the code and how it fits into the overall system before you begin reviewing it. This will help you identify any issues or potential improvements.
- Check for correctness: Review the code to ensure that it is correct and complete. Look for any bugs, syntax errors, or logical errors.
- Review for style and readability: Check that the code follows your team's style guide and is easy to read and understand. Look for things like naming conventions, indentation, and commenting.
- Check for security vulnerabilities: Review the code to ensure that it is secure and does not have any vulnerabilities.
- Consider performance: Consider the performance of the code and look for any potential bottlenecks or inefficiencies.
- Provide constructive feedback: When providing feedback, be respectful and focus on the code itself rather than the person who wrote it. Provide specific examples and suggestions for improvement rather than just pointing out problems.
- Be open to discussion: Code review is a collaborative process, and it is important to be open to discussion and willing to consider different perspectives.
- Follow up on feedback: Make sure to follow up on any feedback you receive and address any issues or suggestions that were raised.

Note: This is a general process, and the specific steps and tools used may vary depending on the needs and preferences of your team and project.

## Basic Contribution Principles

Here are a few points that are the basis of the development process and that should always be kept in mind.
- Any change in the sources should match with a JIRA issue
- Any code change must be unit-tested, this is required to ensure non-regression.
- Any code change must be implemented respecting the Coding and Design Guidelines.
- Always create a pull request (PR) from your feature or bug fix branch to the master branch.

# Code Review on GitHub

## Before Code Review

- Make sure you've read and understand the Coding and design Guidelines. The code must be designed for easy review and for future readers of the commits:
- Don't mix cleanups/reformatting with actual code. For example, if you've changed a simple line of code in a class and re-formatted the whole file in a single commit, then your change is invisible in the diff, hidden by all the formatting changes.
- Add the cleanup/format commit first.
- Use several commits for unrelated work.
- Use only one commit for related things. For example, don't have a separate "fix typo" commit if the typo fixed is in another commit of the PR.
- Set a detailed commit description.
- Diffs must be minimal.
- PRs with a lot of commits, let's say 10 for instance, should be avoided. We should be able to make PRs with light diffs. If not possible, create a draft PR and ask for a review as soon as possible.

### Write Tests
- Try to test all aspects of the code you write.

- For bug fixes, writing non-regression tests is mandatory: the tests must fail before the changes, and work after the changes.

- If writing a test seems too complicated, don’t hesitate to discuss it with the developers. They may, when possible, take over the non-regression test and finalize the PR.

## Code Review Process: 

-	Make sure Git is installed and configured.
- Make sure the code builds and passes tests.
-	Clone the GitHub repository locally.
- Create a new branch '<BRANCH>', respecting the branch naming policy. As an example, the branch naming policy could be like this: <TYPE>-<JIRA_ISSUE>-<SHORT_DESCRIPTION>. (For instance: git checkout -b 'fix-HETS-1234-fix-typo-of-ui')
  - As a TYPE, choose between fix, feature, improvement or task.
  - JIRA_ISSURE is the reference of the related Jira issue.
  - SHORT_DESCRIPTION should state what the changes in this branch do, using lowercase with hyphens.
- Apply your changes.
- Add your changes to the Git index: git add -A
- Add a commit message, respecting the commit conventions.
  - JIRA_ISSUE is the reference of the related Jira issue.
  - MESSAGE should state what the change in this commit does
  - BRANCH is the new branch name
  - For instance: git commit -m '<JIRA_ISSUE>: <MESSAGE>'
- Push your changes to the newly created branch in GitHub: git push -u origin <BRANCH>
- Go to the GitHub UI and click on the button to create a PR.
  - Add a first comment to explain your contribution.
  - Request explicitly some reviewers if you are aware of people in charge of the piece of code touched by the PR, or you simply think of someone legitimate or who could be interested.
- Review the code: Use GitHub's code review tools to review the code and make any necessary comments or suggestions. You can use the "Add a comment" feature to leave inline comments, or you can use the "Start a review" feature to leave general comments and suggestions.
- Once the reviewers have added some comments, you must:
   - Take into account all comments requesting changes, either by doing the requested changes, or by discussing further and getting to a consensus between you and the commenters.
  -Reply to any other comment, or simply acknowledge with an appropriate emoji reaction.
  - If there are fixes to do, amend the commits (see below), don't create further commits for the fixes (think about people reading commits one by one to understand the logic of the code). For instance: git commit --amend -m '<MESSAGE>', then git push -f
  - After you've done fixes and amended code, add a comment in the PR to summarize your changes, and ask the commenters and reviewers for another review.
- Once your PR is valid in GitHub, click on the Rebase and Merge button. Valid here means that:
  - The changes have been approved by the reviewers.
  - All checks have passed.
  - The branch has no conflict with the base branch when rebasing.
  - For those OpenShift projects that have GitHub Actions pipelines set up, once a PR is created in GitHub, a GitHub Action is triggered on the related branch and sets some GitHub status checks on the PR, build and deployment to OpenShift Dev environment will be conducted. 
  - Once the Dev Deployment is done successfully, and related features or bug fixed are verified from Dev environment, the developer can make a request to deploy the changes to OpenShift Test environment.
  - Business Analyst will approve the request to Test deploy, once the Test deploy is verified, the developer can make a request to deploy to Product environment.
  - Before Business Analyst approve to deploy the changes to Product, CAB should be applied to describe detailed change data and time, backup plans and the CAB documentation will be reviewed and approved by the change request committee.
  - Once CAB is approved, conduct the changes according to the plan to deploy the changes to Product environment.
  - Ask BA to verify Product environment, if everything is OK, merge the code changes to the master branch. 
- Merge the code: Once all comments and suggestions have been addressed and the code is ready to be merged, use GitHub's merge tools to merge the code into the target branch (usually master).


## During The Code Review

- In your review, be clear about whether you're requesting a change or you're just mentioning a FYI to the committer. 
- Be consistent and don't approve while asking for changes in the comments.
- Do not be overly picky: adjust your review level to the level of the coder. The code doesn't have to be perfect, but the goal is still to have a good code quality.
- While it's OK to write short and to-the-point comments, try not to be needlessly abrupt.
- Note that coders and reviewers may be geographically distant, if you cannot do the review side by side, you should just always assume the best intentions: people are trying to help, not to criticize you personally.
- Approving a PR both does and does not engage the reviewer's responsibility: the reviewer is not expected to be foolproof but it must be a promise that a human eye effectively did look at the code. If a reviewer does not understand the JIRA issue or the majority of the code, they should not approve the PR (it's always OK to add comments).


When reviewing or submitting a PR, there are a lot of things that can be checked. Here is a non-exhaustive and unsorted list of points that should draw your attention:

Review check list and types:
- Are the Coding and Design Guidelines respected?
- Are there non-regression tests covering the changed code?
- Does the PR do what it is supposed to do? If it covers more, maybe some code should go to another PR. If it doesn't cover the full scope of the original issue, there might be some missing content.
- Are there potential security issues?
- Are there any extra files included in the PR that shouldn't be there?
- Were new dependencies added to the project? If yes, why were they added?
- Can I build the branch without any compilation error?
- Are there any new compilation warnings brought by the changes when building the impacted modules?
- Are there any failing tests? If yes, why are they failing?
- Has the related JIRA issue been updated: description, release notes, upgrade notes?
- Is there any impact on the documentation to reflect the changes?

Obviously, we can't expect from a reviewer to address the whole list, neither to always spend a lot of time reviewing a PR. It's up to the reviewers to choose the type of review they are ready to do, for instance:

- "Quick": read the PR globally, check the basic coding guidelines, make sure the non-regression tests aren't missing. This shouldn't take more than one or two hours. This can be the case of reviewers not considering themselves as experts on the topic but can judge if the PR seems globally OK/not OK.
- "Deep and complete": read the commits in detail, checkout the branch, run the tests, open the code in an IDE, etc. This could take up to several days!
- "Compromise": a subtle mix of the above-mentioned strategies.

In any case, a review is always good to have!

## After The Code Review

- Read all comments made, and try not to be offended by the short, sharp or abrupt sentence formulations that a reviewer may use. There may not always be complete phrases or "please", or "could you", but that's OK, it's a technical review, not a social encounter.

- You must take into account all comments requesting changes, either by doing the requested changes (then it's a good idea to 👍 the comment), or by discussing further and getting to a consensus between you and the commenters.

- Reply to any other comment, or simply acknowledge with an appropriate emoji reaction.

- If there are some changes to do, there are basically two solutions:

  - If the PR contains a few commits, let's say 3 or 4, you should amend the appropriate commits and force push the branch. Don't create further commits for the fixes (again, think about people reading commits one by one to understand the logic of the code).
  - If there are a lot of commits, let's say 5 or more, it's OK and probably a good idea to add some additional commits including the new changes:
  - It makes things clearer and easier to re-review.
  - It's safer: rebasing the PR is a risk of impacting some changes that have already been fully reviewed and validated.
  - It is interesting to have in the history the result of a (possibly long) discussion and process that lead to these additional changes.
  - Of course, these are only recommendations and there is no absolute way of doing, it always depends on the case.

- Use the "Resolve conversation" button to let the reviewers know that comments were taken into account.
- It's a good idea to add a message in the PR to summarize your changes and ask the reviewers for another review.

# Code Reviews on Subversion

To conduct a code review based on Subversion, you can follow these steps:
- Create a new branch for the code you want to review. This will allow you to make changes to the code without affecting the main branch.
- Check out the code from the new branch and review it locally on your machine. Look for any issues with the code, such as bugs, security vulnerabilities, or coding style violations.
- Make any necessary changes to the code and commit them to the new branch.
- Once you have finished reviewing the code, you can create a pull request to merge the changes from the new branch into the main branch. This will allow other members of your team to review the changes and provide feedback.
- After the code has been reviewed and any necessary changes have been made, you can merge the pull request and deploy the code to production.

# Tools for Code Review

There are many tools that can be used for code review, and some of them can work with both Subversion and GitHub repositories, such as Review Board and Phabricator, which allow you to manage code reviews in a consistent way across projects, regardless of the version control system being used.

- Git - a version control system that allows you to track changes to your code and work with others on the same codebase

- GitHub - a web-based platform for hosting Git repositories that includes features for code review, such as pull requests and code review comments

- GitLab - a web-based platform for hosting Git repositories that includes features for code review, such as merge requests and code review comments

- Subversion (SVN) - a version control system that allows you to manage code changes and collaborate with other developers

- Bitbucket - a web-based platform for hosting Git and Mercurial repositories that includes features for code review, such as pull requests and code review comments

- Gerrit - an open-source code review tool that integrates with Git repositories and includes features such as code review comments, patch sets, and integration with continuous integration systems.

- Review Board - an open-source code review tool that supports multiple version control systems and includes features such as code review comments, review requests, and integration with bug tracking systems.

- Crucible - a code review tool from Atlassian that supports multiple version control systems and includes features such as code review comments, review requests, and integration with JIRA.

These are just a few examples of the many tools that are available for code review. The best tool for your team will depend on your workflow, the version control system you use, and your specific needs and preferences.
