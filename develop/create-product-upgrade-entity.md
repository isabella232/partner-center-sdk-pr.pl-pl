---
title: Tworzenie jednostki uaktualnienia produktu dla klienta
description: Zasób ProductUpgradeRequest umożliwia utworzenie jednostki uaktualnienia produktu w celu uaktualnienia klienta do danej rodziny produktów.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4e346b7f5294a8847047c85115d8c80f34eaca84
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973420"
---
# <a name="create-a-product-upgrade-entity-for-a-customer"></a>Tworzenie jednostki uaktualnienia produktu dla klienta

Możesz utworzyć jednostkę uaktualnienia produktu, aby uaktualnić klienta do danej rodziny produktów (na przykład planu platformy Azure) przy użyciu **zasobu ProductUpgradeRequest.**

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika. Postępuj zgodnie z [modelem bezpiecznej aplikacji podczas](enable-secure-app-model.md) korzystania z uwierzytelniania app+user z Partner Center API.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Rodzina produktów, do której chcesz uaktualnić klienta.

## <a name="c"></a>C\#

Aby uaktualnić klienta do planu platformy Azure:

1. Utwórz obiekt **ProductUpgradesRequest** i określ identyfikator klienta oraz wartość "Azure" jako rodzinę produktów.

2. Użyj **kolekcji IAggregatePartner.ProductUpgrades.**

3. Wywołaj **metodę Create** i przekaż obiekt **ProductUpgradesRequest,** który zwróci ciąg **nagłówka** lokalizacji.

4. Wyodrębnij **identyfikator upgrade-id** z ciągu nagłówka lokalizacji, który może służyć do wykonywania [zapytań o stan uaktualnienia](get-product-upgrade-status.md).

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
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades HTTP/1.1 |

#### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

#### <a name="request-body"></a>Treść żądania

Treść żądania musi zawierać [zasób ProductUpgradeRequest.](product-upgrade-resources.md#productupgraderequest)

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

Jeśli to się powiedzie, odpowiedź zawiera nagłówek **Location** z kodem URI, który może służyć do pobierania stanu uaktualnienia produktu. Zapisz ten URI do użycia z innymi powiązanymi interfejsami API REST.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)

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
