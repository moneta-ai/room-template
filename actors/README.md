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
