---
title: Wycofywanie transferu
description: Jak wycofać utworzony transfer subskrypcji dla klienta.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a9e1e2a33d21fc1338a36b8ac96b528e70b61c86
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767677"
---
# <a name="withdraw-a-transfer"></a><span data-ttu-id="b790f-103">Wycofywanie transferu</span><span class="sxs-lookup"><span data-stu-id="b790f-103">Withdraw a transfer</span></span>

<span data-ttu-id="b790f-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="b790f-104">**Applies to:**</span></span>

- <span data-ttu-id="b790f-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="b790f-105">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b790f-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b790f-106">Prerequisites</span></span>

- <span data-ttu-id="b790f-107">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b790f-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b790f-108">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b790f-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b790f-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b790f-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b790f-110">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="b790f-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b790f-111">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="b790f-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b790f-112">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="b790f-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b790f-113">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="b790f-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b790f-114">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b790f-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="b790f-115">Identyfikator transferu dla istniejącego transferu.</span><span class="sxs-lookup"><span data-stu-id="b790f-115">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="b790f-116">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="b790f-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b790f-117">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="b790f-117">Request syntax</span></span>

| <span data-ttu-id="b790f-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="b790f-118">Method</span></span>    | <span data-ttu-id="b790f-119">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="b790f-119">Request URI</span></span>                                                                                                 |
|-----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b790f-120">**USUNIĘTY**</span><span class="sxs-lookup"><span data-stu-id="b790f-120">**DELETE**</span></span>| <span data-ttu-id="b790f-121">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/Transfers/{transfer-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="b790f-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>      |

### <a name="uri-parameter"></a><span data-ttu-id="b790f-122">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="b790f-122">URI parameter</span></span>

<span data-ttu-id="b790f-123">Użyj następującego parametru ścieżki, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="b790f-123">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="b790f-124">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b790f-124">Name</span></span>            | <span data-ttu-id="b790f-125">Typ</span><span class="sxs-lookup"><span data-stu-id="b790f-125">Type</span></span>     | <span data-ttu-id="b790f-126">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b790f-126">Required</span></span> | <span data-ttu-id="b790f-127">Opis</span><span class="sxs-lookup"><span data-stu-id="b790f-127">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="b790f-128">**Identyfikator klienta**</span><span class="sxs-lookup"><span data-stu-id="b790f-128">**customer-id**</span></span> | <span data-ttu-id="b790f-129">ciąg</span><span class="sxs-lookup"><span data-stu-id="b790f-129">string</span></span>   | <span data-ttu-id="b790f-130">Tak</span><span class="sxs-lookup"><span data-stu-id="b790f-130">Yes</span></span>      | <span data-ttu-id="b790f-131">Identyfikator GUID sformatowany przez klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="b790f-131">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="b790f-132">**Identyfikator transferu**</span><span class="sxs-lookup"><span data-stu-id="b790f-132">**transfer-id**</span></span> | <span data-ttu-id="b790f-133">ciąg</span><span class="sxs-lookup"><span data-stu-id="b790f-133">string</span></span>   | <span data-ttu-id="b790f-134">Tak</span><span class="sxs-lookup"><span data-stu-id="b790f-134">Yes</span></span>      | <span data-ttu-id="b790f-135">Identyfikator transferu w formacie GUID, który identyfikuje transfer.</span><span class="sxs-lookup"><span data-stu-id="b790f-135">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="b790f-136">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="b790f-136">Request headers</span></span>

<span data-ttu-id="b790f-137">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b790f-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="b790f-138">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="b790f-138">Request example</span></span>

```http
DELETE /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
Connection: keep-alive
```

## <a name="rest-response"></a><span data-ttu-id="b790f-139">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="b790f-139">REST response</span></span>

<span data-ttu-id="b790f-140">Jeśli to się powiedzie, ta metoda nie zwróci zawartości (204).</span><span class="sxs-lookup"><span data-stu-id="b790f-140">If successful, this method returns No Content (204).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b790f-141">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b790f-141">Response success and error codes</span></span>

<span data-ttu-id="b790f-142">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="b790f-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b790f-143">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="b790f-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b790f-144">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b790f-144">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b790f-145">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b790f-145">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
Date: Tue, 24 Mar 2020 23:44:06 GMT
```
