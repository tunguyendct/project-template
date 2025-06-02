# ⚙️ Project Setup Guide (Manual Configuration)

This guide walks you through configuring a project with:

- **Prettier** for code formatting
- **Husky** to run checks before commits
- **lint-staged** to format/lint staged files only
- **@ianvs/prettier-plugin-sort-imports** to sort import declarations by provided Regular Expression order

---


### ✅ Step 1: Install dependencies

```javascript
npm install --save-dev husky lint-staged prettier @ianvs/prettier-plugin-sort-imports
```

### ✅ Step 2: Add script to `package.json`

```json
{
  "scripts": {
    "prepare": "husky install",
    "lint": "eslint . --ext .js,.ts,.jsx,.tsx",
    "format": "prettier --write ."
  },
  "lint-staged": {
    "*.{js,ts,jsx,tsx}": ["eslint --fix", "prettier --write"]
  }
}
```

### ✅ Step 3: Create config files

#### prettier.config.js

```javascript
const config = {
  plugins: ['@trivago/prettier-plugin-sort-imports'],
  importOrder: [
    '^react$',
    '<THIRD_PARTY_MODULES>',
    '^@/.*', // alias
    '^[./].*$', // relative imports
    '^.+\\.css$',
  ],
  importOrderSortSpecifiers: true,
  semi: true,
  singleQuote: true,
  trailingComma: 'es5',
  tabWidth: 2,
};
export default config;
```

### ✅ Step 4: Set up Husky hook
#### .husky/pre-commit
```bash
npx lint-staged
```

### ✅ Folder Structure Example

```pgsql
my-project/
├── .husky/
│   └── pre-commit
├──  prettier.config.js
├── package.json
└── src/
    └── index.ts
```
