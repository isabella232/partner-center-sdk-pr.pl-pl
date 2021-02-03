---
title: Pobieranie listy produktów (według kraju)
description: Możesz użyć zasobu produktu, aby uzyskać zbiór produktów według kraju klienta.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ea239aa008a5b7c33740e9c4697c3795908415cd
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768173"
---
# <a name="get-a-list-of-products-by-country"></a><span data-ttu-id="b5b29-103">Pobieranie listy produktów (według kraju)</span><span class="sxs-lookup"><span data-stu-id="b5b29-103">Get a list of products (by country)</span></span>

<span data-ttu-id="b5b29-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="b5b29-104">**Applies to:**</span></span>

- <span data-ttu-id="b5b29-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="b5b29-105">Partner Center</span></span>
- <span data-ttu-id="b5b29-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="b5b29-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="b5b29-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="b5b29-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="b5b29-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b5b29-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b5b29-109">Poniższe metody umożliwiają pobranie kolekcji produktów dostępnych w danym kraju.</span><span class="sxs-lookup"><span data-stu-id="b5b29-109">You can use the following methods to get a collection of products available in a particular country.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5b29-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b5b29-110">Prerequisites</span></span>

- <span data-ttu-id="b5b29-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b5b29-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b5b29-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b5b29-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b5b29-113">Kraj.</span><span class="sxs-lookup"><span data-stu-id="b5b29-113">A country.</span></span>

## <a name="c"></a><span data-ttu-id="b5b29-114">C\#</span><span class="sxs-lookup"><span data-stu-id="b5b29-114">C\#</span></span>

<span data-ttu-id="b5b29-115">Aby uzyskać listę produktów:</span><span class="sxs-lookup"><span data-stu-id="b5b29-115">To get a list of products:</span></span>

1. <span data-ttu-id="b5b29-116">Użyj kolekcji **IAggregatePartner. Products** , aby wybrać kraj przy użyciu metody **ByCountry ()** .</span><span class="sxs-lookup"><span data-stu-id="b5b29-116">Use your **IAggregatePartner.Products** collection to select the country by using the **ByCountry()** method.</span></span>

2. <span data-ttu-id="b5b29-117">Wybierz widok wykazu przy użyciu metody **ByTargetView ()** .</span><span class="sxs-lookup"><span data-stu-id="b5b29-117">Select the catalog view using the **ByTargetView()** method.</span></span>

3. <span data-ttu-id="b5b29-118">Obowiązkowe Wybierz zakres rezerwacji przy użyciu metody **ByReservationScope ()** .</span><span class="sxs-lookup"><span data-stu-id="b5b29-118">(Optional) Select the reservation scope using the **ByReservationScope()** method.</span></span>

4. <span data-ttu-id="b5b29-119">Obowiązkowe Wybierz segment docelowy przy użyciu metody **ByTargetSegment ()** .</span><span class="sxs-lookup"><span data-stu-id="b5b29-119">(Optional) Select the target segment using the **ByTargetSegment()** method.</span></span>

5. <span data-ttu-id="b5b29-120">Wywołaj metodę **Get ()** lub **GetAsync ()** w celu zwrócenia kolekcji.</span><span class="sxs-lookup"><span data-stu-id="b5b29-120">Call the **Get()** or **GetAsync()** method to return the collection.</span></span>

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

## <a name="java"></a><span data-ttu-id="b5b29-121">Java</span><span class="sxs-lookup"><span data-stu-id="b5b29-121">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="b5b29-122">Aby uzyskać listę produktów:</span><span class="sxs-lookup"><span data-stu-id="b5b29-122">To get a list of products:</span></span>

1. <span data-ttu-id="b5b29-123">Użyj funkcji **IAggregatePartner. getProducts** , aby wybrać kraj przy użyciu funkcji **byCountry ()** .</span><span class="sxs-lookup"><span data-stu-id="b5b29-123">Use your **IAggregatePartner.getProducts** function to select the country by using the **byCountry()** function.</span></span>

2. <span data-ttu-id="b5b29-124">Wybierz widok wykazu przy użyciu funkcji **byTargetView ()** .</span><span class="sxs-lookup"><span data-stu-id="b5b29-124">Select the catalog view using the **byTargetView()** function.</span></span>
3. <span data-ttu-id="b5b29-125">Obowiązkowe Wybierz segment docelowy przy użyciu funkcji **byTargetSegment ()** .</span><span class="sxs-lookup"><span data-stu-id="b5b29-125">(Optional) Select the target segment using the **byTargetSegment()** function.</span></span>

