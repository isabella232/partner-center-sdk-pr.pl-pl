---
title: Pobieranie wszystkich informacji analitycznych dotyczących użycia platformy Azure
description: Jak uzyskać wszystkie informacje dotyczące analizy użycia platformy Azure.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c281dcdeb93771a69a388ad64e1127b24156c809
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768169"
---
# <a name="get-all-azure-usage-analytics-information"></a>Pobieranie wszystkich informacji analitycznych dotyczących użycia platformy Azure

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Jak uzyskać wszystkie informacje dotyczące analizy użycia platformy Azure dla klientów.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie z poświadczeniami użytkownika.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania |
|---------|-------------|
| **Pobierz** | [*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/V1/Analytics/Usage/Azure http/1.1 |

### <a name="uri-parameters"></a>Parametry identyfikatora URI

|Parametr        |Typ                        |Opis               |
|:----------------|:---------------------------|:-------------------------|
|top (pierwsze)              | ciąg                     | Liczba wierszy danych do zwrócenia w żądaniu. Wartość maksymalna i wartość domyślna, jeśli nie zostanie określona, to 10000. Jeśli zapytanie zawiera więcej wierszy, treść odpowiedzi obejmuje następny link, którego można użyć do żądania następnej strony danych.                        |
|Pomiń             | int                        | Liczba wierszy do pominięcia w zapytaniu. Użyj tego parametru, aby uzyskać stronę z dużymi zestawami danych. Na przykład program `top=10000 and skip=0` Pobiera pierwsze 10000 wierszy danych, `top=10000 and skip=10000` pobiera następne 10000 wierszy danych i tak dalej.                       |
|filter           | ciąg                     | Parametr *Filter* żądania zawiera jedną lub więcej instrukcji, które filtrują wiersze w odpowiedzi. Każda instrukcja zawiera pole i wartość, które są skojarzone z `eq` `ne` operatorami or, a instrukcje można łączyć za pomocą `and` lub `or` . Można określić następujące ciągi:<br/><br/>                                                       `customerTenantId`<br/> `customerName`<br/> `subscriptionId`<br/> `subscriptionName`<br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/>**Przykład:**<br/> `.../usage/azure?filter=meterCategory eq 'Data Management'`<br/><br/> **Przykład:**<br/>`.../usage/azure?filter=meterCategory eq 'Data Management' or (usageDate le cast('2018-01-01', Edm.DateTimeOffset) and usageDate le cast('2018-04-01', Edm.DateTimeOffset))`                        |
|aggregationLevel | ciąg                    | Określa zakres czasu, dla którego mają zostać pobrane zagregowane dane. Może być jednym z następujących ciągów: `day` , `week` , lub `month` . Jeśli nie zostanie określony, wartość domyślna to `day` .<br/><br/>                                              `aggregationLevel`Parametr nie jest obsługiwany bez `groupby` . Ten `aggregationLevel` parametr ma zastosowanie do wszystkich pól daty znajdujących się w `groupby` .                                                      |
|OrderBy          |ciąg                     | Instrukcja, która porządkuje wartości danych wynikowych dla każdej instalacji. Składnia jest następująca: `...&orderby=field [order],field [order],...` `field`Parametr może być jednym z następujących ciągów:<br/><br/>                    `customerTenantId`<br/>`customerName`<br/>`subscriptionId`<br/>`subscriptionName`<br/>`usageDate`<br/>`resourceLocation`<br/>`meterCategory`<br/>`meterSubcategory`<br/>`meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/> Parametr *Order* jest opcjonalny i może mieć wartość `asc` lub `desc` , aby określić kolejność rosnącą lub malejącą dla każdego pola. Wartość domyślna to `asc`.<br/><br/>**Przykład:**<br/> `...&orderby=meterCategory,meterUnit`                                                                                           |
|GroupBy          |ciąg                    | Instrukcja, która stosuje agregację danych tylko do określonych pól. Można określić następujące pola:<br/><br/>                                                                                                                     `customerTenantId`<br/>`customerName`<br/> `subscriptionId` <br/> `subscriptionName` <br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit` <br/> `reservationOrderId` <br/> `reservationId` <br/> `consumptionMeterId` <br/> `serviceType` <br/><br/>Zwracane wiersze danych będą zawierać pola określone w `groupby`  parametrze, a także *ilość*.<br/><br/>`groupby`Parametru można użyć z `aggregationLevel` parametrem.<br/><br/>**Przykład:**<br/>`...&groupby=meterCategory,meterUnit` |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [użycia platformy Azure](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) .

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
{
  "customerTenantId": "39A1DFAC-4969-4F31-AF94-D76588189CFE",
  "customerName": "A",
  "subscriptionId": "EC649980-D623-49F5-B7C1-80CC772B83A8",
  "subscriptionName": "AZURE PURCHSE SAMPLE APP",
  "usageDate": "2018-05-27T00:00:00",
  "resourceLocation": "useast",
  "meterCategory": "Data Management",
  "meterSubcategory": "None",
  "meterUnit": "10,000s",
  "reservationOrderId": "",
  "reservationId": "",
  "consumptionMeterId": "",
  "serviceType": "",
  "quantity": 20
}
```

## <a name="see-also"></a>Zobacz też

- [Analiza Centrum partnerskiego — zasoby](partner-center-analytics-resources.md)
