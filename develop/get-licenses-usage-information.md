---
title: Pobieranie informacji dotyczących użycia licencji
description: Jak uzyskać informacje o użyciu licencji na poziomie obciążenia dla pakietu Office i usługi Dynamics.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a144fd078a36289e4a2c70880817b1f0ca627e8a
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768161"
---
# <a name="get-licenses-usage-information"></a>Pobieranie informacji dotyczących użycia licencji

**Dotyczy**

- Centrum partnerskie

Jak uzyskać informacje o użyciu licencji na poziomie obciążenia dla pakietu Office i usługi Dynamics.

## <a name="prerequisites"></a>Wymagania wstępne

Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Analytics/Commercial/Usage/License/http/1.1 |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="uri-parameters"></a>Parametry identyfikatora URI

| Parametr         | Typ     | Opis | Wymagane |
|-------------------|----------|-------------|----------|
| top (pierwsze)               | ciąg   | Liczba wierszy danych do zwrócenia w żądaniu. Wartość maksymalna i wartość domyślna, jeśli nie zostanie określona, to 10000. Jeśli zapytanie zawiera więcej wierszy, treść odpowiedzi obejmuje następny link, którego można użyć do żądania następnej strony danych. | Nie |
| Pomiń              | int      | Liczba wierszy do pominięcia w zapytaniu. Użyj tego parametru, aby uzyskać stronę z dużymi zestawami danych. Na przykład: Top = 10000 i Skip = 0 pobiera pierwsze 10000 wierszy danych, Top = 10000 i Skip = 10000 pobiera następne 10000 wierszy danych i tak dalej. | Nie |
| filter            | ciąg   | Parametr *Filter* żądania zawiera jedną lub więcej instrukcji, które filtrują wiersze w odpowiedzi. Każda instrukcja zawiera pole i wartość, które są skojarzone z **`eq`** **`ne`** operatorami or, a instrukcje można łączyć za pomocą **`and`** lub **`or`** . Oto przykładowe parametry *filtru* :<br/><br/>*Filter = workloadCode EQ "SFB"*<br/><br/>*Filter = workloadCode EQ "SFB"* lub (*Channel EQ "Odsprzedawca"*)<br/><br/>Można określić następujące pola:<br/><br/>**workloadCode**<br/>**Nr obciążenia**<br/>**Kod servicecode**<br/>**serviceName**<br/>**ukierunkowan**<br/>**customerTenantId**<br/>**customerName**<br/>**Produktu**<br/>**productName** | Nie |
| GroupBy           | ciąg   | Instrukcja, która stosuje agregację danych tylko do określonych pól. Można określić następujące pola:<br/><br/>**workloadCode**<br/>**Nr obciążenia**<br/>**Kod servicecode**<br/>**serviceName**<br/>**channelcustomerTenantId**<br/>**customerName**<br/>**Produktu**<br/>**productName**<br/><br/>Zwracane wiersze danych będą zawierać pola określone w parametrze *GroupBy* , a także następujące:<br/><br/>**licensesActive**<br/>**licensesQualified** | Nie |
| processedDateTime | DateTime | Jeden może określać datę przetworzenia danych użycia. Wartość domyślna to najnowsza Data przetworzenia danych | Nie |

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/usage/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera następujące pola zawierające dane dotyczące użycia licencji.

| Pole             | Typ     | Opis                                   |
|-------------------|----------|-----------------------------------------------|
| workloadCode      | ciąg   | Kod obciążenia                                 |
| Nr obciążenia      | ciąg   | Nazwa obciążenia                                 |
| Kod servicecode       | ciąg   | Kod usługi                                  |
| serviceName       | ciąg   | Nazwa usługi                                  |
| ukierunkowan           | ciąg   | Nazwa kanału, odsprzedawcy                        |
| customerTenantId  | ciąg   | Unikatowy identyfikator dla klienta            |
| customerName      | ciąg   | Nazwa klienta                                 |
| productId         | ciąg   | Unikatowy identyfikator produktu             |
| productName       | ciąg   | Nazwa produktu                                  |
| licensesActive    | długi     | Liczba aktywnych licencji na obciążenie        |
| licensesQualified | długi     | Liczba kwalifikowanych licencji dla obciążenia |
| processedDateTime | DateTime | Data ostatniego przetworzenia danych         |

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

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
      "workloadCode": "SPO",
      "workloadName": "SharePoint",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
      "productName": "OFFICE 365 ENTERPRISE E3",
      "licenseActive": 0,
      "licensesQualified": 1
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "EXO",
      "workloadName": "Exchange",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "45A2423B-E884-448D-A831-D9E139C52D2F",
      "productName": "EXCHANGE ONLINE PROTECTION",
      "licenseActive": 0,
      "licensesQualified": 1
    }
}
```
