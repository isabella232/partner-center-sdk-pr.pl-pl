---
title: Pobieranie cen usług Microsoft Azure Partner Shared Services
description: Jak uzyskać kartę stawki platformy Azure z cenami dla usług udostępnionych Microsoft Azure Partner.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0008d7474f7e57bbbd765afdf2487ee279848ac3
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548808"
---
# <a name="get-prices-for-microsoft-azure-partner-shared-services"></a><span data-ttu-id="2ac73-103">Pobieranie cen usług Microsoft Azure Partner Shared Services</span><span class="sxs-lookup"><span data-stu-id="2ac73-103">Get prices for Microsoft Azure Partner Shared Services</span></span>

<span data-ttu-id="2ac73-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2ac73-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2ac73-105">Jak uzyskać kartę [stawki platformy Azure z](azure-rate-card-resources.md) cenami dla usług udostępnionych Microsoft Azure Partner.</span><span class="sxs-lookup"><span data-stu-id="2ac73-105">How to get an [Azure Rate Card](azure-rate-card-resources.md) with prices for Microsoft Azure Partner Shared Services.</span></span>

<span data-ttu-id="2ac73-106">Ceny różnią się w zależności od rynku i waluty, a ten interfejs API uwzględnia lokalizację.</span><span class="sxs-lookup"><span data-stu-id="2ac73-106">Prices differ by market and currency, and this API takes location into consideration.</span></span> <span data-ttu-id="2ac73-107">Domyślnie interfejs API używa ustawień profilu partnera w języku Partner Center i języku przeglądarki, a te ustawienia można dostosowywać.</span><span class="sxs-lookup"><span data-stu-id="2ac73-107">By default, the API uses your partner profile settings in Partner Center and your browser language, and those settings are customizable.</span></span> <span data-ttu-id="2ac73-108">Świadomość lokalizacji jest szczególnie przydatna, jeśli zarządzasz sprzedażą na wielu rynkach z jednego, scentralizowanego biura.</span><span class="sxs-lookup"><span data-stu-id="2ac73-108">The location awareness is especially relevant if you manage sales in multiple markets from a single, centralized office.</span></span>

## <a name="example-code"></a><span data-ttu-id="2ac73-109">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="2ac73-109">Example Code</span></span>

## <a name="c"></a><span data-ttu-id="2ac73-110">C\#</span><span class="sxs-lookup"><span data-stu-id="2ac73-110">C\#</span></span>

<span data-ttu-id="2ac73-111">Aby uzyskać kartę stawki platformy Azure, wywołaj metodę [**IAzureRateCard.GetShared,**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) aby zwrócić [**zasób AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) zawierający ceny platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2ac73-111">To obtain the Azure Rate Card, call the [**IAzureRateCard.GetShared**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) method to return an [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) resource that contains the Azure prices.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.GetShared();
```

## <a name="java"></a><span data-ttu-id="2ac73-112">Java</span><span class="sxs-lookup"><span data-stu-id="2ac73-112">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="2ac73-113">Aby uzyskać kartę stawki platformy Azure, wywołaj funkcję **IAzureRateCard.getShared,** aby zwrócić szczegóły karty stawki zawierającej ceny platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2ac73-113">To obtain the Azure Rate Card, call the **IAzureRateCard.getShared** function to return rate card details that contains the Azure prices.</span></span>

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().getShared();
```

## <a name="powershell"></a><span data-ttu-id="2ac73-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ac73-114">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="2ac73-115">Aby uzyskać kartę platformy Azure, wykonaj polecenie [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) i określ parametr **SharedServices,** aby zwrócić szczegóły karty stawki zawierające ceny platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2ac73-115">To obtain the Azure Card, execute the [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) command and specify the **SharedServices** parameter to return rate card details that contains the Azure prices.</span></span>

```powershell
Get-PartnerAzureRateCard -SharedServices
```

## <a name="rest-request"></a><span data-ttu-id="2ac73-116">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="2ac73-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2ac73-117">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="2ac73-117">Request syntax</span></span>

| <span data-ttu-id="2ac73-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="2ac73-118">Method</span></span>  | <span data-ttu-id="2ac73-119">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="2ac73-119">Request URI</span></span>                                                               |
|---------|---------------------------------------------------------------------------|
| <span data-ttu-id="2ac73-120">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="2ac73-120">**GET**</span></span> | <span data-ttu-id="2ac73-121">*{baseURL}*/v1/ratecards/azure-shared?currency={currency}&region={region}</span><span class="sxs-lookup"><span data-stu-id="2ac73-121">*{baseURL}*/v1/ratecards/azure-shared?currency={currency}&region={region}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="2ac73-122">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="2ac73-122">URI parameters</span></span>

