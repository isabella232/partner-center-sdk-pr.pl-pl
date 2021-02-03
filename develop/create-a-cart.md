---
title: Tworzenie koszyka
description: Dowiedz się, jak dodać zamówienie dla klienta w koszyku przy użyciu interfejsów API Centrum partnerskiego. Temat zawiera informacje dotyczące tworzenia koszyka i wymagania wstępne.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: a1c559b415a7d42af4e904e09795f92aed7f125f
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/07/2020
ms.locfileid: "97768626"
---
# <a name="create-a-cart-with-a-customer-order"></a><span data-ttu-id="0a6f2-104">Tworzenie koszyka przy użyciu zamówienia klienta</span><span class="sxs-lookup"><span data-stu-id="0a6f2-104">Create a cart with a customer order</span></span>

<span data-ttu-id="0a6f2-105">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="0a6f2-105">**Applies to:**</span></span>

- <span data-ttu-id="0a6f2-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="0a6f2-106">Partner Center</span></span>
- <span data-ttu-id="0a6f2-107">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="0a6f2-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="0a6f2-108">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="0a6f2-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="0a6f2-109">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0a6f2-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0a6f2-110">Możesz dodać zamówienie dla klienta w koszyku.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-110">You can add an order for a customer in a cart.</span></span> <span data-ttu-id="0a6f2-111">Aby uzyskać więcej informacji o tym, co jest obecnie dostępne do sprzedawania, zobacz [oferty partnerów w programie Cloud Solution Provider](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="0a6f2-111">For more information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a6f2-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0a6f2-112">Prerequisites</span></span>

- <span data-ttu-id="0a6f2-113">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0a6f2-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0a6f2-114">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-114">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="0a6f2-115">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0a6f2-115">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0a6f2-116">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-116">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0a6f2-117">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-117">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0a6f2-118">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-118">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0a6f2-119">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="0a6f2-119">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0a6f2-120">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0a6f2-120">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="0a6f2-121">C\#</span><span class="sxs-lookup"><span data-stu-id="0a6f2-121">C\#</span></span>

<span data-ttu-id="0a6f2-122">Aby utworzyć zamówienie dla klienta:</span><span class="sxs-lookup"><span data-stu-id="0a6f2-122">To create an order for a customer:</span></span>

1. <span data-ttu-id="0a6f2-123">Utwórz wystąpienie obiektu koszyka.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-123">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="0a6f2-124">Utwórz listę obiektów **CartLineItem** i przypisz listę do właściwości LineItems koszyka.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-124">Create a list of **CartLineItem** objects, and assign the list to the cart's LineItems property.</span></span> <span data-ttu-id="0a6f2-125">Każdy element wiersza koszyka zawiera informacje o zakupie jednego produktu.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-125">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="0a6f2-126">Musisz mieć co najmniej jeden element wiersza koszyka.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-126">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="0a6f2-127">Uzyskaj interfejs do operacji koszyka, wywołując metodę **IAggregatePartner. Customers. ById** z identyfikatorem klienta, aby zidentyfikować klienta, a następnie pobierając interfejs z właściwości **koszyka** .</span><span class="sxs-lookup"><span data-stu-id="0a6f2-127">Obtain an interface to cart operations by calling the **IAggregatePartner.Customers.ById** method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.</span></span>

4. <span data-ttu-id="0a6f2-128">Wywołaj metodę **Create** lub **onasync** , aby utworzyć koszyk.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-128">Call the **Create** or **CreateAsync** method to create the cart.</span></span>

### <a name="c-example"></a><span data-ttu-id="0a6f2-129">\#Przykład C</span><span class="sxs-lookup"><span data-stu-id="0a6f2-129">C\# example</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

var cart = new Cart()
{
    LineItems = new List<CartLineItem>()
    {
        new CartLineItem()
        {
      /* Microsoft Azure Subscription */
            Id = 0,
            CatalogItemId = "MS-AZR-0145P",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1Y"
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 1,
            CatalogItemId = "DZH318Z0BQ36:004G:DZH318Z08C0S",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P1Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 2,
            CatalogItemId = "DZH318Z0BQ36:004J:DZH318Z08B8X",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P3Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Perpetual Software */
            Id = 3,
            CatalogItemId = "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime
        },
        new CartLineItem()
        {
      /* SaaS */
            Id = 4,
            CatalogItemId = "DZH318Z0BXWC:0002:DZH318Z0BMRV",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1M"
        },
        new CartLineItem()
        {
      /* SaaS Free Trial */
            Id = 5,
            CatalogItemId = "DZH318Z0C0WF:0001:DZH318Z0BP69",
            Quantity = 10,
            BillingCycle = BillingCycleType.None,
            TermDuration = "P1M",
            RenewsTo = new RenewsTo
            {
                TermDuration = "P1Y"
            }
        }
    }
};

cart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

## <a name="java"></a><span data-ttu-id="0a6f2-130">Java</span><span class="sxs-lookup"><span data-stu-id="0a6f2-130">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="0a6f2-131">Aby utworzyć zamówienie dla klienta:</span><span class="sxs-lookup"><span data-stu-id="0a6f2-131">To create an order for a customer:</span></span>

1. <span data-ttu-id="0a6f2-132">Utwórz wystąpienie obiektu koszyka.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-132">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="0a6f2-133">Utwórz listę obiektów **CartLineItem** i przypisz listę do elementów linii koszyka.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-133">Create a list of **CartLineItem** objects, and assign the list to the cart's line items.</span></span> <span data-ttu-id="0a6f2-134">Każdy element wiersza koszyka zawiera informacje o zakupie jednego produktu.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-134">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="0a6f2-135">Musisz mieć co najmniej jeden element wiersza koszyka.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-135">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="0a6f2-136">Uzyskaj interfejs do operacji koszyka, wywołując funkcję **IAggregatePartner. GetCustomers (). byId** z identyfikatorem klienta, aby zidentyfikować klienta, a następnie pobierając interfejs z funkcji **getkoszyk** .</span><span class="sxs-lookup"><span data-stu-id="0a6f2-136">Obtain an interface to cart operations by calling the **IAggregatePartner.getCustomers().byId** function with the customer ID to identify the customer, and then retrieving the interface from the **getCart** function.</span></span>

4. <span data-ttu-id="0a6f2-137">Wywołaj funkcję **Create** , aby utworzyć koszyk.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-137">Call the **create** function to create the cart.</span></span>

## <a name="java-example"></a><span data-ttu-id="0a6f2-138">Przykład Java</span><span class="sxs-lookup"><span data-stu-id="0a6f2-138">Java example</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;
// String catalogItemId;

CartLineItem lineItem = new CartLineItem();

lineItem.setBillingCycle(BillingCycleType.OneTime);
lineItem.setCatalogItemId(catalogItemId);
lineItem.setFriendlyName("Sample RI Purchase");
lineItem.setQuantity(1);

Map<String, String> provisioningContext = new HashMap<String,String>();

provisioningContext.put("duration", "3Years");
provisioningContext.put("scope", "shared");
provisioningContext.put("subscriptionId", subscriptionId);

lineItem.setProvisioningContext(provisioningContext);

List<CartLineItem> lineItemList = new ArrayList<CartLineItem>();
lineItemList.add(lineItem);

Cart cart = new Cart();
cart.setLineItems(lineItemList);

Cart cartCreated = partnerOperations.getCustomers().byId(customerId).getCarts().create(cart);
```

## <a name="powershell"></a><span data-ttu-id="0a6f2-139">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a6f2-139">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="0a6f2-140">Aby utworzyć zamówienie dla klienta:</span><span class="sxs-lookup"><span data-stu-id="0a6f2-140">To create an order for a customer:</span></span>

1. <span data-ttu-id="0a6f2-141">Utwórz wystąpienie obiektu koszyka.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-141">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="0a6f2-142">Utwórz listę obiektów **CartLineItem** i przypisz listę do elementów linii koszyka.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-142">Create a list of **CartLineItem** objects, and assign the list to the cart's line items.</span></span> <span data-ttu-id="0a6f2-143">Każdy element wiersza koszyka zawiera informacje o zakupie jednego produktu.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-143">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="0a6f2-144">Musisz mieć co najmniej jeden element wiersza koszyka.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-144">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="0a6f2-145">Wykonaj polecenie [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) , aby utworzyć koszyk.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-145">Execute the [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) command to create the cart.</span></span>

```powershell
# $customerId
# $subscriptionId
# $catalogItemId

$lineItem = New-Object -TypeName Microsoft.Store.PartnerCenter.PowerShell.Models.Carts.PSCartLineItem

$lineItem.BillingCycle = 'OneTime'
$lineItem.CatalogItemId = $catalogItemId
$lineItem.FriendlyName = 'Sample RI Purchase'
$lineItem.ProvisioningContext.Add('duration', '1Year')
$lineItem.ProvisioningContext.Add('scope', 'shared')
$lineItem.ProvisioningContext.Add('subscriptionId', $subsciptionId)
$lineItem.Quantity = 10

New-PartnerCustomerCart -CustomerId $customerId -LineItems $lineItem
```

## <a name="rest-request"></a><span data-ttu-id="0a6f2-146">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="0a6f2-146">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0a6f2-147">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="0a6f2-147">Request syntax</span></span>

| <span data-ttu-id="0a6f2-148">Metoda</span><span class="sxs-lookup"><span data-stu-id="0a6f2-148">Method</span></span>   | <span data-ttu-id="0a6f2-149">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="0a6f2-149">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0a6f2-150">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="0a6f2-150">**POST**</span></span> | <span data-ttu-id="0a6f2-151">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/Carts http/1.1</span><span class="sxs-lookup"><span data-stu-id="0a6f2-151">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span></span>                        |

### <a name="uri-parameter"></a><span data-ttu-id="0a6f2-152">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="0a6f2-152">URI parameter</span></span>

<span data-ttu-id="0a6f2-153">Użyj następującego parametru ścieżki, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-153">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="0a6f2-154">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0a6f2-154">Name</span></span>            | <span data-ttu-id="0a6f2-155">Typ</span><span class="sxs-lookup"><span data-stu-id="0a6f2-155">Type</span></span>     | <span data-ttu-id="0a6f2-156">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0a6f2-156">Required</span></span> | <span data-ttu-id="0a6f2-157">Opis</span><span class="sxs-lookup"><span data-stu-id="0a6f2-157">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="0a6f2-158">**Identyfikator klienta**</span><span class="sxs-lookup"><span data-stu-id="0a6f2-158">**customer-id**</span></span> | <span data-ttu-id="0a6f2-159">ciąg</span><span class="sxs-lookup"><span data-stu-id="0a6f2-159">string</span></span>   | <span data-ttu-id="0a6f2-160">Tak</span><span class="sxs-lookup"><span data-stu-id="0a6f2-160">Yes</span></span>      | <span data-ttu-id="0a6f2-161">Identyfikator GUID sformatowany przez klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-161">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="0a6f2-162">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="0a6f2-162">Request headers</span></span>

<span data-ttu-id="0a6f2-163">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0a6f2-163">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0a6f2-164">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="0a6f2-164">Request body</span></span>

<span data-ttu-id="0a6f2-165">W tej tabeli opisano właściwości [koszyka](cart-resources.md) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-165">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="0a6f2-166">Właściwość</span><span class="sxs-lookup"><span data-stu-id="0a6f2-166">Property</span></span>              | <span data-ttu-id="0a6f2-167">Typ</span><span class="sxs-lookup"><span data-stu-id="0a6f2-167">Type</span></span>             | <span data-ttu-id="0a6f2-168">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0a6f2-168">Required</span></span>        | <span data-ttu-id="0a6f2-169">Opis</span><span class="sxs-lookup"><span data-stu-id="0a6f2-169">Description</span></span> |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0a6f2-170">identyfikator</span><span class="sxs-lookup"><span data-stu-id="0a6f2-170">id</span></span>                    | <span data-ttu-id="0a6f2-171">ciąg</span><span class="sxs-lookup"><span data-stu-id="0a6f2-171">string</span></span>           | <span data-ttu-id="0a6f2-172">Nie</span><span class="sxs-lookup"><span data-stu-id="0a6f2-172">No</span></span>              | <span data-ttu-id="0a6f2-173">Identyfikator koszyka, który jest dostarczany po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-173">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="0a6f2-174">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="0a6f2-174">creationTimeStamp</span></span>     | <span data-ttu-id="0a6f2-175">DateTime</span><span class="sxs-lookup"><span data-stu-id="0a6f2-175">DateTime</span></span>         | <span data-ttu-id="0a6f2-176">Nie</span><span class="sxs-lookup"><span data-stu-id="0a6f2-176">No</span></span>              | <span data-ttu-id="0a6f2-177">Data i godzina utworzenia koszyka.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-177">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="0a6f2-178">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-178">Applied upon successful creation of the cart.</span></span>         |
| <span data-ttu-id="0a6f2-179">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="0a6f2-179">lastModifiedTimeStamp</span></span> | <span data-ttu-id="0a6f2-180">DateTime</span><span class="sxs-lookup"><span data-stu-id="0a6f2-180">DateTime</span></span>         | <span data-ttu-id="0a6f2-181">Nie</span><span class="sxs-lookup"><span data-stu-id="0a6f2-181">No</span></span>              | <span data-ttu-id="0a6f2-182">Data ostatniej aktualizacji koszyka w formacie daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-182">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="0a6f2-183">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-183">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="0a6f2-184">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="0a6f2-184">expirationTimeStamp</span></span>   | <span data-ttu-id="0a6f2-185">DateTime</span><span class="sxs-lookup"><span data-stu-id="0a6f2-185">DateTime</span></span>         | <span data-ttu-id="0a6f2-186">Nie</span><span class="sxs-lookup"><span data-stu-id="0a6f2-186">No</span></span>              | <span data-ttu-id="0a6f2-187">Data wygaśnięcia koszyka w formacie daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-187">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="0a6f2-188">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-188">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="0a6f2-189">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="0a6f2-189">lastModifiedUser</span></span>      | <span data-ttu-id="0a6f2-190">ciąg</span><span class="sxs-lookup"><span data-stu-id="0a6f2-190">string</span></span>           | <span data-ttu-id="0a6f2-191">Nie</span><span class="sxs-lookup"><span data-stu-id="0a6f2-191">No</span></span>              | <span data-ttu-id="0a6f2-192">Użytkownik, który ostatnio zaktualizował koszyk.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-192">The user who last updated the cart.</span></span> <span data-ttu-id="0a6f2-193">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-193">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="0a6f2-194">lineItems</span><span class="sxs-lookup"><span data-stu-id="0a6f2-194">lineItems</span></span>             | <span data-ttu-id="0a6f2-195">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="0a6f2-195">Array of objects</span></span> | <span data-ttu-id="0a6f2-196">Tak</span><span class="sxs-lookup"><span data-stu-id="0a6f2-196">Yes</span></span>             | <span data-ttu-id="0a6f2-197">Tablica zasobów [CartLineItem](cart-resources.md#cartlineitem) .</span><span class="sxs-lookup"><span data-stu-id="0a6f2-197">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                     |

<span data-ttu-id="0a6f2-198">W tej tabeli opisano właściwości [CartLineItem](cart-resources.md#cartlineitem) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-198">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

|      <span data-ttu-id="0a6f2-199">Właściwość</span><span class="sxs-lookup"><span data-stu-id="0a6f2-199">Property</span></span>       |            <span data-ttu-id="0a6f2-200">Typ</span><span class="sxs-lookup"><span data-stu-id="0a6f2-200">Type</span></span>             | <span data-ttu-id="0a6f2-201">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0a6f2-201">Required</span></span> |                                                                                         <span data-ttu-id="0a6f2-202">Opis</span><span class="sxs-lookup"><span data-stu-id="0a6f2-202">Description</span></span>                                                                                         |
|---------------------|-----------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         <span data-ttu-id="0a6f2-203">identyfikator</span><span class="sxs-lookup"><span data-stu-id="0a6f2-203">id</span></span>          |           <span data-ttu-id="0a6f2-204">ciąg</span><span class="sxs-lookup"><span data-stu-id="0a6f2-204">string</span></span>            |    <span data-ttu-id="0a6f2-205">Nie</span><span class="sxs-lookup"><span data-stu-id="0a6f2-205">No</span></span>    |                                                     <span data-ttu-id="0a6f2-206">Unikatowy identyfikator dla elementu w wierszu koszyka.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-206">A Unique identifier for a cart line item.</span></span> <span data-ttu-id="0a6f2-207">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-207">Applied upon successful creation of cart.</span></span>                                                     |
|      <span data-ttu-id="0a6f2-208">catalogId</span><span class="sxs-lookup"><span data-stu-id="0a6f2-208">catalogId</span></span>      |           <span data-ttu-id="0a6f2-209">ciąg</span><span class="sxs-lookup"><span data-stu-id="0a6f2-209">string</span></span>            |   <span data-ttu-id="0a6f2-210">Tak</span><span class="sxs-lookup"><span data-stu-id="0a6f2-210">Yes</span></span>    |                                                                                <span data-ttu-id="0a6f2-211">Identyfikator elementu katalogu.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-211">The catalog item identifier.</span></span>                                                                                 |
|    <span data-ttu-id="0a6f2-212">friendlyName</span><span class="sxs-lookup"><span data-stu-id="0a6f2-212">friendlyName</span></span>     |           <span data-ttu-id="0a6f2-213">ciąg</span><span class="sxs-lookup"><span data-stu-id="0a6f2-213">string</span></span>            |    <span data-ttu-id="0a6f2-214">Nie</span><span class="sxs-lookup"><span data-stu-id="0a6f2-214">No</span></span>    |                                                    <span data-ttu-id="0a6f2-215">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-215">Optional.</span></span> <span data-ttu-id="0a6f2-216">Przyjazna nazwa dla elementu zdefiniowanego przez partnera, która pomaga w odróżnieniu od siebie.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-216">The friendly name for the item defined by the partner to help disambiguate.</span></span>                                                    |
|      <span data-ttu-id="0a6f2-217">quantity</span><span class="sxs-lookup"><span data-stu-id="0a6f2-217">quantity</span></span>       |             <span data-ttu-id="0a6f2-218">int</span><span class="sxs-lookup"><span data-stu-id="0a6f2-218">int</span></span>             |   <span data-ttu-id="0a6f2-219">Tak</span><span class="sxs-lookup"><span data-stu-id="0a6f2-219">Yes</span></span>    |                                                                            <span data-ttu-id="0a6f2-220">Liczba licencji lub wystąpień.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-220">The number of licenses or instances.</span></span>                                                                             |
|    <span data-ttu-id="0a6f2-221">currencyCode</span><span class="sxs-lookup"><span data-stu-id="0a6f2-221">currencyCode</span></span>     |           <span data-ttu-id="0a6f2-222">ciąg</span><span class="sxs-lookup"><span data-stu-id="0a6f2-222">string</span></span>            |    <span data-ttu-id="0a6f2-223">Nie</span><span class="sxs-lookup"><span data-stu-id="0a6f2-223">No</span></span>    |                                                                                     <span data-ttu-id="0a6f2-224">Kod waluty.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-224">The currency code.</span></span>                                                                                      |
|    <span data-ttu-id="0a6f2-225">billingCycle</span><span class="sxs-lookup"><span data-stu-id="0a6f2-225">billingCycle</span></span>     |           <span data-ttu-id="0a6f2-226">Obiekt</span><span class="sxs-lookup"><span data-stu-id="0a6f2-226">Object</span></span>            |   <span data-ttu-id="0a6f2-227">Tak</span><span class="sxs-lookup"><span data-stu-id="0a6f2-227">Yes</span></span>    |                                                                    <span data-ttu-id="0a6f2-228">Typ cyklu rozliczeniowego ustawiony dla bieżącego okresu.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-228">The type of billing cycle set for the current period.</span></span>                                                                    |
|    <span data-ttu-id="0a6f2-229">uczestnicy</span><span class="sxs-lookup"><span data-stu-id="0a6f2-229">participants</span></span>     | <span data-ttu-id="0a6f2-230">Lista par ciągów obiektów</span><span class="sxs-lookup"><span data-stu-id="0a6f2-230">List of Object String pairs</span></span> |    <span data-ttu-id="0a6f2-231">Nie</span><span class="sxs-lookup"><span data-stu-id="0a6f2-231">No</span></span>    |                                                                <span data-ttu-id="0a6f2-232">Kolekcja PartnerId on Record (MPNID) na zakupie.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-232">A collection of PartnerId on Record (MPNID) on the purchase.</span></span>                                                                 |
| <span data-ttu-id="0a6f2-233">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="0a6f2-233">provisioningContext</span></span> | <span data-ttu-id="0a6f2-234">Ciąg<słownika, ciąg></span><span class="sxs-lookup"><span data-stu-id="0a6f2-234">Dictionary<string, string></span></span>  |    <span data-ttu-id="0a6f2-235">Nie</span><span class="sxs-lookup"><span data-stu-id="0a6f2-235">No</span></span>    | <span data-ttu-id="0a6f2-236">Informacje wymagane do aprowizacji dla niektórych elementów w wykazie.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-236">Information required for provisioning for some items in the catalog.</span></span> <span data-ttu-id="0a6f2-237">Właściwość provisioningVariables w jednostce SKU wskazuje, które właściwości są wymagane dla określonych elementów w wykazie.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-237">The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.</span></span> |
|     <span data-ttu-id="0a6f2-238">kolejność</span><span class="sxs-lookup"><span data-stu-id="0a6f2-238">orderGroup</span></span>      |           <span data-ttu-id="0a6f2-239">ciąg</span><span class="sxs-lookup"><span data-stu-id="0a6f2-239">string</span></span>            |    <span data-ttu-id="0a6f2-240">Nie</span><span class="sxs-lookup"><span data-stu-id="0a6f2-240">No</span></span>    |                                                                   <span data-ttu-id="0a6f2-241">Grupa wskazująca, które elementy mogą być umieszczone razem.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-241">A group to indicate which items can be placed together.</span></span>                                                                   |
|        <span data-ttu-id="0a6f2-242">error</span><span class="sxs-lookup"><span data-stu-id="0a6f2-242">error</span></span>        |           <span data-ttu-id="0a6f2-243">Obiekt</span><span class="sxs-lookup"><span data-stu-id="0a6f2-243">Object</span></span>            |    <span data-ttu-id="0a6f2-244">Nie</span><span class="sxs-lookup"><span data-stu-id="0a6f2-244">No</span></span>    |                                                                     <span data-ttu-id="0a6f2-245">Zastosowano po utworzeniu koszyka w przypadku błędu.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-245">Applied after cart is created in case of an error.</span></span>                                                                      |
|     <span data-ttu-id="0a6f2-246">renewsTo</span><span class="sxs-lookup"><span data-stu-id="0a6f2-246">renewsTo</span></span>        | <span data-ttu-id="0a6f2-247">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="0a6f2-247">Array of objects</span></span>            |    <span data-ttu-id="0a6f2-248">Nie</span><span class="sxs-lookup"><span data-stu-id="0a6f2-248">No</span></span>    |                                                    <span data-ttu-id="0a6f2-249">Tablica zasobów [RenewsTo](cart-resources.md#renewsto) .</span><span class="sxs-lookup"><span data-stu-id="0a6f2-249">An array of [RenewsTo](cart-resources.md#renewsto) resources.</span></span>                                                                            |

<span data-ttu-id="0a6f2-250">W tej tabeli opisano właściwości [RenewsTo](cart-resources.md#renewsto) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-250">This table describes the [RenewsTo](cart-resources.md#renewsto) properties in the request body.</span></span>

| <span data-ttu-id="0a6f2-251">Właściwość</span><span class="sxs-lookup"><span data-stu-id="0a6f2-251">Property</span></span>              | <span data-ttu-id="0a6f2-252">Typ</span><span class="sxs-lookup"><span data-stu-id="0a6f2-252">Type</span></span>             | <span data-ttu-id="0a6f2-253">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0a6f2-253">Required</span></span>        | <span data-ttu-id="0a6f2-254">Opis</span><span class="sxs-lookup"><span data-stu-id="0a6f2-254">Description</span></span> |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0a6f2-255">termDuration</span><span class="sxs-lookup"><span data-stu-id="0a6f2-255">termDuration</span></span>          | <span data-ttu-id="0a6f2-256">ciąg</span><span class="sxs-lookup"><span data-stu-id="0a6f2-256">string</span></span>           | <span data-ttu-id="0a6f2-257">Nie</span><span class="sxs-lookup"><span data-stu-id="0a6f2-257">No</span></span>              | <span data-ttu-id="0a6f2-258">Reprezentacja ISO 8601 okresu ważności.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-258">An ISO 8601 representation of the renewal term's duration.</span></span> <span data-ttu-id="0a6f2-259">Bieżące obsługiwane wartości to **P1M** (1 miesiąc) i **P1Y** (1 rok).</span><span class="sxs-lookup"><span data-stu-id="0a6f2-259">The current supported values are **P1M** (1 month) and **P1Y** (1 year).</span></span> |

### <a name="request-example"></a><span data-ttu-id="0a6f2-260">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="0a6f2-260">Request example</span></span>

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 496
Expect: 100-continue

{
  "lineItems": [
    {
    /* Microsoft Azure Subscription */
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1Y"
    },
    {
    /* Azure Reserved Instance */
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      }
    },
    {
    /* Azure Reserved Instance */
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "single"
      }
    },
    {
    /* Perpetual Software */
      "id": 3,
      "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSFM",
      "quantity": 1,
      "billingCycle": "one_time"
    },
    {
    /* SaaS */
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1M"
    },
  {
    /* SaaS Free Trial */
       "id": 5,
       "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
       "quantity": 10,
       "billingCycle": "none",
       "termDuration": "P1M",
       "renewsTo": {
         "termDuration": "P1Y"
       }
    }
  ]
}
```

## <a name="rest-response"></a><span data-ttu-id="0a6f2-261">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="0a6f2-261">REST response</span></span>

<span data-ttu-id="0a6f2-262">Jeśli to się powiedzie, ta metoda zwraca zasób [koszyka](cart-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-262">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0a6f2-263">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="0a6f2-263">Response success and error codes</span></span>

<span data-ttu-id="0a6f2-264">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-264">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0a6f2-265">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="0a6f2-265">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0a6f2-266">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0a6f2-266">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0a6f2-267">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="0a6f2-267">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
{
  "id": "3655b1a0-b1c9-4268-9824-577fdbc4d0be",
  "creationTimestamp": "2019-01-16T00:45:41.6062996Z",
  "lastModifiedTimestamp": "2019-01-16T00:45:41.6062996Z",
  "expirationTimestamp": "2019-01-16T01:00:54.4188497Z",
  "lastModifiedUser": "1824b7fc-2fac-4478-b177-66823c40ab75",
  "status": "Active",
  "lineItems": [
    {
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1Y",
      "orderGroup": "OMS-0"
    },
    {
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 3,
      "catalogItemId": "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "orderGroup": "0"
    },
    {
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1M",
      "orderGroup": "1"
    },
  {
      "id": 5,
      "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
      "quantity": 10,
      "currencyCode": "USD",
      "billingCycle": "none",
      "termDuration": "P1M",
      "renewsTo": {
  "termDuration": "P1Y"
      },
    "orderGroup": "2"
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/28045616-f6b9-462f-9701-0d89b5e65c44/carts/3655b1a0-b1c9-4268-9824-577fdbc4d0be",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Cart"
  }
}
```
