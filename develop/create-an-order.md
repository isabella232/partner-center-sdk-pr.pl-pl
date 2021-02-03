---
title: Utwórz zamówienie klienta
description: Dowiedz się, jak utworzyć zamówienie dla klienta przy użyciu interfejsów API usługi Partner Center. Artykuł zawiera wymagania wstępne, kroki i przykłady.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ce176909a1f9c350f1c16615171de57a7beb888d
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/07/2020
ms.locfileid: "97768625"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a><span data-ttu-id="943ad-104">Tworzenie zamówienia dla klienta przy użyciu interfejsów API Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="943ad-104">Create an order for a customer using Partner Center APIs</span></span>

<span data-ttu-id="943ad-105">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="943ad-105">**Applies to:**</span></span>

- <span data-ttu-id="943ad-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="943ad-106">Partner Center</span></span>
- <span data-ttu-id="943ad-107">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="943ad-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="943ad-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="943ad-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="943ad-109">Tworzenie **zamówienia na produkty wystąpień zarezerwowanych maszyn wirtualnych platformy Azure** ma zastosowanie *tylko* do:</span><span class="sxs-lookup"><span data-stu-id="943ad-109">Creating an **order for Azure reserved VM instance products** applies *only* to:</span></span>

- <span data-ttu-id="943ad-110">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="943ad-110">Partner Center</span></span>

