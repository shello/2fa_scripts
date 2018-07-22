# `oathtool_from_otpauth_uri`

Reads a [`otpauth://`](https://github.com/google/google-authenticator/wiki/Key-Uri-Format)
URI on the first argument, or from the standard input, and invokes
[`oathtool`](https://www.nongnu.org/oath-toolkit/) with the parameters from the
URI set, allowing extra parameters to be passed to `oathtool`.

## Examples

Passing a common OATH TOTP `otpauth://` URI. The output will differ, as the
time of execution is used for generating the verification token.

```
$ ./oathtool_from_otpauth_uri "otpauth://totp/ACME%20Co:john.doe@email.com?secret=HXDMVJECJJWSRB3HWIZR4IFUGFTMXBOZ&issuer=ACME%20Co"
610308
```

OATH HOTP is supported as well:

```
$ ./oathtool_from_otpauth_uri "otpauth://hotp/ACME%20Co:john.doe@email.com?secret=HXDMVJECJJWSRB3HWIZR4IFUGFTMXBOZ&issuer=ACME%20Co&counter=1618"
217735
```

It is possible to pass the URI to `./oathtool_from_otpauth_uri` from the
Standard Input using a pipe:

```
$ echo "otpauth://hotp/ACME%20Co:john.doe@email.com?secret=HXDMVJECJJWSRB3HWIZR4IFUGFTMXBOZ&issuer=ACME%20Co&counter=1618" | ./oathtool_from_otpauth_uri
217735
```

The `algorithm`, `digits` and `period` (for TOTP) parameters are also supported:

```
$ ./oathtool_from_otpauth_uri "otpauth://totp/ACME%20Co:john.doe@email.com?secret=HXDMVJECJJWSRB3HWIZR4IFUGFTMXBOZ&issuer=ACME%20Co&algorithm=SHA512&digits=8&period=60"
55435877
```
