---
title: Usuwanie odsprzedawcy pośredniego w piaskownicy
description: Zawiera informacje na temat usuwania odsprzedawców pośrednich piaskownicy i włączania testowania end-to-end przy użyciu interfejsów API.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ba1fd002ac62aba4e414d263b33ecc8153054602
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973013"
---
# <a name="delete-indirect-reseller-in-sandbox"></a><span data-ttu-id="8ac1e-103">Usuwanie odsprzedawcy pośredniego w piaskownicy</span><span class="sxs-lookup"><span data-stu-id="8ac1e-103">Delete Indirect Reseller in Sandbox</span></span>

<span data-ttu-id="8ac1e-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="8ac1e-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="8ac1e-105">W tym dokumencie przedstawiono sposób usuwania dostawców pośrednich piaskownicy i włączania testowania end-to-end przy użyciu interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="8ac1e-105">This document shows how to delete Sandbox Indirect Providers and enable end-to-end testing using APIs.</span></span>

> [!Important]
> <span data-ttu-id="8ac1e-106">W tym dokumencie opisano funkcje, które są dozwolone tylko w środowisku piaskownicy dla środowisk modelu pośredniego.</span><span class="sxs-lookup"><span data-stu-id="8ac1e-106">This document describes features that are only allowed in the Sandbox environment for Indirect Model experiences.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ac1e-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8ac1e-107">Prerequisites</span></span>

