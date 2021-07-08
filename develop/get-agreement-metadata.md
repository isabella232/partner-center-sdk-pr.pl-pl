---
title: Pobieranie metadanych umowy dla umowy dotyczącej platformy Microsoft Cloud
description: W tym artykule wyjaśniono, jak uzyskać metadane umowy dla Umowa dotycząca platformy Microsoft Cloud.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 2588327e72a13de75eb9e02675edbd535491adc4
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760797"
---
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a>Pobieranie metadanych umowy dla umowy dotyczącej platformy Microsoft Cloud

**Dotyczy:** Partner Center

**Nie dotyczy:** Partner Center obsługiwane przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Zasób **AgreementMetaData** jest obecnie obsługiwany Partner Center tylko w chmurze publicznej firmy Microsoft.

## <a name="prerequisites"></a>Wymagania wstępne

- Jeśli używasz zestawu SDK platformy Partner Center .NET, wymagana jest wersja 1.9 lub nowsza.

- Jeśli używasz zestawu SDK Partner Center Java, wymagana jest wersja 1.8 lub nowsza.

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](./partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie aplikacji i użytkowników.

## <a name="net-version-114-or-newer"></a>.NET (wersja 1.14 lub nowsza)

Aby pobrać metadane umowy dla Umowa dotycząca platformy Microsoft Cloud:

1. Najpierw pobierz **kolekcję IAggregatePartner.AgreementDetails.**

2. Wywołaj **metodę ByAgreementType,** aby filtrować kolekcję w Umowa dotycząca platformy Microsoft Cloud.

3. Na koniec wywołaj **metodę Get** lub **GetAsync.**

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

Kompletny przykład można znaleźć w klasie [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) w projekcie [aplikacji testowej konsoli.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)

## <a name="net-version-19---113"></a>.NET (wersja 1.9–1.13)

Aby pobrać metadane umowy dla Umowa dotycząca platformy Microsoft Cloud:

Najpierw pobierz **kolekcję IAggregatePartner.AgreementDetails,** a następnie wywołaj metody **Get** lub **GetAsync.** Następnie wyszukaj element w kolekcji, który odpowiada wartości Umowa dotycząca platformy Microsoft Cloud:

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Aby pobrać metadane umowy dla Umowa dotycząca platformy Microsoft Cloud:

Najpierw wywołaj **funkcję IAggregatePartner.getAgreementDetails,** a następnie wywołaj **funkcję get.** Następnie wyszukaj element w kolekcji, który odpowiada wartości Umowa dotycząca platformy Microsoft Cloud:

```java
// IAggregatePartner partnerOperations;

ResourceCollection<AgreementMetaData> agreements = partnerOperations.getAgreements().get();

AgreementMetaData microsoftCloudAgreement;

for (AgreementMetaData metadata : agreements)
{
    if(metadata.getAgreementType() == AgreementType.MicrosoftCloudAgreement)
    {
        microsoftCloudAgreement = metadata;
    }
}
```

Kompletny przykład można znaleźć w klasie [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) w projekcie [aplikacji testowej konsoli.](https://github.com/Microsoft/Partner-Center-Java-Samples)

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Aby pobrać metadane umowy dla Umowa dotycząca platformy Microsoft Cloud:

Użyj polecenia [**Get-PartnerAgreementDetail.**](/powershell/module/partnercenter/get-partneragreementdetail) Następnie wyszukaj element w kolekcji, który odpowiada wartości Umowa dotycząca platformy Microsoft Cloud:

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest-request"></a>Żądanie REST

Aby pobrać metadane umowy dla Umowa dotycząca platformy Microsoft Cloud, najpierw utwórz żądanie REST w celu pobrania **kolekcji AgreementMetaData.** Następnie wyszukaj element w kolekcji, który odpowiada wartości Umowa dotycząca platformy Microsoft Cloud.

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreements HTTP/1.1 |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca kolekcję **zasobów AgreementMetaData** w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 1,
    "items": [
        {
            "templateId": "998b88de-aa99-4388-a42c-1b3517d49490",
            "agreementType": "MicrosoftCloudAgreement",
            "agreementLink": "https://docs.microsoft.com/partner-center/agreements",
            "versionRank": 0
        }
    ],
    "links": {
        "self": {
            "uri": "/agreements",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

Aby zidentyfikować zasób w odpowiedzi, który odpowiada właściwości Umowa dotycząca platformy Microsoft Cloud, poszukaj zasobu, którego właściwość **agreementType** ma wartość "MicrosoftCloudAgreement".
