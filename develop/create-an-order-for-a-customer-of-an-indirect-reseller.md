---
title: Utwórz zamówienie klienta na potrzeby pośredniego odsprzedawcy
description: Dowiedz się, jak za pomocą interfejsów API usługi Partner Center utworzyć zamówienie dla klienta pośredniego odsprzedawcy. Artykuł zawiera wymagania wstępne, kroki i Exmaples.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f72ecec8d82e6b8a1bc53c277206cafd7d8a4e03
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770155"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a><span data-ttu-id="4f4f8-104">Utwórz zamówienie dla klienta odsprzedawcy pośredniego</span><span class="sxs-lookup"><span data-stu-id="4f4f8-104">Create an order for a customer of an indirect reseller</span></span>

<span data-ttu-id="4f4f8-105">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="4f4f8-105">**Applies to:**</span></span>

- <span data-ttu-id="4f4f8-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="4f4f8-106">Partner Center</span></span>

<span data-ttu-id="4f4f8-107">Jak utworzyć zamówienie dla klienta pośredniego odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-107">How to create an order for a customer of an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f4f8-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4f4f8-108">Prerequisites</span></span>

- <span data-ttu-id="4f4f8-109">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4f4f8-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4f4f8-110">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="4f4f8-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4f4f8-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4f4f8-112">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4f4f8-113">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4f4f8-114">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4f4f8-115">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="4f4f8-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4f4f8-116">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4f4f8-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="4f4f8-117">Identyfikator oferty elementu do zakupu.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-117">The offer identifier of the item to purchase.</span></span>

- <span data-ttu-id="4f4f8-118">Identyfikator dzierżawy pośredniego odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-118">The tenant identifier of the indirect reseller.</span></span>

## <a name="c"></a><span data-ttu-id="4f4f8-119">C\#</span><span class="sxs-lookup"><span data-stu-id="4f4f8-119">C\#</span></span>

<span data-ttu-id="4f4f8-120">Aby utworzyć zamówienie dla klienta pośredniego odsprzedawcy:</span><span class="sxs-lookup"><span data-stu-id="4f4f8-120">To create an order for a customer of an indirect reseller:</span></span>

1. <span data-ttu-id="4f4f8-121">Pobierz kolekcję pośrednich odsprzedawcaów, które mają relację z zalogowanym partnerem.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-121">Get a collection of the indirect resellers that have a relationship with the signed-in partner.</span></span>

2. <span data-ttu-id="4f4f8-122">Pobierz zmienną lokalną do elementu w kolekcji, który jest zgodny z IDENTYFIKATORem pośredniego odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-122">Get a local variable to the item in the collection that matches the indirect reseller ID.</span></span> <span data-ttu-id="4f4f8-123">Ten krok pozwala uzyskać dostęp do właściwości [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) odsprzedawcy podczas tworzenia zamówienia.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-123">This step helps you access the reseller's [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) property when you create the order.</span></span>

3. <span data-ttu-id="4f4f8-124">Utwórz wystąpienie obiektu [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) i ustaw właściwość [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) na identyfikator klienta, aby zarejestrować klienta.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-124">Instantiate an [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and set the [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) property to the customer identifier in order to record the customer.</span></span>

4. <span data-ttu-id="4f4f8-125">Utwórz listę obiektów [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) i przypisz listę do właściwości [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) zamówienia.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-125">Create a list of [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) objects, and assign the list to the order's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) property.</span></span> <span data-ttu-id="4f4f8-126">Każdy element wiersza zamówienia zawiera informacje o zakupie dla jednej oferty.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-126">Each order line item contains the purchase information for one offer.</span></span> <span data-ttu-id="4f4f8-127">Upewnij się, że właściwość [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) w każdym wierszu jest WYpełniona IDENTYFIKATORem MPN pośredniego odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-127">Be sure to populate the [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) property in each line item with the MPN ID of the indirect reseller.</span></span> <span data-ttu-id="4f4f8-128">Musisz mieć co najmniej jeden element wiersza zamówienia.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-128">You must have at least one order line item.</span></span>