| <span data-ttu-id="2ac73-123">Nazwa</span><span class="sxs-lookup"><span data-stu-id="2ac73-123">Name</span></span>     | <span data-ttu-id="2ac73-124">Typ</span><span class="sxs-lookup"><span data-stu-id="2ac73-124">Type</span></span>   | <span data-ttu-id="2ac73-125">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2ac73-125">Required</span></span> | <span data-ttu-id="2ac73-126">Opis</span><span class="sxs-lookup"><span data-stu-id="2ac73-126">Description</span></span>                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2ac73-127">currency</span><span class="sxs-lookup"><span data-stu-id="2ac73-127">currency</span></span> | <span data-ttu-id="2ac73-128">ciąg</span><span class="sxs-lookup"><span data-stu-id="2ac73-128">string</span></span> | <span data-ttu-id="2ac73-129">Nie</span><span class="sxs-lookup"><span data-stu-id="2ac73-129">No</span></span>       | <span data-ttu-id="2ac73-130">Opcjonalny trzyliterowy kod ISO waluty, w której zostaną podane stawki zasobów (na przykład `EUR` ).</span><span class="sxs-lookup"><span data-stu-id="2ac73-130">Optional three letter ISO code for the currency in which the resource rates will be provided (for example `EUR`).</span></span> <span data-ttu-id="2ac73-131">Wartością domyślną jest waluta skojarzona z rynek w profilu partnera.</span><span class="sxs-lookup"><span data-stu-id="2ac73-131">The default is the currency associated with the market in the partner profile.</span></span> |
| <span data-ttu-id="2ac73-132">region</span><span class="sxs-lookup"><span data-stu-id="2ac73-132">region</span></span>   | <span data-ttu-id="2ac73-133">ciąg</span><span class="sxs-lookup"><span data-stu-id="2ac73-133">string</span></span> | <span data-ttu-id="2ac73-134">Nie</span><span class="sxs-lookup"><span data-stu-id="2ac73-134">No</span></span>       | <span data-ttu-id="2ac73-135">Opcjonalny dwuliterowy kod kraju/regionu ISO, który wskazuje rynek, na którym zakupiono ofertę (na przykład `FR` ).</span><span class="sxs-lookup"><span data-stu-id="2ac73-135">Optional two-letter ISO country/region code that indicates the market where the offer is purchased (for example `FR`).</span></span> <span data-ttu-id="2ac73-136">Wartość domyślna to kod kraju/regionu ustawiony w profilu partnera.</span><span class="sxs-lookup"><span data-stu-id="2ac73-136">The default is the country/region code set in the partner profile.</span></span>        |

<span data-ttu-id="2ac73-137">Jeśli opcjonalny nagłówek X-Locale jest uwzględniony w żądaniu, jego wartość określa język używany dla szczegółów w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="2ac73-137">If the optional X-Locale header is included in the request, its value determines the language used for the details in the response.</span></span>

### <a name="request-headers"></a><span data-ttu-id="2ac73-138">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="2ac73-138">Request headers</span></span>

<span data-ttu-id="2ac73-139">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2ac73-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2ac73-140">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="2ac73-140">Request body</span></span>

<span data-ttu-id="2ac73-141">Brak.</span><span class="sxs-lookup"><span data-stu-id="2ac73-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2ac73-142">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="2ac73-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/ratecards/azure-shared HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07ced227-3f32-4eeb-8062-f0bef849a9bc
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="2ac73-143">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="2ac73-143">REST response</span></span>

<span data-ttu-id="2ac73-144">Jeśli żądanie powiedzie się, zwraca zasób [karty stawki platformy Azure.](azure-rate-card-resources.md)</span><span class="sxs-lookup"><span data-stu-id="2ac73-144">If the request is successful, it returns an [Azure Rate Card](azure-rate-card-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2ac73-145">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2ac73-145">Response success and error codes</span></span>

<span data-ttu-id="2ac73-146">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="2ac73-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2ac73-147">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="2ac73-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2ac73-148">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2ac73-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2ac73-149">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2ac73-149">Response example</span></span>

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
    "locale": "en-US",
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
