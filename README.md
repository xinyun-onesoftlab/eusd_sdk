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

### `getAccountBalance(accountRS)`

Fetches balance for a given account.

- **Parameters:**
    - `accountRS` (`string`) – Reed-Solomon (RS) account ID.
- **Returns:** `Promise<Array|null>` – An array of balance objects or `null` on error.

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


---

### Flutter Reference
https://api.dart.dev/dart-js_interop/


## Code Sample (Flutter)

**pubspec.yaml**
>dependencies: <br/>
  js: ^0.6.5
 

**pubspec.yaml**
>@JS('EUSD_library')<br/>
> library eusd_library;
>import 'package:js/js.dart';<br/>
><br/>@JS()<br/>
>external String generateMnemonic();<br/>
><br/>@JS()<br/>
>external JsAccount generateAccount(String mnemonic);<br/>
><br/>@JS()<br/>
>external Object accountSync(String mnemonic);<br/> // returns a Promise
><br/>@JS()<br/>
>external Object getAccountTransaction(String accountRS);<br/>
><br/>@JS()<br/>
>external Object getTransactionDetail(String fullHash);<br/>
><br/>@JS()<br/>
>external Object getTotalDistribute();<br/>
><br/>@JS()<br/>
>external Object getConstant();<br/>
><br/>@JS()<br/>
>external Object transferEUSD(String address, dynamic amount, String secretPhrase);<br/>
><br/>@JS()<br/>
>@anonymous
>class JsAccount {
>external String get account;<br/>
>external String get accountRS;<br/>
>external String get publicKey;<br/>
>}

**index.html**<br/>
`<script src="EUSD_library.js"></script>`<br/>
`<script defer src="main.dart.js"></script>`

**Dart Code**
>import 'eusd_library_interop.dart';<br/>
><br/>
>void main() {<br/>
>final mnemonic = generateMnemonic();<br/>
>print("Mnemonic: \$mnemonic");<br/>
><br/>
>final account = generateAccount(mnemonic);<br/>
>print("Account ID: \${account.accountRS}");<br/>
>}


**Remark**<br/>
All async JS functions (accountSync, etc.) return JS Promises, so to handle them in Dart, use promiseToFuture from package:js/js_util.dart.
>import 'dart:js_util';<br/>
>import 'eusd_library_interop.dart';<br/>
><br/>
>Future<void> loadAccount() async { {<br/>
>final result = await promiseToFuture(accountSync("your secret phrase"));<br/>
> print(result);<br/>
>}