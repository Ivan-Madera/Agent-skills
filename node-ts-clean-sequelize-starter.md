---
name: node-ts-clean-sequelize-starter
description: Generate a production-ready Node.js + TypeScript + Express + Sequelize project using clean architecture, including migrations, seeders, testing, linting, docker, env validation, logging, and example endpoint.
---

# 🚀 Node TS Clean Architecture + Sequelize (SR Skill)

## 🎯 Goal

Scaffold a **production-ready backend** with:

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

## 📁 Project Structure

``` id="3g7b5o"
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
### ⚙️ Init Project

```bash
npm init -y
npm install express sequelize sequelize-cli mysql2 joi log4js dotenv helmet cors
npm install -D typescript ts-node tsconfig-paths jest ts-jest @types/jest @types/node @types/express @types/cors eslint typescript-eslint prettier
```

### ⚙️ TS Config (aliases)

**`tsconfig.json`**
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

### 📦 package.json scripts

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

### 🗂 Sequelize Setup

**`.sequelizerc`** (Root folder configuration)
```javascript
const path = require('path');

module.exports = {
  'config': path.resolve('src', 'infrastructure', 'database', 'database.js'),
  'models-path': path.resolve('src', 'infrastructure', 'database', 'models'),
  'seeders-path': path.resolve('src', 'infrastructure', 'database', 'seeders'),
  'migrations-path': path.resolve('src', 'infrastructure', 'database', 'migrations')
};
```

**`src/infrastructure/database/database.js`** (For CLI usage)
```javascript
require('dotenv').config();

module.exports = {
  development: {
    username: process.env.DB_USER,
    password: process.env.DB_PASS,
    database: process.env.DB_NAME,
    host: process.env.DB_HOST,
    dialect: 'mysql'
  },
  production: {
    // production config...
  }
};
```

**`src/infrastructure/database/sequelize.ts`** (Application connection)
```typescript
import { Sequelize } from 'sequelize';
import { config } from '@/config';

export const sequelize = new Sequelize(
  config.DATABASE.DB_NAME,
  config.DATABASE.DB_USER,
  config.DATABASE.DB_PASS,
  {
    host: config.DATABASE.DB_HOST,
    dialect: 'mysql',
    logging: false,
  }
);
```

Run initialization (if not creating folders manually):
```bash
npx sequelize-cli init
```

#### Example Migration (`src/infrastructure/database/migrations/...`)

```javascript
'use strict';

module.exports = {
  async up(queryInterface, Sequelize) {
    await queryInterface.createTable('users', {
      id: { type: Sequelize.INTEGER, primaryKey: true, autoIncrement: true },
      name: Sequelize.STRING,
      createdAt: Sequelize.DATE,
      updatedAt: Sequelize.DATE
    });
  },
  async down(queryInterface) {
    await queryInterface.dropTable('users');
  }
};
```

#### Example Seeder (`src/infrastructure/database/seeders/...`)

```javascript
'use strict';

module.exports = {
  async up(queryInterface) {
    await queryInterface.bulkInsert('users', [
      { name: 'Ivan', createdAt: new Date(), updatedAt: new Date() }
    ]);
  },
  async down(queryInterface) {
    await queryInterface.bulkDelete('users', null, {});
  }
};
```

### 🔐 ENV + Config + Joi

**.env.example**
```env
PORT=3000
DB_HOST=localhost
DB_USER=root
DB_PASS=password
DB_NAME=test
NODE_ENV=development
```

**`src/config/index.ts`**
```typescript
import Joi from 'joi';
import dotenv from 'dotenv';

dotenv.config();

export interface EnvConfig {
  ENV: string;
  PORT: number;
  DATABASE: {
    DB_NAME: string;
    DB_USER: string;
    DB_PASS: string;
    DB_HOST: string;
  };
}

const schema = Joi.object({
  NODE_ENV: Joi.string().valid('development', 'production').default('development'),
  PORT: Joi.number().default(3000),
  DB_NAME: Joi.string().default('test'),
  DB_USER: Joi.string().default('root'),
  DB_PASS: Joi.string().default('password'),
  DB_HOST: Joi.string().default('localhost')
})
  .unknown()
  .required();

const { error, value: envVars } = schema.validate(process.env, {
  abortEarly: false,
  convert: true
});

if (error) {
  throw new Error(`Error en la configuración de las variables de entorno: \n${error.message}`);
}

