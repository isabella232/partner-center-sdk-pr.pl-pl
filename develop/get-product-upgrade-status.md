---
title: Pobieranie stanu uaktualnienia produktu dla klienta
description: Za pomocą zasobu ProductUpgradeRequest można określić stan uaktualnienia produktu dla klienta do nowej rodziny produktów, np. z subskrypcji Microsoft Azure (MS-AZR-0145P) do planu platformy Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1819887d459ec72a48ea2b7a5a4121dc56718313
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767914"
---
# <a name="get-the-product-upgrade-status-for-a-customer"></a><span data-ttu-id="5584d-103">Pobieranie stanu uaktualnienia produktu dla klienta</span><span class="sxs-lookup"><span data-stu-id="5584d-103">Get the product upgrade status for a customer</span></span>

<span data-ttu-id="5584d-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="5584d-104">**Applies to:**</span></span>

- <span data-ttu-id="5584d-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="5584d-105">Partner Center</span></span>

<span data-ttu-id="5584d-106">Za pomocą zasobu [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) można pobrać stan uaktualnienia do nowej rodziny produktów.</span><span class="sxs-lookup"><span data-stu-id="5584d-106">You can use the [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource to get the status of an upgrade to a new product family.</span></span> <span data-ttu-id="5584d-107">Ten zasób jest stosowany podczas uaktualniania klienta z subskrypcji Microsoft Azure (MS-AZR-0145P) do planu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5584d-107">This resource applies when you're upgrading a customer from an Microsoft Azure (MS-AZR-0145P) subscription to an Azure plan.</span></span> <span data-ttu-id="5584d-108">Pomyślne żądanie zwraca zasób [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) .</span><span class="sxs-lookup"><span data-stu-id="5584d-108">A successful request returns the [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5584d-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5584d-109">Prerequisites</span></span>

- <span data-ttu-id="5584d-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5584d-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5584d-111">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5584d-111">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="5584d-112">Postępuj zgodnie z [bezpiecznym modelem aplikacji](enable-secure-app-model.md) podczas korzystania z aplikacji i uwierzytelniania użytkowników za pomocą interfejsów API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="5584d-112">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="5584d-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5584d-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5584d-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="5584d-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5584d-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="5584d-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5584d-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="5584d-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5584d-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="5584d-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5584d-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5584d-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="5584d-119">Rodzina produktów.</span><span class="sxs-lookup"><span data-stu-id="5584d-119">The product family.</span></span>

- <span data-ttu-id="5584d-120">Identyfikator uaktualnienia żądania uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="5584d-120">The upgrade-id of an upgrade request.</span></span>

## <a name="c"></a><span data-ttu-id="5584d-121">C\#</span><span class="sxs-lookup"><span data-stu-id="5584d-121">C\#</span></span>

<span data-ttu-id="5584d-122">Aby sprawdzić, czy klient kwalifikuje się do uaktualnienia do planu platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="5584d-122">To check if a customer is eligible to upgrade to Azure plan:</span></span>

1. <span data-ttu-id="5584d-123">Utwórz obiekt **ProductUpgradesRequest** i określ identyfikator klienta oraz "Azure" jako rodzinę produktów.</span><span class="sxs-lookup"><span data-stu-id="5584d-123">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="5584d-124">Użyj kolekcji **IAggregatePartner. ProductUpgrades** .</span><span class="sxs-lookup"><span data-stu-id="5584d-124">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>

3. <span data-ttu-id="5584d-125">Wywołaj metodę **ById** i przekaż **Identyfikator upgrade-ID**.</span><span class="sxs-lookup"><span data-stu-id="5584d-125">Call the **ById** method and pass in the **upgrade-id**.</span></span>

4. <span data-ttu-id="5584d-126">Wywołaj metodę **checkStatus** i przekaż obiekt **ProductUpgradesRequest** , który zwróci obiekt **ProductUpgradeStatus** .</span><span class="sxs-lookup"><span data-stu-id="5584d-126">Call the **CheckStatus** method and pass in the **ProductUpgradesRequest** object, which will return a **ProductUpgradeStatus** object.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesStatus productUpgradeStatus = partnerOperations.ProductUpgrades.ById(selectedUpgradeId).CheckStatus(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest-request"></a><span data-ttu-id="5584d-127">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="5584d-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5584d-128">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="5584d-128">Request syntax</span></span>

| <span data-ttu-id="5584d-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="5584d-129">Method</span></span>   | <span data-ttu-id="5584d-130">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="5584d-130">Request URI</span></span> |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="5584d-131">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="5584d-131">**POST**</span></span> | <span data-ttu-id="5584d-132">[*{baseURL}*](partner-center-rest-urls.md)/V1/productUpgrades/{upgrade-ID}/status http/1.1</span><span class="sxs-lookup"><span data-stu-id="5584d-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="5584d-133">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="5584d-133">URI parameter</span></span>

<span data-ttu-id="5584d-134">Użyj następującego parametru zapytania, aby określić klienta, dla którego otrzymujesz stan uaktualnienia produktu.</span><span class="sxs-lookup"><span data-stu-id="5584d-134">Use the following query parameter to specify the customer for whom you're getting a product upgrade status.</span></span>

| <span data-ttu-id="5584d-135">Nazwa</span><span class="sxs-lookup"><span data-stu-id="5584d-135">Name</span></span>               | <span data-ttu-id="5584d-136">Typ</span><span class="sxs-lookup"><span data-stu-id="5584d-136">Type</span></span> | <span data-ttu-id="5584d-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="5584d-137">Required</span></span> | <span data-ttu-id="5584d-138">Opis</span><span class="sxs-lookup"><span data-stu-id="5584d-138">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="5584d-139">**Identyfikator uaktualnienia**</span><span class="sxs-lookup"><span data-stu-id="5584d-139">**upgrade-id**</span></span> | <span data-ttu-id="5584d-140">GUID</span><span class="sxs-lookup"><span data-stu-id="5584d-140">GUID</span></span> | <span data-ttu-id="5584d-141">Tak</span><span class="sxs-lookup"><span data-stu-id="5584d-141">Yes</span></span> | <span data-ttu-id="5584d-142">Wartość jest identyfikatorem uaktualnienia sformatowanym przez identyfikator GUID.</span><span class="sxs-lookup"><span data-stu-id="5584d-142">The value is a GUID-formatted upgrade identifier.</span></span> <span data-ttu-id="5584d-143">Możesz użyć tego identyfikatora, aby określić uaktualnienie do śledzenia.</span><span class="sxs-lookup"><span data-stu-id="5584d-143">You can use this identifier to specify an upgrade to track.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5584d-144">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="5584d-144">Request headers</span></span>

<span data-ttu-id="5584d-145">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5584d-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5584d-146">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="5584d-146">Request body</span></span>

<span data-ttu-id="5584d-147">Treść żądania musi zawierać zasób [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) .</span><span class="sxs-lookup"><span data-stu-id="5584d-147">The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="5584d-148">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="5584d-148">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4/status  HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
 {
    "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
    "productFamily": "azure"
  }
  "Attributes": {
  "ObjectType": "ProductUpgradeRequest"
  }
}
```

## <a name="rest-response"></a><span data-ttu-id="5584d-149">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="5584d-149">REST response</span></span>

<span data-ttu-id="5584d-150">Jeśli to się powiedzie, metoda zwraca zasób [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) w treści.</span><span class="sxs-lookup"><span data-stu-id="5584d-150">If successful, this method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource in the body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5584d-151">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="5584d-151">Response success and error codes</span></span>

<span data-ttu-id="5584d-152">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="5584d-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5584d-153">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="5584d-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5584d-154">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5584d-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5584d-155">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="5584d-155">Response example</span></span>

```http
HTTP/1.1 200 Ok
Content-Length: 150
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 04 Oct 2019 20:35:35 GMT

{
    "id": "42d075a4-bfe7-43e7-af6d-7c68a57edcb4",
    "status": "Completed",
    "productFamily": "Azure",
    "lineItems": [
        {
            "sourceProduct": {
                "id": "b1beb621-3cad-4d7a-b360-62db33ce028e",
                "name": "AzureSubscription"
            },
            "targetProduct": {
                "id": "d231908e-31c1-de0e-027b-bc5ce11f09d9",
                "name": "Microsoft Azure plan"
            },
            "upgradedDate": "2019-08-29T23:47:28.8524555Z",
            "status": "Completed"
        }
    ]
}

```
