# Async Tasks Queue - AI Development Guide

## Package Overview

**async-tasks-queue** is a TypeScript npm package that provides a simple and efficient sequential task queue for Node.js. It ensures that async tasks are executed one after another, regardless of when they are enqueued.

### Core Functionality
- **Sequential Execution**: All tasks are processed in the order they were added
- **Promise-based**: Returns promises that resolve with task results
- **Error Handling**: Properly propagates errors from failed tasks
- **TypeScript Support**: Full type definitions included

## Project Structure

```
async-tasks-queue/
├── src/
│   └── AsyncTasksQueue.ts     # Main class implementation
├── tests/
│   └── AsyncQueue.test.ts     # Comprehensive test suite
├── dist/                      # Compiled JavaScript + type definitions
├── index.ts                   # Main export file
├── package.json               # NPM package configuration
├── tsconfig.json              # TypeScript config (development + tests)
├── tsconfig.build.json        # TypeScript config (production build)
├── jest.config.js             # Jest test configuration
└── README.md                  # User documentation
```

## Configuration Files

### TypeScript Configuration

**tsconfig.json** (Development + Tests):
- Includes both `src/` and `tests/` directories
- Enables path aliases: `@/*` → `src/*`, `@tests/*` → `tests/*`
- Generates source maps and declaration maps
- Strict type checking enabled

**tsconfig.build.json** (Production Build):
- Excludes `tests/` directory
- Only compiles source code for npm package
- Used by `npm run build` command

### Jest Configuration

**jest.config.js**:
- Uses `ts-jest` for TypeScript support
- Maps path aliases for tests: `@/` → `src/`
- Node.js test environment

## Available Commands

### Development Commands
```bash
npm run dev          # Run tests in watch mode
npm test             # Run tests once
npm run build        # Compile TypeScript to dist/
```

### Publishing Commands
```bash
npm run prepublishOnly  # Auto-runs before npm publish
npm pack               # Create local package for testing
npm publish            # Publish to npm registry
```

## Working with the Package

### For AI Assistants

**When modifying the source code:**
1. **Location**: All source code is in `src/AsyncTasksQueue.ts`
2. **Exports**: Main export is in `index.ts`
3. **Testing**: Always run `npm test` after changes
4. **Building**: Use `npm run build` to compile changes

**When adding new features:**
1. **Implementation**: Add to `src/AsyncTasksQueue.ts`
2. **Tests**: Add corresponding tests in `tests/AsyncQueue.test.ts`
3. **Types**: Ensure TypeScript types are properly defined
4. **Documentation**: Update `README.md` if API changes

**When fixing bugs:**
1. **Reproduce**: Create test case in `tests/AsyncQueue.test.ts`
2. **Fix**: Modify `src/AsyncTasksQueue.ts`
3. **Verify**: Run `npm test` to ensure all tests pass
4. **Build**: Run `npm run build` to compile

### Key Implementation Details

**AsyncTasksQueue Class:**
- **Private queue**: Array of task objects with resolve/reject functions
- **Private processing**: Boolean flag to prevent concurrent processing
- **enqueue()**: Adds task to queue and triggers processing
- **process()**: Sequential task execution loop

**Path Aliases:**
- `@/AsyncTasksQueue` → `src/AsyncTasksQueue.ts`
- `@tests/*` → `tests/*`
- Configured in both TypeScript and Jest

**Test Strategy:**
- Tests verify sequential execution order
- Tests check queue state management
- Tests validate timing (tasks execute in sequence, not parallel)
- Tests cover error handling scenarios

## Package Publishing Workflow

1. **Development**: Make changes in `src/`
2. **Testing**: Run `npm test` to verify functionality
3. **Building**: Run `npm run build` to compile to `dist/`
4. **Packaging**: Run `npm pack` to test package contents
5. **Publishing**: Run `npm publish` to release

## Important Notes for AI

- **Always test changes**: The test suite is comprehensive and catches edge cases
- **Maintain backward compatibility**: This is a utility library used by other projects
- **Follow TypeScript best practices**: Use strict typing and proper error handling
- **Keep it simple**: The package should remain lightweight and focused
- **Documentation**: Update README.md for any API changes

## Dependencies

**Production**: Zero dependencies (completely self-contained)
**Development**: TypeScript, Jest, ts-jest, type definitions

The package is designed to be lightweight with zero production dependencies for maximum compatibility and minimal footprint.