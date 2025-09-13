# GPG署名付きコミットを有効にする

## 手順

### GPGキーを生成する

```bash
gpg --full-gen-key
```

```log
gpg (GnuPG) 2.4.7-unknown; Copyright (C) 2024 g10 Code GmbH
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

gpg: directory '****/.gnupg' created
Please select what kind of key you want:
   (1) RSA and RSA
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
   (9) ECC (sign and encrypt) *default*
  (10) ECC (sign only)
  (14) Existing key from card
Your selection? 1                                                              <- 1を選択
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 4096                                          <- なんとなく4096を指定
Requested keysize is 4096 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 1y                                                        <- とりあえず1年で設定した
Key expires at 2026年08月15日 17時18分05秒
Is this correct? (y/N) y

GnuPG needs to construct a user ID to identify your key.

Real name: rmatttu
Email address: mggggk@gmail.com
Comment: Github GPG key                                                        <- name、メール、キーのコメントを入力した
You selected this USER-ID:
    "rmatttu (Github GPG key) <mggggk@gmail.com>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: *********trustdb.gpg: trustdb created
gpg: directory '*********/.gnupg/openpgp-revocs.d' created
gpg: revocation certificate stored as '*********/.gnupg/openpgp-revocs.d/D9EFA39C815ED905C4031B6DB314C14E27DC44D1.rev'
public and secret key created and signed.

pub   rsa4096 2025-08-15 [SC] [expires: 2026-08-15]
      D9EFA39C815ED905C4031B6DB314C14E27DC44D1
uid                      rmatttu (Github GPG key) <mggggk@gmail.com>
sub   rsa4096 2025-08-15 [E] [expires: 2026-08-15]
```

```bash
gpg --list-secret-keys --keyid-format=long
```

```log
gpg: checking the trustdb
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: depth: 0  valid:   1  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 1u
gpg: next trustdb check due at 2026-08-15
[keyboxd]
---------
sec   rsa4096/B314C14E27DC44D1 2025-08-15 [SC] [expires: 2026-08-15]
      D9EFA39C815ED905C4031B6DB314C14E27DC44D1
uid                 [ultimate] rmatttu (Github GPG key) <mggggk@gmail.com>
ssb   rsa4096/1E2CCD4DFB415E68 2025-08-15 [E] [expires: 2026-08-15]
```

生成したキーを確認する。公開鍵を出力する。

```bash
gpg --armor --export B314C14E27DC44D1
```

```log
-----BEGIN PGP PUBLIC KEY BLOCK-----

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
HzuDcOntGPAlUtLxNplDobHaJokySA==
=+IJl
-----END PGP PUBLIC KEY BLOCK-----
```

### GitHub.comにGPGキーを登録する

