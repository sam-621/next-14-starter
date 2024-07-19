# Lib

Lib folder works as the `internal library for the project`, here is where all my application modules belong to and also a `common` module

## Example

```
|-- lib
    |-- order
        |-- data
            |-- index.ts
        |-- actions
            |-- index.ts
        |-- components
            |-- server.ts
            |-- client.ts
    |-- customer
        |-- data
            |-- index.ts
        |-- actions
            |-- index.ts
        |-- components
            |-- server.ts
            |-- client.ts
    |-- common
        |-- hooks
            |-- index.ts
        |-- utils
            |-- index.ts
        |-- components
            |-- server.ts
            |-- client.ts
```

### why in components we got a `server.ts` and a `client.ts` instead of an `index.ts`?

We know that in Next.js 14 we got both server and client components, if we re export all of them in a single index.ts, problems will start to come, is I import a client component from a client component, Next will throw an error saying that you cannot import server components in client components and this is because we are importing our client component from the index file where also have server components re exporting

```ts
// /components/index.ts

// If some component import ones from this file, it will load every component
export * from 'server-component.tsx';
export * from 'client-component.tsx';
```

```ts
// some-other-client-component.tsx
'use client';

import { ClientComponent } from '@/lib/order/component'; // get client component but also load server component and throw an error

// ...
```
