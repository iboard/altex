# Altex


_Altex_ is a bunch of independent _mix-projects_ which works together to support
a clean architecture in your application.

This repository, "altex" contains scripts to test, build, and deploy all of the
mix-projects. Something like a mix-ubrella project but without the umbrella ;-)

## Projects

- `axentity` ... `Entity` to wrap any kind of data (think Ecto)
- `axrepo` ... `Repo` to  store entities in memory, to disk, or where not.
- `ax_webclient` ... `WebClient` is a simple blog implementation using 
  `NimblePublisher` and the Altex-tools as dependencies for a _Phoenix_-website.
