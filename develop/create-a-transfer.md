---
title: Tworzenie transferu
description: Jak utworzyć przeniesienie subskrypcji dla klienta.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d459a0a96912ab27f312bc73af16af2d4fdb518c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973710"
---
# <a name="create-a-transfer"></a>Tworzenie transferu

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/transfery HTTP/1.1                    |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru ścieżki, aby zidentyfikować klienta.

| Nazwa            | Typ     | Wymagane | Opis                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **identyfikator klienta** | ciąg   | Tak      | Identyfikator GUID sformatowany jako identyfikator klienta, który identyfikuje klienta.             |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano [właściwości TransferEntity](transfer-entity-resources.md) w treści żądania.

| Właściwość              | Typ          | Wymagane  | Opis                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| identyfikator                    | ciąg        | Nie    | Identyfikator transferEntity, który jest dostarczany po pomyślnym utworzeniu obiektu transferEntity.                               |
| createdTime (czas utworzenia)           | DateTime      | Nie    | Data utworzenia przeniesieniaJedność w formacie daty i godziny. Stosowane po pomyślnym utworzeniu transferEntity.      |
| lastModifiedTime      | DateTime      | Nie    | Data ostatniej aktualizacji transakcji transferEntity w formacie daty i godziny. Stosowane po pomyślnym utworzeniu transferEntity. |
| lastModifiedUser      | ciąg        | Nie    | Użytkownik, który ostatnio zaktualizował transferEntity. Stosowane po pomyślnym utworzeniu transferEntity.                          |
| Customername          | ciąg        | Nie    | Opcjonalny. Nazwa klienta, którego subskrypcje są przenoszone.                                              |
| customerTenantId      | ciąg        | Nie    | Identyfikator GUID sformatowany jako identyfikator klienta, który identyfikuje klienta. Stosowane po pomyślnym utworzeniu transferEntity.         |
| partnertenantid       | ciąg        | Nie    | Identyfikator GUID sformatowany jako identyfikator partnera, który identyfikuje partnera.                                                                   |
| sourcePartnerName (Nazwa partycji źródłowej)     | ciąg        | Nie    | Opcjonalny. Nazwa organizacji partnera, który inicjuje przeniesienie.                                           |
| sourcePartnerTenantId | ciąg        | Tak   | Identyfikator GUID sformatowany jako identyfikator partnera, który identyfikuje partnera inicjujące przeniesienie.                                           |
| targetPartnerName (nazwa_serwera_docelowego)     | ciąg        | Nie    | Opcjonalny. Nazwa organizacji partnera, której celem jest przeniesienie.                                         |
| targetPartnerTenantId | ciąg        | Tak   | Identyfikator GUID sformatowany jako partner-id, który identyfikuje partnera, do którego jest skierowany transfer.                                  |
| lineItems             | Tablica obiektów | Tak| Tablica zasobów [TransferLineItem.](transfer-entity-resources.md#transferlineitem)                                   |
| status                | ciąg        | Nie    | Stan transferEntity. Możliwe wartości to "Aktywne" (można je usunąć/przesłać) i "Ukończono" (zostało już zakończone). Stosowane po pomyślnym utworzeniu transferEntity.|

W tej tabeli [opisano właściwości TransferLineItem](transfer-entity-resources.md#transferlineitem) w treści żądania.

|      Właściwość       |            Typ             | Wymagane | Opis                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| identyfikator                   | ciąg                     | Nie       | Unikatowy identyfikator elementu wiersza przeniesienia. Stosowane po pomyślnym utworzeniu transferEntity.|
| subscriptionId       | ciąg                     | Tak      | Identyfikator subskrypcji.                                                                         |
| quantity             | int                        | Nie       | Liczba licencji lub wystąpień.                                                                 |
| billingCycle         | Obiekt                     | Nie       | Typ cyklu rozliczeniowego ustawiony dla bieżącego okresu.                                                |
| Friendlyname         | ciąg                     | Nie       | Opcjonalny. Przyjazna nazwa elementu zdefiniowanego przez partnera w celu uujednoznania.                |
| partnerIdOnRecord    | ciąg                     | Nie       | PartnerId on Record (IDENTYFIKATOR MPN) przy zakupie, który ma miejsce po zaakceptowaniu przeniesienia.              |
| offerId              | ciąg                     | Nie       | Identyfikator oferty.                                                                                |
| addonItems           | Lista obiektów **TransferLineItem** | Nie | Kolekcja elementów wiersza transferEntity dla dodatków, które zostaną przeniesione wraz z subskrypcją podstawową, która jest przesyłana. Stosowane po pomyślnym utworzeniu transferEntity.|
| transferError        | ciąg                     | Nie       | Zastosowane po transferEntity jest akceptowana, jeśli wystąpi błąd.                                        |
| status               | ciąg                     | Nie       | Stan lineitem w transferEntity.                                                    |

### <a name="request-example"></a>Przykład żądania

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Expect: 100-continue

{
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lineItems": [
        {
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "partnerIdOnRecord": "517285"
        },
        {
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "partnerIdOnRecord": "517285"
        }
    ]
}
```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca wypełniony [zasób TransferEnity](transfer-entity-resources.md) w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 201 Created
Content-Length: 138
Content-Type: application/json; charset=utf-8
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US,en-US
{
    "id": "67c5b05b-09b5-47ba-9047-5056fe2afa4f",
    "status": "Active",
    "createdTime": "2020-03-24T20:44:14.9602781Z",
    "lastModifiedTime": "2020-03-24T20:44:15Z",
    "customerTenantId": "823c6c3f-9259-4d51-bae2-5dd06743177f",
    "partnertenantid": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lastModifiedUser": "d0648481-b615-45c9-8cd1-ff87940dbdc4",
    "lineItems": [
        {
            "id": 0,
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "offerId": "50E9A47A-7B4D-4970-9D90-CAE927F53753",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 for Sales Enterprise Attach to Qualifying Dynamics 365 Base Offer",
            "quantity": 1,
            "addonItems": [
                {
                    "id": 0,
                    "subscriptionId": "D738C6C9-DDBD-46E9-B316-65F9D9B3ECB4",
                    "offerId": "2BCF9FE8-8B65-4FCF-9240-419203FB8CF4",
                    "billingCycle": "annual",
                    "friendlyName": "Dynamics 365 - Additional Production Instance (Qualified Offer)",
                    "quantity": 4
                }
            ]
        },
        {
            "id": 0,
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "offerId": "455DDD41-32ED-4E2D-B3A2-BBCB22CAA467",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 Customer Engagement Plan Patch",
            "quantity": 8,
            "addonItems": []
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "TransferEntity"
    }
}
```
