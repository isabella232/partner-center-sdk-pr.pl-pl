---
title: Tworzenie zamówienia klienta dla odsprzedawcy pośredniego
description: Dowiedz się, jak Partner Center api do tworzenia zamówienia dla klienta odsprzedawcy pośredniego. Artykuł zawiera wymagania wstępne, kroki i przykłady.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6253ba2289ea1f58e7d8eaa960d7d0daaa887f0d
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973551"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a><span data-ttu-id="d3aea-104">Utwórz zamówienie dla klienta odsprzedawcy pośredniego</span><span class="sxs-lookup"><span data-stu-id="d3aea-104">Create an order for a customer of an indirect reseller</span></span>

<span data-ttu-id="d3aea-105">Jak utworzyć zamówienie dla klienta odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="d3aea-105">How to create an order for a customer of an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3aea-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d3aea-106">Prerequisites</span></span>

- <span data-ttu-id="d3aea-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d3aea-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d3aea-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d3aea-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="d3aea-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d3aea-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d3aea-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="d3aea-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d3aea-111">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="d3aea-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d3aea-112">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="d3aea-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d3aea-113">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="d3aea-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d3aea-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d3aea-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d3aea-115">Identyfikator oferty przedmiotu do zakupu.</span><span class="sxs-lookup"><span data-stu-id="d3aea-115">The offer identifier of the item to purchase.</span></span>

- <span data-ttu-id="d3aea-116">Identyfikator dzierżawy odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="d3aea-116">The tenant identifier of the indirect reseller.</span></span>

## <a name="c"></a><span data-ttu-id="d3aea-117">C\#</span><span class="sxs-lookup"><span data-stu-id="d3aea-117">C\#</span></span>

<span data-ttu-id="d3aea-118">Aby utworzyć zamówienie dla klienta odsprzedawcy pośredniego:</span><span class="sxs-lookup"><span data-stu-id="d3aea-118">To create an order for a customer of an indirect reseller:</span></span>

1. <span data-ttu-id="d3aea-119">Pobierz kolekcję odsprzedawców pośrednich, którzy mają relację z zalogowanym partnerem.</span><span class="sxs-lookup"><span data-stu-id="d3aea-119">Get a collection of the indirect resellers that have a relationship with the signed-in partner.</span></span>

2. <span data-ttu-id="d3aea-120">Pobierz zmienną lokalną do elementu w kolekcji, który odpowiada identyfikatorowi odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="d3aea-120">Get a local variable to the item in the collection that matches the indirect reseller ID.</span></span> <span data-ttu-id="d3aea-121">Ten krok pomaga uzyskać dostęp do właściwości [**MpnId odsprzedawcy**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) podczas tworzenia zamówienia.</span><span class="sxs-lookup"><span data-stu-id="d3aea-121">This step helps you access the reseller's [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) property when you create the order.</span></span>

3. <span data-ttu-id="d3aea-122">Za pomocą wystąpienia obiektu [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) ustaw właściwość [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) na identyfikator klienta, aby zarejestrować klienta.</span><span class="sxs-lookup"><span data-stu-id="d3aea-122">Instantiate an [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and set the [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) property to the customer identifier in order to record the customer.</span></span>

4. <span data-ttu-id="d3aea-123">Utwórz listę obiektów [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) i przypisz listę do właściwości [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) zamówienia.</span><span class="sxs-lookup"><span data-stu-id="d3aea-123">Create a list of [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) objects, and assign the list to the order's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) property.</span></span> <span data-ttu-id="d3aea-124">Każdy element wiersza zamówienia zawiera informacje o zakupie dla jednej oferty.</span><span class="sxs-lookup"><span data-stu-id="d3aea-124">Each order line item contains the purchase information for one offer.</span></span> <span data-ttu-id="d3aea-125">Pamiętaj, aby w każdym wierszu wypełnić właściwość [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) identyfikatorem MPN odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="d3aea-125">Be sure to populate the [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) property in each line item with the MPN ID of the indirect reseller.</span></span> <span data-ttu-id="d3aea-126">Musisz mieć co najmniej jeden wiersz zamówienia.</span><span class="sxs-lookup"><span data-stu-id="d3aea-126">You must have at least one order line item.</span></span>

5. <span data-ttu-id="d3aea-127">Uzyskaj interfejs do obsługi zamówień operacji, wywołując metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta, a następnie pobierz interfejs z [**właściwości Orders.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders)</span><span class="sxs-lookup"><span data-stu-id="d3aea-127">Obtain an interface to order operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieve the interface from the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.</span></span>

6. <span data-ttu-id="d3aea-128">Wywołaj [**metodę Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) lub [**CreateAsync,**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) aby utworzyć zamówienie.</span><span class="sxs-lookup"><span data-stu-id="d3aea-128">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method to create the order.</span></span>

### <a name="c-example"></a><span data-ttu-id="d3aea-129">Przykład w \# języku C</span><span class="sxs-lookup"><span data-stu-id="d3aea-129">C\# example</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string indirectResellerId;

// Get the indirect resellers with a relationship to the signed-in partner.
var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);

