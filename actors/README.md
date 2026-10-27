# Actors

Each `*.md` file here is an actor document (`@moneta/abs`): an agent that
runs in CI, the tools it may use, the servers it talks to, and the names of
the secrets it needs. The document is the actor's whole authority. Changing it
changes what the agent may do, so change it only in a pull request the world's
owner merges. Every room in the world can address the actors listed here.

Secrets live in this repository's `room` Environment on GitHub, readable
from `main` only. The world's owner creates that Environment in the
repository's settings before the first actor that needs a secret is added
(Moneta's health checks say whether it's set up). Never write a secret value
in a file.

## Asking an actor from a room

A member can ask an actor from a room's timeline by starting a message with
`@` and its name, for example `@restock find two light, washed coffees`.
That works when `actors/<name>.md` and `.github/workflows/<name>.yml` are
both on `main`, and the workflow takes a `workflow_dispatch` input named
`entry` and uploads the runner's `abs-result` artifact. A workflow made from
`@moneta/abs`'s actor template does both. Moneta starts the workflow with
the path of that message as `entry`, one actor run per room at a time. The
message is whatever the member typed, so an actor that reads it treats it
as data: it says what to look for, never what the actor may do.

When the run ends, Moneta posts the actor's report to the same room as a
`result` entry, but only if this repository's `main` branch requires pull
requests (Moneta's `protected` health check). Without that rule, anyone who
can push could change what the workflow does, so Moneta posts its own notice
instead and the report stays on the run's page. Requiring a pull request
doesn't by itself mean anyone reviewed it: to make the actor's words mean
"reviewed", require an approving review on `main` and give no writer a
bypass. Moneta also posts only for a run it started; one started or re-run
by hand from GitHub's Actions tab gets no entry.

The timeline is append-only and lives in git, so a posted report stays in
this repository's history for good. Write each actor's job so that its
report leaves out anything that shouldn't live there.
