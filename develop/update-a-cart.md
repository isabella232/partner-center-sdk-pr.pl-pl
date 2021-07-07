---
title: Aktualizowanie koszyka
description: Jak zaktualizować zamówienie klienta w koszyku.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8954d4dad39f9b1a1b9a2f213e0231f01856fcd2
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446687"
---
# <a name="update-a-cart"></a><span data-ttu-id="2f3a5-103">Aktualizowanie koszyka</span><span class="sxs-lookup"><span data-stu-id="2f3a5-103">Update a cart</span></span>

<span data-ttu-id="2f3a5-104">Jak zaktualizować zamówienie klienta w koszyku.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-104">How to update an order for a customer in a cart.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f3a5-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2f3a5-105">Prerequisites</span></span>

- <span data-ttu-id="2f3a5-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2f3a5-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2f3a5-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="2f3a5-108">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2f3a5-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2f3a5-109">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="2f3a5-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2f3a5-110">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="2f3a5-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2f3a5-111">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2f3a5-112">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2f3a5-113">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2f3a5-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="2f3a5-114">Identyfikator koszyka dla istniejącego koszyka.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-114">A Cart ID for an existing cart.</span></span>

## <a name="c"></a><span data-ttu-id="2f3a5-115">C\#</span><span class="sxs-lookup"><span data-stu-id="2f3a5-115">C\#</span></span>

<span data-ttu-id="2f3a5-116">Aby zaktualizować zamówienie klienta, pobierz koszyk przy użyciu metody **Get(),** przekazując identyfikatory klienta i koszyka przy użyciu **funkcji ById().**</span><span class="sxs-lookup"><span data-stu-id="2f3a5-116">To update an order for a customer, get the cart using the **Get()** method by passing the customer and cart IDs using the **ById()** function.</span></span> <span data-ttu-id="2f3a5-117">Wprowadzić niezbędne zmiany w koszyku.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-117">Make the necessary changes to the cart.</span></span> <span data-ttu-id="2f3a5-118">Teraz wywołaj **metodę Put** przy użyciu identyfikatorów klientów i koszyka przy użyciu **metody ById().**</span><span class="sxs-lookup"><span data-stu-id="2f3a5-118">Now call the **Put** method by using customer and cart IDs using the **ById()** method.</span></span>

<span data-ttu-id="2f3a5-119">Na koniec wywołaj **metodę Put()** lub **PutAsync(),** aby utworzyć zamówienie.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-119">Finally, call the **Put()** or **PutAsync()** method to create the order.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="rest-request"></a><span data-ttu-id="2f3a5-120">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="2f3a5-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2f3a5-121">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="2f3a5-121">Request syntax</span></span>

| <span data-ttu-id="2f3a5-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="2f3a5-122">Method</span></span>  | <span data-ttu-id="2f3a5-123">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="2f3a5-123">Request URI</span></span>                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2f3a5-124">**PUT**</span><span class="sxs-lookup"><span data-stu-id="2f3a5-124">**PUT**</span></span> | <span data-ttu-id="2f3a5-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2f3a5-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1</span></span>              |

### <a name="uri-parameters"></a><span data-ttu-id="2f3a5-126">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="2f3a5-126">URI parameters</span></span>

<span data-ttu-id="2f3a5-127">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i określić koszyk do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-127">Use the following path parameters to identify the customer, and specify the cart to be updated.</span></span>

| <span data-ttu-id="2f3a5-128">Nazwa</span><span class="sxs-lookup"><span data-stu-id="2f3a5-128">Name</span></span>            | <span data-ttu-id="2f3a5-129">Typ</span><span class="sxs-lookup"><span data-stu-id="2f3a5-129">Type</span></span>     | <span data-ttu-id="2f3a5-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2f3a5-130">Required</span></span> | <span data-ttu-id="2f3a5-131">Opis</span><span class="sxs-lookup"><span data-stu-id="2f3a5-131">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="2f3a5-132">**identyfikator klienta**</span><span class="sxs-lookup"><span data-stu-id="2f3a5-132">**customer-id**</span></span> | <span data-ttu-id="2f3a5-133">ciąg</span><span class="sxs-lookup"><span data-stu-id="2f3a5-133">string</span></span>   | <span data-ttu-id="2f3a5-134">Tak</span><span class="sxs-lookup"><span data-stu-id="2f3a5-134">Yes</span></span>      | <span data-ttu-id="2f3a5-135">Identyfikator klienta sformatowany w formacie GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-135">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="2f3a5-136">**cart-id**</span><span class="sxs-lookup"><span data-stu-id="2f3a5-136">**cart-id**</span></span>     | <span data-ttu-id="2f3a5-137">ciąg</span><span class="sxs-lookup"><span data-stu-id="2f3a5-137">string</span></span>   | <span data-ttu-id="2f3a5-138">Tak</span><span class="sxs-lookup"><span data-stu-id="2f3a5-138">Yes</span></span>      | <span data-ttu-id="2f3a5-139">Identyfikator GUID w formacie cart-id, który identyfikuje koszyk.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-139">A GUID formatted cart-id that identifies the cart.</span></span>                     |

