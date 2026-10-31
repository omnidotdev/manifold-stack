# Manifold

Universal artifact registry: one registry for OCI container images, npm
packages, Cargo crates, schemas (OpenAPI, GraphQL, JSON Schema), and WebAssembly
modules. Hosted at [manifold.omni.dev](https://manifold.omni.dev).

This is a metarepo. Each service is an independent repository under `services/`:

| Service | Description |
| --- | --- |
| [`manifold-api`](./services/manifold-api) | Bun/Elysia API: the OCI `/v2`, npm, and Cargo registry endpoints, plus a Postgraphile GraphQL API (Drizzle/Postgres) |
| [`manifold-app`](./services/manifold-app) | TanStack Start dashboard |
| [`manifold-core`](./services/manifold-core) | Rust core library (storage, digest, and registry primitives) |

## Self-hosting

The registry runs on Postgres plus the API and dashboard. Requirements: Docker
and Docker Compose.

```sh
cp .env.local.template .env.local   # then set DB_PASSWORD
docker compose up
```

The dashboard, the API, and Postgres start together. Auth and billing degrade
gracefully when their integrations are unset, so a self-host instance works
without them. See each service's README for configuration.

## Development

Local orchestration uses [Tilt](https://tilt.dev), which loads each service's
own `Tiltfile`:

```sh
tilt up
```

## License

Apache-2.0. See [LICENSE.md](./LICENSE.md).
