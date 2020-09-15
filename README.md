# padrao-solid-tdd

### Projeto padrão em typescript com solid e tdd

- [1]

Dependências úteis

Gerenciar o padrão de mensagem de commit (fix), (feat), (test) ...
`npm install -D git-commit-msg-linter -D`

Projeto em typescript e tipagem
`npm install -D typescript @types/node`

Javascript Estilo Padrão [Funciona apenas com projetos javascript]
<https://standardjs.com/>

- [2]

Para utilizar em projeto typescript utilizar o Eslint
<https://github.com/standard/eslint-config-standard-with-typescript#readme>

`npm install --save-dev eslint@7 eslint-plugin-standard@4 eslint-plugin-promise@4 eslint-plugin-import@2 eslint-plugin-node@11 @typescript-eslint/eslint-plugin@4 eslint-config-standard-with-typescript`

- [3]

Configurar o eslint-whit-standard
criar um arquivo de configuração na raiz do projeto
nome do arquivo: 

`.eslintrc.json`

```json
{
  "extends": "standard-with-typescript",
  "parserOptions": {
    "ecmaVersion": 7,
    "sourceType": "module",
    "project":"./tsconfig.json"
  },
  "rules": {
    "quotes": ["error", "single"],
    "semi": ["error", "always"],
      "@typescript-eslint/strict-boolean-expressions":"off",
      "@typescript-eslint/consistent-type-definitions":"off",
      "@typescript-eslint/comma-spacing":"off",
      "@typescript-eslint/method-signature-style":"off",
      "@typescript-eslint/semi":"off"
  }
}
```

- [4]

Criar o eslint ignore

`.eslintignore`

Inserir a pasta node_modules e dist para serem ignorados

- [5]

Instalar o hysky para usar hooks e validar os códigos antes de realizar um commit

<https://www.npmjs.com/package/husky>

`npm install husky -D`

Criar arquivo de configuração para o husky
nome do arquivo 

`.huskyrc.json `

```json
{
    "hooks":{
        "pre-commit": "lint-staged"
    }
}
```

- [6]

husky trabalha em conjunto com outra biblioteca lint-staged, o que permite validar apenas os arquivos que estão na stage
<https://www.npmjs.com/package/lint-staged>

`npm install lint-staged -D`

Apos intalar criar na raiz do projeto o arquivo de configuração
.lintstagedrc.json

```json
{
    "*.ts": [
     "eslint 'src/**' --fix",
     "npm run test:staged"
    ]
}
```

- [7]

Instalar o jest para realizar os testes

`npm install -D jest @types/jest ts-jest`

Inicializar o jest no projeto se tiver o jest instalado de forma global

`npm install jest --global`

`jest --init`

Ajustar o arquivo de configuração do jest

`jest.config.js`

```javascript
module.exports = {
  collectCoverageFrom: [
    '<rootDir>/src/**/*.ts',
    '!<rootDir>/src/main/**',
    '!<rootDir>/src/**/*spec.ts',
    '!<rootDir>/src/**/*test.ts',
    '!<rootDir>/src/**/*test.js',
    '!<rootDir>/src/**/*spec.js',
    '!**/tests/**',
    '!**/test/**'
  ],
  coverageDirectory: 'coverage',
  coveragePathIgnorePatterns: ['\\\\node_modules\\\\'],
  coverageProvider: 'v8',
  roots: [
    '<rootDir>/src'
  ],
  testEnvironment: 'node',
  testPathIgnorePatterns: ['\\\\node_modules\\\\'],
  transform: {
    '.+\\.ts$': 'ts-jest'
  }
};
```

- [8]

Crie um arquivo de configuração do typescript

`npx tsc --init`

```json

{
  "compilerOptions": {
    "target": "ES2019",
    "module": "commonjs",
    "allowJs": true,
    "outDir": "./dist",
    "strict": true,
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true
  }
}
```

Criar a tag de testes no package.json

```json
  "scripts": {
    "test": "jest --passWithNoTests",
    "test:live": "jest --watch",
    "test:staged": "jest --passWithNoTests",
    "dev:server": "ts-node-dev --respawn --transpile-only src/app.ts"
  }
```

- [9]

Verificar se alguma biblioteca possui atualização

<https://www.npmjs.com/package/npm-check>

`npm install -g npm-check`

Comandos:
`npm-check -u` verifica atualizações de forma interativa

`npm-check -s -u` verifica atualizações de forma interativa e remove dependências não utilizadas

`npm-check -g` verifica atualizações em dependências globais

- [10]

Instalar ts node dev para realizar a compilação em tempo real 

`npm install ts-node-dev --save-dev`

Configurar o package.json para executar o arquivo do servidor typescript

`"dev:server": "ts-node-dev --respawn --transpile-only src/app.ts"`
