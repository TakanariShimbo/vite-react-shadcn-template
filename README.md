# Ref

install tailwind to vite https://ui.shadcn.com/docs/installation/vite

install shadcn to vite https://ui.shadcn.com/docs/installation/vite

change theme of shadcn https://ui.shadcn.com/themes

# Memo

1. create vite

```sh
npm create vite@latest .
```

- choose react, ts + swc

2. install default libs

```sh
npm install
```

3. check site

```sh
npm run dev
```

4. install tailwinds

```sh
npm install -D tailwindcss postcss autoprefixer
```

5. init tailwind

```sh
npx tailwindcss init -p
```

6. add content to tailwind.config.js

```js:tailwind.config.js
/** @type {import('tailwindcss').Config} */
export default {
  content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"], // added
  theme: {
    extend: {},
  },
  plugins: [],
};
```

7. replace index.css

```css:src/index.css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

8. test tailwind

- remove src/asserts
- remove src/App.css
- replace src/App.tsx

```tsx:src/App.tsx
import React from "react";

type AppProps = {};

const App: React.FC<AppProps> = ({}: AppProps): JSX.Element => {
  return (
    <div className="flex justify-center flex-col items-center">
      <p className="p-24 text-3xl font-bold text-slate-900">HELLO WORLD</p>
    </div>
  );
};

export default App;
```

check site

```sh
npm run dev
```

9. add compilerOptions to tsconfig.json

```json:tsconfig.json
{
  // ...

  /* Shadcn */
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```

10. add compilerOptions to tsconfig.app.json

```json:tsconfig.app.json
{
  "compilerOptions": {
    // ...

    /* Shadcn */
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  },

  // ...
}
```

11. install @types/node

```sh
npm install -D @types/node
```

12. add resolve to vite.config.ts

```ts:vite.config.ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react-swc";
import path from "path"; // added

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],

  // added
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
});
```

13. init shadcn

```sh
npx shadcn-ui@latest init
```

- choose like blow

```
√ Would you like to use TypeScript (recommended)? ... yes
√ Which style would you like to use? » Default
√ Which color would you like to use as base color? » Slate
√ Where is your global CSS file? ... src/index.css
√ Would you like to use CSS variables for colors? ... yes
√ Are you using a custom tailwind prefix eg. tw-? (Leave blank if not) ...
√ Where is your tailwind.config.js located? ... tailwind.config.js
√ Configure the import alias for components: ... @/components
√ Configure the import alias for utils: ... @/lib/utils
√ Are you using React Server Components? ... no
√ Write configuration to components.json. Proceed? ... yes
```

14. test shadcn

```sh
npx shadcn-ui@latest add button
```

```tsx:src/App.tsx
import React, { useState } from "react";
import { Button } from "@/components/ui/button";

type AppProps = {};

const App: React.FC<AppProps> = ({}: AppProps): JSX.Element => {
  const [count, setCount] = useState<number>(0);

  return (
    <div className="flex justify-center flex-col items-center">
      <p className="p-24 text-3xl font-bold text-primary">HELLO WORLD</p>
      <Button onClick={() => setCount((prev) => prev + 1)}>Clicked {count} times</Button>
    </div>
  );
};

export default App;
```

check site

```sh
npm run dev
```
