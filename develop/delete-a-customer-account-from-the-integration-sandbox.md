---
title: Usuwanie konta klienta z piaskownicy integracji
description: Jak usunąć konto klienta z piaskownicy integracji w środowisku produkcyjnym (TIP).
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e3a1642c0202c174ddd4f65a6aeda2752def9176
ms.sourcegitcommit: b1ff781b67b1d322820bbcac2c583229201a8c07
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/29/2020
ms.locfileid: "97768157"
---
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a><span data-ttu-id="72623-103">Usuwanie konta klienta z piaskownicy integracji</span><span class="sxs-lookup"><span data-stu-id="72623-103">Delete a customer account from the integration sandbox</span></span>

<span data-ttu-id="72623-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="72623-104">**Applies to:**</span></span>

- <span data-ttu-id="72623-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="72623-105">Partner Center</span></span>
- <span data-ttu-id="72623-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="72623-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="72623-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="72623-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="72623-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="72623-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="72623-109">W tym artykule wyjaśniono, jak przerwać relację między partnerem a kontem klienta i odzyskać przydział do testowania w obszarze piaskownicy integracji produkcji (TIP).</span><span class="sxs-lookup"><span data-stu-id="72623-109">This article explains, how to break the relationship between the partner and the customer account and regain the quota for Testing in Production (Tip) integration sandbox.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72623-110">Usunięcie konta klienta spowoduje przeczyszczenie wszystkich zasobów skojarzonych z tą dzierżawą klienta.</span><span class="sxs-lookup"><span data-stu-id="72623-110">When you delete a customer account, all resources associated with that customer tenant will be purged.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72623-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="72623-111">Prerequisites</span></span>

- <span data-ttu-id="72623-112">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="72623-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="72623-113">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="72623-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="72623-114">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="72623-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="72623-115">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="72623-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="72623-116">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="72623-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="72623-117">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="72623-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="72623-118">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="72623-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="72623-119">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="72623-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="72623-120">Wszystkie Azure Reserved Virtual Machine Instances i zamówienia zakupu oprogramowania muszą zostać anulowane przed usunięciem klienta z piaskownicy integracji z poradami.</span><span class="sxs-lookup"><span data-stu-id="72623-120">All Azure Reserved Virtual Machine Instances and software purchase orders must be cancelled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="c"></a><span data-ttu-id="72623-121">C\#</span><span class="sxs-lookup"><span data-stu-id="72623-121">C\#</span></span>

<span data-ttu-id="72623-122">Aby usunąć klienta z piaskownicy integracji z poradami:</span><span class="sxs-lookup"><span data-stu-id="72623-122">To delete a customer from the Tip integration sandbox:</span></span>

