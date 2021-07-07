---
title: Zmiana cyklu rozliczeniowego
description: Dowiedz się, jak zaktualizować subskrypcję klienta do rozliczeń miesięcznych lub rocznych przy użyciu Partner Center API. Możesz to również zrobić z Partner Center nawigacyjnego.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 435309229e2cb038c936028943f4c2cf27b032a7
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974118"
---
# <a name="change-a-customer-subscription-billing-cycle"></a><span data-ttu-id="4791f-104">Zmienianie cyklu rozliczeniowego subskrypcji klienta</span><span class="sxs-lookup"><span data-stu-id="4791f-104">Change a customer subscription billing cycle</span></span>

<span data-ttu-id="4791f-105">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="4791f-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4791f-106">Aktualizuje zamówienie [z](order-resources.md) rozliczenia miesięcznego na roczne lub rocznego na miesięczne.</span><span class="sxs-lookup"><span data-stu-id="4791f-106">Updates an [Order](order-resources.md) from monthly to annual billing or from annual to monthly billing.</span></span>

<span data-ttu-id="4791f-107">Na Partner Center nawigacyjnym można wykonać tę operację, przechodząc do strony szczegółów subskrypcji klienta.</span><span class="sxs-lookup"><span data-stu-id="4791f-107">In the Partner Center dashboard, this operation can be performed by navigating to a customer's subscription details page.</span></span> <span data-ttu-id="4791f-108">W tym miejscu zobaczysz opcję definiowania bieżącego cyklu rozliczeniowego dla subskrypcji z możliwością jej zmiany i przesyłania.</span><span class="sxs-lookup"><span data-stu-id="4791f-108">Once there, you will see an option defining the current billing cycle for the subscription with the ability to change and submit it.</span></span>

<span data-ttu-id="4791f-109">**Poza zakresem** tego artykułu:</span><span class="sxs-lookup"><span data-stu-id="4791f-109">**Out of scope** for this article:</span></span>

- <span data-ttu-id="4791f-110">Zmiana cyklu rozliczeniowego dla wersji próbnych</span><span class="sxs-lookup"><span data-stu-id="4791f-110">Changing the billing cycle for trials</span></span>
- <span data-ttu-id="4791f-111">Zmiana cykli rozliczeniowych dla wszystkich ofert poza rocznym okresem (miesięcznych, sześciorocznych) & subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4791f-111">Changing the billing cycles for any non-annual term offers (monthly, six-year) & Azure subscriptions</span></span>
- <span data-ttu-id="4791f-112">Zmienianie cykli rozliczeniowych dla nieaktywnych subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4791f-112">Changing the billing cycles for inactive subscriptions</span></span>
- <span data-ttu-id="4791f-113">Zmienianie cykli rozliczeniowych dla subskrypcji Usługi online Microsoft opartych na licencjach</span><span class="sxs-lookup"><span data-stu-id="4791f-113">Changing billing cycles for Microsoft online services license-based subscriptions</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4791f-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4791f-114">Prerequisites</span></span>

- <span data-ttu-id="4791f-115">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4791f-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4791f-116">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4791f-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="4791f-117">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4791f-117">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4791f-118">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="4791f-118">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4791f-119">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="4791f-119">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4791f-120">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="4791f-120">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4791f-121">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="4791f-121">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4791f-122">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4791f-122">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="4791f-123">Identyfikator zamówienia.</span><span class="sxs-lookup"><span data-stu-id="4791f-123">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="4791f-124">C\#</span><span class="sxs-lookup"><span data-stu-id="4791f-124">C\#</span></span>

<span data-ttu-id="4791f-125">Aby zmienić częstotliwość cyklu rozliczeniowego, zaktualizuj [**właściwość Order.BillingCycle.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle)</span><span class="sxs-lookup"><span data-stu-id="4791f-125">To change the frequency of the billing cycle, update the [**Order.BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) property.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="4791f-126">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="4791f-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4791f-127">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="4791f-127">Request syntax</span></span>

| <span data-ttu-id="4791f-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="4791f-128">Method</span></span>    | <span data-ttu-id="4791f-129">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="4791f-129">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4791f-130">**Patch**</span><span class="sxs-lookup"><span data-stu-id="4791f-130">**PATCH**</span></span> | <span data-ttu-id="4791f-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4791f-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="4791f-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="4791f-132">URI parameter</span></span>

