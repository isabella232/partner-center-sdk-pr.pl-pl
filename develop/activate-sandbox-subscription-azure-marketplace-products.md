---
title: Aktywuj subskrypcję piaskownicy dla komercyjnych produktów Marketplace
description: Dowiedz się, jak korzystać z interfejsów API REST usługi C/# i Centrum partnerskiego, aby aktywować subskrypcję piaskownicy dla komercyjnych produktów Marketplace.
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a78b2c84368b29f1378f46971c4814929094e299
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/11/2020
ms.locfileid: "97768509"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-saas-products-to-enable-billing"></a>Aktywuj subskrypcję piaskownicy dla komercyjnych produktów SaaS Marketplace, aby włączyć rozliczenia

**Dotyczy:**

- Centrum partnerskie

Jak aktywować subskrypcję dla komercyjnych produktów jako usługi (SaaS) na kontach piaskownicy integracji, aby włączyć rozliczenia.

> [!NOTE]
> Istnieje możliwość aktywowania subskrypcji komercyjnych produktów SaaS Marketplace z kont piaskownicy integracji. Jeśli masz subskrypcję produkcyjną, należy odwiedzić witrynę wydawcy, aby ukończyć proces instalacji. Rozliczanie subskrypcji rozpocznie się dopiero po zakończeniu instalacji.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Konto partnera piaskownicy integracji z klientem z aktywną subskrypcją dla komercyjnych produktów SaaS Marketplace.

- W przypadku partnerów korzystających z zestawu SDK platformy .NET w usłudze Partner Center musisz użyć zestawu SDK 1.14.0 lub nowszego, aby uzyskać dostęp do tej funkcji.

## <a name="c"></a>C\#

Wykonaj następujące kroki, aby aktywować subskrypcję dla komercyjnych produktów SaaS Marketplace:

1. Utwórz interfejs dla dostępnych operacji subskrypcji. Należy zidentyfikować klienta i określić identyfikator subskrypcji wersji próbnej subskrypcji.

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. Aktywuj subskrypcję przy użyciu operacji **uaktywniania** .

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda     | Identyfikator URI żądania                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **POUBOJOWEGO** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/{Subscription-ID}/Activate http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

| Nazwa                   | Typ     | Wymagane | Opis                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Identyfikator dzierżawy klienta** | **guid** | Y | Wartość to identyfikator identyfikatora dzierżawy klienta w formacie GUID (**Identyfikator dzierżawy klienta**), który umożliwia określenie klienta. |
| **Identyfikator subskrypcji** | **guid** | Y | Wartość jest identyfikatorem subskrypcji w formacie GUID (**Identyfikator subskrypcji**), który umożliwia określenie subskrypcji. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
POST https://api.partnercenter.microsoft.com/v1/customers/42b5f772-5c5c-4bce-b9d7-bdadeecca411/subscriptions/87363db7-39ab-dd25-d371-94340aaa2f97/activate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

```

## <a name="rest-response"></a>Odpowiedź REST

Ta metoda zwraca właściwości **identyfikatora subskrypcji** i **stanu** .

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 79
Content-Type: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "subscriptionId":"87363db7-39ab-dd25-d371-94340aaa2f97",
    "status":"Success"
}
```
