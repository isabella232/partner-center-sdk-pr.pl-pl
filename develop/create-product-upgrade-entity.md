---
title: Tworzenie jednostki uaktualnienia produktu dla klienta
description: Za pomocą zasobu ProductUpgradeRequest można utworzyć jednostkę uaktualnienia produktu w celu uaktualnienia klienta do danej rodziny produktów.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 45830033d93e0906eafc169cf04b997e2ff7c3d8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767750"
---
# <a name="create-a-product-upgrade-entity-for-a-customer"></a><span data-ttu-id="284ab-103">Tworzenie jednostki uaktualnienia produktu dla klienta</span><span class="sxs-lookup"><span data-stu-id="284ab-103">Create a product upgrade entity for a customer</span></span>

<span data-ttu-id="284ab-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="284ab-104">**Applies to:**</span></span>

- <span data-ttu-id="284ab-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="284ab-105">Partner Center</span></span>

<span data-ttu-id="284ab-106">Można utworzyć jednostkę uaktualnienia produktu w celu uaktualnienia klienta do danej rodziny produktów (na przykład planu platformy Azure) przy użyciu zasobu **ProductUpgradeRequest** .</span><span class="sxs-lookup"><span data-stu-id="284ab-106">You can create a product upgrade entity to upgrade a customer to a given product family (for example, Azure plan) using the **ProductUpgradeRequest** resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="284ab-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="284ab-107">Prerequisites</span></span>

- <span data-ttu-id="284ab-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="284ab-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="284ab-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="284ab-109">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="284ab-110">Postępuj zgodnie z [bezpiecznym modelem aplikacji](enable-secure-app-model.md) podczas korzystania z aplikacji i uwierzytelniania użytkowników za pomocą interfejsów API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="284ab-110">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="284ab-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="284ab-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="284ab-112">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="284ab-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="284ab-113">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="284ab-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="284ab-114">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="284ab-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="284ab-115">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="284ab-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="284ab-116">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="284ab-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="284ab-117">Rodzina produktów, do której ma zostać uaktualniony klient.</span><span class="sxs-lookup"><span data-stu-id="284ab-117">The product family to which you want to upgrade the customer.</span></span>

## <a name="c"></a><span data-ttu-id="284ab-118">C\#</span><span class="sxs-lookup"><span data-stu-id="284ab-118">C\#</span></span>

<span data-ttu-id="284ab-119">Aby uaktualnić klienta do planu platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="284ab-119">To upgrade a customer to Azure plan:</span></span>

1. <span data-ttu-id="284ab-120">Utwórz obiekt **ProductUpgradesRequest** i określ identyfikator klienta oraz "Azure" jako rodzinę produktów.</span><span class="sxs-lookup"><span data-stu-id="284ab-120">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="284ab-121">Użyj kolekcji **IAggregatePartner. ProductUpgrades** .</span><span class="sxs-lookup"><span data-stu-id="284ab-121">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>

3. <span data-ttu-id="284ab-122">Wywołaj metodę **Create** i przekaż obiekt **ProductUpgradesRequest** , który zwróci ciąg **nagłówka lokalizacji** .</span><span class="sxs-lookup"><span data-stu-id="284ab-122">Call the **Create** method and pass in the **ProductUpgradesRequest** object, which will return a **location header** string.</span></span>

4. <span data-ttu-id="284ab-123">Wyodrębnij **Identyfikator upgrade** z ciągu nagłówka lokalizacji, którego można użyć do [zbadania stanu uaktualnienia](get-product-upgrade-status.md).</span><span class="sxs-lookup"><span data-stu-id="284ab-123">Extract the **upgrade-id** from the location header string which can be used to [query the upgrade status](get-product-upgrade-status.md).</span></span>

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "Azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

var productUpgradeLocationHeader = partnerOperations.ProductUpgrades.Create(productUpgradeRequest);

var upgradeId = Regex.Split(productUpgradeLocationHeader, "/")[1];

```

## <a name="rest-request"></a><span data-ttu-id="284ab-124">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="284ab-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="284ab-125">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="284ab-125">Request syntax</span></span>

| <span data-ttu-id="284ab-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="284ab-126">Method</span></span>   | <span data-ttu-id="284ab-127">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="284ab-127">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="284ab-128">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="284ab-128">**POST**</span></span> | <span data-ttu-id="284ab-129">[*{baseURL}*](partner-center-rest-urls.md)/V1/productupgrades http/1.1</span><span class="sxs-lookup"><span data-stu-id="284ab-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades HTTP/1.1</span></span> |

#### <a name="request-headers"></a><span data-ttu-id="284ab-130">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="284ab-130">Request headers</span></span>

<span data-ttu-id="284ab-131">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="284ab-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

#### <a name="request-body"></a><span data-ttu-id="284ab-132">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="284ab-132">Request body</span></span>

<span data-ttu-id="284ab-133">Treść żądania musi zawierać zasób [ProductUpgradeRequest](product-upgrade-resources.md#productupgraderequest) .</span><span class="sxs-lookup"><span data-stu-id="284ab-133">The request body must contain a [ProductUpgradeRequest](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

#### <a name="request-example"></a><span data-ttu-id="284ab-134">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="284ab-134">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades HTTP/1.1
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
  "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
  "productFamily": "Azure"
}
```

## <a name="rest-response"></a><span data-ttu-id="284ab-135">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="284ab-135">REST response</span></span>

<span data-ttu-id="284ab-136">Jeśli to się powiedzie, odpowiedź zawiera nagłówek **lokalizacji** z identyfikatorem URI, którego można użyć do pobrania stanu uaktualnienia produktu.</span><span class="sxs-lookup"><span data-stu-id="284ab-136">If successful, the response contains a **Location** header that has a URI that can be used to retrieve product upgrade status.</span></span> <span data-ttu-id="284ab-137">Zapisz ten identyfikator URI do użycia z innymi powiązanymi interfejsami API REST.</span><span class="sxs-lookup"><span data-stu-id="284ab-137">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="284ab-138">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="284ab-138">Response success and error codes</span></span>

<span data-ttu-id="284ab-139">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="284ab-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="284ab-140">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="284ab-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="284ab-141">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="284ab-141">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="284ab-142">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="284ab-142">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: productUpgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 28 Sep 2019 20:35:35 GMT
```
