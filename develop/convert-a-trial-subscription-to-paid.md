---
title: Konwertowanie wersji próbnej subskrypcji na płatną
description: Dowiedz się, jak używać interfejsów API usługi Partner Center, aby przekonwertować subskrypcję wersji próbnej na płatną.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 59dcf6caf21d407b2fba4cc8438bc435fda9dc77
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768585"
---
# <a name="convert-a-trial-subscription-to-paid-using-partner-center-apis"></a><span data-ttu-id="98ebf-103">Konwertuj subskrypcję wersji próbnej na płatną przy użyciu interfejsów API Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="98ebf-103">Convert a trial subscription to paid using Partner Center APIs</span></span>

<span data-ttu-id="98ebf-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="98ebf-104">**Applies to:**</span></span>

- <span data-ttu-id="98ebf-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="98ebf-105">Partner Center</span></span>

<span data-ttu-id="98ebf-106">Możesz przekonwertować subskrypcję wersji próbnej na płatną.</span><span class="sxs-lookup"><span data-stu-id="98ebf-106">You can convert a trial subscription to paid.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98ebf-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="98ebf-107">Prerequisites</span></span>

- <span data-ttu-id="98ebf-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="98ebf-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="98ebf-109">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="98ebf-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="98ebf-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="98ebf-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="98ebf-111">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="98ebf-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="98ebf-112">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="98ebf-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="98ebf-113">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="98ebf-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="98ebf-114">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="98ebf-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="98ebf-115">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="98ebf-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="98ebf-116">Identyfikator subskrypcji aktywnej subskrypcji próbnej.</span><span class="sxs-lookup"><span data-stu-id="98ebf-116">A subscription ID for an active trial subscription.</span></span>

- <span data-ttu-id="98ebf-117">Dostępna oferta konwersji.</span><span class="sxs-lookup"><span data-stu-id="98ebf-117">An available conversion offer.</span></span>

## <a name="convert-a-trial-subscription-to-paid-through-code"></a><span data-ttu-id="98ebf-118">Konwertuj subskrypcję wersji próbnej na płatną za pomocą kodu</span><span class="sxs-lookup"><span data-stu-id="98ebf-118">Convert a trial subscription to paid through code</span></span>

<span data-ttu-id="98ebf-119">Aby przekonwertować subskrypcję próbną na płatną, należy najpierw uzyskać kolekcję dostępnych konwersji.</span><span class="sxs-lookup"><span data-stu-id="98ebf-119">To convert a trial subscription to a paid one, you must first obtain a collection of the trial conversions available.</span></span> <span data-ttu-id="98ebf-120">Następnie musisz wybrać ofertę konwersji, którą chcesz zakupić.</span><span class="sxs-lookup"><span data-stu-id="98ebf-120">Then, you must choose the conversion offer that you want to purchase.</span></span>

<span data-ttu-id="98ebf-121">Oferty konwersji określają liczbę domyślną dla tej samej liczby licencji co subskrypcja wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="98ebf-121">The conversion offers will specify a quantity that defaults to the same number of licenses as the trial subscription.</span></span> <span data-ttu-id="98ebf-122">Tę ilość można zmienić, ustawiając właściwość [**ilość**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) na liczbę licencji, które chcesz zakupić.</span><span class="sxs-lookup"><span data-stu-id="98ebf-122">You can change this quantity by setting the [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) property to the number of licenses that you want to purchase.</span></span>

> [!NOTE]
> <span data-ttu-id="98ebf-123">Niezależnie od liczby zakupionych licencji Identyfikator subskrypcji wersji próbnej jest ponownie używany w przypadku zakupionych licencji.</span><span class="sxs-lookup"><span data-stu-id="98ebf-123">Regardless of the number of licenses purchased, the subscription ID of the trial is reused for the purchased licenses.</span></span> <span data-ttu-id="98ebf-124">W związku z tym, okres próbny znika i jest zastępowany przez zakup.</span><span class="sxs-lookup"><span data-stu-id="98ebf-124">As a result, the trial in effect disappears and is replaced by the purchase.</span></span>

<span data-ttu-id="98ebf-125">Wykonaj następujące kroki, aby przekonwertować subskrypcję próbną za pomocą kodu:</span><span class="sxs-lookup"><span data-stu-id="98ebf-125">Use the following steps to convert a trial subscription through code:</span></span>