5. <span data-ttu-id="4f4f8-129">Uzyskaj interfejs do porządkowania operacji, wywołując metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta, a następnie pobrać interfejs z właściwości [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) .</span><span class="sxs-lookup"><span data-stu-id="4f4f8-129">Obtain an interface to order operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieve the interface from the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.</span></span>

6. <span data-ttu-id="4f4f8-130">Wywołaj metodę [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) lub [**onasync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) , aby utworzyć zamówienie.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-130">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method to create the order.</span></span>

### <a name="c-example"></a><span data-ttu-id="4f4f8-131">\#Przykład C</span><span class="sxs-lookup"><span data-stu-id="4f4f8-131">C\# example</span></span>

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

<span data-ttu-id="4f4f8-132">**Przykład**:**projekt** [aplikacji testowej konsoli](console-test-app.md): **Klasa** przykładów zestawu SDK Centrum partnerskiego: PlaceOrderForCustomer.cs</span><span class="sxs-lookup"><span data-stu-id="4f4f8-132">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: PlaceOrderForCustomer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="4f4f8-133">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="4f4f8-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4f4f8-134">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="4f4f8-134">Request syntax</span></span>

| <span data-ttu-id="4f4f8-135">Metoda</span><span class="sxs-lookup"><span data-stu-id="4f4f8-135">Method</span></span>   | <span data-ttu-id="4f4f8-136">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="4f4f8-136">Request URI</span></span>                                                                            |
|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="4f4f8-137">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="4f4f8-137">**POST**</span></span> | <span data-ttu-id="4f4f8-138">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/Orders http/1.1</span><span class="sxs-lookup"><span data-stu-id="4f4f8-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="4f4f8-139">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="4f4f8-139">URI parameters</span></span>

<span data-ttu-id="4f4f8-140">Użyj następującego parametru ścieżki, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-140">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="4f4f8-141">Nazwa</span><span class="sxs-lookup"><span data-stu-id="4f4f8-141">Name</span></span>        | <span data-ttu-id="4f4f8-142">Typ</span><span class="sxs-lookup"><span data-stu-id="4f4f8-142">Type</span></span>   | <span data-ttu-id="4f4f8-143">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4f4f8-143">Required</span></span> | <span data-ttu-id="4f4f8-144">Opis</span><span class="sxs-lookup"><span data-stu-id="4f4f8-144">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="4f4f8-145">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="4f4f8-145">customer-id</span></span> | <span data-ttu-id="4f4f8-146">ciąg</span><span class="sxs-lookup"><span data-stu-id="4f4f8-146">string</span></span> | <span data-ttu-id="4f4f8-147">Tak</span><span class="sxs-lookup"><span data-stu-id="4f4f8-147">Yes</span></span>      | <span data-ttu-id="4f4f8-148">Ciąg w formacie GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-148">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4f4f8-149">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="4f4f8-149">Request headers</span></span>

<span data-ttu-id="4f4f8-150">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4f4f8-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4f4f8-151">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="4f4f8-151">Request body</span></span>

#### <a name="order"></a><span data-ttu-id="4f4f8-152">Zamówienie</span><span class="sxs-lookup"><span data-stu-id="4f4f8-152">Order</span></span>

<span data-ttu-id="4f4f8-153">W tej tabeli opisano właściwości **zamówienia** w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-153">This table describes the **Order** properties in the request body.</span></span>

