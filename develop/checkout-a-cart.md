---
title: Finalizacja zakupu koszyka
description: Dowiedz się, jak sprawdzić zamówienie klienta w koszyku przy użyciu interfejsów API Centrum partnerskiego. Możesz to zrobić, aby zakończyć zamówienie klienta.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 094817a34cd29bc96788fcfb6a16610a8192d784
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768594"
---
# <a name="checkout-an-order-for-a-customer-in-a-cart"></a><span data-ttu-id="5add9-104">Wyewidencjonowywanie zamówienia dla klienta w koszyku</span><span class="sxs-lookup"><span data-stu-id="5add9-104">Checkout an order for a customer in a cart</span></span>

<span data-ttu-id="5add9-105">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="5add9-105">**Applies to:**</span></span>

- <span data-ttu-id="5add9-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="5add9-106">Partner Center</span></span>
- <span data-ttu-id="5add9-107">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="5add9-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="5add9-108">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="5add9-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="5add9-109">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="5add9-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5add9-110">Jak wyewidencjonować zamówienie dla klienta w koszyku.</span><span class="sxs-lookup"><span data-stu-id="5add9-110">How to checkout an order for a customer in a cart.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5add9-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5add9-111">Prerequisites</span></span>

- <span data-ttu-id="5add9-112">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5add9-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5add9-113">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5add9-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5add9-114">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5add9-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5add9-115">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="5add9-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5add9-116">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="5add9-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5add9-117">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="5add9-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5add9-118">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="5add9-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5add9-119">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5add9-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="5add9-120">Identyfikator koszyka dla istniejącego koszyka.</span><span class="sxs-lookup"><span data-stu-id="5add9-120">A Cart ID for an existing cart.</span></span>

## <a name="c"></a><span data-ttu-id="5add9-121">C\#</span><span class="sxs-lookup"><span data-stu-id="5add9-121">C\#</span></span>

<span data-ttu-id="5add9-122">Aby wyewidencjonować zamówienie dla klienta, Uzyskaj odwołanie do koszyka przy użyciu identyfikatora koszyka i klienta.</span><span class="sxs-lookup"><span data-stu-id="5add9-122">To checkout an order for a customer, get a reference to the cart using the cart and customer identifier.</span></span> <span data-ttu-id="5add9-123">Na koniec Wywołaj funkcje **Create** lub **setasync** , aby zakończyć zamówienie.</span><span class="sxs-lookup"><span data-stu-id="5add9-123">Finally, call the **Create** or **CreateAsync** functions to complete the order.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Checkout();
```

## <a name="java"></a><span data-ttu-id="5add9-124">Java</span><span class="sxs-lookup"><span data-stu-id="5add9-124">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

<span data-ttu-id="5add9-125">Aby wyewidencjonować zamówienie dla klienta, Uzyskaj odwołanie do koszyka przy użyciu identyfikatora koszyka i klienta.</span><span class="sxs-lookup"><span data-stu-id="5add9-125">To checkout an order for a customer, get a reference to the cart using the cart and customer identifier.</span></span> <span data-ttu-id="5add9-126">Na koniec wywołaj funkcję **Create** , aby zakończyć zamówienie.</span><span class="sxs-lookup"><span data-stu-id="5add9-126">Finally, call the **create** function to complete the order.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String cartId;

Cart cart = partnerOperations.getCustomers().byId(customerId).getCart().byId(cartId).checkout();
```

## <a name="powershell"></a><span data-ttu-id="5add9-127">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5add9-127">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

<span data-ttu-id="5add9-128">Aby wyewidencjonować zamówienie dla klienta, wykonaj polecenie [**Submit-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Submit-PartnerCustomerCart.md) , aby zakończyć zamówienie.</span><span class="sxs-lookup"><span data-stu-id="5add9-128">To checkout an order for a customer, execute the [**Submit-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Submit-PartnerCustomerCart.md) to complete the order.</span></span>

```powershell
# $customerId
# $cartId

Submit-PartnerCustomerCart -CartId $cartId -CustomerId $customerId
```

## <a name="rest-request"></a><span data-ttu-id="5add9-129">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="5add9-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5add9-130">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="5add9-130">Request syntax</span></span>

| <span data-ttu-id="5add9-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="5add9-131">Method</span></span>   | <span data-ttu-id="5add9-132">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="5add9-132">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5add9-133">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="5add9-133">**POST**</span></span> | <span data-ttu-id="5add9-134">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/Carts/{Cart-ID}/Checkout http/1.1</span><span class="sxs-lookup"><span data-stu-id="5add9-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id}/checkout HTTP/1.1</span></span>     |

### <a name="uri-parameters"></a><span data-ttu-id="5add9-135">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="5add9-135">URI parameters</span></span>

<span data-ttu-id="5add9-136">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i określić koszyk, który ma zostać wyewidencjonowany.</span><span class="sxs-lookup"><span data-stu-id="5add9-136">Use the following path parameters to identify the customer and specify the cart to be checked out.</span></span>

