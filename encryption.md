# Encryption

Before sending api request, your data must be encrypted with AES CTR 256bit encryption method, the decryption key must be encrypted with RSA 2048 bit encryption using the API public key we sent you. Each client_id will have different key/vector.

AES encryption sample:

```javascript
const aesjs = require('aes-js');

const text = '{"credentials":{ "username": "xxxxx", "password": "xxxxx" },"service_id":8,"callback_url":"https://callback.url.com","only_get_accounts":true,"type":"auto"}';
var key = [82, 22, 180, 226, 160, 167, 221, 201, 203, 201, 170, 110, 127, 82, 88, 39, 23, 202, 33, 122, 5, 183, 202, 110, 138, 220, 122, 177, 15, 217, 232, 92];
var iv = [34, 85, 64, 36, 83, 67, 24, 68, 24, 15, 2, 4, 94, 24, 79, 45];

var textBytes = aesjs.utils.utf8.toBytes(text);
var aesCtr = new aesjs.ModeOfOperation.ctr(key,iv );
var encryptedBytes = aesCtr.encrypt(textBytes);
var encryptedHex = aesjs.utils.hex.fromBytes(encryptedBytes);
console.log('AES encrypted: ', encryptedHex);
encryptedBytes = aesjs.utils.hex.toBytes(encryptedHex);
aesCtr = new aesjs.ModeOfOperation.ctr(key, iv);
var decryptedBytes = aesCtr.decrypt(encryptedBytes);
var decryptedText = aesjs.utils.utf8.fromBytes(decryptedBytes);
console.log('AES decrypted: ', decryptedText);
```

RSA encryption sample:

```javascript
const NodeRSA = require('node-rsa');

const publickey = new NodeRSA({ b: 2048 });
publickey.importKey(fs.readFileSync('./public.key'));
publickey.setOptions({ encryptionScheme: 'pkcs1' });

var AESecryptionKey = JSON.stringify(key);
console.log('AES Key: ', AESecryptionKey);
var aeskey = publickey.encrypt(AESecryptionKey, 'base64');
console.log('AES Key RSA encrypted: ', aeskey);
```