---
title: Pobieranie informacji dotyczących wdrażania licencji
description: How to get deployment information for Office and Dynamics licenses (Jak uzyskać informacje o wdrażaniu Office licencji usługi Dynamics).
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c47ab4f839c102c7a7bcab0169bf13955ab49beb97c48800e882598714347e67
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990719"
---
# <a name="get-licenses-deployment-information"></a>Pobieranie informacji dotyczących wdrażania licencji

How to get deployment information for Office and Dynamics licenses (Jak uzyskać informacje o wdrażaniu Office licencji usługi Dynamics).

## <a name="prerequisites"></a>Wymagania wstępne

Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1 |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="uri-parameters"></a>Parametry URI

| Parametr         | Typ     | Opis | Wymagane |
|-------------------|----------|-------------|----------|
| top (pierwsze)               | ciąg   | Liczba wierszy danych do zwrócenia w żądaniu. Wartość maksymalna i wartość domyślna, jeśli nie zostanie określona, to 10000. Jeśli w zapytaniu znajduje się więcej wierszy, treść odpowiedzi zawiera następny link, za pomocą których można zażądać następnej strony danych. | Nie |
| Pomiń              | int      | Liczba wierszy do pominięcia w zapytaniu. Ten parametr umożliwia stronicować duże zestawy danych. Na przykład wartości top=10000 i skip=0 pobierają pierwsze 10000 wierszy danych, top=10000, a skip=10000 pobiera następne 10000 wierszy danych i tak dalej. | Nie |
| filter            | ciąg   | Parametr *filtru* żądania zawiera co najmniej jedną instrukcje filtrują wiersze w odpowiedzi. Każda instrukcja zawiera pole i wartość, które są skojarzone z operatorami lub , a instrukcje mogą być łączone przy `eq` `ne` użyciu instrukcji lub `and` `or` . Oto kilka przykładowych *parametrów filtru:*<br/><br/> *filter=serviceCode eq 'O365'*<br/> *filter=serviceCode eq 'O365'* or (*channel eq 'Reseller'*)<br/><br/> Można określić następujące pola:<br/><br/>**kod usługi**<br/>**Servicename**<br/>**Kanał**<br/>**customerTenantId**<br/>**Customername**<br/>**Productid**<br/>**Productname**  | Nie |
| Groupby           | ciąg   | Instrukcja, która stosuje agregację danych tylko do określonych pól. Można określić następujące pola:<br/><br/>**kod usługi**<br/>**Servicename**<br/>**Kanał**<br/>**customerTenantId**<br/>**Customername**<br/>**Productid**<br/>**Productname**<br/><br/> Zwrócone wiersze danych będą zawierać pola określone w parametrze *grupowania* i następujące elementy:<br/><br/>**licencjeWdeployed**<br/>**licensesSold**  | Nie |
| processedDateTime | DateTime | Można określić datę przetwarzania danych użycia. Wartość domyślna to najpóźniejsza data przetwarzania danych | Nie |

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/deployment/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia treść odpowiedzi zawiera następujące pola zawierające dane dotyczące wdrożonych licencji.

| Pole             | Typ     | Opis                           |
|-------------------|----------|---------------------------------------|
| kod usługi       | ciąg   | Kod usługi                          |
| Servicename       | ciąg   | Nazwa usługi                          |
| Kanał           | ciąg   | Nazwa kanału, odsprzedawca                |
| customerTenantId  | ciąg   | Unikatowy identyfikator klienta    |
| Customername      | ciąg   | Nazwa klienta                         |
| productId         | ciąg   | Unikatowy identyfikator produktu     |
| Productname       | ciąg   | Nazwa produktu                          |
| licencjeWdeployed  | długi     | Liczba wdrożonych licencji           |
| licensesSold      | długi     | Liczba sprzedanych licencji               |
| processedDateTime | DateTime | Data ostatniego przetworzenia danych |

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 4
Date: Wed, 24 Oct 2018 22:37:18 GMT
{
  "Value": [

{
      "processedDateTime": "2018-10-14T00:00:00",
      "serviceCode": "crm",
      "serviceName": "Microsoft Dynamics",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "54B84594-9C77-4499-8D65-5E0D5F410E78",
      "productName": "DYNAMICS AX TASK",
      "licensesDeployed": 0,
      "licensesSold": 9
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "D3B4FE1F-9992-4930-8ACB-CA6EC609365E",
      "productName": "DOMESTIC AND INTERNATIONAL CALLING PLAN",
      "licensesDeployed": 0,
      "licensesSold": 5
    }
],
  "@nextLink": null,
  "TotalCount": 2
}
```
