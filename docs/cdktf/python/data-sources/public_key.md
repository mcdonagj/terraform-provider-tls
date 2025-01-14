---

<!-- Please do not edit this file, it is generated. -->
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "tls_public_key Data Source - terraform-provider-tls"
subcategory: ""
description: |-
  Get a public key from a PEM-encoded private key.
  Use this data source to get the public key from a PEM (RFC 1421) https://datatracker.ietf.org/doc/html/rfc1421 or OpenSSH PEM (RFC 4716) https://datatracker.ietf.org/doc/html/rfc4716 formatted private key, for use in other resources.
---

# tls_public_key (Data Source)

Get a public key from a PEM-encoded private key.

Use this data source to get the public key from a [PEM (RFC 1421)](https://datatracker.ietf.org/doc/html/rfc1421) or [OpenSSH PEM (RFC 4716)](https://datatracker.ietf.org/doc/html/rfc4716) formatted private key, for use in other resources.

## Example Usage

```python
# DO NOT EDIT. Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
from constructs import Construct
from cdktf import Fn, Token, TerraformStack
#
# Provider bindings are generated by running `cdktf get`.
# See https://cdk.tf/provider-generation for more details.
#
from imports.tls.data_tls_public_key import DataTlsPublicKey
from imports.tls.private_key import PrivateKey
class MyConvertedCode(TerraformStack):
    def __init__(self, scope, name):
        super().__init__(scope, name)
        ed25519_example = PrivateKey(self, "ed25519-example",
            algorithm="ED25519"
        )
        DataTlsPublicKey(self, "private_key_openssh-example",
            private_key_openssh=Token.as_string(Fn.file("~/.ssh/id_rsa_rfc4716"))
        )
        DataTlsPublicKey(self, "private_key_pem-example",
            private_key_pem=ed25519_example.private_key_pem
        )
```

<!-- schema generated by tfplugindocs -->
## Schema

### Optional

- `private_key_openssh` (String, Sensitive) The private key (in  [OpenSSH PEM (RFC 4716)](https://datatracker.ietf.org/doc/html/rfc4716) format) to extract the public key from. This is _mutually exclusive_ with `private_key_pem`. Currently-supported algorithms for keys are: `RSA`, `ECDSA`, `ED25519`.
- `private_key_pem` (String, Sensitive) The private key (in [PEM (RFC 1421)](https://datatracker.ietf.org/doc/html/rfc1421) format) to extract the public key from. This is _mutually exclusive_ with `private_key_openssh`. Currently-supported algorithms for keys are: `RSA`, `ECDSA`, `ED25519`.

### Read-Only

- `algorithm` (String) The name of the algorithm used by the given private key. Possible values are: `RSA`, `ECDSA`, `ED25519`.
- `id` (String) Unique identifier for this data source: hexadecimal representation of the SHA1 checksum of the data source.
- `public_key_fingerprint_md5` (String) The fingerprint of the public key data in OpenSSH MD5 hash format, e.g. `aa:bb:cc:...`. Only available if the selected private key format is compatible, as per the rules for `public_key_openssh` and [ECDSA P224 limitations](../../docs#limitations).
- `public_key_fingerprint_sha256` (String) The fingerprint of the public key data in OpenSSH SHA256 hash format, e.g. `SHA256:...`. Only available if the selected private key format is compatible, as per the rules for `public_key_openssh` and [ECDSA P224 limitations](../../docs#limitations).
- `public_key_openssh` (String) The public key, in  [OpenSSH PEM (RFC 4716)](https://datatracker.ietf.org/doc/html/rfc4716) format. This is also known as ['Authorized Keys'](https://www.ssh.com/academy/ssh/authorized_keys/openssh#format-of-the-authorized-keys-file) format. This is not populated for `ECDSA` with curve `P224`, as it is [not supported](../../docs#limitations). **NOTE**: the [underlying](https://pkg.go.dev/encoding/pem#Encode) [libraries](https://pkg.go.dev/golang.org/x/crypto/ssh#MarshalAuthorizedKey) that generate this value append a `\n` at the end of the PEM. In case this disrupts your use case, we recommend using [`trimspace()`](https://www.terraform.io/language/functions/trimspace).
- `public_key_pem` (String) The public key, in [PEM (RFC 1421)](https://datatracker.ietf.org/doc/html/rfc1421) format. **NOTE**: the [underlying](https://pkg.go.dev/encoding/pem#Encode) [libraries](https://pkg.go.dev/golang.org/x/crypto/ssh#MarshalAuthorizedKey) that generate this value append a `\n` at the end of the PEM. In case this disrupts your use case, we recommend using [`trimspace()`](https://www.terraform.io/language/functions/trimspace).

<!-- cache-key: cdktf-0.19.0 input-025d5bde39901a91ba6cb60272c97a78a0c01a6de59d77d7dea035490ff6ee0a 556251879b8ed0dc4c87a76b568667e0ab5e2c46efdd14a05c556daf05678783-->