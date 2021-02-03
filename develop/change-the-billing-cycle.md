---
title: Zmiana cyklu rozliczeniowego
description: Dowiedz się, jak zaktualizować subskrypcję klienta do miesięcznej lub rocznej rozliczania przy użyciu interfejsów API Centrum partnerskiego. Można to również zrobić z poziomu pulpitu nawigacyjnego Centrum partnerskiego.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 8a2879db061ced799e29d84e71be5b1259b07689
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768601"
---
# <a name="change-a-customer-subscription-billing-cycle"></a><span data-ttu-id="91b2d-104">Zmień cykl rozliczeniowy subskrypcji klienta</span><span class="sxs-lookup"><span data-stu-id="91b2d-104">Change a customer subscription billing cycle</span></span>

<span data-ttu-id="91b2d-105">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="91b2d-105">**Applies to:**</span></span>

- <span data-ttu-id="91b2d-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="91b2d-106">Partner Center</span></span>
- <span data-ttu-id="91b2d-107">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="91b2d-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="91b2d-108">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="91b2d-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="91b2d-109">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="91b2d-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="91b2d-110">Aktualizuje [Zamówienie](order-resources.md) od miesięcznego do rocznego rozliczania lub rocznego rozliczania.</span><span class="sxs-lookup"><span data-stu-id="91b2d-110">Updates an [Order](order-resources.md) from monthly to annual billing or from annual to monthly billing.</span></span>

<span data-ttu-id="91b2d-111">Na pulpicie nawigacyjnym Centrum partnerskiego można wykonać tę operację, przechodząc do strony szczegółów subskrypcji klienta.</span><span class="sxs-lookup"><span data-stu-id="91b2d-111">In the Partner Center dashboard, this operation can be performed by navigating to a customer's subscription details page.</span></span> <span data-ttu-id="91b2d-112">W tej chwili zobaczysz opcję definiującą bieżący cykl rozliczeniowy dla subskrypcji z możliwością jej zmiany i przesłania.</span><span class="sxs-lookup"><span data-stu-id="91b2d-112">Once there, you will see an option defining the current billing cycle for the subscription with the ability to change and submit it.</span></span>

<span data-ttu-id="91b2d-113">**Poza zakresem** tego artykułu:</span><span class="sxs-lookup"><span data-stu-id="91b2d-113">**Out of scope** for this article:</span></span>

- <span data-ttu-id="91b2d-114">Zmiana cyklu rozliczeniowego dla prób</span><span class="sxs-lookup"><span data-stu-id="91b2d-114">Changing the billing cycle for trials</span></span>
- <span data-ttu-id="91b2d-115">Zmiana cykli rozliczeń w przypadku ofert nierocznych (miesięcznych, 6-letnich) & subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="91b2d-115">Changing the billing cycles for any non-annual term offers (monthly, 6-year) & Azure subscriptions</span></span>
- <span data-ttu-id="91b2d-116">Zmiana cykli rozliczeń dla nieaktywnych subskrypcji</span><span class="sxs-lookup"><span data-stu-id="91b2d-116">Changing the billing cycles for inactive subscriptions</span></span>
- <span data-ttu-id="91b2d-117">Zmiana cykli rozliczeń dla subskrypcji opartych na licencji programu Microsoft Usługi online</span><span class="sxs-lookup"><span data-stu-id="91b2d-117">Changing billing cycles for Microsoft online services license-based subscriptions</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91b2d-118">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="91b2d-118">Prerequisites</span></span>

- <span data-ttu-id="91b2d-119">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="91b2d-119">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="91b2d-120">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="91b2d-120">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="91b2d-121">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="91b2d-121">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="91b2d-122">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="91b2d-122">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="91b2d-123">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="91b2d-123">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="91b2d-124">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="91b2d-124">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="91b2d-125">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="91b2d-125">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="91b2d-126">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="91b2d-126">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="91b2d-127">Identyfikator zamówienia.</span><span class="sxs-lookup"><span data-stu-id="91b2d-127">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="91b2d-128">C\#</span><span class="sxs-lookup"><span data-stu-id="91b2d-128">C\#</span></span>

