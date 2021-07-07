---
title: Usuwanie konta klienta z piaskownicy integracji
description: Jak usunąć konto klienta z piaskownicy integracji Testowanie w środowisku produkcyjnym (porada).
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b9d9e44ac9c40bd4e3c7e1a9e04253f853dfd96c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973132"
---
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a><span data-ttu-id="e6713-103">Usuwanie konta klienta z piaskownicy integracji</span><span class="sxs-lookup"><span data-stu-id="e6713-103">Delete a customer account from the integration sandbox</span></span>

<span data-ttu-id="e6713-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e6713-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e6713-105">W tym artykule wyjaśniono, jak przerwać relację między partnerem a kontem klienta i odzyskać limit przydziału piaskownicy integracji Testowanie w środowisku produkcyjnym (porada).</span><span class="sxs-lookup"><span data-stu-id="e6713-105">This article explains, how to break the relationship between the partner and the customer account and regain the quota for Testing in Production (Tip) integration sandbox.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6713-106">Usunięcie konta klienta spowoduje usunięcie wszystkich zasobów skojarzonych z tą dzierżawą klienta.</span><span class="sxs-lookup"><span data-stu-id="e6713-106">When you delete a customer account, all resources associated with that customer tenant will be purged.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6713-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e6713-107">Prerequisites</span></span>

- <span data-ttu-id="e6713-108">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e6713-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e6713-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e6713-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e6713-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e6713-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e6713-111">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="e6713-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e6713-112">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="e6713-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e6713-113">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="e6713-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e6713-114">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="e6713-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e6713-115">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e6713-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="e6713-116">Wszystkie Azure Reserved Virtual Machine Instances i zamówienia zakupu oprogramowania muszą zostać anulowane przed usunięciem klienta z piaskownicy integracji Porada.</span><span class="sxs-lookup"><span data-stu-id="e6713-116">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="c"></a><span data-ttu-id="e6713-117">C\#</span><span class="sxs-lookup"><span data-stu-id="e6713-117">C\#</span></span>

<span data-ttu-id="e6713-118">Aby usunąć klienta z piaskownicy Porada integracji:</span><span class="sxs-lookup"><span data-stu-id="e6713-118">To delete a customer from the Tip integration sandbox:</span></span>

