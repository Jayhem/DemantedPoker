## Project Goal
The goal is to create a poker platform that is completely trustless and decentralized. Using [Ethereum](https://ethereum.org), [WAKU](https://our.status.im/v1-2-release/), [IPFS](https://ipfs.org), ZKP technos like [Circom](https://github.com/iden3/circom/blob/master/TUTORIAL.md) and possibly others like Swarm, NuCypher,...

## Project design
When designing a project that uses a blockchain as the backend of the application there are some constraints on speed, confidentiality and the cost (tx fees) of doing so. To that end, one overarching design constraint will be to minimize the write operations to the blockchain.

### Card shuffling and security ###
In order to have a poker software that cannot be gamed, the card shuffling needs to be done in a manner that cannot be eavesdropped on. It this were to be done on a blockchain it would be observable (with some exceptions like [Secret Network](https://scrt.network/), thus would not be secure. To avoid this issue, we can use the concept of [mental poker](https://en.wikipedia.org/wiki/Mental_poker), which uses requires the players to communicate via p2p (WAKU) and each shuffle and encrypt the deck.

### Poker game information source of truth
When cards and chip counts are all handled by p2p communication, how can you prevent one of the participants from injecting false information (with the intention of skewing the game to their advantage) in the game? By clever use of crypographic commitments we can always prove what happened. 
The only time one would need to store data on the blockchain would be when there is loss of communication between the players.

This project was bootstrapped with [Create Eth App](https://github.com/paulrberg/create-eth-app).

## Project Structure

The default template is a monorepo created with [Yarn Workspaces](https://classic.yarnpkg.com/en/docs/workspaces/).

Workspaces makes it possible to setup multiple packages in such a way that we only need to run `yarn install` once to install all of them in
a single pass. Dependencies are hoisted at the root.

```
my-eth-app
├── README.md
├── node_modules
├── package.json
├── .gitignore
└── packages
    ├── contracts
    │   ├── README.json
    │   ├── package.json
    │   └── src
    │       ├── abis
    │       │   ├── erc20.json
    │       │   └── ownable.json
    │       ├── addresses.js
    │       └── index.js
    ├── react-app
    │   ├── README.md
    │   ├── node_modules
    │   ├── package.json
    │   ├── public
    │   │   ├── favicon.ico
    │   │   ├── index.html
    │   │   ├── logo192.png
    │   │   ├── logo512.png
    │   │   ├── manifest.json
    │   │   └── robots.txt
    │   └── src
    │       ├── App.css
    │       ├── App.js
    │       ├── App.test.js
    │       ├── ethereumLogo.svg
    │       ├── index.css
    │       ├── index.js
    │       ├── serviceWorker.js
    │       └── setupTests.js
    └── subgraph
        ├── README.md
        ├── abis
        │   └── erc20.json
        ├── package.json
        ├── schema.graphql
        ├── src
        │   └── mappings
        │       ├── tokens.ts
        │       └── transfers.ts
        └── subgraph.yaml
```

Owing to this dependency on Yarn Workspaces, Create Eth App can't be used with npm.

## Available Scripts

In the project directory, you can run:

### React App

#### `yarn react-app:start`

Runs the React app in development mode.<br>
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will automatically reload if you make changes to the code.<br>
You will see the build errors and lint warnings in the console.

#### `yarn react-app:test`

Runs the React test watcher in an interactive mode.<br>
By default, runs tests related to files changed since the last commit.

[Read more about testing React.](https://facebook.github.io/create-react-app/docs/running-tests)

#### `yarn react-app:build`

Builds the React app for production to the `build` folder.<br />
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.<br />
Your app is ready to be deployed!

See the React documentation on [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

#### `yarn react-app:eject`

**Note: this is a one-way operation. Once you `react-app:eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` the React app at any time. This command will
remove the single build dependency from your React package.

Instead, it will copy all the configuration files and the transitive dependencies (Webpack, Babel, ESLint, etc) right
into the `react-app` package so you have full control over them. All of the commands except `react-app:eject` will still work,
but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `react-app:eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

### Subgraph

The Graph is a tool for for indexing events emitted on the Ethereum blockchain. It provides you with an easy-to-use GraphQL API. <br/>

To learn more, check out the [The Graph documentation](https://thegraph.com/docs).

#### `yarn subgraph:codegen`

Generates AssemblyScript types for smart contract ABIs and the subgraph schema.

#### `yarn subgraph:build`

Compiles the subgraph to WebAssembly.

#### `yarn subgraph:auth`

Before deploying your subgraph, you need to sign up on the
[Graph Explorer](https://thegraph.com/explorer/). There, you will be given an access token. Drop it in the command
below:

```sh
GRAPH_ACCESS_TOKEN=your-access-token-here yarn subgraph:auth
```

#### `yarn subgraph:deploy`

Deploys the subgraph to the official Graph Node.<br/>

Replace `paulrberg/create-eth-app` in the package.json script with your subgraph's name.

You may also want to [read more about the hosted service](https://thegraph.com/docs/quick-start#hosted-service).
