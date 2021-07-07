---
title: Zakup dodatku do subskrypcji
description: Jak kupić dodatek do istniejącej subskrypcji.
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d8b700a2ad41a37ca0ad745f3e7767449974b18a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547686"
---
# <a name="purchase-an-add-on-to-a-subscription"></a><span data-ttu-id="ee680-103">Zakup dodatku do subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ee680-103">Purchase an add-on to a subscription</span></span>

<span data-ttu-id="ee680-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ee680-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ee680-105">Jak kupić dodatek do istniejącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ee680-105">How to purchase an add-on to an existing subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee680-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ee680-106">Prerequisites</span></span>

- <span data-ttu-id="ee680-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ee680-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ee680-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ee680-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="ee680-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ee680-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ee680-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="ee680-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ee680-111">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="ee680-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ee680-112">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="ee680-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ee680-113">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="ee680-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ee680-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ee680-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="ee680-115">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ee680-115">A subscription ID.</span></span> <span data-ttu-id="ee680-116">Jest to istniejąca subskrypcja, dla której należy zakupić ofertę dodatku.</span><span class="sxs-lookup"><span data-stu-id="ee680-116">This is the existing subscription for which to purchase an add-on offer.</span></span>

- <span data-ttu-id="ee680-117">Identyfikator oferty identyfikujący ofertę dodatku do zakupu.</span><span class="sxs-lookup"><span data-stu-id="ee680-117">An offer ID that identifies the add-on offer to purchase.</span></span>

## <a name="purchasing-an-add-on-through-code"></a><span data-ttu-id="ee680-118">Kupowanie dodatku za pomocą kodu</span><span class="sxs-lookup"><span data-stu-id="ee680-118">Purchasing an add-on through code</span></span>

<span data-ttu-id="ee680-119">Po zakupie dodatku do subskrypcji aktualizujesz oryginalne zamówienie subskrypcji przy użyciu zamówienia dodatku.</span><span class="sxs-lookup"><span data-stu-id="ee680-119">When you purchase an add-on to a subscription, you are updating the original subscription order with the order for the add-on.</span></span> <span data-ttu-id="ee680-120">W poniższych przykładach customerId jest identyfikatorem klienta, subscriptionId to identyfikator subskrypcji, a addOnOfferId to identyfikator oferty dla dodatku.</span><span class="sxs-lookup"><span data-stu-id="ee680-120">In the following, customerId is the customer ID, subscriptionId is the subscription ID, and addOnOfferId is the offer ID for the add-on.</span></span>

<span data-ttu-id="ee680-121">Oto konkretne kroki:</span><span class="sxs-lookup"><span data-stu-id="ee680-121">Here are the steps:</span></span>

