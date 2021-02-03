---
title: Pobieranie cen usług Microsoft Azure Partner Shared Services
description: Jak uzyskać kartę stawki platformy Azure z cenami usług udostępnionych Microsoft Azure partnerskich.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: cd396c35b6b89de4d0f092ba4da738a2ed0ac633
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768478"
---
# <a name="get-prices-for-microsoft-azure-partner-shared-services"></a><span data-ttu-id="e5e52-103">Pobieranie cen usług Microsoft Azure Partner Shared Services</span><span class="sxs-lookup"><span data-stu-id="e5e52-103">Get prices for Microsoft Azure Partner Shared Services</span></span>

<span data-ttu-id="e5e52-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="e5e52-104">**Applies To**</span></span>

- <span data-ttu-id="e5e52-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="e5e52-105">Partner Center</span></span>
- <span data-ttu-id="e5e52-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="e5e52-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="e5e52-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e5e52-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e5e52-108">Jak uzyskać [kartę stawki platformy Azure](azure-rate-card-resources.md) z cenami usług udostępnionych Microsoft Azure partnerskich.</span><span class="sxs-lookup"><span data-stu-id="e5e52-108">How to get an [Azure Rate Card](azure-rate-card-resources.md) with prices for Microsoft Azure Partner Shared Services.</span></span>

<span data-ttu-id="e5e52-109">Ceny różnią się w zależności od rynku i waluty, a ten interfejs API przyjmuje lokalizację.</span><span class="sxs-lookup"><span data-stu-id="e5e52-109">Prices differ by market and currency, and this API takes location into consideration.</span></span> <span data-ttu-id="e5e52-110">Domyślnie interfejs API używa ustawień profilu partnera w centrum partnerskim i w języku przeglądarki. te ustawienia można dostosować.</span><span class="sxs-lookup"><span data-stu-id="e5e52-110">By default, the API uses your partner profile settings in Partner Center and your browser language, and those settings are customizable.</span></span> <span data-ttu-id="e5e52-111">Rozpoznawanie lokalizacji jest szczególnie istotne w przypadku zarządzania sprzedażą na wielu rynkach z jednego, scentralizowanego biura.</span><span class="sxs-lookup"><span data-stu-id="e5e52-111">The location awareness is especially relevant if you manage sales in multiple markets from a single, centralized office.</span></span>

## <a name="example-code"></a><span data-ttu-id="e5e52-112">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="e5e52-112">Example Code</span></span>

## <a name="c"></a><span data-ttu-id="e5e52-113">C\#</span><span class="sxs-lookup"><span data-stu-id="e5e52-113">C\#</span></span>

<span data-ttu-id="e5e52-114">Aby uzyskać kartę stawki platformy Azure, wywołaj metodę [**IAzureRateCard. Getshared**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) w celu zwrócenia zasobu [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) zawierającego ceny platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e5e52-114">To obtain the Azure Rate Card, call the [**IAzureRateCard.GetShared**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) method to return an [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) resource that contains the Azure prices.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.GetShared();
```

## <a name="java"></a><span data-ttu-id="e5e52-115">Java</span><span class="sxs-lookup"><span data-stu-id="e5e52-115">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="e5e52-116">Aby uzyskać kartę stawki platformy Azure, wywołaj funkcję **IAzureRateCard. Getshared** , aby zwracała szczegóły karty szybkości zawierającej ceny platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e5e52-116">To obtain the Azure Rate Card, call the **IAzureRateCard.getShared** function to return rate card details that contains the Azure prices.</span></span>

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().getShared();
```

## <a name="powershell"></a><span data-ttu-id="e5e52-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5e52-117">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="e5e52-118">Aby uzyskać kartę platformy Azure, wykonaj polecenie [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) i określ parametr **SharedServices** w celu zwrócenia szczegółów karty częstotliwość, która zawiera ceny platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e5e52-118">To obtain the Azure Card, execute the [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) command and specify the **SharedServices** parameter to return rate card details that contains the Azure prices.</span></span>

```powershell
Get-PartnerAzureRateCard -SharedServices
```

## <a name="rest-request"></a><span data-ttu-id="e5e52-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="e5e52-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e5e52-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="e5e52-120">Request syntax</span></span>