<span data-ttu-id="943ad-111">Aby uzyskać informacje o tym, co jest obecnie dostępne do sprzedawania, zobacz [oferty partnerów w programie Cloud Solution Provider](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="943ad-111">For information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="943ad-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="943ad-112">Prerequisites</span></span>

- <span data-ttu-id="943ad-113">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="943ad-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="943ad-114">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="943ad-114">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="943ad-115">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="943ad-115">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="943ad-116">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="943ad-116">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="943ad-117">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="943ad-117">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="943ad-118">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="943ad-118">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="943ad-119">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="943ad-119">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="943ad-120">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="943ad-120">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="943ad-121">Identyfikator oferty.</span><span class="sxs-lookup"><span data-stu-id="943ad-121">An offer identifier.</span></span>

## <a name="c"></a><span data-ttu-id="943ad-122">C\#</span><span class="sxs-lookup"><span data-stu-id="943ad-122">C\#</span></span>

<span data-ttu-id="943ad-123">Aby utworzyć zamówienie dla klienta:</span><span class="sxs-lookup"><span data-stu-id="943ad-123">To create an order for a customer:</span></span>

1. <span data-ttu-id="943ad-124">Utwórz wystąpienie obiektu [**Order**](order-resources.md) i ustaw właściwość **ReferenceCustomerID** na identyfikator klienta, aby zarejestrować klienta.</span><span class="sxs-lookup"><span data-stu-id="943ad-124">Instantiate an [**Order**](order-resources.md) object and set the **ReferenceCustomerID** property to the customer ID to record the customer.</span></span>

2. <span data-ttu-id="943ad-125">Utwórz listę obiektów [**OrderLineItem**](order-resources.md#orderlineitem) i przypisz listę do właściwości **LineItems** zamówienia.</span><span class="sxs-lookup"><span data-stu-id="943ad-125">Create a list of [**OrderLineItem**](order-resources.md#orderlineitem) objects, and assign the list to the order's **LineItems** property.</span></span> <span data-ttu-id="943ad-126">Każdy element wiersza zamówienia zawiera informacje o zakupie dla jednej oferty.</span><span class="sxs-lookup"><span data-stu-id="943ad-126">Each order line item contains the purchase information for one offer.</span></span> <span data-ttu-id="943ad-127">Musisz mieć co najmniej jeden element wiersza zamówienia.</span><span class="sxs-lookup"><span data-stu-id="943ad-127">You must have at least one order line item.</span></span>

3. <span data-ttu-id="943ad-128">Uzyskaj interfejs do porządkowania operacji.</span><span class="sxs-lookup"><span data-stu-id="943ad-128">Obtain an interface to order operations.</span></span> <span data-ttu-id="943ad-129">Najpierw Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="943ad-129">First, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="943ad-130">Następnie Pobierz interfejs z właściwości [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) .</span><span class="sxs-lookup"><span data-stu-id="943ad-130">Next, retrieve the interface from the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.</span></span>

4. <span data-ttu-id="943ad-131">Wywołaj metodę [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) lub [**onasync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) i przekaż obiekt [**Order**](order-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="943ad-131">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method and pass in the [**Order**](order-resources.md) object.</span></span>

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

<span data-ttu-id="943ad-132">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="943ad-132">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="943ad-133">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: CreateOrder.cs</span><span class="sxs-lookup"><span data-stu-id="943ad-133">**Project**: Partner Center SDK Samples **Class**: CreateOrder.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="943ad-134">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="943ad-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="943ad-135">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="943ad-135">Request syntax</span></span>

| <span data-ttu-id="943ad-136">Metoda</span><span class="sxs-lookup"><span data-stu-id="943ad-136">Method</span></span>   | <span data-ttu-id="943ad-137">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="943ad-137">Request URI</span></span>                                                                            |
|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="943ad-138">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="943ad-138">**POST**</span></span> | <span data-ttu-id="943ad-139">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/Orders http/1.1</span><span class="sxs-lookup"><span data-stu-id="943ad-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="943ad-140">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="943ad-140">URI parameters</span></span>

<span data-ttu-id="943ad-141">Użyj następującego parametru ścieżki, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="943ad-141">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="943ad-142">Nazwa</span><span class="sxs-lookup"><span data-stu-id="943ad-142">Name</span></span>        | <span data-ttu-id="943ad-143">Typ</span><span class="sxs-lookup"><span data-stu-id="943ad-143">Type</span></span>   | <span data-ttu-id="943ad-144">Wymagane</span><span class="sxs-lookup"><span data-stu-id="943ad-144">Required</span></span> | <span data-ttu-id="943ad-145">Opis</span><span class="sxs-lookup"><span data-stu-id="943ad-145">Description</span></span>                                                |
|-------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="943ad-146">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="943ad-146">customer-id</span></span> | <span data-ttu-id="943ad-147">ciąg</span><span class="sxs-lookup"><span data-stu-id="943ad-147">string</span></span> | <span data-ttu-id="943ad-148">Tak</span><span class="sxs-lookup"><span data-stu-id="943ad-148">Yes</span></span>      | <span data-ttu-id="943ad-149">Identyfikator GUID sformatowany przez klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="943ad-149">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="943ad-150">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="943ad-150">Request headers</span></span>

<span data-ttu-id="943ad-151">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="943ad-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="943ad-152">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="943ad-152">Request body</span></span>

#### <a name="order"></a><span data-ttu-id="943ad-153">Zamówienie</span><span class="sxs-lookup"><span data-stu-id="943ad-153">Order</span></span>

<span data-ttu-id="943ad-154">W tej tabeli opisano właściwości [zamówienia](order-resources.md) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="943ad-154">This table describes the [Order](order-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="943ad-155">Właściwość</span><span class="sxs-lookup"><span data-stu-id="943ad-155">Property</span></span>             | <span data-ttu-id="943ad-156">Typ</span><span class="sxs-lookup"><span data-stu-id="943ad-156">Type</span></span>                        | <span data-ttu-id="943ad-157">Wymagane</span><span class="sxs-lookup"><span data-stu-id="943ad-157">Required</span></span>                        | <span data-ttu-id="943ad-158">Opis</span><span class="sxs-lookup"><span data-stu-id="943ad-158">Description</span></span>                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| <span data-ttu-id="943ad-159">identyfikator</span><span class="sxs-lookup"><span data-stu-id="943ad-159">id</span></span>                   | <span data-ttu-id="943ad-160">ciąg</span><span class="sxs-lookup"><span data-stu-id="943ad-160">string</span></span>                      | <span data-ttu-id="943ad-161">Nie</span><span class="sxs-lookup"><span data-stu-id="943ad-161">No</span></span>                              | <span data-ttu-id="943ad-162">Identyfikator zamówienia, który jest dostarczany po pomyślnym utworzeniu zamówienia.</span><span class="sxs-lookup"><span data-stu-id="943ad-162">An order identifier that is supplied upon successful creation of the order.</span></span>   |
| <span data-ttu-id="943ad-163">referenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="943ad-163">referenceCustomerId</span></span>  | <span data-ttu-id="943ad-164">ciąg</span><span class="sxs-lookup"><span data-stu-id="943ad-164">string</span></span>                      | <span data-ttu-id="943ad-165">Nie</span><span class="sxs-lookup"><span data-stu-id="943ad-165">No</span></span>                              | <span data-ttu-id="943ad-166">Identyfikator klienta.</span><span class="sxs-lookup"><span data-stu-id="943ad-166">The customer identifier.</span></span> |
| <span data-ttu-id="943ad-167">billingCycle</span><span class="sxs-lookup"><span data-stu-id="943ad-167">billingCycle</span></span>         | <span data-ttu-id="943ad-168">ciąg</span><span class="sxs-lookup"><span data-stu-id="943ad-168">string</span></span>                      | <span data-ttu-id="943ad-169">Nie</span><span class="sxs-lookup"><span data-stu-id="943ad-169">No</span></span>                              | <span data-ttu-id="943ad-170">Wskazuje częstotliwość, z jaką jest rozliczany partner dla tego zamówienia.</span><span class="sxs-lookup"><span data-stu-id="943ad-170">Indicates the frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="943ad-171">Obsługiwane wartości to nazwy elementów członkowskich Znalezione w [BillingCycleType](product-resources.md#billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="943ad-171">Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype).</span></span> <span data-ttu-id="943ad-172">Wartość domyślna to "Monthly" lub "jednorazowej" podczas tworzenia kolejności.</span><span class="sxs-lookup"><span data-stu-id="943ad-172">The default is "Monthly" or "OneTime" at order creation.</span></span> <span data-ttu-id="943ad-173">To pole jest stosowane po pomyślnym utworzeniu zamówienia.</span><span class="sxs-lookup"><span data-stu-id="943ad-173">This field is applied upon successful creation of the order.</span></span> |
| <span data-ttu-id="943ad-174">lineItems</span><span class="sxs-lookup"><span data-stu-id="943ad-174">lineItems</span></span>            | <span data-ttu-id="943ad-175">Tablica zasobów [OrderLineItem](order-resources.md#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="943ad-175">array of [OrderLineItem](order-resources.md#orderlineitem) resources</span></span> | <span data-ttu-id="943ad-176">Tak</span><span class="sxs-lookup"><span data-stu-id="943ad-176">Yes</span></span>      | <span data-ttu-id="943ad-177">Lista elementów oferty, do których klient kupuje, wraz z ilością.</span><span class="sxs-lookup"><span data-stu-id="943ad-177">An itemized list of the offers the customer is purchasing including the quantity.</span></span>        |
| <span data-ttu-id="943ad-178">currencyCode</span><span class="sxs-lookup"><span data-stu-id="943ad-178">currencyCode</span></span>         | <span data-ttu-id="943ad-179">ciąg</span><span class="sxs-lookup"><span data-stu-id="943ad-179">string</span></span>                      | <span data-ttu-id="943ad-180">Nie</span><span class="sxs-lookup"><span data-stu-id="943ad-180">No</span></span>                              | <span data-ttu-id="943ad-181">Tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="943ad-181">Read-only.</span></span> <span data-ttu-id="943ad-182">Waluta użyta podczas umieszczania zamówienia.</span><span class="sxs-lookup"><span data-stu-id="943ad-182">The currency used when placing the order.</span></span> <span data-ttu-id="943ad-183">Stosowane po pomyślnym utworzeniu zamówienia.</span><span class="sxs-lookup"><span data-stu-id="943ad-183">Applied upon successful creation of the order.</span></span>           |
| <span data-ttu-id="943ad-184">creationDate</span><span class="sxs-lookup"><span data-stu-id="943ad-184">creationDate</span></span>         | <span data-ttu-id="943ad-185">datetime</span><span class="sxs-lookup"><span data-stu-id="943ad-185">datetime</span></span>                    | <span data-ttu-id="943ad-186">Nie</span><span class="sxs-lookup"><span data-stu-id="943ad-186">No</span></span>                              | <span data-ttu-id="943ad-187">Tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="943ad-187">Read-only.</span></span> <span data-ttu-id="943ad-188">Data, w której zamówienie zostało utworzone, w formacie daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="943ad-188">The date the order was created, in date-time format.</span></span> <span data-ttu-id="943ad-189">Stosowane po pomyślnym utworzeniu zamówienia.</span><span class="sxs-lookup"><span data-stu-id="943ad-189">Applied upon successful creation of the order.</span></span>                                   |
| <span data-ttu-id="943ad-190">status</span><span class="sxs-lookup"><span data-stu-id="943ad-190">status</span></span>               | <span data-ttu-id="943ad-191">ciąg</span><span class="sxs-lookup"><span data-stu-id="943ad-191">string</span></span>                      | <span data-ttu-id="943ad-192">Nie</span><span class="sxs-lookup"><span data-stu-id="943ad-192">No</span></span>                              | <span data-ttu-id="943ad-193">Tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="943ad-193">Read-only.</span></span> <span data-ttu-id="943ad-194">Stan zamówienia.</span><span class="sxs-lookup"><span data-stu-id="943ad-194">The status of the order.</span></span>  <span data-ttu-id="943ad-195">Obsługiwane wartości to nazwy elementów członkowskich Znalezione w [OrderStatus](order-resources.md#orderstatus).</span><span class="sxs-lookup"><span data-stu-id="943ad-195">Supported values are the member names found in [OrderStatus](order-resources.md#orderstatus).</span></span>        |
| <span data-ttu-id="943ad-196">linki</span><span class="sxs-lookup"><span data-stu-id="943ad-196">links</span></span>                | [<span data-ttu-id="943ad-197">OrderLinks</span><span class="sxs-lookup"><span data-stu-id="943ad-197">OrderLinks</span></span>](utility-resources.md#resourcelinks)              | <span data-ttu-id="943ad-198">Nie</span><span class="sxs-lookup"><span data-stu-id="943ad-198">No</span></span>                              | <span data-ttu-id="943ad-199">Linki do zasobów odpowiadające kolejności.</span><span class="sxs-lookup"><span data-stu-id="943ad-199">The resource links corresponding to the Order.</span></span> |
| <span data-ttu-id="943ad-200">atrybuty</span><span class="sxs-lookup"><span data-stu-id="943ad-200">attributes</span></span>           | [<span data-ttu-id="943ad-201">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="943ad-201">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="943ad-202">Nie</span><span class="sxs-lookup"><span data-stu-id="943ad-202">No</span></span>                              | <span data-ttu-id="943ad-203">Atrybuty metadanych odpowiadające kolejności.</span><span class="sxs-lookup"><span data-stu-id="943ad-203">The metadata attributes corresponding to the Order.</span></span> |

#### <a name="orderlineitem"></a><span data-ttu-id="943ad-204">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="943ad-204">OrderLineItem</span></span>

<span data-ttu-id="943ad-205">W tej tabeli opisano właściwości [OrderLineItem](order-resources.md#orderlineitem) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="943ad-205">This table describes the [OrderLineItem](order-resources.md#orderlineitem) properties in the request body.</span></span>

>[!NOTE]
><span data-ttu-id="943ad-206">PartnerIdOnRecord należy podać tylko wtedy, gdy Dostawca pośredni umieści zamówienie w imieniu pośredniego odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="943ad-206">The partnerIdOnRecord should only be provided when an indirect provider places an order on behalf of an indirect reseller.</span></span> <span data-ttu-id="943ad-207">Jest on używany do przechowywania tylko identyfikatora Microsoft Partner Network pośredniego Odsprzedawcy (nigdy nie jest to identyfikator dostawcy pośredniego).</span><span class="sxs-lookup"><span data-stu-id="943ad-207">It's used to store the Microsoft Partner Network ID of the indirect reseller only (never the ID of the indirect provider).</span></span>

| <span data-ttu-id="943ad-208">Nazwa</span><span class="sxs-lookup"><span data-stu-id="943ad-208">Name</span></span>                 | <span data-ttu-id="943ad-209">Typ</span><span class="sxs-lookup"><span data-stu-id="943ad-209">Type</span></span>   | <span data-ttu-id="943ad-210">Wymagane</span><span class="sxs-lookup"><span data-stu-id="943ad-210">Required</span></span> | <span data-ttu-id="943ad-211">Opis</span><span class="sxs-lookup"><span data-stu-id="943ad-211">Description</span></span>                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="943ad-212">lineItemNumber</span><span class="sxs-lookup"><span data-stu-id="943ad-212">lineItemNumber</span></span>       | <span data-ttu-id="943ad-213">int</span><span class="sxs-lookup"><span data-stu-id="943ad-213">int</span></span>    | <span data-ttu-id="943ad-214">Tak</span><span class="sxs-lookup"><span data-stu-id="943ad-214">Yes</span></span>      | <span data-ttu-id="943ad-215">Każdy element wiersza w kolekcji pobiera unikatowy numer wiersza, licząc do wartości z przedziału od 0 do count-1.</span><span class="sxs-lookup"><span data-stu-id="943ad-215">Each line item in the collection gets a unique line number, counting up from 0 to count-1.</span></span>                                                                                                                                                 |
| <span data-ttu-id="943ad-216">offerId</span><span class="sxs-lookup"><span data-stu-id="943ad-216">offerId</span></span>              | <span data-ttu-id="943ad-217">ciąg</span><span class="sxs-lookup"><span data-stu-id="943ad-217">string</span></span> | <span data-ttu-id="943ad-218">Tak</span><span class="sxs-lookup"><span data-stu-id="943ad-218">Yes</span></span>      | <span data-ttu-id="943ad-219">Identyfikator oferty.</span><span class="sxs-lookup"><span data-stu-id="943ad-219">The offer identifier.</span></span>                                                                                                                                                                                                                      |
| <span data-ttu-id="943ad-220">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="943ad-220">subscriptionId</span></span>       | <span data-ttu-id="943ad-221">ciąg</span><span class="sxs-lookup"><span data-stu-id="943ad-221">string</span></span> | <span data-ttu-id="943ad-222">Nie</span><span class="sxs-lookup"><span data-stu-id="943ad-222">No</span></span>       | <span data-ttu-id="943ad-223">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="943ad-223">The subscription identifier.</span></span>                                                                                                                                                                                                               |
| <span data-ttu-id="943ad-224">parentSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="943ad-224">parentSubscriptionId</span></span> | <span data-ttu-id="943ad-225">ciąg</span><span class="sxs-lookup"><span data-stu-id="943ad-225">string</span></span> | <span data-ttu-id="943ad-226">Nie</span><span class="sxs-lookup"><span data-stu-id="943ad-226">No</span></span>       | <span data-ttu-id="943ad-227">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="943ad-227">Optional.</span></span> <span data-ttu-id="943ad-228">Identyfikator subskrypcji nadrzędnej w ofercie dodatku.</span><span class="sxs-lookup"><span data-stu-id="943ad-228">The ID of the parent subscription in an add-on offer.</span></span> <span data-ttu-id="943ad-229">Dotyczy tylko poprawki.</span><span class="sxs-lookup"><span data-stu-id="943ad-229">Applies to PATCH only.</span></span>                                                                                                                                                     |
| <span data-ttu-id="943ad-230">friendlyName</span><span class="sxs-lookup"><span data-stu-id="943ad-230">friendlyName</span></span>         | <span data-ttu-id="943ad-231">ciąg</span><span class="sxs-lookup"><span data-stu-id="943ad-231">string</span></span> | <span data-ttu-id="943ad-232">Nie</span><span class="sxs-lookup"><span data-stu-id="943ad-232">No</span></span>       | <span data-ttu-id="943ad-233">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="943ad-233">Optional.</span></span> <span data-ttu-id="943ad-234">Przyjazna nazwa dla subskrypcji zdefiniowanej przez partnera, która pomaga w odróżnieniu od siebie.</span><span class="sxs-lookup"><span data-stu-id="943ad-234">The friendly name for the subscription defined by the partner to help disambiguate.</span></span>                                                                                                                                              |
| <span data-ttu-id="943ad-235">quantity</span><span class="sxs-lookup"><span data-stu-id="943ad-235">quantity</span></span>             | <span data-ttu-id="943ad-236">int</span><span class="sxs-lookup"><span data-stu-id="943ad-236">int</span></span>    | <span data-ttu-id="943ad-237">Tak</span><span class="sxs-lookup"><span data-stu-id="943ad-237">Yes</span></span>      | <span data-ttu-id="943ad-238">Liczba licencji dla subskrypcji opartej na licencji.</span><span class="sxs-lookup"><span data-stu-id="943ad-238">The number of licenses for a license-based subscription.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="943ad-239">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="943ad-239">partnerIdOnRecord</span></span>    | <span data-ttu-id="943ad-240">ciąg</span><span class="sxs-lookup"><span data-stu-id="943ad-240">string</span></span> | <span data-ttu-id="943ad-241">Nie</span><span class="sxs-lookup"><span data-stu-id="943ad-241">No</span></span>       | <span data-ttu-id="943ad-242">Gdy Dostawca pośredni umieści zamówienie w imieniu pośredniego odsprzedawcy, Wypełnij to pole IDENTYFIKATORem MPN **pośredniego odsprzedawcy** (nigdy nie jest identyfikatorem dostawcy pośredniego).</span><span class="sxs-lookup"><span data-stu-id="943ad-242">When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider).</span></span> <span data-ttu-id="943ad-243">Zapewnia to odpowiednie Księgowanie zachęt.</span><span class="sxs-lookup"><span data-stu-id="943ad-243">This ensures proper accounting for incentives.</span></span> |
| <span data-ttu-id="943ad-244">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="943ad-244">provisioningContext</span></span>  | <span data-ttu-id="943ad-245">Ciąg<słownika, ciąg></span><span class="sxs-lookup"><span data-stu-id="943ad-245">Dictionary<string, string></span></span>                | <span data-ttu-id="943ad-246">Nie</span><span class="sxs-lookup"><span data-stu-id="943ad-246">No</span></span>       |  <span data-ttu-id="943ad-247">Informacje wymagane do aprowizacji dla niektórych elementów w wykazie.</span><span class="sxs-lookup"><span data-stu-id="943ad-247">Information required for provisioning for some items in the catalog.</span></span> <span data-ttu-id="943ad-248">Właściwość provisioningVariables w jednostce SKU wskazuje, które właściwości są wymagane dla określonych elementów w wykazie.</span><span class="sxs-lookup"><span data-stu-id="943ad-248">The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.</span></span>                  |
| <span data-ttu-id="943ad-249">linki</span><span class="sxs-lookup"><span data-stu-id="943ad-249">links</span></span>                | [<span data-ttu-id="943ad-250">OrderLineItemLinks</span><span class="sxs-lookup"><span data-stu-id="943ad-250">OrderLineItemLinks</span></span>](order-resources.md#orderlineitemlinks) | <span data-ttu-id="943ad-251">Nie</span><span class="sxs-lookup"><span data-stu-id="943ad-251">No</span></span>       |  <span data-ttu-id="943ad-252">Tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="943ad-252">Read-only.</span></span> <span data-ttu-id="943ad-253">Linki do zasobów odpowiadające elementowi wiersza zamówienia.</span><span class="sxs-lookup"><span data-stu-id="943ad-253">The resource links corresponding to the Order line item.</span></span>  |
| <span data-ttu-id="943ad-254">atrybuty</span><span class="sxs-lookup"><span data-stu-id="943ad-254">attributes</span></span>           | [<span data-ttu-id="943ad-255">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="943ad-255">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="943ad-256">Nie</span><span class="sxs-lookup"><span data-stu-id="943ad-256">No</span></span>       | <span data-ttu-id="943ad-257">Atrybuty metadanych odpowiadające OrderLineItem.</span><span class="sxs-lookup"><span data-stu-id="943ad-257">The metadata attributes corresponding to the OrderLineItem.</span></span> |
| <span data-ttu-id="943ad-258">renewsTo</span><span class="sxs-lookup"><span data-stu-id="943ad-258">renewsTo</span></span>             | <span data-ttu-id="943ad-259">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="943ad-259">Array of objects</span></span>                          | <span data-ttu-id="943ad-260">Nie</span><span class="sxs-lookup"><span data-stu-id="943ad-260">No</span></span>    |<span data-ttu-id="943ad-261">Tablica zasobów [RenewsTo](order-resources.md#renewsto) .</span><span class="sxs-lookup"><span data-stu-id="943ad-261">An array of [RenewsTo](order-resources.md#renewsto) resources.</span></span>                                                                            |

##### <a name="renewsto"></a><span data-ttu-id="943ad-262">RenewsTo</span><span class="sxs-lookup"><span data-stu-id="943ad-262">RenewsTo</span></span>

<span data-ttu-id="943ad-263">W tej tabeli opisano właściwości [RenewsTo](order-resources.md#renewsto) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="943ad-263">This table describes the [RenewsTo](order-resources.md#renewsto) properties in the request body.</span></span>

| <span data-ttu-id="943ad-264">Właściwość</span><span class="sxs-lookup"><span data-stu-id="943ad-264">Property</span></span>              | <span data-ttu-id="943ad-265">Typ</span><span class="sxs-lookup"><span data-stu-id="943ad-265">Type</span></span>             | <span data-ttu-id="943ad-266">Wymagane</span><span class="sxs-lookup"><span data-stu-id="943ad-266">Required</span></span>        | <span data-ttu-id="943ad-267">Opis</span><span class="sxs-lookup"><span data-stu-id="943ad-267">Description</span></span> |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="943ad-268">termDuration</span><span class="sxs-lookup"><span data-stu-id="943ad-268">termDuration</span></span>          | <span data-ttu-id="943ad-269">ciąg</span><span class="sxs-lookup"><span data-stu-id="943ad-269">string</span></span>           | <span data-ttu-id="943ad-270">Nie</span><span class="sxs-lookup"><span data-stu-id="943ad-270">No</span></span>              | <span data-ttu-id="943ad-271">Reprezentacja ISO 8601 okresu ważności.</span><span class="sxs-lookup"><span data-stu-id="943ad-271">An ISO 8601 representation of the renewal term's duration.</span></span> <span data-ttu-id="943ad-272">Bieżące obsługiwane wartości to **P1M** (1 miesiąc) i **P1Y** (1 rok).</span><span class="sxs-lookup"><span data-stu-id="943ad-272">The current supported values are **P1M** (1 month) and **P1Y** (1 year).</span></span> |

### <a name="request-example"></a><span data-ttu-id="943ad-273">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="943ad-273">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="943ad-274">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="943ad-274">REST response</span></span>

<span data-ttu-id="943ad-275">Jeśli to się powiedzie, metoda zwraca zasób [zamówienia](order-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="943ad-275">If successful, the method returns an [Order](order-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="943ad-276">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="943ad-276">Response success and error codes</span></span>

<span data-ttu-id="943ad-277">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="943ad-277">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="943ad-278">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="943ad-278">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="943ad-279">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="943ad-279">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="943ad-280">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="943ad-280">Response example</span></span>

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
