# Async Tasks Queue

A simple and efficient async tasks queue for Node.js with TypeScript support.

## Installation

```bash
npm install async-tasks-queue
```

## Usage

### Basic Usage

```typescript
import AsyncTasksQueue from 'async-tasks-queue';

const queue = new AsyncTasksQueue();

// Add tasks to the queue
const task1 = queue.enqueue(async () => {
  await new Promise(resolve => setTimeout(resolve, 1000));
  return 'Task 1 completed';
});

const task2 = queue.enqueue(async () => {
  await new Promise(resolve => setTimeout(resolve, 500));
  return 'Task 2 completed';
});

// Tasks will be executed sequentially
const result1 = await task1; // Waits 1 second
const result2 = await task2; // Waits additional 0.5 seconds
```

### Usage with Error Handling

```typescript
import AsyncTasksQueue from 'async-tasks-queue';

const queue = new AsyncTasksQueue();

try {
  const result = await queue.enqueue(async () => {
    // Simulate an error
    throw new Error('Something went wrong');
  });
} catch (error) {
  console.error('Task error:', error.message);
}
```

### Example with Multiple Tasks

```typescript
import AsyncTasksQueue from 'async-tasks-queue';

const queue = new AsyncTasksQueue();

// Function simulating database operation
async function simulateDatabaseOperation(id: number): Promise<string> {
  await new Promise(resolve => setTimeout(resolve, Math.random() * 1000));
  return `Operation ${id} completed`;
}

// Add multiple tasks
const tasks = [];
for (let i = 1; i <= 5; i++) {
  tasks.push(queue.enqueue(() => simulateDatabaseOperation(i)));
}

// All tasks will be executed sequentially
const results = await Promise.all(tasks);
console.log(results);
// Output: ['Operation 1 completed', 'Operation 2 completed', ...]
```

## API

### `enqueue<T>(task: () => Promise<T>): Promise<T>`

Adds a task to the queue and returns a Promise that will be resolved when the task completes.

**Parameters:**
- `task`: Async function returning a Promise

**Returns:**
- Promise that will be resolved with the task result or rejected with an error

## Features

- **Sequential execution**: All tasks are executed one after another
- **Error handling**: Errors in tasks are properly propagated
- **TypeScript**: Full TypeScript type support
- **Lightweight**: Zero production dependencies
- **Simple**: Intuitive API without complex configuration

## Development

For developers working on this package, see [`docs/DEVELOPMENT.md`](docs/DEVELOPMENT.md) for detailed technical documentation, project structure, configuration details, and development workflow. This file serves as a comprehensive guide for AI assistants and developers working with the codebase.

## License

MIT 