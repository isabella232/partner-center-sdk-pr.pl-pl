---
title: Pobieranie wszystkich informacji analitycznych dotyczących użycia platformy Azure
description: Jak uzyskać wszystkie informacje dotyczące analizy użycia platformy Azure.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 7fe987c7dc50d55b26cd72d5aead52963eb1cfbe
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760219"
---
# <a name="get-all-azure-usage-analytics-information"></a>Pobieranie wszystkich informacji analitycznych dotyczących użycia platformy Azure

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Jak uzyskać wszystkie informacje dotyczące analizy użycia platformy Azure dla klientów.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń użytkownika.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania |
|---------|-------------|
| **Pobierz** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry URI

|Parametr        |Typ                        |Opis               |
|:----------------|:---------------------------|:-------------------------|
|top (pierwsze)              | ciąg                     | Liczba wierszy danych do zwrócenia w żądaniu. Wartość maksymalna i wartość domyślna, jeśli nie zostanie określona, to 10000. Jeśli w zapytaniu znajduje się więcej wierszy, treść odpowiedzi zawiera następny link, za pomocą których można zażądać następnej strony danych.                        |
|Pomiń             | int                        | Liczba wierszy do pominięcia w zapytaniu. Ten parametr umożliwia stronicować duże zestawy danych. Na przykład `top=10000 and skip=0` program pobiera pierwsze 10 000 wierszy danych, pobiera kolejne `top=10000 and skip=10000` 10000 wierszy danych i tak dalej.                       |
|filter           | ciąg                     | Parametr *filtru* żądania zawiera co najmniej jedną instrukcje, które filtruje wiersze w odpowiedzi. Każda instrukcja zawiera pole i wartość, które są skojarzone z operatorami lub , a instrukcje można łączyć przy `eq` `ne` użyciu instrukcji lub `and` `or` . Można określić następujące ciągi:<br/><br/>                                                       `customerTenantId`<br/> `customerName`<br/> `subscriptionId`<br/> `subscriptionName`<br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/>**Przykład:**<br/> `.../usage/azure?filter=meterCategory eq 'Data Management'`<br/><br/> **Przykład:**<br/>`.../usage/azure?filter=meterCategory eq 'Data Management' or (usageDate le cast('2018-01-01', Edm.DateTimeOffset) and usageDate le cast('2018-04-01', Edm.DateTimeOffset))`                        |
|aggregationLevel | ciąg                    | Określa zakres czasu, dla którego mają zostać pobrane zagregowane dane. Może być jednym z następujących ciągów: `day` `week` , lub `month` . Jeśli nie zostanie on nieokreślony, wartość domyślna to `day` .<br/><br/>                                              Parametr `aggregationLevel` nie jest obsługiwany bez parametru `groupby` . Parametr `aggregationLevel` ma zastosowanie do wszystkich pól dat obecnych w tabeli `groupby` .                                                      |
|Orderby          |ciąg                     | Instrukcja, która nakazuje wartości danych wynikowych dla każdej instalacji. Składnia jest następująca: `...&orderby=field [order],field [order],...` Parametr `field` może być jednym z następujących ciągów:<br/><br/>                    `customerTenantId`<br/>`customerName`<br/>`subscriptionId`<br/>`subscriptionName`<br/>`usageDate`<br/>`resourceLocation`<br/>`meterCategory`<br/>`meterSubcategory`<br/>`meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/> Parametr *order* jest opcjonalny i może mieć wartość lub , aby określić kolejność rosnącą lub malejącą odpowiednio dla `asc` każdego `desc` pola. Wartość domyślna to `asc`.<br/><br/>**Przykład:**<br/> `...&orderby=meterCategory,meterUnit`                                                                                           |
|Groupby          |ciąg                    | Instrukcja, która stosuje agregację danych tylko do określonych pól. Można określić następujące pola:<br/><br/>                                                                                                                     `customerTenantId`<br/>`customerName`<br/> `subscriptionId` <br/> `subscriptionName` <br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit` <br/> `reservationOrderId` <br/> `reservationId` <br/> `consumptionMeterId` <br/> `serviceType` <br/><br/>Zwracane wiersze danych będą zawierać pola określone w `groupby`  parametrze i *wartości Quantity*.<br/><br/>Parametru `groupby` można używać z `aggregationLevel` parametrem .<br/><br/>**Przykład:**<br/>`...&groupby=meterCategory,meterUnit` |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [użycia platformy Azure.](partner-center-analytics-resources.md#csp-program-azure-usage-analytics)

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

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
