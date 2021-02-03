---
title: Aktualizowanie koszyka
description: Jak zaktualizować zamówienie dla klienta w koszyku.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7c0806ccc87281b9b34005f22cd8d6ad57fb5de5
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767834"
---
# <a name="update-a-cart"></a><span data-ttu-id="7bc0c-103">Aktualizowanie koszyka</span><span class="sxs-lookup"><span data-stu-id="7bc0c-103">Update a cart</span></span>

<span data-ttu-id="7bc0c-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="7bc0c-104">**Applies To**</span></span>

- <span data-ttu-id="7bc0c-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="7bc0c-105">Partner Center</span></span>

<span data-ttu-id="7bc0c-106">Jak zaktualizować zamówienie dla klienta w koszyku.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-106">How to update an order for a customer in a cart.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7bc0c-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7bc0c-107">Prerequisites</span></span>

- <span data-ttu-id="7bc0c-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7bc0c-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7bc0c-109">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7bc0c-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7bc0c-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7bc0c-111">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7bc0c-112">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7bc0c-113">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7bc0c-114">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="7bc0c-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7bc0c-115">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7bc0c-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="7bc0c-116">Identyfikator koszyka dla istniejącego koszyka.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-116">A Cart ID for an existing cart.</span></span>

## <a name="c"></a><span data-ttu-id="7bc0c-117">C\#</span><span class="sxs-lookup"><span data-stu-id="7bc0c-117">C\#</span></span>

<span data-ttu-id="7bc0c-118">Aby zaktualizować zamówienie dla klienta, należy uzyskać koszyk przy użyciu metody **Get ()** przez przekazanie identyfikatora klienta i koszyka przy użyciu funkcji **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="7bc0c-118">To update an order for a customer, get the cart using the **Get()** method by passing the customer and cart ID's using the **ById()** function.</span></span> <span data-ttu-id="7bc0c-119">Wprowadź niezbędne zmiany w koszyku.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-119">Make the necessary changes to the cart.</span></span> <span data-ttu-id="7bc0c-120">Teraz Wywołaj metodę **Put** przy użyciu identyfikatora klienta i koszyka przy użyciu metody **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="7bc0c-120">Now call the **Put** method by using customer and cart ID's using the **ById()** method.</span></span>

<span data-ttu-id="7bc0c-121">Na koniec Wywołaj metodę **Put ()** lub **PutAsync ()** , aby utworzyć zamówienie.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-121">Finally, call the **Put()** or **PutAsync()** method to create the order.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="rest-request"></a><span data-ttu-id="7bc0c-122">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="7bc0c-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7bc0c-123">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="7bc0c-123">Request syntax</span></span>

