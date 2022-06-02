# lerna-monorepo
lerna-monorepo

## Шаги создания
1. В корне репозитория создаю пакет веб-клиента 
```npx create-react-app web-client```
2. Устанавливая lerna
```npm i -D lerna```
3. Инициализируем lerna в проекте
```npx lerna init```
- в корне появился файл package.json
- создан lerna.json
- создана папка packages
4. Идем в корень в package.json добавляем версию ```"version": "1.0.0",```
5. Идем в lerna.json меняем версию на ```"version": "1.0.0",```
6. Перемещаем web-client папку в папку packages
7. Создадим в packages бекенд пакет/приложение
```
cd packages
mkdir server-api
cd server-api
npm init --yes
```
8. В lerna-monorepo/packages/server-api 
- создаем index.js
- ставим пакети ```npm i express body-parser```
- пишем мини приложение в index.js

9. Теперь когда мы хотим чтобы node_modules были общими у packages, и лежали в корне проекта, то с помощью lerna
- сперва удаляем node_modules в lerna-monorepo/packages/server-api и lerna-monorepo/packages/web-client ```npx lerna clean -y```
- ставим все пакеты нужные нашим packages в корневой node_modules ```npx lerna bootstrap --hoist```

10. В lerna-monorepo/packages/server-api/package.json переписываем команды    
```json
  "scripts": {
    "start": "node index.js",
    "test": "echo testing Node server"
  },
```

11. В lerna-monorepo/packages/web-client/package.json переписываем команды    
```json
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "echo testing React App",
    "eject": "react-scripts eject"
  },
```

12. В lerna-monorepo/packages.json создаем команды    
```json
  "scripts": {
    "start": "lerna run start",
    "test": "lerna run test",
    "new-version": "lerna version --conventional-commits --yes",
    "diff": "lerna diff"
  },
```