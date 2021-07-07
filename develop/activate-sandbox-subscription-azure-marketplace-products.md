---
title: Aktywowanie subskrypcji piaskownicy dla produktów platformy handlowej
description: Dowiedz się, jak używać języka C/# i Partner Center API REST do aktywowania subskrypcji piaskownicy dla produktów platformy handlowej.
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b32c3e87462f58218771fc5da7da56ed177489cb
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025704"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-saas-products-to-enable-billing"></a>Aktywowanie subskrypcji piaskownicy dla produktów SaaS komercyjnej platformy handlowej w celu włączenia rozliczeń

Jak aktywować subskrypcję komercyjnych produktów platformy handlowej oprogramowania jako usługi (SaaS) z kont piaskownicy integracji w celu włączenia rozliczeń.

> [!NOTE]
> Subskrypcję produktów SaaS komercyjnej platformy handlowej można aktywować tylko z kont piaskownicy integracji. Jeśli masz subskrypcję produkcyjną, musisz odwiedzić witrynę wydawcy, aby ukończyć proces instalacji. Rozliczanie subskrypcji rozpocznie się dopiero po zakończeniu konfiguracji.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Konto partnera piaskownicy integracji z klientem, który ma aktywną subskrypcję produktów SaaS komercyjnej platformy handlowej.

- W przypadku partnerów korzystających Partner Center .NET SDK należy użyć zestawu SDK w wersji 1.14.0 lub wyższej, aby uzyskać dostęp do tej możliwości.

## <a name="c"></a>C\#

Aby aktywować subskrypcję produktów SaaS na platformie handlowej, należy wykonać następujące czynności:

1. Udostępnij interfejs dla operacji subskrypcji. Należy zidentyfikować klienta i określić identyfikator subskrypcji wersji próbnej.

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. Aktywuj subskrypcję przy użyciu **operacji** Aktywuj.

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda     | Identyfikator URI żądania                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/activate HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

| Nazwa                   | Typ     | Wymagane | Opis                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **identyfikator dzierżawy klienta** | **guid** | Y | Wartość jest identyfikatorem dzierżawy klienta w formacie GUID **(customer-tenant-id),** który umożliwia określenie klienta. |
| **subscription-id** | **guid** | Y | Wartość jest identyfikatorem subskrypcji w formacie GUID **(subscription-id),** który umożliwia określenie subskrypcji. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

Ta metoda zwraca **właściwości subscription-id** **i status.**

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)

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
