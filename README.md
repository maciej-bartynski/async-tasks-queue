# Async Tasks Queue

Prosta i wydajna kolejka zadań asynchronicznych dla Node.js z obsługą TypeScript.

## Instalacja

```bash
npm install async-tasks-queue
```

## Użycie

### Podstawowe użycie

```typescript
import AsyncTasksQueue from 'async-tasks-queue';

const queue = new AsyncTasksQueue();

// Dodaj zadania do kolejki
const task1 = queue.enqueue(async () => {
  await new Promise(resolve => setTimeout(resolve, 1000));
  return 'Zadanie 1 ukończone';
});

const task2 = queue.enqueue(async () => {
  await new Promise(resolve => setTimeout(resolve, 500));
  return 'Zadanie 2 ukończone';
});

// Zadania będą wykonywane sekwencyjnie
const result1 = await task1; // Czeka 1 sekundę
const result2 = await task2; // Czeka dodatkowe 0.5 sekundy
```

### Użycie z obsługą błędów

```typescript
import AsyncTasksQueue from 'async-tasks-queue';

const queue = new AsyncTasksQueue();

try {
  const result = await queue.enqueue(async () => {
    // Symulacja błędu
    throw new Error('Coś poszło nie tak');
  });
} catch (error) {
  console.error('Błąd w zadaniu:', error.message);
}
```

### Przykład z wieloma zadaniami

```typescript
import AsyncTasksQueue from 'async-tasks-queue';

const queue = new AsyncTasksQueue();

// Funkcja symulująca pracę z bazą danych
async function simulateDatabaseOperation(id: number): Promise<string> {
  await new Promise(resolve => setTimeout(resolve, Math.random() * 1000));
  return `Operacja ${id} ukończona`;
}

// Dodaj wiele zadań
const tasks = [];
for (let i = 1; i <= 5; i++) {
  tasks.push(queue.enqueue(() => simulateDatabaseOperation(i)));
}

// Wszystkie zadania będą wykonywane sekwencyjnie
const results = await Promise.all(tasks);
console.log(results);
// Output: ['Operacja 1 ukończona', 'Operacja 2 ukończona', ...]
```

## API

### `enqueue<T>(task: () => Promise<T>): Promise<T>`

Dodaje zadanie do kolejki i zwraca Promise, który zostanie rozwiązany po ukończeniu zadania.

**Parametry:**
- `task`: Funkcja asynchroniczna zwracająca Promise

**Zwraca:**
- Promise, który zostanie rozwiązany z wynikiem zadania lub odrzucony z błędem

## Funkcje

- **Sekwencyjne wykonywanie**: Wszystkie zadania są wykonywane jeden po drugim
- **Obsługa błędów**: Błędy w zadaniach są prawidłowo propagowane
- **TypeScript**: Pełna obsługa typów TypeScript
- **Lekka**: Minimalne zależności, tylko `uuid` jako zależność produkcyjna
- **Prosta**: Intuicyjne API bez skomplikowanej konfiguracji

## Licencja

MIT 