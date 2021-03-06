---
title: Validere 
description: Operasjoner for å validere skjemasett
weight: 10
---

## Validering utføres med VALIDATE på message
Følgende request validerer en melding sitt skjemasett.

Validering av meldinger er kun mulig for skjemasett som er under utfylling.

Når valideringen er utført returneres `HTTP 200` med en body som inneholder resultatet av valideringen.

Header
```HTTP
GET https://www.altinn.no/api/{who}/messages/{messageid}/validate HTTP/1.1
Content-Type: application/hal+json
ApiKey: myKey
```
For vellykket validering uten feil vil `Success` være satt til `true` og `ValidationWarnings` vil inneholde en liste over alle advarsler skjemaene gir.

Body 
```JSON
{
    "Success": true,
    "ValidationErrors": [],
    "ValidationWarnings": [
        {
            "FieldName": "FieldNameExample1",
            "ErrorMessage": "String example 1."
        },
        {
            "FieldName": "FieldNameExample2",
            "ErrorMessage": "String example 2."
        },
        {
            "FieldName": "FieldNameExample3",
            "ErrorMessage": "String example 3."
        }
    ]
}
```

For feilende validering vil `Success` være satt til `false` og `ValidationWarnings`/`ValidationErrors` vil inneholde en liste over alle advarsler/feilmeldinger skjemaene gir.

Body 
```JSON
{
    "Success": false,
    "ValidationErrors": [
        {
            "FieldName": "FieldNameExample1",
            "ErrorMessage": "String example 1."
        },
        {
            "FieldName": "FieldNameExample2",
            "ErrorMessage": "String example 2."
        },
        {
            "FieldName": "FieldNameExample3",
            "ErrorMessage": "String example 3."
        }
    ],
    "ValidationWarnings": [
        {
            "FieldName": "FieldNameExample1",
            "ErrorMessage": "String example 1."
        },
        {
            "FieldName": "FieldNameExample2",
            "ErrorMessage": "String example 2."
        },
        {
            "FieldName": "FieldNameExample3",
            "ErrorMessage": "String example 3."
        }
    ]
}
```