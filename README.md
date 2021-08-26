Clone (use --recurse-submodules)

```
git clone --recurse-submodules GITHUB_URL
```

Check out a given branch (and the corresponding commits at each submodule)

```
git checkout --recurse-submodules --force develop
```

Now you need to install, link and locally build the packages linked by lerna.

```
npm run bootstrap
```

```
cd js-uprtcl
npm run build
cd ..
```

Now you should run the [Web Server](https://github.com/uprtcl/js-uprtcl-server/tree/develop) (Check it's README file, but you need to create an `.env` file and run dgraph with docker);

If you want to run a Web3 environment, you need to run along with the preivous step the following services:

- [IPFS](https://ipfs.io/) Service: Make sure you have a running daemon on your computer or assign an already deployed peer as environment variable to **Linked Thoughts** and **Watchman**

- [Uprtcl Blockchain Network](https://github.com/uprtcl/eth-uprtcl) (Only run `npm i` and `npm run dev`);

- [Blockchain Watchman](https://github.com/sotous/blockchain-watchman-uprtcl/tree/eth-refactor) (Check it's README file, you will need to create an `.env` file.);

Please, follow the steps in order, this way the **Watchman** will be able to connect to the **Uprtcl Blokchcain Network** and to the **IPFS** network to serve as a monitoring service targeting the indexing purpose.

Finally you can run the consuming application which uses the libraries and connects to the Web Server.

```
cd linked-thoughts
touch src/services/env.ts
```

And fill it with the following content:

**Web2**

```ts
export const env = {
  // host: 'https://api.intercreativity.io/uprtcl/1',
  host: 'http://localhost:3100/uprtcl/1',
};
```

**Web3**

```ts
export const env = {
  // host: 'https://api.intercreativity.io/uprtcl/1',
  host: 'http://localhost:3100/uprtcl/1',
  ethers: {
    provider: 'http://localhost:8545', // Blockchain test network (web3)
  },
  ipfs: {
    // IPFS daemon
    protocol: 'http',
    host: '127.0.0.1',
    port: 5002,
  },
};
```

Then run the app in dev mode

```
cd linked-thoughts
npm run dev
```

Now open `localhost:8002` on your browser and you should see the application. Use Metamask to login as Auth0 access is limited to an oklist.


> ### [Quick Start](https://github.com/sotous/js-uprtcl-dev/edit/eth-refactor/README.md#alternative-solution)
> If you already have Dgraph, IPFS and the ETH test network running somewhere, you could just run `npm run dev` after clonning and installing.
