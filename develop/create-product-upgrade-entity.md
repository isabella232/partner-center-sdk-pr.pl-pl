---
title: Tworzenie jednostki uaktualnienia produktu dla klienta
description: Zasób ProductUpgradeRequest umożliwia utworzenie jednostki uaktualnienia produktu w celu uaktualnienia klienta do danej rodziny produktów.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4e346b7f5294a8847047c85115d8c80f34eaca84
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973420"
---
# <a name="create-a-product-upgrade-entity-for-a-customer"></a><span data-ttu-id="51bb8-103">Tworzenie jednostki uaktualnienia produktu dla klienta</span><span class="sxs-lookup"><span data-stu-id="51bb8-103">Create a product upgrade entity for a customer</span></span>

<span data-ttu-id="51bb8-104">Możesz utworzyć jednostkę uaktualnienia produktu, aby uaktualnić klienta do danej rodziny produktów (na przykład planu platformy Azure) przy użyciu **zasobu ProductUpgradeRequest.**</span><span class="sxs-lookup"><span data-stu-id="51bb8-104">You can create a product upgrade entity to upgrade a customer to a given product family (for example, Azure plan) using the **ProductUpgradeRequest** resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51bb8-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="51bb8-105">Prerequisites</span></span>

- <span data-ttu-id="51bb8-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="51bb8-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="51bb8-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="51bb8-107">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="51bb8-108">Postępuj zgodnie z [modelem bezpiecznej aplikacji podczas](enable-secure-app-model.md) korzystania z uwierzytelniania app+user z Partner Center API.</span><span class="sxs-lookup"><span data-stu-id="51bb8-108">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="51bb8-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="51bb8-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="51bb8-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="51bb8-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="51bb8-111">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="51bb8-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="51bb8-112">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="51bb8-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="51bb8-113">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="51bb8-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="51bb8-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="51bb8-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="51bb8-115">Rodzina produktów, do której chcesz uaktualnić klienta.</span><span class="sxs-lookup"><span data-stu-id="51bb8-115">The product family to which you want to upgrade the customer.</span></span>

## <a name="c"></a><span data-ttu-id="51bb8-116">C\#</span><span class="sxs-lookup"><span data-stu-id="51bb8-116">C\#</span></span>

<span data-ttu-id="51bb8-117">Aby uaktualnić klienta do planu platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="51bb8-117">To upgrade a customer to Azure plan:</span></span>

1. <span data-ttu-id="51bb8-118">Utwórz obiekt **ProductUpgradesRequest** i określ identyfikator klienta oraz wartość "Azure" jako rodzinę produktów.</span><span class="sxs-lookup"><span data-stu-id="51bb8-118">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="51bb8-119">Użyj **kolekcji IAggregatePartner.ProductUpgrades.**</span><span class="sxs-lookup"><span data-stu-id="51bb8-119">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>

3. <span data-ttu-id="51bb8-120">Wywołaj **metodę Create** i przekaż obiekt **ProductUpgradesRequest,** który zwróci ciąg **nagłówka** lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="51bb8-120">Call the **Create** method and pass in the **ProductUpgradesRequest** object, which will return a **location header** string.</span></span>

4. <span data-ttu-id="51bb8-121">Wyodrębnij **identyfikator upgrade-id** z ciągu nagłówka lokalizacji, który może służyć do wykonywania [zapytań o stan uaktualnienia](get-product-upgrade-status.md).</span><span class="sxs-lookup"><span data-stu-id="51bb8-121">Extract the **upgrade-id** from the location header string that can be used to [query the upgrade status](get-product-upgrade-status.md).</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="51bb8-122">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="51bb8-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="51bb8-123">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="51bb8-123">Request syntax</span></span>

| <span data-ttu-id="51bb8-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="51bb8-124">Method</span></span>   | <span data-ttu-id="51bb8-125">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="51bb8-125">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="51bb8-126">**Post**</span><span class="sxs-lookup"><span data-stu-id="51bb8-126">**POST**</span></span> | <span data-ttu-id="51bb8-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="51bb8-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades HTTP/1.1</span></span> |

#### <a name="request-headers"></a><span data-ttu-id="51bb8-128">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="51bb8-128">Request headers</span></span>

<span data-ttu-id="51bb8-129">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="51bb8-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

#### <a name="request-body"></a><span data-ttu-id="51bb8-130">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="51bb8-130">Request body</span></span>

<span data-ttu-id="51bb8-131">Treść żądania musi zawierać [zasób ProductUpgradeRequest.](product-upgrade-resources.md#productupgraderequest)</span><span class="sxs-lookup"><span data-stu-id="51bb8-131">The request body must contain a [ProductUpgradeRequest](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

#### <a name="request-example"></a><span data-ttu-id="51bb8-132">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="51bb8-132">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="51bb8-133">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="51bb8-133">REST response</span></span>

<span data-ttu-id="51bb8-134">Jeśli to się powiedzie, odpowiedź zawiera nagłówek **Location** z kodem URI, który może służyć do pobierania stanu uaktualnienia produktu.</span><span class="sxs-lookup"><span data-stu-id="51bb8-134">If successful, the response contains a **Location** header that has a URI that can be used to retrieve product upgrade status.</span></span> <span data-ttu-id="51bb8-135">Zapisz ten URI do użycia z innymi powiązanymi interfejsami API REST.</span><span class="sxs-lookup"><span data-stu-id="51bb8-135">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="51bb8-136">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="51bb8-136">Response success and error codes</span></span>

<span data-ttu-id="51bb8-137">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="51bb8-137">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="51bb8-138">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="51bb8-138">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="51bb8-139">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="51bb8-139">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="51bb8-140">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="51bb8-140">Response example</span></span>

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
