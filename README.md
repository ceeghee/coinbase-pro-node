# Coinbase Pro API

![David](https://img.shields.io/david/bennyn/coinbase-pro-node?style=flat-square) [![codecov](https://codecov.io/gh/bennyn/coinbase-pro-node/branch/master/graph/badge.svg)](https://codecov.io/gh/bennyn/coinbase-pro-node)

[Coinbase Pro][1] API for Node.js, written in TypeScript and covered by tests.

## Motivation

This project was created to continue an active **Coinbase Pro API** after Coinbase deprecated the official Node.js library on [January, 16 2020](https://github.com/coinbase/coinbase-node/issues/140#issuecomment-574990136). The official predecessor was also deprecated on [July, 19th 2016](https://github.com/coinbase/coinbase-exchange-node/commit/b8347efdb4e2589367c1395b646d283c9c391681).

## Features

Advantages over the [official counterpart][3]:

- **Alive.** Not archived and ready-only. Pull Requests are welcome!
- **Typed.** Source code is 100% TypeScript. No need to install external typings.
- **Tested.** Code coverage is at 100%. No surprises when using it.
- **Robust.** WebSocket reconnection is built-in. No problems if your Wi-Fi is gone.
- **Easy-to-use.** HTTP requests are easy to customize. HMAC signing and JSON formatting is already included.

## Installation

**npm**

```bash
npm install coinbase-pro-node
```

**Yarn**

```bash
yarn add coinbase-pro-node
```

## Usage

**Node.js setup**

```javascript
const {CoinbasePro} = require('coinbase-pro-node');

// API Keys can be generated here:
// https://pro.coinbase.com/profile/api
// https://public.sandbox.pro.coinbase.com/profile/api
const auth = {
  apiKey: '',
  apiSecret: '',
  passphrase: '',
  useSandbox: true,
};

const client = new CoinbasePro(auth);
```

## REST Example

**Query accounts**

```javascript
const tradingAccounts = await client.rest.account.listAccounts();
const message = `You can trade "${tradingAccounts.length}" different pairs.`;
console.log(message);
```

## WebSocket Example

**Event registration**

```javascript
client.on(WebSocketClient.TOPIC.ON_MESSAGE, event => {
  console.log(`Received event of type "${event.type}".`);
});

await client.ws.connect();

client.ws.subscribeToTickers(['BTC-USD', 'ETH-EUR']);
```

## Resources

- [Coinbase Pro API Reference][2]
- [Coinbase Pro API][3]
- [Coinbase Pro Trading Toolkit](https://github.com/coinbase/coinbase-pro-trading-toolkit)

## Contributing

Contributions, issues and feature requests are welcome!

Feel free to check [issues page](https://github.com/bennyn/coinbase-pro-node/issues).

The following commits will help you getting started quickly with the code base:

- [Add REST API endpoint](https://github.com/bennyn/coinbase-pro-node/commit/8a150fecb7d32b7b7cd39a8109985f665aaee26e)

## Maintainers

[![Benny Neugebauer on Stack Exchange][stack_exchange_bennyn_badge]][stack_exchange_bennyn_url]

## License

This project is [MIT](./LICENSE) licensed.

## Show your support

Give a ⭐️ if this project helped you!

[1]: https://pro.coinbase.com/
[2]: https://docs.pro.coinbase.com/
[3]: https://github.com/coinbase/coinbase-pro-node
[stack_exchange_bennyn_badge]: http://stackexchange.com/users/flair/203782.png?theme=default
[stack_exchange_bennyn_url]: http://stackexchange.com/users/203782/benny-neugebauer?tab=accounts