// Find the matching reseller in the collection.
var selectedIndirectReseller = (indirectResellers != null && indirectResellers.Items.Any()) ?
    indirectResellers.Items.FirstOrDefault(reseller => reseller.Id.Equals(indirectResellerId, StringComparison.OrdinalIgnoreCase)) :
    null;

// Prepare the order and populate the PartnerIdOnRecord with the reseller&#39;s Microsoft Partner Network Id.
var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "New offer purchase.",
            Quantity = 5,
            PartnerIdOnRecord = selectedIndirectReseller != null ? selectedIndirectReseller.MpnId : null
        }
    }
};

// Place the order.
var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

<span data-ttu-id="d3aea-130">**Przykład:** [Aplikacja testowa konsoli](console-test-app.md)**Project**: zestaw SDK Centrum partnerskiego Samples **Class**: PlaceOrderForCustomer.cs</span><span class="sxs-lookup"><span data-stu-id="d3aea-130">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: PlaceOrderForCustomer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d3aea-131">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="d3aea-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d3aea-132">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="d3aea-132">Request syntax</span></span>

| <span data-ttu-id="d3aea-133">Metoda</span><span class="sxs-lookup"><span data-stu-id="d3aea-133">Method</span></span>   | <span data-ttu-id="d3aea-134">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="d3aea-134">Request URI</span></span>                                                                            |
|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="d3aea-135">**Post**</span><span class="sxs-lookup"><span data-stu-id="d3aea-135">**POST**</span></span> | <span data-ttu-id="d3aea-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d3aea-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="d3aea-137">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="d3aea-137">URI parameters</span></span>

<span data-ttu-id="d3aea-138">Użyj następującego parametru ścieżki, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="d3aea-138">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="d3aea-139">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d3aea-139">Name</span></span>        | <span data-ttu-id="d3aea-140">Typ</span><span class="sxs-lookup"><span data-stu-id="d3aea-140">Type</span></span>   | <span data-ttu-id="d3aea-141">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d3aea-141">Required</span></span> | <span data-ttu-id="d3aea-142">Opis</span><span class="sxs-lookup"><span data-stu-id="d3aea-142">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="d3aea-143">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="d3aea-143">customer-id</span></span> | <span data-ttu-id="d3aea-144">ciąg</span><span class="sxs-lookup"><span data-stu-id="d3aea-144">string</span></span> | <span data-ttu-id="d3aea-145">Tak</span><span class="sxs-lookup"><span data-stu-id="d3aea-145">Yes</span></span>      | <span data-ttu-id="d3aea-146">Ciąg w formacie identyfikatora GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="d3aea-146">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d3aea-147">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="d3aea-147">Request headers</span></span>

<span data-ttu-id="d3aea-148">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d3aea-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d3aea-149">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="d3aea-149">Request body</span></span>

#### <a name="order"></a><span data-ttu-id="d3aea-150">Zamówienie</span><span class="sxs-lookup"><span data-stu-id="d3aea-150">Order</span></span>

<span data-ttu-id="d3aea-151">W tej tabeli **opisano właściwości** Order w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="d3aea-151">This table describes the **Order** properties in the request body.</span></span>