export const config: EnvConfig = {
  ENV: envVars.NODE_ENV,
  PORT: envVars.PORT,
  DATABASE: {
    DB_NAME: envVars.DB_NAME,
    DB_USER: envVars.DB_USER,
    DB_PASS: envVars.DB_PASS,
    DB_HOST: envVars.DB_HOST
  }
};
```

### 🪵 Logger (log4js)

```typescript
import { configure, getLogger } from 'log4js';

configure({
  appenders: {
    stdout: {
      type: 'stdout',
      layout: {
        type: 'pattern',
        pattern: '%[[%x{time}] - [%p] | %m %]',
        tokens: {
          time: () => new Date().toLocaleString('es-MX', { hour12: false })
        }
      }
    }
  },
  categories: { default: { appenders: ['stdout'], level: 'debug' } }
});

export const logger = getLogger();
```

### 🧠 Clean Architecture Example

#### Domain Entity

```typescript
export interface User {
  id: number;
  name: string;
}
```

#### Use Case

```typescript
export class GetUsers {
  constructor(private repo: any) {}

  execute() {
    return this.repo.findAll();
  }
}
```

#### Model (Sequelize TS)

**`src/infrastructure/database/models/User.ts`**
```typescript
import { DataTypes, Model } from 'sequelize';
import { sequelize } from '../sequelize';

export class UserModel extends Model {
  public id!: number;
  public name!: string;
}

UserModel.init(
  {
    id: { type: DataTypes.INTEGER, autoIncrement: true, primaryKey: true },
    name: { type: DataTypes.STRING, allowNull: false },
  },
  { sequelize, tableName: 'users' }
);
```

#### Repository (Sequelize)

**`src/infrastructure/database/user.repository.ts`**
```typescript
import { UserModel } from './models/User';

export class UserRepository {
  async findAll() {
    return UserModel.findAll();
  }
}
```

#### Controller

```typescript
import { Request, Response } from 'express';

export class UserController {
  constructor(private useCase: any) {}

  async get(req: Request, res: Response) {
    const data = await this.useCase.execute();
    res.json({ success: true, data });
  }
}
```

#### Route

```typescript
import { Router } from 'express';

export const userRoutes = (controller: any) => {
  const router = Router();
  router.get('/users', controller.get.bind(controller));
  return router;
};
```

### 🌐 App Init

```typescript
import express from 'express';
import helmet from 'helmet';
import cors from 'cors';
import { config } from '@/config';
import { userRoutes } from '@/interfaces/routes/user.routes';

const app = express();

app.use(helmet());
app.use(cors());
app.use(express.json());

app.get('/health', (_, res) => res.send('OK'));

app.use(userRoutes(/* inject controller */));

app.listen(config.PORT);
```

### ❌ Error Handler

```typescript
import { Request, Response, NextFunction } from 'express';

export const errorHandler = (err: any, req: Request, res: Response, _next: NextFunction) => {
  res.status(500).json({ success: false, message: err.message });
};
```

### 🧪 Jest

**jest.config.js**
```javascript
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'node'
};
```

### 🎨 ESLint (eslint.config.mjs)

```javascript
import tseslint from 'typescript-eslint';

export default tseslint.config(
  ...tseslint.configs.recommended,
  {
    files: ['**/*.ts'],
    rules: {
      semi: ['error', 'always'],
      '@typescript-eslint/no-explicit-any': 'off',
      '@typescript-eslint/no-unused-vars': ['error', { argsIgnorePattern: '^_' }]
    }
  }
);
```

### 💅 Prettier

**.prettierrc**
```json
{
  "semi": true,
  "trailingComma": "all",
  "singleQuote": true,
  "printWidth": 120,
  "tabWidth": 2
}
```

### 🐳 Docker

**Dockerfile**
```dockerfile
FROM node:20
WORKDIR /app
COPY . .
RUN npm install
CMD ["npm", "run", "dev"]
```

**docker-compose.yml**
```yaml
version: '3'
services:
  app:
    build: .
    ports:
      - "3000:3000"
```

**.dockerignore**
```
node_modules
dist
```

### 📁 .gitignore

```
node_modules
dist
.env
```

### 📄 README.md

```markdown
# my-repo
```

### ✅ Validation Step

After executing the skill, validate that the template starts up correctly:

1. Ensure `.env` is created from `.env.example`:
   ```bash
   cp .env.example .env
   ```
2. Run ESLint:
   ```bash
   npm run lint
   ```
3. Run the development server:
   ```bash
   npm run dev
   ```
4. Verify the console outputs that the server is running on port 3000.

### 🧠 Activation

```text
"create node clean architecture project"
"scaffold backend ts sequelize"
"init api pro"
```

---
