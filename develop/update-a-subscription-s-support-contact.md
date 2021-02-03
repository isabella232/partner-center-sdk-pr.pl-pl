---
title: Aktualizowanie informacji kontaktowych pomocy technicznej subskrypcji
description: Jak zaktualizować kontakt z pomocą techniczną w ramach subskrypcji do jednego z odsprzedawcaów dodanych przez partnera.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c8c6b658cfe6e14c75b0c06b177920ce3eb1b4ed
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768266"
---
# <a name="update-a-subscriptions-support-contact"></a><span data-ttu-id="4686e-103">Aktualizowanie informacji kontaktowych pomocy technicznej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4686e-103">Update a subscription's support contact</span></span>

<span data-ttu-id="4686e-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="4686e-104">**Applies To**</span></span>

- <span data-ttu-id="4686e-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="4686e-105">Partner Center</span></span>
- <span data-ttu-id="4686e-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="4686e-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="4686e-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="4686e-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4686e-108">Jak zaktualizować kontakt z pomocą techniczną w ramach subskrypcji do jednego z odsprzedawcaów dodanych przez partnera.</span><span class="sxs-lookup"><span data-stu-id="4686e-108">How to update a subscription's support contact to one of the partner's value added resellers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4686e-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4686e-109">Prerequisites</span></span>

- <span data-ttu-id="4686e-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4686e-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4686e-111">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4686e-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="4686e-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4686e-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4686e-113">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="4686e-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4686e-114">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="4686e-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4686e-115">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="4686e-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4686e-116">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="4686e-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4686e-117">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4686e-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="4686e-118">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="4686e-118">A subscription identifier.</span></span>

- <span data-ttu-id="4686e-119">Informacje na temat nowej osoby kontaktowej pomocy technicznej: Identyfikator dzierżawy, identyfikator Microsoft Partner Network i nazwa.</span><span class="sxs-lookup"><span data-stu-id="4686e-119">Information about the new support contact: tenant identifier, Microsoft Partner Network identifier, and name.</span></span> <span data-ttu-id="4686e-120">Kontakt z pomocą techniczną musi być jednym z odsprzedawcaów dodanych przez partnera.</span><span class="sxs-lookup"><span data-stu-id="4686e-120">The support contact must be one of the partner's value added resellers.</span></span>

## <a name="c"></a><span data-ttu-id="4686e-121">C\#</span><span class="sxs-lookup"><span data-stu-id="4686e-121">C\#</span></span>

<span data-ttu-id="4686e-122">Aby zaktualizować kontakt z pomocą techniczną subskrypcji, najpierw Utwórz wystąpienie i wypełnij obiekt [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) nowymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="4686e-122">To update a subscription's support contact, first instantiate and populate a [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) object with the new values.</span></span> <span data-ttu-id="4686e-123">Następnie użyj metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="4686e-123">Then use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="4686e-124">Następnie uzyskaj interfejs do operacji subskrybowania, wywołując metodę [**Subscription. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="4686e-124">Next, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="4686e-125">Następnie użyj właściwości [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) , aby uzyskać interfejs do obsługi operacji kontaktowych.</span><span class="sxs-lookup"><span data-stu-id="4686e-125">Then, use the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) property to obtain an interface to support contact operations.</span></span> <span data-ttu-id="4686e-126">Na koniec Wywołaj metodę [**Update**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) lub [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) z wypełnionym obiektem SupportContact w celu zaktualizowania kontaktu z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="4686e-126">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) or [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) method with the populated SupportContact object to update the support contact.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Instantiate a SupportContact object and populate it with the new support contact information.
var supportContact = new SupportContact()
{
    Name = "Support contact's name",
    SupportTenantId = "Support contact's tenant ID",
    SupportMpnId = "Support contact's MPN ID"
};

