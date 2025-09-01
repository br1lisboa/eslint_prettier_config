# 🚀 Configuración ESLint + Prettier para Organizar Imports

Configuración completa para organizar automáticamente los imports en proyectos React, React Native y Next.js.

## 📦 Instalación

### 1. Instalar dependencias

```bash
# Con npm
npm install --save-dev eslint-plugin-import prettier-plugin-organize-imports

# Con yarn
yarn add -D eslint-plugin-import prettier-plugin-organize-imports

# Con pnpm
pnpm add -D eslint-plugin-import prettier-plugin-organize-imports
```

### 2. Instalar dependencias base (si no las tienes)

```bash
# Con npm
npm install --save-dev eslint prettier

# Con yarn
yarn add -D eslint prettier

# Con pnpm
pnpm add -D eslint prettier
```

## ⚙️ Configuración

### 1. Archivo `.eslintrc.js`

```javascript
module.exports = {
    extends: [
        'eslint:recommended',
        '@typescript-eslint/recommended', // Si usas TypeScript
    ],
    plugins: ['import'],
    rules: {
        'import/order': [
            'error',
            {
                groups: [
                    'builtin', // Node.js built-in modules
                    'external', // npm packages
                    'internal', // imports from within the project
                    'parent', // imports from parent directory
                    'sibling', // imports from same directory
                    'index', // imports from index file
                ],
                'newlines-between': 'always',
                alphabetize: {
                    order: 'asc',
                    caseInsensitive: true,
                },
            },
        ],
    },
};
```

### 2. Archivo `.prettierrc`

```json
{
    "semi": true,
    "trailingComma": "es5",
    "singleQuote": true,
    "printWidth": 80,
    "tabWidth": 2,
    "plugins": ["prettier-plugin-organize-imports"]
}
```

### 3. Archivo `.prettierignore`

```
node_modules
dist
build
.next
.vercel
coverage
```

## 🔧 Configuración VS Code

### 1. Instalar extensiones

-   ESLint (`dbaeumer.vscode-eslint`)
-   Prettier (`esbenp.prettier-vscode`)

### 2. Configuración en `settings.json`

```json
{
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true,
        "source.organizeImports": true
    },
    "eslint.validate": ["javascript", "javascriptreact", "typescript", "typescriptreact"]
}
```

## 📱 Configuración específica por proyecto

### React Native

```javascript
// .eslintrc.js
module.exports = {
    extends: ['@react-native', 'eslint:recommended'],
    plugins: ['import'],
    rules: {
        'import/order': [
            'error',
            {
                groups: ['builtin', 'external', 'internal', 'parent', 'sibling', 'index'],
                'newlines-between': 'always',
                alphabetize: {
                    order: 'asc',
                    caseInsensitive: true,
                },
            },
        ],
    },
};
```

### Next.js

```javascript
// .eslintrc.js
module.exports = {
    extends: ['next/core-web-vitals', 'eslint:recommended'],
    plugins: ['import'],
    rules: {
        'import/order': [
            'error',
            {
                groups: ['builtin', 'external', 'internal', 'parent', 'sibling', 'index'],
                'newlines-between': 'always',
                alphabetize: {
                    order: 'asc',
                    caseInsensitive: true,
                },
            },
        ],
    },
};
```

## 🎯 Scripts de package.json

```json
{
    "scripts": {
        "lint": "eslint . --ext .js,.jsx,.ts,.tsx",
        "lint:fix": "eslint . --ext .js,.jsx,.ts,.tsx --fix",
        "format": "prettier --write .",
        "format:check": "prettier --check ."
    }
}
```

## 🚀 Uso

### Formatear al guardar (automático)

-   Simplemente guarda tu archivo (Ctrl+S / Cmd+S)
-   Los imports se organizarán automáticamente

### Formatear manualmente

```bash
# Formatear todos los archivos
npm run format

# Verificar formato sin cambiar
npm run format:check

# Lintear y arreglar
npm run lint:fix
```

## 📋 Versiones utilizadas

```json
{
    "devDependencies": {
        "eslint": "^8.57.1",
        "eslint-plugin-import": "^2.29.1",
        "prettier": "^2.8.8",
        "prettier-plugin-organize-imports": "^3.2.4"
    }
}
```

## ✨ Resultado

Antes:

```typescript
import { useState } from 'react';
import React from 'react';

import { Button } from '@/components';

import './styles.css';
```

Después:

```typescript
import React from 'react';
import { useState } from 'react';

import { Button } from '@/components';

import './styles.css';
```

## 🔍 Troubleshooting

### Error: "Cannot find module 'prettier/plugins/babel'"

-   Usa `prettier-plugin-organize-imports` en lugar de `@trivago/prettier-plugin-sort-imports`
-   Es más estable y compatible

### Los imports no se organizan

-   Verifica que tengas `"editor.formatOnSave": true` en VS Code
-   Asegúrate de que Prettier sea el formateador por defecto
-   Reinicia VS Code después de instalar las extensiones

### Conflictos con ESLint

-   El plugin de import de ESLint se encarga del orden
-   Prettier se encarga del formato
-   Ambos trabajan en armonía

## 📚 Recursos adicionales

-   [ESLint Import Plugin](https://github.com/import-js/eslint-plugin-import)
-   [Prettier Plugin Organize Imports](https://github.com/simonhaenisch/prettier-plugin-organize-imports)
-   [VS Code ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
-   [VS Code Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
