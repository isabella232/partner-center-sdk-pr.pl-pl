---
title: Zakup dodatku do subskrypcji
description: Jak kupić dodatek do istniejącej subskrypcji.
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 975a2516bccdc6274bfec5d6a3286a649fc4f808
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768313"
---
# <a name="purchase-an-add-on-to-a-subscription"></a><span data-ttu-id="ccef9-103">Zakup dodatku do subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ccef9-103">Purchase an add-on to a subscription</span></span>

<span data-ttu-id="ccef9-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="ccef9-104">**Applies To**</span></span>

- <span data-ttu-id="ccef9-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="ccef9-105">Partner Center</span></span>
- <span data-ttu-id="ccef9-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="ccef9-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="ccef9-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ccef9-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ccef9-108">Jak kupić dodatek do istniejącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ccef9-108">How to purchase an add-on to an existing subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ccef9-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ccef9-109">Prerequisites</span></span>

- <span data-ttu-id="ccef9-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ccef9-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ccef9-111">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ccef9-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="ccef9-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ccef9-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ccef9-113">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="ccef9-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ccef9-114">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="ccef9-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ccef9-115">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="ccef9-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ccef9-116">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="ccef9-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ccef9-117">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ccef9-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="ccef9-118">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ccef9-118">A subscription ID.</span></span> <span data-ttu-id="ccef9-119">Jest to istniejąca subskrypcja, dla której ma zostać nabyta oferta dodatku.</span><span class="sxs-lookup"><span data-stu-id="ccef9-119">This is the existing subscription for which to purchase an add-on offer.</span></span>

- <span data-ttu-id="ccef9-120">Identyfikator oferty identyfikujący ofertę dodatku do zakupu.</span><span class="sxs-lookup"><span data-stu-id="ccef9-120">An offer ID that identifies the add-on offer to purchase.</span></span>

## <a name="purchasing-an-add-on-through-code"></a><span data-ttu-id="ccef9-121">Kupowanie dodatku poprzez kod</span><span class="sxs-lookup"><span data-stu-id="ccef9-121">Purchasing an add-on through code</span></span>

<span data-ttu-id="ccef9-122">W przypadku zakupu dodatku do subskrypcji aktualizowana jest oryginalna kolejność subskrypcji z kolejnością dla dodatku.</span><span class="sxs-lookup"><span data-stu-id="ccef9-122">When you purchase an add-on to a subscription you are updating the original subscription order with the order for the add-on.</span></span> <span data-ttu-id="ccef9-123">W poniższym przypadku IDKlienta jest IDENTYFIKATORem klienta, Identyfikator subskrypcji oznacza subskrypcję, a addOnOfferId to identyfikator oferty dla dodatku.</span><span class="sxs-lookup"><span data-stu-id="ccef9-123">In the following, customerId is the customer ID, subscriptionId is the subscription ID, and addOnOfferId is the offer ID for the add-on.</span></span>

<span data-ttu-id="ccef9-124">Oto konkretne kroki:</span><span class="sxs-lookup"><span data-stu-id="ccef9-124">Here are the steps:</span></span>

