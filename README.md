## API Reference

### `generateMnemonic()`

Generates a new secret phrase (mnemonic).

- **Returns:** `string` – A randomly generated mnemonic phrase.

---

### `generateAccount(mnemonic, deviceId)`

Generates an account from a secret phrase (mnemonic) and an optional device identifier to prevent duplication.

- **Parameters:**
    - `mnemonic` (`string`) – The user's secret phrase or mnemonic.
    - `deviceId` (`string`, optional) – A unique identifier like a device ID to differentiate account generation.
- **Returns:** `Object`
    - `account` (`string`) – Numeric account ID.
    - `accountRS` (`string`) – Human-readable Reed-Solomon address.
    - `publicKey` (`string`) – Derived public key.
- **Note:** Adding a `deviceId` or similar string ensures that the same mnemonic doesn't generate identical accounts across different devices.

---

### `accountSync(mnemonic)`

Fetches account information from a remote API using a secret phrase.

- **Parameters:**
    - `mnemonic` (`string`)
- **Returns:** `Promise<Object|null>` – A JSON object with the account ID, or `null` if an error occurs.

---

### `getAccountTransaction(accountRS)`

Fetches transactions for a given account.

- **Parameters:**
    - `accountRS` (`string`) – Reed-Solomon (RS) account ID.
- **Returns:** `Promise<Array|null>` – An array of transaction objects or `null` on error.

---

### `getTransactionDetail(fullHash)`

Fetches detailed information about a specific transaction.

- **Parameters:**
    - `fullHash` (`string`) – The full hash of the transaction.
- **Returns:** `Promise<Object|null>` – A JSON object with transaction details or `null` on error.

---

### `getTotalDistribute()`

Fetches the total distributed EUSD amount from the remote API.

- **Returns:** `Promise<Object|null>` – A JSON object with the total distributed amount, or `null` on error.

---

### `transferEUSD(address, amount, secretPhrase)`

Transfers EUSD to a specified recipient by making a POST request to the external API.

- **Parameters:**
    - `address` (`string`) – Recipient’s account address in RS format.
    - `amount` (`number|string`) – Amount of EUSD to transfer (need transfer 10 juts pass 10).
    - `secretPhrase` (`string`) – Sender’s secret phrase.
- **Returns:** `Promise<Object|null>` – A JSON object with the transaction result, or `null` on error.