---
title: Pobieranie cen platformy Microsoft Azure
description: Jak uzyskać kartę usługi Azure rate z cenami w czasie rzeczywistym dla oferty platformy Azure. Cennik platformy Azure jest dość często dynamiczny i zmieniany.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0716f0428b13604105b435a2ce8287a8b4609fea
ms.sourcegitcommit: 64c498d3571f2287305968890578bc7396779621
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/19/2020
ms.locfileid: "97770292"
---
# <a name="get-prices-for-microsoft-azure"></a><span data-ttu-id="90406-104">Pobieranie cen platformy Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="90406-104">Get prices for Microsoft Azure</span></span>

<span data-ttu-id="90406-105">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="90406-105">**Applies To**</span></span>

- <span data-ttu-id="90406-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="90406-106">Partner Center</span></span>
- <span data-ttu-id="90406-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="90406-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="90406-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="90406-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="90406-109">Jak uzyskać [kartę usługi Azure rate](azure-rate-card-resources.md) z cenami w czasie rzeczywistym dla oferty platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="90406-109">How to get an [Azure Rate Card](azure-rate-card-resources.md) with real-time prices for an Azure offer.</span></span> <span data-ttu-id="90406-110">Cennik platformy Azure jest dość często dynamiczny i zmieniany.</span><span class="sxs-lookup"><span data-stu-id="90406-110">Azure pricing is quite dynamic and changes frequently.</span></span>

<span data-ttu-id="90406-111">Aby śledzić użycie i pomóc w przewidywaniu miesięcznych opłat i rachunków dla poszczególnych klientów, możesz połączyć tę kwerendę z kartą usługi Azure rate, aby uzyskać ceny za Microsoft Azure z żądaniem [uzyskania rekordów użycia klienta na platformie Azure](get-a-customer-s-utilization-record-for-azure.md).</span><span class="sxs-lookup"><span data-stu-id="90406-111">To track usage and help predict your monthly bill and the bills for individual customers, you can combine this Azure Rate Card query to get prices for Microsoft Azure with a request to [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md).</span></span>

