---
title: Konwertowanie wersji próbnej subskrypcji na płatną
description: Dowiedz się, jak za pomocą Partner Center API przekonwertować subskrypcję wersji próbnej na płatną.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1876cfc796b683bfff00b7d137bcfe0b7162c78
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973863"
---
# <a name="convert-a-trial-subscription-to-paid-using-partner-center-apis"></a><span data-ttu-id="6c131-103">Konwertowanie subskrypcji próbnej na płatną przy użyciu Partner Center API</span><span class="sxs-lookup"><span data-stu-id="6c131-103">Convert a trial subscription to paid using Partner Center APIs</span></span>

<span data-ttu-id="6c131-104">Subskrypcję wersji próbnej można przekonwertować na płatną.</span><span class="sxs-lookup"><span data-stu-id="6c131-104">You can convert a trial subscription to paid.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c131-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6c131-105">Prerequisites</span></span>

- <span data-ttu-id="6c131-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6c131-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6c131-107">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6c131-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="6c131-108">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6c131-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6c131-109">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="6c131-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6c131-110">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="6c131-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6c131-111">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="6c131-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6c131-112">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="6c131-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6c131-113">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6c131-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="6c131-114">Identyfikator subskrypcji dla aktywnej subskrypcji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="6c131-114">A subscription ID for an active trial subscription.</span></span>

- <span data-ttu-id="6c131-115">Dostępna oferta konwersji.</span><span class="sxs-lookup"><span data-stu-id="6c131-115">An available conversion offer.</span></span>

## <a name="convert-a-trial-subscription-to-a-paid-subscription-through-code"></a><span data-ttu-id="6c131-116">Konwertowanie subskrypcji wersji próbnej na płatną subskrypcję za pomocą kodu</span><span class="sxs-lookup"><span data-stu-id="6c131-116">Convert a trial subscription to a paid subscription through code</span></span>

<span data-ttu-id="6c131-117">Aby przekonwertować subskrypcję wersji próbnej na płatną, musisz najpierw uzyskać kolekcję dostępnych konwersji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="6c131-117">To convert a trial subscription to a paid one, you must first obtain a collection of the trial conversions available.</span></span> <span data-ttu-id="6c131-118">Następnie należy wybrać ofertę konwersji, którą chcesz kupić.</span><span class="sxs-lookup"><span data-stu-id="6c131-118">Then, you must choose the conversion offer that you want to purchase.</span></span>

<span data-ttu-id="6c131-119">Oferty konwersji określają domyślną liczbę licencji, która jest taka sama jak w przypadku subskrypcji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="6c131-119">The conversion offers will specify a quantity that defaults to the same number of licenses as the trial subscription.</span></span> <span data-ttu-id="6c131-120">Możesz zmienić tę ilość, ustawiając właściwość [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) na liczbę licencji, które chcesz kupić.</span><span class="sxs-lookup"><span data-stu-id="6c131-120">You can change this quantity by setting the [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) property to the number of licenses that you want to purchase.</span></span>

> [!NOTE]
> <span data-ttu-id="6c131-121">Niezależnie od liczby zakupionych licencji identyfikator subskrypcji wersji próbnej jest ponownie wykorzystywany dla zakupionych licencji.</span><span class="sxs-lookup"><span data-stu-id="6c131-121">Regardless of the number of licenses purchased, the subscription ID of the trial is reused for the purchased licenses.</span></span> <span data-ttu-id="6c131-122">W związku z tym okres próbny znika i jest zastępowany zakupem.</span><span class="sxs-lookup"><span data-stu-id="6c131-122">As a result, the trial in effect disappears and is replaced by the purchase.</span></span>

<span data-ttu-id="6c131-123">Aby przekonwertować subskrypcję wersji próbnej za pomocą kodu, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6c131-123">Use the following steps to convert a trial subscription through code:</span></span>

