---
title: Pobieranie informacji dotyczących użycia licencji
description: Jak uzyskać informacje o użyciu licencji na poziomie obciążenia dla usług Office i Dynamics.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ea3658089ce7eb5c1ad7cc65c3db34f9b6353cdd
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445984"
---
# <a name="get-licenses-usage-information"></a>Pobieranie informacji dotyczących użycia licencji

Jak uzyskać informacje o użyciu licencji na poziomie obciążenia dla usług Office i Dynamics.

## <a name="prerequisites"></a>Wymagania wstępne

Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1 |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="uri-parameters"></a>Parametry URI

| Parametr         | Typ     | Opis | Wymagane |
|-------------------|----------|-------------|----------|
| top (pierwsze)               | ciąg   | Liczba wierszy danych do zwrócenia w żądaniu. Wartość maksymalna i wartość domyślna, jeśli nie zostanie określona, to 10000. Jeśli w zapytaniu znajduje się więcej wierszy, treść odpowiedzi zawiera następny link, za pomocą których można zażądać następnej strony danych. | Nie |
| Pomiń              | int      | Liczba wierszy do pominięcia w zapytaniu. Ten parametr umożliwia stronicować duże zestawy danych. Na przykład wartości top=10000 i skip=0 pobierają pierwsze 10000 wierszy danych, top=10000, a skip=10000 pobiera następne 10000 wierszy danych i tak dalej. | Nie |
| filter            | ciąg   | Parametr *filter* żądania zawiera co najmniej jedną instrukcje filtrują wiersze w odpowiedzi. Każda instrukcja zawiera pole i wartość, które są skojarzone z operatorami lub , a instrukcje mogą być łączone przy **`eq`** **`ne`** użyciu lub **`and`** **`or`** . Oto kilka przykładowych *parametrów filtru:*<br/><br/>*filter=workloadCode eq 'SFB'*<br/><br/>*filter=workloadCode eq 'SFB'* or (*channel eq 'Reseller'*)<br/><br/>Można określić następujące pola:<br/><br/>**workloadCode**<br/>**nazwa_obciążenia**<br/>**kod usługi**<br/>**Servicename**<br/>**Kanał**<br/>**customerTenantId**<br/>**Customername**<br/>**Productid**<br/>**Productname** | Nie |
| Groupby           | ciąg   | Instrukcja, która stosuje agregację danych tylko do określonych pól. Można określić następujące pola:<br/><br/>**workloadCode**<br/>**nazwa_obciążenia**<br/>**kod usługi**<br/>**Servicename**<br/>**channelcustomerTenantId**<br/>**Customername**<br/>**Productid**<br/>**Productname**<br/><br/>Zwrócone wiersze danych będą zawierać pola określone w parametrze *grupowania* i następujące elementy:<br/><br/>**licensesActive**<br/>**licensesQualified** | Nie |
| processedDateTime | DateTime | Można określić datę przetwarzania danych użycia. Wartość domyślna to najpóźniejsza data przetwarzania danych | Nie |

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

W przypadku powodzenia treść odpowiedzi zawiera następujące pola zawierające dane dotyczące użycia licencji.

| Pole             | Typ     | Opis                                   |
|-------------------|----------|-----------------------------------------------|
| workloadCode      | ciąg   | Kod obciążenia                                 |
| nazwa_obciążenia      | ciąg   | Nazwa obciążenia                                 |
| kod usługi       | ciąg   | Kod usługi                                  |
| Servicename       | ciąg   | Nazwa usługi                                  |
| Kanał           | ciąg   | Nazwa kanału, odsprzedawca                        |
| customerTenantId  | ciąg   | Unikatowy identyfikator klienta            |
| Customername      | ciąg   | Nazwa klienta                                 |
| productId         | ciąg   | Unikatowy identyfikator produktu             |
| Productname       | ciąg   | Nazwa produktu                                  |
| licensesActive    | długi     | Liczba aktywnych licencji na obciążenie        |
| licensesQualified | długi     | Liczba kwalifikowanych licencji dla obciążenia |
| processedDateTime | DateTime | Data ostatniego przetworzenia danych         |

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)

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
