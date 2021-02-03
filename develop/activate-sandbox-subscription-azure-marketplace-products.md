---
title: Aktywuj subskrypcję piaskownicy dla komercyjnych produktów Marketplace
description: Dowiedz się, jak korzystać z interfejsów API REST usługi C/# i Centrum partnerskiego, aby aktywować subskrypcję piaskownicy dla komercyjnych produktów Marketplace.
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a78b2c84368b29f1378f46971c4814929094e299
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/11/2020
ms.locfileid: "97768509"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-saas-products-to-enable-billing"></a><span data-ttu-id="09824-103">Aktywuj subskrypcję piaskownicy dla komercyjnych produktów SaaS Marketplace, aby włączyć rozliczenia</span><span class="sxs-lookup"><span data-stu-id="09824-103">Activate a sandbox subscription for commercial marketplace SaaS products to enable billing</span></span>

<span data-ttu-id="09824-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="09824-104">**Applies to:**</span></span>

- <span data-ttu-id="09824-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="09824-105">Partner Center</span></span>

<span data-ttu-id="09824-106">Jak aktywować subskrypcję dla komercyjnych produktów jako usługi (SaaS) na kontach piaskownicy integracji, aby włączyć rozliczenia.</span><span class="sxs-lookup"><span data-stu-id="09824-106">How to activate a subscription for commercial marketplace Software as a Service (SaaS) products from integration sandbox accounts to enable billing.</span></span>

> [!NOTE]
> <span data-ttu-id="09824-107">Istnieje możliwość aktywowania subskrypcji komercyjnych produktów SaaS Marketplace z kont piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="09824-107">It's only possible to activate a subscription for commercial marketplace SaaS products from integration sandbox accounts.</span></span> <span data-ttu-id="09824-108">Jeśli masz subskrypcję produkcyjną, należy odwiedzić witrynę wydawcy, aby ukończyć proces instalacji.</span><span class="sxs-lookup"><span data-stu-id="09824-108">If you have a production subscription, you must visit the publisher's site to complete the setup process.</span></span> <span data-ttu-id="09824-109">Rozliczanie subskrypcji rozpocznie się dopiero po zakończeniu instalacji.</span><span class="sxs-lookup"><span data-stu-id="09824-109">Subscription billing will begin only after setup is complete.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09824-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="09824-110">Prerequisites</span></span>

- <span data-ttu-id="09824-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="09824-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="09824-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="09824-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="09824-113">Konto partnera piaskownicy integracji z klientem z aktywną subskrypcją dla komercyjnych produktów SaaS Marketplace.</span><span class="sxs-lookup"><span data-stu-id="09824-113">An integration sandbox partner account with a customer having an active subscription for commercial marketplace SaaS products.</span></span>

- <span data-ttu-id="09824-114">W przypadku partnerów korzystających z zestawu SDK platformy .NET w usłudze Partner Center musisz użyć zestawu SDK 1.14.0 lub nowszego, aby uzyskać dostęp do tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="09824-114">For partners using Partner Center .NET SDK, you must use SDK version 1.14.0 or higher to access this capability.</span></span>

## <a name="c"></a><span data-ttu-id="09824-115">C\#</span><span class="sxs-lookup"><span data-stu-id="09824-115">C\#</span></span>

<span data-ttu-id="09824-116">Wykonaj następujące kroki, aby aktywować subskrypcję dla komercyjnych produktów SaaS Marketplace:</span><span class="sxs-lookup"><span data-stu-id="09824-116">Use the following steps to activate a subscription for commercial marketplace SaaS products:</span></span>

1. <span data-ttu-id="09824-117">Utwórz interfejs dla dostępnych operacji subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="09824-117">Make an interface to the subscription operations available.</span></span> <span data-ttu-id="09824-118">Należy zidentyfikować klienta i określić identyfikator subskrypcji wersji próbnej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="09824-118">You must identify the customer and specify the subscription identifier of the trial subscription.</span></span>

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. <span data-ttu-id="09824-119">Aktywuj subskrypcję przy użyciu operacji **uaktywniania** .</span><span class="sxs-lookup"><span data-stu-id="09824-119">Activate the subscription using the **Activate** operation.</span></span>

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a><span data-ttu-id="09824-120">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="09824-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="09824-121">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="09824-121">Request syntax</span></span>

| <span data-ttu-id="09824-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="09824-122">Method</span></span>     | <span data-ttu-id="09824-123">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="09824-123">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="09824-124">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="09824-124">**POST**</span></span> | <span data-ttu-id="09824-125">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/{Subscription-ID}/Activate http/1.1</span><span class="sxs-lookup"><span data-stu-id="09824-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/activate HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="09824-126">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="09824-126">URI parameter</span></span>

| <span data-ttu-id="09824-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="09824-127">Name</span></span>                   | <span data-ttu-id="09824-128">Typ</span><span class="sxs-lookup"><span data-stu-id="09824-128">Type</span></span>     | <span data-ttu-id="09824-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="09824-129">Required</span></span> | <span data-ttu-id="09824-130">Opis</span><span class="sxs-lookup"><span data-stu-id="09824-130">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="09824-131">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="09824-131">**customer-tenant-id**</span></span> | <span data-ttu-id="09824-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="09824-132">**guid**</span></span> | <span data-ttu-id="09824-133">Y</span><span class="sxs-lookup"><span data-stu-id="09824-133">Y</span></span> | <span data-ttu-id="09824-134">Wartość to identyfikator identyfikatora dzierżawy klienta w formacie GUID (**Identyfikator dzierżawy klienta**), który umożliwia określenie klienta.</span><span class="sxs-lookup"><span data-stu-id="09824-134">The value is a GUID-formatted customer tenant identifier (**customer-tenant-id**), which allows you to specify a customer.</span></span> |
| <span data-ttu-id="09824-135">**Identyfikator subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="09824-135">**subscription-id**</span></span> | <span data-ttu-id="09824-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="09824-136">**guid**</span></span> | <span data-ttu-id="09824-137">Y</span><span class="sxs-lookup"><span data-stu-id="09824-137">Y</span></span> | <span data-ttu-id="09824-138">Wartość jest identyfikatorem subskrypcji w formacie GUID (**Identyfikator subskrypcji**), który umożliwia określenie subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="09824-138">The value is a GUID-formatted subscription identifier (**subscription-id**), which allows you to specify a subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="09824-139">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="09824-139">Request headers</span></span>

<span data-ttu-id="09824-140">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="09824-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="09824-141">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="09824-141">Request body</span></span>

<span data-ttu-id="09824-142">Brak.</span><span class="sxs-lookup"><span data-stu-id="09824-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="09824-143">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="09824-143">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/42b5f772-5c5c-4bce-b9d7-bdadeecca411/subscriptions/87363db7-39ab-dd25-d371-94340aaa2f97/activate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

```

## <a name="rest-response"></a><span data-ttu-id="09824-144">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="09824-144">REST response</span></span>

<span data-ttu-id="09824-145">Ta metoda zwraca właściwości **identyfikatora subskrypcji** i **stanu** .</span><span class="sxs-lookup"><span data-stu-id="09824-145">This method returns the **subscription-id** and **status** properties.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="09824-146">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="09824-146">Response success and error codes</span></span>

<span data-ttu-id="09824-147">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="09824-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="09824-148">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="09824-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="09824-149">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="09824-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="09824-150">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="09824-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 79
Content-Type: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "subscriptionId":"87363db7-39ab-dd25-d371-94340aaa2f97",
    "status":"Success"
}
```
