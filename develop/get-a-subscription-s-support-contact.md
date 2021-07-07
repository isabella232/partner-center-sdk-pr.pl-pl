---
title: Pobieranie informacji kontaktowych pomocy technicznej subskrypcji
description: Jak uzyskać kontakt z pomocą techniczną dla subskrypcji.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b6c98e5ed96f2ca4787e93504c9e094bd46ae783
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760763"
---
# <a name="get-a-subscriptions-support-contact"></a><span data-ttu-id="84e90-103">Pobieranie informacji kontaktowych pomocy technicznej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="84e90-103">Get a subscription's support contact</span></span>

<span data-ttu-id="84e90-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="84e90-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="84e90-105">Jak uzyskać kontakt z pomocą techniczną dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="84e90-105">How to get a subscription's support contact.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84e90-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="84e90-106">Prerequisites</span></span>

- <span data-ttu-id="84e90-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="84e90-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="84e90-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="84e90-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="84e90-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="84e90-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="84e90-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="84e90-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="84e90-111">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="84e90-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="84e90-112">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="84e90-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="84e90-113">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="84e90-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="84e90-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="84e90-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="84e90-115">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="84e90-115">A subscription identifier.</span></span>

## <a name="c"></a><span data-ttu-id="84e90-116">C\#</span><span class="sxs-lookup"><span data-stu-id="84e90-116">C\#</span></span>

<span data-ttu-id="84e90-117">Aby uzyskać kontakt z pomocą techniczną dla subskrypcji, zacznij od metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta.</span><span class="sxs-lookup"><span data-stu-id="84e90-117">To get a subscription's support contact, start by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="84e90-118">Następnie pobierz interfejs do operacji subskrypcji, wywołując metodę [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="84e90-118">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="84e90-119">Następnie użyj właściwości [**SupportContact,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) aby uzyskać interfejs do obsługi operacji kontaktowych, a następnie wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) aby pobrać obiekt [**SupportContact.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact)</span><span class="sxs-lookup"><span data-stu-id="84e90-119">Next, use the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) property to obtain an interface to support contact operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve subscription's support contact.
var supportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).SupportContact.Get();
```

<span data-ttu-id="84e90-120">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="84e90-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="84e90-121">**Project:** zestaw SDK Centrum partnerskiego Samples Class : GetSubscriptionSupportContact.cs **(Klasa** przykładów kodu: GetSubscriptionSupportContact.cs)</span><span class="sxs-lookup"><span data-stu-id="84e90-121">**Project**: Partner Center SDK Samples **Class**: GetSubscriptionSupportContact.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="84e90-122">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="84e90-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="84e90-123">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="84e90-123">Request syntax</span></span>

| <span data-ttu-id="84e90-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="84e90-124">Method</span></span>  | <span data-ttu-id="84e90-125">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="84e90-125">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="84e90-126">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="84e90-126">**GET**</span></span> | <span data-ttu-id="84e90-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="84e90-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="84e90-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="84e90-128">URI parameter</span></span>

<span data-ttu-id="84e90-129">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="84e90-129">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="84e90-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="84e90-130">Name</span></span>            | <span data-ttu-id="84e90-131">Typ</span><span class="sxs-lookup"><span data-stu-id="84e90-131">Type</span></span>   | <span data-ttu-id="84e90-132">Wymagane</span><span class="sxs-lookup"><span data-stu-id="84e90-132">Required</span></span> | <span data-ttu-id="84e90-133">Opis</span><span class="sxs-lookup"><span data-stu-id="84e90-133">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="84e90-134">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="84e90-134">customer-id</span></span>     | <span data-ttu-id="84e90-135">ciąg</span><span class="sxs-lookup"><span data-stu-id="84e90-135">string</span></span> | <span data-ttu-id="84e90-136">Tak</span><span class="sxs-lookup"><span data-stu-id="84e90-136">Yes</span></span>      | <span data-ttu-id="84e90-137">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="84e90-137">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="84e90-138">subscription-id</span><span class="sxs-lookup"><span data-stu-id="84e90-138">subscription-id</span></span> | <span data-ttu-id="84e90-139">ciąg</span><span class="sxs-lookup"><span data-stu-id="84e90-139">string</span></span> | <span data-ttu-id="84e90-140">Tak</span><span class="sxs-lookup"><span data-stu-id="84e90-140">Yes</span></span>      | <span data-ttu-id="84e90-141">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje subskrypcję wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="84e90-141">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="84e90-142">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="84e90-142">Request headers</span></span>

<span data-ttu-id="84e90-143">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="84e90-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="84e90-144">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="84e90-144">Request body</span></span>

<span data-ttu-id="84e90-145">Brak.</span><span class="sxs-lookup"><span data-stu-id="84e90-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="84e90-146">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="84e90-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="84e90-147">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="84e90-147">REST response</span></span>

<span data-ttu-id="84e90-148">Jeśli to się powiedzie, treść odpowiedzi zawiera [zasób SupportContact.](subscription-resources.md#supportcontact)</span><span class="sxs-lookup"><span data-stu-id="84e90-148">If successful, the response body contains the [SupportContact](subscription-resources.md#supportcontact) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="84e90-149">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="84e90-149">Response success and error codes</span></span>

<span data-ttu-id="84e90-150">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="84e90-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="84e90-151">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="84e90-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="84e90-152">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="84e90-152">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="84e90-153">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="84e90-153">Response example</span></span>

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
