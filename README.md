# Code Review Checklist

This is a living document. If you would like to contribute changes, please send
a pull request. Everyone is encouraged to participate in conversations on each
pull request, so watch this repository for changes.

## Code Review Process

Before starting a development cycle, a code review process should be established. Some considerations:

- [ ] Have code reviewers been established for the project?

  If it is a sole-developer project, is there an outside developer will bandwidth able to review proposed changes?
  
- [ ] What is the process for developers to alert others developers that a pull request is ready for review?

  Oftentimes, this can be facilitated with an `@ mention` and a change of the pull request's label.
  
- [ ] What is the process to signal that a pull request has been reviewed and can be merged?

- [ ] Once the pull request is ready to be merged, who will merge it?

  Anyone? The pull request author? The project lead?

- [ ] Does anyone in particular need to sign off on the pull request before it can be merged to `master`?

  Does the project lead or project manager need to sign off on the change, in addition to other pull request reviewers?

- [ ] How are pull requests going to be mapped to requirements?

  When reviewing a pull request, how will the reviewer know what requirements are applicable?

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