1. <span data-ttu-id="6c131-124">Uzyskiwanie interfejsu do dostępnych operacji subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6c131-124">Get an interface to the subscription operations available.</span></span> <span data-ttu-id="6c131-125">Należy zidentyfikować klienta i określić identyfikator subskrypcji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="6c131-125">You must identify the customer and specify the subscription identifier of the trial subscription.</span></span>

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. <span data-ttu-id="6c131-126">Pobierz kolekcję dostępnych ofert konwersji.</span><span class="sxs-lookup"><span data-stu-id="6c131-126">Get a collection of the available conversion offers.</span></span> <span data-ttu-id="6c131-127">Aby uzyskać więcej informacji i szczegółów dotyczących żądania/odpowiedzi dla tej metody, zobacz Get a list of trial conversion offers (Uzyskiwanie listy ofert konwersji w wersji [próbnej).](get-a-list-of-trial-conversion-offers.md)</span><span class="sxs-lookup"><span data-stu-id="6c131-127">For more information and details on the request/response for this method, see [Get a list of trial conversion offers](get-a-list-of-trial-conversion-offers.md).</span></span>

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. <span data-ttu-id="6c131-128">Wybierz ofertę konwersji.</span><span class="sxs-lookup"><span data-stu-id="6c131-128">Choose a conversion offer.</span></span> <span data-ttu-id="6c131-129">Poniższy kod wybiera pierwszą ofertę konwersji w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="6c131-129">The following code chooses the first conversion offer in the collection.</span></span>

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. <span data-ttu-id="6c131-130">Opcjonalnie określ liczbę licencji do zakupu.</span><span class="sxs-lookup"><span data-stu-id="6c131-130">Optionally, specify the number of licenses to purchase.</span></span> <span data-ttu-id="6c131-131">Wartość domyślna to liczba licencji w subskrypcji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="6c131-131">The default is the number of licenses in the trial subscription.</span></span>

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. <span data-ttu-id="6c131-132">Wywołaj [**metodę Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) lub [**CreateAsync,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) aby przekonwertować subskrypcję wersji próbnej na płatną.</span><span class="sxs-lookup"><span data-stu-id="6c131-132">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) method to convert the trial subscription to paid.</span></span>

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a><span data-ttu-id="6c131-133">C\#</span><span class="sxs-lookup"><span data-stu-id="6c131-133">C\#</span></span>

<span data-ttu-id="6c131-134">Aby przekonwertować subskrypcję wersji próbnej na płatną:</span><span class="sxs-lookup"><span data-stu-id="6c131-134">To convert a trial subscription to a paid one:</span></span>

1. <span data-ttu-id="6c131-135">Użyj metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="6c131-135">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="6c131-136">Uzyskaj interfejs do operacji subskrypcji, wywołując metodę [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem subskrypcji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="6c131-136">Get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the trial subscription ID.</span></span> <span data-ttu-id="6c131-137">Zapisz odwołanie do interfejsu operacji subskrypcji w zmiennej lokalnej.</span><span class="sxs-lookup"><span data-stu-id="6c131-137">Save a reference to the subscription operations interface in a local variable.</span></span>

3. <span data-ttu-id="6c131-138">Użyj właściwości [**Conversions,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) aby uzyskać interfejs dostępnych operacji na konwersjach, a następnie wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) aby pobrać kolekcję dostępnych [**ofert konwersji.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion)</span><span class="sxs-lookup"><span data-stu-id="6c131-138">Use the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve a collection of available [**Conversion**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) offers.</span></span> <span data-ttu-id="6c131-139">Musisz wybrać jedną z nich.</span><span class="sxs-lookup"><span data-stu-id="6c131-139">You must choose one.</span></span> <span data-ttu-id="6c131-140">W poniższym przykładzie domyślna jest pierwsza dostępna konwersja.</span><span class="sxs-lookup"><span data-stu-id="6c131-140">The following example defaults to the first conversion available.</span></span>

4. <span data-ttu-id="6c131-141">Użyj odwołania do interfejsu operacji subskrypcji zapisanego w zmiennej lokalnej i właściwości [**Conversions,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) aby uzyskać interfejs do dostępnych operacji na konwersjach.</span><span class="sxs-lookup"><span data-stu-id="6c131-141">Use the reference to the subscription operations interface that you saved in a local variable and the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions.</span></span>

