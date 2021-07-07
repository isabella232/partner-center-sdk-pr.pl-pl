---
title: Uzyskiwanie stanu uaktualnienia produktu dla klienta
description: Możesz użyć zasobu ProductUpgradeRequest, aby określić stan uaktualnienia produktu dla klienta do nowej rodziny produktów, na przykład z subskrypcji usługi Microsoft Azure (MS-AZR-0145P) do planu platformy Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 03d925dd0fae987226ad1f8e71fad380ba144b83
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445565"
---
# <a name="get-the-product-upgrade-status-for-a-customer"></a><span data-ttu-id="20f0e-103">Uzyskiwanie stanu uaktualnienia produktu dla klienta</span><span class="sxs-lookup"><span data-stu-id="20f0e-103">Get the product upgrade status for a customer</span></span>

<span data-ttu-id="20f0e-104">Możesz użyć zasobu [**ProductUpgradeRequest,**](product-upgrade-resources.md#productupgraderequest) aby uzyskać stan uaktualnienia do nowej rodziny produktów.</span><span class="sxs-lookup"><span data-stu-id="20f0e-104">You can use the [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource to get the status of an upgrade to a new product family.</span></span> <span data-ttu-id="20f0e-105">Ten zasób ma zastosowanie w przypadku uaktualniania klienta z subskrypcji Microsoft Azure (MS-AZR-0145P) do planu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="20f0e-105">This resource applies when you're upgrading a customer from a Microsoft Azure (MS-AZR-0145P) subscription to an Azure plan.</span></span> <span data-ttu-id="20f0e-106">Żądanie pomyślne zwraca [**zasób ProductUpgradesEligibility.**](product-upgrade-resources.md#productupgradeseligibility)</span><span class="sxs-lookup"><span data-stu-id="20f0e-106">A successful request returns the [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20f0e-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="20f0e-107">Prerequisites</span></span>

- <span data-ttu-id="20f0e-108">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="20f0e-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="20f0e-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="20f0e-109">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="20f0e-110">Postępuj zgodnie z [modelem bezpiecznej aplikacji w](enable-secure-app-model.md) przypadku korzystania z uwierzytelniania app+user z Partner Center API.</span><span class="sxs-lookup"><span data-stu-id="20f0e-110">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="20f0e-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="20f0e-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="20f0e-112">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="20f0e-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="20f0e-113">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="20f0e-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="20f0e-114">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="20f0e-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="20f0e-115">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="20f0e-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="20f0e-116">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="20f0e-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="20f0e-117">Rodzina produktów.</span><span class="sxs-lookup"><span data-stu-id="20f0e-117">The product family.</span></span>

- <span data-ttu-id="20f0e-118">Identyfikator uaktualnienia żądania uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="20f0e-118">The upgrade-id of an upgrade request.</span></span>

## <a name="c"></a><span data-ttu-id="20f0e-119">C\#</span><span class="sxs-lookup"><span data-stu-id="20f0e-119">C\#</span></span>

<span data-ttu-id="20f0e-120">Aby sprawdzić, czy klient kwalifikuje się do uaktualnienia do planu platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="20f0e-120">To check if a customer is eligible to upgrade to Azure plan:</span></span>

1. <span data-ttu-id="20f0e-121">Utwórz obiekt **ProductUpgradesRequest** i określ identyfikator klienta oraz wartość "Azure" jako rodzinę produktów.</span><span class="sxs-lookup"><span data-stu-id="20f0e-121">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="20f0e-122">Użyj **kolekcji IAggregatePartner.ProductUpgrades.**</span><span class="sxs-lookup"><span data-stu-id="20f0e-122">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>

3. <span data-ttu-id="20f0e-123">Wywołaj **metodę ById** i przekaż **identyfikator upgrade-id**.</span><span class="sxs-lookup"><span data-stu-id="20f0e-123">Call the **ById** method and pass in the **upgrade-id**.</span></span>

4. <span data-ttu-id="20f0e-124">Wywołaj **metodę CheckStatus** i przekaż obiekt **ProductUpgradesRequest,** który zwróci **obiekt ProductUpgradeStatus.**</span><span class="sxs-lookup"><span data-stu-id="20f0e-124">Call the **CheckStatus** method and pass in the **ProductUpgradesRequest** object, which will return a **ProductUpgradeStatus** object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="20f0e-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="20f0e-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="20f0e-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="20f0e-126">Request syntax</span></span>

| <span data-ttu-id="20f0e-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="20f0e-127">Method</span></span>   | <span data-ttu-id="20f0e-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="20f0e-128">Request URI</span></span> |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="20f0e-129">**Post**</span><span class="sxs-lookup"><span data-stu-id="20f0e-129">**POST**</span></span> | <span data-ttu-id="20f0e-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="20f0e-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="20f0e-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="20f0e-131">URI parameter</span></span>

<span data-ttu-id="20f0e-132">Użyj następującego parametru zapytania, aby określić klienta, dla którego jest zwracany stan uaktualnienia produktu.</span><span class="sxs-lookup"><span data-stu-id="20f0e-132">Use the following query parameter to specify the customer for whom you're getting a product upgrade status.</span></span>

| <span data-ttu-id="20f0e-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="20f0e-133">Name</span></span>               | <span data-ttu-id="20f0e-134">Typ</span><span class="sxs-lookup"><span data-stu-id="20f0e-134">Type</span></span> | <span data-ttu-id="20f0e-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="20f0e-135">Required</span></span> | <span data-ttu-id="20f0e-136">Opis</span><span class="sxs-lookup"><span data-stu-id="20f0e-136">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="20f0e-137">**identyfikator uaktualnienia**</span><span class="sxs-lookup"><span data-stu-id="20f0e-137">**upgrade-id**</span></span> | <span data-ttu-id="20f0e-138">GUID</span><span class="sxs-lookup"><span data-stu-id="20f0e-138">GUID</span></span> | <span data-ttu-id="20f0e-139">Tak</span><span class="sxs-lookup"><span data-stu-id="20f0e-139">Yes</span></span> | <span data-ttu-id="20f0e-140">Wartość jest identyfikator uaktualnienia sformatowany identyfikator GUID.</span><span class="sxs-lookup"><span data-stu-id="20f0e-140">The value is a GUID-formatted upgrade identifier.</span></span> <span data-ttu-id="20f0e-141">Ten identyfikator umożliwia określenie uaktualnienia do śledzenia.</span><span class="sxs-lookup"><span data-stu-id="20f0e-141">You can use this identifier to specify an upgrade to track.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="20f0e-142">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="20f0e-142">Request headers</span></span>

<span data-ttu-id="20f0e-143">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="20f0e-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="20f0e-144">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="20f0e-144">Request body</span></span>

<span data-ttu-id="20f0e-145">Treść żądania musi zawierać [**zasób ProductUpgradeRequest.**](product-upgrade-resources.md#productupgraderequest)</span><span class="sxs-lookup"><span data-stu-id="20f0e-145">The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="20f0e-146">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="20f0e-146">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="20f0e-147">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="20f0e-147">REST response</span></span>

<span data-ttu-id="20f0e-148">W przypadku powodzenia ta metoda zwraca [**zasób ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) w treści.</span><span class="sxs-lookup"><span data-stu-id="20f0e-148">If successful, this method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource in the body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="20f0e-149">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="20f0e-149">Response success and error codes</span></span>

<span data-ttu-id="20f0e-150">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="20f0e-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="20f0e-151">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="20f0e-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="20f0e-152">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="20f0e-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="20f0e-153">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="20f0e-153">Response example</span></span>

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
