# TeamBoard - Continuous Course Project

TeamBoard is the shared project that grows across all 5 days of the course. It is a minimal Kanban ticket system: a ticket has a title, description, assigned person, and status (`To Do` -> `In Progress` -> `Done`).

This folder holds the parts of TeamBoard that more than one module reuses. Individual project labs link only the files they need from here; not every exercise routes through this folder.

## How TeamBoard Grows

| After module | TeamBoard gains                                                            | Where it lives                                  |
| ------------ | -------------------------------------------------------------------------- | ----------------------------------------------- |
| m01          | Initial README/concept (Copilot-assisted draft)                            | `starter/README-draft.md`                       |
| m02          | Local Git repository with HTML skeleton                                    | participant-local, see `l02-local-repo-setup`   |
| m03          | GitHub remote, conflict merge locally, `README.md` merged via PR           | participant GitHub account                      |
| m04          | GitHub Actions lint/build workflow                                         | `checkpoints/day1-ci/.github/workflows/ci.yml`  |
| m05-m06      | Node.js + TypeScript backend scaffold                                      | `checkpoints/day2-ts-backend/`                  |
| m07-m08      | Typed `Ticket`/`Status` models, `TicketService`/`TicketRepository` classes | `checkpoints/day2-ts-backend/src/`              |
| m11-m13      | Dockerfile + `docker-compose.yml` (backend + MongoDB)                      | `checkpoints/day3-containerized/`               |
| m14-m16      | REST + GraphQL API, MongoDB-backed, JWT-secured                            | `checkpoints/day4-api-secured/`                 |
| m17          | Responsive Kanban layout (Bootstrap 5 + Sass + Gulp)                       | `checkpoints/day4-api-secured/frontend-static/` |
| m18-m19      | React SPA connected to the secured API                                     | `checkpoints/day5-react-spa/`                   |
| m22          | Final walkthrough state (no new code, presentation only)                   | `checkpoints/day5-react-spa/`                   |

## Folder Roles

- `starter/`: the deliberately incomplete state participants begin from on Day 1.
- `checkpoints/`: coherent, working snapshots at each day boundary, used as a recovery path if a participant falls behind. Each checkpoint only contains behavior participants have already learned up to that point.
- `contracts/`: participant-facing interface contracts (e.g., the `Ticket` REST/GraphQL shape) that stay stable once published, so later modules do not silently change an earlier agreement.

## Using a Checkpoint

If your local TeamBoard state does not match what a lab expects, copy the matching `checkpoints/dayN-*` folder into your working directory instead of debugging from scratch. Checkpoints are recovery points, not shortcuts around the exercises: complete the current lab's own tasks after restoring a checkpoint.
