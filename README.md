# Node ES6 URL Shortener

![](https://img.shields.io/badge/node-success-brightgreen.svg)
![](https://img.shields.io/badge/test-success-brightgreen.svg)

# Stack

![](https://img.shields.io/badge/node_8-✓-blue.svg)
![](https://img.shields.io/badge/ES6-✓-blue.svg)
![](https://img.shields.io/badge/express-✓-blue.svg)
![](https://img.shields.io/badge/sequelize-✓-blue.svg)

***

<h3 align="center">Please help this repo with a :star: if you find it useful! :blush:</h3>

***

# File structure

```
node-es6-url-shortener/
│
├── api/
│   ├── controllers/
│   │   └── UrlController.js
│   │
│   ├── models/
│   │   └── Url.js
│   │
│   └── helpers/
│      └── base58.js
│
├── config/
│   ├── env/
│   │   ├── development.js
│   │   ├── index.js
│   │   ├── production.js
│   │   └── test.js
│   │
│   ├── routes/
│   │   ├── index.js
│   │   └── url.js
│   │
│   ├── express.js
│   └── sequelize.js
│
├── view/
│   ├── css/
│   │   └── styles.css
│   │
│   ├── javascript/
│   │   └── shorten.js
│   │
│   └── index.html
│
├── test/
│   └── url.test.js
│
├── .eslintrc                     * ESLint configuration file
├── .gitignore                    * Example git ignore file
├── index.mjs                     * Entry point of our Node's app
├── LICENSE                       * MIT License
├── package.json                  * Defines our JavaScript dependencies
├── package-lock.json             * Defines our exact JavaScript dependencies tree
└── README.md                     * This file
```

# Screenshot

<p align="center">
  <img src="https://github.com/murraco/node-es6-url-shortener/blob/master/screenshot.png" width="90%" />
</p>

# Introduction

## What's a URL Shortener?

 URL shortening is a technique to convert a long URL (site or page address) to a shorter version. This shorter version of the URL is usually cleaner and easier to share or remember. When someone accesses the shortened address, the browser redirects to the original (large) url address. It is also called URL redirection or URL redirect.

For example, the large version of this url:
http://en.wikipedia.org/wiki/URL_shortening

Can be shortened with bit.do service to this small address, that redirects to the previous longer address:
http://bit.do/urlwiki

## How does it work?

Essentially, your database has 3 fields: `primaryKey`, `shortCode` and `targetURL`.

Normally the `shortCode` is simply the `primaryKey` (which is an int) converted to another base. So for instance base 36 (so 0 through 9, and then 'a' through 'z').

This makes it easy to look up the `targetURL` in the database, since you can just decode it to base 10 and find the primary key.

You will also have short URLs since the number of URLs you can have is 36^n where n is the number of characters in the shortened URL. So you can see that just with 4 letters you can have a possible of 2,313,441 different URLs. If you use capital letters (a larger base), this gets even larger. 

## How to use this code?

1. Make sure you have the latest stable version of Node.js installed

```
$ sudo npm cache clean -f
$ sudo npm install -g n
$ sudo n stable
```

2. Configure your database and jsonwebtoken in `config/env`. For example `config/env/development.js` would look like this:

```js
module.exports = {
  mysql: {
    host: 'localhost',
    port: 3306,
    database: 'shortener_dev',
    username: 'root',
    password: '',
  }
};
```
  
3. Fork this repository and clone it
  
```
$ git clone https://github.com/<your-user>/node-es6-url-shortener
```
  
4. Navigate into the folder  

```
$ cd node-es6-url-shortener
```
  
5. Install NPM dependencies

```
$ npm install
```
  
6. Make sure you have a MySQL DB up and running, if you don't, using docker is the easiest way

```
$ docker run -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -t mysql -d mysql
```
Login into the container, update the root user and create databases

```
$ docker exec -it <CONTAINER ID> mysql -uroot
$ ALTER USER root IDENTIFIED WITH mysql_native_password BY 'root';
$ CREATE DATABASE shortener_dev;
$ CREATE DATABASE shortener_dev_dev;
$ CREATE DATABASE shortener_dev_test;
```

7. Run the project

```
$ node index.js
```
  
8. Or use `nodemon` for live-reload
  
```
$ npm start
```

> `npm start` will run `nodemon index.js`.

9. Navigate to `http://localhost:3000` in your browser to test it!

10. If you want to execute the tests

```
$ npm test
```

> `npm test` will run `mocha`.

# Contribution

- Report issues
- Open pull request with improvements
- Spread the word
- Reach out to me directly at <mauriurraco@gmail.com>
