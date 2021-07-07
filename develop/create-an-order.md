---
title: Tworzenie zamówienia klienta
description: Dowiedz się, jak Partner Center api do tworzenia zamówienia dla klienta. Artykuł zawiera wymagania wstępne, kroki i przykłady.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c3a86a99f43bdeec5e4c560ab59e1924b76c0636
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973552"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a><span data-ttu-id="89470-104">Tworzenie zamówienia dla klienta przy użyciu interfejsów PARTNER CENTER API</span><span class="sxs-lookup"><span data-stu-id="89470-104">Create an order for a customer using Partner Center APIs</span></span>

<span data-ttu-id="89470-105">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="89470-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="89470-106">Tworzenie zamówienia **dla produktów wystąpienia zarezerwowanego maszyny wirtualnej platformy Azure** ma zastosowanie tylko *do:*</span><span class="sxs-lookup"><span data-stu-id="89470-106">Creating an **order for Azure reserved VM instance products** applies *only* to:</span></span>

- <span data-ttu-id="89470-107">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="89470-107">Partner Center</span></span>

<span data-ttu-id="89470-108">Aby uzyskać informacje o tym, co jest obecnie dostępne do sprzedaży, zobacz [Oferty partnerów w Dostawca rozwiązań w chmurze programie](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="89470-108">For information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89470-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="89470-109">Prerequisites</span></span>

- <span data-ttu-id="89470-110">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="89470-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="89470-111">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89470-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="89470-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="89470-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="89470-113">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="89470-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="89470-114">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="89470-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="89470-115">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="89470-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="89470-116">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="89470-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="89470-117">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="89470-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="89470-118">Identyfikator oferty.</span><span class="sxs-lookup"><span data-stu-id="89470-118">An offer identifier.</span></span>

## <a name="c"></a><span data-ttu-id="89470-119">C\#</span><span class="sxs-lookup"><span data-stu-id="89470-119">C\#</span></span>

<span data-ttu-id="89470-120">Aby utworzyć zamówienie dla klienta:</span><span class="sxs-lookup"><span data-stu-id="89470-120">To create an order for a customer:</span></span>

1. <span data-ttu-id="89470-121">Za pomocą wystąpienia obiektu [**Order**](order-resources.md) ustaw właściwość **ReferenceCustomerID** na identyfikator klienta, aby zarejestrować klienta.</span><span class="sxs-lookup"><span data-stu-id="89470-121">Instantiate an [**Order**](order-resources.md) object and set the **ReferenceCustomerID** property to the customer ID to record the customer.</span></span>

2. <span data-ttu-id="89470-122">Utwórz listę obiektów [**OrderLineItem**](order-resources.md#orderlineitem) i przypisz listę do właściwości **LineItems** zamówienia.</span><span class="sxs-lookup"><span data-stu-id="89470-122">Create a list of [**OrderLineItem**](order-resources.md#orderlineitem) objects, and assign the list to the order's **LineItems** property.</span></span> <span data-ttu-id="89470-123">Każdy element wiersza zamówienia zawiera informacje o zakupie dla jednej oferty.</span><span class="sxs-lookup"><span data-stu-id="89470-123">Each order line item contains the purchase information for one offer.</span></span> <span data-ttu-id="89470-124">Musisz mieć co najmniej jeden wiersz zamówienia.</span><span class="sxs-lookup"><span data-stu-id="89470-124">You must have at least one order line item.</span></span>

3. <span data-ttu-id="89470-125">Uzyskiwanie interfejsu do zamawiania operacji.</span><span class="sxs-lookup"><span data-stu-id="89470-125">Obtain an interface to order operations.</span></span> <span data-ttu-id="89470-126">Najpierw wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="89470-126">First, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="89470-127">Następnie pobierz interfejs z właściwości [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) (Zamówienia).</span><span class="sxs-lookup"><span data-stu-id="89470-127">Next, retrieve the interface from the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.</span></span>

4. <span data-ttu-id="89470-128">Wywołaj [**metodę Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) lub [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) i przekaż obiekt [**Order.**](order-resources.md)</span><span class="sxs-lookup"><span data-stu-id="89470-128">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method and pass in the [**Order**](order-resources.md) object.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string offerId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "new offer purchase",
            Quantity = 1,
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", "5198C069-3DAA-403A-8660-5BE11BFD12EE" },
                { "scope", "shared" },
                { "duration", "3Years" }
            }
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

<span data-ttu-id="89470-129">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="89470-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="89470-130">**Project:** zestaw SDK Centrum partnerskiego **Samples, klasa:** CreateOrder.cs</span><span class="sxs-lookup"><span data-stu-id="89470-130">**Project**: Partner Center SDK Samples **Class**: CreateOrder.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="89470-131">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="89470-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="89470-132">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="89470-132">Request syntax</span></span>

| <span data-ttu-id="89470-133">Metoda</span><span class="sxs-lookup"><span data-stu-id="89470-133">Method</span></span>   | <span data-ttu-id="89470-134">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="89470-134">Request URI</span></span>                                                                            |
|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="89470-135">**Post**</span><span class="sxs-lookup"><span data-stu-id="89470-135">**POST**</span></span> | <span data-ttu-id="89470-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="89470-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="89470-137">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="89470-137">URI parameters</span></span>

<span data-ttu-id="89470-138">Użyj następującego parametru ścieżki, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="89470-138">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="89470-139">Nazwa</span><span class="sxs-lookup"><span data-stu-id="89470-139">Name</span></span>        | <span data-ttu-id="89470-140">Typ</span><span class="sxs-lookup"><span data-stu-id="89470-140">Type</span></span>   | <span data-ttu-id="89470-141">Wymagane</span><span class="sxs-lookup"><span data-stu-id="89470-141">Required</span></span> | <span data-ttu-id="89470-142">Opis</span><span class="sxs-lookup"><span data-stu-id="89470-142">Description</span></span>                                                |
|-------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="89470-143">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="89470-143">customer-id</span></span> | <span data-ttu-id="89470-144">ciąg</span><span class="sxs-lookup"><span data-stu-id="89470-144">string</span></span> | <span data-ttu-id="89470-145">Tak</span><span class="sxs-lookup"><span data-stu-id="89470-145">Yes</span></span>      | <span data-ttu-id="89470-146">Identyfikator GUID sformatowany jako identyfikator klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="89470-146">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="89470-147">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="89470-147">Request headers</span></span>

<span data-ttu-id="89470-148">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="89470-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="89470-149">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="89470-149">Request body</span></span>

#### <a name="order"></a><span data-ttu-id="89470-150">Zamówienie</span><span class="sxs-lookup"><span data-stu-id="89470-150">Order</span></span>

<span data-ttu-id="89470-151">W tej tabeli [opisano właściwości](order-resources.md) Order w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="89470-151">This table describes the [Order](order-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="89470-152">Właściwość</span><span class="sxs-lookup"><span data-stu-id="89470-152">Property</span></span>             | <span data-ttu-id="89470-153">Typ</span><span class="sxs-lookup"><span data-stu-id="89470-153">Type</span></span>                        | <span data-ttu-id="89470-154">Wymagane</span><span class="sxs-lookup"><span data-stu-id="89470-154">Required</span></span>                        | <span data-ttu-id="89470-155">Opis</span><span class="sxs-lookup"><span data-stu-id="89470-155">Description</span></span>                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| <span data-ttu-id="89470-156">identyfikator</span><span class="sxs-lookup"><span data-stu-id="89470-156">id</span></span>                   | <span data-ttu-id="89470-157">ciąg</span><span class="sxs-lookup"><span data-stu-id="89470-157">string</span></span>                      | <span data-ttu-id="89470-158">Nie</span><span class="sxs-lookup"><span data-stu-id="89470-158">No</span></span>                              | <span data-ttu-id="89470-159">Identyfikator zamówienia podany po pomyślnym utworzeniu zamówienia.</span><span class="sxs-lookup"><span data-stu-id="89470-159">An order identifier that is supplied upon successful creation of the order.</span></span>   |
| <span data-ttu-id="89470-160">referenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="89470-160">referenceCustomerId</span></span>  | <span data-ttu-id="89470-161">ciąg</span><span class="sxs-lookup"><span data-stu-id="89470-161">string</span></span>                      | <span data-ttu-id="89470-162">Nie</span><span class="sxs-lookup"><span data-stu-id="89470-162">No</span></span>                              | <span data-ttu-id="89470-163">Identyfikator klienta.</span><span class="sxs-lookup"><span data-stu-id="89470-163">The customer identifier.</span></span> |
| <span data-ttu-id="89470-164">billingCycle</span><span class="sxs-lookup"><span data-stu-id="89470-164">billingCycle</span></span>         | <span data-ttu-id="89470-165">ciąg</span><span class="sxs-lookup"><span data-stu-id="89470-165">string</span></span>                      | <span data-ttu-id="89470-166">Nie</span><span class="sxs-lookup"><span data-stu-id="89470-166">No</span></span>                              | <span data-ttu-id="89470-167">Wskazuje częstotliwość, za pomocą której partner jest rozliczany za to zamówienie.</span><span class="sxs-lookup"><span data-stu-id="89470-167">Indicates the frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="89470-168">Obsługiwane wartości to nazwy członków w [typie BillingCycleType](product-resources.md#billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="89470-168">Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype).</span></span> <span data-ttu-id="89470-169">Wartość domyślna to "Monthly" lub "OneTime" podczas tworzenia zamówienia.</span><span class="sxs-lookup"><span data-stu-id="89470-169">The default is "Monthly" or "OneTime" at order creation.</span></span> <span data-ttu-id="89470-170">To pole jest stosowane po pomyślnym utworzeniu zamówienia.</span><span class="sxs-lookup"><span data-stu-id="89470-170">This field is applied upon successful creation of the order.</span></span> |
| <span data-ttu-id="89470-171">lineItems</span><span class="sxs-lookup"><span data-stu-id="89470-171">lineItems</span></span>            | <span data-ttu-id="89470-172">tablica [zasobów OrderLineItem](order-resources.md#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="89470-172">array of [OrderLineItem](order-resources.md#orderlineitem) resources</span></span> | <span data-ttu-id="89470-173">Tak</span><span class="sxs-lookup"><span data-stu-id="89470-173">Yes</span></span>      | <span data-ttu-id="89470-174">Lista pozycji ofert, które klient kupuje, łącznie z ilością.</span><span class="sxs-lookup"><span data-stu-id="89470-174">An itemized list of the offers the customer is purchasing including the quantity.</span></span>        |
| <span data-ttu-id="89470-175">currencyCode</span><span class="sxs-lookup"><span data-stu-id="89470-175">currencyCode</span></span>         | <span data-ttu-id="89470-176">ciąg</span><span class="sxs-lookup"><span data-stu-id="89470-176">string</span></span>                      | <span data-ttu-id="89470-177">Nie</span><span class="sxs-lookup"><span data-stu-id="89470-177">No</span></span>                              | <span data-ttu-id="89470-178">Tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="89470-178">Read-only.</span></span> <span data-ttu-id="89470-179">Waluta używana podczas składania zamówienia.</span><span class="sxs-lookup"><span data-stu-id="89470-179">The currency used when placing the order.</span></span> <span data-ttu-id="89470-180">Stosowane po pomyślnym utworzeniu zamówienia.</span><span class="sxs-lookup"><span data-stu-id="89470-180">Applied upon successful creation of the order.</span></span>           |
| <span data-ttu-id="89470-181">Creationdate</span><span class="sxs-lookup"><span data-stu-id="89470-181">creationDate</span></span>         | <span data-ttu-id="89470-182">datetime</span><span class="sxs-lookup"><span data-stu-id="89470-182">datetime</span></span>                    | <span data-ttu-id="89470-183">Nie</span><span class="sxs-lookup"><span data-stu-id="89470-183">No</span></span>                              | <span data-ttu-id="89470-184">Tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="89470-184">Read-only.</span></span> <span data-ttu-id="89470-185">Data utworzenia zamówienia w formacie data/godzina.</span><span class="sxs-lookup"><span data-stu-id="89470-185">The date the order was created, in date-time format.</span></span> <span data-ttu-id="89470-186">Stosowane po pomyślnym utworzeniu zamówienia.</span><span class="sxs-lookup"><span data-stu-id="89470-186">Applied upon successful creation of the order.</span></span>                                   |
| <span data-ttu-id="89470-187">status</span><span class="sxs-lookup"><span data-stu-id="89470-187">status</span></span>               | <span data-ttu-id="89470-188">ciąg</span><span class="sxs-lookup"><span data-stu-id="89470-188">string</span></span>                      | <span data-ttu-id="89470-189">Nie</span><span class="sxs-lookup"><span data-stu-id="89470-189">No</span></span>                              | <span data-ttu-id="89470-190">Tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="89470-190">Read-only.</span></span> <span data-ttu-id="89470-191">Stan zamówienia.</span><span class="sxs-lookup"><span data-stu-id="89470-191">The status of the order.</span></span>  <span data-ttu-id="89470-192">Obsługiwane wartości to nazwy członków w [orderstatus](order-resources.md#orderstatus).</span><span class="sxs-lookup"><span data-stu-id="89470-192">Supported values are the member names found in [OrderStatus](order-resources.md#orderstatus).</span></span>        |
| <span data-ttu-id="89470-193">Linki</span><span class="sxs-lookup"><span data-stu-id="89470-193">links</span></span>                | [<span data-ttu-id="89470-194">OrderLinks</span><span class="sxs-lookup"><span data-stu-id="89470-194">OrderLinks</span></span>](utility-resources.md#resourcelinks)              | <span data-ttu-id="89470-195">Nie</span><span class="sxs-lookup"><span data-stu-id="89470-195">No</span></span>                              | <span data-ttu-id="89470-196">Zasób łączy się z zamówieniem.</span><span class="sxs-lookup"><span data-stu-id="89470-196">The resource links corresponding to the Order.</span></span> |
| <span data-ttu-id="89470-197">atrybuty</span><span class="sxs-lookup"><span data-stu-id="89470-197">attributes</span></span>           | [<span data-ttu-id="89470-198">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="89470-198">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="89470-199">Nie</span><span class="sxs-lookup"><span data-stu-id="89470-199">No</span></span>                              | <span data-ttu-id="89470-200">Atrybuty metadanych odpowiadające kolejności.</span><span class="sxs-lookup"><span data-stu-id="89470-200">The metadata attributes corresponding to the Order.</span></span> |

#### <a name="orderlineitem"></a><span data-ttu-id="89470-201">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="89470-201">OrderLineItem</span></span>

<span data-ttu-id="89470-202">W tej tabeli [opisano właściwości OrderLineItem](order-resources.md#orderlineitem) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="89470-202">This table describes the [OrderLineItem](order-resources.md#orderlineitem) properties in the request body.</span></span>

>[!NOTE]
><span data-ttu-id="89470-203">Rekord partnerIdOnRecord powinien być podany tylko wtedy, gdy dostawca pośredni złozy zamówienie w imieniu odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="89470-203">The partnerIdOnRecord should only be provided when an indirect provider places an order on behalf of an indirect reseller.</span></span> <span data-ttu-id="89470-204">Jest on używany do przechowywania Microsoft Partner Network tylko odsprzedawcy pośredniego (nigdy identyfikatora dostawcy pośredniego).</span><span class="sxs-lookup"><span data-stu-id="89470-204">It's used to store the Microsoft Partner Network ID of the indirect reseller only (never the ID of the indirect provider).</span></span>

| <span data-ttu-id="89470-205">Nazwa</span><span class="sxs-lookup"><span data-stu-id="89470-205">Name</span></span>                 | <span data-ttu-id="89470-206">Typ</span><span class="sxs-lookup"><span data-stu-id="89470-206">Type</span></span>   | <span data-ttu-id="89470-207">Wymagane</span><span class="sxs-lookup"><span data-stu-id="89470-207">Required</span></span> | <span data-ttu-id="89470-208">Opis</span><span class="sxs-lookup"><span data-stu-id="89470-208">Description</span></span>                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="89470-209">lineItemNumber</span><span class="sxs-lookup"><span data-stu-id="89470-209">lineItemNumber</span></span>       | <span data-ttu-id="89470-210">int</span><span class="sxs-lookup"><span data-stu-id="89470-210">int</span></span>    | <span data-ttu-id="89470-211">Tak</span><span class="sxs-lookup"><span data-stu-id="89470-211">Yes</span></span>      | <span data-ttu-id="89470-212">Każdy element wiersza w kolekcji otrzymuje unikatowy numer wiersza, licząc od 0 do count-1.</span><span class="sxs-lookup"><span data-stu-id="89470-212">Each line item in the collection gets a unique line number, counting up from 0 to count-1.</span></span>                                                                                                                                                 |
| <span data-ttu-id="89470-213">offerId</span><span class="sxs-lookup"><span data-stu-id="89470-213">offerId</span></span>              | <span data-ttu-id="89470-214">ciąg</span><span class="sxs-lookup"><span data-stu-id="89470-214">string</span></span> | <span data-ttu-id="89470-215">Tak</span><span class="sxs-lookup"><span data-stu-id="89470-215">Yes</span></span>      | <span data-ttu-id="89470-216">Identyfikator oferty.</span><span class="sxs-lookup"><span data-stu-id="89470-216">The offer identifier.</span></span>                                                                                                                                                                                                                      |
| <span data-ttu-id="89470-217">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="89470-217">subscriptionId</span></span>       | <span data-ttu-id="89470-218">ciąg</span><span class="sxs-lookup"><span data-stu-id="89470-218">string</span></span> | <span data-ttu-id="89470-219">Nie</span><span class="sxs-lookup"><span data-stu-id="89470-219">No</span></span>       | <span data-ttu-id="89470-220">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="89470-220">The subscription identifier.</span></span>                                                                                                                                                                                                               |
| <span data-ttu-id="89470-221">parentSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="89470-221">parentSubscriptionId</span></span> | <span data-ttu-id="89470-222">ciąg</span><span class="sxs-lookup"><span data-stu-id="89470-222">string</span></span> | <span data-ttu-id="89470-223">Nie</span><span class="sxs-lookup"><span data-stu-id="89470-223">No</span></span>       | <span data-ttu-id="89470-224">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="89470-224">Optional.</span></span> <span data-ttu-id="89470-225">Identyfikator subskrypcji nadrzędnej w ofercie dodatku.</span><span class="sxs-lookup"><span data-stu-id="89470-225">The ID of the parent subscription in an add-on offer.</span></span> <span data-ttu-id="89470-226">Dotyczy tylko PATCH.</span><span class="sxs-lookup"><span data-stu-id="89470-226">Applies to PATCH only.</span></span>                                                                                                                                                     |
| <span data-ttu-id="89470-227">Friendlyname</span><span class="sxs-lookup"><span data-stu-id="89470-227">friendlyName</span></span>         | <span data-ttu-id="89470-228">ciąg</span><span class="sxs-lookup"><span data-stu-id="89470-228">string</span></span> | <span data-ttu-id="89470-229">Nie</span><span class="sxs-lookup"><span data-stu-id="89470-229">No</span></span>       | <span data-ttu-id="89470-230">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="89470-230">Optional.</span></span> <span data-ttu-id="89470-231">Przyjazna nazwa subskrypcji zdefiniowanej przez partnera w celu ujednoznacznienia.</span><span class="sxs-lookup"><span data-stu-id="89470-231">The friendly name for the subscription defined by the partner to help disambiguate.</span></span>                                                                                                                                              |
| <span data-ttu-id="89470-232">quantity</span><span class="sxs-lookup"><span data-stu-id="89470-232">quantity</span></span>             | <span data-ttu-id="89470-233">int</span><span class="sxs-lookup"><span data-stu-id="89470-233">int</span></span>    | <span data-ttu-id="89470-234">Tak</span><span class="sxs-lookup"><span data-stu-id="89470-234">Yes</span></span>      | <span data-ttu-id="89470-235">Liczba licencji dla subskrypcji opartej na licencjach.</span><span class="sxs-lookup"><span data-stu-id="89470-235">The number of licenses for a license-based subscription.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="89470-236">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="89470-236">partnerIdOnRecord</span></span>    | <span data-ttu-id="89470-237">ciąg</span><span class="sxs-lookup"><span data-stu-id="89470-237">string</span></span> | <span data-ttu-id="89470-238">Nie</span><span class="sxs-lookup"><span data-stu-id="89470-238">No</span></span>       | <span data-ttu-id="89470-239">Gdy dostawca pośredni złozy zamówienie w imieniu odsprzedawcy pośredniego, wypełnij to pole identyfikatorem MPN tylko odsprzedawcy pośredniego **(nigdy** identyfikatorem dostawcy pośredniego).</span><span class="sxs-lookup"><span data-stu-id="89470-239">When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider).</span></span> <span data-ttu-id="89470-240">Zapewnia to odpowiednią ewidencjonowanie zachęt.</span><span class="sxs-lookup"><span data-stu-id="89470-240">This ensures proper accounting for incentives.</span></span> |
| <span data-ttu-id="89470-241">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="89470-241">provisioningContext</span></span>  | <span data-ttu-id="89470-242">Ciąg<, ciąg></span><span class="sxs-lookup"><span data-stu-id="89470-242">Dictionary<string, string></span></span>                | <span data-ttu-id="89470-243">Nie</span><span class="sxs-lookup"><span data-stu-id="89470-243">No</span></span>       |  <span data-ttu-id="89470-244">Informacje wymagane do aprowizowania niektórych elementów w wykazie.</span><span class="sxs-lookup"><span data-stu-id="89470-244">Information required for provisioning for some items in the catalog.</span></span> <span data-ttu-id="89470-245">Właściwość provisioningVariables w sku wskazuje, które właściwości są wymagane dla określonych elementów w wykazie.</span><span class="sxs-lookup"><span data-stu-id="89470-245">The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.</span></span>                  |
| <span data-ttu-id="89470-246">Linki</span><span class="sxs-lookup"><span data-stu-id="89470-246">links</span></span>                | [<span data-ttu-id="89470-247">OrderLineItemLinks</span><span class="sxs-lookup"><span data-stu-id="89470-247">OrderLineItemLinks</span></span>](order-resources.md#orderlineitemlinks) | <span data-ttu-id="89470-248">Nie</span><span class="sxs-lookup"><span data-stu-id="89470-248">No</span></span>       |  <span data-ttu-id="89470-249">Tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="89470-249">Read-only.</span></span> <span data-ttu-id="89470-250">Zasób łączy się z elementem wiersza Order.</span><span class="sxs-lookup"><span data-stu-id="89470-250">The resource links corresponding to the Order line item.</span></span>  |
| <span data-ttu-id="89470-251">atrybuty</span><span class="sxs-lookup"><span data-stu-id="89470-251">attributes</span></span>           | [<span data-ttu-id="89470-252">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="89470-252">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="89470-253">Nie</span><span class="sxs-lookup"><span data-stu-id="89470-253">No</span></span>       | <span data-ttu-id="89470-254">Atrybuty metadanych odpowiadające OrderLineItem.</span><span class="sxs-lookup"><span data-stu-id="89470-254">The metadata attributes corresponding to the OrderLineItem.</span></span> |
| <span data-ttu-id="89470-255">renewsTo</span><span class="sxs-lookup"><span data-stu-id="89470-255">renewsTo</span></span>             | <span data-ttu-id="89470-256">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="89470-256">Array of objects</span></span>                          | <span data-ttu-id="89470-257">Nie</span><span class="sxs-lookup"><span data-stu-id="89470-257">No</span></span>    |<span data-ttu-id="89470-258">Tablica zasobów [RenewsTo.](order-resources.md#renewsto)</span><span class="sxs-lookup"><span data-stu-id="89470-258">An array of [RenewsTo](order-resources.md#renewsto) resources.</span></span>                                                                            |

##### <a name="renewsto"></a><span data-ttu-id="89470-259">RenewsTo</span><span class="sxs-lookup"><span data-stu-id="89470-259">RenewsTo</span></span>

<span data-ttu-id="89470-260">W tej tabeli [opisano właściwości RenewsTo](order-resources.md#renewsto) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="89470-260">This table describes the [RenewsTo](order-resources.md#renewsto) properties in the request body.</span></span>

| <span data-ttu-id="89470-261">Właściwość</span><span class="sxs-lookup"><span data-stu-id="89470-261">Property</span></span>              | <span data-ttu-id="89470-262">Typ</span><span class="sxs-lookup"><span data-stu-id="89470-262">Type</span></span>             | <span data-ttu-id="89470-263">Wymagane</span><span class="sxs-lookup"><span data-stu-id="89470-263">Required</span></span>        | <span data-ttu-id="89470-264">Opis</span><span class="sxs-lookup"><span data-stu-id="89470-264">Description</span></span> |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="89470-265">termDuration</span><span class="sxs-lookup"><span data-stu-id="89470-265">termDuration</span></span>          | <span data-ttu-id="89470-266">ciąg</span><span class="sxs-lookup"><span data-stu-id="89470-266">string</span></span>           | <span data-ttu-id="89470-267">Nie</span><span class="sxs-lookup"><span data-stu-id="89470-267">No</span></span>              | <span data-ttu-id="89470-268">Reprezentacja czasu trwania okresu odnowienia w standardach ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="89470-268">An ISO 8601 representation of the renewal term's duration.</span></span> <span data-ttu-id="89470-269">Obecnie obsługiwane wartości to **P1M** (1 miesiąc) i **P1Y** (1 rok).</span><span class="sxs-lookup"><span data-stu-id="89470-269">The current supported values are **P1M** (1 month) and **P1Y** (1 year).</span></span> |

### <a name="request-example"></a><span data-ttu-id="89470-270">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="89470-270">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Length: 691
Content-Type: application/json

{
  "BillingCycle": "one_time",
  "CurrencyCode": "USD",
  "LineItems": [
    {
      "LineItemNumber": 0,
      "ProvisioningContext": {
        "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
        "scope": "shared",
        "duration": "1Year"
      },
      "OfferId": "DZH318Z0BQ4B:0047:DZH318Z0DSM8",
      "FriendlyName": "A_sample_Azure_RI",
      "Quantity": 1
    }
  ]
}
```

## <a name="rest-response"></a><span data-ttu-id="89470-271">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="89470-271">REST response</span></span>

<span data-ttu-id="89470-272">W przypadku powodzenia metoda zwraca [zasób Order](order-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="89470-272">If successful, the method returns an [Order](order-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="89470-273">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="89470-273">Response success and error codes</span></span>

<span data-ttu-id="89470-274">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="89470-274">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="89470-275">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="89470-275">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="89470-276">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="89470-276">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="89470-277">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="89470-277">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 788
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b593cbb7-b358-4b31-81fc-e60b9c277a7f
MS-RequestId: 025f4c19-217f-49d6-a056-391902c62fb3
Date: Thu, 15 Mar 2018 22:30:02 GMT

{
  "id": "Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
  "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
  "billingCycle": "one_time",
  "currencyCode": "USD",
  "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "84A03D81-6B37-4D66-8D4A-FAEA24541538",
        "friendlyName": "A_sample_Azure_RI",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4B/skus/0047?country=US",
                "method": "GET",
                "headers": []
            }
        }
    } ],
    "creationDate": "2018-03-15T22:30:02.085152Z",
    "status": "pending",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
