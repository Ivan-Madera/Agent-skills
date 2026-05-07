---
name: node-ts-clean-sequelize-starter
description: Generate a production-ready Node.js + TypeScript + Express + Sequelize project using clean architecture, including migrations, seeders, testing, linting, docker, env validation, logging, and example endpoint.
---

# Node TS Clean Architecture + Sequelize

Generate a **production-ready backend** with:

- Node + TypeScript + Express
- Sequelize ORM (migrations + seeders)
- Clean Architecture
- Env validation (Joi)
- Logging (log4js)
- Testing (Jest)
- Linting (ESLint new config + Prettier)
- Docker
- Example endpoint across ALL layers

---

## Project Structure

```
src/
  config/
  infrastructure/
    database/
    http/
    logger/
  domain/
    entities/
    repositories/
  application/
    use-cases/
  interfaces/
    controllers/
    routes/
  shared/
    errors/
    utils/

tests/
  unit/
  integration/
```

## Core Components

### TS Config (aliases)

**`tsconfig.json`** with path aliases for clean imports:

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "CommonJS",
    "paths": {
      "@/*": ["./src/*"]
    },
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  },
  "include": ["src/**/*"]
}
```

### Sequelize Setup

**`.sequelizerc`** (Root folder configuration) points to the database configuration and migration paths.

**`src/infrastructure/database/database.js`** handles environment-specific database configuration.

**`src/infrastructure/database/sequelize.ts`** creates the application connection with Sequelize.

### Clean Architecture Layers

**Domain Entity:** Core business logic (interfaces/types)

**Use Case:** Application business logic

**Model (Sequelize TS):** ORM representation

**Repository:** Data access abstraction

**Controller:** HTTP request/response handling

**Route:** Express route definitions

### Configuration

**ENV + Config + Joi** for environment validation:

- `.env.example` with required variables
- `src/config/index.ts` with Joi schema validation

### Logging (log4js)

Structured logging with timestamps and log levels.

### Error Handler

Global error handler middleware for Express.

### Testing (Jest)

**jest.config.js** configured with TypeScript support via ts-jest.

### Linting

**ESLint (eslint.config.mjs)** with TypeScript rules and **Prettier** for code formatting.

### Docker

Dockerfile for containerization and docker-compose.yml for local development.

---

## When to use this skill

- Use this when you need to scaffold a new production-ready Node.js backend
- This is helpful for projects requiring clean architecture with TypeScript
- Use this to generate a complete starter with all enterprise patterns included
- This is ideal for teams that need database migrations, seeders, and comprehensive testing setup

## How to use it

### Init Project

```bash
npm init -y
npm install express sequelize sequelize-cli mysql2 joi log4js dotenv helmet cors
npm install -D typescript ts-node tsconfig-paths jest ts-jest @types/jest @types/node @types/express @types/cors eslint typescript-eslint prettier
```

### Package.json Scripts

```json
{
  "scripts": {
    "dev": "ts-node -r tsconfig-paths/register src/index.ts",
    "build": "tsc",
    "start": "node dist/index.js",
    "new:migration": "npx sequelize-cli migration:generate --name",
    "new:seeder": "npx sequelize-cli seed:generate --name",
    "migrate": "npx sequelize-cli db:migrate",
    "migrate:undo": "npx sequelize-cli db:migrate:undo",
    "seeder": "npx sequelize-cli db:seed:all",
    "seeder:undo": "npx sequelize-cli db:seed:undo:all",
    "lint": "eslint \"src/**/*.ts\" --fix",
    "test": "jest"
  }
}
```

### Sequelize Initialization

```bash
npx sequelize-cli init
```

Create example migration and seeder files in respective directories.

### App Initialization

Create express app with middleware (helmet, cors), health check endpoint, and error handler:

```typescript
import express from 'express';
import helmet from 'helmet';
import cors from 'cors';

const app = express();

app.use(helmet());
app.use(cors());
app.use(express.json());

app.get('/health', (_, res) => res.send('OK'));
app.listen(config.PORT);
```

### .gitignore Setup

```
node_modules
dist
.env
```

### Validation Step

After executing the skill, validate that the template starts up correctly:

1. Ensure `.env` is created from `.env.example`: `cp .env.example .env`
2. Run ESLint: `npm run lint`
3. Run the development server: `npm run dev`
4. Verify the console outputs that the server is running on port 3000

## Activation Triggers

- "create node clean architecture project"
- "scaffold backend ts sequelize"
- "init api pro"
