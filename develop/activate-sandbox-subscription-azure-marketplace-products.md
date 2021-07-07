---
title: Aktywowanie subskrypcji piaskownicy dla produktów platformy handlowej
description: Dowiedz się, jak używać języka C/# i Partner Center API REST do aktywowania subskrypcji piaskownicy dla produktów platformy handlowej.
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b32c3e87462f58218771fc5da7da56ed177489cb
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025704"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-saas-products-to-enable-billing"></a><span data-ttu-id="d68ff-103">Aktywowanie subskrypcji piaskownicy dla produktów SaaS komercyjnej platformy handlowej w celu włączenia rozliczeń</span><span class="sxs-lookup"><span data-stu-id="d68ff-103">Activate a sandbox subscription for commercial marketplace SaaS products to enable billing</span></span>

<span data-ttu-id="d68ff-104">Jak aktywować subskrypcję komercyjnych produktów platformy handlowej oprogramowania jako usługi (SaaS) z kont piaskownicy integracji w celu włączenia rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="d68ff-104">How to activate a subscription for commercial marketplace Software as a Service (SaaS) products from integration sandbox accounts to enable billing.</span></span>

> [!NOTE]
> <span data-ttu-id="d68ff-105">Subskrypcję produktów SaaS komercyjnej platformy handlowej można aktywować tylko z kont piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="d68ff-105">It's only possible to activate a subscription for commercial marketplace SaaS products from integration sandbox accounts.</span></span> <span data-ttu-id="d68ff-106">Jeśli masz subskrypcję produkcyjną, musisz odwiedzić witrynę wydawcy, aby ukończyć proces instalacji.</span><span class="sxs-lookup"><span data-stu-id="d68ff-106">If you have a production subscription, you must visit the publisher's site to complete the setup process.</span></span> <span data-ttu-id="d68ff-107">Rozliczanie subskrypcji rozpocznie się dopiero po zakończeniu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d68ff-107">Subscription billing will begin only after setup is complete.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d68ff-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d68ff-108">Prerequisites</span></span>

- <span data-ttu-id="d68ff-109">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d68ff-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d68ff-110">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d68ff-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d68ff-111">Konto partnera piaskownicy integracji z klientem, który ma aktywną subskrypcję produktów SaaS komercyjnej platformy handlowej.</span><span class="sxs-lookup"><span data-stu-id="d68ff-111">An integration sandbox partner account with a customer having an active subscription for commercial marketplace SaaS products.</span></span>

- <span data-ttu-id="d68ff-112">W przypadku partnerów korzystających Partner Center .NET SDK należy użyć zestawu SDK w wersji 1.14.0 lub wyższej, aby uzyskać dostęp do tej możliwości.</span><span class="sxs-lookup"><span data-stu-id="d68ff-112">For partners using Partner Center .NET SDK, you must use SDK version 1.14.0 or higher to access this capability.</span></span>

## <a name="c"></a><span data-ttu-id="d68ff-113">C\#</span><span class="sxs-lookup"><span data-stu-id="d68ff-113">C\#</span></span>

<span data-ttu-id="d68ff-114">Aby aktywować subskrypcję produktów SaaS na platformie handlowej, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d68ff-114">Use the following steps to activate a subscription for commercial marketplace SaaS products:</span></span>

1. <span data-ttu-id="d68ff-115">Udostępnij interfejs dla operacji subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d68ff-115">Make an interface to the subscription operations available.</span></span> <span data-ttu-id="d68ff-116">Należy zidentyfikować klienta i określić identyfikator subskrypcji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="d68ff-116">You must identify the customer and specify the subscription identifier of the trial subscription.</span></span>

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. <span data-ttu-id="d68ff-117">Aktywuj subskrypcję przy użyciu **operacji** Aktywuj.</span><span class="sxs-lookup"><span data-stu-id="d68ff-117">Activate the subscription using the **Activate** operation.</span></span>

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a><span data-ttu-id="d68ff-118">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="d68ff-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d68ff-119">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="d68ff-119">Request syntax</span></span>

| <span data-ttu-id="d68ff-120">Metoda</span><span class="sxs-lookup"><span data-stu-id="d68ff-120">Method</span></span>     | <span data-ttu-id="d68ff-121">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="d68ff-121">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="d68ff-122">**Post**</span><span class="sxs-lookup"><span data-stu-id="d68ff-122">**POST**</span></span> | <span data-ttu-id="d68ff-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/activate HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d68ff-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/activate HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d68ff-124">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="d68ff-124">URI parameter</span></span>

| <span data-ttu-id="d68ff-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d68ff-125">Name</span></span>                   | <span data-ttu-id="d68ff-126">Typ</span><span class="sxs-lookup"><span data-stu-id="d68ff-126">Type</span></span>     | <span data-ttu-id="d68ff-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d68ff-127">Required</span></span> | <span data-ttu-id="d68ff-128">Opis</span><span class="sxs-lookup"><span data-stu-id="d68ff-128">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d68ff-129">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="d68ff-129">**customer-tenant-id**</span></span> | <span data-ttu-id="d68ff-130">**guid**</span><span class="sxs-lookup"><span data-stu-id="d68ff-130">**guid**</span></span> | <span data-ttu-id="d68ff-131">Y</span><span class="sxs-lookup"><span data-stu-id="d68ff-131">Y</span></span> | <span data-ttu-id="d68ff-132">Wartość jest identyfikatorem dzierżawy klienta w formacie GUID **(customer-tenant-id),** który umożliwia określenie klienta.</span><span class="sxs-lookup"><span data-stu-id="d68ff-132">The value is a GUID-formatted customer tenant identifier (**customer-tenant-id**), which allows you to specify a customer.</span></span> |
| <span data-ttu-id="d68ff-133">**subscription-id**</span><span class="sxs-lookup"><span data-stu-id="d68ff-133">**subscription-id**</span></span> | <span data-ttu-id="d68ff-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="d68ff-134">**guid**</span></span> | <span data-ttu-id="d68ff-135">Y</span><span class="sxs-lookup"><span data-stu-id="d68ff-135">Y</span></span> | <span data-ttu-id="d68ff-136">Wartość jest identyfikatorem subskrypcji w formacie GUID **(subscription-id),** który umożliwia określenie subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d68ff-136">The value is a GUID-formatted subscription identifier (**subscription-id**), which allows you to specify a subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d68ff-137">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="d68ff-137">Request headers</span></span>

<span data-ttu-id="d68ff-138">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d68ff-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d68ff-139">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="d68ff-139">Request body</span></span>

<span data-ttu-id="d68ff-140">Brak.</span><span class="sxs-lookup"><span data-stu-id="d68ff-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d68ff-141">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="d68ff-141">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/42b5f772-5c5c-4bce-b9d7-bdadeecca411/subscriptions/87363db7-39ab-dd25-d371-94340aaa2f97/activate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

```

## <a name="rest-response"></a><span data-ttu-id="d68ff-142">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="d68ff-142">REST response</span></span>

<span data-ttu-id="d68ff-143">Ta metoda zwraca **właściwości subscription-id** **i status.**</span><span class="sxs-lookup"><span data-stu-id="d68ff-143">This method returns the **subscription-id** and **status** properties.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d68ff-144">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d68ff-144">Response success and error codes</span></span>

<span data-ttu-id="d68ff-145">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="d68ff-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d68ff-146">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="d68ff-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d68ff-147">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d68ff-147">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d68ff-148">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d68ff-148">Response example</span></span>

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