1.  <span data-ttu-id="ee680-122">Pobierz interfejs do operacji dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ee680-122">Get an interface to the operations for the subscription.</span></span>

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  <span data-ttu-id="ee680-123">Użyj tego interfejsu, aby utworzyć wystąpienia obiektu subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ee680-123">Use that interface to instantiate a subscription object.</span></span> <span data-ttu-id="ee680-124">W ten sposób uzyskujesz szczegółowe informacje o subskrypcji nadrzędnej, w tym identyfikator zamówienia.</span><span class="sxs-lookup"><span data-stu-id="ee680-124">This gets you the parent subscription details, including the order ID.</span></span>

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  <span data-ttu-id="ee680-125">Utworzyć wystąpienia nowego [**obiektu Order.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order)</span><span class="sxs-lookup"><span data-stu-id="ee680-125">Instantiate a new [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object.</span></span> <span data-ttu-id="ee680-126">To wystąpienie zamówienia służy do aktualizowania oryginalnego zamówienia użytego do zakupu subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ee680-126">This order instance is used to update the original order used to purchase the subscription.</span></span> <span data-ttu-id="ee680-127">Dodaj element jedno wierszowy do kolejności, która reprezentuje dodatek.</span><span class="sxs-lookup"><span data-stu-id="ee680-127">Add a single-line item to the order that represents the add-on.</span></span>
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

4.  <span data-ttu-id="ee680-128">Zaktualizuj oryginalne zamówienie subskrypcji przy użyciu nowego zamówienia dla dodatku.</span><span class="sxs-lookup"><span data-stu-id="ee680-128">Update the original order for the subscription with the new order for the add-on.</span></span>
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a><span data-ttu-id="ee680-129">C\#</span><span class="sxs-lookup"><span data-stu-id="ee680-129">C\#</span></span>

<span data-ttu-id="ee680-130">Aby kupić dodatek, zacznij od uzyskania interfejsu dla operacji subskrypcji, wywołując metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta, oraz metodę [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) w celu zidentyfikowania subskrypcji, która ma ofertę dodatku.</span><span class="sxs-lookup"><span data-stu-id="ee680-130">To purchase an add-on, begin by obtaining an interface to the subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the subscription that has the add-on offer.</span></span> <span data-ttu-id="ee680-131">Użyj tego [**interfejsu,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) aby pobrać szczegóły subskrypcji, wywołując [**get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span><span class="sxs-lookup"><span data-stu-id="ee680-131">Use that [**interface**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) to retrieve the subscription details by calling [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span></span> <span data-ttu-id="ee680-132">Szczegóły subskrypcji zawierają identyfikator zamówienia subskrypcji, który jest kolejnością do zaktualizowania przy użyciu dodatku.</span><span class="sxs-lookup"><span data-stu-id="ee680-132">The subscription details contain the order ID of the subscription order, which is the order to be updated with the add-on.</span></span>

<span data-ttu-id="ee680-133">Następnie należy utworzyć wystąpienie nowego obiektu [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) i wypełnić go pojedynczym wystąpieniem [**LineItem,**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) które zawiera informacje identyfikujące dodatek, jak pokazano w poniższym fragmencie kodu.</span><span class="sxs-lookup"><span data-stu-id="ee680-133">Next, instantiate a new [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and populate it with a single [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) instance that contains the information to identify the add-on, as shown in the following code snippet.</span></span> <span data-ttu-id="ee680-134">Użyjesz tego nowego obiektu, aby zaktualizować zamówienie subskrypcji przy użyciu dodatku.</span><span class="sxs-lookup"><span data-stu-id="ee680-134">You'll use this new object to update the subscription order with the add-on.</span></span> <span data-ttu-id="ee680-135">Na koniec wywołaj metodę [**Patch,**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) aby zaktualizować zamówienie subskrypcji, po pierwszym zidentyfikowaniu klienta za pomocą metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) i z zamówieniem [**orders.ById.**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="ee680-135">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) method to update the subscription order, after first identifying the customer with [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) and the order with [**Orders.ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).</span></span>

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

<span data-ttu-id="ee680-136">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="ee680-136">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="ee680-137">**Project:** zestaw SDK Centrum partnerskiego Samples **Class**: AddSubscriptionAddOn.cs</span><span class="sxs-lookup"><span data-stu-id="ee680-137">**Project**: Partner Center SDK Samples **Class**: AddSubscriptionAddOn.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="ee680-138">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="ee680-138">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ee680-139">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="ee680-139">Request syntax</span></span>

| <span data-ttu-id="ee680-140">Metoda</span><span class="sxs-lookup"><span data-stu-id="ee680-140">Method</span></span>    | <span data-ttu-id="ee680-141">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="ee680-141">Request URI</span></span>                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ee680-142">**Patch**</span><span class="sxs-lookup"><span data-stu-id="ee680-142">**PATCH**</span></span> | <span data-ttu-id="ee680-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ee680-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="ee680-144">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="ee680-144">URI parameters</span></span>

<span data-ttu-id="ee680-145">Użyj następujących parametrów, aby zidentyfikować klienta i zamówienie.</span><span class="sxs-lookup"><span data-stu-id="ee680-145">Use the following parameters to identify the customer and order.</span></span>

| <span data-ttu-id="ee680-146">Nazwa</span><span class="sxs-lookup"><span data-stu-id="ee680-146">Name</span></span>                   | <span data-ttu-id="ee680-147">Typ</span><span class="sxs-lookup"><span data-stu-id="ee680-147">Type</span></span>     | <span data-ttu-id="ee680-148">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ee680-148">Required</span></span> | <span data-ttu-id="ee680-149">Opis</span><span class="sxs-lookup"><span data-stu-id="ee680-149">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="ee680-150">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="ee680-150">**customer-tenant-id**</span></span> | <span data-ttu-id="ee680-151">**guid**</span><span class="sxs-lookup"><span data-stu-id="ee680-151">**guid**</span></span> | <span data-ttu-id="ee680-152">Y</span><span class="sxs-lookup"><span data-stu-id="ee680-152">Y</span></span>        | <span data-ttu-id="ee680-153">Wartość jest identyfikatorem GUID w **formacie customer-tenant-id,** który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="ee680-153">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |
| <span data-ttu-id="ee680-154">**order-id**</span><span class="sxs-lookup"><span data-stu-id="ee680-154">**order-id**</span></span>           | <span data-ttu-id="ee680-155">**guid**</span><span class="sxs-lookup"><span data-stu-id="ee680-155">**guid**</span></span> | <span data-ttu-id="ee680-156">Y</span><span class="sxs-lookup"><span data-stu-id="ee680-156">Y</span></span>        | <span data-ttu-id="ee680-157">Identyfikator zamówienia.</span><span class="sxs-lookup"><span data-stu-id="ee680-157">The order identifier.</span></span>                                                              |

### <a name="request-headers"></a><span data-ttu-id="ee680-158">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="ee680-158">Request headers</span></span>

<span data-ttu-id="ee680-159">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ee680-159">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ee680-160">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="ee680-160">Request body</span></span>

<span data-ttu-id="ee680-161">W poniższych tabelach opisano właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="ee680-161">The following tables describe the properties in the request body.</span></span>

## <a name="order"></a><span data-ttu-id="ee680-162">Zamówienie</span><span class="sxs-lookup"><span data-stu-id="ee680-162">Order</span></span>

| <span data-ttu-id="ee680-163">Nazwa</span><span class="sxs-lookup"><span data-stu-id="ee680-163">Name</span></span>                | <span data-ttu-id="ee680-164">Typ</span><span class="sxs-lookup"><span data-stu-id="ee680-164">Type</span></span>             | <span data-ttu-id="ee680-165">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ee680-165">Required</span></span> | <span data-ttu-id="ee680-166">Opis</span><span class="sxs-lookup"><span data-stu-id="ee680-166">Description</span></span>                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| <span data-ttu-id="ee680-167">Id</span><span class="sxs-lookup"><span data-stu-id="ee680-167">Id</span></span>                  | <span data-ttu-id="ee680-168">ciąg</span><span class="sxs-lookup"><span data-stu-id="ee680-168">string</span></span>           | <span data-ttu-id="ee680-169">N</span><span class="sxs-lookup"><span data-stu-id="ee680-169">N</span></span>        | <span data-ttu-id="ee680-170">Identyfikator zamówienia.</span><span class="sxs-lookup"><span data-stu-id="ee680-170">The order ID.</span></span>                                        |
| <span data-ttu-id="ee680-171">ReferenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="ee680-171">ReferenceCustomerId</span></span> | <span data-ttu-id="ee680-172">ciąg</span><span class="sxs-lookup"><span data-stu-id="ee680-172">string</span></span>           | <span data-ttu-id="ee680-173">Y</span><span class="sxs-lookup"><span data-stu-id="ee680-173">Y</span></span>        | <span data-ttu-id="ee680-174">Identyfikator klienta.</span><span class="sxs-lookup"><span data-stu-id="ee680-174">The customer ID.</span></span>                                     |
| <span data-ttu-id="ee680-175">LineItems</span><span class="sxs-lookup"><span data-stu-id="ee680-175">LineItems</span></span>           | <span data-ttu-id="ee680-176">tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="ee680-176">array of objects</span></span> | <span data-ttu-id="ee680-177">Y</span><span class="sxs-lookup"><span data-stu-id="ee680-177">Y</span></span>        | <span data-ttu-id="ee680-178">Tablica obiektów [OrderLineItem.](#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="ee680-178">An array of [OrderLineItem](#orderlineitem) objects.</span></span> |
| <span data-ttu-id="ee680-179">Creationdate</span><span class="sxs-lookup"><span data-stu-id="ee680-179">CreationDate</span></span>        | <span data-ttu-id="ee680-180">ciąg</span><span class="sxs-lookup"><span data-stu-id="ee680-180">string</span></span>           | <span data-ttu-id="ee680-181">N</span><span class="sxs-lookup"><span data-stu-id="ee680-181">N</span></span>        | <span data-ttu-id="ee680-182">Data utworzenia zamówienia w formacie data/godzina.</span><span class="sxs-lookup"><span data-stu-id="ee680-182">The date the order was created, in date-time format.</span></span> |
| <span data-ttu-id="ee680-183">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="ee680-183">Attributes</span></span>          | <span data-ttu-id="ee680-184">object</span><span class="sxs-lookup"><span data-stu-id="ee680-184">object</span></span>           | <span data-ttu-id="ee680-185">N</span><span class="sxs-lookup"><span data-stu-id="ee680-185">N</span></span>        | <span data-ttu-id="ee680-186">Zawiera "ObjectType": "Order".</span><span class="sxs-lookup"><span data-stu-id="ee680-186">Contains "ObjectType": "Order".</span></span>                      |

## <a name="orderlineitem"></a><span data-ttu-id="ee680-187">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="ee680-187">OrderLineItem</span></span>

| <span data-ttu-id="ee680-188">Nazwa</span><span class="sxs-lookup"><span data-stu-id="ee680-188">Name</span></span>                 | <span data-ttu-id="ee680-189">Typ</span><span class="sxs-lookup"><span data-stu-id="ee680-189">Type</span></span>   | <span data-ttu-id="ee680-190">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ee680-190">Required</span></span> | <span data-ttu-id="ee680-191">Opis</span><span class="sxs-lookup"><span data-stu-id="ee680-191">Description</span></span>                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="ee680-192">LineItemNumber</span><span class="sxs-lookup"><span data-stu-id="ee680-192">LineItemNumber</span></span>       | <span data-ttu-id="ee680-193">liczba</span><span class="sxs-lookup"><span data-stu-id="ee680-193">number</span></span> | <span data-ttu-id="ee680-194">Y</span><span class="sxs-lookup"><span data-stu-id="ee680-194">Y</span></span>        | <span data-ttu-id="ee680-195">Numer elementu wiersza rozpoczynający się od 0.</span><span class="sxs-lookup"><span data-stu-id="ee680-195">The line item number, starting with 0.</span></span>                       |
| <span data-ttu-id="ee680-196">OfferId</span><span class="sxs-lookup"><span data-stu-id="ee680-196">OfferId</span></span>              | <span data-ttu-id="ee680-197">ciąg</span><span class="sxs-lookup"><span data-stu-id="ee680-197">string</span></span> | <span data-ttu-id="ee680-198">Y</span><span class="sxs-lookup"><span data-stu-id="ee680-198">Y</span></span>        | <span data-ttu-id="ee680-199">Identyfikator oferty dodatku.</span><span class="sxs-lookup"><span data-stu-id="ee680-199">The offer ID of the add-on.</span></span>                                  |
| <span data-ttu-id="ee680-200">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="ee680-200">SubscriptionId</span></span>       | <span data-ttu-id="ee680-201">ciąg</span><span class="sxs-lookup"><span data-stu-id="ee680-201">string</span></span> | <span data-ttu-id="ee680-202">N</span><span class="sxs-lookup"><span data-stu-id="ee680-202">N</span></span>        | <span data-ttu-id="ee680-203">Identyfikator zakupionej subskrypcji dodatku.</span><span class="sxs-lookup"><span data-stu-id="ee680-203">The ID of the add-on subscription purchased.</span></span>                 |
| <span data-ttu-id="ee680-204">ParentSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="ee680-204">ParentSubscriptionId</span></span> | <span data-ttu-id="ee680-205">ciąg</span><span class="sxs-lookup"><span data-stu-id="ee680-205">string</span></span> | <span data-ttu-id="ee680-206">Y</span><span class="sxs-lookup"><span data-stu-id="ee680-206">Y</span></span>        | <span data-ttu-id="ee680-207">Identyfikator subskrypcji nadrzędnej, która ma ofertę dodatku.</span><span class="sxs-lookup"><span data-stu-id="ee680-207">The ID of the parent subscription that has the add-on offer.</span></span> |
| <span data-ttu-id="ee680-208">FriendlyName</span><span class="sxs-lookup"><span data-stu-id="ee680-208">FriendlyName</span></span>         | <span data-ttu-id="ee680-209">ciąg</span><span class="sxs-lookup"><span data-stu-id="ee680-209">string</span></span> | <span data-ttu-id="ee680-210">N</span><span class="sxs-lookup"><span data-stu-id="ee680-210">N</span></span>        | <span data-ttu-id="ee680-211">Przyjazna nazwa dla tego elementu wiersza.</span><span class="sxs-lookup"><span data-stu-id="ee680-211">The friendly name for this line item.</span></span>                        |
| <span data-ttu-id="ee680-212">Liczba</span><span class="sxs-lookup"><span data-stu-id="ee680-212">Quantity</span></span>             | <span data-ttu-id="ee680-213">liczba</span><span class="sxs-lookup"><span data-stu-id="ee680-213">number</span></span> | <span data-ttu-id="ee680-214">Y</span><span class="sxs-lookup"><span data-stu-id="ee680-214">Y</span></span>        | <span data-ttu-id="ee680-215">Liczba licencji.</span><span class="sxs-lookup"><span data-stu-id="ee680-215">The number of licenses.</span></span>                                      |
| <span data-ttu-id="ee680-216">PartnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="ee680-216">PartnerIdOnRecord</span></span>    | <span data-ttu-id="ee680-217">ciąg</span><span class="sxs-lookup"><span data-stu-id="ee680-217">string</span></span> | <span data-ttu-id="ee680-218">N</span><span class="sxs-lookup"><span data-stu-id="ee680-218">N</span></span>        | <span data-ttu-id="ee680-219">Identyfikator MPN partnera rekordu.</span><span class="sxs-lookup"><span data-stu-id="ee680-219">The MPN ID of the partner of record.</span></span>                         |
| <span data-ttu-id="ee680-220">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="ee680-220">Attributes</span></span>           | <span data-ttu-id="ee680-221">object</span><span class="sxs-lookup"><span data-stu-id="ee680-221">object</span></span> | <span data-ttu-id="ee680-222">N</span><span class="sxs-lookup"><span data-stu-id="ee680-222">N</span></span>        | <span data-ttu-id="ee680-223">Zawiera "ObjectType": "OrderLineItem".</span><span class="sxs-lookup"><span data-stu-id="ee680-223">Contains "ObjectType": "OrderLineItem".</span></span>                      |

### <a name="request-example"></a><span data-ttu-id="ee680-224">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="ee680-224">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="ee680-225">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="ee680-225">REST response</span></span>

<span data-ttu-id="ee680-226">W przypadku powodzenia ta metoda zwraca zaktualizowaną kolejność subskrypcji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ee680-226">If successful, this method returns the updated subscription order in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ee680-227">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ee680-227">Response success and error codes</span></span>

<span data-ttu-id="ee680-228">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="ee680-228">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ee680-229">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="ee680-229">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ee680-230">Aby uzyskać pełną listę, zobacz [Partner Center Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ee680-230">For the full list, see [Partner Center Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ee680-231">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ee680-231">Response example</span></span>

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
