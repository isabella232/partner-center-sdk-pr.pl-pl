---
title: Pobieranie cen platformy Microsoft Azure
description: Jak uzyskać kartę stawki platformy Azure z cenami w czasie rzeczywistym dla oferty platformy Azure. Cennik platformy Azure jest dość dynamiczny i często się zmienia.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4f66ab19ef3723fbaa27acff941cf48683a7c25c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548791"
---
# <a name="get-prices-for-microsoft-azure"></a><span data-ttu-id="62038-104">Pobieranie cen platformy Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="62038-104">Get prices for Microsoft Azure</span></span>

<span data-ttu-id="62038-105">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="62038-105">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="62038-106">Jak uzyskać kartę [stawki platformy Azure](azure-rate-card-resources.md) z cenami w czasie rzeczywistym dla oferty platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="62038-106">How to get an [Azure Rate Card](azure-rate-card-resources.md) with real-time prices for an Azure offer.</span></span> <span data-ttu-id="62038-107">Cennik platformy Azure jest dość dynamiczny i często się zmienia.</span><span class="sxs-lookup"><span data-stu-id="62038-107">Azure pricing is quite dynamic and changes frequently.</span></span>

<span data-ttu-id="62038-108">Aby śledzić użycie i ułatwić przewidywanie miesięcznego rachunku oraz rachunku dla poszczególnych klientów, możesz połączyć to zapytanie dotyczące karty stawki platformy Azure w celu uzyskania cen platformy Microsoft Azure z żądaniem uzyskania rekordów wykorzystania klienta dla platformy [Azure.](get-a-customer-s-utilization-record-for-azure.md)</span><span class="sxs-lookup"><span data-stu-id="62038-108">To track usage and help predict your monthly bill and the bills for individual customers, you can combine this Azure Rate Card query to get prices for Microsoft Azure with a request to [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md).</span></span>