4. <span data-ttu-id="b5b29-126">Wywołaj funkcję **Get ()** w celu zwrócenia kolekcji.</span><span class="sxs-lookup"><span data-stu-id="b5b29-126">Call the **get()** function to return the collection.</span></span>

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## <a name="powershell"></a><span data-ttu-id="b5b29-127">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b5b29-127">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="b5b29-128">Aby uzyskać listę produktów:</span><span class="sxs-lookup"><span data-stu-id="b5b29-128">To get a list of products:</span></span>

1. <span data-ttu-id="b5b29-129">Wykonaj polecenie [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) .</span><span class="sxs-lookup"><span data-stu-id="b5b29-129">Execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command.</span></span>

2. <span data-ttu-id="b5b29-130">Wybierz katalog, określając parametr **wykazu** .</span><span class="sxs-lookup"><span data-stu-id="b5b29-130">Select the catalog by specifying the **Catalog** parameter.</span></span>
3. <span data-ttu-id="b5b29-131">Obowiązkowe Wybierz segment docelowy, określając parametr **segmentu** .</span><span class="sxs-lookup"><span data-stu-id="b5b29-131">(Optional) Select the target segment by specifying the **Segment** parameter.</span></span>

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a><span data-ttu-id="b5b29-132">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="b5b29-132">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b5b29-133">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="b5b29-133">Request syntax</span></span>

| <span data-ttu-id="b5b29-134">Metoda</span><span class="sxs-lookup"><span data-stu-id="b5b29-134">Method</span></span>  | <span data-ttu-id="b5b29-135">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="b5b29-135">Request URI</span></span>                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="b5b29-136">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="b5b29-136">**GET**</span></span> | <span data-ttu-id="b5b29-137">[*{baseURL}*](partner-center-rest-urls.md)/V1/Products? Country = {country} &targetView = {targetView} &targetSegment = {TARGETSEGMENT} http/1.1</span><span class="sxs-lookup"><span data-stu-id="b5b29-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="b5b29-138">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="b5b29-138">URI parameters</span></span>

<span data-ttu-id="b5b29-139">Użyj następującej ścieżki i parametrów zapytania, aby uzyskać listę produktów.</span><span class="sxs-lookup"><span data-stu-id="b5b29-139">Use the following path and query parameters to get a list of products.</span></span>

