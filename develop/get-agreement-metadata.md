---
title: Pobieranie metadanych umowy dla umowy dotyczącej platformy Microsoft Cloud
description: W tym artykule wyjaśniono, jak uzyskać metadane umów dla Microsoft Cloud umowy.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c6a404eb38c4c31d3e69bb598872b932d8985529
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768049"
---
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a>Pobieranie metadanych umowy dla umowy dotyczącej platformy Microsoft Cloud

**Dotyczy**

- Centrum partnerskie

> [!NOTE]
> Zasób **AgreementMetaData** jest obecnie obsługiwany przez centrum partnerskie tylko w chmurze publicznej firmy Microsoft. Nie dotyczy:
> - Centrum partnerskie obsługiwane przez firmę 21Vianet
> - Centrum partnerskie dla Microsoft Cloud Niemcy
> - Centrum partnerskie Microsoft Cloud for US Government

## <a name="prerequisites"></a>Wymagania wstępne

- W przypadku korzystania z zestawu SDK platformy .NET w programie Partner Center wymagany jest program w wersji 1,9 lub nowszej.

- W przypadku korzystania z zestawu SDK języka Java Centrum partnerskiego wymagana jest wersja 1,8 lub nowsza.

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](./partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie aplikacji i użytkowników..

## <a name="net-version-114-or-newer"></a>.NET (wersja 1,14 lub nowsza)

Aby pobrać metadane umowy dla Microsoft Cloud umowy:

1. Najpierw pobierz kolekcję **IAggregatePartner. AgreementDetails** .

2. Wywołaj metodę **ByAgreementType** , aby odfiltrować kolekcję do umowy Microsoft Cloud.

3. Na koniec Wywołaj metodę **Get** lub **GetAsync** .

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

Pełny przykład można znaleźć w klasie [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) z projektu [aplikacji testowej konsoli](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .

## <a name="net-version-19---113"></a>.NET (wersja 1,9-1,13)

Aby pobrać metadane umów dla Microsoft Cloud umowy:

Najpierw pobierz kolekcję **IAggregatePartner. AgreementDetails** , a następnie wywołaj metody **Get** lub **GetAsync** . Następnie wyszukaj element w kolekcji, który odpowiada umowie Microsoft Cloud:

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Aby pobrać metadane umów dla Microsoft Cloud umowy:

Najpierw wywołaj funkcję **IAggregatePartner. getAgreementDetails** , a następnie wywołaj funkcję **Get** . Następnie wyszukaj element w kolekcji, który odpowiada umowie Microsoft Cloud:

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

Pełny przykład można znaleźć w klasie [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) z projektu [aplikacji testowej konsoli](https://github.com/Microsoft/Partner-Center-Java-Samples) .

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Aby pobrać metadane umów dla Microsoft Cloud umowy:

Użyj polecenia [**Get-PartnerAgreementDetail**](/powershell/module/partnercenter/get-partneragreementdetail) . Następnie wyszukaj element w kolekcji, który odpowiada umowie Microsoft Cloud:

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest-request"></a>Żądanie REST

Aby pobrać metadane umowy Microsoft Cloud, najpierw Utwórz żądanie REST w celu pobrania kolekcji **AgreementMetaData** . Następnie wyszukaj element w kolekcji, który odpowiada umowie Microsoft Cloud.

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{ BASEURL \}*](partner-center-rest-urls.md)/V1/Agreements http/1.1 |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

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

Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów **AgreementMetaData** w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

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

Aby zidentyfikować zasób w odpowiedzi, który odpowiada umowie Microsoft Cloud, poszukaj zasobu, którego właściwość **agreementtype** ma wartość "MicrosoftCloudAgreement".
