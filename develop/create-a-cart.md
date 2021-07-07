---
title: Tworzenie koszyka
description: Dowiedz się, jak Partner Center api do dodawania zamówienia dla klienta w koszyku. Temat zawiera informacje na temat tworzenia koszyka i wymagań wstępnych.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: dba54d4f6b97f3d0a51e2f87b32edca686466b89
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973778"
---
# <a name="create-a-cart-with-a-customer-order"></a><span data-ttu-id="44b88-104">Tworzenie koszyka z zamówieniem klienta</span><span class="sxs-lookup"><span data-stu-id="44b88-104">Create a cart with a customer order</span></span>

<span data-ttu-id="44b88-105">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="44b88-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="44b88-106">Możesz dodać zamówienie dla klienta w koszyku.</span><span class="sxs-lookup"><span data-stu-id="44b88-106">You can add an order for a customer in a cart.</span></span> <span data-ttu-id="44b88-107">Aby uzyskać więcej informacji o tym, co jest obecnie dostępne do sprzedaży, zobacz [Oferty partnerów w Dostawca rozwiązań w chmurze sprzedaży.](/partner-center/csp-offers)</span><span class="sxs-lookup"><span data-stu-id="44b88-107">For more information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44b88-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="44b88-108">Prerequisites</span></span>

- <span data-ttu-id="44b88-109">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="44b88-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="44b88-110">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="44b88-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="44b88-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="44b88-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="44b88-112">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="44b88-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="44b88-113">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="44b88-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="44b88-114">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="44b88-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="44b88-115">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="44b88-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="44b88-116">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="44b88-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="44b88-117">C\#</span><span class="sxs-lookup"><span data-stu-id="44b88-117">C\#</span></span>

<span data-ttu-id="44b88-118">Aby utworzyć zamówienie dla klienta:</span><span class="sxs-lookup"><span data-stu-id="44b88-118">To create an order for a customer:</span></span>

1. <span data-ttu-id="44b88-119">Utworzyć wystąpienia obiektu koszyka.</span><span class="sxs-lookup"><span data-stu-id="44b88-119">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="44b88-120">Utwórz listę obiektów **CartLineItem** i przypisz listę do właściwości LineItems koszyka.</span><span class="sxs-lookup"><span data-stu-id="44b88-120">Create a list of **CartLineItem** objects, and assign the list to the cart's LineItems property.</span></span> <span data-ttu-id="44b88-121">Każdy element koszyka zawiera informacje o zakupie dla jednego produktu.</span><span class="sxs-lookup"><span data-stu-id="44b88-121">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="44b88-122">Musisz mieć co najmniej jeden element wiersza koszyka.</span><span class="sxs-lookup"><span data-stu-id="44b88-122">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="44b88-123">Uzyskaj interfejs do obsługi operacji koszyka, wywołując metodę **IAggregatePartner.Customers.ById** z identyfikatorem klienta w celu zidentyfikowania klienta, a następnie pobierania interfejsu z właściwości **Cart.**</span><span class="sxs-lookup"><span data-stu-id="44b88-123">Obtain an interface to cart operations by calling the **IAggregatePartner.Customers.ById** method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.</span></span>

4. <span data-ttu-id="44b88-124">Wywołaj **metodę Create** lub **CreateAsync,** aby utworzyć koszyk.</span><span class="sxs-lookup"><span data-stu-id="44b88-124">Call the **Create** or **CreateAsync** method to create the cart.</span></span>

### <a name="c-example"></a><span data-ttu-id="44b88-125">Przykład w \# języku C</span><span class="sxs-lookup"><span data-stu-id="44b88-125">C\# example</span></span>

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

## <a name="java"></a><span data-ttu-id="44b88-126">Java</span><span class="sxs-lookup"><span data-stu-id="44b88-126">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="44b88-127">Aby utworzyć zamówienie dla klienta:</span><span class="sxs-lookup"><span data-stu-id="44b88-127">To create an order for a customer:</span></span>