1. <span data-ttu-id="72623-123">Przekaż poświadczenia konta TIP do metody [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) , aby uzyskać Interfejs [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) dla operacji partnerskich.</span><span class="sxs-lookup"><span data-stu-id="72623-123">Pass your Tip account credentials to the [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to partner operations.</span></span>

2. <span data-ttu-id="72623-124">Użyj interfejsu operacji partnera do pobrania kolekcji uprawnień:</span><span class="sxs-lookup"><span data-stu-id="72623-124">Use the partner operations interface to retrieve the collection of entitlements:</span></span>

    1. <span data-ttu-id="72623-125">Wywołaj metodę [**Customers. ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby określić klienta.</span><span class="sxs-lookup"><span data-stu-id="72623-125">Call the [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer.</span></span>

    2. <span data-ttu-id="72623-126">Wywołaj Właściwość **uprawnienia** .</span><span class="sxs-lookup"><span data-stu-id="72623-126">Call the **Entitlements** property.</span></span>

    3. <span data-ttu-id="72623-127">Wywołaj metodę **Get** lub **GetAsync** , aby pobrać kolekcję [**uprawnień**](entitlement-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="72623-127">Call the **Get** or **GetAsync** method to retrieve the [**Entitlement**](entitlement-resources.md) collection.</span></span>

3. <span data-ttu-id="72623-128">Upewnij się, że wszystkie Azure Reserved Virtual Machine Instances i zamówienia zakupu oprogramowania dla tego klienta zostały anulowane.</span><span class="sxs-lookup"><span data-stu-id="72623-128">Make sure that all Azure Reserved Virtual Machine Instances and software purchase orders for that customer are cancelled.</span></span> <span data-ttu-id="72623-129">Dla każdego [**uprawnienia**](entitlement-resources.md) w kolekcji:</span><span class="sxs-lookup"><span data-stu-id="72623-129">For each [**Entitlement**](entitlement-resources.md) in the collection:</span></span>

    1. <span data-ttu-id="72623-130">Użyj [**uprawnienia. ReferenceOrder.Id**](entitlement-resources.md#referenceorder) , aby uzyskać lokalną kopię odpowiedniej [kolejności](order-resources.md#order) z kolekcji zamówień klienta.</span><span class="sxs-lookup"><span data-stu-id="72623-130">Use the [**entitlement.ReferenceOrder.Id**](entitlement-resources.md#referenceorder) to get a local copy of the corresponding [Order](order-resources.md#order) from the customer's collection of orders.</span></span>

    2. <span data-ttu-id="72623-131">Ustaw właściwość [**Order. status**](order-resources.md#order) na wartość "anulowana".</span><span class="sxs-lookup"><span data-stu-id="72623-131">Set the [**Order.Status**](order-resources.md#order) property to "Cancelled".</span></span>

    3. <span data-ttu-id="72623-132">Aby zaktualizować kolejność, użyj metody **patch ()** .</span><span class="sxs-lookup"><span data-stu-id="72623-132">Use the **Patch()** method to update the order.</span></span>

4. <span data-ttu-id="72623-133">Anuluj wszystkie zamówienia.</span><span class="sxs-lookup"><span data-stu-id="72623-133">Cancel all orders.</span></span> <span data-ttu-id="72623-134">Na przykład poniższy kod przykład używa pętli, aby sondować każde zamówienie do momentu, gdy jego stan to "anulowane".</span><span class="sxs-lookup"><span data-stu-id="72623-134">For example, the following code sample uses a loop to poll each order until its status is "Cancelled".</span></span>

    ``` csharp
    // IPartnerCredentials tipAccountCredentials;
    // Customer tenant Id to be deleted.
    // string customerTenantId;

    IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

    // Get all entitlements whose order must be cancelled.
    ResourceCollection<Entitlement> entitlements = tipAccountPartnerOperations.Customers.ById(customerTenantId).Entitlements.Get();

    // Cancel all orders
    foreach (var entitlement in entitlements)
    {
        var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
        order.Status = "Cancelled";
        order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(order.Id).Patch(order);
    }

    // Keep polling until the status of all orders is "Cancelled".
    bool proceed = true;
    do
    {
        // Check if all the orders were cancelled.
        foreach (var entitlement in entitlements)
        {
            var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
            if (!order.Status.Equals("Cancelled", StringComparison.OrdinalIgnoreCase))
            {
                proceed = false;
            }
        }

        // Wait for a few seconds.
        Thread.Sleep(5000);
    }
    while (proceed == false);

    tipAccountPartnerOperations.Customers.ById(customerTenantId).Delete();
    ```

5. <span data-ttu-id="72623-135">Upewnij się, że wszystkie zamówienia zostały anulowane przez wywołanie metody **delete** dla klienta.</span><span class="sxs-lookup"><span data-stu-id="72623-135">Make sure all orders are cancelled by calling the **Delete** method for the customer.</span></span>

<span data-ttu-id="72623-136">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="72623-136">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="72623-137">**Projekt**: Partner Center PartnerCenterSDK. FeaturesSamples **klasy**: DeleteCustomerFromTipAccount.cs</span><span class="sxs-lookup"><span data-stu-id="72623-137">**Project**: Partner Center PartnerCenterSDK.FeaturesSamples **Class**: DeleteCustomerFromTipAccount.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="72623-138">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="72623-138">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="72623-139">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="72623-139">Request syntax</span></span>

| <span data-ttu-id="72623-140">Metoda</span><span class="sxs-lookup"><span data-stu-id="72623-140">Method</span></span>     | <span data-ttu-id="72623-141">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="72623-141">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="72623-142">DELETE</span><span class="sxs-lookup"><span data-stu-id="72623-142">DELETE</span></span>     | <span data-ttu-id="72623-143">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="72623-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="72623-144">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="72623-144">URI parameter</span></span>

<span data-ttu-id="72623-145">Użyj następującego parametru zapytania, aby usunąć klienta.</span><span class="sxs-lookup"><span data-stu-id="72623-145">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="72623-146">Nazwa</span><span class="sxs-lookup"><span data-stu-id="72623-146">Name</span></span>                   | <span data-ttu-id="72623-147">Typ</span><span class="sxs-lookup"><span data-stu-id="72623-147">Type</span></span>     | <span data-ttu-id="72623-148">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72623-148">Required</span></span> | <span data-ttu-id="72623-149">Opis</span><span class="sxs-lookup"><span data-stu-id="72623-149">Description</span></span>                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="72623-150">Identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="72623-150">customer-tenant-id</span></span>     | <span data-ttu-id="72623-151">GUID</span><span class="sxs-lookup"><span data-stu-id="72623-151">GUID</span></span>     | <span data-ttu-id="72623-152">Y</span><span class="sxs-lookup"><span data-stu-id="72623-152">Y</span></span>        | <span data-ttu-id="72623-153">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="72623-153">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="72623-154">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="72623-154">Request headers</span></span>

<span data-ttu-id="72623-155">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="72623-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="72623-156">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="72623-156">Request body</span></span>

<span data-ttu-id="72623-157">Brak.</span><span class="sxs-lookup"><span data-stu-id="72623-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="72623-158">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="72623-158">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="72623-159">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="72623-159">REST response</span></span>

<span data-ttu-id="72623-160">Jeśli to się powiedzie, ta metoda zwraca pustą odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="72623-160">If successful, this method returns an empty response.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="72623-161">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="72623-161">Response success and error codes</span></span>

<span data-ttu-id="72623-162">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="72623-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="72623-163">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="72623-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="72623-164">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="72623-164">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="72623-165">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="72623-165">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
