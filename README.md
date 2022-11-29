# Wittr

This is a silly little demo app for an offline-first course.

You could run the app either using machine dependnecies, or using docker

## Running using local machine

### Installing

Dependencies:

* [Node.js](https://nodejs.org/en/) v0.12.7 or above

Then check out the project and run:

```sh
npm install
```

### Running

```sh
npm run serve
```

### Using the app

You should now have the app server at [localhost:8888](http://localhost:8888) and the config server at [localhost:8889](http://localhost:8889).

You can also configure the ports:

```sh
npm run serve -- --server-port=8000 --config-server-port=8001
```

## Running using docker

```sh
docker-compose up
```

Here also you should have the app server at [localhost:8888](http://localhost:8888) and the config server at [localhost:8889](http://localhost:8889).

You can configure the ports by changing them in `docker-compose.yml` before starting:

```yml
ports:
  # <host>:<container>
  - 8000:8888
  - 8001:8889
```

## Troubleshooting

* Errors while executing `npm run serve`.
  * The first thing to try is to upgrade to latest version of node.
  * If latest version also produces errors, try installing v4.5.0.
    * An easy fix for that would be [to use `nvm`](http://stackoverflow.com/a/7718438/1585523).
* If you get any node-sass errors, try running `npm rebuild node-sass --force` or the remove `node_modules` folder and run `npm install` again

Для запуска сервера нужно сделать несколько предварительных действий. 
1) Установить node.js версии 12.7.0. На ранних - ещё не заработает, на поздних - уже.
2) В package.json добавить секцию
"resolutions": {
    "graceful-fs": "^4.2.10"
  }
}, а в секцию scripts добавить срочку
"preinstall": "npx npm-force-resolutions" 
3) Во время выполнения заданий после каждого git reset --hard исправлять Server.js: в начале файла добавлять импорт
import https from 'https';
а после сотой строки, найти и исправить http на https в строках
const flickrUrl = `https://farm${req.params.farm}.....
const flickrRequest = https.request......
