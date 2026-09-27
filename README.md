# NestJS Docker Boilerplate

Reusable NestJS starter with Docker development and multi-stage production builds.

## Versions

- NestJS 12.1.0 (latest stable `@nestjs/core` at repository creation)
- Nest CLI 12.0.7
- Node.js 24.21.0 Alpine (Node 24 LTS)
- TypeScript 5.9.x

Node 24 is the LTS branch used by this template. The Node project recommends Active LTS or Maintenance LTS for production applications.

## Docker development

```bash
git clone <repo-url>
cd nestjs-docker-boilerplate
docker compose up --build
```

Open http://localhost:4000.

The project source is bind-mounted into `/app`. `node_modules` is kept in a Docker named volume so Linux dependencies are not written into the Windows source directory.

Stop:

```bash
docker compose down
```

## Local development (without Docker)

Requires Node 24 LTS and npm.

```bash
npm install
npm run dev
```

Open http://localhost:3001.

Other scripts:

```bash
npm run build
npm start
npm run typecheck
```

## Production container

```bash
docker compose -f docker-compose.prod.yml up --build -d
```

Stop:

```bash
docker compose -f docker-compose.prod.yml down
```

## Project layout

```text
src/                     NestJS source
Dockerfile               development/build/production stages
docker-compose.yml       development
docker-compose.prod.yml  production
```

## Notes

- The development container listens on all interfaces (`0.0.0.0`) so Docker port publishing works.
- The production stage runs the compiled application as the non-root `node` user.
- If you run `npm install` locally, commit the generated `package-lock.json` for reproducible installs. The Dockerfile supports both a repository with and without a lockfile.
