---
name: gitbutler-phantom-changes
description: Use when GitButler reports removed files already absent from the branch and remote, rejects them as "no effective change to commit", or discard toggles removals into additions.
---

# Recover GitButler Phantom Changes

Treat this symptom as a possible stale Git index before rewriting history or
resetting GitButler metadata.

1. Verify the branch tip and remote tree already have the intended files:

   ```bash
   git rev-parse HEAD refs/remotes/<remote>/<branch>
   git ls-tree HEAD -- <paths>
   git ls-tree refs/remotes/<remote>/<branch> -- <paths>
   ```

2. With authorization to rebuild the managed workspace, expose the underlying
   Git state:

   ```bash
   but teardown --checkout-to <branch>
   git status --short --branch
   ```

3. Apply this recovery only when each phantom path is absent from `HEAD` and the
   working tree but appears as `AD`: staged as an addition and deleted in the
   working tree. Unstage only those verified paths:

   ```bash
   git restore --staged -- <paths>
   git status --short --branch
   ```

   The status must now be clean. Do not use `reset`, restore file contents, or
   rewrite commits for this signature.

4. Reinitialize and verify:

   ```bash
   but setup
   but status --json
   ```

   Require no uncommitted changes and confirm the applied branch tip still
   matches its remote.

`but teardown` alone does not clear stale index entries; running `but setup`
before unstaging them can import the phantom state again. If the paths do not
show the exact `AD` signature, stop and diagnose the differing state instead of
applying this procedure.