| <span data-ttu-id="4f4f8-154">Nazwa</span><span class="sxs-lookup"><span data-stu-id="4f4f8-154">Name</span></span> | <span data-ttu-id="4f4f8-155">Typ</span><span class="sxs-lookup"><span data-stu-id="4f4f8-155">Type</span></span> | <span data-ttu-id="4f4f8-156">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4f4f8-156">Required</span></span> | <span data-ttu-id="4f4f8-157">Opis</span><span class="sxs-lookup"><span data-stu-id="4f4f8-157">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="4f4f8-158">identyfikator</span><span class="sxs-lookup"><span data-stu-id="4f4f8-158">id</span></span> | <span data-ttu-id="4f4f8-159">ciąg</span><span class="sxs-lookup"><span data-stu-id="4f4f8-159">string</span></span> | <span data-ttu-id="4f4f8-160">Nie</span><span class="sxs-lookup"><span data-stu-id="4f4f8-160">No</span></span> | <span data-ttu-id="4f4f8-161">Identyfikator zamówienia, który jest dostarczany po pomyślnym utworzeniu zamówienia.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-161">An order identifier that is supplied upon successful creation of the order.</span></span> |
| <span data-ttu-id="4f4f8-162">referenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="4f4f8-162">referenceCustomerId</span></span> | <span data-ttu-id="4f4f8-163">ciąg</span><span class="sxs-lookup"><span data-stu-id="4f4f8-163">string</span></span> | <span data-ttu-id="4f4f8-164">Tak</span><span class="sxs-lookup"><span data-stu-id="4f4f8-164">Yes</span></span> | <span data-ttu-id="4f4f8-165">Identyfikator klienta.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-165">The customer identifier.</span></span> |
| <span data-ttu-id="4f4f8-166">billingCycle</span><span class="sxs-lookup"><span data-stu-id="4f4f8-166">billingCycle</span></span> | <span data-ttu-id="4f4f8-167">ciąg</span><span class="sxs-lookup"><span data-stu-id="4f4f8-167">string</span></span> | <span data-ttu-id="4f4f8-168">Nie</span><span class="sxs-lookup"><span data-stu-id="4f4f8-168">No</span></span> | <span data-ttu-id="4f4f8-169">Częstotliwość, z jaką jest rozliczany partner dla tego zamówienia.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-169">The frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="4f4f8-170">Wartość domyślna to &quot; miesiąc &quot; i jest stosowana po pomyślnym utworzeniu zamówienia.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-170">The default is &quot;Monthly&quot; and is applied upon successful creation of the order.</span></span> <span data-ttu-id="4f4f8-171">Obsługiwane wartości to nazwy elementów członkowskich Znalezione w [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="4f4f8-171">Supported values are the member names found in [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype).</span></span> <span data-ttu-id="4f4f8-172">Uwaga: funkcja rocznego rozliczania nie jest jeszcze ogólnie dostępna.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-172">Note: the annual billing feature isn't yet generally available.</span></span> <span data-ttu-id="4f4f8-173">Pomoc techniczna dotycząca rozliczeń rocznych jest dostępna wkrótce.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-173">Support for annual billing is coming soon.</span></span> |
| <span data-ttu-id="4f4f8-174">lineItems</span><span class="sxs-lookup"><span data-stu-id="4f4f8-174">lineItems</span></span> | <span data-ttu-id="4f4f8-175">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="4f4f8-175">array of objects</span></span> | <span data-ttu-id="4f4f8-176">Tak</span><span class="sxs-lookup"><span data-stu-id="4f4f8-176">Yes</span></span> | <span data-ttu-id="4f4f8-177">Tablica zasobów [**OrderLineItem**](#orderlineitem) .</span><span class="sxs-lookup"><span data-stu-id="4f4f8-177">An array of [**OrderLineItem**](#orderlineitem) resources.</span></span> |
| <span data-ttu-id="4f4f8-178">creationDate</span><span class="sxs-lookup"><span data-stu-id="4f4f8-178">creationDate</span></span> | <span data-ttu-id="4f4f8-179">ciąg</span><span class="sxs-lookup"><span data-stu-id="4f4f8-179">string</span></span> | <span data-ttu-id="4f4f8-180">Nie</span><span class="sxs-lookup"><span data-stu-id="4f4f8-180">No</span></span> | <span data-ttu-id="4f4f8-181">Data, w której zamówienie zostało utworzone, w formacie daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-181">The date the order was created, in date-time format.</span></span> <span data-ttu-id="4f4f8-182">Stosowane po pomyślnym utworzeniu zamówienia.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-182">Applied upon successful creation of the order.</span></span> |
| <span data-ttu-id="4f4f8-183">atrybuty</span><span class="sxs-lookup"><span data-stu-id="4f4f8-183">attributes</span></span> | <span data-ttu-id="4f4f8-184">object</span><span class="sxs-lookup"><span data-stu-id="4f4f8-184">object</span></span> | <span data-ttu-id="4f4f8-185">Nie</span><span class="sxs-lookup"><span data-stu-id="4f4f8-185">No</span></span> | <span data-ttu-id="4f4f8-186">Zawiera "ObjectType": "Order".</span><span class="sxs-lookup"><span data-stu-id="4f4f8-186">Contains "ObjectType": "Order".</span></span> |

#### <a name="orderlineitem"></a><span data-ttu-id="4f4f8-187">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="4f4f8-187">OrderLineItem</span></span>

<span data-ttu-id="4f4f8-188">W tej tabeli opisano właściwości **OrderLineItem** w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-188">This table describes the **OrderLineItem** properties in the request body.</span></span>

| <span data-ttu-id="4f4f8-189">Nazwa</span><span class="sxs-lookup"><span data-stu-id="4f4f8-189">Name</span></span> | <span data-ttu-id="4f4f8-190">Typ</span><span class="sxs-lookup"><span data-stu-id="4f4f8-190">Type</span></span> | <span data-ttu-id="4f4f8-191">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4f4f8-191">Required</span></span> | <span data-ttu-id="4f4f8-192">Opis</span><span class="sxs-lookup"><span data-stu-id="4f4f8-192">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="4f4f8-193">lineItemNumber</span><span class="sxs-lookup"><span data-stu-id="4f4f8-193">lineItemNumber</span></span> | <span data-ttu-id="4f4f8-194">int</span><span class="sxs-lookup"><span data-stu-id="4f4f8-194">int</span></span> | <span data-ttu-id="4f4f8-195">Tak</span><span class="sxs-lookup"><span data-stu-id="4f4f8-195">Yes</span></span> | <span data-ttu-id="4f4f8-196">Każdy element wiersza w kolekcji pobiera unikatowy numer wiersza, licząc do wartości z przedziału od 0 do count-1.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-196">Each line item in the collection gets a unique line number, counting up from 0 to count-1.</span></span> |
| <span data-ttu-id="4f4f8-197">offerId</span><span class="sxs-lookup"><span data-stu-id="4f4f8-197">offerId</span></span> | <span data-ttu-id="4f4f8-198">ciąg</span><span class="sxs-lookup"><span data-stu-id="4f4f8-198">string</span></span> | <span data-ttu-id="4f4f8-199">Tak</span><span class="sxs-lookup"><span data-stu-id="4f4f8-199">Yes</span></span> | <span data-ttu-id="4f4f8-200">Identyfikator oferty.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-200">The offer identifier.</span></span> |
| <span data-ttu-id="4f4f8-201">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="4f4f8-201">subscriptionId</span></span> | <span data-ttu-id="4f4f8-202">ciąg</span><span class="sxs-lookup"><span data-stu-id="4f4f8-202">string</span></span> | <span data-ttu-id="4f4f8-203">Nie</span><span class="sxs-lookup"><span data-stu-id="4f4f8-203">No</span></span> | <span data-ttu-id="4f4f8-204">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-204">The subscription identifier.</span></span> |
| <span data-ttu-id="4f4f8-205">parentSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="4f4f8-205">parentSubscriptionId</span></span> | <span data-ttu-id="4f4f8-206">ciąg</span><span class="sxs-lookup"><span data-stu-id="4f4f8-206">string</span></span> | <span data-ttu-id="4f4f8-207">Nie</span><span class="sxs-lookup"><span data-stu-id="4f4f8-207">No</span></span> | <span data-ttu-id="4f4f8-208">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-208">Optional.</span></span> <span data-ttu-id="4f4f8-209">Identyfikator subskrypcji nadrzędnej w ofercie dodatku.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-209">The ID of the parent subscription in an add-on offer.</span></span> <span data-ttu-id="4f4f8-210">Dotyczy tylko poprawki.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-210">Applies to PATCH only.</span></span> |
| <span data-ttu-id="4f4f8-211">friendlyName</span><span class="sxs-lookup"><span data-stu-id="4f4f8-211">friendlyName</span></span> | <span data-ttu-id="4f4f8-212">ciąg</span><span class="sxs-lookup"><span data-stu-id="4f4f8-212">string</span></span> | <span data-ttu-id="4f4f8-213">Nie</span><span class="sxs-lookup"><span data-stu-id="4f4f8-213">No</span></span> | <span data-ttu-id="4f4f8-214">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-214">Optional.</span></span> <span data-ttu-id="4f4f8-215">Przyjazna nazwa dla subskrypcji zdefiniowanej przez partnera, która pomaga w odróżnieniu od siebie.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-215">The friendly name for the subscription defined by the partner to help disambiguate.</span></span> |
| <span data-ttu-id="4f4f8-216">quantity</span><span class="sxs-lookup"><span data-stu-id="4f4f8-216">quantity</span></span> | <span data-ttu-id="4f4f8-217">int</span><span class="sxs-lookup"><span data-stu-id="4f4f8-217">int</span></span> | <span data-ttu-id="4f4f8-218">Tak</span><span class="sxs-lookup"><span data-stu-id="4f4f8-218">Yes</span></span> | <span data-ttu-id="4f4f8-219">Liczba licencji dla subskrypcji opartej na licencji.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-219">The number of licenses for a license-based subscription.</span></span> |
| <span data-ttu-id="4f4f8-220">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="4f4f8-220">partnerIdOnRecord</span></span> | <span data-ttu-id="4f4f8-221">ciąg</span><span class="sxs-lookup"><span data-stu-id="4f4f8-221">string</span></span> | <span data-ttu-id="4f4f8-222">Nie</span><span class="sxs-lookup"><span data-stu-id="4f4f8-222">No</span></span> | <span data-ttu-id="4f4f8-223">Gdy Dostawca pośredni umieści zamówienie w imieniu pośredniego odsprzedawcy, Wypełnij to pole IDENTYFIKATORem MPN **pośredniego odsprzedawcy** (nigdy nie jest identyfikatorem dostawcy pośredniego).</span><span class="sxs-lookup"><span data-stu-id="4f4f8-223">When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider).</span></span> <span data-ttu-id="4f4f8-224">Zapewnia to odpowiednie Księgowanie zachęt.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-224">This ensures proper accounting for incentives.</span></span> <span data-ttu-id="4f4f8-225">**Niedostarczenie identyfikatora MPN odsprzedawcy nie powoduje błędu zamówienia. Jednak odsprzedawca nie jest zarejestrowany i w związku z tym, że obliczenia bodźce mogą nie uwzględniać sprzedaży.**</span><span class="sxs-lookup"><span data-stu-id="4f4f8-225">**Failure to provide the reseller MPN ID does not cause the order to fail. However, the reseller isn't recorded and as a consequence incentive calculations may not include the sale.**</span></span> |
| <span data-ttu-id="4f4f8-226">atrybuty</span><span class="sxs-lookup"><span data-stu-id="4f4f8-226">attributes</span></span> | <span data-ttu-id="4f4f8-227">object</span><span class="sxs-lookup"><span data-stu-id="4f4f8-227">object</span></span> | <span data-ttu-id="4f4f8-228">Nie</span><span class="sxs-lookup"><span data-stu-id="4f4f8-228">No</span></span> | <span data-ttu-id="4f4f8-229">Zawiera "ObjectType": "OrderLineItem".</span><span class="sxs-lookup"><span data-stu-id="4f4f8-229">Contains "ObjectType":"OrderLineItem".</span></span> |

### <a name="request-example"></a><span data-ttu-id="4f4f8-230">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="4f4f8-230">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="4f4f8-231">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="4f4f8-231">REST response</span></span>

<span data-ttu-id="4f4f8-232">Jeśli to się powiedzie, treść odpowiedzi zawiera zapełnione [zamówione](order-resources.md) zasoby.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-232">If successful, the response body contains the populated [Order](order-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4f4f8-233">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4f4f8-233">Response success and error codes</span></span>

<span data-ttu-id="4f4f8-234">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-234">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4f4f8-235">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="4f4f8-235">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4f4f8-236">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4f4f8-236">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4f4f8-237">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4f4f8-237">Response example</span></span>

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
