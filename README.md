# vetkd-ICP demo

This repository provides a canister (`src/system_api`) that offers the vetKD system API proposed in https://github.com/dfinity/interface-spec/pull/158.

- An example app backend canister (`src/app_backend`) implemented in **Rust** that makes use of this system API to provide caller-specific symmetric keys that can be used for AES encryption and decryption.

- An example frontend (`src/app_frontend_js`) that uses the backend from Javascript in the browser.

  The frontend uses the [ic-vetkd-utils](https://github.com/dfinity/ic/tree/master/packages/ic-vetkd-utils) to create a transport key pair that is used to obtain a verifiably encrypted key from the system API, to decrypt this key, and to derive a symmetric key to be used for AES encryption/decryption.

  the `ic-vetkd-utils` are not yet published as NPM package, a respective package file (`ic-vetkd-utils-0.1.0.tgz`) is included in this repository.

- We can do IBE encryption-decryption as well.

- [System API canister implementation](https://github.com/dfinity/examples/blob/master/rust/vetkd/src/system_api/src/lib.rs#L19-L26).

## Prerequisites

1. Install the [IC SDK](https://internetcomputer.org/docs/current/developer-docs/setup/install/).
2. Install [Node.js](https://nodejs.org/en/download/).
3. Install [Rust](https://www.rust-lang.org/tools/install), and add Wasm as a target (`rustup target add wasm32-unknown-unknown`).

## Running Locally

- #### Step 1: Start a local internet computer.

```sh
dfx start
```

- #### Step 2: Open a new terminal window.

- #### Step 3: Ensure `dfx` uses the canister IDs that are hard-coded in the Rust source code:

```sh
dfx canister create system_api --specified-id s55qq-oqaaa-aaaaa-aaakq-cai
```

Without this, the `dfx` may use different canister IDs for the `system_api` and `app_backend` canisters in your local environment.

- #### Step 4: Ensure that the required node modules are available in your project directory, if needed, by running the following command:

```sh
npm install
```

- #### Step 5:. Register, build, and deploy the project:

```sh
dfx deploy
```

- #### Step 6: Open the URL for the `app_frontend_js` in your browser.

NOTE: This repository also takes code from the examples dfinity provides.