<span data-ttu-id="4791f-133">W tej tabeli wymieniono parametr zapytania wymagany do zmiany ilości subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="4791f-133">This table lists the required query parameter to change the quantity of the subscription.</span></span>

| <span data-ttu-id="4791f-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="4791f-134">Name</span></span>                   | <span data-ttu-id="4791f-135">Typ</span><span class="sxs-lookup"><span data-stu-id="4791f-135">Type</span></span> | <span data-ttu-id="4791f-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4791f-136">Required</span></span> | <span data-ttu-id="4791f-137">Opis</span><span class="sxs-lookup"><span data-stu-id="4791f-137">Description</span></span>                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| <span data-ttu-id="4791f-138">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="4791f-138">**customer-tenant-id**</span></span> | <span data-ttu-id="4791f-139">GUID</span><span class="sxs-lookup"><span data-stu-id="4791f-139">GUID</span></span> |    <span data-ttu-id="4791f-140">Y</span><span class="sxs-lookup"><span data-stu-id="4791f-140">Y</span></span>     | <span data-ttu-id="4791f-141">Identyfikator GUID **sformatowany jako customer-tenant-id,** który identyfikuje klienta</span><span class="sxs-lookup"><span data-stu-id="4791f-141">A GUID formatted **customer-tenant-id** that identifies the customer</span></span> |
| <span data-ttu-id="4791f-142">**order-id**</span><span class="sxs-lookup"><span data-stu-id="4791f-142">**order-id**</span></span>           | <span data-ttu-id="4791f-143">GUID</span><span class="sxs-lookup"><span data-stu-id="4791f-143">GUID</span></span> |    <span data-ttu-id="4791f-144">Y</span><span class="sxs-lookup"><span data-stu-id="4791f-144">Y</span></span>     | <span data-ttu-id="4791f-145">Identyfikator zamówienia</span><span class="sxs-lookup"><span data-stu-id="4791f-145">The order identifier</span></span>                                                 |

### <a name="request-headers"></a><span data-ttu-id="4791f-146">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="4791f-146">Request headers</span></span>

<span data-ttu-id="4791f-147">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="4791f-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4791f-148">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="4791f-148">Request body</span></span>

<span data-ttu-id="4791f-149">W poniższych tabelach opisano właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="4791f-149">The following tables describe the properties in the request body.</span></span>

### <a name="order"></a><span data-ttu-id="4791f-150">Zamówienie</span><span class="sxs-lookup"><span data-stu-id="4791f-150">Order</span></span>