1. <span data-ttu-id="98ebf-126">Uzyskaj interfejs do dostępnych operacji subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="98ebf-126">Get an interface to the subscription operations available.</span></span> <span data-ttu-id="98ebf-127">Należy zidentyfikować klienta i określić identyfikator subskrypcji wersji próbnej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="98ebf-127">You must identify the customer and specify the subscription identifier of the trial subscription.</span></span>

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. <span data-ttu-id="98ebf-128">Pobierz kolekcję dostępnych ofert konwersji.</span><span class="sxs-lookup"><span data-stu-id="98ebf-128">Get a collection of the available conversion offers.</span></span> <span data-ttu-id="98ebf-129">Aby uzyskać więcej informacji i szczegóły dotyczące żądania/odpowiedzi dla tej metody, zobacz [Pobieranie listy ofert konwersji wersji próbnej](get-a-list-of-trial-conversion-offers.md).</span><span class="sxs-lookup"><span data-stu-id="98ebf-129">For more information and details on the request/response for this method, see [Get a list of trial conversion offers](get-a-list-of-trial-conversion-offers.md).</span></span>

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. <span data-ttu-id="98ebf-130">Wybierz ofertę konwersji.</span><span class="sxs-lookup"><span data-stu-id="98ebf-130">Choose a conversion offer.</span></span> <span data-ttu-id="98ebf-131">Poniższy kod wybiera pierwszą ofertę konwersji w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="98ebf-131">The following code chooses the first conversion offer in the collection.</span></span>

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. <span data-ttu-id="98ebf-132">Opcjonalnie możesz określić liczbę licencji do zakupu.</span><span class="sxs-lookup"><span data-stu-id="98ebf-132">Optionally, specify the number of licenses to purchase.</span></span> <span data-ttu-id="98ebf-133">Wartość domyślna to liczba licencji w subskrypcji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="98ebf-133">The default is the number of licenses in the trial subscription.</span></span>

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. <span data-ttu-id="98ebf-134">Wywołaj metodę [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) lub [**onasync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) , aby przekonwertować subskrypcję wersji próbnej na płatne.</span><span class="sxs-lookup"><span data-stu-id="98ebf-134">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) method to convert the trial subscription to paid.</span></span>

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a><span data-ttu-id="98ebf-135">C\#</span><span class="sxs-lookup"><span data-stu-id="98ebf-135">C\#</span></span>

<span data-ttu-id="98ebf-136">Aby przekonwertować subskrypcję próbną na jedną płatną:</span><span class="sxs-lookup"><span data-stu-id="98ebf-136">To convert a trial subscription to a paid one:</span></span>

1. <span data-ttu-id="98ebf-137">Użyj metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="98ebf-137">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="98ebf-138">Uzyskaj interfejs do operacji subskrybowania, wywołując metodę [**Subscription. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem subskrypcji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="98ebf-138">Get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the trial subscription ID.</span></span> <span data-ttu-id="98ebf-139">Zapisz odwołanie do interfejsu operacji subskrypcji w zmiennej lokalnej.</span><span class="sxs-lookup"><span data-stu-id="98ebf-139">Save a reference to the subscription operations interface in a local variable.</span></span>

3. <span data-ttu-id="98ebf-140">Użyj właściwości [**konwersje**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) , aby uzyskać interfejs do dostępnych operacji dla konwersji, a następnie wywołać metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) w celu pobrania kolekcji dostępnych ofert [**konwersji**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) .</span><span class="sxs-lookup"><span data-stu-id="98ebf-140">Use the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve a collection of available [**Conversion**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) offers.</span></span> <span data-ttu-id="98ebf-141">Musisz wybrać jeden z nich.</span><span class="sxs-lookup"><span data-stu-id="98ebf-141">You must choose one.</span></span> <span data-ttu-id="98ebf-142">Poniższy przykład jest wartością domyślną dla pierwszej dostępnej konwersji.</span><span class="sxs-lookup"><span data-stu-id="98ebf-142">The following example defaults to the first conversion available.</span></span>

4. <span data-ttu-id="98ebf-143">Użyj odwołania do interfejsu operacji subskrypcji zapisanego w zmiennej lokalnej i właściwości [**konwersje**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) , aby uzyskać interfejs do dostępnych operacji na konwersji.</span><span class="sxs-lookup"><span data-stu-id="98ebf-143">Use the reference to the subscription operations interface that you saved in a local variable and the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions.</span></span>

5. <span data-ttu-id="98ebf-144">Przekaż wybrany obiekt oferty konwersji do metody [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) lub [**IsAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) w celu próby konwersji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="98ebf-144">Pass the selected conversion offer object to the [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) method to attempt the trial conversion.</span></span>

### <a name="c-example"></a><span data-ttu-id="98ebf-145">\#Przykład C</span><span class="sxs-lookup"><span data-stu-id="98ebf-145">C\# example</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get subscription operations for the trial subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the available conversions.
var conversions = subscriptionOperations.Conversions.Get();

