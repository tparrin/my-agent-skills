# Building Custom Activepieces Pieces

Activepieces boasts a highly extensible ecosystem where pieces are just TypeScript `npm` packages. Anyone can develop and publish them.

## Piece Architecture

A custom piece usually looks like this in source code:
```typescript
import { createPiece } from '@activepieces/pieces-framework';
import { customAction } from './actions/custom-action';
import { customTrigger } from './triggers/custom-trigger';

export const customPiece = createPiece({
  displayName: 'Custom Piece',
  auth: undefined, // Or define an OAuth2 / API Key connection schema
  minimumSupportedRelease: '0.20.0',
  logoUrl: 'https://cdn.example.com/logo.png',
  authors: ['username'],
  actions: [customAction],
  triggers: [customTrigger],
});
```

## Key Framework Abstractions

1. **Properties (`Property`)**: The schema for inputs a user provides in the UI. E.g., `Property.ShortText`, `Property.Dropdown`, `Property.OAuth2`.
2. **Actions (`createAction`)**: Functions that execute when called. They define an `auth` validation, `props` required, and an async `run` method holding the execution logic.
3. **Triggers (`createTrigger`)**: Define events. Two flavors:
   - Polling: `run` method periodically queries an API and compares against the last known state.
   - Webhook: Register `onEnable`, unregister `onDisable`, and process payload via `run`.

When a user asks you to write a piece, structure it around the `@activepieces/pieces-framework` libraries.
