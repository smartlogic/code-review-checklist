# Code Review Checklist

This is a living document. If you would like to contribute changes, please send
a pull request. Everyone is encouraged to participate in conversations on each
pull request, so watch this repository for changes.

## Feature Development Process

Before starting a development cycle, the project team should agree on a development process to ensure efficient communication and high quality control. Code review should be an integral part of this process. Here are some guidelines and considerations for establishing an effective code review process:

- [ ] Establish code reviewers for the project

  - If the project requires only a sole-developer, make an arrangement with other developers at the company to review major changes in order to get feedback and ensure quality product delivery.
  - If there are part time developers on the project, establish guidelines for communicating the status of work-in-progress features for when those developers are not actively contributing. This will help the team avoid bottlenecks.

- [ ] Set timeliness expectations

  It's often helpful to establish an expectation for when fellow developers will perform code reviews as well as to more generally check-in with the rest of the team. A good guideline to follow is for each developer to check-in at least once every 24 hours. 

- [ ] Communicating when a pull request is ready for code review

  Depending on personal perference, some developers may open a pull request and track their progress as the feature goes from the `work-in-progress` state to the `ready-for-review` state, while others will only open a pull request once the feature is `ready-for-review`. Individuals preferences should be communicated to the rest of the team at the start of the project, and a system should be established to commnicate when other developers should proceed with code review. Some suggestions for this process are:
  - Use GitHub's label system to communicate the status of a pull request, such as `WIP`, `pending CI`, `for review`, and `ready to merge`
  - If a team member has experience with a specific area of the codebase or technology, call their attention to the pull request and request they review the change by using an `@mention`. Similarly, if your team has designated a particular system for code reviews, `@mention` those developers to alert them that the change is ready for review.

- [ ] Verify the project's branch management and deployment process

  Before a development cycle begins, the team should decide on a convention for how feature branches will be merged to `master` and how those changes will be deployed to the various environments that have been established. Here's a few methods for branch management:
  - Merge feature branches to `master` and deploy to each of the environments at-will. No scheduled deployment window necessary. Standard agile development approach. The `master` branch tracks directly with the Production environment.
  - Maintain a `production` branch separately from `master` to facilitate a more traditional waterfall deployment. The `production` branch tracks directly with the Production environment, while the lower environments (e.g. Staging) track to `master`.
  - Maintain a `beta` branch into which the feature branches are merged. The `beta` branch will then get merged to `master` after a predetermined amount of progress has been made, using a more traditional waterfall deployment approach. The `master` branch tracks directly with the Production environment, while the lower environments (e.g. Staging) track to the `beta` branch.

- [ ] Feature ownership

  From the point at which a developer `starts` a Pivotal story, through opening a pull request, through getting the feature branch merged and the story delivered, they should be thought of as the *owner* of this feature. This means that they are responsible for ensuring:
  - the feature's status is accurately conveyed via the Pivotal story as well as the GitHub pull request
  - the code changes pass CI
  - the pull request is peer-reviewed
  - the story is delivered to the client for review in a timely fashion
  The pull request's author should monitor the status of the pull request and ensure it is moving through the review process in a timely manner, following up with other developers or the client as necessary to faciliate this.

- [ ] Reviewing a pull request

  Following the established code review process for the project, peer developers should review the pull request based on the guidelines delineated in the [Code Review Considerations](#code-review-considerations) section below. A couple of things to remember:
  - Don't forget to update the pull request's status using GitHub's labeling system, as appropriate.
  - Before a development cycle begins, determine if anyone on the development team must sign-off on the pull request before it can be merged in addition to the standard reviewers (e.g. the project lead, project manager, etc.).
  - Upon satisfactory review, reviewers should leave a comment on the pull request with a :+1: (with or without qualifications for merging).
  
- [ ] What is the process to signal that a pull request has been reviewed and can be merged?

- [ ] Once the pull request is ready to be merged, who will merge it?

  Anyone? The pull request author? The project lead?

- [ ] How are pull requests going to be mapped to requirements?

  When reviewing a pull request, how will the reviewer know what requirements are applicable?

- [ ] Keeping the process up-to-date

  Changes to the feature development process should be revisited as necessary at each iteration meeting. This will keep the process operating effectively, reduce confusion, and faciliate reasonable expectations for everyone on the team. Some indicators of when the process should be reviewed:
  - a developer is no longer full-time on the project, or a developer joins the team
  - it is noticed that the client has more feedback then usual, or is rejecting an unreasonable number of stories, indicating there may be a quality control issue

## Code Review Considerations

### Database Migrations

- [ ] Will this migration break in the future?

  Migrations that run today can break in the future. The most common cause is
  migrations that reference application code. Classes and methods can be removed
  or renamed. See [this awesome blog post](http://blog.testdouble.com/posts/2014-11-04-healthy-migration-habits.html)
  for examples and solutions.

- [ ] Will this require a maintenance window?

  Code gets deployed first, then migrations run. If the code depends on the
  migration, you should use a maintenance window when deploying the change. In
  general, prefer more, smaller deploys that don't require a maintenance window.

  If there is not a production environment, don't worry about it.

- [ ] Will this require significant downtime?

  Certain changes might be very slow. For example, adding a column with a
  default value to a table with 100mm rows is going to take a while. Plan ahead.
  In general, prefer more, smaller deploys that can run concurrently with
  production traffic.

  If there is not a production environment, don't worry about it.

### User Experience

- [ ] Does this change meet all of the requirements (as specified in the Pivotal story and other sources)? When previewing the change, does it meet both the letter and spirit of the requirements?

- [ ] Does the change result in an intuitive and well-conceived user experience? Is the change consistent with existing design patterns?

### Housekeeping

- [ ] Is the documentation still correct?

  Would a new developer be able to get up and running? Will existing developers
  need to install new dependencies? If so, will it be immediately obvious what
  they need, and how they can get it?

- [ ] If there are infrastructure or dependency changes, are deployment considerations taken into account? Is there a plan established to update non-dev/test environments?

- [ ] If code was removed as part of this change, is there now unused code (CSS, javascript, ruby methods, etc.) or files that should also be removed?

- [ ] Does the change introduce new code that effectively does the same thing as existing methods, test steps, etc.?

- [ ] Is the change well-tested based on previously established testing conventions within the codebase?