[SSH and GPG keys](https://github.com/settings/keys)を参考に設定する。

### ローカルのGitにて、GPGキー設定を行う

```bash
# このリポジトリにのみ設定を適用する
git config --local commit.gpgsign true
```

```bash
git config --local user.signingkey <GPGキーID>
# ↓
# e.g. git config --local user.signingkey B314C14E27DC44D1
```

以下のコマンドでgitの設定値を確認する。

```bash
git config --local --list
#
# 中略...
#
# user.signingkey=B314C14E27DC44D1
# commit.gpgsign=true
#
# ↑ 設定したGPGキーが確認できた
#
```

以下のコマンドでコミットしてみる。

```bash
git commit -S
```

テキストエディタが起動するので、コミットメッセージを入力する。また、テキストエディタを終了すると、パスフレーズの入力を求められた。

### コミットに署名されているか確認

```bash
git log --show-signature
```

```log
# ↓　署名付きコミットされている

commit dd2499b3644c2b2223a39d0a013db963b2a56665 (HEAD -> main)
gpg: Signature made 2025年08月16日 16時19分38秒
gpg:                using RSA key D9EFA39C815ED905C4031B6DB314C14E27DC44D1
gpg: Good signature from "rmatttu (Github GPG key) <mggggk@gmail.com>" [ultimate]
Author: mggggk <mggggk@gmail.com>
Date:   Sat Aug 16 16:19:32 2025 +0900

    Add .gitignore


# ↓　署名付きコミットされている

commit 2d19fad5cd115a0176342e03e6046d1eaedd1231 (origin/main, origin/HEAD)
gpg: Signature made 2025年08月16日 16時10分24秒
gpg:                using RSA key D9EFA39C815ED905C4031B6DB314C14E27DC44D1
gpg: Good signature from "rmatttu (Github GPG key) <mggggk@gmail.com>" [ultimate]
Author: mggggk <mggggk@gmail.com>
Date:   Sat Aug 16 16:10:06 2025 +0900

    Update README.md 2

# ↓　署名付きコミットされていない！

commit 22c292881a137421892bcf2bb01f1a9aaba09251
Author: mggggk <mggggk@gmail.com>
Date:   Sat Aug 16 16:01:08 2025 +0900

    Update README.md

commit eca854d3939180e7281e670c59514cba6c79f247
Author: mggggk <mggggk@gmail.com>
Date:   Sat Aug 16 16:00:20 2025 +0900

    First commit
```

### Github Actionsでgoreleaserを設定

Repository secretsに設定

- `secrets.GITHUB_TOKEN`
- `secrets.GPG_PRIVATE_KEY`
- `secrets.PASSPHRASE`

```bash
gpg --armor --export-secret-keys <KEY_IDENTIFIER>
# e.g. gpg --armor --export-secret-keys B314C14E27DC44D1
```

### Signs

- [goreleaser/goreleaser-action: GitHub Action for GoReleaser](https://github.com/goreleaser/goreleaser-action?tab=readme-ov-file#signing)
- [terraform - How can I use GoReleaser to sign a binary with a GPG key that requires a passphrase - Stack Overflow](https://stackoverflow.com/questions/69006478/how-can-i-use-goreleaser-to-sign-a-binary-with-a-gpg-key-that-requires-a-passphr)
  - `.goreleaser.yaml`のサンプル

その他

- [WindowsにてVisual Studio Codeからcommitするときにgpg署名する #Git - Qiita](https://qiita.com/yumetodo/items/7c25c1d6de92921faa3e)

## キーのエクスポート・インポート

### エクスポート

GPGキーをファイルとしてエクスポートし、信頼できる経路で別マシンへ転送します。

```bash
gpg --export-secret-keys B314C14E27DC44D1 > github_gpg_private.key
```

### インポート

```bash
gpg --import github_gpg_private.key
```

インポートしたGPGキーは、初期設定では信頼しない設定となっているようです。

```bash
gpg --list-secret-keys --keyid-format=long
```

```log
----------------------------
sec   rsa4096/B314C14E27DC44D1 2025-08-15 [SC] [expires: 2026-08-15]
      D9EFA39C815ED905C4031B6DB314C14E27DC44D1
uid                 [ unknown] rmatttu (Github GPG key) <mggggk@gmail.com>
ssb   rsa4096/1E2CCD4DFB415E68 2025-08-15 [E] [expires: 2026-08-15]
```

uidが`[ unknown]`となっている。以下のコマンドでキーを信頼する。

```bash
gpg --edit-key B314C14E27DC44D1 trust quit
```

```log
gpg (GnuPG) 2.2.40; Copyright (C) 2022 g10 Code GmbH
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Secret key is available.

sec  rsa4096/B314C14E27DC44D1
     created: 2025-08-15  expires: 2026-08-15  usage: SC
     trust: unknown       validity: unknown
ssb  rsa4096/1E2CCD4DFB415E68
     created: 2025-08-15  expires: 2026-08-15  usage: E
[ unknown] (1). rmatttu (Github GPG key) <mggggk@gmail.com>

sec  rsa4096/B314C14E27DC44D1
     created: 2025-08-15  expires: 2026-08-15  usage: SC
     trust: unknown       validity: unknown
ssb  rsa4096/1E2CCD4DFB415E68
     created: 2025-08-15  expires: 2026-08-15  usage: E
[ unknown] (1). rmatttu (Github GPG key) <mggggk@gmail.com>

Please decide how far you trust this user to correctly verify other users' keys
(by looking at passports, checking fingerprints from different sources, etc.)

  1 = I don't know or won't say
  2 = I do NOT trust
  3 = I trust marginally
  4 = I trust fully
  5 = I trust ultimately
  m = back to the main menu

Your decision? 5
Do you really want to set this key to ultimate trust? (y/N) y

sec  rsa4096/B314C14E27DC44D1
     created: 2025-08-15  expires: 2026-08-15  usage: SC
     trust: ultimate      validity: unknown
ssb  rsa4096/1E2CCD4DFB415E68
     created: 2025-08-15  expires: 2026-08-15  usage: E
[ unknown] (1). rmatttu (Github GPG key) <mggggk@gmail.com>
Please note that the shown key validity is not necessarily correct
unless you restart the program.
```

### GPGキーのパスフレーズ入力で失敗するとき

以下のコマンド実行時。

```bash
echo 'test' | gpg --clearsign
```

以下のエラーが発生した。

```log
gpg: signing failed: Inappropriate ioctl for device
```

fishでは以下のコマンドを実行し、環境変数を設定する。

```bash
set -gx GPG_TTY (tty)
```

参考

- [GPG キーのエクスポート/インポート - Smile Engineering Blog](https://smile-jsp.hateblo.jp/entry/2020/12/13/132318)
- [署名付きcommitでerror: gpg failed to sign the dataになるとき．](https://zenn.dev/taqxlow/articles/91c4da91e67a1b)
- [GPG won't work with fish · Issue #6643 · fish-shell/fish-shell](https://github.com/fish-shell/fish-shell/issues/6643)