1.  <span data-ttu-id="ccef9-125">Pobierz interfejs do operacji dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ccef9-125">Get an interface to the operations for the subscription.</span></span>

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  <span data-ttu-id="ccef9-126">Użyj tego interfejsu, aby utworzyć wystąpienie obiektu subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ccef9-126">Use that interface to instantiate a subscription object.</span></span> <span data-ttu-id="ccef9-127">Spowoduje to pobranie szczegółów subskrypcji nadrzędnej, w tym identyfikatora zamówienia.</span><span class="sxs-lookup"><span data-stu-id="ccef9-127">This gets you the parent subscription details, including the order id.</span></span>

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  <span data-ttu-id="ccef9-128">Tworzenie wystąpienia nowego obiektu [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) .</span><span class="sxs-lookup"><span data-stu-id="ccef9-128">Instantiate a new [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object.</span></span> <span data-ttu-id="ccef9-129">To wystąpienie zamówienia służy do aktualizowania oryginalnego zamówienia używanego do zakupu subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ccef9-129">This order instance is used to update the original order used to purchase the subscription.</span></span> <span data-ttu-id="ccef9-130">Dodaj pojedynczy wiersz elementu do kolejności, która reprezentuje dodatek.</span><span class="sxs-lookup"><span data-stu-id="ccef9-130">Add a single line item to the order that represents the add-on.</span></span>
    ``` csharp
    var orderToUpdate = new Order()
    {
        ReferenceCustomerId = customerId,
        LineItems = new List<OrderLineItem>()
        {
            new OrderLineItem()
            {
                LineItemNumber = 0,
                OfferId = addOnOfferId,
                FriendlyName = "Some friendly name",
                Quantity = 2,
                ParentSubscriptionId = subscriptionId
            }
        }
    };
    ```

4.  <span data-ttu-id="ccef9-131">Zaktualizuj oryginalne zamówienie dla subskrypcji za pomocą nowej kolejności dla dodatku.</span><span class="sxs-lookup"><span data-stu-id="ccef9-131">Update the original order for the subscription with the new order for the add-on.</span></span>
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a><span data-ttu-id="ccef9-132">C\#</span><span class="sxs-lookup"><span data-stu-id="ccef9-132">C\#</span></span>

<span data-ttu-id="ccef9-133">Aby kupić dodatek, Zacznij od uzyskania interfejsu do operacji subskrypcji przez wywołanie metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta i metodę [**Subscription. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) , aby zidentyfikować subskrypcję z ofertą dodatku.</span><span class="sxs-lookup"><span data-stu-id="ccef9-133">To purchase an add-on, begin by obtaining an interface to the subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the subscription that has the add-on offer.</span></span> <span data-ttu-id="ccef9-134">Użyj tego [**interfejsu**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) , aby pobrać szczegóły subskrypcji przez wywołanie metody [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span><span class="sxs-lookup"><span data-stu-id="ccef9-134">Use that [**interface**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) to retrieve the subscription details by calling [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span></span> <span data-ttu-id="ccef9-135">Dlaczego są potrzebne szczegóły subskrypcji?</span><span class="sxs-lookup"><span data-stu-id="ccef9-135">Why do you need the subscription details?</span></span> <span data-ttu-id="ccef9-136">Ponieważ potrzebujesz identyfikatora zamówienia w kolejności subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ccef9-136">Because you need the order id of the subscription order.</span></span> <span data-ttu-id="ccef9-137">Jest to zamówienie, które ma zostać zaktualizowane przy użyciu dodatku.</span><span class="sxs-lookup"><span data-stu-id="ccef9-137">That's the order to be updated with the add-on.</span></span>

<span data-ttu-id="ccef9-138">Następnie Utwórz wystąpienie nowego obiektu [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) i wypełnij je pojedynczym wystąpieniem [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) zawierającym informacje umożliwiające zidentyfikowanie dodatku, jak pokazano w poniższym fragmencie kodu.</span><span class="sxs-lookup"><span data-stu-id="ccef9-138">Next, instantiate a new [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and populate it with a single [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) instance that contains the information to identify the add-on, as shown in the following code snippet.</span></span> <span data-ttu-id="ccef9-139">Ten nowy obiekt zostanie użyty do zaktualizowania zamówienia subskrypcji z dodatkiem.</span><span class="sxs-lookup"><span data-stu-id="ccef9-139">You'll use this new object to update the subscription order with the add-on.</span></span> <span data-ttu-id="ccef9-140">Na koniec Wywołaj metodę [**patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) , aby zaktualizować kolejność subskrypcji, po pierwszym zidentyfikowaniu klienta z [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) i Order with [**Orders. ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).</span><span class="sxs-lookup"><span data-stu-id="ccef9-140">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) method to update the subscription order, after first identifying the customer with [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) and the order with [**Orders.ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;
// string addOnOfferId;

// Get an interface to the operations for the subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the parent subscription details.
var parentSubscription = subscriptionOperations.Get();

// In order to buy an add-on subscription for this offer, we need to patch/update the order through which the base offer was purchased
// by creating an order object with a single line item which represents the add-on offer purchase.
var orderToUpdate = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = addOnOfferId,
            FriendlyName = "Some friendly name",
            Quantity = 2,
            ParentSubscriptionId = subscriptionId
        }
    }
};

// Update the order to apply the add on purchase.
Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
```

<span data-ttu-id="ccef9-141">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="ccef9-141">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="ccef9-142">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: AddSubscriptionAddOn.cs</span><span class="sxs-lookup"><span data-stu-id="ccef9-142">**Project**: Partner Center SDK Samples **Class**: AddSubscriptionAddOn.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="ccef9-143">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="ccef9-143">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ccef9-144">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="ccef9-144">Request syntax</span></span>

| <span data-ttu-id="ccef9-145">Metoda</span><span class="sxs-lookup"><span data-stu-id="ccef9-145">Method</span></span>    | <span data-ttu-id="ccef9-146">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="ccef9-146">Request URI</span></span>                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ccef9-147">**WYSŁANA**</span><span class="sxs-lookup"><span data-stu-id="ccef9-147">**PATCH**</span></span> | <span data-ttu-id="ccef9-148">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="ccef9-148">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="ccef9-149">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="ccef9-149">URI parameters</span></span>

<span data-ttu-id="ccef9-150">Aby zidentyfikować klienta i zamówienie, użyj następujących parametrów.</span><span class="sxs-lookup"><span data-stu-id="ccef9-150">Use the following parameters to identify the customer and order.</span></span>

| <span data-ttu-id="ccef9-151">Nazwa</span><span class="sxs-lookup"><span data-stu-id="ccef9-151">Name</span></span>                   | <span data-ttu-id="ccef9-152">Typ</span><span class="sxs-lookup"><span data-stu-id="ccef9-152">Type</span></span>     | <span data-ttu-id="ccef9-153">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ccef9-153">Required</span></span> | <span data-ttu-id="ccef9-154">Opis</span><span class="sxs-lookup"><span data-stu-id="ccef9-154">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="ccef9-155">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="ccef9-155">**customer-tenant-id**</span></span> | <span data-ttu-id="ccef9-156">**guid**</span><span class="sxs-lookup"><span data-stu-id="ccef9-156">**guid**</span></span> | <span data-ttu-id="ccef9-157">Y</span><span class="sxs-lookup"><span data-stu-id="ccef9-157">Y</span></span>        | <span data-ttu-id="ccef9-158">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="ccef9-158">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |
| <span data-ttu-id="ccef9-159">**Identyfikator zamówienia**</span><span class="sxs-lookup"><span data-stu-id="ccef9-159">**order-id**</span></span>           | <span data-ttu-id="ccef9-160">**guid**</span><span class="sxs-lookup"><span data-stu-id="ccef9-160">**guid**</span></span> | <span data-ttu-id="ccef9-161">Y</span><span class="sxs-lookup"><span data-stu-id="ccef9-161">Y</span></span>        | <span data-ttu-id="ccef9-162">Identyfikator zamówienia.</span><span class="sxs-lookup"><span data-stu-id="ccef9-162">The order identifier.</span></span>                                                              |

### <a name="request-headers"></a><span data-ttu-id="ccef9-163">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="ccef9-163">Request headers</span></span>

<span data-ttu-id="ccef9-164">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ccef9-164">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ccef9-165">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="ccef9-165">Request body</span></span>

<span data-ttu-id="ccef9-166">W poniższych tabelach opisano właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="ccef9-166">The following tables describe the properties in the request body.</span></span>

## <a name="order"></a><span data-ttu-id="ccef9-167">Zamówienie</span><span class="sxs-lookup"><span data-stu-id="ccef9-167">Order</span></span>

| <span data-ttu-id="ccef9-168">Nazwa</span><span class="sxs-lookup"><span data-stu-id="ccef9-168">Name</span></span>                | <span data-ttu-id="ccef9-169">Typ</span><span class="sxs-lookup"><span data-stu-id="ccef9-169">Type</span></span>             | <span data-ttu-id="ccef9-170">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ccef9-170">Required</span></span> | <span data-ttu-id="ccef9-171">Opis</span><span class="sxs-lookup"><span data-stu-id="ccef9-171">Description</span></span>                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| <span data-ttu-id="ccef9-172">Id</span><span class="sxs-lookup"><span data-stu-id="ccef9-172">Id</span></span>                  | <span data-ttu-id="ccef9-173">ciąg</span><span class="sxs-lookup"><span data-stu-id="ccef9-173">string</span></span>           | <span data-ttu-id="ccef9-174">N</span><span class="sxs-lookup"><span data-stu-id="ccef9-174">N</span></span>        | <span data-ttu-id="ccef9-175">Identyfikator zamówienia.</span><span class="sxs-lookup"><span data-stu-id="ccef9-175">The order ID.</span></span>                                        |
| <span data-ttu-id="ccef9-176">ReferenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="ccef9-176">ReferenceCustomerId</span></span> | <span data-ttu-id="ccef9-177">ciąg</span><span class="sxs-lookup"><span data-stu-id="ccef9-177">string</span></span>           | <span data-ttu-id="ccef9-178">Y</span><span class="sxs-lookup"><span data-stu-id="ccef9-178">Y</span></span>        | <span data-ttu-id="ccef9-179">Identyfikator klienta.</span><span class="sxs-lookup"><span data-stu-id="ccef9-179">The customer ID.</span></span>                                     |
| <span data-ttu-id="ccef9-180">LineItems</span><span class="sxs-lookup"><span data-stu-id="ccef9-180">LineItems</span></span>           | <span data-ttu-id="ccef9-181">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="ccef9-181">array of objects</span></span> | <span data-ttu-id="ccef9-182">Y</span><span class="sxs-lookup"><span data-stu-id="ccef9-182">Y</span></span>        | <span data-ttu-id="ccef9-183">Tablica obiektów [OrderLineItem](#orderlineitem) .</span><span class="sxs-lookup"><span data-stu-id="ccef9-183">An array of [OrderLineItem](#orderlineitem) objects.</span></span> |
| <span data-ttu-id="ccef9-184">CreationDate</span><span class="sxs-lookup"><span data-stu-id="ccef9-184">CreationDate</span></span>        | <span data-ttu-id="ccef9-185">ciąg</span><span class="sxs-lookup"><span data-stu-id="ccef9-185">string</span></span>           | <span data-ttu-id="ccef9-186">N</span><span class="sxs-lookup"><span data-stu-id="ccef9-186">N</span></span>        | <span data-ttu-id="ccef9-187">Data, w której zamówienie zostało utworzone, w formacie daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="ccef9-187">The date the order was created, in date-time format.</span></span> |
| <span data-ttu-id="ccef9-188">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="ccef9-188">Attributes</span></span>          | <span data-ttu-id="ccef9-189">object</span><span class="sxs-lookup"><span data-stu-id="ccef9-189">object</span></span>           | <span data-ttu-id="ccef9-190">N</span><span class="sxs-lookup"><span data-stu-id="ccef9-190">N</span></span>        | <span data-ttu-id="ccef9-191">Zawiera "ObjectType": "Order".</span><span class="sxs-lookup"><span data-stu-id="ccef9-191">Contains "ObjectType": "Order".</span></span>                      |

## <a name="orderlineitem"></a><span data-ttu-id="ccef9-192">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="ccef9-192">OrderLineItem</span></span>

| <span data-ttu-id="ccef9-193">Nazwa</span><span class="sxs-lookup"><span data-stu-id="ccef9-193">Name</span></span>                 | <span data-ttu-id="ccef9-194">Typ</span><span class="sxs-lookup"><span data-stu-id="ccef9-194">Type</span></span>   | <span data-ttu-id="ccef9-195">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ccef9-195">Required</span></span> | <span data-ttu-id="ccef9-196">Opis</span><span class="sxs-lookup"><span data-stu-id="ccef9-196">Description</span></span>                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="ccef9-197">LineItemNumber</span><span class="sxs-lookup"><span data-stu-id="ccef9-197">LineItemNumber</span></span>       | <span data-ttu-id="ccef9-198">liczba</span><span class="sxs-lookup"><span data-stu-id="ccef9-198">number</span></span> | <span data-ttu-id="ccef9-199">Y</span><span class="sxs-lookup"><span data-stu-id="ccef9-199">Y</span></span>        | <span data-ttu-id="ccef9-200">Numer elementu wiersza, zaczynając od 0.</span><span class="sxs-lookup"><span data-stu-id="ccef9-200">The line item number, starting with 0.</span></span>                       |
| <span data-ttu-id="ccef9-201">OfferId</span><span class="sxs-lookup"><span data-stu-id="ccef9-201">OfferId</span></span>              | <span data-ttu-id="ccef9-202">ciąg</span><span class="sxs-lookup"><span data-stu-id="ccef9-202">string</span></span> | <span data-ttu-id="ccef9-203">Y</span><span class="sxs-lookup"><span data-stu-id="ccef9-203">Y</span></span>        | <span data-ttu-id="ccef9-204">Identyfikator oferty dodatku.</span><span class="sxs-lookup"><span data-stu-id="ccef9-204">The offer ID of the add-on.</span></span>                                  |
| <span data-ttu-id="ccef9-205">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="ccef9-205">SubscriptionId</span></span>       | <span data-ttu-id="ccef9-206">ciąg</span><span class="sxs-lookup"><span data-stu-id="ccef9-206">string</span></span> | <span data-ttu-id="ccef9-207">N</span><span class="sxs-lookup"><span data-stu-id="ccef9-207">N</span></span>        | <span data-ttu-id="ccef9-208">Identyfikator zakupionej subskrypcji dodatku.</span><span class="sxs-lookup"><span data-stu-id="ccef9-208">The ID of the add-on subscription purchased.</span></span>                 |
| <span data-ttu-id="ccef9-209">ParentSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="ccef9-209">ParentSubscriptionId</span></span> | <span data-ttu-id="ccef9-210">ciąg</span><span class="sxs-lookup"><span data-stu-id="ccef9-210">string</span></span> | <span data-ttu-id="ccef9-211">Y</span><span class="sxs-lookup"><span data-stu-id="ccef9-211">Y</span></span>        | <span data-ttu-id="ccef9-212">Identyfikator subskrypcji nadrzędnej z ofertą dodatku.</span><span class="sxs-lookup"><span data-stu-id="ccef9-212">The ID of the parent subscription that has the add-on offer.</span></span> |
| <span data-ttu-id="ccef9-213">FriendlyName</span><span class="sxs-lookup"><span data-stu-id="ccef9-213">FriendlyName</span></span>         | <span data-ttu-id="ccef9-214">ciąg</span><span class="sxs-lookup"><span data-stu-id="ccef9-214">string</span></span> | <span data-ttu-id="ccef9-215">N</span><span class="sxs-lookup"><span data-stu-id="ccef9-215">N</span></span>        | <span data-ttu-id="ccef9-216">Przyjazna nazwa dla tego elementu wiersza.</span><span class="sxs-lookup"><span data-stu-id="ccef9-216">The friendly name for this line item.</span></span>                        |
| <span data-ttu-id="ccef9-217">Ilość</span><span class="sxs-lookup"><span data-stu-id="ccef9-217">Quantity</span></span>             | <span data-ttu-id="ccef9-218">liczba</span><span class="sxs-lookup"><span data-stu-id="ccef9-218">number</span></span> | <span data-ttu-id="ccef9-219">Y</span><span class="sxs-lookup"><span data-stu-id="ccef9-219">Y</span></span>        | <span data-ttu-id="ccef9-220">Liczba licencji.</span><span class="sxs-lookup"><span data-stu-id="ccef9-220">The number of licenses.</span></span>                                      |
| <span data-ttu-id="ccef9-221">PartnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="ccef9-221">PartnerIdOnRecord</span></span>    | <span data-ttu-id="ccef9-222">ciąg</span><span class="sxs-lookup"><span data-stu-id="ccef9-222">string</span></span> | <span data-ttu-id="ccef9-223">N</span><span class="sxs-lookup"><span data-stu-id="ccef9-223">N</span></span>        | <span data-ttu-id="ccef9-224">IDENTYFIKATOR MPN partnera rekordu.</span><span class="sxs-lookup"><span data-stu-id="ccef9-224">The MPN ID of the partner of record.</span></span>                         |
| <span data-ttu-id="ccef9-225">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="ccef9-225">Attributes</span></span>           | <span data-ttu-id="ccef9-226">object</span><span class="sxs-lookup"><span data-stu-id="ccef9-226">object</span></span> | <span data-ttu-id="ccef9-227">N</span><span class="sxs-lookup"><span data-stu-id="ccef9-227">N</span></span>        | <span data-ttu-id="ccef9-228">Zawiera "ObjectType": "OrderLineItem".</span><span class="sxs-lookup"><span data-stu-id="ccef9-228">Contains "ObjectType": "OrderLineItem".</span></span>                      |

### <a name="request-example"></a><span data-ttu-id="ccef9-229">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="ccef9-229">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/CF3B0E37-BE0B-4CDD-B584-D1A97D98A922 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 414
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": null,
            "ParentSubscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "FriendlyName": "Some friendly name",
            "Quantity": 2,
            "PartnerIdOnRecord": null,
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

## <a name="rest-response"></a><span data-ttu-id="ccef9-230">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="ccef9-230">REST response</span></span>

<span data-ttu-id="ccef9-231">Jeśli to się powiedzie, ta metoda zwraca zaktualizowany porządek subskrypcji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ccef9-231">If successful, this method returns the updated subscription order in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ccef9-232">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ccef9-232">Response success and error codes</span></span>

<span data-ttu-id="ccef9-233">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="ccef9-233">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ccef9-234">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="ccef9-234">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ccef9-235">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ccef9-235">For the full list, see [Partner Center Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ccef9-236">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ccef9-236">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1135
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CV: WtFy3zI8V0u2lnT9.0
MS-ServerId: 020021921
Date: Wed, 25 Jan 2017 23:01:08 GMT

{
    "id": "cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
    "referenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "billingCycle": "none",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "195416C1-3447-423A-B37B-EE59A99A19C4",
            "subscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
                    "method": "GET",
                    "headers": []
                }
            }
        }, {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "968BA1CF-C146-4ADF-A300-308DCF718EEE",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/968BA1CF-C146-4ADF-A300-308DCF718EEE",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-01-25T14:53:12.093-08:00",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6ImNmM2IwZTM3LWJlMGItNGNkZC1iNTg0LWQxYTk3ZDk4YTkyMiIsInZlcnNpb24iOjJ9",
        "objectType": "Order"
    }
}
```
