# perseta-onboard

The front door for PersetaLab invites: https://go.persetalab.com/
(the same page is also at https://sisentience.github.io/perseta-onboard/).

- `index.html` reads the invite from the link fragment (`#t=<token>`). Browsers never
  send the fragment to this host. The page loads `locator.json`, then opens the
  welcome page on the lab's desk.
- `locator.json` names the desk's current address (`app_url`) and its support host
  (`rd_host`, `rd_port`). A scheduled publisher keeps it current.
- `locator.sig` is the ECDSA P-256 signature (SHA-256, DER, base64 on one line) over the
  exact bytes of `locator.json`. `locator.pub` is the public key that checks it:

      openssl dgst -sha256 -verify locator.pub -signature <(openssl base64 -d -A < locator.sig) locator.json

Nothing in this repository is secret. Never commit an invite link here.