| <span data-ttu-id="4791f-151">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4791f-151">Property</span></span>           | <span data-ttu-id="4791f-152">Typ</span><span class="sxs-lookup"><span data-stu-id="4791f-152">Type</span></span>             | <span data-ttu-id="4791f-153">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4791f-153">Required</span></span> | <span data-ttu-id="4791f-154">Opis</span><span class="sxs-lookup"><span data-stu-id="4791f-154">Description</span></span>                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| <span data-ttu-id="4791f-155">Id</span><span class="sxs-lookup"><span data-stu-id="4791f-155">Id</span></span>                 | <span data-ttu-id="4791f-156">ciąg</span><span class="sxs-lookup"><span data-stu-id="4791f-156">string</span></span>           |    <span data-ttu-id="4791f-157">N</span><span class="sxs-lookup"><span data-stu-id="4791f-157">N</span></span>     | <span data-ttu-id="4791f-158">Identyfikator zamówienia podany po pomyślnym utworzeniu zamówienia</span><span class="sxs-lookup"><span data-stu-id="4791f-158">An order identifier that is supplied upon successful creation of the order</span></span> |
|<span data-ttu-id="4791f-159">ReferenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="4791f-159">ReferenceCustomerId</span></span> | <span data-ttu-id="4791f-160">ciąg</span><span class="sxs-lookup"><span data-stu-id="4791f-160">string</span></span>           |    <span data-ttu-id="4791f-161">Y</span><span class="sxs-lookup"><span data-stu-id="4791f-161">Y</span></span>     | <span data-ttu-id="4791f-162">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="4791f-162">The customer identifier</span></span>                                                    |
| <span data-ttu-id="4791f-163">BillingCycle</span><span class="sxs-lookup"><span data-stu-id="4791f-163">BillingCycle</span></span>       | <span data-ttu-id="4791f-164">ciąg</span><span class="sxs-lookup"><span data-stu-id="4791f-164">string</span></span>           |    <span data-ttu-id="4791f-165">Y</span><span class="sxs-lookup"><span data-stu-id="4791f-165">Y</span></span>     | <span data-ttu-id="4791f-166">Wskazuje częstotliwość, za pomocą której partner jest rozliczany za to zamówienie.</span><span class="sxs-lookup"><span data-stu-id="4791f-166">Indicates the frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="4791f-167">Obsługiwane wartości to nazwy członków w [typie BillingCycleType](product-resources.md#billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="4791f-167">Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype).</span></span> |
| <span data-ttu-id="4791f-168">LineItems</span><span class="sxs-lookup"><span data-stu-id="4791f-168">LineItems</span></span>          | <span data-ttu-id="4791f-169">tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="4791f-169">array of objects</span></span> |    <span data-ttu-id="4791f-170">Y</span><span class="sxs-lookup"><span data-stu-id="4791f-170">Y</span></span>     | <span data-ttu-id="4791f-171">Tablica zasobów [OrderLineItem](#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="4791f-171">An array of [OrderLineItem](#orderlineitem) resources</span></span>                      |
| <span data-ttu-id="4791f-172">Creationdate</span><span class="sxs-lookup"><span data-stu-id="4791f-172">CreationDate</span></span>       | <span data-ttu-id="4791f-173">datetime</span><span class="sxs-lookup"><span data-stu-id="4791f-173">datetime</span></span>         |    <span data-ttu-id="4791f-174">N</span><span class="sxs-lookup"><span data-stu-id="4791f-174">N</span></span>     | <span data-ttu-id="4791f-175">Data utworzenia zamówienia w formacie data/godzina</span><span class="sxs-lookup"><span data-stu-id="4791f-175">The date the order was created, in date-time format</span></span>                        |
| <span data-ttu-id="4791f-176">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="4791f-176">Attributes</span></span>         | <span data-ttu-id="4791f-177">Obiekt</span><span class="sxs-lookup"><span data-stu-id="4791f-177">Object</span></span>           |    <span data-ttu-id="4791f-178">N</span><span class="sxs-lookup"><span data-stu-id="4791f-178">N</span></span>     | <span data-ttu-id="4791f-179">Zawiera "ObjectType": "OrderLineItem"</span><span class="sxs-lookup"><span data-stu-id="4791f-179">Contains "ObjectType": "OrderLineItem"</span></span>                                     |

### <a name="orderlineitem"></a><span data-ttu-id="4791f-180">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="4791f-180">OrderLineItem</span></span>

| <span data-ttu-id="4791f-181">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4791f-181">Property</span></span>             | <span data-ttu-id="4791f-182">Typ</span><span class="sxs-lookup"><span data-stu-id="4791f-182">Type</span></span>   | <span data-ttu-id="4791f-183">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4791f-183">Required</span></span> | <span data-ttu-id="4791f-184">Opis</span><span class="sxs-lookup"><span data-stu-id="4791f-184">Description</span></span>                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="4791f-185">LineItemNumber</span><span class="sxs-lookup"><span data-stu-id="4791f-185">LineItemNumber</span></span>       | <span data-ttu-id="4791f-186">liczba</span><span class="sxs-lookup"><span data-stu-id="4791f-186">number</span></span> |    <span data-ttu-id="4791f-187">Y</span><span class="sxs-lookup"><span data-stu-id="4791f-187">Y</span></span>     | <span data-ttu-id="4791f-188">Numer elementu wiersza rozpoczynający się od 0</span><span class="sxs-lookup"><span data-stu-id="4791f-188">The line item number, starting with 0</span></span>                                              |
| <span data-ttu-id="4791f-189">OfferId</span><span class="sxs-lookup"><span data-stu-id="4791f-189">OfferId</span></span>              | <span data-ttu-id="4791f-190">ciąg</span><span class="sxs-lookup"><span data-stu-id="4791f-190">string</span></span> |    <span data-ttu-id="4791f-191">Y</span><span class="sxs-lookup"><span data-stu-id="4791f-191">Y</span></span>     | <span data-ttu-id="4791f-192">Identyfikator oferty</span><span class="sxs-lookup"><span data-stu-id="4791f-192">The ID of the offer</span></span>                                                                |
| <span data-ttu-id="4791f-193">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="4791f-193">SubscriptionId</span></span>       | <span data-ttu-id="4791f-194">ciąg</span><span class="sxs-lookup"><span data-stu-id="4791f-194">string</span></span> |    <span data-ttu-id="4791f-195">Y</span><span class="sxs-lookup"><span data-stu-id="4791f-195">Y</span></span>     | <span data-ttu-id="4791f-196">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4791f-196">The ID of the subscription</span></span>                                                         |
| <span data-ttu-id="4791f-197">FriendlyName</span><span class="sxs-lookup"><span data-stu-id="4791f-197">FriendlyName</span></span>         | <span data-ttu-id="4791f-198">ciąg</span><span class="sxs-lookup"><span data-stu-id="4791f-198">string</span></span> |    <span data-ttu-id="4791f-199">N</span><span class="sxs-lookup"><span data-stu-id="4791f-199">N</span></span>     | <span data-ttu-id="4791f-200">Przyjazna nazwa subskrypcji zdefiniowanej przez partnera w celu uujednoznania</span><span class="sxs-lookup"><span data-stu-id="4791f-200">The friendly name for the subscription defined by the partner to help disambiguate</span></span> |
| <span data-ttu-id="4791f-201">Liczba</span><span class="sxs-lookup"><span data-stu-id="4791f-201">Quantity</span></span>             | <span data-ttu-id="4791f-202">liczba</span><span class="sxs-lookup"><span data-stu-id="4791f-202">number</span></span> |    <span data-ttu-id="4791f-203">Y</span><span class="sxs-lookup"><span data-stu-id="4791f-203">Y</span></span>     | <span data-ttu-id="4791f-204">Liczba licencji lub wystąpień</span><span class="sxs-lookup"><span data-stu-id="4791f-204">The number of licenses or instances</span></span>                                                |
| <span data-ttu-id="4791f-205">PartnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="4791f-205">PartnerIdOnRecord</span></span>    | <span data-ttu-id="4791f-206">ciąg</span><span class="sxs-lookup"><span data-stu-id="4791f-206">string</span></span> |    <span data-ttu-id="4791f-207">N</span><span class="sxs-lookup"><span data-stu-id="4791f-207">N</span></span>     | <span data-ttu-id="4791f-208">Identyfikator MPN partnera rekordu</span><span class="sxs-lookup"><span data-stu-id="4791f-208">The MPN ID of the partner of record</span></span>                                                |
| <span data-ttu-id="4791f-209">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="4791f-209">Attributes</span></span>           | <span data-ttu-id="4791f-210">Obiekt</span><span class="sxs-lookup"><span data-stu-id="4791f-210">Object</span></span> |    <span data-ttu-id="4791f-211">N</span><span class="sxs-lookup"><span data-stu-id="4791f-211">N</span></span>     | <span data-ttu-id="4791f-212">Zawiera "ObjectType": "OrderLineItem"</span><span class="sxs-lookup"><span data-stu-id="4791f-212">Contains "ObjectType": "OrderLineItem"</span></span>                                             |

### <a name="request-example"></a><span data-ttu-id="4791f-213">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="4791f-213">Request example</span></span>

<span data-ttu-id="4791f-214">Aktualizowanie do rozliczenia rocznego</span><span class="sxs-lookup"><span data-stu-id="4791f-214">Update to annual billing</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="4791f-215">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="4791f-215">REST response</span></span>

<span data-ttu-id="4791f-216">W przypadku powodzenia ta metoda zwraca zaktualizowaną kolejność subskrypcji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="4791f-216">If successful, this method returns the updated subscription order in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4791f-217">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4791f-217">Response success and error codes</span></span>

<span data-ttu-id="4791f-218">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="4791f-218">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4791f-219">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="4791f-219">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4791f-220">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4791f-220">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4791f-221">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4791f-221">Response example</span></span>

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