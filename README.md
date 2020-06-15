# Criando projeto JS com Babel e Webpack Dev Server
----

*Este tutorial foi criado baseado no curso de ES6 do [Rocketseat](https://rocketseat.com.br/).*

## Instalar NodeJS e Yarn
* [NodeJS](https://nodejs.org/en/)
* [Yarn](https://classic.yarnpkg.com/pt-BR/)


----
## Executar e configurar o Yarn
Ir à pasta fonte do projeto e executar o comando:

    yarn init

Esse comando criará um arquivo chamado `package.json`, que contém as informações de dependência do projeto.

No `package.json`, criar a chave `devDependencies` em baixo de `"license"`, de forma que as dependências instaladas sejam somente para ambiente de desenvolvimento. Deve ficar assim:

    {
      "name": "tutorial",
      "version": "1.0.0",
      "main": "main.js",
      "license": "MIT",
      "devDependencies": {

      },
    }

A flag `-D` ao executar o `yarn add` serve para listar a dependência como sendo de desenvolvimento.

## Organizando os diretórios
Crie as pasta `src/` e `public/`. 

A pasta `src/` conterá todos os arquivos `.js` do seu projeto, que serão monitorados pelo * Webpack. * Já a pasta `public/` conterá os arquivos que não serão monitorados pelo *Webpack*, como os arquivos * HTML * e * CSS. *

Crie os arquivos `public/index.html` e `src/main.js`.

O `index.html` deve importar o script `bundle.js` em seu corpo.

----
## Instalando e configurando o Babel
Execute os comandos: 

    yarn add @babel/core -D
    yarn add @babel/cli -D
    yarn add @babel/preset-env -D
    yarn add babel-loader -D

Crie o arquivo `.babelrc` na raíz do projeto com o seguinte conteúdo:

    {
      "presets": ["@babel/preset-env"]
    }

----
## Instalando e configurando o Webpack e o Webpack Dev Server

Execute os comandos: 

    yarn add webpack webpack-cli webpack-dev-server -D

Crie o arquivo `webpack.config.js` na raiz do projeto. 

Esse arquivo deve conter o seguinte conteúdo: 

    module.exports = {
      entry: "./src/main.js",
      output: {
        path: __dirname + "/public",
        filename: "bundle.js",
      },
      devServer: {
        contentBase: __dirname + "/public",
      },
      module: {
        rules: [
          {
            test: /\.js$/,
            exclude: /node_modules/,
            use: {
              loader: "babel-loader",
            },
          },
        ],
      },
    };

## Criando os scripts de execução do Webpack
No arquivo `package.json`, abaixo das dependências, adicionar:

    "scripts": {
      "dev": "webpack-dev-server --mode=development",
      "build": "webpack-dev-server --mode=production"
    }

## Executando
Para executar o *Webpack*, basta rodar `yarn dev` na raíz do projeto. 

Para gerar o arquivo `bundle.js` (a fim de produção), basta rordar `yarn build`. O arquivo estará na pasta `public/`.

## Estrutura do projeto
    ├── node_modules
    ├── public/
    │   └── index.html
    ├── src/
    │   └── main.js
    ├── package.json
    ├── .babelrc
    ├── .webpack.config.js
    └── .yarn.lock
    
