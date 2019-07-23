# Criando uma Api REST com NodeJS

## Criando a base do projeto

Crie uma pasta como o nome do projeto (mkdir _nome-projeto_)

Entre na pasta e inicie o [Git](https://git-scm.com/)

```
git init
```

Criar o arquivo .gitignore (touch .gitignore)

```
node_modules
.env
```

Execute os comandos abaixos (você precisará do [Yarn](https://yarnpkg.com/pt-BR))

```
yarn init -y
yarn add express
yarn add sucrase nodemon -D
```

#### Crie os arquivos

**src/routes.js**

```
import { Router } from "express";

const routes = new Router();

routes.get("/", (req, res) => {
  return res.json({ status: "on-line" });
});

export default routes;
```

**src/app.js**

```
import express from "express";
import routes from "./routes";

class App {
  constructor() {
    this.server = express();

    this.middlewares();
    this.routes();
  }

  middlewares() {
    this.server.use(express.json());
  }

  routes() {
    this.server.use(routes);
  }
}

export default new App().server;

```

**src/server.js**

```
import app from "./app";

app.listen(3333);
```

Criar o arquivo **nodemon.json**

```
{
  "execMap": {
    "js": "sucrase-node"
  }
}
```

#### Altere o arquivo

Acresentar no arquivo **package.json**

```
  "scripts": {
    "dev": "nodemon src/server.js"
  }
```


