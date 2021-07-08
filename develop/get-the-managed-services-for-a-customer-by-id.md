---
title: Pobieranie usług zarządzanych dla klienta według identyfikatora
description: Pobiera usługi zarządzane dla klienta. Innymi słowy, uzyskaj linki do wszystkich subskrypcji klienta, do których masz delegowane uprawnienia administratora. Możesz użyć tych linków, aby zapewnić pomoc techniczną i żądania obsługi plików w firmie Microsoft.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1cf7e7b62113bd96b00fdc2301e4e7ac4f5d4243
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548451"
---
# <a name="get-the-managed-services-for-a-customer-by-id"></a><span data-ttu-id="95630-105">Pobieranie usług zarządzanych dla klienta według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="95630-105">Get the managed services for a customer by ID</span></span>

<span data-ttu-id="95630-106">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="95630-106">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="95630-107">Pobiera usługi zarządzane dla klienta.</span><span class="sxs-lookup"><span data-stu-id="95630-107">Gets the managed services for a customer.</span></span> <span data-ttu-id="95630-108">Innymi słowy, uzyskaj linki do wszystkich subskrypcji klienta, do których masz delegowane uprawnienia administratora.</span><span class="sxs-lookup"><span data-stu-id="95630-108">In other words, get links to all of the customer's subscriptions for which you have delegated admin privileges.</span></span> <span data-ttu-id="95630-109">Możesz użyć tych linków, aby zapewnić pomoc techniczną i żądania obsługi plików w firmie Microsoft.</span><span class="sxs-lookup"><span data-stu-id="95630-109">You can use these links to provide support and file service requests with Microsoft.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95630-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="95630-110">Prerequisites</span></span>

- <span data-ttu-id="95630-111">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="95630-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="95630-112">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="95630-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="95630-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="95630-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="95630-114">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="95630-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="95630-115">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="95630-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="95630-116">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="95630-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="95630-117">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="95630-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="95630-118">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="95630-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="95630-119">C\#</span><span class="sxs-lookup"><span data-stu-id="95630-119">C\#</span></span>

<span data-ttu-id="95630-120">Aby wyświetlić listę wszystkich usług zarządzanych dla klienta, użyj kolekcji **IAggregatePartner.Customers** i wywołaj [**metodę ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="95630-120">To display a list of all the managed services for a customer, use your **IAggregatePartner.Customers** collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="95630-121">Następnie wywołaj [**właściwość ManagedServices,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) a następnie metody [**Get()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) lub [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="95630-121">Then call the [**ManagedServices**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerID as Customer;

ResourceCollection<ManagedService> managedServices = partnerOperations.Customers.ById(selectedCustomerId).ManagedServices.Get();
```

<span data-ttu-id="95630-122">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="95630-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="95630-123">**Project:** PartnerCenterSDK.FeaturesSamples, **klasa:** CustomerManagedServices.cs</span><span class="sxs-lookup"><span data-stu-id="95630-123">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: CustomerManagedServices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="95630-124">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="95630-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="95630-125">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="95630-125">Request syntax</span></span>

| <span data-ttu-id="95630-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="95630-126">Method</span></span>  | <span data-ttu-id="95630-127">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="95630-127">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="95630-128">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="95630-128">**GET**</span></span> | <span data-ttu-id="95630-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/managedservices HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="95630-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/managedservices HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="95630-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="95630-130">URI parameter</span></span>

<span data-ttu-id="95630-131">Użyj następującego parametru zapytania, aby pobrać usługi zarządzane przez klienta.</span><span class="sxs-lookup"><span data-stu-id="95630-131">Use the following query parameter to get the customer's managed services.</span></span>

| <span data-ttu-id="95630-132">Nazwa</span><span class="sxs-lookup"><span data-stu-id="95630-132">Name</span></span>                   | <span data-ttu-id="95630-133">Typ</span><span class="sxs-lookup"><span data-stu-id="95630-133">Type</span></span>     | <span data-ttu-id="95630-134">Wymagane</span><span class="sxs-lookup"><span data-stu-id="95630-134">Required</span></span> | <span data-ttu-id="95630-135">Opis</span><span class="sxs-lookup"><span data-stu-id="95630-135">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="95630-136">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="95630-136">**customer-tenant-id**</span></span> | <span data-ttu-id="95630-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="95630-137">**guid**</span></span> | <span data-ttu-id="95630-138">Y</span><span class="sxs-lookup"><span data-stu-id="95630-138">Y</span></span>        | <span data-ttu-id="95630-139">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="95630-139">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="95630-140">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="95630-140">Request headers</span></span>

<span data-ttu-id="95630-141">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="95630-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="95630-142">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="95630-142">Request body</span></span>

<span data-ttu-id="95630-143">Brak.</span><span class="sxs-lookup"><span data-stu-id="95630-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="95630-144">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="95630-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/managedservices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
```

## <a name="rest-response"></a><span data-ttu-id="95630-145">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="95630-145">REST response</span></span>

<span data-ttu-id="95630-146">W przypadku powodzenia ta metoda zwraca kolekcję obiektów **usługi zarządzanej** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="95630-146">If successful, this method returns a collection of **Managed Service** objects in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="95630-147">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="95630-147">Response success and error codes</span></span>

<span data-ttu-id="95630-148">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="95630-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="95630-149">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="95630-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="95630-150">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="95630-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="95630-151">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="95630-151">Response example</span></span>

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