| <span data-ttu-id="d3aea-152">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d3aea-152">Name</span></span> | <span data-ttu-id="d3aea-153">Typ</span><span class="sxs-lookup"><span data-stu-id="d3aea-153">Type</span></span> | <span data-ttu-id="d3aea-154">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d3aea-154">Required</span></span> | <span data-ttu-id="d3aea-155">Opis</span><span class="sxs-lookup"><span data-stu-id="d3aea-155">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="d3aea-156">identyfikator</span><span class="sxs-lookup"><span data-stu-id="d3aea-156">id</span></span> | <span data-ttu-id="d3aea-157">ciąg</span><span class="sxs-lookup"><span data-stu-id="d3aea-157">string</span></span> | <span data-ttu-id="d3aea-158">Nie</span><span class="sxs-lookup"><span data-stu-id="d3aea-158">No</span></span> | <span data-ttu-id="d3aea-159">Identyfikator zamówienia podany po pomyślnym utworzeniu zamówienia.</span><span class="sxs-lookup"><span data-stu-id="d3aea-159">An order identifier that is supplied upon successful creation of the order.</span></span> |
| <span data-ttu-id="d3aea-160">referenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="d3aea-160">referenceCustomerId</span></span> | <span data-ttu-id="d3aea-161">ciąg</span><span class="sxs-lookup"><span data-stu-id="d3aea-161">string</span></span> | <span data-ttu-id="d3aea-162">Tak</span><span class="sxs-lookup"><span data-stu-id="d3aea-162">Yes</span></span> | <span data-ttu-id="d3aea-163">Identyfikator klienta.</span><span class="sxs-lookup"><span data-stu-id="d3aea-163">The customer identifier.</span></span> |
| <span data-ttu-id="d3aea-164">billingCycle</span><span class="sxs-lookup"><span data-stu-id="d3aea-164">billingCycle</span></span> | <span data-ttu-id="d3aea-165">ciąg</span><span class="sxs-lookup"><span data-stu-id="d3aea-165">string</span></span> | <span data-ttu-id="d3aea-166">Nie</span><span class="sxs-lookup"><span data-stu-id="d3aea-166">No</span></span> | <span data-ttu-id="d3aea-167">Częstotliwość, za jaką partner jest rozliczany za to zamówienie.</span><span class="sxs-lookup"><span data-stu-id="d3aea-167">The frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="d3aea-168">Wartość domyślna &quot; to Co miesiąc i jest stosowana po &quot; pomyślnym utworzeniu zamówienia.</span><span class="sxs-lookup"><span data-stu-id="d3aea-168">The default is &quot;Monthly&quot; and is applied upon successful creation of the order.</span></span> <span data-ttu-id="d3aea-169">Obsługiwane wartości to nazwy członków w [**typie BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="d3aea-169">Supported values are the member names found in [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype).</span></span> <span data-ttu-id="d3aea-170">Uwaga: funkcja rozliczeń rocznych nie jest jeszcze ogólnie dostępna.</span><span class="sxs-lookup"><span data-stu-id="d3aea-170">Note: the annual billing feature isn't yet generally available.</span></span> <span data-ttu-id="d3aea-171">Obsługa rozliczeń rocznych zostanie w wkrótce wywłasz ędna.</span><span class="sxs-lookup"><span data-stu-id="d3aea-171">Support for annual billing is coming soon.</span></span> |
| <span data-ttu-id="d3aea-172">lineItems</span><span class="sxs-lookup"><span data-stu-id="d3aea-172">lineItems</span></span> | <span data-ttu-id="d3aea-173">tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="d3aea-173">array of objects</span></span> | <span data-ttu-id="d3aea-174">Tak</span><span class="sxs-lookup"><span data-stu-id="d3aea-174">Yes</span></span> | <span data-ttu-id="d3aea-175">Tablica zasobów [**OrderLineItem.**](#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="d3aea-175">An array of [**OrderLineItem**](#orderlineitem) resources.</span></span> |
| <span data-ttu-id="d3aea-176">Creationdate</span><span class="sxs-lookup"><span data-stu-id="d3aea-176">creationDate</span></span> | <span data-ttu-id="d3aea-177">ciąg</span><span class="sxs-lookup"><span data-stu-id="d3aea-177">string</span></span> | <span data-ttu-id="d3aea-178">Nie</span><span class="sxs-lookup"><span data-stu-id="d3aea-178">No</span></span> | <span data-ttu-id="d3aea-179">Data utworzenia zamówienia w formacie data/godzina.</span><span class="sxs-lookup"><span data-stu-id="d3aea-179">The date the order was created, in date-time format.</span></span> <span data-ttu-id="d3aea-180">Stosowane po pomyślnym utworzeniu zamówienia.</span><span class="sxs-lookup"><span data-stu-id="d3aea-180">Applied upon successful creation of the order.</span></span> |
| <span data-ttu-id="d3aea-181">atrybuty</span><span class="sxs-lookup"><span data-stu-id="d3aea-181">attributes</span></span> | <span data-ttu-id="d3aea-182">object</span><span class="sxs-lookup"><span data-stu-id="d3aea-182">object</span></span> | <span data-ttu-id="d3aea-183">Nie</span><span class="sxs-lookup"><span data-stu-id="d3aea-183">No</span></span> | <span data-ttu-id="d3aea-184">Zawiera "ObjectType": "Order".</span><span class="sxs-lookup"><span data-stu-id="d3aea-184">Contains "ObjectType": "Order".</span></span> |

#### <a name="orderlineitem"></a><span data-ttu-id="d3aea-185">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="d3aea-185">OrderLineItem</span></span>

<span data-ttu-id="d3aea-186">W tej tabeli **opisano właściwości OrderLineItem** w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="d3aea-186">This table describes the **OrderLineItem** properties in the request body.</span></span>

| <span data-ttu-id="d3aea-187">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d3aea-187">Name</span></span> | <span data-ttu-id="d3aea-188">Typ</span><span class="sxs-lookup"><span data-stu-id="d3aea-188">Type</span></span> | <span data-ttu-id="d3aea-189">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d3aea-189">Required</span></span> | <span data-ttu-id="d3aea-190">Opis</span><span class="sxs-lookup"><span data-stu-id="d3aea-190">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="d3aea-191">lineItemNumber</span><span class="sxs-lookup"><span data-stu-id="d3aea-191">lineItemNumber</span></span> | <span data-ttu-id="d3aea-192">int</span><span class="sxs-lookup"><span data-stu-id="d3aea-192">int</span></span> | <span data-ttu-id="d3aea-193">Tak</span><span class="sxs-lookup"><span data-stu-id="d3aea-193">Yes</span></span> | <span data-ttu-id="d3aea-194">Każdy element wiersza w kolekcji otrzymuje unikatowy numer wiersza, licząc od 0 do count-1.</span><span class="sxs-lookup"><span data-stu-id="d3aea-194">Each line item in the collection gets a unique line number, counting up from 0 to count-1.</span></span> |
| <span data-ttu-id="d3aea-195">offerId</span><span class="sxs-lookup"><span data-stu-id="d3aea-195">offerId</span></span> | <span data-ttu-id="d3aea-196">ciąg</span><span class="sxs-lookup"><span data-stu-id="d3aea-196">string</span></span> | <span data-ttu-id="d3aea-197">Tak</span><span class="sxs-lookup"><span data-stu-id="d3aea-197">Yes</span></span> | <span data-ttu-id="d3aea-198">Identyfikator oferty.</span><span class="sxs-lookup"><span data-stu-id="d3aea-198">The offer identifier.</span></span> |
| <span data-ttu-id="d3aea-199">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="d3aea-199">subscriptionId</span></span> | <span data-ttu-id="d3aea-200">ciąg</span><span class="sxs-lookup"><span data-stu-id="d3aea-200">string</span></span> | <span data-ttu-id="d3aea-201">Nie</span><span class="sxs-lookup"><span data-stu-id="d3aea-201">No</span></span> | <span data-ttu-id="d3aea-202">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d3aea-202">The subscription identifier.</span></span> |
| <span data-ttu-id="d3aea-203">parentSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="d3aea-203">parentSubscriptionId</span></span> | <span data-ttu-id="d3aea-204">ciąg</span><span class="sxs-lookup"><span data-stu-id="d3aea-204">string</span></span> | <span data-ttu-id="d3aea-205">Nie</span><span class="sxs-lookup"><span data-stu-id="d3aea-205">No</span></span> | <span data-ttu-id="d3aea-206">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="d3aea-206">Optional.</span></span> <span data-ttu-id="d3aea-207">Identyfikator subskrypcji nadrzędnej w ofercie dodatku.</span><span class="sxs-lookup"><span data-stu-id="d3aea-207">The ID of the parent subscription in an add-on offer.</span></span> <span data-ttu-id="d3aea-208">Dotyczy tylko patch.</span><span class="sxs-lookup"><span data-stu-id="d3aea-208">Applies to PATCH only.</span></span> |
| <span data-ttu-id="d3aea-209">Friendlyname</span><span class="sxs-lookup"><span data-stu-id="d3aea-209">friendlyName</span></span> | <span data-ttu-id="d3aea-210">ciąg</span><span class="sxs-lookup"><span data-stu-id="d3aea-210">string</span></span> | <span data-ttu-id="d3aea-211">Nie</span><span class="sxs-lookup"><span data-stu-id="d3aea-211">No</span></span> | <span data-ttu-id="d3aea-212">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="d3aea-212">Optional.</span></span> <span data-ttu-id="d3aea-213">Przyjazna nazwa subskrypcji zdefiniowanej przez partnera w celu uujednoznania.</span><span class="sxs-lookup"><span data-stu-id="d3aea-213">The friendly name for the subscription defined by the partner to help disambiguate.</span></span> |
| <span data-ttu-id="d3aea-214">quantity</span><span class="sxs-lookup"><span data-stu-id="d3aea-214">quantity</span></span> | <span data-ttu-id="d3aea-215">int</span><span class="sxs-lookup"><span data-stu-id="d3aea-215">int</span></span> | <span data-ttu-id="d3aea-216">Tak</span><span class="sxs-lookup"><span data-stu-id="d3aea-216">Yes</span></span> | <span data-ttu-id="d3aea-217">Liczba licencji dla subskrypcji opartej na licencjach.</span><span class="sxs-lookup"><span data-stu-id="d3aea-217">The number of licenses for a license-based subscription.</span></span> |
| <span data-ttu-id="d3aea-218">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="d3aea-218">partnerIdOnRecord</span></span> | <span data-ttu-id="d3aea-219">ciąg</span><span class="sxs-lookup"><span data-stu-id="d3aea-219">string</span></span> | <span data-ttu-id="d3aea-220">Nie</span><span class="sxs-lookup"><span data-stu-id="d3aea-220">No</span></span> | <span data-ttu-id="d3aea-221">Gdy dostawca pośredni złozy zamówienie w imieniu odsprzedawcy pośredniego, wypełnij to pole identyfikatorem MPN odsprzedawcy pośredniego **(nigdy** nie identyfikatorem dostawcy pośredniego).</span><span class="sxs-lookup"><span data-stu-id="d3aea-221">When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider).</span></span> <span data-ttu-id="d3aea-222">Zapewnia to odpowiednią ewidencjonowanie zachęt.</span><span class="sxs-lookup"><span data-stu-id="d3aea-222">This ensures proper accounting for incentives.</span></span> <span data-ttu-id="d3aea-223">**Nie podaniem identyfikatora MPN odsprzedawcy nie powoduje niepowodzenia zamówienia. Odsprzedawca nie jest jednak zarejestrowany i w związku z tym obliczenia zachęt mogą nie obejmować sprzedaży.**</span><span class="sxs-lookup"><span data-stu-id="d3aea-223">**Failure to provide the reseller MPN ID does not cause the order to fail. However, the reseller isn't recorded and as a consequence incentive calculations may not include the sale.**</span></span> |
| <span data-ttu-id="d3aea-224">atrybuty</span><span class="sxs-lookup"><span data-stu-id="d3aea-224">attributes</span></span> | <span data-ttu-id="d3aea-225">object</span><span class="sxs-lookup"><span data-stu-id="d3aea-225">object</span></span> | <span data-ttu-id="d3aea-226">Nie</span><span class="sxs-lookup"><span data-stu-id="d3aea-226">No</span></span> | <span data-ttu-id="d3aea-227">Zawiera "ObjectType":"OrderLineItem".</span><span class="sxs-lookup"><span data-stu-id="d3aea-227">Contains "ObjectType":"OrderLineItem".</span></span> |

### <a name="request-example"></a><span data-ttu-id="d3aea-228">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="d3aea-228">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 410
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "BillingCycle": "unknown",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "SubscriptionId": null,
            "ParentSubscriptionId": null,
            "FriendlyName": "New offer purchase.",
            "Quantity": 5,
            "PartnerIdOnRecord": "4847383",
            "Attributes": {
                "ObjectType": "OrderLineItem"
            }
        }
    ],
    "CreationDate": null,
    "Attributes": {
        "ObjectType": "Order"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="d3aea-229">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="d3aea-229">REST response</span></span>

<span data-ttu-id="d3aea-230">Jeśli to się powiedzie, treść odpowiedzi zawiera wypełniony [zasób Order.](order-resources.md)</span><span class="sxs-lookup"><span data-stu-id="d3aea-230">If successful, the response body contains the populated [Order](order-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d3aea-231">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d3aea-231">Response success and error codes</span></span>

<span data-ttu-id="d3aea-232">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="d3aea-232">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d3aea-233">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="d3aea-233">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d3aea-234">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d3aea-234">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d3aea-235">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d3aea-235">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 831
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CV: Nd3Oum/L5EywtKQK.0
MS-ServerId: 020021921
Date: Mon, 10 Apr 2017 23:02:24 GMT

{
    "id": "3eddcac6-63b2-4c40-b0b6-f47e18301492",
    "referenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "billingCycle": "monthly",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "subscriptionId": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "friendlyName": "New offer purchase.",
            "quantity": 5,
            "partnerIdOnRecord": "4847383",
            "links": {
                "subscription": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-04-10T16:02:25.983-07:00",
    "links": {
        "self": {
            "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders/3eddcac6-63b2-4c40-b0b6-f47e18301492",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6IjNlZGRjYWM2LTYzYjItNGM0MC1iMGI2LWY0N2UxODMwMTQ5MiIsInZlcnNpb24iOjF9",
        "objectType": "Order"
    }
}
```
