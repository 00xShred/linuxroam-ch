# linuxroam-ch

Swiss eduroam installer for Linux + NetworkManager.

Inspired by [diverso-lab/linuxroam](https://github.com/diverso-lab/linuxroam). This version keeps the useful CAT profile flow, but fixes the Swiss NetworkManager setting: **no CA certificate is selected**. ETHZ/ZHAW-style Linux instructions tell users to choose “no certificate needed”; the original script wrote a CA certificate and enabled certificate validation.

## Install

One-liner:

```bash
curl -fsSL https://codeberg.org/0xShred/linuxroam-ch/raw/branch/main/install.sh | bash
```

Or clone and inspect first:

```bash
git clone https://codeberg.org/0xShred/linuxroam-ch
cd linuxroam-ch
./install.sh
```

## What it does

- Uses the official [eduroam CAT API](https://cat.eduroam.org/) to list Swiss institutions and read the EAP profile.
- Creates `/etc/NetworkManager/system-connections/eduroam.nmconnection`.
- Sets username/password, EAP method, phase2 auth, and anonymous identity when provided.
- Leaves certificate validation off with `system-ca-certs=false` and no `ca-cert=` line.
- Reloads NetworkManager and tries to connect.

## Uninstall

```bash
curl -fsSL https://codeberg.org/0xShred/linuxroam-ch/raw/branch/main/install.sh | bash -s -- --uninstall
```

Removes the `eduroam` NetworkManager connection and this tool's metadata under `/etc/eduroam`.

## Credits

Based on GPLv3 project [linuxroam](https://github.com/diverso-lab/linuxroam) by Diverso Lab. This fork changes the certificate behavior for Swiss university guidance.
