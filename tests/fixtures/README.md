# Test fixtures

The original hand-written templates, kept as an independent reference that
the generator's output is checked against. They are not used to generate
anything.

Changes from the originals: CRLF converted to LF, IS-IS lines removed
(saved in templates/pod/isis-config.conf and templates/plane/isis-config.conf
for the routing stage).

They describe a 4-plane build (pods 5–8). Placeholders:

| Placeholder | Meaning |
|---|---|
| `tt` | pod number (leaf, spine) or plane number (plane), padded |
| `qq` | router number, padded |
| `pp` | spine template: the plane this spine connects to, padded |
| `s1`–`s4` | plane template: the four spine numbers in this plane's block |
| `b1`–`b4` | pod YAML: this pod's four ports on each plane router |

In tests, IPv4 addresses (`10.10.tt.qq`, `10.11.tt.qq`) are filled in
without padding, per definitions.txt.

The plane fixture only covers pods 1–4 (eth01–16). In a 5–8 pod build the
plane routers have more interfaces, so only eth01–16 are compared.