1. <span data-ttu-id="44b88-128">Utworzyć wystąpienia obiektu koszyka.</span><span class="sxs-lookup"><span data-stu-id="44b88-128">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="44b88-129">Utwórz listę obiektów **CartLineItem** i przypisz listę do pozycji koszyka.</span><span class="sxs-lookup"><span data-stu-id="44b88-129">Create a list of **CartLineItem** objects, and assign the list to the cart's line items.</span></span> <span data-ttu-id="44b88-130">Każdy element koszyka zawiera informacje o zakupie dla jednego produktu.</span><span class="sxs-lookup"><span data-stu-id="44b88-130">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="44b88-131">Musisz mieć co najmniej jeden element wiersza koszyka.</span><span class="sxs-lookup"><span data-stu-id="44b88-131">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="44b88-132">Uzyskaj interfejs do obsługi operacji koszyka, wywołując funkcję **IAggregatePartner.getCustomers().byId** z identyfikatorem klienta w celu zidentyfikowania klienta, a następnie pobierz interfejs z funkcji **getCart.**</span><span class="sxs-lookup"><span data-stu-id="44b88-132">Obtain an interface to cart operations by calling the **IAggregatePartner.getCustomers().byId** function with the customer ID to identify the customer, and then retrieving the interface from the **getCart** function.</span></span>

4. <span data-ttu-id="44b88-133">Wywołaj **funkcję create,** aby utworzyć koszyk.</span><span class="sxs-lookup"><span data-stu-id="44b88-133">Call the **create** function to create the cart.</span></span>

## <a name="java-example"></a><span data-ttu-id="44b88-134">Przykład w języku Java</span><span class="sxs-lookup"><span data-stu-id="44b88-134">Java example</span></span>

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

## <a name="powershell"></a><span data-ttu-id="44b88-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="44b88-135">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="44b88-136">Aby utworzyć zamówienie dla klienta:</span><span class="sxs-lookup"><span data-stu-id="44b88-136">To create an order for a customer:</span></span>

1. <span data-ttu-id="44b88-137">Utworzyć wystąpienia obiektu koszyka.</span><span class="sxs-lookup"><span data-stu-id="44b88-137">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="44b88-138">Utwórz listę obiektów **CartLineItem** i przypisz listę do pozycji koszyka.</span><span class="sxs-lookup"><span data-stu-id="44b88-138">Create a list of **CartLineItem** objects, and assign the list to the cart's line items.</span></span> <span data-ttu-id="44b88-139">Każdy element koszyka zawiera informacje o zakupie dla jednego produktu.</span><span class="sxs-lookup"><span data-stu-id="44b88-139">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="44b88-140">Musisz mieć co najmniej jeden element wiersza koszyka.</span><span class="sxs-lookup"><span data-stu-id="44b88-140">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="44b88-141">Wykonaj polecenie [**New-PartnerCustomerCart,**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) aby utworzyć koszyk.</span><span class="sxs-lookup"><span data-stu-id="44b88-141">Execute the [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) command to create the cart.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="44b88-142">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="44b88-142">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="44b88-143">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="44b88-143">Request syntax</span></span>

| <span data-ttu-id="44b88-144">Metoda</span><span class="sxs-lookup"><span data-stu-id="44b88-144">Method</span></span>   | <span data-ttu-id="44b88-145">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="44b88-145">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="44b88-146">**Post**</span><span class="sxs-lookup"><span data-stu-id="44b88-146">**POST**</span></span> | <span data-ttu-id="44b88-147">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="44b88-147">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span></span>                        |

### <a name="uri-parameter"></a><span data-ttu-id="44b88-148">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="44b88-148">URI parameter</span></span>

