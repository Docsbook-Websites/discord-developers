---
title: Verify Discord Interaction Signatures on Your Endpoint
description: Acknowledge PING requests and validate Ed25519 signature headers so Discord accepts your Interactions Endpoint URL and rejects forged requests.
---

An Interactions Endpoint URL is a public, unauthenticated endpoint. Anyone can send it a request, so Discord requires proof that your app checks who is calling before it will deliver interactions over HTTP.

Discord validates the URL when you save it in your app's settings. Validation fails unless your endpoint already does both of the following.

## 1. Acknowledge PING requests

Discord sends a `POST` request with a `PING` payload, `type: 1`. Your endpoint returns a `200` response with a `PONG` payload, which is also `type: 1`.

```py
@app.route('/', methods=['POST'])
def my_command():
    if request.json["type"] == 1:
        return jsonify({
            "type": 1
        })
```

Provide a valid `Content-Type` when you respond to a `PING`. A correct payload with a missing content type still fails validation.

## 2. Validate the signature headers

Every interaction arrives with two headers:

- `X-Signature-Ed25519` — the signature
- `X-Signature-Timestamp` — the timestamp

Verify the signature on **every** request. If it fails, respond with `401`. Your app's public key is in the Developer Portal.

Two details cause most failures: verify against the **raw** request body as a string, not a re-serialized object, and concatenate the timestamp and body in that order before verifying.

### JavaScript

```js
const nacl = require("tweetnacl");

// Your public key can be found on your application in the Developer Portal
const PUBLIC_KEY = "APPLICATION_PUBLIC_KEY";

const signature = req.get("X-Signature-Ed25519");
const timestamp = req.get("X-Signature-Timestamp");
const body = req.rawBody; // rawBody is expected to be a string, not raw bytes

const isVerified = nacl.sign.detached.verify(
    Buffer.from(timestamp + body),
    Buffer.from(signature, "hex"),
    Buffer.from(PUBLIC_KEY, "hex")
);

if (!isVerified) {
    return res.status(401).end("invalid request signature");
}
```

### Python

```py
from nacl.signing import VerifyKey
from nacl.exceptions import BadSignatureError

# Your public key can be found on your application in the Developer Portal
PUBLIC_KEY = 'APPLICATION_PUBLIC_KEY'

verify_key = VerifyKey(bytes.fromhex(PUBLIC_KEY))

signature = request.headers["X-Signature-Ed25519"]
timestamp = request.headers["X-Signature-Timestamp"]
body = request.data.decode("utf-8")

try:
    verify_key.verify(f'{timestamp}{body}'.encode(), bytes.fromhex(signature))
except BadSignatureError:
    abort(401, 'invalid request signature')
```

## Troubleshooting validation

<!-- widget:accordion -->

### Discord rejects the URL when I save it

Discord sends a `PING` at that moment. If the endpoint is not deployed yet, returns a redirect, or sits behind authentication, validation fails. Deploy first, then save the URL.

### Signature verification fails on every request

The body was parsed and re-serialized before verification. JSON key order and whitespace change the bytes, so the signature no longer matches. Capture the raw body string before any JSON middleware runs.

### It works locally but not in production

The public key differs per application. Confirm the deployed app uses the key of the same application whose endpoint URL you configured.

<!-- /widget -->

## Next steps

- [Receiving and responding](./receiving-and-responding.md) — what to send once a request passes verification
- [Deploy on Cloudflare Workers](../guides/hosting-on-cloudflare-workers.md) — a verified endpoint with no server to maintain
- [Choosing a transport](../get-started/choosing-a-transport.md) — when HTTP is the right choice at all
