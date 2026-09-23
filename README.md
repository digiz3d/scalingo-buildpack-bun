# Scalingo Buildpack for Bun

Installs a pinned Bun runtime and builds Bun applications on Scalingo.

## Usage

Set the following environment variable on the Scalingo application:

```text
BUILDPACK_URL=https://github.com/digiz3d/scalingo-buildpack-bun
```

Pin the buildpack URL to a tag or commit for reproducible deployments.

The application must contain:

- A `package.json` file with a `start` script.
- A `.bun-version` file containing an exact version such as `1.4.2`.

A `Procfile` is optional. Without one, the buildpack starts the application with:

```text
/app/bin/bun run start
```

## Build

The buildpack:

1. Installs the pinned Bun version into `/app/bin`.
2. Runs `bun install --frozen-lockfile` with Scalingo's persistent build cache.
3. Runs `bun run --if-present build`.

Any failed installation or build command fails the deployment.
