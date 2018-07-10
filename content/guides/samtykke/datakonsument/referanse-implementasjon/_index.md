---
title: Sha-256 Referanse-implementasjon
description: Altinns referanse-implementasjon for hashing av fødseslsnummer
weight: 30
---


## Altinns referanse-implementasjon for hashing av fødseslsnummer

Om UserToken er spesifisert i samtykke-forespørselen begrenser man forespørselen til ett enkelt fødselsnummer som kan gi samtykket.
Om ikke riktig fødselsnummer er logget inn vil sluttbrukeren bli omdirigert til innlogginssiden, og må logge inn på nytt med riktig fødselsnummer.

UserToken oppgies som en tekst-streng på 32 hexadesimale bokstaver. Tekst-strengen er en  Sha-256 hash av brukerens personnummer, uten mellomrom. For mer informasjon om Sha256 se [Wikipedia, SHA-2](https://en.wikipedia.org/wiki/SHA-2).

Under følger Altinns referanse-implementasjon for hashing av fødseslsnummer i C#:

```
string Sha256Hash(string value)
{
    StringBuilder sb = new StringBuilder();
    using (var hash = SHA256.Create())
    {
        Encoding enc = Encoding.UTF8;
        Byte[] result = hash.ComputeHash(enc.GetBytes(value));
        foreach (Byte b in result)
        {
            sb.Append(b.ToString("x2"));
        }
    }
    return sb.ToString();
}
```

Ved riktig bruk vil UserToken for fødselsnummer 01234567891 se slik ut:

``
UserToken=2edb6e72d5aaf346259b36a79bdb8a6cde1d7e537b92e6a2c60ffbb9ce93a4db
``
