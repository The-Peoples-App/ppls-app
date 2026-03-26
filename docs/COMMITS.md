# Team Operations & Technical Workflows

## 1. The "Inside-Out" Protocol
Because we utilize a private submodule for strategy, we follow a strict **"Inside-Out"** commit pattern. This ensures sensitive data remains air-gapped and prevents "Broken Pointer" errors on the public site.

### 1.1 Automated Safety Rail (Recommended for Devs)
To simplify the submodule-then-parent sequence, use the custom auditor script:

* Usage: `./bin/hpush`
* Function: This script blocks the public push if it detects uncommitted internal changes or an outdated pointer.

### 1.2 Manual Step-by-Step (Fallback)
If you are not using the script, follow these steps exactly:

   1. **Enter Submodule:** `cd docs/internal`
   2. **Commit Content:** `git add .` -> `git commit -m "..."`
   3. **Push Internal Remote:** `git push origin main`
   4. **Exit to Root:** `cd ../..`
   5. **Update Pointer:** `git add docs/internal` (This stages the new "Coordinates").
   6. **Commit & Push Public:** `git commit -m "chore: sync internal"` -> `git push origin main`

------------------------------
### 2. Instructions for Non-Technical Staff (GitHub Desktop)
If you are using the **GitHub Desktop** application, follow this two-stage process:
#### Stage A: The Internal Update

   1. Open GitHub Desktop and select the `ppls-app-internal` repository.
   2. Make your changes in the `docs/internal` folder.
   3. In GitHub Desktop, you will see your changes. **Commit** and **Push** them to the `main` branch.
   * *Note: Do not skip the "Push" step, or others won't see your updates.*
   
#### Stage B: The Public Sync

   1. Switch the repository in GitHub Desktop to `the-peoples-app` (the public one).
   2. You will see a "change" listed for the folder `docs/internal`. This is the **Pointer Update**.
   3. **Commit** this change with the summary: `sync internal docs`.
   4. **Push** to the origin.

------------------------------
### 3. Session Governance (Neovim/Tmux)
To avoid Git index corruption, **do not manage both repositories from the same terminal session.**

* **Public Session:** Root `ppls-app/`. Use for Code/ADRs.
* **Private Session:** Folder `docs/internal/`. Use for internal strategy.
* **Vim-Fugitive:** Only run `:G` commands within the session dedicated to that specific repository.

------------------------------
### 4. The `bin/hpush` Script Source

See the [Script Source Section] in the repository for the full bash code.

------------------------------
### 5. Environment Setup

* **Protocol:** Use `git -c protocol.file.allow=always` for local submodule additions.
* **Ignore Rules:** `.easignore` must include `docs/internal/` to keep strategy out of production builds.

------------------------------

> **Architect’s Note:** To avoid local desync, it is recommended to work exclusively within the `docs/internal` directory of the public project rather than maintaining a separate standalone clone of the internal repository. If using a standalone clone, you must `push` from the standalone and `pull` within the submodule to synchronize the local state.

