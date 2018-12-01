                      Cucumber Linux from Scratch
                                Week 8
                            December 2, 2018

# Key Signing Party

This week, we will be having a key signing party. Signing each other's PGP keys allows us to begin to develop our own personal Webs of Trust. A Web of Trust is structured how it sounds: it is a web of key signatures that allows you to verify the authenticity of other people's PGP keys.

## Generating a PGP Key with GPG

If you do not already have a PGP key, generate one now. To start, install the GNU Privacy Guard (GPG).

If you do already have a PGP key and have GPG installed, you can skip this part and go right to the signing portion. Enjoy some cake while you are waiting for other people to generate their keys. :D

### Install GPG if Need Be

Refer to the platform specific instructions below.

#### Windows

Install the Windows Installer from GPG's website: https://www.gnupg.org/ftp/gcrypt/binary/gnupg-w32-2.2.11_20181106.exe

#### MacOS

Install GnuPG for OSX from Sourceforge: https://sourceforge.net/p/gpgosx/docu/Download/

#### Linux

GPG comes standard with most Linux distributions. If it does not, it can usually be installed by installing the `gpg` package from your distribution's package installer.

#### FreeBSD

Install the `gnupg` port:

    pkg install gnupg

#### OpenBSD

Install the `gnupg` port:

    pkg_add gnupg

### Generate the Keypair

Run the following command to begin the interactive key generation utility:

    gpg --full-gen-key

For the most part, you can accept the default options, with one exception:
When asked which key size you would like, I recommend ignoring the default and opting for a 4096 bit key; 2048 bit keys are getting less and less secure; with a high end super computer, a 2048 bit RSA key can be broken in 8 years.

Note that it will take a *long* time to generate the keypair.

Once your keypair finished generating, you will be given a key fingerprint. It is the number that looks like 484CF66FA2A3ADB2939ACB1019D7FD6A30198D3A. Take note of this, you will need it later.

### Generate a Revocation Certificate

In the event that your key is ever compromised or you lose the private key, it is important to have a revocation certificate. Publishing this certificate will indicate to other people that your key is no longer valid. To generate a revocation certificate, run the following command:

    gpg --output revoke.asc --gen-revoke 484CF66FA2A3ADB2939ACB1019D7FD6A30198D3A

The file revoke.asc is your revocation certificate. Make sure to keep it in a safe place; if it is ever stolen, someone could publish it and render your key useless. It may (at a minimum) be a good idea to `chmod 600` it.

### Publish your Public Key to the Key Servers

The public key is used publicly to encrypt messages that are to be sent to you and verify signatures that you have signed. In order to make it easier for people to obtain your public key, it is customary to publish it to publicly accessible key servers. To publish your public key, use the following command (make to replace the key fingerprint in the example with your key fingerprint):

    gpg --send-keys 484CF66FA2A3ADB2939ACB1019D7FD6A30198D3A

## Signing a PGP Key with GPG

To sign a PGP key, it is first necessary to receive the key you are planning to sign from a key server. To do this, run the follow command (substituting the key fingerprint of the key you wish to sign for the one in the example):

    gpg --recv-keys EC5649DA401E22ABFA6736EF6A4463C040102233

Now, sign the public key with your private key. By doing this, you are attesting that the owner information in the key is correct, so *make sure to inspect and verify the owner information before you sign the key.* Once you have done that, use the following command to sign the key:

    gpg --sign-key EC5649DA401E22ABFA6736EF6A4463C040102233

Once you have signed the key, send it back to the key server. Doing this will upload your signature:

    gpg --send-keys EC5649DA401E22ABFA6736EF6A4463C040102233

# Resources

* The GPG Handbook: https://www.gnupg.org/gph/en/manual.html
* The GPG Public Key Server Search Page: http://keys.gnupg.net/
* MIT's PGP Server: https://pgp.mit.edu/

vi:syntax=markdown

