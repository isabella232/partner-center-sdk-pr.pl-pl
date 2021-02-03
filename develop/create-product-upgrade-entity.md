---
title: Tworzenie jednostki uaktualnienia produktu dla klienta
description: Za pomocą zasobu ProductUpgradeRequest można utworzyć jednostkę uaktualnienia produktu w celu uaktualnienia klienta do danej rodziny produktów.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 45830033d93e0906eafc169cf04b997e2ff7c3d8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767750"
---
# <a name="create-a-product-upgrade-entity-for-a-customer"></a>Tworzenie jednostki uaktualnienia produktu dla klienta

**Dotyczy:**

- Centrum partnerskie

Można utworzyć jednostkę uaktualnienia produktu w celu uaktualnienia klienta do danej rodziny produktów (na przykład planu platformy Azure) przy użyciu zasobu **ProductUpgradeRequest** .

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika. Postępuj zgodnie z [bezpiecznym modelem aplikacji](enable-secure-app-model.md) podczas korzystania z aplikacji i uwierzytelniania użytkowników za pomocą interfejsów API Centrum partnerskiego.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Rodzina produktów, do której ma zostać uaktualniony klient.

## <a name="c"></a>C\#

Aby uaktualnić klienta do planu platformy Azure:

1. Utwórz obiekt **ProductUpgradesRequest** i określ identyfikator klienta oraz "Azure" jako rodzinę produktów.

2. Użyj kolekcji **IAggregatePartner. ProductUpgrades** .

3. Wywołaj metodę **Create** i przekaż obiekt **ProductUpgradesRequest** , który zwróci ciąg **nagłówka lokalizacji** .

4. Wyodrębnij **Identyfikator upgrade** z ciągu nagłówka lokalizacji, którego można użyć do [zbadania stanu uaktualnienia](get-product-upgrade-status.md).

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "Azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

var productUpgradeLocationHeader = partnerOperations.ProductUpgrades.Create(productUpgradeRequest);

var upgradeId = Regex.Split(productUpgradeLocationHeader, "/")[1];

```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **POUBOJOWEGO** | [*{baseURL}*](partner-center-rest-urls.md)/V1/productupgrades http/1.1 |

#### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

#### <a name="request-body"></a>Treść żądania

Treść żądania musi zawierać zasób [ProductUpgradeRequest](product-upgrade-resources.md#productupgraderequest) .

#### <a name="request-example"></a>Przykład żądania

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades HTTP/1.1
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
  "productFamily": "Azure"
}
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, odpowiedź zawiera nagłówek **lokalizacji** z identyfikatorem URI, którego można użyć do pobrania stanu uaktualnienia produktu. Zapisz ten identyfikator URI do użycia z innymi powiązanymi interfejsami API REST.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: productUpgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 28 Sep 2019 20:35:35 GMT
```
