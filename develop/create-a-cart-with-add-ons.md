---
title: Tworzenie koszyka z dodatkami
description: Dowiedz się, jak używać Partner Center API do dodawania zamówienia klienta z dodatkimi za pośrednictwem koszyka. Artykuł udostępnia wymagania wstępne i kroki tworzenia koszyka z dodatków.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 513a9607b9194c36253630c91de9622325317c3a
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973761"
---
# <a name="create-a-cart-with-add-ons-to-a-customer-order"></a><span data-ttu-id="ec045-104">Tworzenie koszyka z dodatkimi do zamówienia klienta</span><span class="sxs-lookup"><span data-stu-id="ec045-104">Create a cart with add-ons to a customer order</span></span>

<span data-ttu-id="ec045-105">Dodatki można kupić za pośrednictwem koszyka.</span><span class="sxs-lookup"><span data-stu-id="ec045-105">You can purchase add-ons through a cart.</span></span> <span data-ttu-id="ec045-106">Aby uzyskać więcej informacji o tym, co jest obecnie dostępne do sprzedaży, zobacz [Oferty partnerów w Dostawca rozwiązań w chmurze sprzedaży.](/partner-center/csp-offers)</span><span class="sxs-lookup"><span data-stu-id="ec045-106">For more information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec045-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ec045-107">Prerequisites</span></span>

- <span data-ttu-id="ec045-108">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ec045-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ec045-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ec045-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="ec045-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ec045-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ec045-111">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="ec045-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ec045-112">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="ec045-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ec045-113">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="ec045-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ec045-114">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="ec045-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ec045-115">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ec045-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="ec045-116">C\#</span><span class="sxs-lookup"><span data-stu-id="ec045-116">C\#</span></span>

<span data-ttu-id="ec045-117">Koszyk umożliwia zakup oferty podstawowej i odpowiadających jej dodatków.</span><span class="sxs-lookup"><span data-stu-id="ec045-117">A cart enables the purchase of a base offer and its corresponding add-ons.</span></span> <span data-ttu-id="ec045-118">Wykonaj następujące kroki, aby utworzyć koszyk:</span><span class="sxs-lookup"><span data-stu-id="ec045-118">Follow these steps to create a cart:</span></span>

1. <span data-ttu-id="ec045-119">Utworzyć wystąpienia obiektu [**koszyka.**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart)</span><span class="sxs-lookup"><span data-stu-id="ec045-119">Instantiate a [**Cart**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) object.</span></span>

2. <span data-ttu-id="ec045-120">Utwórz listę obiektów [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) reprezentujących oferty podstawowe i przypisz listę do właściwości [**LineItems koszyka.**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems)</span><span class="sxs-lookup"><span data-stu-id="ec045-120">Create a list of [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) objects that represent the base offer(s), and assign the list to the cart's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) property.</span></span>

3. <span data-ttu-id="ec045-121">W obszarze każdego elementu koszyka oferty podstawowej wypełnij listę elementów **AddOnItems** innymi obiektami **CartLineItem,** z których każdy reprezentuje dodatek, który zostanie zakupiony względem tej oferty podstawowej.</span><span class="sxs-lookup"><span data-stu-id="ec045-121">Under each base offer's cart line item, populate the list of **AddOnItems** with other **CartLineItem** objects that each represent an add-on that will be purchased against that base offer.</span></span>

