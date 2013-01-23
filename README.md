# SSHKey

Generate private and public SSH keys (RSA and DSA supported) using pure Ruby.

	gem install sshkey

Tested on the following Rubies: MRI 1.8.7, 1.9.2, 1.9.3, 2.0.0, REE, JRuby (1.7.2 or later), Rubinius. Ruby must be compiled with OpenSSL support.

[![Build Status](https://secure.travis-ci.org/bensie/sshkey.png)](http://travis-ci.org/bensie/sshkey)

## Usage

### Generate a new key

When generating a new keypair the default key type is 2048-bit RSA, but you can supply the `type` (RSA or DSA) and `bits` in the options.
You can also (optionally) supply a `comment` or `passphrase`:

```ruby
k = SSHKey.generate

k = SSHKey.generate(:type => "DSA", :bits => 1024, :comment => "foo@bar.com", :passphrase => "foobar")
```

### Use your existing key

Return an SSHKey object from an existing RSA or DSA private key (provided as a string)

```ruby
k = SSHKey.new(File.read("~/.ssh/id_rsa"), :comment => "foo@bar.com")
```

### The SSHKey object

#### Private and public keys

Fetch the private and public keys as strings. Note that the `public_key` is the RSA or DSA public key, not an SSH public key.

```ruby
k.private_key
# => "-----BEGIN RSA PRIVATE KEY-----\nMIIEoAIBAAKCAQEAvR7l72CT7UBP6P+02Iut8gKKbKyekz/pQxnckPp1VafuaIwC\nMvYfP4ffVJTcY5IhU9mISNxZf6YDQ0TuD1aOrZYG9wsIgGY0nXhOUZxe/Q5I+V7D\nOI/hSzKF7W0cNCvaJPUSo8+soCLNSQ5mjnV3sRZ6uJwGFN30i1GulqHHKkx3vGxb\niaAL9YG58dPSbPGHFTA/epqUyd1fzCuWHyL9dHW7aw4RroNyEtVdiftAQfaK20I2\nueeDfuEtCPaxQYFQqbz5kKnXQx3fwHRpC7/84xHxsrY576evGxHw4p5EJD37scNN\ncneTG3Ly79/VVSAlrSm6ltutx0+S70scCqK0ewIDAQABAoH/MjwC15LPuDVdBIbn\ngp2XlrEWE8fGV1ainzA/ZkMg55+ztBF8hAzcQAPXTqA76jbmo18k1DWzkDSIqVWl\n5m0XeQRg1T4ZBAIh97H9G7BtispAl/yT3nJZZaAF8wsIctMzHp36VYjUUbTs0nsA\nwtZw9JkEAAVxmBlc26TWuyw9uv4fYXuR+uOsWH8jTTVPvxM9FaCCdK+dOMnswm7Y\nlOAlJj5dANkB2KPwIeE461ThyMo9GHEjpsvciMhKLuBoTSucNkhdgapAmYTSI+/1\nf1cA/KEdCMs9ANr1HFujeS01+N1Xrw/yW6EazaDN1oFHCVORtlB295Eac0Wq6y/P\npf1BAoGBAPIw4HQWsolU3f4FdIvc2POAcSJDRgt++I9Qt/QXq1SJ2dGKIveFiJgo\nZjCfHQFVZ8xl64cLzQ1WagZA1JBbbk9g5RxHDxRv7q+Kn3ogugDo9GUoQvpuuAU6\nXHoR/mLinDorJUnttL3U49xTMfrrut4qkUg+daBVptPtylpio6EDAoGBAMfnYq08\nfd/cPEQ2XPeswgtzXsKNLqA6UXBM7ZauKaFLByjy8peMMF6JPOYlBKQif5k+Egmu\nWIe8oTm8Nn5Ymt32bEd+MkHUC7kFzQeiXnM3u0oKzJMXLAvjSTs296g50YM5zJTC\nl64ACQmQOLZ9tdKorl52ZcmdbBEcZ2uwRvkpAoGAKhs5SrWPgLTSi5FjO9W/mkYg\nZTaQ/PqsOC5ubO+Yh/AXgIiln6cFon6Tlax0HIE+tJibpDT3B3SYplGrIxXiTcao\nzovEIWd8deSB6Xe7HuFhbBzd2DBbqf0FiuuJ8KM5ShuqNfovzDkxDGMic198c5eu\n/oJtbNy3Tm0vGxu/GwUCgYAgmRPXShkAq0pMmUzZups+AMdAFIO47ymelXzc6HOz\ncKevPsbefabZk6mRohG6rkF+fMe2Om8HW3QzFQUR32MJtQh9NA//+hMbTd3cU9bx\nFPJ+pXostkehfKPReyoxjZQjwQYicAUKA8l1fMYyxBclTgp5Lvd0RC5+L9KRlgJM\n2QKBgGVIWRNVpGg38dDqdq/4ue1BoTFhqoMGi6WQm3xa+NH+lyJGacdUhGRz8PxN\nhVKpIj8ljg2Rq/CA9qSgL/Z9rhn8QUMWULuAroCp0S2pMBtZ2RB+Mg2FdVFR9/Ft\nfG7co6mKUGkFPtr48EMfeKY88BRsp3yGOsROGdDsCHItjOVH\n-----END RSA PRIVATE KEY-----\n"

k.public_key
# => "-----BEGIN PUBLIC KEY-----\nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAvR7l72CT7UBP6P+02Iut\n8gKKbKyekz/pQxnckPp1VafuaIwCMvYfP4ffVJTcY5IhU9mISNxZf6YDQ0TuD1aO\nrZYG9wsIgGY0nXhOUZxe/Q5I+V7DOI/hSzKF7W0cNCvaJPUSo8+soCLNSQ5mjnV3\nsRZ6uJwGFN30i1GulqHHKkx3vGxbiaAL9YG58dPSbPGHFTA/epqUyd1fzCuWHyL9\ndHW7aw4RroNyEtVdiftAQfaK20I2ueeDfuEtCPaxQYFQqbz5kKnXQx3fwHRpC7/8\n4xHxsrY576evGxHw4p5EJD37scNNcneTG3Ly79/VVSAlrSm6ltutx0+S70scCqK0\newIDAQAB\n-----END PUBLIC KEY-----\n"
```

Fetch the SSH public key as a string.

```ruby
k.ssh_public_key
# => "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC9HuXvYJPtQE/o/7TYi63yAopsrJ6TP+lDGdyQ+nVVp+5ojAIy9h8/h99UlNxjkiFT2YhI3Fl/pgNDRO4PVo6tlgb3CwiAZjSdeE5RnF79Dkj5XsM4j+FLMoXtbRw0K9ok9RKjz6ygIs1JDmaOdXexFnq4nAYU3fSLUa6WoccqTHe8bFuJoAv1gbnx09Js8YcVMD96mpTJ3V/MK5YfIv10dbtrDhGug3IS1V2J+0BB9orbQja554N+4S0I9rFBgVCpvPmQqddDHd/AdGkLv/zjEfGytjnvp68bEfDinkQkPfuxw01yd5MbcvLv39VVICWtKbqW263HT5LvSxwKorR7"
```

#### Encryption

If a passcode is set when a key is generated or by setting the `passcode` accessor, you can
fetch the encrypted version of the private key.

```ruby
k.passcode = "foo"
# => "foo"

k.encrypted_private_key
# => "-----BEGIN RSA PRIVATE KEY-----\nProc-Type: 4,ENCRYPTED\nDEK-Info: AES-128-CBC,748B766CFB185C3BD1D7E4D31113EBDA\n\ntWbfOuAjBlSZdq3kdJTLZJ7prjNWOKuGpeesNfVZDziIaZNCUakvgnUFdX3IZZnj\nEYITfjZ1TEUY3EkemL/57txiP3A4iOMDK2JGg8lp3G45x6c9XucJ2YxgvMye/ugP\n014MzLvBNunWq8TolkFj4gbc+WCqsyFqGdpRsf/hx7PcLDd2nvS5zxjBAPno87KN\nYgEnZYrpyl01ePucwFVWlrlGJdc0+F+0Ms5gpjMds56YL3Rwv9BlWzapVtrqN29r\nZg0otylPAyuGJOQ8srDOa+pbSySXvcdoKfR6xQ9fIB0tUfGgrH3c5O0/rEW7FSiO\n6ng4ntXXOKKkQfCezXQVvqMjKtKAbcKaPYAvrB2Gp2VIPUN5tN52nKuWvQWPA0P/\nm/uKiFkvzDWj8xMEOdzDAG9/7ysX+T5angvhfT23+NEdGIlPZLDRHI3f+2Itn99f\nvVoDYUXiyd5h7VwOTn6scebbvyPY8DiWpB/5iaU8WBPr7TVTl9n2z+Gmy4eg3wS0\nTU4hGlKv7MiITO2+dOCZTVrKn9/gTgmtyiLucb4huBH88Nsj4zWnTrVjMMBWsTUD\nkzvo9081zgDKKeawcbZYdI1Tc4epV7SMTHpx1ztzIlPdQ6kRaWomwMSarQeSlhJe\naFx67cde6M3Kc3LOgE0VT+3NvVLnkDwkytwnQKLd6oT3d1kFxWXjMwqiPbSzz3bf\nkOhG01gsJDXIzAgDlOlhE+Qlsd3yc734UIH98rTFMVB00HS36WLuz3hh+Ew4rsrf\nDIuRIdxL/4GVdQ8J5WpSoN0tF5iQD1wpEMU2vUjYjj9TZkhpOpnK3UVvbKd4WPsV\n956XJT7ZDvX4+pvHc5GJq/UX5h42kycY0hftUoLapXt5Nhb/fL8mUT8Eix184uiO\n5mA3fgRP3oGJ28N653X/+kL2YhXCeTd2VjkVhKruuoex96Igyt8W7wW5y7MOPezf\nwfo8IzidcJcDR1W4OEOXr+oDlCE1CLGCzmenR+AUIisqz45yb5G076l8PQkI3NWC\nBhT1YbTds4QzrndIDZgMm65ZCaklm+FVHWV61rXd9rlugcq+flQuXAE/EnFtySMc\n3lztrzXulLXzgLrYG355JbQFddwehO7LdxKZA9LHC9/odcoVI9RBj1CzshYtlftR\nn56nxPTIxRTVjQdgCZ6VcjZhwv1I904NtGm4SZupiShXsbHzAfaeJ54GMq4PRlgN\nmH7JrI9/puBb1dLD0XNgPtmYIo18v9e7g9o+un/wDtxCTxhQtD0npPo1IuW4cW7q\n07lZPwGkN2FD2PNTBGXeQ6/EXTHxlyFn62GSr+DmXu0O8MJS827Vd4b8QmKzRTxf\nFEmtVhiD15KlrQxwajmhqfY6KHRxbBuG/w7ioRr2Vl0G9NmKwmJkQO8dM+mJ8rVE\nsWvm8xVm1bowahzDVPnyFUUjuGNi6jFElkv8zvlQUoTcjSZHPrQSHuX742f5Spph\nLLCHdGZ2Ry8UGPlqKtvd6V/z25NsBgbuit+hNkBsdIztH7MVGAhKSMgk1FgXmKzV\nmZnPigq5WAHtIvojzI9NfZxU2Avif0yymXNtOnipw0sCJ0notN8NuGdQEmyxThqW\n-----END RSA PRIVATE KEY-----\n"
```

#### Comments

Keys can optionally have a comment that is shown as part of the public SSH key. Get or
set the key's comment with the `comment` accessor.

```ruby
k.comment
# => nil

k.comment = "me@me.com"
# => "me@me.com"

k.ssh_public_key
# => "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC9HuXvYJPtQE/o/7TYi63yAopsrJ6TP+lDGdyQ+nVVp+5ojAIy9h8/h99UlNxjkiFT2YhI3Fl/pgNDRO4PVo6tlgb3CwiAZjSdeE5RnF79Dkj5XsM4j+FLMoXtbRw0K9ok9RKjz6ygIs1JDmaOdXexFnq4nAYU3fSLUa6WoccqTHe8bFuJoAv1gbnx09Js8YcVMD96mpTJ3V/MK5YfIv10dbtrDhGug3IS1V2J+0BB9orbQja554N+4S0I9rFBgVCpvPmQqddDHd/AdGkLv/zjEfGytjnvp68bEfDinkQkPfuxw01yd5MbcvLv39VVICWtKbqW263HT5LvSxwKorR7 me@me.com"
```

#### Bit length

Determine the strength of the key in bits as an integer.

```ruby
k.bits
# => 2048
```

#### Fingerprints

It is often helpful to use a fingerprint to visually or programmatically check if one key
matches another. Fetch either an MD5 (OpenSSH default) or SHA1 fingerprint of the SSH public key.

```ruby
k.md5_fingerprint
# => "2a:89:84:c9:29:05:d1:f8:49:79:1c:ba:73:99:eb:af"

k.sha1_fingerprint
# => "e4:f9:79:f2:fe:d6:be:2d:ef:2e:c2:fa:aa:f8:b0:17:34:fe:0d:c0"
```

#### Randomart

Generate OpenSSH compatible ASCII art fingerprints - see http://www.opensource.apple.com/source/OpenSSH/OpenSSH-175/openssh/key.c (key_fingerprint_randomart function)

```ruby
puts k.randomart
+--[ RSA 2048]----+
|o+ o..           |
|..+.o            |
| ooo             |
|.++. o           |
|+o+ +   S        |
|.. + o .         |
|  . + .          |
|   . .           |
|    Eo.          |
+-----------------+
```

#### Original OpenSSL key object

Return the original `OpenSSL::PKey::RSA` or `OpenSSL::PKey::DSA` object.

http://www.ruby-doc.org/stdlib/libdoc/openssl/rdoc/classes/OpenSSL/PKey/RSA.html
http://www.ruby-doc.org/stdlib/libdoc/openssl/rdoc/classes/OpenSSL/PKey/DSA.html

```ruby
k.key_object
# => -----BEGIN RSA PRIVATE KEY-----\nMIIEowI...
```

### Validate existing SSH public keys

Determine if a given SSH public key is valid. Very useful to test user input of public keys to make sure they accurately copy/pasted the key. Just pass the SSH public key as a string.

```ruby
SSHKey.valid_ssh_public_key? "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC9HuXvYJPtQE/o/7TYi63yAopsrJ6TP+lDGdyQ+nVVp+5ojAIy9h8/h99UlNxjkiFT2YhI3Fl/pgNDRO4PVo6tlgb3CwiAZjSdeE5RnF79Dkj5XsM4j+FLMoXtbRw0K9ok9RKjz6ygIs1JDmaOdXexFnq4nAYU3fSLUa6WoccqTHe8bFuJoAv1gbnx09Js8YcVMD96mpTJ3V/MK5YfIv10dbtrDhGug3IS1V2J+0BB9orbQja554N+4S0I9rFBgVCpvPmQqddDHd/AdGkLv/zjEfGytjnvp68bEfDinkQkPfuxw01yd5MbcvLv39VVICWtKbqW263HT5LvSxwKorR7"
# => true
```

## Copyright

Copyright (c) 2011-2013 James Miller
