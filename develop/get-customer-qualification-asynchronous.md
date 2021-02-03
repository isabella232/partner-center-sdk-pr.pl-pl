---
title: Pobierz kwalifikacje klienta
description: Dowiedz się, jak używać walidacji asynchronicznej w celu uzyskania kwalifikacji klienta za pośrednictwem interfejsu API Centrum partnerskiego. Partnerzy mogą używać tego do weryfikowania klientów edukacyjnych.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 9f9b9aaddde0d66caf9c7ef32e8fba6d5e3aba36
ms.sourcegitcommit: 0c98496e972aebe10eba23822aa229125bfc035d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770188"
---
# <a name="get-a-customers-qualifications-via-asynchronous-validation"></a><span data-ttu-id="1e0a0-104">Pobierz kwalifikacje klienta za pośrednictwem walidacji asynchronicznej</span><span class="sxs-lookup"><span data-stu-id="1e0a0-104">Get a customer's qualifications via asynchronous validation</span></span>

<span data-ttu-id="1e0a0-105">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="1e0a0-105">**Applies To**</span></span>

- <span data-ttu-id="1e0a0-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="1e0a0-106">Partner Center</span></span>

<span data-ttu-id="1e0a0-107">Dowiedz się, jak uzyskać kwalifikacje klienta asynchronicznie za pośrednictwem interfejsów API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="1e0a0-107">Learn how to get a customer's qualifications asynchronously via Partner Center APIs.</span></span> <span data-ttu-id="1e0a0-108">Aby dowiedzieć się, jak to zrobić synchronicznie, zobacz [pobieranie kwalifikacji klienta za pośrednictwem walidacji synchronicznej](get-customer-qualification-synchronous.md).</span><span class="sxs-lookup"><span data-stu-id="1e0a0-108">To learn how to do this synchronously, see [Get a customer's qualification via synchronous validation](get-customer-qualification-synchronous.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e0a0-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1e0a0-109">Prerequisites</span></span>

- <span data-ttu-id="1e0a0-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1e0a0-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1e0a0-111">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1e0a0-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1e0a0-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1e0a0-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1e0a0-113">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="1e0a0-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1e0a0-114">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="1e0a0-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1e0a0-115">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="1e0a0-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1e0a0-116">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="1e0a0-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1e0a0-117">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1e0a0-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="1e0a0-118">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="1e0a0-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1e0a0-119">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="1e0a0-119">Request syntax</span></span>

| <span data-ttu-id="1e0a0-120">Metoda</span><span class="sxs-lookup"><span data-stu-id="1e0a0-120">Method</span></span>  | <span data-ttu-id="1e0a0-121">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="1e0a0-121">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1e0a0-122">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="1e0a0-122">**GET**</span></span> | <span data-ttu-id="1e0a0-123">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Qualifications http/1.1</span><span class="sxs-lookup"><span data-stu-id="1e0a0-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="1e0a0-124">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="1e0a0-124">URI parameter</span></span>

<span data-ttu-id="1e0a0-125">Ta tabela zawiera listę wymaganych parametrów zapytania, aby uzyskać wszystkie kwalifikacje.</span><span class="sxs-lookup"><span data-stu-id="1e0a0-125">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="1e0a0-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1e0a0-126">Name</span></span>               | <span data-ttu-id="1e0a0-127">Typ</span><span class="sxs-lookup"><span data-stu-id="1e0a0-127">Type</span></span>   | <span data-ttu-id="1e0a0-128">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1e0a0-128">Required</span></span> | <span data-ttu-id="1e0a0-129">Opis</span><span class="sxs-lookup"><span data-stu-id="1e0a0-129">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="1e0a0-130">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="1e0a0-130">**customer-tenant-id**</span></span> | <span data-ttu-id="1e0a0-131">ciąg</span><span class="sxs-lookup"><span data-stu-id="1e0a0-131">string</span></span> | <span data-ttu-id="1e0a0-132">Tak</span><span class="sxs-lookup"><span data-stu-id="1e0a0-132">Yes</span></span>      | <span data-ttu-id="1e0a0-133">Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="1e0a0-133">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1e0a0-134">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="1e0a0-134">Request headers</span></span>

<span data-ttu-id="1e0a0-135">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1e0a0-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1e0a0-136">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="1e0a0-136">Request body</span></span>

<span data-ttu-id="1e0a0-137">Brak.</span><span class="sxs-lookup"><span data-stu-id="1e0a0-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1e0a0-138">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="1e0a0-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="1e0a0-139">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="1e0a0-139">REST response</span></span>

<span data-ttu-id="1e0a0-140">Jeśli to się powiedzie, ta metoda zwraca kolekcję kwalifikacji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="1e0a0-140">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="1e0a0-141">Poniżej przedstawiono przykłady wywołania **Get** na kliencie z kwalifikacją **edukacyjną** .</span><span class="sxs-lookup"><span data-stu-id="1e0a0-141">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1e0a0-142">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1e0a0-142">Response success and error codes</span></span>

<span data-ttu-id="1e0a0-143">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="1e0a0-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1e0a0-144">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="1e0a0-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1e0a0-145">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1e0a0-145">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="1e0a0-146">Przykłady odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1e0a0-146">Response examples</span></span>

<span data-ttu-id="1e0a0-147">W tej sekcji przedstawiono odpowiedzi, które mogą zostać wyświetlone, gdy klient `vettingStatus` jest:</span><span class="sxs-lookup"><span data-stu-id="1e0a0-147">This section shows responses you might receive when a customer's `vettingStatus` is:</span></span>

- <span data-ttu-id="1e0a0-148">Approved (Zatwierdzono)</span><span class="sxs-lookup"><span data-stu-id="1e0a0-148">Approved</span></span>
- <span data-ttu-id="1e0a0-149">Przegląd</span><span class="sxs-lookup"><span data-stu-id="1e0a0-149">In Review</span></span>
- <span data-ttu-id="1e0a0-150">Odmowa</span><span class="sxs-lookup"><span data-stu-id="1e0a0-150">Denied</span></span>

<span data-ttu-id="1e0a0-151">**Zatwierdzono** przykład:</span><span class="sxs-lookup"><span data-stu-id="1e0a0-151">**Approved** example:</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "Approved",
    }
]

```

<span data-ttu-id="1e0a0-152">Przykład **w przeglądzie** :</span><span class="sxs-lookup"><span data-stu-id="1e0a0-152">**In Review** example:</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "InReview",
        "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
    }
]

```

<span data-ttu-id="1e0a0-153">Przykład **odmowy** :</span><span class="sxs-lookup"><span data-stu-id="1e0a0-153">**Denied** example:</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "Denied",
        "vettingReason": "Not an Education Customer", // example Vetting Reason
        "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
    }
]

```

## <a name="related-articles"></a><span data-ttu-id="1e0a0-154">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="1e0a0-154">Related articles</span></span>

- [<span data-ttu-id="1e0a0-155">Aktualizowanie kwalifikacji klienta</span><span class="sxs-lookup"><span data-stu-id="1e0a0-155">Update a customer's qualifications</span></span>](update-a-customer-s-qualifications.md)