# Code Review Checklist

This is a living document. If you would like to contribute changes, please send
a pull request. Everyone is encouraged to participate in conversations on each
pull request, so watch this repository for changes.

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

- [ ] Will this change affect sample data?

  Does the migration a new fields, new models, or remove/change existing fields? If the application uses database seeding or has a sample dataset in the form of a database dump or script, update these items to reflect the new state of the database. Also ensure that running the script, importing the database dump, or running the database seeds from an empty database can be executed successfully after this change.
  
### User Experience

- [ ] Does this change meet all of the requirements (as specified in the Pivotal story and other sources)? When previewing the change, does it meet both the letter and spirit of the requirements?

- [ ] Does the change result in an intuitive and well-conceived user experience? Is the change consistent with existing design patterns?

### Housekeeping

- [ ] Is the documentation still correct?

  Would a new developer be able to get up and running? Will existing developers
  need to install new dependencies? If so, will it be immediately obvious what
  they need, and how they can get it?

- [ ] If there are infrastructure or dependency changes, are deployment considerations taken into account? Is there a plan established to update non-dev/test environments?

- [ ] If code was removed as part of this change, is there now unused code (CSS, javascript, ruby methods, metrics tracking, etc.) or files that should also be removed?

- [ ] Does the change introduce new code that effectively does the same thing as existing methods, test steps, etc.?

- [ ] Is the change well-tested based on previously established testing conventions within the codebase?
