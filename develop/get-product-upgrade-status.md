---
title: Pobieranie stanu uaktualnienia produktu dla klienta
description: Za pomocą zasobu ProductUpgradeRequest można określić stan uaktualnienia produktu dla klienta do nowej rodziny produktów, np. z subskrypcji Microsoft Azure (MS-AZR-0145P) do planu platformy Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1819887d459ec72a48ea2b7a5a4121dc56718313
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767914"
---
# <a name="get-the-product-upgrade-status-for-a-customer"></a>Pobieranie stanu uaktualnienia produktu dla klienta

**Dotyczy:**

- Centrum partnerskie

Za pomocą zasobu [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) można pobrać stan uaktualnienia do nowej rodziny produktów. Ten zasób jest stosowany podczas uaktualniania klienta z subskrypcji Microsoft Azure (MS-AZR-0145P) do planu platformy Azure. Pomyślne żądanie zwraca zasób [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) .

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika. Postępuj zgodnie z [bezpiecznym modelem aplikacji](enable-secure-app-model.md) podczas korzystania z aplikacji i uwierzytelniania użytkowników za pomocą interfejsów API Centrum partnerskiego.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Rodzina produktów.

- Identyfikator uaktualnienia żądania uaktualnienia.

## <a name="c"></a>C\#

Aby sprawdzić, czy klient kwalifikuje się do uaktualnienia do planu platformy Azure:

1. Utwórz obiekt **ProductUpgradesRequest** i określ identyfikator klienta oraz "Azure" jako rodzinę produktów.

2. Użyj kolekcji **IAggregatePartner. ProductUpgrades** .

3. Wywołaj metodę **ById** i przekaż **Identyfikator upgrade-ID**.

4. Wywołaj metodę **checkStatus** i przekaż obiekt **ProductUpgradesRequest** , który zwróci obiekt **ProductUpgradeStatus** .

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesStatus productUpgradeStatus = partnerOperations.ProductUpgrades.ById(selectedUpgradeId).CheckStatus(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania |
|----------|-----------------------------------------------------------------------------------------------|
| **POUBOJOWEGO** | [*{baseURL}*](partner-center-rest-urls.md)/V1/productUpgrades/{upgrade-ID}/status http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby określić klienta, dla którego otrzymujesz stan uaktualnienia produktu.

| Nazwa               | Typ | Wymagane | Opis                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| **Identyfikator uaktualnienia** | GUID | Tak | Wartość jest identyfikatorem uaktualnienia sformatowanym przez identyfikator GUID. Możesz użyć tego identyfikatora, aby określić uaktualnienie do śledzenia. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Treść żądania musi zawierać zasób [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) .

### <a name="request-example"></a>Przykład żądania

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4/status  HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
 {
    "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
    "productFamily": "azure"
  }
  "Attributes": {
  "ObjectType": "ProductUpgradeRequest"
  }
}
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, metoda zwraca zasób [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) w treści.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 Ok
Content-Length: 150
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 04 Oct 2019 20:35:35 GMT

{
    "id": "42d075a4-bfe7-43e7-af6d-7c68a57edcb4",
    "status": "Completed",
    "productFamily": "Azure",
    "lineItems": [
        {
            "sourceProduct": {
                "id": "b1beb621-3cad-4d7a-b360-62db33ce028e",
                "name": "AzureSubscription"
            },
            "targetProduct": {
                "id": "d231908e-31c1-de0e-027b-bc5ce11f09d9",
                "name": "Microsoft Azure plan"
            },
            "upgradedDate": "2019-08-29T23:47:28.8524555Z",
            "status": "Completed"
        }
    ]
}

```