<span data-ttu-id="44b88-149">Użyj następującego parametru ścieżki, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="44b88-149">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="44b88-150">Nazwa</span><span class="sxs-lookup"><span data-stu-id="44b88-150">Name</span></span>            | <span data-ttu-id="44b88-151">Typ</span><span class="sxs-lookup"><span data-stu-id="44b88-151">Type</span></span>     | <span data-ttu-id="44b88-152">Wymagane</span><span class="sxs-lookup"><span data-stu-id="44b88-152">Required</span></span> | <span data-ttu-id="44b88-153">Opis</span><span class="sxs-lookup"><span data-stu-id="44b88-153">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="44b88-154">**identyfikator klienta**</span><span class="sxs-lookup"><span data-stu-id="44b88-154">**customer-id**</span></span> | <span data-ttu-id="44b88-155">ciąg</span><span class="sxs-lookup"><span data-stu-id="44b88-155">string</span></span>   | <span data-ttu-id="44b88-156">Tak</span><span class="sxs-lookup"><span data-stu-id="44b88-156">Yes</span></span>      | <span data-ttu-id="44b88-157">Identyfikator GUID sformatowany jako identyfikator klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="44b88-157">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="44b88-158">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="44b88-158">Request headers</span></span>

<span data-ttu-id="44b88-159">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="44b88-159">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="44b88-160">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="44b88-160">Request body</span></span>