| <span data-ttu-id="7bc0c-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="7bc0c-124">Method</span></span>  | <span data-ttu-id="7bc0c-125">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="7bc0c-125">Request URI</span></span>                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7bc0c-126">**PUT**</span><span class="sxs-lookup"><span data-stu-id="7bc0c-126">**PUT**</span></span> | <span data-ttu-id="7bc0c-127">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/Carts/{Cart-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="7bc0c-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1</span></span>              |

### <a name="uri-parameters"></a><span data-ttu-id="7bc0c-128">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="7bc0c-128">URI parameters</span></span>

<span data-ttu-id="7bc0c-129">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i określić koszyk do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-129">Use the following path parameters to identify the customer, and specify the cart to be updated.</span></span>

| <span data-ttu-id="7bc0c-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="7bc0c-130">Name</span></span>            | <span data-ttu-id="7bc0c-131">Typ</span><span class="sxs-lookup"><span data-stu-id="7bc0c-131">Type</span></span>     | <span data-ttu-id="7bc0c-132">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7bc0c-132">Required</span></span> | <span data-ttu-id="7bc0c-133">Opis</span><span class="sxs-lookup"><span data-stu-id="7bc0c-133">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="7bc0c-134">**Identyfikator klienta**</span><span class="sxs-lookup"><span data-stu-id="7bc0c-134">**customer-id**</span></span> | <span data-ttu-id="7bc0c-135">ciąg</span><span class="sxs-lookup"><span data-stu-id="7bc0c-135">string</span></span>   | <span data-ttu-id="7bc0c-136">Tak</span><span class="sxs-lookup"><span data-stu-id="7bc0c-136">Yes</span></span>      | <span data-ttu-id="7bc0c-137">Identyfikator GUID sformatowany przez klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-137">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="7bc0c-138">**Identyfikator koszyka**</span><span class="sxs-lookup"><span data-stu-id="7bc0c-138">**cart-id**</span></span>     | <span data-ttu-id="7bc0c-139">ciąg</span><span class="sxs-lookup"><span data-stu-id="7bc0c-139">string</span></span>   | <span data-ttu-id="7bc0c-140">Tak</span><span class="sxs-lookup"><span data-stu-id="7bc0c-140">Yes</span></span>      | <span data-ttu-id="7bc0c-141">Identyfikator koszyka w formacie GUID, który identyfikuje koszyk.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-141">A GUID formatted cart-id that identifies the cart.</span></span>                     |

### <a name="request-headers"></a><span data-ttu-id="7bc0c-142">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="7bc0c-142">Request headers</span></span>

<span data-ttu-id="7bc0c-143">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7bc0c-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7bc0c-144">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="7bc0c-144">Request body</span></span>

<span data-ttu-id="7bc0c-145">W tej tabeli opisano właściwości [koszyka](cart-resources.md) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-145">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="7bc0c-146">Właściwość</span><span class="sxs-lookup"><span data-stu-id="7bc0c-146">Property</span></span>              | <span data-ttu-id="7bc0c-147">Typ</span><span class="sxs-lookup"><span data-stu-id="7bc0c-147">Type</span></span>             | <span data-ttu-id="7bc0c-148">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7bc0c-148">Required</span></span>        | <span data-ttu-id="7bc0c-149">Opis</span><span class="sxs-lookup"><span data-stu-id="7bc0c-149">Description</span></span>                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7bc0c-150">identyfikator</span><span class="sxs-lookup"><span data-stu-id="7bc0c-150">id</span></span>                    | <span data-ttu-id="7bc0c-151">ciąg</span><span class="sxs-lookup"><span data-stu-id="7bc0c-151">string</span></span>           | <span data-ttu-id="7bc0c-152">Nie</span><span class="sxs-lookup"><span data-stu-id="7bc0c-152">No</span></span>              | <span data-ttu-id="7bc0c-153">Identyfikator koszyka, który jest dostarczany po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-153">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="7bc0c-154">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="7bc0c-154">creationTimeStamp</span></span>     | <span data-ttu-id="7bc0c-155">DateTime</span><span class="sxs-lookup"><span data-stu-id="7bc0c-155">DateTime</span></span>         | <span data-ttu-id="7bc0c-156">Nie</span><span class="sxs-lookup"><span data-stu-id="7bc0c-156">No</span></span>              | <span data-ttu-id="7bc0c-157">Data i godzina utworzenia koszyka.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-157">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="7bc0c-158">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-158">Applied upon successful creation of the cart.</span></span>        |
| <span data-ttu-id="7bc0c-159">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="7bc0c-159">lastModifiedTimeStamp</span></span> | <span data-ttu-id="7bc0c-160">DateTime</span><span class="sxs-lookup"><span data-stu-id="7bc0c-160">DateTime</span></span>         | <span data-ttu-id="7bc0c-161">Nie</span><span class="sxs-lookup"><span data-stu-id="7bc0c-161">No</span></span>              | <span data-ttu-id="7bc0c-162">Data ostatniej aktualizacji koszyka w formacie daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-162">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="7bc0c-163">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-163">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="7bc0c-164">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="7bc0c-164">expirationTimeStamp</span></span>   | <span data-ttu-id="7bc0c-165">DateTime</span><span class="sxs-lookup"><span data-stu-id="7bc0c-165">DateTime</span></span>         | <span data-ttu-id="7bc0c-166">Nie</span><span class="sxs-lookup"><span data-stu-id="7bc0c-166">No</span></span>              | <span data-ttu-id="7bc0c-167">Data wygaśnięcia koszyka w formacie daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-167">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="7bc0c-168">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-168">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="7bc0c-169">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="7bc0c-169">lastModifiedUser</span></span>      | <span data-ttu-id="7bc0c-170">ciąg</span><span class="sxs-lookup"><span data-stu-id="7bc0c-170">string</span></span>           | <span data-ttu-id="7bc0c-171">Nie</span><span class="sxs-lookup"><span data-stu-id="7bc0c-171">No</span></span>              | <span data-ttu-id="7bc0c-172">Użytkownik, który ostatnio zaktualizował koszyk.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-172">The user who last updated the cart.</span></span> <span data-ttu-id="7bc0c-173">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-173">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="7bc0c-174">lineItems</span><span class="sxs-lookup"><span data-stu-id="7bc0c-174">lineItems</span></span>             | <span data-ttu-id="7bc0c-175">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="7bc0c-175">Array of objects</span></span> | <span data-ttu-id="7bc0c-176">Tak</span><span class="sxs-lookup"><span data-stu-id="7bc0c-176">Yes</span></span>             | <span data-ttu-id="7bc0c-177">Tablica zasobów [CartLineItem](cart-resources.md#cartlineitem) .</span><span class="sxs-lookup"><span data-stu-id="7bc0c-177">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                               |

<span data-ttu-id="7bc0c-178">W tej tabeli opisano właściwości [CartLineItem](cart-resources.md#cartlineitem) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-178">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

| <span data-ttu-id="7bc0c-179">Właściwość</span><span class="sxs-lookup"><span data-stu-id="7bc0c-179">Property</span></span>             | <span data-ttu-id="7bc0c-180">Typ</span><span class="sxs-lookup"><span data-stu-id="7bc0c-180">Type</span></span>                        | <span data-ttu-id="7bc0c-181">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7bc0c-181">Required</span></span>     | <span data-ttu-id="7bc0c-182">Opis</span><span class="sxs-lookup"><span data-stu-id="7bc0c-182">Description</span></span>                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7bc0c-183">identyfikator</span><span class="sxs-lookup"><span data-stu-id="7bc0c-183">id</span></span>                   | <span data-ttu-id="7bc0c-184">ciąg</span><span class="sxs-lookup"><span data-stu-id="7bc0c-184">string</span></span>                      | <span data-ttu-id="7bc0c-185">Nie</span><span class="sxs-lookup"><span data-stu-id="7bc0c-185">No</span></span>           | <span data-ttu-id="7bc0c-186">Unikatowy identyfikator dla elementu w wierszu koszyka.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-186">A Unique identifier for a cart line item.</span></span> <span data-ttu-id="7bc0c-187">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-187">Applied upon successful creation of cart.</span></span>                |
| <span data-ttu-id="7bc0c-188">catalogId</span><span class="sxs-lookup"><span data-stu-id="7bc0c-188">catalogId</span></span>            | <span data-ttu-id="7bc0c-189">ciąg</span><span class="sxs-lookup"><span data-stu-id="7bc0c-189">string</span></span>                      | <span data-ttu-id="7bc0c-190">Tak</span><span class="sxs-lookup"><span data-stu-id="7bc0c-190">Yes</span></span>          | <span data-ttu-id="7bc0c-191">Identyfikator elementu katalogu.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-191">The catalog item identifier.</span></span>                                                                       |
| <span data-ttu-id="7bc0c-192">friendlyName</span><span class="sxs-lookup"><span data-stu-id="7bc0c-192">friendlyName</span></span>         | <span data-ttu-id="7bc0c-193">ciąg</span><span class="sxs-lookup"><span data-stu-id="7bc0c-193">string</span></span>                      | <span data-ttu-id="7bc0c-194">Nie</span><span class="sxs-lookup"><span data-stu-id="7bc0c-194">No</span></span>           | <span data-ttu-id="7bc0c-195">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-195">Optional.</span></span> <span data-ttu-id="7bc0c-196">Przyjazna nazwa dla elementu zdefiniowanego przez partnera, która pomaga w odróżnieniu od siebie.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-196">The friendly name for the item defined by the partner to help disambiguate.</span></span>              |
| <span data-ttu-id="7bc0c-197">quantity</span><span class="sxs-lookup"><span data-stu-id="7bc0c-197">quantity</span></span>             | <span data-ttu-id="7bc0c-198">int</span><span class="sxs-lookup"><span data-stu-id="7bc0c-198">int</span></span>                         | <span data-ttu-id="7bc0c-199">Tak</span><span class="sxs-lookup"><span data-stu-id="7bc0c-199">Yes</span></span>          | <span data-ttu-id="7bc0c-200">Liczba licencji lub wystąpień.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-200">The number of licenses or instances.</span></span>     |
| <span data-ttu-id="7bc0c-201">currencyCode</span><span class="sxs-lookup"><span data-stu-id="7bc0c-201">currencyCode</span></span>         | <span data-ttu-id="7bc0c-202">ciąg</span><span class="sxs-lookup"><span data-stu-id="7bc0c-202">string</span></span>                      | <span data-ttu-id="7bc0c-203">Nie</span><span class="sxs-lookup"><span data-stu-id="7bc0c-203">No</span></span>           | <span data-ttu-id="7bc0c-204">Kod waluty.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-204">The currency code.</span></span>                                                                                 |
| <span data-ttu-id="7bc0c-205">billingCycle</span><span class="sxs-lookup"><span data-stu-id="7bc0c-205">billingCycle</span></span>         | <span data-ttu-id="7bc0c-206">Obiekt</span><span class="sxs-lookup"><span data-stu-id="7bc0c-206">Object</span></span>                      | <span data-ttu-id="7bc0c-207">Tak</span><span class="sxs-lookup"><span data-stu-id="7bc0c-207">Yes</span></span>          | <span data-ttu-id="7bc0c-208">Typ cyklu rozliczeniowego ustawiony dla bieżącego okresu.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-208">The type of billing cycle set for the current period.</span></span>                                              |
| <span data-ttu-id="7bc0c-209">uczestnicy</span><span class="sxs-lookup"><span data-stu-id="7bc0c-209">participants</span></span>         | <span data-ttu-id="7bc0c-210">Lista par ciągów obiektów</span><span class="sxs-lookup"><span data-stu-id="7bc0c-210">List of Object String pairs</span></span> | <span data-ttu-id="7bc0c-211">Nie</span><span class="sxs-lookup"><span data-stu-id="7bc0c-211">No</span></span>           | <span data-ttu-id="7bc0c-212">Kolekcja uczestników zakupu.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-212">A collection of participants on the purchase.</span></span>                                                      |
| <span data-ttu-id="7bc0c-213">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="7bc0c-213">provisioningContext</span></span>  | <span data-ttu-id="7bc0c-214">Ciąg<słownika, ciąg></span><span class="sxs-lookup"><span data-stu-id="7bc0c-214">Dictionary<string, string></span></span>  | <span data-ttu-id="7bc0c-215">Nie</span><span class="sxs-lookup"><span data-stu-id="7bc0c-215">No</span></span>           | <span data-ttu-id="7bc0c-216">Kontekst używany do aprowizacji oferty.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-216">A context used for provisioning of offer.</span></span>                                                          |
| <span data-ttu-id="7bc0c-217">kolejność</span><span class="sxs-lookup"><span data-stu-id="7bc0c-217">orderGroup</span></span>           | <span data-ttu-id="7bc0c-218">ciąg</span><span class="sxs-lookup"><span data-stu-id="7bc0c-218">string</span></span>                      | <span data-ttu-id="7bc0c-219">Nie</span><span class="sxs-lookup"><span data-stu-id="7bc0c-219">No</span></span>           | <span data-ttu-id="7bc0c-220">Grupa wskazująca, które elementy mogą być umieszczone razem.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-220">A group to indicate which items can be placed together.</span></span>                                            |
| <span data-ttu-id="7bc0c-221">error</span><span class="sxs-lookup"><span data-stu-id="7bc0c-221">error</span></span>                | <span data-ttu-id="7bc0c-222">Obiekt</span><span class="sxs-lookup"><span data-stu-id="7bc0c-222">Object</span></span>                      | <span data-ttu-id="7bc0c-223">Nie</span><span class="sxs-lookup"><span data-stu-id="7bc0c-223">No</span></span>           | <span data-ttu-id="7bc0c-224">Zastosowano po utworzeniu koszyka w przypadku błędu.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-224">Applied after cart is created in case of an error.</span></span>                                                 |

### <a name="request-example"></a><span data-ttu-id="7bc0c-225">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="7bc0c-225">Request example</span></span>

```http
PUT /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/65faf57b-0205-47ee-92b3-08dcf233ea73/ HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 496
Expect: 100-continue

{
    {
        "Id":"b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
        "CreationTimestamp":"2018-03-15T17:15:02.3840528Z",
        "LastModifiedTimestamp":"2018-03-15T17:15:02.3840528Z",
        "ExpirationTimestamp":"0001-01-01T00:00:00",
        "LastModifiedUser":"2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
        "LineItems":[
            {
                "Id":0,
                "CatalogItemId":"DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
                "FriendlyName":"A_sample_Azure_RI",
                "Quantity":2,
                "BillingCycle":"one_time",
                "ProvisioningContext": {
                    "SubscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                    "Scope": "shared",
                    "Duration": "1Year"
                }
            }
        ],
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="7bc0c-226">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="7bc0c-226">REST response</span></span>

<span data-ttu-id="7bc0c-227">Jeśli to się powiedzie, ta metoda zwraca zasób [koszyka](cart-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-227">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7bc0c-228">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7bc0c-228">Response success and error codes</span></span>

<span data-ttu-id="7bc0c-229">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-229">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7bc0c-230">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="7bc0c-230">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7bc0c-231">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7bc0c-231">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7bc0c-232">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7bc0c-232">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
{
    "id": "b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
    "creationTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedUser": "2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
    "lineItems": [
        {
            "id": 0,
            "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
            "friendlyName": "A_sample_Azure_RI",
            "quantity": 2,
            "currencyCode": "USD",
            "billingCycle": "one_time",
            "ProvisioningContext": {
                "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                "scope": "shared",
                "duration": "1Year"
            }
            "orderGroup": "0"
        }
    ],
    "links": {
        "self": {
            "uri": "/v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Cart"
    }
}
```