| <span data-ttu-id="b5b29-140">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b5b29-140">Name</span></span>                   | <span data-ttu-id="b5b29-141">Typ</span><span class="sxs-lookup"><span data-stu-id="b5b29-141">Type</span></span>     | <span data-ttu-id="b5b29-142">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b5b29-142">Required</span></span> | <span data-ttu-id="b5b29-143">Opis</span><span class="sxs-lookup"><span data-stu-id="b5b29-143">Description</span></span>                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| <span data-ttu-id="b5b29-144">country</span><span class="sxs-lookup"><span data-stu-id="b5b29-144">country</span></span>                | <span data-ttu-id="b5b29-145">ciąg</span><span class="sxs-lookup"><span data-stu-id="b5b29-145">string</span></span>   | <span data-ttu-id="b5b29-146">Tak</span><span class="sxs-lookup"><span data-stu-id="b5b29-146">Yes</span></span>      | <span data-ttu-id="b5b29-147">Identyfikator kraju/regionu.</span><span class="sxs-lookup"><span data-stu-id="b5b29-147">The country/region ID.</span></span>                                                  |
| <span data-ttu-id="b5b29-148">targetView</span><span class="sxs-lookup"><span data-stu-id="b5b29-148">targetView</span></span>             | <span data-ttu-id="b5b29-149">ciąg</span><span class="sxs-lookup"><span data-stu-id="b5b29-149">string</span></span>   | <span data-ttu-id="b5b29-150">Tak</span><span class="sxs-lookup"><span data-stu-id="b5b29-150">Yes</span></span>      | <span data-ttu-id="b5b29-151">Identyfikuje widok docelowy wykazu.</span><span class="sxs-lookup"><span data-stu-id="b5b29-151">Identifies the target view of the catalog.</span></span> <span data-ttu-id="b5b29-152">Obsługiwane są następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="b5b29-152">The supported values are:</span></span> <br/><br/><span data-ttu-id="b5b29-153">**Azure**, w tym wszystkie elementy platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b5b29-153">**Azure**, which includes all Azure items</span></span><br/><br/><span data-ttu-id="b5b29-154">**AzureReservations**, która obejmuje wszystkie elementy rezerwacji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b5b29-154">**AzureReservations**, which includes all Azure reservation items</span></span><br/><br/><span data-ttu-id="b5b29-155">**AzureReservationsVM**, w tym wszystkie elementy rezerwacji maszyny wirtualnej (VM)</span><span class="sxs-lookup"><span data-stu-id="b5b29-155">**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</span></span><br/><br/><span data-ttu-id="b5b29-156">**AzureReservationsSQL**, która obejmuje wszystkie elementy rezerwacji SQL</span><span class="sxs-lookup"><span data-stu-id="b5b29-156">**AzureReservationsSQL**, which includes all SQL reservation items</span></span><br/><br/><span data-ttu-id="b5b29-157">**AzureReservationsCosmosDb**, która obejmuje wszystkie elementy zastrzeżeń bazy danych Cosmos</span><span class="sxs-lookup"><span data-stu-id="b5b29-157">**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</span></span><br/><br/><span data-ttu-id="b5b29-158">**MicrosoftAzure**, w tym elementy subskrypcji Microsoft Azure (**MS-AZR-0145P**) i plany platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b5b29-158">**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</span></span><br/><br/><span data-ttu-id="b5b29-159">**OnlineServices**, która obejmuje wszystkie elementy usługi online (w tym komercyjne produkty Marketplace)</span><span class="sxs-lookup"><span data-stu-id="b5b29-159">**OnlineServices**, which includes all online service items (including commercial marketplace products)</span></span><br/><br/><span data-ttu-id="b5b29-160">**Oprogramowanie**, które obejmuje wszystkie elementy oprogramowania</span><span class="sxs-lookup"><span data-stu-id="b5b29-160">**Software**, which includes all software items</span></span><br/><br/><span data-ttu-id="b5b29-161">**SoftwareSUSELinux**, który obejmuje wszystkie elementy oprogramowania SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="b5b29-161">**SoftwareSUSELinux**, which includes all software SUSE Linux items</span></span><br/><br/><span data-ttu-id="b5b29-162">**SoftwarePerpetual**, który obejmuje wszystkie bezterminowe elementy oprogramowania</span><span class="sxs-lookup"><span data-stu-id="b5b29-162">**SoftwarePerpetual**, which includes all perpetual software items</span></span><br/><br/><span data-ttu-id="b5b29-163">**SoftwareSubscriptions** obejmujący wszystkie elementy subskrypcji oprogramowania</span><span class="sxs-lookup"><span data-stu-id="b5b29-163">**SoftwareSubscriptions**, which includes all software subscription items</span></span>    |
| <span data-ttu-id="b5b29-164">targetSegment</span><span class="sxs-lookup"><span data-stu-id="b5b29-164">targetSegment</span></span>          | <span data-ttu-id="b5b29-165">ciąg</span><span class="sxs-lookup"><span data-stu-id="b5b29-165">string</span></span>   | <span data-ttu-id="b5b29-166">Nie</span><span class="sxs-lookup"><span data-stu-id="b5b29-166">No</span></span>       | <span data-ttu-id="b5b29-167">Identyfikuje segment docelowy.</span><span class="sxs-lookup"><span data-stu-id="b5b29-167">Identifies the target segment.</span></span> <span data-ttu-id="b5b29-168">Widok dla różnych docelowych odbiorców.</span><span class="sxs-lookup"><span data-stu-id="b5b29-168">The view for different target audiences.</span></span> <span data-ttu-id="b5b29-169">Obsługiwane są następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="b5b29-169">The supported values are:</span></span> <br/><br/><span data-ttu-id="b5b29-170">**lekki**</span><span class="sxs-lookup"><span data-stu-id="b5b29-170">**commercial**</span></span><br/><span data-ttu-id="b5b29-171">**oświat**</span><span class="sxs-lookup"><span data-stu-id="b5b29-171">**education**</span></span><br/><span data-ttu-id="b5b29-172">**Zarządowi**</span><span class="sxs-lookup"><span data-stu-id="b5b29-172">**government**</span></span><br/><span data-ttu-id="b5b29-173">**non profit**</span><span class="sxs-lookup"><span data-stu-id="b5b29-173">**nonprofit**</span></span>  |
| <span data-ttu-id="b5b29-174">reservationScope</span><span class="sxs-lookup"><span data-stu-id="b5b29-174">reservationScope</span></span> | <span data-ttu-id="b5b29-175">ciąg</span><span class="sxs-lookup"><span data-stu-id="b5b29-175">string</span></span>   | <span data-ttu-id="b5b29-176">Nie</span><span class="sxs-lookup"><span data-stu-id="b5b29-176">No</span></span> | <span data-ttu-id="b5b29-177">Podczas wykonywania zapytania dotyczącego listy produktów dla Azure Reservations należy określić, `reservationScope=AzurePlan` Aby uzyskać listę produktów, które mają zastosowanie do planów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b5b29-177">When querying for a list of products for Azure Reservations, specify `reservationScope=AzurePlan` to get a list of products that are applicable to Azure plans.</span></span> <span data-ttu-id="b5b29-178">Wyklucz ten parametr, aby uzyskać listę produktów dla rezerwacji platformy Azure, które mają zastosowanie do subskrypcji Microsoft Azure (**MS-AZR-0145P**).</span><span class="sxs-lookup"><span data-stu-id="b5b29-178">Exclude this parameter to get a list of products for Azure reservations, which are applicable to Microsoft Azure (**MS-AZR-0145P**) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="b5b29-179">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="b5b29-179">Request headers</span></span>

