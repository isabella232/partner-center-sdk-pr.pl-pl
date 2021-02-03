---
title: Tworzenie transferu
description: Jak utworzyć transfer subskrypcji dla klienta.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d5e70cc5b7ce4fcfa715f581a2151f0b8d1922b0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767761"
---
# <a name="create-a-transfer"></a>Tworzenie transferu

**Dotyczy:**

- Centrum partnerskie

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **POUBOJOWEGO** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/Transfers http/1.1                    |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru ścieżki, aby zidentyfikować klienta.

| Nazwa            | Typ     | Wymagane | Opis                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **Identyfikator klienta** | ciąg   | Tak      | Identyfikator GUID sformatowany przez klienta, który identyfikuje klienta.             |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano właściwości [TransferEntity](transfer-entity-resources.md) w treści żądania.

| Właściwość              | Typ          | Wymagane  | Opis                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| identyfikator                    | ciąg        | Nie    | Identyfikator transferEntity, który jest dostarczany po pomyślnym utworzeniu transferEntity.                               |
| createdTime           | DateTime      | Nie    | Data, w której utworzono transferEntity, w formacie daty i godziny. Stosowane po pomyślnym utworzeniu transferEntity.      |
| lastModifiedTime      | DateTime      | Nie    | Data ostatniej aktualizacji transferEntity w formacie daty i godziny. Stosowane po pomyślnym utworzeniu transferEntity. |
| lastModifiedUser      | ciąg        | Nie    | Użytkownik, który ostatnio zaktualizował transferEntity. Stosowane po pomyślnym utworzeniu transferEntity.                          |
| customerName          | ciąg        | Nie    | Opcjonalny. Nazwa klienta, którego subskrypcje są transferowane.                                              |
| customerTenantId      | ciąg        | Nie    | Identyfikator GUID sformatowany przez klienta, który identyfikuje klienta. Stosowane po pomyślnym utworzeniu transferEntity.         |
| partnertenantid       | ciąg        | Nie    | Identyfikator GUID w formacie identyfikatora partnera, który identyfikuje partnera.                                                                   |
| sourcePartnerName     | ciąg        | Nie    | Opcjonalny. Nazwa organizacji partnera, która inicjuje transfer.                                           |
| sourcePartnerTenantId | ciąg        | Tak   | Identyfikator GUID w formacie identyfikatora partnera, który identyfikuje partnera inicjującego transfer.                                           |
| targetPartnerName     | ciąg        | Nie    | Opcjonalny. Nazwa organizacji partnera, do której przeznaczony jest transfer.                                         |
| targetPartnerTenantId | ciąg        | Tak   | Identyfikator partnera w formacie GUID, który identyfikuje partnera, do którego jest przeznaczony transfer.                                  |
| lineItems             | Tablica obiektów | Tak| Tablica zasobów [TransferLineItem](transfer-entity-resources.md#transferlineitem) .                                   |
| status                | ciąg        | Nie    | Stan transferEntity. Możliwe wartości to "Active" (można je usunąć/przesłać) i "ukończone" (zostały już ukończone). Stosowane po pomyślnym utworzeniu transferEntity.|

W tej tabeli opisano właściwości [TransferLineItem](transfer-entity-resources.md#transferlineitem) w treści żądania.

|      Właściwość       |            Typ             | Wymagane | Opis                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| identyfikator                   | ciąg                     | Nie       | Unikatowy identyfikator elementu wiersza przeniesienia. Stosowane po pomyślnym utworzeniu transferEntity.|
| subscriptionId       | ciąg                     | Tak      | Identyfikator subskrypcji.                                                                         |
| quantity             | int                        | Nie       | Liczba licencji lub wystąpień.                                                                 |
| billingCycle         | Obiekt                     | Nie       | Typ cyklu rozliczeniowego ustawiony dla bieżącego okresu.                                                |
| friendlyName         | ciąg                     | Nie       | Opcjonalny. Przyjazna nazwa dla elementu zdefiniowanego przez partnera, która pomaga w odróżnieniu od siebie.                |
| partnerIdOnRecord    | ciąg                     | Nie       | PartnerId on Record (MPNID) zakupu, który ma miejsce, gdy transfer zostanie zaakceptowany.              |
| offerId              | ciąg                     | Nie       | Identyfikator oferty.                                                                                |
| addonItems           | Lista obiektów **TransferLineItem** | Nie | Kolekcja elementów transferEntity line dla dodatków, które będą transferowane wraz z subskrypcją podstawową, która jest transferowana. Stosowane po pomyślnym utworzeniu transferEntity.|
| transferError        | ciąg                     | Nie       | Stosowane po zaakceptowaniu transferEntity w przypadku błędu.                                        |
| status               | ciąg                     | Nie       | Stan LineItem w transferEntity.                                                    |

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

Jeśli to się powiedzie, ta metoda zwraca wypełniony zasób [TransferEnity](transfer-entity-resources.md) w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

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