| <span data-ttu-id="5add9-137">Nazwa</span><span class="sxs-lookup"><span data-stu-id="5add9-137">Name</span></span>            | <span data-ttu-id="5add9-138">Typ</span><span class="sxs-lookup"><span data-stu-id="5add9-138">Type</span></span>     | <span data-ttu-id="5add9-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="5add9-139">Required</span></span> | <span data-ttu-id="5add9-140">Opis</span><span class="sxs-lookup"><span data-stu-id="5add9-140">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="5add9-141">**Identyfikator klienta**</span><span class="sxs-lookup"><span data-stu-id="5add9-141">**customer-id**</span></span> | <span data-ttu-id="5add9-142">ciąg</span><span class="sxs-lookup"><span data-stu-id="5add9-142">string</span></span>   | <span data-ttu-id="5add9-143">Tak</span><span class="sxs-lookup"><span data-stu-id="5add9-143">Yes</span></span>      | <span data-ttu-id="5add9-144">Identyfikator GUID sformatowany przez klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="5add9-144">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="5add9-145">**Identyfikator koszyka**</span><span class="sxs-lookup"><span data-stu-id="5add9-145">**cart-id**</span></span>     | <span data-ttu-id="5add9-146">ciąg</span><span class="sxs-lookup"><span data-stu-id="5add9-146">string</span></span>   | <span data-ttu-id="5add9-147">Tak</span><span class="sxs-lookup"><span data-stu-id="5add9-147">Yes</span></span>      | <span data-ttu-id="5add9-148">Identyfikator koszyka w formacie GUID, który identyfikuje koszyk.</span><span class="sxs-lookup"><span data-stu-id="5add9-148">A GUID formatted cart-id that identifies the cart.</span></span>                     |

### <a name="request-headers"></a><span data-ttu-id="5add9-149">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="5add9-149">Request headers</span></span>

<span data-ttu-id="5add9-150">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5add9-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5add9-151">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="5add9-151">Request body</span></span>

<span data-ttu-id="5add9-152">Brak.</span><span class="sxs-lookup"><span data-stu-id="5add9-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5add9-153">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="5add9-153">Request example</span></span>

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605/checkout HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 0
Expect: 100-continue

No-Content-Body
```

## <a name="rest-response"></a><span data-ttu-id="5add9-154">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="5add9-154">REST response</span></span>

<span data-ttu-id="5add9-155">Jeśli to się powiedzie, treść odpowiedzi zawiera wypełniony zasób [CartCheckoutResult](cart-resources.md#cartcheckoutresult) .</span><span class="sxs-lookup"><span data-stu-id="5add9-155">If successful, the response body contains the populated [CartCheckoutResult](cart-resources.md#cartcheckoutresult) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5add9-156">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="5add9-156">Response success and error codes</span></span>

<span data-ttu-id="5add9-157">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="5add9-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5add9-158">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="5add9-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5add9-159">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5add9-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5add9-160">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="5add9-160">Response example</span></span>

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
?{
  "orders": [
    {
      "id": "3c6f2530-1e31-4088-8230-dd1c31a18bce",
      "alternateId": "3c6f2530-1e31-4088-8230-dd1c31a18bce",
      "referenceCustomerId": "28045616-f6b9-462f-9701-0d89b5e65c44",
      "billingCycle": "monthly",
      "currencyCode": "USD",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "MS-AZR-0145P",
          "subscriptionId": "EF2E1307-86E6-40E3-A794-872403FBD31C",
          "termDuration": "P1Y",
          "transactionType": "New",
          "friendlyName": "Microsoft Azure",
          "quantity": 1,
          "links": {...}
        }
      ],
      "creationDate": "2019-01-16T00:48:44.76+00:00",
      "status": "completed",
      "transactionType": "UserPurchase",
      "links": {...},
      ...
    },
    {
      "id": "311qiN8iFwkv-XARWMvXRYAwYKMACVqv1",
      "alternateId": "0a3624c6e47d",
      "referenceCustomerId": "28045616-f6b9-462f-9701-0d89b5e65c44",
      "billingCycle": "one_time",
      "currencyCode": "USD",
      "currencySymbol": "$",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
          "termDuration": "P1Y",
          "transactionType": "New",
          "friendlyName": "Reserved VM Instance, Standard_NV12, US East 2, 1 Year",
          "quantity": 1,
          "links": {...}
        },
        {
          "lineItemNumber": 1,
          "offerId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
          "termDuration": "P3Y",
          "transactionType": "New",
          "friendlyName": "Reserved VM Instance, Standard_NV12, US East 2, 3 Years",
          "quantity": 1,
          "links": {...}
        },
        {
          "lineItemNumber": 2,
          "offerId": "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
          "transactionType": "New",
          "friendlyName": "BizTalk Server 2016 Branch",
          "quantity": 1,
          "links": {...}
        }
      ],
      "creationDate": "2019-01-16T00:48:51.6578126Z",
      "status": "pending",
      "transactionType": "UserPurchase",
      "links": {...},
      ...
    },
    {
      "id": "HVu_cO8Ea7fNRQP4ia1QTpZap-kg_7P71",
      "alternateId": "55a4e6854d54",
      "referenceCustomerId": "28045616-f6b9-462f-9701-0d89b5e65c44",
      "billingCycle": "monthly",
      "currencyCode": "USD",
      "currencySymbol": "$",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
          "termDuration": "P1M",
          "transactionType": "New",
          "friendlyName": "Barracuda WaaS - Medium Plan",
          "quantity": 1,
          "links": {...}
        }
      ],
      "creationDate": "2019-01-16T00:48:44.4514129Z",
      "status": "pending",
      "transactionType": "UserPurchase",
      "links": {...},
      ...
    }
  ],
  ...
}
```
