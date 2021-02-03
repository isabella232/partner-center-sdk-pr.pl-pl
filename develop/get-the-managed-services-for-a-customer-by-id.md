---
title: Pobieranie usług zarządzanych dla klienta według identyfikatora
description: Pobiera zarządzane usługi dla klienta. Innymi słowy, uzyskaj linki do wszystkich subskrypcji klienta, do których masz uprawnienia administratora delegowanego. Możesz użyć tych linków, aby zapewnić pomoc techniczną i żądania usług plików firmie Microsoft.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4764fce6a80035ea4b9dcc6677a3da28fc863eb7
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768409"
---
# <a name="get-the-managed-services-for-a-customer-by-id"></a><span data-ttu-id="ffd64-105">Pobieranie usług zarządzanych dla klienta według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="ffd64-105">Get the managed services for a customer by ID</span></span>

<span data-ttu-id="ffd64-106">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="ffd64-106">**Applies To**</span></span>

- <span data-ttu-id="ffd64-107">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="ffd64-107">Partner Center</span></span>
- <span data-ttu-id="ffd64-108">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="ffd64-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="ffd64-109">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ffd64-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ffd64-110">Pobiera zarządzane usługi dla klienta.</span><span class="sxs-lookup"><span data-stu-id="ffd64-110">Gets the managed services for a customer.</span></span> <span data-ttu-id="ffd64-111">Innymi słowy, uzyskaj linki do wszystkich subskrypcji klienta, do których masz uprawnienia administratora delegowanego.</span><span class="sxs-lookup"><span data-stu-id="ffd64-111">In other words, get links to all of the customer's subscriptions for which you have delegated admin privileges.</span></span> <span data-ttu-id="ffd64-112">Możesz użyć tych linków, aby zapewnić pomoc techniczną i żądania usług plików firmie Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ffd64-112">You can use these links to provide support and file service requests with Microsoft.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffd64-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ffd64-113">Prerequisites</span></span>

- <span data-ttu-id="ffd64-114">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ffd64-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ffd64-115">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ffd64-115">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="ffd64-116">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ffd64-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ffd64-117">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="ffd64-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ffd64-118">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="ffd64-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ffd64-119">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="ffd64-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ffd64-120">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="ffd64-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ffd64-121">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ffd64-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="ffd64-122">C\#</span><span class="sxs-lookup"><span data-stu-id="ffd64-122">C\#</span></span>

<span data-ttu-id="ffd64-123">Aby wyświetlić listę wszystkich usług zarządzanych dla klienta, Użyj kolekcji **IAggregatePartner. Customers** i Wywołaj metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="ffd64-123">To display a list of all the managed services for a customer, use your **IAggregatePartner.Customers** collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="ffd64-124">Następnie Wywołaj Właściwość [**ManagedServices**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) , a następnie metodę [**Get ()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) lub [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="ffd64-124">Then call the [**ManagedServices**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerID as Customer;

ResourceCollection<ManagedService> managedServices = partnerOperations.Customers.ById(selectedCustomerId).ManagedServices.Get();
```

<span data-ttu-id="ffd64-125">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="ffd64-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="ffd64-126">**Project**: PartnerCenterSDK. FeaturesSamples **Klasa**: CustomerManagedServices.cs</span><span class="sxs-lookup"><span data-stu-id="ffd64-126">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: CustomerManagedServices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="ffd64-127">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="ffd64-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ffd64-128">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="ffd64-128">Request syntax</span></span>

| <span data-ttu-id="ffd64-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="ffd64-129">Method</span></span>  | <span data-ttu-id="ffd64-130">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="ffd64-130">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ffd64-131">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="ffd64-131">**GET**</span></span> | <span data-ttu-id="ffd64-132">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/managedservices http/1.1</span><span class="sxs-lookup"><span data-stu-id="ffd64-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/managedservices HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="ffd64-133">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="ffd64-133">URI parameter</span></span>

<span data-ttu-id="ffd64-134">Użyj następującego parametru zapytania, aby pobrać zarządzane usługi klienta.</span><span class="sxs-lookup"><span data-stu-id="ffd64-134">Use the following query parameter to get the customer's managed services.</span></span>

| <span data-ttu-id="ffd64-135">Nazwa</span><span class="sxs-lookup"><span data-stu-id="ffd64-135">Name</span></span>                   | <span data-ttu-id="ffd64-136">Typ</span><span class="sxs-lookup"><span data-stu-id="ffd64-136">Type</span></span>     | <span data-ttu-id="ffd64-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ffd64-137">Required</span></span> | <span data-ttu-id="ffd64-138">Opis</span><span class="sxs-lookup"><span data-stu-id="ffd64-138">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="ffd64-139">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="ffd64-139">**customer-tenant-id**</span></span> | <span data-ttu-id="ffd64-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="ffd64-140">**guid**</span></span> | <span data-ttu-id="ffd64-141">Y</span><span class="sxs-lookup"><span data-stu-id="ffd64-141">Y</span></span>        | <span data-ttu-id="ffd64-142">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="ffd64-142">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ffd64-143">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="ffd64-143">Request headers</span></span>

<span data-ttu-id="ffd64-144">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ffd64-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ffd64-145">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="ffd64-145">Request body</span></span>

<span data-ttu-id="ffd64-146">Brak.</span><span class="sxs-lookup"><span data-stu-id="ffd64-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ffd64-147">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="ffd64-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/managedservices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
```

## <a name="rest-response"></a><span data-ttu-id="ffd64-148">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="ffd64-148">REST response</span></span>

<span data-ttu-id="ffd64-149">Jeśli to się powiedzie, ta metoda zwraca kolekcję obiektów **usługi zarządzanej** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ffd64-149">If successful, this method returns a collection of **Managed Service** objects in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ffd64-150">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ffd64-150">Response success and error codes</span></span>

<span data-ttu-id="ffd64-151">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="ffd64-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ffd64-152">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="ffd64-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ffd64-153">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ffd64-153">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ffd64-154">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ffd64-154">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 10588
Content-Type: application/json
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
Date: Mon, 23 Nov 2015 18:02:12 GMT

{
    "totalCount": 2,
    "items": [{
        "id": "Exchange",
        "name": "Exchange",
        "groupName": "Office",
        "links": {
            "adminService": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Exchange&InitialDomain=<domain>&PrimaryDomain=<domain>",
                "method": "GET",
                "headers": []
            },
            "serviceHealth": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=ServiceStatus",
                "method": "GET",
                "headers": []
            },
            "serviceTicket": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Support",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "ManagedService"
        }
    },
    {
        "id": "MicrosoftCommunicationsOnline",
        "name": "SkypeforBusiness",
        "groupName": "Office",
        "links": {
            "adminService": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=MicrosoftCommunicationsOnline",
                "method": "GET",
                "headers": []
            },
            "serviceHealth": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=ServiceStatus",
                "method": "GET",
                "headers": []
            },
            "serviceTicket": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Support",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "ManagedService"
        }
    }
```