<span data-ttu-id="62038-109">Ceny różnią się w zależności od rynku i waluty, a ten interfejs API uwzględnia lokalizację.</span><span class="sxs-lookup"><span data-stu-id="62038-109">Prices differ by market and currency, and this API takes location into consideration.</span></span> <span data-ttu-id="62038-110">Domyślnie interfejs API używa ustawień profilu partnera w języku Partner Center i języku przeglądarki, a te ustawienia można dostosowywać.</span><span class="sxs-lookup"><span data-stu-id="62038-110">By default, the API uses your partner profile settings in Partner Center and your browser language, and those settings are customizable.</span></span> <span data-ttu-id="62038-111">Świadomość lokalizacji jest szczególnie przydatna, jeśli zarządzasz sprzedażą na wielu rynkach z jednego, scentralizowanego biura.</span><span class="sxs-lookup"><span data-stu-id="62038-111">The location awareness is especially relevant if you manage sales in multiple markets from a single, centralized office.</span></span> <span data-ttu-id="62038-112">Aby uzyskać więcej informacji, zobacz [Parametry URI](#uri-parameters).</span><span class="sxs-lookup"><span data-stu-id="62038-112">For more information, see [URI parameters](#uri-parameters).</span></span>

## <a name="c"></a><span data-ttu-id="62038-113">C\#</span><span class="sxs-lookup"><span data-stu-id="62038-113">C\#</span></span>

<span data-ttu-id="62038-114">Aby uzyskać kartę stawki platformy Azure, wywołaj metodę [**IAzureRateCard.Get,**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) aby zwrócić [**zasób AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) zawierający ceny platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="62038-114">To obtain the Azure Rate Card, call the [**IAzureRateCard.Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) method to return an [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) resource that contains the Azure prices.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

<span data-ttu-id="62038-115">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="62038-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="62038-116">**Project:** zestaw SDK Centrum partnerskiego Samples Class : GetAzureRateCard.cs **(Klasa** przykładów zestaw SDK Centrum partnerskiego: GetAzureRateCard.cs)</span><span class="sxs-lookup"><span data-stu-id="62038-116">**Project**: Partner Center SDK Samples **Class**: GetAzureRateCard.cs</span></span>

## <a name="java"></a><span data-ttu-id="62038-117">Java</span><span class="sxs-lookup"><span data-stu-id="62038-117">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="62038-118">Aby uzyskać kartę stawki platformy Azure, wywołaj funkcję **IAzureRateCard.get,** aby zwrócić szczegóły karty stawki zawierające ceny platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="62038-118">To obtain the Azure Rate Card, call the **IAzureRateCard.get** function to return rate card details that contains the Azure prices.</span></span>

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

## <a name="powershell"></a><span data-ttu-id="62038-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="62038-119">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="62038-120">Aby uzyskać kartę platformy Azure, wykonaj polecenie [**Get-PartnerAzureRateCard,**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) aby zwrócić szczegóły karty stawki zawierające ceny platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="62038-120">To obtain the Azure Card, execute the [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) command to return rate card details that contains the Azure prices.</span></span>

```powershell
Get-PartnerAzureRateCard
```

## <a name="rest-request"></a><span data-ttu-id="62038-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="62038-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="62038-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="62038-122">Request syntax</span></span>

| <span data-ttu-id="62038-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="62038-123">Method</span></span>  | <span data-ttu-id="62038-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="62038-124">Request URI</span></span>                                                        |
|---------|--------------------------------------------------------------------|
| <span data-ttu-id="62038-125">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="62038-125">**GET**</span></span> | <span data-ttu-id="62038-126">*{baseURL}*/v1/ratecards/azure?currency={currency}&region={region}</span><span class="sxs-lookup"><span data-stu-id="62038-126">*{baseURL}*/v1/ratecards/azure?currency={currency}&region={region}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="62038-127">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="62038-127">URI parameters</span></span>

| <span data-ttu-id="62038-128">Nazwa</span><span class="sxs-lookup"><span data-stu-id="62038-128">Name</span></span>     | <span data-ttu-id="62038-129">Typ</span><span class="sxs-lookup"><span data-stu-id="62038-129">Type</span></span>   | <span data-ttu-id="62038-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="62038-130">Required</span></span> | <span data-ttu-id="62038-131">Opis</span><span class="sxs-lookup"><span data-stu-id="62038-131">Description</span></span>                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="62038-132">currency</span><span class="sxs-lookup"><span data-stu-id="62038-132">currency</span></span> | <span data-ttu-id="62038-133">ciąg</span><span class="sxs-lookup"><span data-stu-id="62038-133">string</span></span> | <span data-ttu-id="62038-134">Nie</span><span class="sxs-lookup"><span data-stu-id="62038-134">No</span></span>       | <span data-ttu-id="62038-135">Opcjonalny trzyliterowy kod ISO waluty, w której zostaną podane stawki zasobów (na przykład `EUR` ).</span><span class="sxs-lookup"><span data-stu-id="62038-135">Optional three letter ISO code for the currency in which the resource rates will be provided (for example `EUR`).</span></span> <span data-ttu-id="62038-136">Wartość domyślna to `USD`.</span><span class="sxs-lookup"><span data-stu-id="62038-136">The default is `USD`.</span></span> |
| <span data-ttu-id="62038-137">region</span><span class="sxs-lookup"><span data-stu-id="62038-137">region</span></span>   | <span data-ttu-id="62038-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="62038-138">string</span></span> | <span data-ttu-id="62038-139">Nie</span><span class="sxs-lookup"><span data-stu-id="62038-139">No</span></span>       | <span data-ttu-id="62038-140">Opcjonalny dwuliterowy kod kraju/regionu ISO, który wskazuje rynek, na którym zakupiono ofertę (na przykład `FR` ).</span><span class="sxs-lookup"><span data-stu-id="62038-140">Optional two-letter ISO country/region code that indicates the market where the offer is purchased (for example `FR`).</span></span> <span data-ttu-id="62038-141">Wartość domyślna to `US`.</span><span class="sxs-lookup"><span data-stu-id="62038-141">The default is `US`.</span></span>        |

<span data-ttu-id="62038-142">W żądaniu możesz uwzględnić [](headers.md#rest-request-headers) opcjonalny nagłówek X-Locale.</span><span class="sxs-lookup"><span data-stu-id="62038-142">You can include the optional X-Locale [header](headers.md#rest-request-headers) in your request.</span></span> <span data-ttu-id="62038-143">Jeśli nie dołączysz nagłówka X-Locale, zostanie użyta wartość domyślna ("en-US").</span><span class="sxs-lookup"><span data-stu-id="62038-143">If you don't include the X-Locale header, the default value ("en-US") is used.</span></span>

- <span data-ttu-id="62038-144">W przypadku podania parametrów waluty i regionu w żądaniu wartość X-Locale jest używana do określenia języka odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="62038-144">If you provide currency and region parameters in your request, the value of X-Locale is used to determine the response's language.</span></span>

- <span data-ttu-id="62038-145">Jeśli w żądaniu nie podaniem parametrów regionu i waluty, wartość X-Locale (Ustawienia lokalne X) jest używana do określenia regionu, waluty i języka odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="62038-145">If you don't provide region and currency parameters in your request, the value of X-Locale is used to determine the response's region, currency, and language.</span></span>

### <a name="request-header"></a><span data-ttu-id="62038-146">Nagłówek żądania</span><span class="sxs-lookup"><span data-stu-id="62038-146">Request header</span></span>

<span data-ttu-id="62038-147">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="62038-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="62038-148">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="62038-148">Request body</span></span>

<span data-ttu-id="62038-149">Brak.</span><span class="sxs-lookup"><span data-stu-id="62038-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="62038-150">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="62038-150">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="62038-151">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="62038-151">REST response</span></span>

<span data-ttu-id="62038-152">Jeśli żądanie powiedzie się, zwraca zasób [karty stawki platformy Azure.](azure-rate-card-resources.md)</span><span class="sxs-lookup"><span data-stu-id="62038-152">If the request is successful, it returns an [Azure Rate Card](azure-rate-card-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="62038-153">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="62038-153">Response success and error codes</span></span>

<span data-ttu-id="62038-154">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="62038-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="62038-155">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="62038-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="62038-156">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="62038-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="62038-157">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="62038-157">Response example</span></span>

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