- <span data-ttu-id="8ac1e-108">Poświadczenia zgodnie z opisem w te [Partner Center Authentication (Uwierzytelnianie).](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8ac1e-108">Credentials as described in [Partner Center Authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8ac1e-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8ac1e-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller"></a><span data-ttu-id="8ac1e-110">Dostawca pośredni piaskownicy — usuwanie odsprzedawcy pośredniego piaskownicy</span><span class="sxs-lookup"><span data-stu-id="8ac1e-110">Sandbox Indirect Provider – Delete Sandbox Indirect Reseller</span></span> 

<span data-ttu-id="8ac1e-111">Ta funkcja jest dostępna tylko w piaskownicy i umożliwia dostawcom pośrednim piaskownicy tworzenie odsprzedawców pośrednich piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="8ac1e-111">This feature is only available in the Sandbox and gives Sandbox Indirect Providers an ability to create Sandbox Indirect Resellers.</span></span>

1. <span data-ttu-id="8ac1e-112">Wymagania wstępne dotyczące usuwania odsprzedawcy pośredniego piaskownicy</span><span class="sxs-lookup"><span data-stu-id="8ac1e-112">Prerequisites for Deleting a Sandbox Indirect Reseller</span></span>
    1. <span data-ttu-id="8ac1e-113">Wstrzymywanie subskrypcji dla każdego klienta odsprzedawcy pośredniego piaskownicy</span><span class="sxs-lookup"><span data-stu-id="8ac1e-113">Suspend the subscriptions for each customer of Sandbox Indirect Reseller</span></span>
    2. <span data-ttu-id="8ac1e-114">Usuń wszystkich klientów odsprzedawcy pośredniego</span><span class="sxs-lookup"><span data-stu-id="8ac1e-114">Delete all customers of Indirect Reseller</span></span>
2. <span data-ttu-id="8ac1e-115">Dozwolony limit pięciu odsprzedawców pośrednich piaskownicy na dostawcę pośredniego piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="8ac1e-115">Limit of five Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> <span data-ttu-id="8ac1e-116">Po usunięciu odsprzedawcy pośredniego piaskownicy limit przydziału zostanie zresetowany.</span><span class="sxs-lookup"><span data-stu-id="8ac1e-116">Once the Sandbox Indirect reseller is deleted, the quota will be reset.</span></span>

## <a name="delete-sandbox-indirect-reseller-through-api"></a><span data-ttu-id="8ac1e-117">Usuwanie odsprzedawcy pośredniego piaskownicy za pośrednictwem interfejsu API</span><span class="sxs-lookup"><span data-stu-id="8ac1e-117">Delete Sandbox Indirect Reseller through API</span></span>

### <a name="rest-request"></a><span data-ttu-id="8ac1e-118">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="8ac1e-118">REST request</span></span>

#### <a name="request-syntax"></a><span data-ttu-id="8ac1e-119">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="8ac1e-119">Request syntax</span></span>

| <span data-ttu-id="8ac1e-120">Metoda</span><span class="sxs-lookup"><span data-stu-id="8ac1e-120">Method</span></span> | <span data-ttu-id="8ac1e-121">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="8ac1e-121">Request URI</span></span>                                                                             |
|------------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="8ac1e-122">**Usunąć**</span><span class="sxs-lookup"><span data-stu-id="8ac1e-122">**DELETE**</span></span> | <span data-ttu-id="8ac1e-123">[*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller/{resellerId}</span><span class="sxs-lookup"><span data-stu-id="8ac1e-123">[*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller/{resellerId}</span></span> |

#### <a name="request-headers"></a><span data-ttu-id="8ac1e-124">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="8ac1e-124">Request headers</span></span>

- <span data-ttu-id="8ac1e-125">Ten interfejs API jest idempotentny (nie da innego wyniku, jeśli wywołasz go wielokrotnie)</span><span class="sxs-lookup"><span data-stu-id="8ac1e-125">This API is idempotent (it will not yield a different result if you call it multiple times)</span></span>
- <span data-ttu-id="8ac1e-126">Wymagany jest identyfikator żądania i identyfikator korelacji</span><span class="sxs-lookup"><span data-stu-id="8ac1e-126">A request ID and correlation ID are required</span></span>
- <span data-ttu-id="8ac1e-127">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST)](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8ac1e-127">For more information, see [Partner Center REST headers](headers.md)</span></span>

### <a name="request-example"></a><span data-ttu-id="8ac1e-128">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="8ac1e-128">Request Example</span></span>

<span data-ttu-id="8ac1e-129">Usunąć https://api.partnercenter.microsoft.com/v1/sandboxIndirectReseller/{resellerID}</span><span class="sxs-lookup"><span data-stu-id="8ac1e-129">DELETE https://api.partnercenter.microsoft.com/v1/sandboxIndirectReseller/{resellerID}</span></span>

```http
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

####  <a name="response-example"></a><span data-ttu-id="8ac1e-130">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8ac1e-130">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Feb 2021 00:43:02 GMT
```

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="8ac1e-131">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8ac1e-131">Response success and error codes</span></span>

<span data-ttu-id="8ac1e-132">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz inne informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="8ac1e-132">Each response comes with an HTTP status code that indicates success or failure and other debugging information.</span></span> <span data-ttu-id="8ac1e-133">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="8ac1e-133">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8ac1e-134">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8ac1e-134">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="8ac1e-135">Ta metoda zwraca następujące kody powodzenia i błędów:</span><span class="sxs-lookup"><span data-stu-id="8ac1e-135">This method returns the following status success and error codes:</span></span>

| <span data-ttu-id="8ac1e-136">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="8ac1e-136">HTTP Status Code</span></span>                     | <span data-ttu-id="8ac1e-137">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="8ac1e-137">Error code</span></span>     | <span data-ttu-id="8ac1e-138">Opis</span><span class="sxs-lookup"><span data-stu-id="8ac1e-138">Description</span></span>                                      |
|--------------------------------------|----------------|--------------------------------------------------|
| <span data-ttu-id="8ac1e-139">401</span><span class="sxs-lookup"><span data-stu-id="8ac1e-139">401</span></span>                                  | <span data-ttu-id="8ac1e-140">6002</span><span class="sxs-lookup"><span data-stu-id="8ac1e-140">6002</span></span>           | <span data-ttu-id="8ac1e-141">Nieautoryzowany token lub konto dostawcy porad</span><span class="sxs-lookup"><span data-stu-id="8ac1e-141">Unauthorized token or Not a Tip Provider Account</span></span> |
| <span data-ttu-id="8ac1e-142">403</span><span class="sxs-lookup"><span data-stu-id="8ac1e-142">403</span></span>                                  | <span data-ttu-id="8ac1e-143">6003</span><span class="sxs-lookup"><span data-stu-id="8ac1e-143">6003</span></span>           | <span data-ttu-id="8ac1e-144">Usuwanie środowiska IR piaskownicy jest niedozwolone</span><span class="sxs-lookup"><span data-stu-id="8ac1e-144">Delete Sandbox IR is not allowed</span></span>                 |
| <span data-ttu-id="8ac1e-145">403</span><span class="sxs-lookup"><span data-stu-id="8ac1e-145">403</span></span>                                  | <span data-ttu-id="8ac1e-146">6004</span><span class="sxs-lookup"><span data-stu-id="8ac1e-146">6004</span></span>           | <span data-ttu-id="8ac1e-147">Tworzenie operacji środowiska IR piaskownicy jest niedozwolone</span><span class="sxs-lookup"><span data-stu-id="8ac1e-147">Create Sandbox IR operation not allowed</span></span>          |
| <span data-ttu-id="8ac1e-148">409</span><span class="sxs-lookup"><span data-stu-id="8ac1e-148">409</span></span>                                  | <span data-ttu-id="8ac1e-149">1003</span><span class="sxs-lookup"><span data-stu-id="8ac1e-149">1003</span></span>           | <span data-ttu-id="8ac1e-150">Konflikt podczas tworzenia dzierżawy</span><span class="sxs-lookup"><span data-stu-id="8ac1e-150">Conflict while creating tenant</span></span>                   |