// If there are no conversions available, we&#39;re done.
// Otherwise, convert the trial to the first available conversion offer.
if (conversions.TotalCount <= 0)
{
    System.Console.WriteLine("This subscription has no conversions");
}
else
{
    // Default to the first conversion.
    var selectedConversion = conversions.Items.ToList()[0];

    // Convert the trial and return the result.
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
}
```

## <a name="rest-request"></a><span data-ttu-id="98ebf-146">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="98ebf-146">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="98ebf-147">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="98ebf-147">Request syntax</span></span>

| <span data-ttu-id="98ebf-148">Metoda</span><span class="sxs-lookup"><span data-stu-id="98ebf-148">Method</span></span>   | <span data-ttu-id="98ebf-149">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="98ebf-149">Request URI</span></span>                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="98ebf-150">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="98ebf-150">**POST**</span></span> | <span data-ttu-id="98ebf-151">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/subscriptions/{Subscription-ID}/conversions http/1.1</span><span class="sxs-lookup"><span data-stu-id="98ebf-151">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="98ebf-152">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="98ebf-152">URI parameter</span></span>

<span data-ttu-id="98ebf-153">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i subskrypcję wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="98ebf-153">Use the following path parameters to identify the customer and trial subscription.</span></span>

| <span data-ttu-id="98ebf-154">Nazwa</span><span class="sxs-lookup"><span data-stu-id="98ebf-154">Name</span></span>            | <span data-ttu-id="98ebf-155">Typ</span><span class="sxs-lookup"><span data-stu-id="98ebf-155">Type</span></span>   | <span data-ttu-id="98ebf-156">Wymagane</span><span class="sxs-lookup"><span data-stu-id="98ebf-156">Required</span></span> | <span data-ttu-id="98ebf-157">Opis</span><span class="sxs-lookup"><span data-stu-id="98ebf-157">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="98ebf-158">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="98ebf-158">customer-id</span></span>     | <span data-ttu-id="98ebf-159">ciąg</span><span class="sxs-lookup"><span data-stu-id="98ebf-159">string</span></span> | <span data-ttu-id="98ebf-160">Tak</span><span class="sxs-lookup"><span data-stu-id="98ebf-160">Yes</span></span>      | <span data-ttu-id="98ebf-161">Ciąg w formacie GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="98ebf-161">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="98ebf-162">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="98ebf-162">subscription-id</span></span> | <span data-ttu-id="98ebf-163">ciąg</span><span class="sxs-lookup"><span data-stu-id="98ebf-163">string</span></span> | <span data-ttu-id="98ebf-164">Tak</span><span class="sxs-lookup"><span data-stu-id="98ebf-164">Yes</span></span>      | <span data-ttu-id="98ebf-165">Ciąg w formacie GUID, który identyfikuje subskrypcję wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="98ebf-165">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="98ebf-166">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="98ebf-166">Request headers</span></span>

<span data-ttu-id="98ebf-167">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="98ebf-167">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="98ebf-168">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="98ebf-168">Request body</span></span>

<span data-ttu-id="98ebf-169">W treści żądania musi znajdować się wypełniony zawarty zasób [konwersji](conversions-resources.md#conversion) .</span><span class="sxs-lookup"><span data-stu-id="98ebf-169">A populated [Conversion](conversions-resources.md#conversion) resource must be included in the request body.</span></span>

### <a name="request-example"></a><span data-ttu-id="98ebf-170">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="98ebf-170">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 234
Expect: 100-continue

{
    "OfferId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "TargetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "OrderId": "D51A052E-043C-4A2A-AA37-2BB938CEF6C1",
    "Quantity": 25,
    "BillingCycle": "monthly",
    "Attributes": {
        "ObjectType": "Conversion"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="98ebf-171">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="98ebf-171">REST response</span></span>

<span data-ttu-id="98ebf-172">Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [ConversionResult](conversions-resources.md#conversionresult) .</span><span class="sxs-lookup"><span data-stu-id="98ebf-172">If successful, the response body contains a [ConversionResult](conversions-resources.md#conversionresult) resource.</span></span>

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="98ebf-173">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="98ebf-173">Response success and error codes</span></span>

<span data-ttu-id="98ebf-174">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="98ebf-174">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="98ebf-175">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="98ebf-175">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="98ebf-176">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="98ebf-176">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="98ebf-177">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="98ebf-177">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 211
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CV: kW4GzmhvHEqCq1ls.0
MS-ServerId: 030020643
Date: Thu, 15 Jun 2017 23:10:40 GMT

 {
    "subscriptionId": "488745B5-2086-4912-802C-6ABB9F7C3638",
    "offerId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "targetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "attributes": {
        "objectType": "ConversionResult"
    }
}
```