5. <span data-ttu-id="6c131-142">Przekaż wybrany obiekt oferty konwersji do [**metody Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) lub [**CreateAsync,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) aby spróbować przetworzyć wersję próbną.</span><span class="sxs-lookup"><span data-stu-id="6c131-142">Pass the selected conversion offer object to the [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) method to attempt the trial conversion.</span></span>

### <a name="c-example"></a><span data-ttu-id="6c131-143">Przykład języka C \#</span><span class="sxs-lookup"><span data-stu-id="6c131-143">C\# example</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="6c131-144">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="6c131-144">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6c131-145">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="6c131-145">Request syntax</span></span>

| <span data-ttu-id="6c131-146">Metoda</span><span class="sxs-lookup"><span data-stu-id="6c131-146">Method</span></span>   | <span data-ttu-id="6c131-147">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="6c131-147">Request URI</span></span>                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6c131-148">**Post**</span><span class="sxs-lookup"><span data-stu-id="6c131-148">**POST**</span></span> | <span data-ttu-id="6c131-149">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6c131-149">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="6c131-150">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="6c131-150">URI parameter</span></span>

<span data-ttu-id="6c131-151">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i subskrypcję wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="6c131-151">Use the following path parameters to identify the customer and trial subscription.</span></span>

| <span data-ttu-id="6c131-152">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6c131-152">Name</span></span>            | <span data-ttu-id="6c131-153">Typ</span><span class="sxs-lookup"><span data-stu-id="6c131-153">Type</span></span>   | <span data-ttu-id="6c131-154">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6c131-154">Required</span></span> | <span data-ttu-id="6c131-155">Opis</span><span class="sxs-lookup"><span data-stu-id="6c131-155">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="6c131-156">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="6c131-156">customer-id</span></span>     | <span data-ttu-id="6c131-157">ciąg</span><span class="sxs-lookup"><span data-stu-id="6c131-157">string</span></span> | <span data-ttu-id="6c131-158">Tak</span><span class="sxs-lookup"><span data-stu-id="6c131-158">Yes</span></span>      | <span data-ttu-id="6c131-159">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="6c131-159">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="6c131-160">subscription-id</span><span class="sxs-lookup"><span data-stu-id="6c131-160">subscription-id</span></span> | <span data-ttu-id="6c131-161">ciąg</span><span class="sxs-lookup"><span data-stu-id="6c131-161">string</span></span> | <span data-ttu-id="6c131-162">Tak</span><span class="sxs-lookup"><span data-stu-id="6c131-162">Yes</span></span>      | <span data-ttu-id="6c131-163">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje subskrypcję wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="6c131-163">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6c131-164">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="6c131-164">Request headers</span></span>

<span data-ttu-id="6c131-165">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6c131-165">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6c131-166">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="6c131-166">Request body</span></span>

<span data-ttu-id="6c131-167">Wypełniony zasób [konwersji](conversions-resources.md#conversion) musi zostać uwzględniony w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="6c131-167">A populated [Conversion](conversions-resources.md#conversion) resource must be included in the request body.</span></span>

### <a name="request-example"></a><span data-ttu-id="6c131-168">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="6c131-168">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="6c131-169">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="6c131-169">REST response</span></span>

<span data-ttu-id="6c131-170">Jeśli to się powiedzie, treść odpowiedzi zawiera [zasób ConversionResult.](conversions-resources.md#conversionresult)</span><span class="sxs-lookup"><span data-stu-id="6c131-170">If successful, the response body contains a [ConversionResult](conversions-resources.md#conversionresult) resource.</span></span>

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="6c131-171">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6c131-171">Response success and error codes</span></span>

<span data-ttu-id="6c131-172">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="6c131-172">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6c131-173">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="6c131-173">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6c131-174">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6c131-174">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="6c131-175">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6c131-175">Response example</span></span>

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
