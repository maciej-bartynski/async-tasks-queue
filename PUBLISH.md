# Instrukcje publikacji paczki npm

## Przygotowanie do publikacji

1. **Zaloguj się do npm** (jeśli nie masz konta, utwórz je na npmjs.com):
   ```bash
   npm login
   ```

2. **Sprawdź czy wszystko jest gotowe**:
   ```bash
   npm run build
   npm test
   npm pack
   ```

3. **Zaktualizuj wersję** (jeśli potrzebne):
   ```bash
   npm version patch  # 1.0.0 -> 1.0.1
   npm version minor  # 1.0.0 -> 1.1.0
   npm version major  # 1.0.0 -> 2.0.0
   ```

## Publikacja

### Pierwsza publikacja
```bash
npm publish
```

### Aktualizacja istniejącej paczki
```bash
npm publish
```

### Publikacja z tagiem (np. beta)
```bash
npm publish --tag beta
```

## Sprawdzenie po publikacji

1. **Sprawdź czy paczka jest dostępna**:
   ```bash
   npm view async-tasks-queue
   ```

2. **Przetestuj instalację**:
   ```bash
   npm install async-tasks-queue
   ```

3. **Sprawdź na stronie npm**:
   https://www.npmjs.com/package/async-tasks-queue

## Ważne uwagi

- Upewnij się, że nazwa paczki `async-tasks-queue` jest dostępna na npm
- Sprawdź czy wszystkie pliki są włączone w paczkę (sprawdź `.npmignore`)
- Upewnij się, że testy przechodzą przed publikacją
- Zaktualizuj `package.json` z właściwymi danymi autora i repozytorium

## Struktura paczki

Paczka zawiera:
- `dist/` - skompilowane pliki JavaScript i deklaracje TypeScript
- `README.md` - dokumentacja
- `package.json` - metadane paczki

Pliki wykluczone:
- `src/` - pliki źródłowe TypeScript
- `tests/` - pliki testów
- `tsconfig.json`, `jest.config.js` - pliki konfiguracyjne
- `node_modules/` - zależności 