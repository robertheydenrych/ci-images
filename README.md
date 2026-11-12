# ci-images

The container images the author's PHP/Laravel CI jobs run in. Both are `serversideup/php:8.5-cli` with Node 22, npm and
git already installed, so CI jobs don't compile or download them on every run. See [php/Dockerfile](php/Dockerfile).

| Image | Extra PHP extensions |
|---|---|
| `ghcr.io/robertheydenrych/ci-php` | `gd`, `intl` |
| `ghcr.io/robertheydenrych/ci-php-lean` | none |
| `ghcr.io/robertheydenrych/ci-php-gd` | `gd` |

Tags are `YYYYMMDD-<short sha>` (pin one) and `latest`. A workflow builds both when the Dockerfile changes and every
Monday, and checks what is in each before pushing it.