<span data-ttu-id="91b2d-129">Aby zmienić częstotliwość cyklu rozliczeniowego, zaktualizuj właściwość [**Order. BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) .</span><span class="sxs-lookup"><span data-stu-id="91b2d-129">To change the frequency of the billing cycle, update the [**Order.BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) property.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string orderId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    BillingCycle = BillingCycleType.Annual,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = offerId,
            SubscriptionId = "69829602-C219-40FD-A3D5-4150FCA41A19",
            Quantity = 1
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.ById(orderId).Patch(order);
```

## <a name="rest-request"></a><span data-ttu-id="91b2d-130">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="91b2d-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="91b2d-131">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="91b2d-131">Request syntax</span></span>

| <span data-ttu-id="91b2d-132">Metoda</span><span class="sxs-lookup"><span data-stu-id="91b2d-132">Method</span></span>    | <span data-ttu-id="91b2d-133">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="91b2d-133">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="91b2d-134">**WYSŁANA**</span><span class="sxs-lookup"><span data-stu-id="91b2d-134">**PATCH**</span></span> | <span data-ttu-id="91b2d-135">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="91b2d-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="91b2d-136">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="91b2d-136">URI parameter</span></span>

<span data-ttu-id="91b2d-137">Ta tabela zawiera listę wymaganych parametrów zapytania, aby zmienić liczbę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="91b2d-137">This table lists the required query parameter to change the quantity of the subscription.</span></span>

| <span data-ttu-id="91b2d-138">Nazwa</span><span class="sxs-lookup"><span data-stu-id="91b2d-138">Name</span></span>                   | <span data-ttu-id="91b2d-139">Typ</span><span class="sxs-lookup"><span data-stu-id="91b2d-139">Type</span></span> | <span data-ttu-id="91b2d-140">Wymagane</span><span class="sxs-lookup"><span data-stu-id="91b2d-140">Required</span></span> | <span data-ttu-id="91b2d-141">Opis</span><span class="sxs-lookup"><span data-stu-id="91b2d-141">Description</span></span>                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| <span data-ttu-id="91b2d-142">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="91b2d-142">**customer-tenant-id**</span></span> | <span data-ttu-id="91b2d-143">GUID</span><span class="sxs-lookup"><span data-stu-id="91b2d-143">GUID</span></span> |    <span data-ttu-id="91b2d-144">Y</span><span class="sxs-lookup"><span data-stu-id="91b2d-144">Y</span></span>     | <span data-ttu-id="91b2d-145">Identyfikator GUID w formacie identyfikatora **dzierżawy klienta** , który identyfikuje klienta</span><span class="sxs-lookup"><span data-stu-id="91b2d-145">A GUID formatted **customer-tenant-id** that identifies the customer</span></span> |
| <span data-ttu-id="91b2d-146">**Identyfikator zamówienia**</span><span class="sxs-lookup"><span data-stu-id="91b2d-146">**order-id**</span></span>           | <span data-ttu-id="91b2d-147">GUID</span><span class="sxs-lookup"><span data-stu-id="91b2d-147">GUID</span></span> |    <span data-ttu-id="91b2d-148">Y</span><span class="sxs-lookup"><span data-stu-id="91b2d-148">Y</span></span>     | <span data-ttu-id="91b2d-149">Identyfikator zamówienia</span><span class="sxs-lookup"><span data-stu-id="91b2d-149">The order identifier</span></span>                                                 |

### <a name="request-headers"></a><span data-ttu-id="91b2d-150">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="91b2d-150">Request headers</span></span>

<span data-ttu-id="91b2d-151">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="91b2d-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="91b2d-152">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="91b2d-152">Request body</span></span>

<span data-ttu-id="91b2d-153">W poniższych tabelach opisano właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="91b2d-153">The following tables describe the properties in the request body.</span></span>

### <a name="order"></a><span data-ttu-id="91b2d-154">Zamówienie</span><span class="sxs-lookup"><span data-stu-id="91b2d-154">Order</span></span>

| <span data-ttu-id="91b2d-155">Właściwość</span><span class="sxs-lookup"><span data-stu-id="91b2d-155">Property</span></span>           | <span data-ttu-id="91b2d-156">Typ</span><span class="sxs-lookup"><span data-stu-id="91b2d-156">Type</span></span>             | <span data-ttu-id="91b2d-157">Wymagane</span><span class="sxs-lookup"><span data-stu-id="91b2d-157">Required</span></span> | <span data-ttu-id="91b2d-158">Opis</span><span class="sxs-lookup"><span data-stu-id="91b2d-158">Description</span></span>                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| <span data-ttu-id="91b2d-159">Id</span><span class="sxs-lookup"><span data-stu-id="91b2d-159">Id</span></span>                 | <span data-ttu-id="91b2d-160">ciąg</span><span class="sxs-lookup"><span data-stu-id="91b2d-160">string</span></span>           |    <span data-ttu-id="91b2d-161">N</span><span class="sxs-lookup"><span data-stu-id="91b2d-161">N</span></span>     | <span data-ttu-id="91b2d-162">Identyfikator zamówienia, który jest dostarczany po pomyślnym utworzeniu zamówienia</span><span class="sxs-lookup"><span data-stu-id="91b2d-162">An order identifier that is supplied upon successful creation of the order</span></span> |
|<span data-ttu-id="91b2d-163">ReferenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="91b2d-163">ReferenceCustomerId</span></span> | <span data-ttu-id="91b2d-164">ciąg</span><span class="sxs-lookup"><span data-stu-id="91b2d-164">string</span></span>           |    <span data-ttu-id="91b2d-165">Y</span><span class="sxs-lookup"><span data-stu-id="91b2d-165">Y</span></span>     | <span data-ttu-id="91b2d-166">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="91b2d-166">The customer identifier</span></span>                                                    |
| <span data-ttu-id="91b2d-167">BillingCycle</span><span class="sxs-lookup"><span data-stu-id="91b2d-167">BillingCycle</span></span>       | <span data-ttu-id="91b2d-168">ciąg</span><span class="sxs-lookup"><span data-stu-id="91b2d-168">string</span></span>           |    <span data-ttu-id="91b2d-169">Y</span><span class="sxs-lookup"><span data-stu-id="91b2d-169">Y</span></span>     | <span data-ttu-id="91b2d-170">Wskazuje częstotliwość, z jaką jest rozliczany partner dla tego zamówienia.</span><span class="sxs-lookup"><span data-stu-id="91b2d-170">Indicates the frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="91b2d-171">Obsługiwane wartości to nazwy elementów członkowskich Znalezione w [BillingCycleType](product-resources.md#billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="91b2d-171">Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype).</span></span> |
| <span data-ttu-id="91b2d-172">LineItems</span><span class="sxs-lookup"><span data-stu-id="91b2d-172">LineItems</span></span>          | <span data-ttu-id="91b2d-173">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="91b2d-173">array of objects</span></span> |    <span data-ttu-id="91b2d-174">Y</span><span class="sxs-lookup"><span data-stu-id="91b2d-174">Y</span></span>     | <span data-ttu-id="91b2d-175">Tablica zasobów [OrderLineItem](#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="91b2d-175">An array of [OrderLineItem](#orderlineitem) resources</span></span>                      |
| <span data-ttu-id="91b2d-176">CreationDate</span><span class="sxs-lookup"><span data-stu-id="91b2d-176">CreationDate</span></span>       | <span data-ttu-id="91b2d-177">datetime</span><span class="sxs-lookup"><span data-stu-id="91b2d-177">datetime</span></span>         |    <span data-ttu-id="91b2d-178">N</span><span class="sxs-lookup"><span data-stu-id="91b2d-178">N</span></span>     | <span data-ttu-id="91b2d-179">Data, w której zamówienie zostało utworzone, w formacie daty i godziny</span><span class="sxs-lookup"><span data-stu-id="91b2d-179">The date the order was created, in date-time format</span></span>                        |
| <span data-ttu-id="91b2d-180">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="91b2d-180">Attributes</span></span>         | <span data-ttu-id="91b2d-181">Obiekt</span><span class="sxs-lookup"><span data-stu-id="91b2d-181">Object</span></span>           |    <span data-ttu-id="91b2d-182">N</span><span class="sxs-lookup"><span data-stu-id="91b2d-182">N</span></span>     | <span data-ttu-id="91b2d-183">Zawiera "ObjectType": "OrderLineItem"</span><span class="sxs-lookup"><span data-stu-id="91b2d-183">Contains "ObjectType": "OrderLineItem"</span></span>                                     |

### <a name="orderlineitem"></a><span data-ttu-id="91b2d-184">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="91b2d-184">OrderLineItem</span></span>

| <span data-ttu-id="91b2d-185">Właściwość</span><span class="sxs-lookup"><span data-stu-id="91b2d-185">Property</span></span>             | <span data-ttu-id="91b2d-186">Typ</span><span class="sxs-lookup"><span data-stu-id="91b2d-186">Type</span></span>   | <span data-ttu-id="91b2d-187">Wymagane</span><span class="sxs-lookup"><span data-stu-id="91b2d-187">Required</span></span> | <span data-ttu-id="91b2d-188">Opis</span><span class="sxs-lookup"><span data-stu-id="91b2d-188">Description</span></span>                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="91b2d-189">LineItemNumber</span><span class="sxs-lookup"><span data-stu-id="91b2d-189">LineItemNumber</span></span>       | <span data-ttu-id="91b2d-190">liczba</span><span class="sxs-lookup"><span data-stu-id="91b2d-190">number</span></span> |    <span data-ttu-id="91b2d-191">Y</span><span class="sxs-lookup"><span data-stu-id="91b2d-191">Y</span></span>     | <span data-ttu-id="91b2d-192">Numer elementu wiersza, zaczynając od 0</span><span class="sxs-lookup"><span data-stu-id="91b2d-192">The line item number, starting with 0</span></span>                                              |
| <span data-ttu-id="91b2d-193">OfferId</span><span class="sxs-lookup"><span data-stu-id="91b2d-193">OfferId</span></span>              | <span data-ttu-id="91b2d-194">ciąg</span><span class="sxs-lookup"><span data-stu-id="91b2d-194">string</span></span> |    <span data-ttu-id="91b2d-195">Y</span><span class="sxs-lookup"><span data-stu-id="91b2d-195">Y</span></span>     | <span data-ttu-id="91b2d-196">Identyfikator oferty</span><span class="sxs-lookup"><span data-stu-id="91b2d-196">The ID of the offer</span></span>                                                                |
| <span data-ttu-id="91b2d-197">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="91b2d-197">SubscriptionId</span></span>       | <span data-ttu-id="91b2d-198">ciąg</span><span class="sxs-lookup"><span data-stu-id="91b2d-198">string</span></span> |    <span data-ttu-id="91b2d-199">Y</span><span class="sxs-lookup"><span data-stu-id="91b2d-199">Y</span></span>     | <span data-ttu-id="91b2d-200">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="91b2d-200">The ID of the subscription</span></span>                                                         |
| <span data-ttu-id="91b2d-201">FriendlyName</span><span class="sxs-lookup"><span data-stu-id="91b2d-201">FriendlyName</span></span>         | <span data-ttu-id="91b2d-202">ciąg</span><span class="sxs-lookup"><span data-stu-id="91b2d-202">string</span></span> |    <span data-ttu-id="91b2d-203">N</span><span class="sxs-lookup"><span data-stu-id="91b2d-203">N</span></span>     | <span data-ttu-id="91b2d-204">Przyjazna nazwa dla subskrypcji zdefiniowanej przez partnera, aby pomóc w odróżnieniu</span><span class="sxs-lookup"><span data-stu-id="91b2d-204">The friendly name for the subscription defined by the partner to help disambiguate</span></span> |
| <span data-ttu-id="91b2d-205">Ilość</span><span class="sxs-lookup"><span data-stu-id="91b2d-205">Quantity</span></span>             | <span data-ttu-id="91b2d-206">liczba</span><span class="sxs-lookup"><span data-stu-id="91b2d-206">number</span></span> |    <span data-ttu-id="91b2d-207">Y</span><span class="sxs-lookup"><span data-stu-id="91b2d-207">Y</span></span>     | <span data-ttu-id="91b2d-208">Liczba licencji lub wystąpień</span><span class="sxs-lookup"><span data-stu-id="91b2d-208">The number of licenses or instances</span></span>                                                |
| <span data-ttu-id="91b2d-209">PartnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="91b2d-209">PartnerIdOnRecord</span></span>    | <span data-ttu-id="91b2d-210">ciąg</span><span class="sxs-lookup"><span data-stu-id="91b2d-210">string</span></span> |    <span data-ttu-id="91b2d-211">N</span><span class="sxs-lookup"><span data-stu-id="91b2d-211">N</span></span>     | <span data-ttu-id="91b2d-212">IDENTYFIKATOR MPN partnera rekordu</span><span class="sxs-lookup"><span data-stu-id="91b2d-212">The MPN ID of the partner of record</span></span>                                                |
| <span data-ttu-id="91b2d-213">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="91b2d-213">Attributes</span></span>           | <span data-ttu-id="91b2d-214">Obiekt</span><span class="sxs-lookup"><span data-stu-id="91b2d-214">Object</span></span> |    <span data-ttu-id="91b2d-215">N</span><span class="sxs-lookup"><span data-stu-id="91b2d-215">N</span></span>     | <span data-ttu-id="91b2d-216">Zawiera "ObjectType": "OrderLineItem"</span><span class="sxs-lookup"><span data-stu-id="91b2d-216">Contains "ObjectType": "OrderLineItem"</span></span>                                             |

### <a name="request-example"></a><span data-ttu-id="91b2d-217">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="91b2d-217">Request example</span></span>

<span data-ttu-id="91b2d-218">Aktualizowanie do rozliczeń rocznych</span><span class="sxs-lookup"><span data-stu-id="91b2d-218">Update to annual billing</span></span>

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
    "BillingCycle" : "Annual",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
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

## <a name="rest-response"></a><span data-ttu-id="91b2d-219">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="91b2d-219">REST response</span></span>

<span data-ttu-id="91b2d-220">Jeśli to się powiedzie, ta metoda zwraca zaktualizowany porządek subskrypcji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="91b2d-220">If successful, this method returns the updated subscription order in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="91b2d-221">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="91b2d-221">Response success and error codes</span></span>

<span data-ttu-id="91b2d-222">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="91b2d-222">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="91b2d-223">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="91b2d-223">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="91b2d-224">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="91b2d-224">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="91b2d-225">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="91b2d-225">Response example</span></span>

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
    "billingCycle": "Annual",
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
        },
        {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/69829602-C219-40FD-A3D5-4150FCA41A19",
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