<span data-ttu-id="90406-112">Ceny różnią się w zależności od rynku i waluty, a ten interfejs API przyjmuje lokalizację.</span><span class="sxs-lookup"><span data-stu-id="90406-112">Prices differ by market and currency, and this API takes location into consideration.</span></span> <span data-ttu-id="90406-113">Domyślnie interfejs API używa ustawień profilu partnera w centrum partnerskim i w języku przeglądarki. te ustawienia można dostosować.</span><span class="sxs-lookup"><span data-stu-id="90406-113">By default, the API uses your partner profile settings in Partner Center and your browser language, and those settings are customizable.</span></span> <span data-ttu-id="90406-114">Rozpoznawanie lokalizacji jest szczególnie istotne w przypadku zarządzania sprzedażą na wielu rynkach z jednego, scentralizowanego biura.</span><span class="sxs-lookup"><span data-stu-id="90406-114">The location awareness is especially relevant if you manage sales in multiple markets from a single, centralized office.</span></span> <span data-ttu-id="90406-115">Aby uzyskać więcej informacji, zobacz [Parametry identyfikatora URI](#uri-parameters).</span><span class="sxs-lookup"><span data-stu-id="90406-115">For more information, see [URI parameters](#uri-parameters).</span></span>

## <a name="c"></a><span data-ttu-id="90406-116">C\#</span><span class="sxs-lookup"><span data-stu-id="90406-116">C\#</span></span>

<span data-ttu-id="90406-117">Aby uzyskać kartę usługi Azure rate, wywołaj metodę [**IAzureRateCard. Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) w celu zwrócenia zasobu [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) zawierającego ceny platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="90406-117">To obtain the Azure Rate Card, call the [**IAzureRateCard.Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) method to return an [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) resource that contains the Azure prices.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

<span data-ttu-id="90406-118">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="90406-118">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="90406-119">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: GetAzureRateCard.cs</span><span class="sxs-lookup"><span data-stu-id="90406-119">**Project**: Partner Center SDK Samples **Class**: GetAzureRateCard.cs</span></span>

## <a name="java"></a><span data-ttu-id="90406-120">Java</span><span class="sxs-lookup"><span data-stu-id="90406-120">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="90406-121">Aby uzyskać kartę stawki platformy Azure, wywołaj funkcję **IAzureRateCard. Get** w celu zwrócenia szczegółów karty rate zawierającej ceny platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="90406-121">To obtain the Azure Rate Card, call the **IAzureRateCard.get** function to return rate card details that contains the Azure prices.</span></span>

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

## <a name="powershell"></a><span data-ttu-id="90406-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="90406-122">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="90406-123">Aby uzyskać kartę platformy Azure, wykonaj polecenie [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) , aby wyświetlić szczegóły karty stawki zawierającej ceny platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="90406-123">To obtain the Azure Card, execute the [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) command to return rate card details that contains the Azure prices.</span></span>

```powershell
Get-PartnerAzureRateCard
```

## <a name="rest-request"></a><span data-ttu-id="90406-124">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="90406-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="90406-125">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="90406-125">Request syntax</span></span>

| <span data-ttu-id="90406-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="90406-126">Method</span></span>  | <span data-ttu-id="90406-127">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="90406-127">Request URI</span></span>                                                        |
|---------|--------------------------------------------------------------------|
| <span data-ttu-id="90406-128">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="90406-128">**GET**</span></span> | <span data-ttu-id="90406-129">*{baseURL}*/V1/ratecards/Azure? Currency = {currency} &region = {Region}</span><span class="sxs-lookup"><span data-stu-id="90406-129">*{baseURL}*/v1/ratecards/azure?currency={currency}&region={region}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="90406-130">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="90406-130">URI parameters</span></span>

| <span data-ttu-id="90406-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="90406-131">Name</span></span>     | <span data-ttu-id="90406-132">Typ</span><span class="sxs-lookup"><span data-stu-id="90406-132">Type</span></span>   | <span data-ttu-id="90406-133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="90406-133">Required</span></span> | <span data-ttu-id="90406-134">Opis</span><span class="sxs-lookup"><span data-stu-id="90406-134">Description</span></span>                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="90406-135">currency</span><span class="sxs-lookup"><span data-stu-id="90406-135">currency</span></span> | <span data-ttu-id="90406-136">ciąg</span><span class="sxs-lookup"><span data-stu-id="90406-136">string</span></span> | <span data-ttu-id="90406-137">Nie</span><span class="sxs-lookup"><span data-stu-id="90406-137">No</span></span>       | <span data-ttu-id="90406-138">Opcjonalny trzyliterowy kod ISO dla waluty, w której zostaną podane stawki zasobów (na przykład `EUR` ).</span><span class="sxs-lookup"><span data-stu-id="90406-138">Optional three letter ISO code for the currency in which the resource rates will be provided (for example `EUR`).</span></span> <span data-ttu-id="90406-139">Wartość domyślna to `USD`.</span><span class="sxs-lookup"><span data-stu-id="90406-139">The default is `USD`.</span></span> |
| <span data-ttu-id="90406-140">region</span><span class="sxs-lookup"><span data-stu-id="90406-140">region</span></span>   | <span data-ttu-id="90406-141">ciąg</span><span class="sxs-lookup"><span data-stu-id="90406-141">string</span></span> | <span data-ttu-id="90406-142">Nie</span><span class="sxs-lookup"><span data-stu-id="90406-142">No</span></span>       | <span data-ttu-id="90406-143">Opcjonalny dwuliterowy kod kraju/regionu w formacie ISO, który wskazuje rynek zakupu oferty (na przykład `FR` ).</span><span class="sxs-lookup"><span data-stu-id="90406-143">Optional two-letter ISO country/region code that indicates the market where the offer is purchased (for example `FR`).</span></span> <span data-ttu-id="90406-144">Wartość domyślna to `US`.</span><span class="sxs-lookup"><span data-stu-id="90406-144">The default is `US`.</span></span>        |

<span data-ttu-id="90406-145">W żądaniu można uwzględnić opcjonalny [nagłówek](headers.md#rest-request-headers) "X-locale".</span><span class="sxs-lookup"><span data-stu-id="90406-145">You can include the optional X-Locale [header](headers.md#rest-request-headers) in your request.</span></span> <span data-ttu-id="90406-146">Jeśli nie dołączysz nagłówka "X-local", zostanie użyta wartość domyślna ("en-US").</span><span class="sxs-lookup"><span data-stu-id="90406-146">If you don't include the X-Locale header, the default value ("en-US") is used.</span></span>

- <span data-ttu-id="90406-147">Jeśli podano parametry waluty i regionu w żądaniu, wartość X-locale służy do określenia języka odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="90406-147">If you provide currency and region parameters in your request, the value of X-Locale is used to determine the response's language.</span></span>

- <span data-ttu-id="90406-148">Jeśli nie podano parametrów regionu i waluty w żądaniu, wartość X-locale służy do określenia regionu, waluty i języka odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="90406-148">If you don't provide region and currency parameters in your request, the value of X-Locale is used to determine the response's region, currency, and language.</span></span>

### <a name="request-header"></a><span data-ttu-id="90406-149">Nagłówek żądania</span><span class="sxs-lookup"><span data-stu-id="90406-149">Request header</span></span>

<span data-ttu-id="90406-150">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="90406-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="90406-151">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="90406-151">Request body</span></span>

<span data-ttu-id="90406-152">Brak.</span><span class="sxs-lookup"><span data-stu-id="90406-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="90406-153">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="90406-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/ratecards/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07ced227-3f32-4eeb-8062-f0bef849a9bc
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="90406-154">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="90406-154">REST response</span></span>

<span data-ttu-id="90406-155">Jeśli żądanie zakończy się pomyślnie, zwraca zasób [karty usługi Azure rate](azure-rate-card-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="90406-155">If the request is successful, it returns an [Azure Rate Card](azure-rate-card-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="90406-156">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="90406-156">Response success and error codes</span></span>

<span data-ttu-id="90406-157">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="90406-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="90406-158">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="90406-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="90406-159">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="90406-159">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="90406-160">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="90406-160">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1545508
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57b25659-fc00-4215-87e7-2b09bac6845d
MS-RequestId: 870118d0-adbb-41a3-82d2-a3d45ade3c73
MS-CV: CYBB8PXMsEukJBIn.0
MS-ServerId: 201021413
Date: Wed, 01 Feb 2017 00:13:45 GMT

{
    "locale": "en",
    "currency": "USD",
    "isTaxIncluded": false,
    "meters": [{
            "id": "4b836326-7e19-46e6-8bce-1b19bb6cd91e",
            "name": "Unlimited Data - 1 Gbps",
            "rates": {
                "0": 7395.0
            },
            "tags": [],
            "category": "Networking",
            "subcategory": "ExpressRoute",
            "region": "Zone 2",
            "unit": "Connections",
            "includedQuantity": 0.0,
            "effectiveDate": "2015-09-01T00:00:00Z"
        }, {
            "id": "1e8f6d9f-8b40-4c97-80cc-cff87a290a93",
            "name": "Compute Hours",
            "rates": {
                "0": 3.9729
            },
            "tags": [],
            "category": "Cloud Services",
            "subcategory": "Standard_L16 Cloud Services",
            "region": "AU East",
            "unit": "1 Hour",
            "includedQuantity": 0.0,
            "effectiveDate": "2016-09-01T00:00:00Z"
        }, {
            "id": "7a2639ce-ae47-4413-9837-6b4f4b78be3d",
            "name": "Compute Hours",
            "rates": {
                "0": 0.1122
            },
            "tags": [],
            "category": "Virtual Machines",
            "subcategory": "Standard_D1_v2 VM (Windows)",
            "region": "BR South",
            "unit": "Hours",
            "includedQuantity": 0.0,
            "effectiveDate": "2017-01-01T00:00:00Z"
        }
    ],
    "offerTerms": [{
            "name": "Overage discount",
            "discount": 0.15,
            "excludedMeterIds": ["53cc0061-0fe2-4249-bf62-e1008c811f5c", "c82dbd27-c978-43a7-ad41-525a90d8962b"],
            "effectiveDate": "2014-01-01T00:00:00"
        }
    ],
    "attributes": {
        "objectType": "AzureRateCard"
    }
}
```
