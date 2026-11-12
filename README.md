# ci-images

The container image the author's PHP/Laravel CI jobs run in: `ghcr.io/robertheydenrych/ci-php`.

It is `serversideup/php:8.5-cli` with the `gd` and `intl` extensions, Node 22, npm and git already installed, so CI jobs
don't compile or download them on every run. See [php/Dockerfile](php/Dockerfile).

Tags are `YYYYMMDD-<short sha>` (pin one) and `latest`. A workflow rebuilds the image when the Dockerfile changes and
every Monday.
