# Execution Control

This package contains two independent modules designed to enhance control over function execution in
JavaScript/TypeScript projects. It includes a decorator for managing single execution of functions and a class for
handling cancellation tokens.

## Installation

Install via npm:

```bash
npm install execution-control
```

## Modules

### 1. SingleCall Decorator

This decorator ensures that a function can only be called once at a time for a given instance. If the function is
already in progress, the same promise is returned instead of invoking the function again.

#### Usage

```typescript
import { SingleCall } from 'execution-control/single-call';

class Example {
	@SingleCall
	async fetchData() {
		// Your logic here
	}
}
```

In this example, multiple calls to `fetchData()` while a promise is pending will all return the same promise.

### 2. CancellationToken Class

The `CancellationToken` class provides a mechanism to manage and verify cancellation tokens in asynchronous processes.

#### Usage

```typescript
import { CancellationToken } from 'execution-control/cancelation-token';

const token = new CancellationToken();

async function fetchData() {
	const id = token.reset();

	// Perform some operation
	if (!token.check(id)) {
		// Handle cancellation
	}
}
```

The `reset()` method generates a new token, while `check(id)` verifies if the current operation is still valid based on
the last token.

## Module Overview

-   **SingleCall**: Prevents simultaneous calls to the same function, returning the first in-progress promise for
    subsequent calls.
-   **CancellationToken**: Provides a way to control and cancel long-running or asynchronous operations.

## License

This project is licensed under the MIT License.