<span data-ttu-id="b5b29-180">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b5b29-180">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b5b29-181">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="b5b29-181">Request body</span></span>

<span data-ttu-id="b5b29-182">Brak.</span><span class="sxs-lookup"><span data-stu-id="b5b29-182">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="b5b29-183">Przykłady żądań</span><span class="sxs-lookup"><span data-stu-id="b5b29-183">Request examples</span></span>

#### <a name="products-by-country"></a><span data-ttu-id="b5b29-184">Produkty według kraju</span><span class="sxs-lookup"><span data-stu-id="b5b29-184">Products by country</span></span>

<span data-ttu-id="b5b29-185">Postępuj zgodnie z tym przykładem, aby uzyskać listę produktów według kraju dla subskrypcji Microsoft Azure (MS-AZR-0145P) i planów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b5b29-185">Follow this example to get a list of products by country for Microsoft Azure (MS-AZR-0145P) subscriptions and Azure plans.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a><span data-ttu-id="b5b29-186">Rezerwacje maszyn wirtualnych platformy Azure (plan platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="b5b29-186">Azure VM reservations (Azure plan)</span></span>

<span data-ttu-id="b5b29-187">Postępuj zgodnie z tym przykładem, aby uzyskać listę produktów według kraju dla rezerwacji maszyn wirtualnych platformy Azure, które mają zastosowanie do planów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b5b29-187">Follow this example to get a list of products by country for Azure VM reservations that are applicable to Azure plans.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="b5b29-188">Rezerwacje maszyn wirtualnych platformy Azure dla subskrypcji Microsoft Azure (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="b5b29-188">Azure VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="b5b29-189">Postępuj zgodnie z tym przykładem, aby uzyskać listę produktów według kraju dla rezerwacji maszyn wirtualnych platformy Azure, które mają zastosowanie do subskrypcji Microsoft Azure (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="b5b29-189">Follow this example to get a list of products by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="b5b29-190">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="b5b29-190">REST response</span></span>

<span data-ttu-id="b5b29-191">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [**produktu**](product-resources.md#product) .</span><span class="sxs-lookup"><span data-stu-id="b5b29-191">If successful, the response body contains a collection of [**Product**](product-resources.md#product) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b5b29-192">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b5b29-192">Response success and error codes</span></span>

<span data-ttu-id="b5b29-193">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="b5b29-193">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b5b29-194">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="b5b29-194">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b5b29-195">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b5b29-195">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="b5b29-196">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="b5b29-196">This method returns the following error codes:</span></span>

| <span data-ttu-id="b5b29-197">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="b5b29-197">HTTP Status Code</span></span>     | <span data-ttu-id="b5b29-198">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="b5b29-198">Error code</span></span>   | <span data-ttu-id="b5b29-199">Opis</span><span class="sxs-lookup"><span data-stu-id="b5b29-199">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b5b29-200">403</span><span class="sxs-lookup"><span data-stu-id="b5b29-200">403</span></span>                  | <span data-ttu-id="b5b29-201">400030</span><span class="sxs-lookup"><span data-stu-id="b5b29-201">400030</span></span>       | <span data-ttu-id="b5b29-202">Nie można uzyskać dostępu do żądanego targetSegment.</span><span class="sxs-lookup"><span data-stu-id="b5b29-202">Access to the requested targetSegment is not allowed.</span></span>                                                     |
| <span data-ttu-id="b5b29-203">403</span><span class="sxs-lookup"><span data-stu-id="b5b29-203">403</span></span>                  | <span data-ttu-id="b5b29-204">400036</span><span class="sxs-lookup"><span data-stu-id="b5b29-204">400036</span></span>       | <span data-ttu-id="b5b29-205">Nie można uzyskać dostępu do żądanego targetView.</span><span class="sxs-lookup"><span data-stu-id="b5b29-205">Access to the requested targetView is not allowed.</span></span>                                                        |

### <a name="response-example"></a><span data-ttu-id="b5b29-206">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b5b29-206">Response example</span></span>

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
