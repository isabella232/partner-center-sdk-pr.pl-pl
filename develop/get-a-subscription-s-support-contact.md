---
title: Pobieranie informacji kontaktowych pomocy technicznej subskrypcji
description: Jak uzyskać kontakt z pomocą techniczną dla subskrypcji.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df3bce48902d95dc541c4a45e4e633569fc4406e
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768057"
---
# <a name="get-a-subscriptions-support-contact"></a><span data-ttu-id="72146-103">Pobieranie informacji kontaktowych pomocy technicznej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="72146-103">Get a subscription's support contact</span></span>

<span data-ttu-id="72146-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="72146-104">**Applies To**</span></span>

- <span data-ttu-id="72146-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="72146-105">Partner Center</span></span>
- <span data-ttu-id="72146-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="72146-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="72146-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="72146-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="72146-108">Jak uzyskać kontakt z pomocą techniczną dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="72146-108">How to get a subscription's support contact.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72146-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="72146-109">Prerequisites</span></span>

- <span data-ttu-id="72146-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="72146-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="72146-111">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="72146-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="72146-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="72146-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="72146-113">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="72146-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="72146-114">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="72146-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="72146-115">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="72146-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="72146-116">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="72146-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="72146-117">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="72146-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="72146-118">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="72146-118">A subscription identifier.</span></span>

## <a name="c"></a><span data-ttu-id="72146-119">C\#</span><span class="sxs-lookup"><span data-stu-id="72146-119">C\#</span></span>

<span data-ttu-id="72146-120">Aby uzyskać kontakt z pomocą techniczną subskrypcji, Zacznij od użycia metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="72146-120">To get a subscription's support contact, start by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="72146-121">Następnie uzyskaj interfejs do operacji subskrybowania, wywołując metodę Subscription [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="72146-121">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="72146-122">Następnie użyj właściwości [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) , aby uzyskać interfejs do obsługi operacji kontaktowych, a następnie Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) , aby pobrać obiekt [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) .</span><span class="sxs-lookup"><span data-stu-id="72146-122">Next, use the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) property to obtain an interface to support contact operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve subscription's support contact.
var supportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).SupportContact.Get();
```

<span data-ttu-id="72146-123">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="72146-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="72146-124">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: GetSubscriptionSupportContact.cs</span><span class="sxs-lookup"><span data-stu-id="72146-124">**Project**: Partner Center SDK Samples **Class**: GetSubscriptionSupportContact.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="72146-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="72146-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="72146-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="72146-126">Request syntax</span></span>

| <span data-ttu-id="72146-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="72146-127">Method</span></span>  | <span data-ttu-id="72146-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="72146-128">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="72146-129">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="72146-129">**GET**</span></span> | <span data-ttu-id="72146-130">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/subscriptions/{Subscription-ID}/supportcontact http/1.1</span><span class="sxs-lookup"><span data-stu-id="72146-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="72146-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="72146-131">URI parameter</span></span>

<span data-ttu-id="72146-132">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="72146-132">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="72146-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="72146-133">Name</span></span>            | <span data-ttu-id="72146-134">Typ</span><span class="sxs-lookup"><span data-stu-id="72146-134">Type</span></span>   | <span data-ttu-id="72146-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72146-135">Required</span></span> | <span data-ttu-id="72146-136">Opis</span><span class="sxs-lookup"><span data-stu-id="72146-136">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="72146-137">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="72146-137">customer-id</span></span>     | <span data-ttu-id="72146-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="72146-138">string</span></span> | <span data-ttu-id="72146-139">Tak</span><span class="sxs-lookup"><span data-stu-id="72146-139">Yes</span></span>      | <span data-ttu-id="72146-140">Ciąg w formacie GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="72146-140">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="72146-141">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="72146-141">subscription-id</span></span> | <span data-ttu-id="72146-142">ciąg</span><span class="sxs-lookup"><span data-stu-id="72146-142">string</span></span> | <span data-ttu-id="72146-143">Tak</span><span class="sxs-lookup"><span data-stu-id="72146-143">Yes</span></span>      | <span data-ttu-id="72146-144">Ciąg w formacie GUID, który identyfikuje subskrypcję wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="72146-144">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="72146-145">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="72146-145">Request headers</span></span>

<span data-ttu-id="72146-146">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="72146-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="72146-147">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="72146-147">Request body</span></span>

<span data-ttu-id="72146-148">Brak.</span><span class="sxs-lookup"><span data-stu-id="72146-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="72146-149">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="72146-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="72146-150">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="72146-150">REST response</span></span>

<span data-ttu-id="72146-151">Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [SupportContact](subscription-resources.md#supportcontact) .</span><span class="sxs-lookup"><span data-stu-id="72146-151">If successful, the response body contains the [SupportContact](subscription-resources.md#supportcontact) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="72146-152">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="72146-152">Response success and error codes</span></span>

<span data-ttu-id="72146-153">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="72146-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="72146-154">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="72146-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="72146-155">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="72146-155">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="72146-156">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="72146-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CV: bLbUhqy0+ESOX1v4.0
MS-ServerId: 201022015
Date: Tue, 20 Jun 2017 19:30:19 GMT

{
    "supportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "supportMpnId": "4391507",
    "name": "Trey Research",
    "links": {
        "self": {
            "uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "method": "Get",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SupportContact"
    }
}
```
