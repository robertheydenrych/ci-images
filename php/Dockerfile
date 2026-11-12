# syntax=docker/dockerfile:1

# The image the PHP apps' CI jobs run in: the PHP the production Dockerfiles build on, with the things every job
# used to install itself already in it. Built and pushed to ghcr.io by .github/workflows/ci-php-image.yml.
#
#   gd, intl   compiled from source (intl is C++), so every job spent about two minutes on them. The same two extensions
#              the apps' production Dockerfiles add (gd for image sizes and PhpSpreadsheet, intl for Laravel's helpers).
#   Node 22    copied from the official image, as the apps' production Dockerfiles do for their build stage, instead of
#              actions/setup-node downloading it in each job.
#   git        for the jobs that need a checkout with history.
#
# The jobs still run with `options: --user root`, as before; nothing here changes who they run as.
FROM serversideup/php:8.5-cli

USER root

# Named by the build, so one Dockerfile makes both images: "gd intl" for ci-php (Goosie Lou), empty for ci-php-lean
# (Budgeter, whose production image has no extensions either).
ARG PHP_EXTENSIONS="gd intl"
RUN if [ -n "$PHP_EXTENSIONS" ]; then install-php-extensions $PHP_EXTENSIONS; fi

RUN apt-get update \
 && apt-get install -y --no-install-recommends git \
 && rm -rf /var/lib/apt/lists/*

COPY --from=node:22-slim /usr/local/bin/node /usr/local/bin/node
COPY --from=node:22-slim /usr/local/lib/node_modules /usr/local/lib/node_modules
RUN ln -s /usr/local/lib/node_modules/npm/bin/npm-cli.js /usr/local/bin/npm \
 && ln -s /usr/local/lib/node_modules/npm/bin/npx-cli.js /usr/local/bin/npx

USER www-data