4. <span data-ttu-id="ec045-122">Uzyskaj interfejs do obsługi operacji koszyka przy użyciu narzędzia [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) w celu wywołania metody [**ICustomerCollection.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta, a następnie pobierania interfejsu z właściwości **Cart.**</span><span class="sxs-lookup"><span data-stu-id="ec045-122">Obtain an interface to cart operations by using [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) to call the [**ICustomerCollection.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.</span></span>

5. <span data-ttu-id="ec045-123">Na koniec wywołaj [**metodę Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) lub [**CreateAsync,**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) aby utworzyć koszyk.</span><span class="sxs-lookup"><span data-stu-id="ec045-123">Finally, call the [**Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) method to create the cart.</span></span>

### <a name="c-example"></a><span data-ttu-id="ec045-124">Przykład w \# języku C</span><span class="sxs-lookup"><span data-stu-id="ec045-124">C\# example</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "A_base_offer_ID",
                FriendlyName = "Myofferpurchase",
                Quantity = 3,
                BillingCycle = BillingCycleType.Monthly,
                AddonItems = new List<CartLineItem>
                {
                    new CartLineItem
                    {
                        Id = 1,
                        CatalogItemId = "An_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 2,
                    },
                    new CartLineItem
                    {
                        Id = 2,
                        CatalogItemId = "Another_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 3
                    }
                }
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

<span data-ttu-id="ec045-125">Wykonaj następujące kroki, aby utworzyć koszyk, który umożliwi zakup dodatków dla istniejących subskrypcji podstawowych:</span><span class="sxs-lookup"><span data-stu-id="ec045-125">Follow these steps to create a cart that will enable the purchase of add-on(s) against existing base subscription(s):</span></span>

1. <span data-ttu-id="ec045-126">Utwórz koszyk **z** nowym elementem **CartLineItem** zawierającym identyfikator subskrypcji we właściwości **ProvisioningContext z** kluczem "ParentSubscriptionId".</span><span class="sxs-lookup"><span data-stu-id="ec045-126">Create a **Cart** with a new **CartLineItem** containing the subscription ID in the **ProvisioningContext** property with key "ParentSubscriptionId".</span></span>

2. <span data-ttu-id="ec045-127">Wywołaj **metodę Create** lub **CreateAsync.**</span><span class="sxs-lookup"><span data-stu-id="ec045-127">Call the **Create** or **CreateAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "An_addon_item_ID",
                ProvisioningContext = new Dictionary<string, string>
                {
                    {
                        "ParentSubscriptionId", "An_existing_subscription_Id"
                    }
                },
                Quantity = 1,
                BillingCycle = BillingCycleType.Annual,
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(selectedCustomerId).Carts.Create(cart);
```

## <a name="rest-request"></a><span data-ttu-id="ec045-128">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="ec045-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ec045-129">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="ec045-129">Request syntax</span></span>

| <span data-ttu-id="ec045-130">Metoda</span><span class="sxs-lookup"><span data-stu-id="ec045-130">Method</span></span>   | <span data-ttu-id="ec045-131">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="ec045-131">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ec045-132">**Post**</span><span class="sxs-lookup"><span data-stu-id="ec045-132">**POST**</span></span> | <span data-ttu-id="ec045-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ec045-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span></span>                        |

#### <a name="uri-parameter"></a><span data-ttu-id="ec045-134">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="ec045-134">URI parameter</span></span>

<span data-ttu-id="ec045-135">Użyj następującego parametru ścieżki, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="ec045-135">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="ec045-136">Nazwa</span><span class="sxs-lookup"><span data-stu-id="ec045-136">Name</span></span>            | <span data-ttu-id="ec045-137">Typ</span><span class="sxs-lookup"><span data-stu-id="ec045-137">Type</span></span>     | <span data-ttu-id="ec045-138">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ec045-138">Required</span></span> | <span data-ttu-id="ec045-139">Opis</span><span class="sxs-lookup"><span data-stu-id="ec045-139">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="ec045-140">**identyfikator klienta**</span><span class="sxs-lookup"><span data-stu-id="ec045-140">**customer-id**</span></span> | <span data-ttu-id="ec045-141">ciąg</span><span class="sxs-lookup"><span data-stu-id="ec045-141">string</span></span>   | <span data-ttu-id="ec045-142">Tak</span><span class="sxs-lookup"><span data-stu-id="ec045-142">Yes</span></span>      | <span data-ttu-id="ec045-143">Identyfikator GUID sformatowany jako identyfikator klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="ec045-143">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="ec045-144">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="ec045-144">Request headers</span></span>

<span data-ttu-id="ec045-145">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ec045-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ec045-146">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="ec045-146">Request body</span></span>

<span data-ttu-id="ec045-147">W tej tabeli [opisano](cart-resources.md) właściwości koszyka w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="ec045-147">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="ec045-148">Właściwość</span><span class="sxs-lookup"><span data-stu-id="ec045-148">Property</span></span>              | <span data-ttu-id="ec045-149">Typ</span><span class="sxs-lookup"><span data-stu-id="ec045-149">Type</span></span>             | <span data-ttu-id="ec045-150">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ec045-150">Required</span></span>        | <span data-ttu-id="ec045-151">Opis</span><span class="sxs-lookup"><span data-stu-id="ec045-151">Description</span></span> |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ec045-152">identyfikator</span><span class="sxs-lookup"><span data-stu-id="ec045-152">id</span></span>                    | <span data-ttu-id="ec045-153">ciąg</span><span class="sxs-lookup"><span data-stu-id="ec045-153">string</span></span>           | <span data-ttu-id="ec045-154">Nie</span><span class="sxs-lookup"><span data-stu-id="ec045-154">No</span></span>              | <span data-ttu-id="ec045-155">Identyfikator koszyka, który jest dostarczany po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="ec045-155">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="ec045-156">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="ec045-156">creationTimeStamp</span></span>     | <span data-ttu-id="ec045-157">DateTime</span><span class="sxs-lookup"><span data-stu-id="ec045-157">DateTime</span></span>         | <span data-ttu-id="ec045-158">Nie</span><span class="sxs-lookup"><span data-stu-id="ec045-158">No</span></span>              | <span data-ttu-id="ec045-159">Data utworzenia koszyka w formacie data/godzina.</span><span class="sxs-lookup"><span data-stu-id="ec045-159">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="ec045-160">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="ec045-160">Applied upon successful creation of the cart.</span></span>         |
| <span data-ttu-id="ec045-161">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="ec045-161">lastModifiedTimeStamp</span></span> | <span data-ttu-id="ec045-162">DateTime</span><span class="sxs-lookup"><span data-stu-id="ec045-162">DateTime</span></span>         | <span data-ttu-id="ec045-163">Nie</span><span class="sxs-lookup"><span data-stu-id="ec045-163">No</span></span>              | <span data-ttu-id="ec045-164">Data ostatniej aktualizacji koszyka w formacie data/godzina.</span><span class="sxs-lookup"><span data-stu-id="ec045-164">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="ec045-165">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="ec045-165">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="ec045-166">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="ec045-166">expirationTimeStamp</span></span>   | <span data-ttu-id="ec045-167">DateTime</span><span class="sxs-lookup"><span data-stu-id="ec045-167">DateTime</span></span>         | <span data-ttu-id="ec045-168">Nie</span><span class="sxs-lookup"><span data-stu-id="ec045-168">No</span></span>              | <span data-ttu-id="ec045-169">Data wygaśnięcia koszyka w formacie data/godzina.</span><span class="sxs-lookup"><span data-stu-id="ec045-169">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="ec045-170">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="ec045-170">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="ec045-171">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="ec045-171">lastModifiedUser</span></span>      | <span data-ttu-id="ec045-172">ciąg</span><span class="sxs-lookup"><span data-stu-id="ec045-172">string</span></span>           | <span data-ttu-id="ec045-173">Nie</span><span class="sxs-lookup"><span data-stu-id="ec045-173">No</span></span>              | <span data-ttu-id="ec045-174">Użytkownik, który ostatnio zaktualizował koszyk.</span><span class="sxs-lookup"><span data-stu-id="ec045-174">The user who last updated the cart.</span></span> <span data-ttu-id="ec045-175">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="ec045-175">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="ec045-176">lineItems</span><span class="sxs-lookup"><span data-stu-id="ec045-176">lineItems</span></span>             | <span data-ttu-id="ec045-177">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="ec045-177">Array of objects</span></span> | <span data-ttu-id="ec045-178">Tak</span><span class="sxs-lookup"><span data-stu-id="ec045-178">Yes</span></span>             | <span data-ttu-id="ec045-179">Tablica [zasobów CartLineItem.](cart-resources.md#cartlineitem)</span><span class="sxs-lookup"><span data-stu-id="ec045-179">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                             |

<span data-ttu-id="ec045-180">W tej tabeli [opisano właściwości CartLineItem](cart-resources.md#cartlineitem) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="ec045-180">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

| <span data-ttu-id="ec045-181">Właściwość</span><span class="sxs-lookup"><span data-stu-id="ec045-181">Property</span></span>             | <span data-ttu-id="ec045-182">Typ</span><span class="sxs-lookup"><span data-stu-id="ec045-182">Type</span></span>                             | <span data-ttu-id="ec045-183">Opis</span><span class="sxs-lookup"><span data-stu-id="ec045-183">Description</span></span>                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ec045-184">identyfikator</span><span class="sxs-lookup"><span data-stu-id="ec045-184">id</span></span>                   | <span data-ttu-id="ec045-185">ciąg</span><span class="sxs-lookup"><span data-stu-id="ec045-185">string</span></span>                           | <span data-ttu-id="ec045-186">Unikatowy identyfikator elementu wiersza koszyka.</span><span class="sxs-lookup"><span data-stu-id="ec045-186">A unique identifier for a cart line item.</span></span> <span data-ttu-id="ec045-187">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="ec045-187">Applied upon successful creation of cart.</span></span>                                                                   |
| <span data-ttu-id="ec045-188">catalogId</span><span class="sxs-lookup"><span data-stu-id="ec045-188">catalogId</span></span>            | <span data-ttu-id="ec045-189">ciąg</span><span class="sxs-lookup"><span data-stu-id="ec045-189">string</span></span>                           | <span data-ttu-id="ec045-190">Identyfikator elementu katalogu.</span><span class="sxs-lookup"><span data-stu-id="ec045-190">The catalog item identifier.</span></span>                                                                                                                          |
| <span data-ttu-id="ec045-191">Friendlyname</span><span class="sxs-lookup"><span data-stu-id="ec045-191">friendlyName</span></span>         | <span data-ttu-id="ec045-192">ciąg</span><span class="sxs-lookup"><span data-stu-id="ec045-192">string</span></span>                           | <span data-ttu-id="ec045-193">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="ec045-193">Optional.</span></span> <span data-ttu-id="ec045-194">Przyjazna nazwa elementu zdefiniowanego przez partnera w celu uujednoznania.</span><span class="sxs-lookup"><span data-stu-id="ec045-194">The friendly name for the item defined by the partner to help disambiguate.</span></span>                                                                 |
| <span data-ttu-id="ec045-195">quantity</span><span class="sxs-lookup"><span data-stu-id="ec045-195">quantity</span></span>             | <span data-ttu-id="ec045-196">int</span><span class="sxs-lookup"><span data-stu-id="ec045-196">int</span></span>                              | <span data-ttu-id="ec045-197">Liczba licencji lub wystąpień.</span><span class="sxs-lookup"><span data-stu-id="ec045-197">The number of licenses or instances.</span></span>                                                                                                                  |
| <span data-ttu-id="ec045-198">currencyCode</span><span class="sxs-lookup"><span data-stu-id="ec045-198">currencyCode</span></span>         | <span data-ttu-id="ec045-199">ciąg</span><span class="sxs-lookup"><span data-stu-id="ec045-199">string</span></span>                           | <span data-ttu-id="ec045-200">Kod waluty.</span><span class="sxs-lookup"><span data-stu-id="ec045-200">The currency code.</span></span>                                                                                                                                    |
| <span data-ttu-id="ec045-201">billingCycle</span><span class="sxs-lookup"><span data-stu-id="ec045-201">billingCycle</span></span>         | <span data-ttu-id="ec045-202">Obiekt</span><span class="sxs-lookup"><span data-stu-id="ec045-202">Object</span></span>                           | <span data-ttu-id="ec045-203">Typ cyklu rozliczeniowego ustawiony dla bieżącego okresu.</span><span class="sxs-lookup"><span data-stu-id="ec045-203">The type of billing cycle set for the current period.</span></span>                                                                                                 |
| <span data-ttu-id="ec045-204">uczestnicy</span><span class="sxs-lookup"><span data-stu-id="ec045-204">participants</span></span>         | <span data-ttu-id="ec045-205">Lista par ciągów obiektów</span><span class="sxs-lookup"><span data-stu-id="ec045-205">List of Object String pairs</span></span>      | <span data-ttu-id="ec045-206">Kolekcja identyfikatorów PartnerId w rekordzie (identyfikator MPN) podczas zakupu.</span><span class="sxs-lookup"><span data-stu-id="ec045-206">A collection of PartnerId on Record (MPN ID) on the purchase.</span></span>                                                                                          |
| <span data-ttu-id="ec045-207">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="ec045-207">provisioningContext</span></span>  | <span data-ttu-id="ec045-208">Słownik<ciąg, ciąg></span><span class="sxs-lookup"><span data-stu-id="ec045-208">Dictionary<string, string></span></span>       | <span data-ttu-id="ec045-209">Kontekst używany do aprowizowania oferty.</span><span class="sxs-lookup"><span data-stu-id="ec045-209">A context used for provisioning of offer.</span></span>                                                                                                             |
| <span data-ttu-id="ec045-210">orderGroup</span><span class="sxs-lookup"><span data-stu-id="ec045-210">orderGroup</span></span>           | <span data-ttu-id="ec045-211">ciąg</span><span class="sxs-lookup"><span data-stu-id="ec045-211">string</span></span>                           | <span data-ttu-id="ec045-212">Grupa wskazująca, które elementy można ze sobą umieścić.</span><span class="sxs-lookup"><span data-stu-id="ec045-212">A group to indicate which items can be placed together.</span></span>                                                                                               |
| <span data-ttu-id="ec045-213">addonItems</span><span class="sxs-lookup"><span data-stu-id="ec045-213">addonItems</span></span>           | <span data-ttu-id="ec045-214">Lista obiektów **CartLineItem**</span><span class="sxs-lookup"><span data-stu-id="ec045-214">List of **CartLineItem** objects</span></span> | <span data-ttu-id="ec045-215">Kolekcja elementów wiersza koszyka dla dodatków, które zostaną zakupione w ramach subskrypcji podstawowej, która wynika z zakupu elementu wiersza koszyka nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="ec045-215">A collection of cart line items for add-ons that will be purchased towards the base subscription that results from the parent cart line item's purchase.</span></span> |
| <span data-ttu-id="ec045-216">error</span><span class="sxs-lookup"><span data-stu-id="ec045-216">error</span></span>                | <span data-ttu-id="ec045-217">Obiekt</span><span class="sxs-lookup"><span data-stu-id="ec045-217">Object</span></span>                           | <span data-ttu-id="ec045-218">Zastosowane po utworzeniu koszyka, jeśli wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="ec045-218">Applied after cart is created if there is an error.</span></span>                                                                                                    |

### <a name="request-example-new-base-subscription"></a><span data-ttu-id="ec045-219">Przykład żądania (nowa subskrypcja podstawowa)</span><span class="sxs-lookup"><span data-stu-id="ec045-219">Request example (new base subscription)</span></span>

<span data-ttu-id="ec045-220">W poniższym przykładzie rest pokazano, jak utworzyć koszyk z elementami dodatków dla nowej subskrypcji podstawowej.</span><span class="sxs-lookup"><span data-stu-id="ec045-220">The following REST example shows how to create a cart with add-on items for a new base subscription.</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "FriendlyName":"Myofferpurchase",
            "Quantity":3,
            "BillingCycle":"monthly",
            "AddonItems": [
                {
                    "Id":1,
                    "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "Quantity":2,
                    "BillingCycle":"monthly"
                },
                {
                    "Id":2,
                    "CatalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "Quantity":3,
                    "BillingCycle":"monthly"
                }
            ]
        }
    ]
}
```

#### <a name="request-example-existing-base-subscription"></a><span data-ttu-id="ec045-221">Przykład żądania (istniejąca subskrypcja podstawowa)</span><span class="sxs-lookup"><span data-stu-id="ec045-221">Request example (existing base subscription)</span></span>

<span data-ttu-id="ec045-222">W poniższym przykładzie rest pokazano, jak dołączać dodatki do istniejącej subskrypcji podstawowej.</span><span class="sxs-lookup"><span data-stu-id="ec045-222">The following REST example shows how to append add-ons to an existing base subscription.</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "Quantity":1,
            "BillingCycle":"annual",
            "ProvisioningContext":{"ParentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"}
        }
    ]
}
```

## <a name="rest-response"></a><span data-ttu-id="ec045-223">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="ec045-223">REST response</span></span>

<span data-ttu-id="ec045-224">W przypadku powodzenia ta metoda zwraca wypełniony zasób [koszyka](cart-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ec045-224">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="ec045-225">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ec045-225">Response success and error codes</span></span>

<span data-ttu-id="ec045-226">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="ec045-226">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ec045-227">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="ec045-227">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ec045-228">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ec045-228">For the full list, see [Error Codes](error-codes.md).</span></span>

#### <a name="response-example-new-base-subscription"></a><span data-ttu-id="ec045-229">Przykład odpowiedzi (nowa subskrypcja podstawowa)</span><span class="sxs-lookup"><span data-stu-id="ec045-229">Response example (new base subscription)</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 958
Content-Type: application/json
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:29:05 GMT

{
    "id":"dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
    "creationTimestamp":"2018-11-01T22:29:03.6900182Z",
    "lastModifiedTimestamp":"2018-11-01T22:29:03.6900182Z",
    "expirationTimestamp":"2018-11-01T22:44:05.0025799Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "friendlyName":"Myofferpurchase",
            "quantity":3,
            "currencyCode":"USD",
            "billingCycle":"monthly",
            "orderGroup":"OMS-0",
            "addonItems": [
                {
                    "id":1,
                    "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "quantity":2,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                },
                {
                    "id":2,
                    "catalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "quantity":3,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                }
            ]
        }
],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```

#### <a name="response-example-existing-base-subscription"></a><span data-ttu-id="ec045-230">Przykład odpowiedzi (istniejąca subskrypcja podstawowa)</span><span class="sxs-lookup"><span data-stu-id="ec045-230">Response example (existing base subscription)</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 707
Content-Type: application/json
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:46:18 GMT

{
    "id":"4d927e27-93d1-448b-abe5-819b66ecca22",
    "creationTimestamp":"2018-11-01T22:46:16.2996364Z",
    "lastModifiedTimestamp":"2018-11-01T22:46:16.2996364Z",
    "expirationTimestamp":"2018-11-01T23:01:18.7543264Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "quantity":1,
            "currencyCode":"USD",
            "billingCycle":"annual",
            "provisioningContext": {
                "parentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"
            },
            "orderGroup":"OMS-0"
        }
    ],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/4d927e27-93d1-448b-abe5-819b66ecca22",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```
