<div align="center">
  <a href="https://particle.network/">
    <img src="https://i.imgur.com/xmdzXU4.png" style="display: inline-block; vertical-align: middle;" />
  </a>
  <a href="https://another-link.com/">
    <img src="https://docs.kakarot.org/img/logo.svg" style="display: inline-block; vertical-align: middle; width: 400px; heigh: 150px;" />
  </a>
  <h3>
    @particle-network/auth-core @particle-network/aa Demo Application 
  </h3>
</div>


# Particle Auth, Account Abstraction SDK, Next.js, ethers V6, with Kakarot

## Table of contents

⚡️ Basic demo application using `@particle-network/auth-core` and `@particle-network/aa` to initiate social login and send transactions via an account abstraction smart account on IoTex.

This is a lower-level library that powers `@particle-network/auth-core-modal`. The developer implementing this library must build most additional functionality beyond the aforementioned (login and transaction execution).

This app allows you to log in using social logins and interact with the Ethereum Sepolia and Base Sepolia testnets by displaying account information and sending a transfer transaction to an address you can input in the UI. The user can select to send a gasless transaction or pay gas with the native token.

This demo is built in both Next JS and Native React.

> The Next application is within the `kakarot-particle-aa-nextjs` directory.

Built using:

- **Particle Auth Core**
- **Particle AA SDK**
- **ethers.js V6.x.x**
- **TypeScript**
- **Tailwind CSS**

## What is Kakarot zkEVM

[Kakarot zkEVM](https://www.kakarot.org/) is a zk-rollup built on the Starknet stack, leveraging CairoVM and StarknetOS runtime for provable execution. Fully compatible with Ethereum, Kakarot benefits from the latest EVM upgrades and innovations in zero-knowledge technology, making it a powerful and seamless platform for dApp development.

## 🔑 Particle Auth Core

Particle Auth Core, a component of Particle Network's Wallet-as-a-Service, enables seamless onboarding to an application-embedded MPC-TSS/AA wallet facilitated by social login, such as Google, GitHub, email, phone number, etc. - as an alternative to Particle Auth, the Auth Core SDK comes with more control over the modal itself, application-embedded popups rather than redirects, and so on.

👉 Learn more about [Particle Auth](https://developers.particle.network/docs/building-with-particle-auth).

## 🪪 Account Abstraction SDK

Particle Network natively supports and facilitates the end-to-end utilization of ERC-4337 account abstraction. This is primarily done through the account abstraction SDK, which can construct, sponsor, and send UserOperations, deploy smart accounts, retrieve fee quotes, and perform other vital functions.

> Every gasless transaction is automatically sponsored on testnet. On mainnet, you'll need to deposit USDT into Paymaster.

👉 Learn more about the [Particle AA SDK](https://developers.particle.network/docs/aa-web-quickstart).

***

👉 Learn more about [Particle Network](https://particle.network).

## 🛠️ Quickstart

### Clone this repository
```
git clone https://github.com/Particle-Network/kakarot-auth-aa-demo.git
```

### Move into the app directory (Next JS)

```sh
cd kakarot-particle-aa-nextjs
```

### Install dependencies

```sh
yarn install
```

Or

```sh
npm install
```

### Set environment variables
This project requires several keys from Particle Network to be defined in `.env`. The following should be defined:
- `NEXT_PUBLIC_PROJECT_ID`, the ID of the corresponding application in your [Particle Network dashboard](https://dashboard.particle.network/#/applications).
- `NEXT_PUBLIC_CLIENT_KEY`, the ID of the corresponding project in your [Particle Network dashboard](https://dashboard.particle.network/#/applications).
-  `NEXT_PUBLIC_APP_ID`, the client key of the corresponding project in your [Particle Network dashboard](https://dashboard.particle.network/#/applications).

### Start the project
```sh
npm run dev
```

Or

```sh
yarn dev
```

## Development Next JS

Particle Auth config is in `src/app/layout.tsx`. 

### Config social logins

List of available social logins:

```sh
{
  email: 'email',
  phone: 'phone',
  facebook: 'facebook',
  google: 'google',
  apple: 'apple',
  twitter: 'twitter',
  discord: 'discord',
  github: 'github',
  twitch: 'twitch',
  microsoft: 'microsoft',
  linkedin: 'linkedin',
  jwt: 'jwt'
}
```

### AA options

You can configure the smart account using the `aaOptions` object in `src/app/page.tsx`.

---

- **BICONOMY**, a [Biconomy smart account](https://www.biconomy.io/smart-accounts).
  - `version`, either `1.0.0` or `2.0.0`; both versions of Biconomy's smart account implementation are supported.
  - `chainIds`, an array of chain IDs in which the smart account is expected to be used.
- **CYBERCONNECT**, a [CyberConnect smart account](https://wallet.cyber.co/).
  - `version`, currently only `1.0.0` is supported for `CYBERCONNECT`.
  - `chainIds`, an array of chain IDs in which the smart account is expected to be used.
- **SIMPLE**, a [SimpleAccount implementation](https://github.com/eth-infinitism/account-abstraction/blob/develop/contracts/samples/SimpleAccount.sol).
  - `version`, either `1.0.0` or `2.0.0` is supported for `SIMPLE`.
  - `chainIds`, an array of chain IDs in which the smart account is expected to be used.
- **LIGHT**, a [Light Account implementation by Alchemy](https://github.com/alchemyplatform/light-account).
  - `version`, currently only `1.0.2` is supported for `LIGHT`.
  - `chainIds`, an array of chain IDs in which the smart account is expected to be used.
- **XTERIO**, a [Xterio smart account](https://xter.io/build).
  - `version`, currently only `1.0.0` is supported for `XTERIO`.
  - `chainIds`, an array of chain IDs in which the smart account is expected to be used.

---

```ts
  // Set up and configure the smart account
  const smartAccount = new SmartAccount(provider, {
    projectId: process.env.REACT_APP_PROJECT_ID!,
    clientKey: process.env.REACT_APP_CLIENT_KEY!,
    appId: process.env.REACT_APP_APP_ID!,
    aaOptions: {
      accountContracts: {
        SIMPLE: [
          {
            version: "1.0.0", // SIMPLE only allows 1.0.0
            chainIds: [KakarotSepolia.id],
          },
        ],
      },
    },
  });

  // Use this syntax to upadate the smartAccount if you define more that one smart account provider in accountContracts
  //smartAccount.setSmartAccountContract({ name: "SIMPLE", version: "1.0.0" });
 ```