<span data-ttu-id="44b88-161">W tej tabeli [opisano](cart-resources.md) właściwości koszyka w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="44b88-161">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="44b88-162">Właściwość</span><span class="sxs-lookup"><span data-stu-id="44b88-162">Property</span></span>              | <span data-ttu-id="44b88-163">Typ</span><span class="sxs-lookup"><span data-stu-id="44b88-163">Type</span></span>             | <span data-ttu-id="44b88-164">Wymagane</span><span class="sxs-lookup"><span data-stu-id="44b88-164">Required</span></span>        | <span data-ttu-id="44b88-165">Opis</span><span class="sxs-lookup"><span data-stu-id="44b88-165">Description</span></span> |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="44b88-166">identyfikator</span><span class="sxs-lookup"><span data-stu-id="44b88-166">id</span></span>                    | <span data-ttu-id="44b88-167">ciąg</span><span class="sxs-lookup"><span data-stu-id="44b88-167">string</span></span>           | <span data-ttu-id="44b88-168">Nie</span><span class="sxs-lookup"><span data-stu-id="44b88-168">No</span></span>              | <span data-ttu-id="44b88-169">Identyfikator koszyka, który jest dostarczany po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="44b88-169">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="44b88-170">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="44b88-170">creationTimeStamp</span></span>     | <span data-ttu-id="44b88-171">DateTime</span><span class="sxs-lookup"><span data-stu-id="44b88-171">DateTime</span></span>         | <span data-ttu-id="44b88-172">Nie</span><span class="sxs-lookup"><span data-stu-id="44b88-172">No</span></span>              | <span data-ttu-id="44b88-173">Data utworzenia koszyka w formacie data/godzina.</span><span class="sxs-lookup"><span data-stu-id="44b88-173">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="44b88-174">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="44b88-174">Applied upon successful creation of the cart.</span></span>         |
| <span data-ttu-id="44b88-175">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="44b88-175">lastModifiedTimeStamp</span></span> | <span data-ttu-id="44b88-176">DateTime</span><span class="sxs-lookup"><span data-stu-id="44b88-176">DateTime</span></span>         | <span data-ttu-id="44b88-177">Nie</span><span class="sxs-lookup"><span data-stu-id="44b88-177">No</span></span>              | <span data-ttu-id="44b88-178">Data ostatniej aktualizacji koszyka w formacie data/godzina.</span><span class="sxs-lookup"><span data-stu-id="44b88-178">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="44b88-179">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="44b88-179">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="44b88-180">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="44b88-180">expirationTimeStamp</span></span>   | <span data-ttu-id="44b88-181">DateTime</span><span class="sxs-lookup"><span data-stu-id="44b88-181">DateTime</span></span>         | <span data-ttu-id="44b88-182">Nie</span><span class="sxs-lookup"><span data-stu-id="44b88-182">No</span></span>              | <span data-ttu-id="44b88-183">Data wygaśnięcia koszyka w formacie data/godzina.</span><span class="sxs-lookup"><span data-stu-id="44b88-183">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="44b88-184">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="44b88-184">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="44b88-185">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="44b88-185">lastModifiedUser</span></span>      | <span data-ttu-id="44b88-186">ciąg</span><span class="sxs-lookup"><span data-stu-id="44b88-186">string</span></span>           | <span data-ttu-id="44b88-187">Nie</span><span class="sxs-lookup"><span data-stu-id="44b88-187">No</span></span>              | <span data-ttu-id="44b88-188">Użytkownik, który ostatnio zaktualizował koszyk.</span><span class="sxs-lookup"><span data-stu-id="44b88-188">The user who last updated the cart.</span></span> <span data-ttu-id="44b88-189">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="44b88-189">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="44b88-190">lineItems</span><span class="sxs-lookup"><span data-stu-id="44b88-190">lineItems</span></span>             | <span data-ttu-id="44b88-191">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="44b88-191">Array of objects</span></span> | <span data-ttu-id="44b88-192">Tak</span><span class="sxs-lookup"><span data-stu-id="44b88-192">Yes</span></span>             | <span data-ttu-id="44b88-193">Tablica [zasobów CartLineItem.](cart-resources.md#cartlineitem)</span><span class="sxs-lookup"><span data-stu-id="44b88-193">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                     |

<span data-ttu-id="44b88-194">W tej tabeli [opisano właściwości CartLineItem](cart-resources.md#cartlineitem) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="44b88-194">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

|      <span data-ttu-id="44b88-195">Właściwość</span><span class="sxs-lookup"><span data-stu-id="44b88-195">Property</span></span>       |            <span data-ttu-id="44b88-196">Typ</span><span class="sxs-lookup"><span data-stu-id="44b88-196">Type</span></span>             | <span data-ttu-id="44b88-197">Wymagane</span><span class="sxs-lookup"><span data-stu-id="44b88-197">Required</span></span> |                                                                                         <span data-ttu-id="44b88-198">Opis</span><span class="sxs-lookup"><span data-stu-id="44b88-198">Description</span></span>                                                                                         |
|---------------------|-----------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         <span data-ttu-id="44b88-199">identyfikator</span><span class="sxs-lookup"><span data-stu-id="44b88-199">id</span></span>          |           <span data-ttu-id="44b88-200">ciąg</span><span class="sxs-lookup"><span data-stu-id="44b88-200">string</span></span>            |    <span data-ttu-id="44b88-201">Nie</span><span class="sxs-lookup"><span data-stu-id="44b88-201">No</span></span>    |                                                     <span data-ttu-id="44b88-202">Unikatowy identyfikator elementu wiersza koszyka.</span><span class="sxs-lookup"><span data-stu-id="44b88-202">A unique identifier for a cart line item.</span></span> <span data-ttu-id="44b88-203">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="44b88-203">Applied upon successful creation of cart.</span></span>                                                     |
|      <span data-ttu-id="44b88-204">catalogId</span><span class="sxs-lookup"><span data-stu-id="44b88-204">catalogId</span></span>      |           <span data-ttu-id="44b88-205">ciąg</span><span class="sxs-lookup"><span data-stu-id="44b88-205">string</span></span>            |   <span data-ttu-id="44b88-206">Tak</span><span class="sxs-lookup"><span data-stu-id="44b88-206">Yes</span></span>    |                                                                                <span data-ttu-id="44b88-207">Identyfikator elementu katalogu.</span><span class="sxs-lookup"><span data-stu-id="44b88-207">The catalog item identifier.</span></span>                                                                                 |
|    <span data-ttu-id="44b88-208">Friendlyname</span><span class="sxs-lookup"><span data-stu-id="44b88-208">friendlyName</span></span>     |           <span data-ttu-id="44b88-209">ciąg</span><span class="sxs-lookup"><span data-stu-id="44b88-209">string</span></span>            |    <span data-ttu-id="44b88-210">Nie</span><span class="sxs-lookup"><span data-stu-id="44b88-210">No</span></span>    |                                                    <span data-ttu-id="44b88-211">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="44b88-211">Optional.</span></span> <span data-ttu-id="44b88-212">Przyjazna nazwa elementu zdefiniowanego przez partnera w celu uujednoznania.</span><span class="sxs-lookup"><span data-stu-id="44b88-212">The friendly name for the item defined by the partner to help disambiguate.</span></span>                                                    |
|      <span data-ttu-id="44b88-213">quantity</span><span class="sxs-lookup"><span data-stu-id="44b88-213">quantity</span></span>       |             <span data-ttu-id="44b88-214">int</span><span class="sxs-lookup"><span data-stu-id="44b88-214">int</span></span>             |   <span data-ttu-id="44b88-215">Tak</span><span class="sxs-lookup"><span data-stu-id="44b88-215">Yes</span></span>    |                                                                            <span data-ttu-id="44b88-216">Liczba licencji lub wystąpień.</span><span class="sxs-lookup"><span data-stu-id="44b88-216">The number of licenses or instances.</span></span>                                                                             |
|    <span data-ttu-id="44b88-217">currencyCode</span><span class="sxs-lookup"><span data-stu-id="44b88-217">currencyCode</span></span>     |           <span data-ttu-id="44b88-218">ciąg</span><span class="sxs-lookup"><span data-stu-id="44b88-218">string</span></span>            |    <span data-ttu-id="44b88-219">Nie</span><span class="sxs-lookup"><span data-stu-id="44b88-219">No</span></span>    |                                                                                     <span data-ttu-id="44b88-220">Kod waluty.</span><span class="sxs-lookup"><span data-stu-id="44b88-220">The currency code.</span></span>                                                                                      |
|    <span data-ttu-id="44b88-221">billingCycle</span><span class="sxs-lookup"><span data-stu-id="44b88-221">billingCycle</span></span>     |           <span data-ttu-id="44b88-222">Obiekt</span><span class="sxs-lookup"><span data-stu-id="44b88-222">Object</span></span>            |   <span data-ttu-id="44b88-223">Tak</span><span class="sxs-lookup"><span data-stu-id="44b88-223">Yes</span></span>    |                                                                    <span data-ttu-id="44b88-224">Typ cyklu rozliczeniowego ustawiony dla bieżącego okresu.</span><span class="sxs-lookup"><span data-stu-id="44b88-224">The type of billing cycle set for the current period.</span></span>                                                                    |
|    <span data-ttu-id="44b88-225">uczestnicy</span><span class="sxs-lookup"><span data-stu-id="44b88-225">participants</span></span>     | <span data-ttu-id="44b88-226">Lista par ciągów obiektów</span><span class="sxs-lookup"><span data-stu-id="44b88-226">List of Object String pairs</span></span> |    <span data-ttu-id="44b88-227">Nie</span><span class="sxs-lookup"><span data-stu-id="44b88-227">No</span></span>    |                                                                <span data-ttu-id="44b88-228">Kolekcja PartnerId on Record (MPNID) w zakupie.</span><span class="sxs-lookup"><span data-stu-id="44b88-228">A collection of PartnerId on Record (MPNID) on the purchase.</span></span>                                                                 |
| <span data-ttu-id="44b88-229">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="44b88-229">provisioningContext</span></span> | <span data-ttu-id="44b88-230">Słownik<ciąg, ciąg></span><span class="sxs-lookup"><span data-stu-id="44b88-230">Dictionary<string, string></span></span>  |    <span data-ttu-id="44b88-231">Nie</span><span class="sxs-lookup"><span data-stu-id="44b88-231">No</span></span>    | <span data-ttu-id="44b88-232">Informacje wymagane do aprowizowania niektórych elementów w wykazie.</span><span class="sxs-lookup"><span data-stu-id="44b88-232">Information required for provisioning for some items in the catalog.</span></span> <span data-ttu-id="44b88-233">Właściwość provisioningVariables w sku wskazuje, które właściwości są wymagane dla określonych elementów w wykazie.</span><span class="sxs-lookup"><span data-stu-id="44b88-233">The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.</span></span> |
|     <span data-ttu-id="44b88-234">orderGroup</span><span class="sxs-lookup"><span data-stu-id="44b88-234">orderGroup</span></span>      |           <span data-ttu-id="44b88-235">ciąg</span><span class="sxs-lookup"><span data-stu-id="44b88-235">string</span></span>            |    <span data-ttu-id="44b88-236">Nie</span><span class="sxs-lookup"><span data-stu-id="44b88-236">No</span></span>    |                                                                   <span data-ttu-id="44b88-237">Grupa wskazująca, które elementy można ze sobą umieścić.</span><span class="sxs-lookup"><span data-stu-id="44b88-237">A group to indicate which items can be placed together.</span></span>                                                                   |
|        <span data-ttu-id="44b88-238">error</span><span class="sxs-lookup"><span data-stu-id="44b88-238">error</span></span>        |           <span data-ttu-id="44b88-239">Obiekt</span><span class="sxs-lookup"><span data-stu-id="44b88-239">Object</span></span>            |    <span data-ttu-id="44b88-240">Nie</span><span class="sxs-lookup"><span data-stu-id="44b88-240">No</span></span>    |                                                                     <span data-ttu-id="44b88-241">Zastosowane po utworzeniu koszyka, jeśli wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="44b88-241">Applied after cart is created if there is an error.</span></span>                                                                      |
|     <span data-ttu-id="44b88-242">renewsTo</span><span class="sxs-lookup"><span data-stu-id="44b88-242">renewsTo</span></span>        | <span data-ttu-id="44b88-243">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="44b88-243">Array of objects</span></span>            |    <span data-ttu-id="44b88-244">Nie</span><span class="sxs-lookup"><span data-stu-id="44b88-244">No</span></span>    |                                                    <span data-ttu-id="44b88-245">Tablica zasobów [RenewsTo.](cart-resources.md#renewsto)</span><span class="sxs-lookup"><span data-stu-id="44b88-245">An array of [RenewsTo](cart-resources.md#renewsto) resources.</span></span>                                                                            |

<span data-ttu-id="44b88-246">W tej tabeli opisano [właściwości RenewsTo](cart-resources.md#renewsto) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="44b88-246">This table describes the [RenewsTo](cart-resources.md#renewsto) properties in the request body.</span></span>

| <span data-ttu-id="44b88-247">Właściwość</span><span class="sxs-lookup"><span data-stu-id="44b88-247">Property</span></span>              | <span data-ttu-id="44b88-248">Typ</span><span class="sxs-lookup"><span data-stu-id="44b88-248">Type</span></span>             | <span data-ttu-id="44b88-249">Wymagane</span><span class="sxs-lookup"><span data-stu-id="44b88-249">Required</span></span>        | <span data-ttu-id="44b88-250">Opis</span><span class="sxs-lookup"><span data-stu-id="44b88-250">Description</span></span> |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="44b88-251">termDuration</span><span class="sxs-lookup"><span data-stu-id="44b88-251">termDuration</span></span>          | <span data-ttu-id="44b88-252">ciąg</span><span class="sxs-lookup"><span data-stu-id="44b88-252">string</span></span>           | <span data-ttu-id="44b88-253">Nie</span><span class="sxs-lookup"><span data-stu-id="44b88-253">No</span></span>              | <span data-ttu-id="44b88-254">Reprezentacja iso 8601 czasu trwania okresu odnowienia.</span><span class="sxs-lookup"><span data-stu-id="44b88-254">An ISO 8601 representation of the renewal term's duration.</span></span> <span data-ttu-id="44b88-255">Obecnie obsługiwane wartości to **P1M** (1 miesiąc) i **P1Y** (1 rok).</span><span class="sxs-lookup"><span data-stu-id="44b88-255">The current supported values are **P1M** (1 month) and **P1Y** (1 year).</span></span> |

### <a name="request-example"></a><span data-ttu-id="44b88-256">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="44b88-256">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="44b88-257">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="44b88-257">REST response</span></span>

<span data-ttu-id="44b88-258">W przypadku powodzenia ta metoda zwraca wypełniony zasób [koszyka](cart-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="44b88-258">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="44b88-259">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="44b88-259">Response success and error codes</span></span>

<span data-ttu-id="44b88-260">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="44b88-260">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="44b88-261">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="44b88-261">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="44b88-262">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="44b88-262">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="44b88-263">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="44b88-263">Response example</span></span>

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
