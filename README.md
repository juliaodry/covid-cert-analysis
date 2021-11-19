# covid-cert-analysis

This repository contains the analysis performed on the leaked forged COVID-19 Certificates.
The certificates, contained in string format in the `samples/` directory, have been collected
from the 4Chan and Raid Forums posts.

The results are in the [RESULTS.md](./RESULTS.md) file and can be generated using `./verify.sh`.

Please - stay safe and get vaccinated!

## The situation

On 2021-10-27 [@emanuelelaface](https://github.com/emanuelelaface) created
[an issue](https://github.com/ehn-dcc-development/hcert-spec/issues/103#issue-1036759866)
on [ehn-dcc-development/hcert-spec](https://github.com/ehn-dcc-development/hcert-spec)
to report a possible private key leakage of French and Polish governments.

The issue reports that (online and on Telegram) some forged COVID-19 Certificates
are circulating and are still marked as valid.  
  
The two certificates mentioned in the post are associated with "Adolf Hitler" with two different dates of birth.

## My Opinion

Although the private key leakage isn't unlikely,
especially due to nonce reuse or the possibility of a non-TRNGs being used (e.g: Sony hack),
chances that this is what's happening are low.

The reason for that is that most governments (if not all) are most probably using an HSM to perform
the signing, and thus even the owners of such systems are
likely to not have access to the underlying private key.  
  
What's more plausible is that someone broke the chain of trust
between the government and the doctors / pharmacies / hospitals
or installed malware on their computers and is now able
to generate certificates as if they were generated by a trusted party.  
  
To be able to prove that who claims to have access to a signing key
rather than a signing system (e.g: COVID Certificate signing portal),
one could maybe sign a certificate using an issuing date preceding COVID-19.  
Since the chances of the portals allowing a similar mistake are low, this could be the
only reliable proof (other than having the key itself) to confirm that the
key has been indeed leaked.  
  
Several screenshots on 4Chan seem to confirm my theory,
an EU portal is shown where the user signing the certificates
with the North Macedonian key is able to choose the
country of the certificate too. This results in the weird certificates
signed by North Macedonian's key but reporting the country to be e g: UK.  
  
Here you can find my 
[first](https://github.com/ehn-dcc-development/hcert-spec/issues/103#issuecomment-953346146)
and 
[second](https://github.com/ehn-dcc-development/hcert-spec/issues/103#issuecomment-953382640) 
comment on the topic.


## Disclaimers

This is a collection of forged COVID-19 Certificates that are:
- valid
- clearly forged
- leaked

**I do not generate these certificates, nor I'll provide you with any contact to where you can get these. If you want a valid COVID-19 Certificate,
  get vaccinated or take a rapid test.**

**The samples have been collected by multiple sources and they're freely available on the internet (e.g: 4Chan and Raid Forums)**

## Requirements

- Bash
- [corona-decoder](https://github.com/denysvitali/corona-decoder)
- zbarimg (to decode a QR code into text)

## Generate Results

```sh
./verify.sh > RESULTS.md
```

## Analyze a single certificate

```sh
corona-decoder -v -f ./samples/mickeymouse.txt
```
