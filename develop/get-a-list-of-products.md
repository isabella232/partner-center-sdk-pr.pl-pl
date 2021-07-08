---
title: Pobieranie listy produktów (według kraju)
description: Możesz użyć zasobu Product, aby uzyskać kolekcję produktów według kraju klienta.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 1258727ecbe7c5cc332624577fa8a355e28e3717
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874214"
---
# <a name="get-a-list-of-products-by-country"></a><span data-ttu-id="36ce4-103">Pobieranie listy produktów (według kraju)</span><span class="sxs-lookup"><span data-stu-id="36ce4-103">Get a list of products (by country)</span></span>

<span data-ttu-id="36ce4-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="36ce4-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="36ce4-105">Aby uzyskać kolekcję produktów dostępnych w danym kraju, można użyć następujących metod.</span><span class="sxs-lookup"><span data-stu-id="36ce4-105">You can use the following methods to get a collection of products available in a particular country.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36ce4-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="36ce4-106">Prerequisites</span></span>

- <span data-ttu-id="36ce4-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="36ce4-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="36ce4-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="36ce4-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="36ce4-109">Kraj.</span><span class="sxs-lookup"><span data-stu-id="36ce4-109">A country.</span></span>

## <a name="c"></a><span data-ttu-id="36ce4-110">C\#</span><span class="sxs-lookup"><span data-stu-id="36ce4-110">C\#</span></span>

<span data-ttu-id="36ce4-111">Aby uzyskać listę produktów:</span><span class="sxs-lookup"><span data-stu-id="36ce4-111">To get a list of products:</span></span>

1. <span data-ttu-id="36ce4-112">Użyj **kolekcji IAggregatePartner.Products,** aby wybrać kraj przy użyciu **metody ByCountry().**</span><span class="sxs-lookup"><span data-stu-id="36ce4-112">Use your **IAggregatePartner.Products** collection to select the country by using the **ByCountry()** method.</span></span>

2. <span data-ttu-id="36ce4-113">Wybierz widok wykazu przy użyciu **metody ByTargetView().**</span><span class="sxs-lookup"><span data-stu-id="36ce4-113">Select the catalog view using the **ByTargetView()** method.</span></span>

3. <span data-ttu-id="36ce4-114">(Opcjonalnie) Wybierz zakres rezerwacji przy **użyciu metody ByReservationScope().**</span><span class="sxs-lookup"><span data-stu-id="36ce4-114">(Optional) Select the reservation scope using the **ByReservationScope()** method.</span></span>

4. <span data-ttu-id="36ce4-115">(Opcjonalnie) Wybierz segment docelowy przy użyciu **metody ByTargetSegment().**</span><span class="sxs-lookup"><span data-stu-id="36ce4-115">(Optional) Select the target segment using the **ByTargetSegment()** method.</span></span>

5. <span data-ttu-id="36ce4-116">Wywołaj **metodę Get()** lub **GetAsync(),** aby zwrócić kolekcję.</span><span class="sxs-lookup"><span data-stu-id="36ce4-116">Call the **Get()** or **GetAsync()** method to return the collection.</span></span>

