# #30940

## Current behavior

Updating PDM's lock file, Renovate calls PDM in a way that creates arch-specific lockfile metadata.

This causes subsequent invocations of `pdm install` on different architectures to fail, as can be
seen in the *Lock file maintenance* PR on this repo, which was created by Mend Renovate, whose
runners run on amd64, but has CI pipelines that run on Mac OS (aarch64) fail.

**NOTE:** In the process of creating this repository, I noticed that this is a more general
problem not limited to architectures. Even a slight mismatch in the Python platform
(e.g. `manylinux_2_35_x86_64` instead of `manylinux_2_36_x86_64`) will cause similar issues.
Honestly, this might be worth reporting on PDM's side as well, because I can't imagine what
good this new feature could possibly do...

## Expected behavior

If they don't want to make the default behavior more sane on PDM's side,
Renovate should invoke PDM's lock file update commands in a way that leads
to platform-independent lockfile metadata.

## Link to the Renovate issue or Discussion

https://github.com/renovatebot/renovate/discussions/30940
