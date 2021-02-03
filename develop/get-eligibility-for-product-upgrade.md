---
title: Sprawdź uprawnienia klienta do uaktualniania do planu platformy Azure
description: Za pomocą zasobu ProductUpgradeRequest można zwrócić zasób ProductUpgradesEligibility w celu ustalenia, czy klient ma uprawnienia do uaktualnienia z subskrypcji Microsoft Azure (MS-AZR-0145P) do planu platformy Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 568ed3f4cff7d9cd520e608d43cb89bb78e00ccc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767690"
---
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a>Sprawdź uprawnienia klienta do uaktualniania do planu platformy Azure

**Dotyczy:**

- Centrum partnerskie

Możesz użyć zasobu [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) , aby sprawdzić, czy klient jest uprawniony do uaktualnienia do planu platformy Azure z subskrypcji Microsoft Azure (MS-AZR-0145P) Ta metoda zwraca zasób [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) z uprawnieniem do uaktualnienia produktu klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika. Postępuj zgodnie z [bezpiecznym modelem aplikacji](enable-secure-app-model.md) podczas korzystania z aplikacji i uwierzytelniania użytkowników za pomocą interfejsów API Centrum partnerskiego.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Rodzina produktów.

## <a name="c"></a>C\#

Aby sprawdzić, czy klient kwalifikuje się do uaktualnienia do planu platformy Azure:

1. Utwórz obiekt **ProductUpgradesRequest** i określ identyfikator klienta oraz "Azure" jako rodzinę produktów.

2. Użyj kolekcji **IAggregatePartner. ProductUpgrades** .
3. Wywołaj metodę **CheckEligibility** i przekaż obiekt **ProductUpgradesRequest** , który zwróci obiekt **ProductUpgradesEligibility** .

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesEligibility productUpgradeEligibility = partnerOperations.ProductUpgrades.CheckEligibility(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **POUBOJOWEGO** | [*{baseURL}*](partner-center-rest-urls.md)/V1/productUpgrades/Eligibility http/1.1 |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Treść żądania musi zawierać zasób [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) .

### <a name="request-example"></a>Przykład żądania

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/eligibility HTTP/1.1
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
        "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
        "productFamily": "azure"
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
    "customerId": "c1958bc7-3284-4952-a257-de594ee64743",
    "isEligible": true,
    "productFamily": "azure"
}
```