### <a name="request-headers"></a><span data-ttu-id="2f3a5-140">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="2f3a5-140">Request headers</span></span>

<span data-ttu-id="2f3a5-141">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2f3a5-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2f3a5-142">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="2f3a5-142">Request body</span></span>

<span data-ttu-id="2f3a5-143">W tej tabeli [opisano](cart-resources.md) właściwości koszyka w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-143">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="2f3a5-144">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2f3a5-144">Property</span></span>              | <span data-ttu-id="2f3a5-145">Typ</span><span class="sxs-lookup"><span data-stu-id="2f3a5-145">Type</span></span>             | <span data-ttu-id="2f3a5-146">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2f3a5-146">Required</span></span>        | <span data-ttu-id="2f3a5-147">Opis</span><span class="sxs-lookup"><span data-stu-id="2f3a5-147">Description</span></span>                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2f3a5-148">identyfikator</span><span class="sxs-lookup"><span data-stu-id="2f3a5-148">id</span></span>                    | <span data-ttu-id="2f3a5-149">ciąg</span><span class="sxs-lookup"><span data-stu-id="2f3a5-149">string</span></span>           | <span data-ttu-id="2f3a5-150">Nie</span><span class="sxs-lookup"><span data-stu-id="2f3a5-150">No</span></span>              | <span data-ttu-id="2f3a5-151">Identyfikator koszyka, który jest dostarczany po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-151">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="2f3a5-152">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="2f3a5-152">creationTimeStamp</span></span>     | <span data-ttu-id="2f3a5-153">DateTime</span><span class="sxs-lookup"><span data-stu-id="2f3a5-153">DateTime</span></span>         | <span data-ttu-id="2f3a5-154">Nie</span><span class="sxs-lookup"><span data-stu-id="2f3a5-154">No</span></span>              | <span data-ttu-id="2f3a5-155">Data utworzenia koszyka w formacie data/godzina.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-155">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="2f3a5-156">Zastosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-156">Applied upon successful creation of the cart.</span></span>        |
| <span data-ttu-id="2f3a5-157">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="2f3a5-157">lastModifiedTimeStamp</span></span> | <span data-ttu-id="2f3a5-158">DateTime</span><span class="sxs-lookup"><span data-stu-id="2f3a5-158">DateTime</span></span>         | <span data-ttu-id="2f3a5-159">Nie</span><span class="sxs-lookup"><span data-stu-id="2f3a5-159">No</span></span>              | <span data-ttu-id="2f3a5-160">Data ostatniej aktualizacji koszyka w formacie data/godzina.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-160">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="2f3a5-161">Zastosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-161">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="2f3a5-162">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="2f3a5-162">expirationTimeStamp</span></span>   | <span data-ttu-id="2f3a5-163">DateTime</span><span class="sxs-lookup"><span data-stu-id="2f3a5-163">DateTime</span></span>         | <span data-ttu-id="2f3a5-164">Nie</span><span class="sxs-lookup"><span data-stu-id="2f3a5-164">No</span></span>              | <span data-ttu-id="2f3a5-165">Data wygaśnięcia koszyka w formacie data/godzina.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-165">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="2f3a5-166">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-166">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="2f3a5-167">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="2f3a5-167">lastModifiedUser</span></span>      | <span data-ttu-id="2f3a5-168">ciąg</span><span class="sxs-lookup"><span data-stu-id="2f3a5-168">string</span></span>           | <span data-ttu-id="2f3a5-169">Nie</span><span class="sxs-lookup"><span data-stu-id="2f3a5-169">No</span></span>              | <span data-ttu-id="2f3a5-170">Użytkownik, który ostatnio zaktualizował koszyk.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-170">The user who last updated the cart.</span></span> <span data-ttu-id="2f3a5-171">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-171">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="2f3a5-172">lineItems</span><span class="sxs-lookup"><span data-stu-id="2f3a5-172">lineItems</span></span>             | <span data-ttu-id="2f3a5-173">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="2f3a5-173">Array of objects</span></span> | <span data-ttu-id="2f3a5-174">Tak</span><span class="sxs-lookup"><span data-stu-id="2f3a5-174">Yes</span></span>             | <span data-ttu-id="2f3a5-175">Tablica [zasobów CartLineItem.](cart-resources.md#cartlineitem)</span><span class="sxs-lookup"><span data-stu-id="2f3a5-175">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                               |

<span data-ttu-id="2f3a5-176">W tej tabeli [opisano właściwości CartLineItem](cart-resources.md#cartlineitem) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-176">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

| <span data-ttu-id="2f3a5-177">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2f3a5-177">Property</span></span>             | <span data-ttu-id="2f3a5-178">Typ</span><span class="sxs-lookup"><span data-stu-id="2f3a5-178">Type</span></span>                        | <span data-ttu-id="2f3a5-179">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2f3a5-179">Required</span></span>     | <span data-ttu-id="2f3a5-180">Opis</span><span class="sxs-lookup"><span data-stu-id="2f3a5-180">Description</span></span>                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2f3a5-181">identyfikator</span><span class="sxs-lookup"><span data-stu-id="2f3a5-181">id</span></span>                   | <span data-ttu-id="2f3a5-182">ciąg</span><span class="sxs-lookup"><span data-stu-id="2f3a5-182">string</span></span>                      | <span data-ttu-id="2f3a5-183">Nie</span><span class="sxs-lookup"><span data-stu-id="2f3a5-183">No</span></span>           | <span data-ttu-id="2f3a5-184">Unikatowy identyfikator elementu wiersza koszyka.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-184">A Unique identifier for a cart line item.</span></span> <span data-ttu-id="2f3a5-185">Stosowane po pomyślnym utworzeniu koszyka.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-185">Applied upon successful creation of cart.</span></span>                |
| <span data-ttu-id="2f3a5-186">catalogId</span><span class="sxs-lookup"><span data-stu-id="2f3a5-186">catalogId</span></span>            | <span data-ttu-id="2f3a5-187">ciąg</span><span class="sxs-lookup"><span data-stu-id="2f3a5-187">string</span></span>                      | <span data-ttu-id="2f3a5-188">Tak</span><span class="sxs-lookup"><span data-stu-id="2f3a5-188">Yes</span></span>          | <span data-ttu-id="2f3a5-189">Identyfikator elementu katalogu.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-189">The catalog item identifier.</span></span>                                                                       |
| <span data-ttu-id="2f3a5-190">Friendlyname</span><span class="sxs-lookup"><span data-stu-id="2f3a5-190">friendlyName</span></span>         | <span data-ttu-id="2f3a5-191">ciąg</span><span class="sxs-lookup"><span data-stu-id="2f3a5-191">string</span></span>                      | <span data-ttu-id="2f3a5-192">Nie</span><span class="sxs-lookup"><span data-stu-id="2f3a5-192">No</span></span>           | <span data-ttu-id="2f3a5-193">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-193">Optional.</span></span> <span data-ttu-id="2f3a5-194">Przyjazna nazwa elementu zdefiniowanego przez partnera w celu uujednoznania.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-194">The friendly name for the item defined by the partner to help disambiguate.</span></span>              |
| <span data-ttu-id="2f3a5-195">quantity</span><span class="sxs-lookup"><span data-stu-id="2f3a5-195">quantity</span></span>             | <span data-ttu-id="2f3a5-196">int</span><span class="sxs-lookup"><span data-stu-id="2f3a5-196">int</span></span>                         | <span data-ttu-id="2f3a5-197">Tak</span><span class="sxs-lookup"><span data-stu-id="2f3a5-197">Yes</span></span>          | <span data-ttu-id="2f3a5-198">Liczba licencji lub wystąpień.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-198">The number of licenses or instances.</span></span>     |
| <span data-ttu-id="2f3a5-199">currencyCode</span><span class="sxs-lookup"><span data-stu-id="2f3a5-199">currencyCode</span></span>         | <span data-ttu-id="2f3a5-200">ciąg</span><span class="sxs-lookup"><span data-stu-id="2f3a5-200">string</span></span>                      | <span data-ttu-id="2f3a5-201">Nie</span><span class="sxs-lookup"><span data-stu-id="2f3a5-201">No</span></span>           | <span data-ttu-id="2f3a5-202">Kod waluty.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-202">The currency code.</span></span>                                                                                 |
| <span data-ttu-id="2f3a5-203">billingCycle</span><span class="sxs-lookup"><span data-stu-id="2f3a5-203">billingCycle</span></span>         | <span data-ttu-id="2f3a5-204">Obiekt</span><span class="sxs-lookup"><span data-stu-id="2f3a5-204">Object</span></span>                      | <span data-ttu-id="2f3a5-205">Tak</span><span class="sxs-lookup"><span data-stu-id="2f3a5-205">Yes</span></span>          | <span data-ttu-id="2f3a5-206">Typ cyklu rozliczeniowego ustawiony dla bieżącego okresu.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-206">The type of billing cycle set for the current period.</span></span>                                              |
| <span data-ttu-id="2f3a5-207">uczestnicy</span><span class="sxs-lookup"><span data-stu-id="2f3a5-207">participants</span></span>         | <span data-ttu-id="2f3a5-208">Lista par ciągów obiektów</span><span class="sxs-lookup"><span data-stu-id="2f3a5-208">List of Object String pairs</span></span> | <span data-ttu-id="2f3a5-209">Nie</span><span class="sxs-lookup"><span data-stu-id="2f3a5-209">No</span></span>           | <span data-ttu-id="2f3a5-210">Kolekcja uczestników zakupu.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-210">A collection of participants on the purchase.</span></span>                                                      |
| <span data-ttu-id="2f3a5-211">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="2f3a5-211">provisioningContext</span></span>  | <span data-ttu-id="2f3a5-212">Ciąg<, ciąg></span><span class="sxs-lookup"><span data-stu-id="2f3a5-212">Dictionary<string, string></span></span>  | <span data-ttu-id="2f3a5-213">Nie</span><span class="sxs-lookup"><span data-stu-id="2f3a5-213">No</span></span>           | <span data-ttu-id="2f3a5-214">Kontekst używany do aprowizowania oferty.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-214">A context used for provisioning of offer.</span></span>                                                          |
| <span data-ttu-id="2f3a5-215">orderGroup</span><span class="sxs-lookup"><span data-stu-id="2f3a5-215">orderGroup</span></span>           | <span data-ttu-id="2f3a5-216">ciąg</span><span class="sxs-lookup"><span data-stu-id="2f3a5-216">string</span></span>                      | <span data-ttu-id="2f3a5-217">Nie</span><span class="sxs-lookup"><span data-stu-id="2f3a5-217">No</span></span>           | <span data-ttu-id="2f3a5-218">Grupa wskazująca, które elementy można ze sobą umieścić.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-218">A group to indicate which items can be placed together.</span></span>                                            |
| <span data-ttu-id="2f3a5-219">error</span><span class="sxs-lookup"><span data-stu-id="2f3a5-219">error</span></span>                | <span data-ttu-id="2f3a5-220">Obiekt</span><span class="sxs-lookup"><span data-stu-id="2f3a5-220">Object</span></span>                      | <span data-ttu-id="2f3a5-221">Nie</span><span class="sxs-lookup"><span data-stu-id="2f3a5-221">No</span></span>           | <span data-ttu-id="2f3a5-222">Zastosowane po utworzeniu koszyka w przypadku wystąpienia błędu.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-222">Applied after cart is created in case of an error.</span></span>                                                 |

### <a name="request-example"></a><span data-ttu-id="2f3a5-223">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="2f3a5-223">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="2f3a5-224">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="2f3a5-224">REST response</span></span>

<span data-ttu-id="2f3a5-225">W przypadku powodzenia ta metoda zwraca wypełniony zasób [koszyka](cart-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-225">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2f3a5-226">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2f3a5-226">Response success and error codes</span></span>

<span data-ttu-id="2f3a5-227">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-227">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2f3a5-228">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="2f3a5-228">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2f3a5-229">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2f3a5-229">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2f3a5-230">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2f3a5-230">Response example</span></span>

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
