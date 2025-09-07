# TS quick start

# Table of contents

- [TS quick start](#ts-quick-start)
- [Table of contents](#table-of-contents)
  - [1. Setup typescript environment](#1-setup-typescript-environment)
    - [1.1. Install typescript](#11-install-typescript)
    - [1.2. Create TS project](#12-create-ts-project)
    - [1.3. Compile TS to JS](#13-compile-ts-to-js)
    - [1.4. Project TS file structure](#14-project-ts-file-structure)
    - [1.5. Basic typescript configuration](#15-basic-typescript-configuration)
      - [1.5.1. `package.json`](#151-packagejson)
      - [1.5.2. `tsconfig.json`](#152-tsconfigjson)
      - [1.5.3. `eslintrc.json`](#153-eslintrcjson)
      - [1.5.4. `.prettierrc.json`](#154-prettierrcjson)
      - [1.5.5. `jest.config.json`](#155-jestconfigjson)
      - [1.5.6. `.gitignore`](#156-gitignore)

## 1. Setup typescript environment

### 1.1. Install typescript

- First you need `NodeJS`. You download nodejs <a href="https://nodejs.org/en/download">here</a>
- Then open terminal and run:

```bash
    # typescript install + dev tools
    npm install --save-dev typescript ts-node-dev @types/node
```

- `typescript`: compiler (tsc)
- `ts-node-dev`: run file .ts directly (hot reload)
- `@types/node`: type definitions for Node.js

```bash
    # Check version:
    tsc -v
```

### 1.2. Create TS project

Create `NodeJS` first and TS configuration

```bash
    npm init -y # create default package.json

    npx tsc --init # create tsconfig.json
```

Create `Typescript` file `script.ts`

```typescript
function greet(): string {
  return "Hello World!";
}

console.log(greet());
```

### 1.3. Compile TS to JS

```bash
    # Compile
    tsc script.ts

    # Automatically compile when changing
    tsc --watch
```

### 1.4. Project TS file structure

```perl
    my-project/
    ├── src/                    # main source
    │   ├── index.ts            # entry point
    │   ├── config/             # config (env, db, api)
    │   ├── controllers/        # logic manipulate request
    │   ├── routes/             # route (REST API, GraphQL,…)
    │   ├── models/             # interface, type, class
    │   ├── services/           # business logic
    │   ├── utils/              # utilities
    │   └── middlewares/        # middleware (Express, Koa,…)
    │
    ├── dist/               # build folder (file .js)
    ├── tests/              # test (unit, integration)
    │
    ├── package.json        # project information (npm)
    ├── tsconfig.json       # typescript configuration
    ├── .eslintrc.js        # linting configuration
    ├── .prettierrc         # format code configuration
    └── README.md
```

### 1.5. Basic typescript configuration

#### 1.5.1. `package.json`

- Usage:

  - Save name, version of project
  - Dependencies management (library that is installed by `npm install`)
  - Definition of scripts (build, start, test, ...)

- Key fields:

  - `"name"`: project name (used if you publish to npm).
  - `"version"`: project version (major.minor.patch).
  - `"scripts"`: shortcuts you run with `npm run <script>`

- Standard `package.json` configuration

```json
{
  "name": "my-ts-app",
  "version": "1.0.0",
  "description": "A TypeScript project template",
  "main": "dist/index.js",
  "scripts": {
    "start": "node dist/index.js",
    "build": "tsc",
    "dev": "ts-node-dev --respawn --transpile-only src/index.ts",
    "lint": "eslint 'src/**/*.{ts,tsx}'",
    "format": "prettier --write 'src/**/*.{ts,tsx,json,md}'",
    "test": "jest"
  },
  "dependencies": {
    "express": "^4.19.0"
  },
  "devDependencies": {
    "@types/express": "^4.17.21",
    "@typescript-eslint/eslint-plugin": "^8.0.0",
    "@typescript-eslint/parser": "^8.0.0",
    "eslint": "^9.0.0",
    "jest": "^29.7.0",
    "prettier": "^3.3.0",
    "ts-jest": "^29.2.0",
    "ts-node-dev": "^2.0.0",
    "typescript": "^5.6.0"
  },
  "engines": {
    "node": ">=18.0.0"
  }
}
```

- `"dependencies"`: runtime libraries (needed in production).
- `"devDependencies"`: development-only tools (TypeScript compiler, linters, test frameworks, …).

#### 1.5.2. `tsconfig.json`

- Controls how the TypeScript compiler (tsc) works. This is the most important config file in a TS project.

- Common compilerOptions:
  - `"target"`: JavaScript version output (ES5, ES2015, ES2020, …).
  - `"module"`: module system (CommonJS for Node.js, ESNext for frontend).
  - `"rootDir"`: source folder (usually src).
  - `"outDir"`: compiled output folder (usually dist).
  - `"strict"`: enable strict type-checking (fewer bugs).
  - `"esModuleInterop"`: allows clean imports for older JS libraries.

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "CommonJS",
    "moduleResolution": "Node",
    "rootDir": "src",
    "outDir": "dist",
    "strict": true,
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "skipLibCheck": true,
    "resolveJsonModule": true,
    "allowSyntheticDefaultImports": true,
    "sourceMap": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist", "tests"]
}
```

#### 1.5.3. `eslintrc.json`

- Used for linting (checking code style and possible logic errors).
- Key fields:
  - `"extends"`: base rule sets (e.g., eslint:recommended).
  - `"parser"`: parser (for TS use @typescript-eslint/parser).
  - `"plugins"`: additional rules (e.g., TypeScript-specific).
  - `"rules"`: custom rules you define.

```json
{
  "root": true,
  "env": {
    "es2020": true,
    "node": true,
    "jest": true
  },
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaVersion": 2020,
    "sourceType": "module"
  },
  "plugins": ["@typescript-eslint"],
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "prettier"
  ],
  "rules": {
    "no-console": "warn",
    "semi": ["error", "always"],
    "quotes": ["error", "double"]
  }
}
```

#### 1.5.4. `.prettierrc.json`

Used for automatic code formatting (semicolons, spaces, line width, etc.).

```json
{
  "semi": true,
  "singleQuote": false,
  "tabWidth": 2,
  "trailingComma": "es5",
  "printWidth": 100,
  "endOfLine": "auto"
}
```

#### 1.5.5. `jest.config.json`

Config for Jest (testing framework).

```json
{
  "preset": "ts-jest",
  "testEnvironment": "node",
  "roots": ["<rootDir>/tests"],
  "moduleFileExtensions": ["ts", "js", "json"],
  "transform": {
    "^.+\\.ts$": "ts-jest"
  }
}
```

#### 1.5.6. `.gitignore`

tells Git which files/folders to ignore (node_modules, dist, …).

```bash
    # Node
    node_modules/
    dist/
    .env

    # Logs
    logs/
    *.log

    # Tests
    coverage/

    # Editor
    .vscode/
    .idea/
```
