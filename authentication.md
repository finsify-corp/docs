# Authentication

Authenticate your account when using the API by including your secret API key in the request. You can manage your API keys in the Dashboard. Your API keys carry many privileges, so be sure to keep them secret! Do not share your API keys in publicly accessible areas such GitHub, client-side code, and so forth.

Before sending api request, your data must be encrypted with AES CTR 256bit encryption method, the decryption key must be encrypted with RSA 2048 bit encryption using the API public key we sent you.