```csharp
IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").Get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").ByTargetSegment("commercial").Get();

// Get the products for Azure reservations which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").Get();

// Get the products for Azure reservations which are applicable to Azure plans only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a><span data-ttu-id="36ce4-117">Java</span><span class="sxs-lookup"><span data-stu-id="36ce4-117">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="36ce4-118">Aby uzyskać listę produktów:</span><span class="sxs-lookup"><span data-stu-id="36ce4-118">To get a list of products:</span></span>

1. <span data-ttu-id="36ce4-119">Użyj funkcji **IAggregatePartner.getProducts,** aby wybrać kraj przy użyciu **funkcji byCountry().**</span><span class="sxs-lookup"><span data-stu-id="36ce4-119">Use your **IAggregatePartner.getProducts** function to select the country by using the **byCountry()** function.</span></span>

2. <span data-ttu-id="36ce4-120">Wybierz widok wykazu przy użyciu **funkcji byTargetView().**</span><span class="sxs-lookup"><span data-stu-id="36ce4-120">Select the catalog view using the **byTargetView()** function.</span></span>
3. <span data-ttu-id="36ce4-121">(Opcjonalnie) Wybierz segment docelowy przy użyciu **funkcji byTargetSegment().**</span><span class="sxs-lookup"><span data-stu-id="36ce4-121">(Optional) Select the target segment using the **byTargetSegment()** function.</span></span>

4. <span data-ttu-id="36ce4-122">Wywołaj **funkcję get(),** aby zwrócić kolekcję.</span><span class="sxs-lookup"><span data-stu-id="36ce4-122">Call the **get()** function to return the collection.</span></span>

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## <a name="powershell"></a><span data-ttu-id="36ce4-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="36ce4-123">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="36ce4-124">Aby uzyskać listę produktów:</span><span class="sxs-lookup"><span data-stu-id="36ce4-124">To get a list of products:</span></span>

1. <span data-ttu-id="36ce4-125">Wykonaj polecenie [**Get-PartnerProduct.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md)</span><span class="sxs-lookup"><span data-stu-id="36ce4-125">Execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command.</span></span>

2. <span data-ttu-id="36ce4-126">Wybierz wykaz, określając parametr **Catalog.**</span><span class="sxs-lookup"><span data-stu-id="36ce4-126">Select the catalog by specifying the **Catalog** parameter.</span></span>
3. <span data-ttu-id="36ce4-127">(Opcjonalnie) Wybierz segment docelowy, określając **parametr Segment.**</span><span class="sxs-lookup"><span data-stu-id="36ce4-127">(Optional) Select the target segment by specifying the **Segment** parameter.</span></span>

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a><span data-ttu-id="36ce4-128">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="36ce4-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="36ce4-129">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="36ce4-129">Request syntax</span></span>

| <span data-ttu-id="36ce4-130">Metoda</span><span class="sxs-lookup"><span data-stu-id="36ce4-130">Method</span></span>  | <span data-ttu-id="36ce4-131">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="36ce4-131">Request URI</span></span>                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="36ce4-132">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="36ce4-132">**GET**</span></span> | <span data-ttu-id="36ce4-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="36ce4-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="36ce4-134">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="36ce4-134">URI parameters</span></span>

<span data-ttu-id="36ce4-135">Użyj następującej ścieżki i parametrów zapytania, aby uzyskać listę produktów.</span><span class="sxs-lookup"><span data-stu-id="36ce4-135">Use the following path and query parameters to get a list of products.</span></span>

| <span data-ttu-id="36ce4-136">Nazwa</span><span class="sxs-lookup"><span data-stu-id="36ce4-136">Name</span></span>                   | <span data-ttu-id="36ce4-137">Typ</span><span class="sxs-lookup"><span data-stu-id="36ce4-137">Type</span></span>     | <span data-ttu-id="36ce4-138">Wymagane</span><span class="sxs-lookup"><span data-stu-id="36ce4-138">Required</span></span> | <span data-ttu-id="36ce4-139">Opis</span><span class="sxs-lookup"><span data-stu-id="36ce4-139">Description</span></span>                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| <span data-ttu-id="36ce4-140">country</span><span class="sxs-lookup"><span data-stu-id="36ce4-140">country</span></span>                | <span data-ttu-id="36ce4-141">ciąg</span><span class="sxs-lookup"><span data-stu-id="36ce4-141">string</span></span>   | <span data-ttu-id="36ce4-142">Tak</span><span class="sxs-lookup"><span data-stu-id="36ce4-142">Yes</span></span>      | <span data-ttu-id="36ce4-143">Identyfikator kraju/regionu.</span><span class="sxs-lookup"><span data-stu-id="36ce4-143">The country/region ID.</span></span>                                                  |
| <span data-ttu-id="36ce4-144">targetView</span><span class="sxs-lookup"><span data-stu-id="36ce4-144">targetView</span></span>             | <span data-ttu-id="36ce4-145">ciąg</span><span class="sxs-lookup"><span data-stu-id="36ce4-145">string</span></span>   | <span data-ttu-id="36ce4-146">Tak</span><span class="sxs-lookup"><span data-stu-id="36ce4-146">Yes</span></span>      | <span data-ttu-id="36ce4-147">Określa widok docelowy katalogu.</span><span class="sxs-lookup"><span data-stu-id="36ce4-147">Identifies the target view of the catalog.</span></span> <span data-ttu-id="36ce4-148">Obsługiwane wartości to:</span><span class="sxs-lookup"><span data-stu-id="36ce4-148">The supported values are:</span></span> <br/><br/><span data-ttu-id="36ce4-149">**Azure**, który zawiera wszystkie elementy platformy Azure</span><span class="sxs-lookup"><span data-stu-id="36ce4-149">**Azure**, which includes all Azure items</span></span><br/><br/><span data-ttu-id="36ce4-150">**AzureReservations**, która obejmuje wszystkie elementy rezerwacji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="36ce4-150">**AzureReservations**, which includes all Azure reservation items</span></span><br/><br/><span data-ttu-id="36ce4-151">**AzureReservationsVM,** która zawiera wszystkie elementy rezerwacji maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="36ce4-151">**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</span></span><br/><br/><span data-ttu-id="36ce4-152">**AzureReservationsSQL**, który zawiera wszystkie SQL elementów rezerwacji</span><span class="sxs-lookup"><span data-stu-id="36ce4-152">**AzureReservationsSQL**, which includes all SQL reservation items</span></span><br/><br/><span data-ttu-id="36ce4-153">**AzureReservationsCosmosDb,** który zawiera wszystkie Cosmos rezerwacji bazy danych</span><span class="sxs-lookup"><span data-stu-id="36ce4-153">**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</span></span><br/><br/><span data-ttu-id="36ce4-154">**MicrosoftAzure**, który zawiera elementy dla Microsoft Azure subskrypcji **(MS-AZR-0145P)** i planów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="36ce4-154">**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</span></span><br/><br/><span data-ttu-id="36ce4-155">**OnlineServices**, który obejmuje wszystkie elementy usług online (w tym produkty platformy handlowej)</span><span class="sxs-lookup"><span data-stu-id="36ce4-155">**OnlineServices**, which includes all online service items (including commercial marketplace products)</span></span><br/><br/><span data-ttu-id="36ce4-156">**Oprogramowanie**, które zawiera wszystkie elementy oprogramowania</span><span class="sxs-lookup"><span data-stu-id="36ce4-156">**Software**, which includes all software items</span></span><br/><br/><span data-ttu-id="36ce4-157">**SoftwareSUSELinux**, który zawiera wszystkie elementy oprogramowania SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="36ce4-157">**SoftwareSUSELinux**, which includes all software SUSE Linux items</span></span><br/><br/><span data-ttu-id="36ce4-158">**SoftwarePerpetual**, który obejmuje wszystkie bezterminowe elementy oprogramowania</span><span class="sxs-lookup"><span data-stu-id="36ce4-158">**SoftwarePerpetual**, which includes all perpetual software items</span></span><br/><br/><span data-ttu-id="36ce4-159">**SoftwareSubscriptions**, która obejmuje wszystkie elementy subskrypcji oprogramowania</span><span class="sxs-lookup"><span data-stu-id="36ce4-159">**SoftwareSubscriptions**, which includes all software subscription items</span></span>    |
| <span data-ttu-id="36ce4-160">targetSegment</span><span class="sxs-lookup"><span data-stu-id="36ce4-160">targetSegment</span></span>          | <span data-ttu-id="36ce4-161">ciąg</span><span class="sxs-lookup"><span data-stu-id="36ce4-161">string</span></span>   | <span data-ttu-id="36ce4-162">Nie</span><span class="sxs-lookup"><span data-stu-id="36ce4-162">No</span></span>       | <span data-ttu-id="36ce4-163">Identyfikuje segment docelowy.</span><span class="sxs-lookup"><span data-stu-id="36ce4-163">Identifies the target segment.</span></span> <span data-ttu-id="36ce4-164">Widok dla różnych odbiorców docelowych.</span><span class="sxs-lookup"><span data-stu-id="36ce4-164">The view for different target audiences.</span></span> <span data-ttu-id="36ce4-165">Obsługiwane wartości to:</span><span class="sxs-lookup"><span data-stu-id="36ce4-165">The supported values are:</span></span> <br/><br/><span data-ttu-id="36ce4-166">**Handlowych**</span><span class="sxs-lookup"><span data-stu-id="36ce4-166">**commercial**</span></span><br/><span data-ttu-id="36ce4-167">**Edukacji**</span><span class="sxs-lookup"><span data-stu-id="36ce4-167">**education**</span></span><br/><span data-ttu-id="36ce4-168">**Rząd**</span><span class="sxs-lookup"><span data-stu-id="36ce4-168">**government**</span></span><br/><span data-ttu-id="36ce4-169">**Non-profit**</span><span class="sxs-lookup"><span data-stu-id="36ce4-169">**nonprofit**</span></span>  |
| <span data-ttu-id="36ce4-170">reservationScope (zakres rezerwacji)</span><span class="sxs-lookup"><span data-stu-id="36ce4-170">reservationScope</span></span> | <span data-ttu-id="36ce4-171">ciąg</span><span class="sxs-lookup"><span data-stu-id="36ce4-171">string</span></span>   | <span data-ttu-id="36ce4-172">Nie</span><span class="sxs-lookup"><span data-stu-id="36ce4-172">No</span></span> | <span data-ttu-id="36ce4-173">Podczas wykonywania zapytania o listę produktów dla rezerwacji platformy Azure określ, aby uzyskać listę produktów, które `reservationScope=AzurePlan` mają zastosowanie do planów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36ce4-173">When querying for a list of products for Azure Reservations, specify `reservationScope=AzurePlan` to get a list of products that are applicable to Azure plans.</span></span> <span data-ttu-id="36ce4-174">Wyklucz ten parametr, aby uzyskać listę produktów dla rezerwacji platformy Azure, które mają zastosowanie do subskrypcji Microsoft Azure **(MS-AZR-0145P).**</span><span class="sxs-lookup"><span data-stu-id="36ce4-174">Exclude this parameter to get a list of products for Azure reservations, which are applicable to Microsoft Azure (**MS-AZR-0145P**) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="36ce4-175">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="36ce4-175">Request headers</span></span>

<span data-ttu-id="36ce4-176">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="36ce4-176">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="36ce4-177">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="36ce4-177">Request body</span></span>

<span data-ttu-id="36ce4-178">Brak.</span><span class="sxs-lookup"><span data-stu-id="36ce4-178">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="36ce4-179">Przykłady żądań</span><span class="sxs-lookup"><span data-stu-id="36ce4-179">Request examples</span></span>

#### <a name="products-by-country"></a><span data-ttu-id="36ce4-180">Produkty według kraju</span><span class="sxs-lookup"><span data-stu-id="36ce4-180">Products by country</span></span>

<span data-ttu-id="36ce4-181">Postępuj zgodnie z tym przykładem, aby uzyskać listę produktów według kraju dla subskrypcji Microsoft Azure (MS-AZR-0145P) i planów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36ce4-181">Follow this example to get a list of products by country for Microsoft Azure (MS-AZR-0145P) subscriptions and Azure plans.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a><span data-ttu-id="36ce4-182">Rezerwacje maszyn wirtualnych platformy Azure (plan platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="36ce4-182">Azure VM reservations (Azure plan)</span></span>

<span data-ttu-id="36ce4-183">Postępuj zgodnie z tym przykładem, aby uzyskać listę produktów według krajów dla rezerwacji maszyn wirtualnych platformy Azure, które mają zastosowanie do planów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36ce4-183">Follow this example to get a list of products by country for Azure VM reservations that are applicable to Azure plans.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="36ce4-184">Rezerwacje maszyn wirtualnych platformy Azure Microsoft Azure subskrypcji platformy Azure (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="36ce4-184">Azure VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="36ce4-185">Postępuj zgodnie z tym przykładem, aby uzyskać listę produktów według kraju dla rezerwacji maszyn wirtualnych platformy Azure, które mają zastosowanie do subskrypcji usługi Microsoft Azure (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="36ce4-185">Follow this example to get a list of products by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="36ce4-186">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="36ce4-186">REST response</span></span>

<span data-ttu-id="36ce4-187">W przypadku powodzenia treść odpowiedzi zawiera kolekcję [**zasobów**](product-resources.md#product) produktu.</span><span class="sxs-lookup"><span data-stu-id="36ce4-187">If successful, the response body contains a collection of [**Product**](product-resources.md#product) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="36ce4-188">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="36ce4-188">Response success and error codes</span></span>

<span data-ttu-id="36ce4-189">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="36ce4-189">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="36ce4-190">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="36ce4-190">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="36ce4-191">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="36ce4-191">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="36ce4-192">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="36ce4-192">This method returns the following error codes:</span></span>

| <span data-ttu-id="36ce4-193">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="36ce4-193">HTTP Status Code</span></span>     | <span data-ttu-id="36ce4-194">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="36ce4-194">Error code</span></span>   | <span data-ttu-id="36ce4-195">Opis</span><span class="sxs-lookup"><span data-stu-id="36ce4-195">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="36ce4-196">403</span><span class="sxs-lookup"><span data-stu-id="36ce4-196">403</span></span>                  | <span data-ttu-id="36ce4-197">400030</span><span class="sxs-lookup"><span data-stu-id="36ce4-197">400030</span></span>       | <span data-ttu-id="36ce4-198">Dostęp do żądanego obiektu targetSegment jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="36ce4-198">Access to the requested targetSegment is not allowed.</span></span>                                                     |
| <span data-ttu-id="36ce4-199">403</span><span class="sxs-lookup"><span data-stu-id="36ce4-199">403</span></span>                  | <span data-ttu-id="36ce4-200">400036</span><span class="sxs-lookup"><span data-stu-id="36ce4-200">400036</span></span>       | <span data-ttu-id="36ce4-201">Dostęp do żądanego obiektu targetView nie jest dozwolony.</span><span class="sxs-lookup"><span data-stu-id="36ce4-201">Access to the requested targetView is not allowed.</span></span>                                                        |

### <a name="response-example"></a><span data-ttu-id="36ce4-202">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="36ce4-202">Response example</span></span>

```http
{
    "totalCount": 19,
    "items": [
        {
            "id": "DZH318Z0BQ3Q",
            "title": "Virtual Machines DSv2 Series",
            "description": "Dsv2-series instances are the latest generation of D-series instances that will carry more powerful CPUs which are on average about 35% faster than D-series instances, and carry the same memory and disk configurations as the D-series. Dsv2-series instances are based on the latest generation 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) processor, and with Intel Turbo Boost Technology 2.0 can go to 3.2 GHz.",
            "productType": {
                "id": "Azure",
                "displayName": "Azure",
                "subType": {
                "id": "VirtualMachines",
                "displayName": "VirtualMachines"
                }
            },
            "isMicrosoftProduct": true,
            "publisherName": "Microsoft",
            "links": {
                "skus": {
                    "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BQ3Q?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        ...
    ],
    "links": {
        "self": {
            "uri": "/products?country=US&targetView=Azure",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
