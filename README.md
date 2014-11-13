# Code Review Checklist

This is a living document. If you would like to contribute changes, please send
a pull request. Everyone is encouraged to participate in conversations on each
pull request, so watch this repository for changes.

## Database Migrations

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