// Update the support contact with a new object that has valid VAR values.
var updatedSupportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).SupportContact.Update(supportContact);
```

<span data-ttu-id="4686e-127">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="4686e-127">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="4686e-128">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: UpdateSubscriptionSupportContact.cs</span><span class="sxs-lookup"><span data-stu-id="4686e-128">**Project**: Partner Center SDK Samples **Class**: UpdateSubscriptionSupportContact.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="4686e-129">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="4686e-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4686e-130">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="4686e-130">Request syntax</span></span>

| <span data-ttu-id="4686e-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="4686e-131">Method</span></span>  | <span data-ttu-id="4686e-132">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="4686e-132">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4686e-133">**PUT**</span><span class="sxs-lookup"><span data-stu-id="4686e-133">**PUT**</span></span> | <span data-ttu-id="4686e-134">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/subscriptions/{Subscription-ID}/supportcontact http/1.1</span><span class="sxs-lookup"><span data-stu-id="4686e-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="4686e-135">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="4686e-135">URI parameter</span></span>

<span data-ttu-id="4686e-136">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="4686e-136">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="4686e-137">Nazwa</span><span class="sxs-lookup"><span data-stu-id="4686e-137">Name</span></span>            | <span data-ttu-id="4686e-138">Typ</span><span class="sxs-lookup"><span data-stu-id="4686e-138">Type</span></span>   | <span data-ttu-id="4686e-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4686e-139">Required</span></span> | <span data-ttu-id="4686e-140">Opis</span><span class="sxs-lookup"><span data-stu-id="4686e-140">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="4686e-141">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="4686e-141">customer-id</span></span>     | <span data-ttu-id="4686e-142">ciąg</span><span class="sxs-lookup"><span data-stu-id="4686e-142">string</span></span> | <span data-ttu-id="4686e-143">Tak</span><span class="sxs-lookup"><span data-stu-id="4686e-143">Yes</span></span>      | <span data-ttu-id="4686e-144">Ciąg w formacie GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="4686e-144">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="4686e-145">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4686e-145">subscription-id</span></span> | <span data-ttu-id="4686e-146">ciąg</span><span class="sxs-lookup"><span data-stu-id="4686e-146">string</span></span> | <span data-ttu-id="4686e-147">Tak</span><span class="sxs-lookup"><span data-stu-id="4686e-147">Yes</span></span>      | <span data-ttu-id="4686e-148">Ciąg w formacie GUID, który identyfikuje subskrypcję wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="4686e-148">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4686e-149">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="4686e-149">Request headers</span></span>

<span data-ttu-id="4686e-150">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4686e-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4686e-151">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="4686e-151">Request body</span></span>

<span data-ttu-id="4686e-152">W treści żądania musi znajdować się wypełniony zasób [SupportContact](subscription-resources.md#supportcontact) .</span><span class="sxs-lookup"><span data-stu-id="4686e-152">You must include a populated [SupportContact](subscription-resources.md#supportcontact) resource in the request body.</span></span> <span data-ttu-id="4686e-153">Kontakt z pomocą techniczną musi być członkiem istniejącego odsprzedawcy z relacją do partnera.</span><span class="sxs-lookup"><span data-stu-id="4686e-153">The support contact must be an existing reseller with a relationship to the partner.</span></span>

### <a name="request-example"></a><span data-ttu-id="4686e-154">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="4686e-154">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b72d732a-eed7-4a60-82d1-1b2e6cba0ed2
MS-CorrelationId: 84eff9e1-6a8c-42aa-8678-c00b0d3fb26f
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 320
Expect: 100-continue

{
    "SupportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "SupportMpnId": "4391507",
    "Name": "Trey Research",
    "Links": {
        "Self": {
            "Uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "Method": "Get",
            "Headers": []
        }
    },
    "Attributes": {
        "ObjectType": "SupportContact"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="4686e-155">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="4686e-155">REST response</span></span>

<span data-ttu-id="4686e-156">Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [SupportContact](subscription-resources.md#supportcontact) .</span><span class="sxs-lookup"><span data-stu-id="4686e-156">If successful, the response body contains the [SupportContact](subscription-resources.md#supportcontact) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4686e-157">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4686e-157">Response success and error codes</span></span>

<span data-ttu-id="4686e-158">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="4686e-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4686e-159">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="4686e-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4686e-160">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4686e-160">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4686e-161">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4686e-161">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b0cd9bcc-742e-4c76-9e34-a96d3bdc7673
MS-RequestId: 7591ca22-d4e3-409d-bfa6-09806eaff4f3
MS-CV: W8Tzj6NGckKHcq+E.0
MS-ServerId: 030020344
Date: Wed, 21 Jun 2017 01:01:17 GMT

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