1. <span data-ttu-id="e6713-119">Przekaż swoje poświadczenia konta Porada do [**metody CreatePartnerOperations,**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) aby uzyskać interfejs [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) do operacji partnera.</span><span class="sxs-lookup"><span data-stu-id="e6713-119">Pass your Tip account credentials to the [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to partner operations.</span></span>

2. <span data-ttu-id="e6713-120">Użyj interfejsu operacji partnera, aby pobrać kolekcję uprawnień:</span><span class="sxs-lookup"><span data-stu-id="e6713-120">Use the partner operations interface to retrieve the collection of entitlements:</span></span>

    1. <span data-ttu-id="e6713-121">Wywołaj [**metodę Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby określić klienta.</span><span class="sxs-lookup"><span data-stu-id="e6713-121">Call the [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer.</span></span>

    2. <span data-ttu-id="e6713-122">Wywołaj **właściwość Entitlements.**</span><span class="sxs-lookup"><span data-stu-id="e6713-122">Call the **Entitlements** property.</span></span>

    3. <span data-ttu-id="e6713-123">Wywołaj **metodę Get** lub **GetAsync,** aby pobrać [**kolekcję entitlement.**](entitlement-resources.md)</span><span class="sxs-lookup"><span data-stu-id="e6713-123">Call the **Get** or **GetAsync** method to retrieve the [**Entitlement**](entitlement-resources.md) collection.</span></span>

3. <span data-ttu-id="e6713-124">Upewnij się, że Azure Reserved Virtual Machine Instances i zamówienia zakupu oprogramowania dla tego klienta zostały anulowane.</span><span class="sxs-lookup"><span data-stu-id="e6713-124">Make sure that all Azure Reserved Virtual Machine Instances and software purchase orders for that customer are canceled.</span></span> <span data-ttu-id="e6713-125">Dla każdego [**uprawnienia**](entitlement-resources.md) w kolekcji:</span><span class="sxs-lookup"><span data-stu-id="e6713-125">For each [**Entitlement**](entitlement-resources.md) in the collection:</span></span>

    1. <span data-ttu-id="e6713-126">Użyj [**uprawnienia . ReferenceOrder.Id**](entitlement-resources.md#referenceorder) uzyskać lokalną kopię odpowiedniego [](order-resources.md#order) zamówienia z kolekcji zamówień klienta.</span><span class="sxs-lookup"><span data-stu-id="e6713-126">Use the [**entitlement.ReferenceOrder.Id**](entitlement-resources.md#referenceorder) to get a local copy of the corresponding [Order](order-resources.md#order) from the customer's collection of orders.</span></span>

    2. <span data-ttu-id="e6713-127">Ustaw właściwość [**Order.Status**](order-resources.md#order) na wartość "Cancelled".</span><span class="sxs-lookup"><span data-stu-id="e6713-127">Set the [**Order.Status**](order-resources.md#order) property to "Cancelled".</span></span>

    3. <span data-ttu-id="e6713-128">Użyj metody **Patch(),** aby zaktualizować zamówienie.</span><span class="sxs-lookup"><span data-stu-id="e6713-128">Use the **Patch()** method to update the order.</span></span>

4. <span data-ttu-id="e6713-129">Anuluj wszystkie zamówienia.</span><span class="sxs-lookup"><span data-stu-id="e6713-129">Cancel all orders.</span></span> <span data-ttu-id="e6713-130">Na przykład poniższy przykład kodu używa pętli do sondowania każdego zamówienia do momentu, gdy jego stan to "Cancelled".</span><span class="sxs-lookup"><span data-stu-id="e6713-130">For example, the following code sample uses a loop to poll each order until its status is "Cancelled".</span></span>

    ``` csharp
    // IPartnerCredentials tipAccountCredentials;
    // Customer tenant Id to be deleted.
    // string customerTenantId;

    IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

    // Get all entitlements whose order must be canceled.
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
        // Check if all the orders were canceled.
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

5. <span data-ttu-id="e6713-131">Upewnij się, że wszystkie zamówienia zostały anulowane, wywołując **metodę Delete** dla klienta.</span><span class="sxs-lookup"><span data-stu-id="e6713-131">Make sure all orders are canceled by calling the **Delete** method for the customer.</span></span>

<span data-ttu-id="e6713-132">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e6713-132">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e6713-133">**Project:** Partner Center PartnerCenterSDK.FeaturesSamples, **klasa**: DeleteCustomerFromTipAccount.cs</span><span class="sxs-lookup"><span data-stu-id="e6713-133">**Project**: Partner Center PartnerCenterSDK.FeaturesSamples **Class**: DeleteCustomerFromTipAccount.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e6713-134">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="e6713-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e6713-135">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="e6713-135">Request syntax</span></span>

| <span data-ttu-id="e6713-136">Metoda</span><span class="sxs-lookup"><span data-stu-id="e6713-136">Method</span></span>     | <span data-ttu-id="e6713-137">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="e6713-137">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="e6713-138">DELETE</span><span class="sxs-lookup"><span data-stu-id="e6713-138">DELETE</span></span>     | <span data-ttu-id="e6713-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e6713-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="e6713-140">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="e6713-140">URI parameter</span></span>

<span data-ttu-id="e6713-141">Użyj następującego parametru zapytania, aby usunąć klienta.</span><span class="sxs-lookup"><span data-stu-id="e6713-141">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="e6713-142">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e6713-142">Name</span></span>                   | <span data-ttu-id="e6713-143">Typ</span><span class="sxs-lookup"><span data-stu-id="e6713-143">Type</span></span>     | <span data-ttu-id="e6713-144">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e6713-144">Required</span></span> | <span data-ttu-id="e6713-145">Opis</span><span class="sxs-lookup"><span data-stu-id="e6713-145">Description</span></span>                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="e6713-146">identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="e6713-146">customer-tenant-id</span></span>     | <span data-ttu-id="e6713-147">GUID</span><span class="sxs-lookup"><span data-stu-id="e6713-147">GUID</span></span>     | <span data-ttu-id="e6713-148">Y</span><span class="sxs-lookup"><span data-stu-id="e6713-148">Y</span></span>        | <span data-ttu-id="e6713-149">Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="e6713-149">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e6713-150">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="e6713-150">Request headers</span></span>

<span data-ttu-id="e6713-151">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e6713-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e6713-152">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="e6713-152">Request body</span></span>

<span data-ttu-id="e6713-153">Brak.</span><span class="sxs-lookup"><span data-stu-id="e6713-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e6713-154">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="e6713-154">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="e6713-155">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="e6713-155">REST response</span></span>

<span data-ttu-id="e6713-156">W przypadku powodzenia ta metoda zwraca pustą odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="e6713-156">If successful, this method returns an empty response.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e6713-157">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e6713-157">Response success and error codes</span></span>

<span data-ttu-id="e6713-158">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="e6713-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e6713-159">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="e6713-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e6713-160">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e6713-160">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e6713-161">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e6713-161">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
