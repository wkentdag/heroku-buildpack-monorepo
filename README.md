
# Heroku Monorepo Buildpack

**Heroku Monorepo Buildpack** is a buildpack designed to streamline deploying monorepos with multiple apps on Heroku. This buildpack dynamically sets the build and start commands for specified subdirectories in your monorepo, enabling flexible, multi-app deployments.

## Features

- Supports deploying specific apps within a monorepo to Heroku without copying files.
- Dynamically adjusts `build` and `start` scripts based on environment variables.
- Compatible with `pnpm` for efficient monorepo dependency management.

## Prerequisites

- **Node.js**: Ensure your project’s `package.json` specifies a Node.js version compatible with Heroku (e.g., `20.x`).
- **pnpm**: Recommended for efficient dependency management in monorepos.
- **Heroku CLI**: Install the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli) to interact with your Heroku apps.

## Example of Monorepo Directory Structure

Here’s the recommended structure for the monorepo:

```plaintext
monorepo-root/
├── apps/
│   ├── website/
│   │   ├── package.json
│   │   ├── src/
│   │   └── ...
│   ├── api/
│   │   ├── package.json
│   │   ├── src/
│   │   └── ...
├── packages/
│   ├── ui/
│   │   ├── package.json
│   │   ├── src/
│   │   └── ...
│   └── shared-utils/
│       ├── package.json
│       ├── src/
│       └── ...
├── pnpm-workspace.yaml
├── package.json
└── README.md
```

### Example Configuration for Each App
#### `apps/website/package.json`

```json
{
  "name": "@monorepo/website",
  "version": "1.0.0",
  "scripts": {
    "build": "next build",
    "start": "next start"
  }
}
```

#### `apps/api/package.json`

```json
{
  "name": "@monorepo/api",
  "version": "1.0.0",
  "scripts": {
    "build": "tsc",
    "start": "node dist/index.js"
  }
}
```

## Installation

#### 1. Add Buildpack

Add the `heroku-buildpack-monorepo` repository as a buildpack for your Heroku app. Use the Heroku CLI:

```bash
heroku buildpacks:add https://github.com/leanhub-co/heroku-buildpack-monorepo -a <your-app-name>
```

Ensure the order of buildpacks is correct and it's always in first place.


#### 2. Set Environment Variables

**APP_FILTER**: Define the app directory to build and start in the monorepo (e.g., `@monorepo/website` or `@monorepo/api`).

   ```bash
   heroku config:set APP_FILTER=@monorepo/website -a <your-app-name>
   ```

or with Heroku dashboard you can config both like this :

![Screenshot](https://github.com/user-attachments/assets/b3ee5903-6272-4141-800f-34a068330366)


## License

This project is licensed under the MIT License. See the [LICENSE](https://github.com/leanhub-co/heroku-buildpack-monorepo/blob/main/LICENSE) file for details.

### About LeanHub
##### Created by developers, for developers, [LeanHub](https://leanhub.co)
