---
title: Pobieranie informacji dotyczących wdrażania licencji partnera
description: Jak uzyskać informacje o wdrożeniu licencji partnerów zagregowane w celu uwzględnienia wszystkich klientów.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 229f63d4df4f59cd0fde2bd0fc5e3f10cf6b25c0
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768433"
---
# <a name="get-partner-licenses-deployment-information"></a>Pobieranie informacji dotyczących wdrażania licencji partnera

**Dotyczy**

- Centrum partnerskie

Jak uzyskać informacje o wdrożeniu licencji partnerów zagregowane w celu uwzględnienia wszystkich klientów.

> [!NOTE]
> Ten scenariusz został zastąpiony przez [uzyskanie informacji o wdrożeniu licencji](get-licenses-deployment-information.md).

## <a name="prerequisites"></a>Wymagania wstępne

Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.

## <a name="c"></a>C\#

Aby pobrać zagregowane dane dotyczące wdrożenia licencji, należy najpierw pobrać interfejs do operacji zbierania danych analitycznych na poziomie partnera ze [**IAggregatePartner. Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) właściwości. Następnie można pobrać interfejs do kolekcji analizy licencji poziomu partnera z właściwości [**licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) . Na koniec Wywołaj metodę [**Deployment. Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) , aby uzyskać zagregowane dane dotyczące wdrożenia licencji. Jeśli metoda powiedzie się, otrzymasz kolekcję obiektów [**PartnerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) .

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesDeploymentAnalytics = partnerOperations.Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                           |
|---------|---------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Analytics/licenses/Deployment http/1.1 |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [PartnerLicensesDeploymentInsights](analytics-resources.md#partnerlicensesdeploymentinsights) , które zawierają informacje na temat wdrożonych licencji.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 102030524
Date: Tue, 14 Mar 2017 17:55:01 GMT

{
    "totalCount": 2,
    "items": [{
            "proratedDeploymentPercent": 0.0,
            "licensesSold": 343,
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesDeploymentInsights"
            }
        }, {
            "proratedDeploymentPercent": 1.0,
            "licensesSold": 4464,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesDeploymentInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