| <span data-ttu-id="e5e52-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="e5e52-121">Method</span></span>  | <span data-ttu-id="e5e52-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="e5e52-122">Request URI</span></span>                                                               |
|---------|---------------------------------------------------------------------------|
| <span data-ttu-id="e5e52-123">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="e5e52-123">**GET**</span></span> | <span data-ttu-id="e5e52-124">*{baseURL}*/V1/ratecards/Azure-Shared? Currency = {currency} &region = {Region}</span><span class="sxs-lookup"><span data-stu-id="e5e52-124">*{baseURL}*/v1/ratecards/azure-shared?currency={currency}&region={region}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="e5e52-125">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="e5e52-125">URI parameters</span></span>

| <span data-ttu-id="e5e52-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e5e52-126">Name</span></span>     | <span data-ttu-id="e5e52-127">Typ</span><span class="sxs-lookup"><span data-stu-id="e5e52-127">Type</span></span>   | <span data-ttu-id="e5e52-128">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e5e52-128">Required</span></span> | <span data-ttu-id="e5e52-129">Opis</span><span class="sxs-lookup"><span data-stu-id="e5e52-129">Description</span></span>                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e5e52-130">currency</span><span class="sxs-lookup"><span data-stu-id="e5e52-130">currency</span></span> | <span data-ttu-id="e5e52-131">ciąg</span><span class="sxs-lookup"><span data-stu-id="e5e52-131">string</span></span> | <span data-ttu-id="e5e52-132">Nie</span><span class="sxs-lookup"><span data-stu-id="e5e52-132">No</span></span>       | <span data-ttu-id="e5e52-133">Opcjonalny trzyliterowy kod ISO dla waluty, w której zostaną podane stawki zasobów (na przykład `EUR` ).</span><span class="sxs-lookup"><span data-stu-id="e5e52-133">Optional three letter ISO code for the currency in which the resource rates will be provided (for example `EUR`).</span></span> <span data-ttu-id="e5e52-134">Wartość domyślna to waluta skojarzona z rynkiem w profilu partnera.</span><span class="sxs-lookup"><span data-stu-id="e5e52-134">The default is the currency associated with the market in the partner profile.</span></span> |
| <span data-ttu-id="e5e52-135">region</span><span class="sxs-lookup"><span data-stu-id="e5e52-135">region</span></span>   | <span data-ttu-id="e5e52-136">ciąg</span><span class="sxs-lookup"><span data-stu-id="e5e52-136">string</span></span> | <span data-ttu-id="e5e52-137">Nie</span><span class="sxs-lookup"><span data-stu-id="e5e52-137">No</span></span>       | <span data-ttu-id="e5e52-138">Opcjonalny dwuliterowy kod kraju/regionu w formacie ISO, który wskazuje rynek zakupu oferty (na przykład `FR` ).</span><span class="sxs-lookup"><span data-stu-id="e5e52-138">Optional two-letter ISO country/region code that indicates the market where the offer is purchased (for example `FR`).</span></span> <span data-ttu-id="e5e52-139">Wartość domyślna to kod kraju/regionu ustawiony w profilu partnera.</span><span class="sxs-lookup"><span data-stu-id="e5e52-139">The default is the country/region code set in the partner profile.</span></span>        |

<span data-ttu-id="e5e52-140">Jeśli opcjonalny nagłówek X-locale zostanie uwzględniony w żądaniu, jego wartość określa język używany dla szczegółów odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e5e52-140">If the optional X-Locale header is included in the request, its value determines the language used for the details in the response.</span></span>

### <a name="request-headers"></a><span data-ttu-id="e5e52-141">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="e5e52-141">Request headers</span></span>

<span data-ttu-id="e5e52-142">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e5e52-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e5e52-143">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="e5e52-143">Request body</span></span>

<span data-ttu-id="e5e52-144">Brak.</span><span class="sxs-lookup"><span data-stu-id="e5e52-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e5e52-145">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="e5e52-145">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="e5e52-146">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="e5e52-146">REST response</span></span>

<span data-ttu-id="e5e52-147">Jeśli żądanie zakończy się pomyślnie, zwraca zasób [karty usługi Azure rate](azure-rate-card-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="e5e52-147">If the request is successful, it returns an [Azure Rate Card](azure-rate-card-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e5e52-148">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e5e52-148">Response success and error codes</span></span>

<span data-ttu-id="e5e52-149">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="e5e52-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e5e52-150">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="e5e52-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e5e52-151">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e5e52-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e5e52-152">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e5e52-152">Response example</span></span>

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
