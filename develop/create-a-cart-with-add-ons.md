---
title: Tworzenie koszyka z dodatkami
description: Dowiedz się, jak za pomocą interfejsów API Centrum partnerskiego dodać zamówienie klienta z dodatkami za pomocą koszyka. Artykuł udostępnia wymagania wstępne i kroki tworzenia koszyka z dodatkami.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 81c41405a2f56eb4d1d3447d14b93e05d550cc70
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/07/2020
ms.locfileid: "97768629"
---
# <a name="create-a-cart-with-add-ons-to-a-customer-order"></a><span data-ttu-id="72f47-104">Tworzenie koszyka z dodatkami do zamówienia klienta</span><span class="sxs-lookup"><span data-stu-id="72f47-104">Create a cart with add-ons to a customer order</span></span>

<span data-ttu-id="72f47-105">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="72f47-105">**Applies to:**</span></span>

- <span data-ttu-id="72f47-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="72f47-106">Partner Center</span></span>

<span data-ttu-id="72f47-107">Dodatki można kupić w koszyku.</span><span class="sxs-lookup"><span data-stu-id="72f47-107">You can purchase add-ons through a cart.</span></span> <span data-ttu-id="72f47-108">Aby uzyskać więcej informacji o tym, co jest obecnie dostępne do sprzedawania, zobacz [oferty partnerów w programie Cloud Solution Provider](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="72f47-108">For more information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72f47-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="72f47-109">Prerequisites</span></span>

- <span data-ttu-id="72f47-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="72f47-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="72f47-111">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="72f47-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="72f47-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="72f47-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="72f47-113">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="72f47-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="72f47-114">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="72f47-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="72f47-115">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="72f47-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="72f47-116">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="72f47-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="72f47-117">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="72f47-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="72f47-118">C\#</span><span class="sxs-lookup"><span data-stu-id="72f47-118">C\#</span></span>

<span data-ttu-id="72f47-119">Koszyk umożliwia zakup oferty podstawowej i jej odpowiednich dodatków.</span><span class="sxs-lookup"><span data-stu-id="72f47-119">A cart enables the purchase of a base offer and its corresponding add-ons.</span></span> <span data-ttu-id="72f47-120">Wykonaj następujące kroki, aby utworzyć koszyk:</span><span class="sxs-lookup"><span data-stu-id="72f47-120">Follow these steps to create a cart:</span></span>

1. <span data-ttu-id="72f47-121">Utwórz wystąpienie obiektu [**koszyka**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) .</span><span class="sxs-lookup"><span data-stu-id="72f47-121">Instantiate a [**Cart**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) object.</span></span>

2. <span data-ttu-id="72f47-122">Utwórz listę obiektów [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) reprezentujących oferty podstawowe i przypisz listę do właściwości [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) koszyka.</span><span class="sxs-lookup"><span data-stu-id="72f47-122">Create a list of [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) objects which represent the base offer(s), and assign the list to the cart's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) property.</span></span>

3. <span data-ttu-id="72f47-123">W obszarze każdego elementu linii koszyka podstawowej oferty Wypełnij listę **AddOnItems** innymi obiektami **CartLineItem** , które każdy reprezentuje dodatek, który zostanie zakupiony w ramach tej oferty podstawowej.</span><span class="sxs-lookup"><span data-stu-id="72f47-123">Under each base offer's cart line item, populate the list of **AddOnItems** with other **CartLineItem** objects that each represent an add-on that will be purchased against that base offer.</span></span>

4. <span data-ttu-id="72f47-124">Uzyskaj interfejs do operacji koszyka przy użyciu [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) do wywołania metody [**ICustomerCollection. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta, a następnie pobierając interfejs z właściwości **koszyka** .</span><span class="sxs-lookup"><span data-stu-id="72f47-124">Obtain an interface to cart operations by using [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) to call the [**ICustomerCollection.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.</span></span>

5. <span data-ttu-id="72f47-125">Na koniec Wywołaj metodę [**Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) lub [**onasync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) , aby utworzyć koszyk.</span><span class="sxs-lookup"><span data-stu-id="72f47-125">Finally, call the [**Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) method to create the cart.</span></span>

### <a name="c-example"></a><span data-ttu-id="72f47-126">\#Przykład C</span><span class="sxs-lookup"><span data-stu-id="72f47-126">C\# example</span></span>

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

<span data-ttu-id="72f47-127">Wykonaj następujące kroki, aby utworzyć koszyk, który umożliwi zakup dodatków dla istniejących subskrypcji podstawowych:</span><span class="sxs-lookup"><span data-stu-id="72f47-127">Follow these steps to create a cart which will enable the purchase of add-on(s) against existing base subscription(s):</span></span>

1. <span data-ttu-id="72f47-128">Utwórz **koszyk** z nowym **CARTLINEITEM** zawierającym Identyfikator subskrypcji we właściwości **ProvisioningContext** z kluczem "ParentSubscriptionId".</span><span class="sxs-lookup"><span data-stu-id="72f47-128">Create a **Cart** with a new **CartLineItem** containing the subscription ID in the **ProvisioningContext** property with key "ParentSubscriptionId".</span></span>

2. <span data-ttu-id="72f47-129">Wywoływanie metody **Create** lub **onasync** .</span><span class="sxs-lookup"><span data-stu-id="72f47-129">Call the **Create** or **CreateAsync** method.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="72f47-130">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="72f47-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="72f47-131">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="72f47-131">Request syntax</span></span>

| <span data-ttu-id="72f47-132">Metoda</span><span class="sxs-lookup"><span data-stu-id="72f47-132">Method</span></span>   | <span data-ttu-id="72f47-133">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="72f47-133">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="72f47-134">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="72f47-134">**POST**</span></span> | <span data-ttu-id="72f47-135">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/Carts http/1.1</span><span class="sxs-lookup"><span data-stu-id="72f47-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span></span>                        |

#### <a name="uri-parameter"></a><span data-ttu-id="72f47-136">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="72f47-136">URI parameter</span></span>

<span data-ttu-id="72f47-137">Użyj następującego parametru ścieżki, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="72f47-137">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="72f47-138">Nazwa</span><span class="sxs-lookup"><span data-stu-id="72f47-138">Name</span></span>            | <span data-ttu-id="72f47-139">Typ</span><span class="sxs-lookup"><span data-stu-id="72f47-139">Type</span></span>     | <span data-ttu-id="72f47-140">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72f47-140">Required</span></span> | <span data-ttu-id="72f47-141">Opis</span><span class="sxs-lookup"><span data-stu-id="72f47-141">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="72f47-142">**Identyfikator klienta**</span><span class="sxs-lookup"><span data-stu-id="72f47-142">**customer-id**</span></span> | <span data-ttu-id="72f47-143">ciąg</span><span class="sxs-lookup"><span data-stu-id="72f47-143">string</span></span>   | <span data-ttu-id="72f47-144">Tak</span><span class="sxs-lookup"><span data-stu-id="72f47-144">Yes</span></span>      | <span data-ttu-id="72f47-145">Identyfikator GUID sformatowany przez klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="72f47-145">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="72f47-146">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="72f47-146">Request headers</span></span>

<span data-ttu-id="72f47-147">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="72f47-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="72f47-148">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="72f47-148">Request body</span></span>

<span data-ttu-id="72f47-149">W tej tabeli opisano właściwości [koszyka](cart-resources.md) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="72f47-149">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="72f47-150">Właściwość</span><span class="sxs-lookup"><span data-stu-id="72f47-150">Property</span></span>              | <span data-ttu-id="72f47-151">Typ</span><span class="sxs-lookup"><span data-stu-id="72f47-151">Type</span></span>             | <span data-ttu-id="72f47-152">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72f47-152">Required</span></span>        | <span data-ttu-id="72f47-153">Opis</span><span class="sxs-lookup"><span data-stu-id="72f47-153">Description</span></span> |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="72f47-154">identyfikator</span><span class="sxs-lookup"><span data-stu-id="72f47-154">id</span></span>                    | <span data-ttu-id="72f47-155">ciąg</span><span class="sxs-lookup"><span data-stu-id="72f47-155">string</span></span>           | <span data-ttu-id="72f47-156">Nie</span><span class="sxs-lookup"><span data-stu-id="72f47-156">No</span></span>              | <span data-ttu-id="72f47-157">Identyfikator koszyka, który jest dostarczany po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="72f47-157">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="72f47-158">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="72f47-158">creationTimeStamp</span></span>     | <span data-ttu-id="72f47-159">DateTime</span><span class="sxs-lookup"><span data-stu-id="72f47-159">DateTime</span></span>         | <span data-ttu-id="72f47-160">Nie</span><span class="sxs-lookup"><span data-stu-id="72f47-160">No</span></span>              | <span data-ttu-id="72f47-161">Data i godzina utworzenia koszyka.</span><span class="sxs-lookup"><span data-stu-id="72f47-161">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="72f47-162">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="72f47-162">Applied upon successful creation of the cart.</span></span>         |
| <span data-ttu-id="72f47-163">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="72f47-163">lastModifiedTimeStamp</span></span> | <span data-ttu-id="72f47-164">DateTime</span><span class="sxs-lookup"><span data-stu-id="72f47-164">DateTime</span></span>         | <span data-ttu-id="72f47-165">Nie</span><span class="sxs-lookup"><span data-stu-id="72f47-165">No</span></span>              | <span data-ttu-id="72f47-166">Data ostatniej aktualizacji koszyka w formacie daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="72f47-166">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="72f47-167">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="72f47-167">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="72f47-168">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="72f47-168">expirationTimeStamp</span></span>   | <span data-ttu-id="72f47-169">DateTime</span><span class="sxs-lookup"><span data-stu-id="72f47-169">DateTime</span></span>         | <span data-ttu-id="72f47-170">Nie</span><span class="sxs-lookup"><span data-stu-id="72f47-170">No</span></span>              | <span data-ttu-id="72f47-171">Data wygaśnięcia koszyka w formacie daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="72f47-171">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="72f47-172">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="72f47-172">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="72f47-173">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="72f47-173">lastModifiedUser</span></span>      | <span data-ttu-id="72f47-174">ciąg</span><span class="sxs-lookup"><span data-stu-id="72f47-174">string</span></span>           | <span data-ttu-id="72f47-175">Nie</span><span class="sxs-lookup"><span data-stu-id="72f47-175">No</span></span>              | <span data-ttu-id="72f47-176">Użytkownik, który ostatnio zaktualizował koszyk.</span><span class="sxs-lookup"><span data-stu-id="72f47-176">The user who last updated the cart.</span></span> <span data-ttu-id="72f47-177">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="72f47-177">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="72f47-178">lineItems</span><span class="sxs-lookup"><span data-stu-id="72f47-178">lineItems</span></span>             | <span data-ttu-id="72f47-179">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="72f47-179">Array of objects</span></span> | <span data-ttu-id="72f47-180">Tak</span><span class="sxs-lookup"><span data-stu-id="72f47-180">Yes</span></span>             | <span data-ttu-id="72f47-181">Tablica zasobów [CartLineItem](cart-resources.md#cartlineitem) .</span><span class="sxs-lookup"><span data-stu-id="72f47-181">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                             |

<span data-ttu-id="72f47-182">W tej tabeli opisano właściwości [CartLineItem](cart-resources.md#cartlineitem) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="72f47-182">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

| <span data-ttu-id="72f47-183">Właściwość</span><span class="sxs-lookup"><span data-stu-id="72f47-183">Property</span></span>             | <span data-ttu-id="72f47-184">Typ</span><span class="sxs-lookup"><span data-stu-id="72f47-184">Type</span></span>                             | <span data-ttu-id="72f47-185">Opis</span><span class="sxs-lookup"><span data-stu-id="72f47-185">Description</span></span>                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="72f47-186">identyfikator</span><span class="sxs-lookup"><span data-stu-id="72f47-186">id</span></span>                   | <span data-ttu-id="72f47-187">ciąg</span><span class="sxs-lookup"><span data-stu-id="72f47-187">string</span></span>                           | <span data-ttu-id="72f47-188">Unikatowy identyfikator dla elementu w wierszu koszyka.</span><span class="sxs-lookup"><span data-stu-id="72f47-188">A unique identifier for a cart line item.</span></span> <span data-ttu-id="72f47-189">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="72f47-189">Applied upon successful creation of cart.</span></span>                                                                   |
| <span data-ttu-id="72f47-190">catalogId</span><span class="sxs-lookup"><span data-stu-id="72f47-190">catalogId</span></span>            | <span data-ttu-id="72f47-191">ciąg</span><span class="sxs-lookup"><span data-stu-id="72f47-191">string</span></span>                           | <span data-ttu-id="72f47-192">Identyfikator elementu katalogu.</span><span class="sxs-lookup"><span data-stu-id="72f47-192">The catalog item identifier.</span></span>                                                                                                                          |
| <span data-ttu-id="72f47-193">friendlyName</span><span class="sxs-lookup"><span data-stu-id="72f47-193">friendlyName</span></span>         | <span data-ttu-id="72f47-194">ciąg</span><span class="sxs-lookup"><span data-stu-id="72f47-194">string</span></span>                           | <span data-ttu-id="72f47-195">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="72f47-195">Optional.</span></span> <span data-ttu-id="72f47-196">Przyjazna nazwa dla elementu zdefiniowanego przez partnera, która pomaga w odróżnieniu od siebie.</span><span class="sxs-lookup"><span data-stu-id="72f47-196">The friendly name for the item defined by the partner to help disambiguate.</span></span>                                                                 |
| <span data-ttu-id="72f47-197">quantity</span><span class="sxs-lookup"><span data-stu-id="72f47-197">quantity</span></span>             | <span data-ttu-id="72f47-198">int</span><span class="sxs-lookup"><span data-stu-id="72f47-198">int</span></span>                              | <span data-ttu-id="72f47-199">Liczba licencji lub wystąpień.</span><span class="sxs-lookup"><span data-stu-id="72f47-199">The number of licenses or instances.</span></span>                                                                                                                  |
| <span data-ttu-id="72f47-200">currencyCode</span><span class="sxs-lookup"><span data-stu-id="72f47-200">currencyCode</span></span>         | <span data-ttu-id="72f47-201">ciąg</span><span class="sxs-lookup"><span data-stu-id="72f47-201">string</span></span>                           | <span data-ttu-id="72f47-202">Kod waluty.</span><span class="sxs-lookup"><span data-stu-id="72f47-202">The currency code.</span></span>                                                                                                                                    |
| <span data-ttu-id="72f47-203">billingCycle</span><span class="sxs-lookup"><span data-stu-id="72f47-203">billingCycle</span></span>         | <span data-ttu-id="72f47-204">Obiekt</span><span class="sxs-lookup"><span data-stu-id="72f47-204">Object</span></span>                           | <span data-ttu-id="72f47-205">Typ cyklu rozliczeniowego ustawiony dla bieżącego okresu.</span><span class="sxs-lookup"><span data-stu-id="72f47-205">The type of billing cycle set for the current period.</span></span>                                                                                                 |
| <span data-ttu-id="72f47-206">uczestnicy</span><span class="sxs-lookup"><span data-stu-id="72f47-206">participants</span></span>         | <span data-ttu-id="72f47-207">Lista par ciągów obiektów</span><span class="sxs-lookup"><span data-stu-id="72f47-207">List of Object String pairs</span></span>      | <span data-ttu-id="72f47-208">Kolekcja PartnerId on Record (MPNID) na zakupie.</span><span class="sxs-lookup"><span data-stu-id="72f47-208">A collection of PartnerId on Record (MPNID) on the purchase.</span></span>                                                                                          |
| <span data-ttu-id="72f47-209">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="72f47-209">provisioningContext</span></span>  | <span data-ttu-id="72f47-210">Ciąg<słownika, ciąg></span><span class="sxs-lookup"><span data-stu-id="72f47-210">Dictionary<string, string></span></span>       | <span data-ttu-id="72f47-211">Kontekst używany do aprowizacji oferty.</span><span class="sxs-lookup"><span data-stu-id="72f47-211">A context used for provisioning of offer.</span></span>                                                                                                             |
| <span data-ttu-id="72f47-212">kolejność</span><span class="sxs-lookup"><span data-stu-id="72f47-212">orderGroup</span></span>           | <span data-ttu-id="72f47-213">ciąg</span><span class="sxs-lookup"><span data-stu-id="72f47-213">string</span></span>                           | <span data-ttu-id="72f47-214">Grupa wskazująca, które elementy mogą być umieszczone razem.</span><span class="sxs-lookup"><span data-stu-id="72f47-214">A group to indicate which items can be placed together.</span></span>                                                                                               |
| <span data-ttu-id="72f47-215">addonItems</span><span class="sxs-lookup"><span data-stu-id="72f47-215">addonItems</span></span>           | <span data-ttu-id="72f47-216">Lista obiektów **CartLineItem**</span><span class="sxs-lookup"><span data-stu-id="72f47-216">List of **CartLineItem** objects</span></span> | <span data-ttu-id="72f47-217">Kolekcja elementów wiersza koszyka dla dodatków, które zostaną zakupione w ramach subskrypcji podstawowej, która wynika z zakupu elementu wiersza koszyka nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="72f47-217">A collection of cart line items for add-ons that will be purchased towards the base subscription that results from the parent cart line item's purchase.</span></span> |
| <span data-ttu-id="72f47-218">error</span><span class="sxs-lookup"><span data-stu-id="72f47-218">error</span></span>                | <span data-ttu-id="72f47-219">Obiekt</span><span class="sxs-lookup"><span data-stu-id="72f47-219">Object</span></span>                           | <span data-ttu-id="72f47-220">Zastosowano po utworzeniu koszyka w przypadku błędu.</span><span class="sxs-lookup"><span data-stu-id="72f47-220">Applied after cart is created in case of an error.</span></span>                                                                                                    |

### <a name="request-example-new-base-subscription"></a><span data-ttu-id="72f47-221">Przykład żądania (Nowa subskrypcja podstawowa)</span><span class="sxs-lookup"><span data-stu-id="72f47-221">Request example (new base subscription)</span></span>

<span data-ttu-id="72f47-222">Poniższy przykład REST pokazuje, jak utworzyć koszyk z elementami dodatków dla nowej subskrypcji podstawowej.</span><span class="sxs-lookup"><span data-stu-id="72f47-222">The following REST example shows how to create a cart with add-on items for a new base subscription.</span></span>

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

#### <a name="request-example-existing-base-subscription"></a><span data-ttu-id="72f47-223">Przykład żądania (istniejąca subskrypcja podstawowa)</span><span class="sxs-lookup"><span data-stu-id="72f47-223">Request example (existing base subscription)</span></span>

<span data-ttu-id="72f47-224">Poniższy przykład REST pokazuje, jak dołączyć Dodatki do istniejącej subskrypcji podstawowej.</span><span class="sxs-lookup"><span data-stu-id="72f47-224">The following REST example show how to append add-ons to an existing base subscription.</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="72f47-225">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="72f47-225">REST response</span></span>

<span data-ttu-id="72f47-226">Jeśli to się powiedzie, ta metoda zwraca zasób [koszyka](cart-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="72f47-226">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="72f47-227">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="72f47-227">Response success and error codes</span></span>

<span data-ttu-id="72f47-228">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="72f47-228">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="72f47-229">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="72f47-229">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="72f47-230">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="72f47-230">For the full list, see [Error Codes](error-codes.md).</span></span>

#### <a name="response-example-new-base-subscription"></a><span data-ttu-id="72f47-231">Przykład odpowiedzi (Nowa subskrypcja podstawowa)</span><span class="sxs-lookup"><span data-stu-id="72f47-231">Response example (new base subscription)</span></span>

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

#### <a name="response-example-existing-base-subscription"></a><span data-ttu-id="72f47-232">Przykład odpowiedzi (istniejąca subskrypcja podstawowa)</span><span class="sxs-lookup"><span data-stu-id="72f47-232">Response example (existing base subscription)</span></span>

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
