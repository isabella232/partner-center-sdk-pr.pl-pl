---
title: Pobierz kwalifikacje klienta
description: Dowiedz się, jak używać walidacji asynchronicznej w celu uzyskania kwalifikacji klienta za pośrednictwem interfejsu API Centrum partnerskiego. Partnerzy mogą używać tego do weryfikowania klientów edukacyjnych.
ms.date: 01/21/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 2c860d4a35104131197e06d4712f4ef41ba0008e
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711918"
---
# <a name="get-a-customers-qualification-asynchronously"></a><span data-ttu-id="26bb6-104">Zapoznaj się z kwalifikacją klienta asynchronicznie</span><span class="sxs-lookup"><span data-stu-id="26bb6-104">Get a customer's qualification asynchronously</span></span>

<span data-ttu-id="26bb6-105">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="26bb6-105">**Applies To**</span></span>

- <span data-ttu-id="26bb6-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="26bb6-106">Partner Center</span></span>

<span data-ttu-id="26bb6-107">Jak przeprowadzić asynchroniczne pobieranie kwalifikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="26bb6-107">How to get a customer's qualifications asynchronously.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26bb6-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="26bb6-108">Prerequisites</span></span>

- <span data-ttu-id="26bb6-109">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="26bb6-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="26bb6-110">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="26bb6-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="26bb6-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="26bb6-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="26bb6-112">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="26bb6-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="26bb6-113">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="26bb6-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="26bb6-114">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="26bb6-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="26bb6-115">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="26bb6-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="26bb6-116">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="26bb6-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="26bb6-117">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="26bb6-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="26bb6-118">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="26bb6-118">Request syntax</span></span>

| <span data-ttu-id="26bb6-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="26bb6-119">Method</span></span>  | <span data-ttu-id="26bb6-120">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="26bb6-120">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="26bb6-121">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="26bb6-121">**GET**</span></span> | <span data-ttu-id="26bb6-122">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Qualifications http/1.1</span><span class="sxs-lookup"><span data-stu-id="26bb6-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="26bb6-123">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="26bb6-123">URI parameter</span></span>

<span data-ttu-id="26bb6-124">Ta tabela zawiera listę wymaganych parametrów zapytania, aby uzyskać wszystkie kwalifikacje.</span><span class="sxs-lookup"><span data-stu-id="26bb6-124">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="26bb6-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="26bb6-125">Name</span></span>               | <span data-ttu-id="26bb6-126">Typ</span><span class="sxs-lookup"><span data-stu-id="26bb6-126">Type</span></span>   | <span data-ttu-id="26bb6-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="26bb6-127">Required</span></span> | <span data-ttu-id="26bb6-128">Opis</span><span class="sxs-lookup"><span data-stu-id="26bb6-128">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="26bb6-129">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="26bb6-129">**customer-tenant-id**</span></span> | <span data-ttu-id="26bb6-130">ciąg</span><span class="sxs-lookup"><span data-stu-id="26bb6-130">string</span></span> | <span data-ttu-id="26bb6-131">Tak</span><span class="sxs-lookup"><span data-stu-id="26bb6-131">Yes</span></span>      | <span data-ttu-id="26bb6-132">Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="26bb6-132">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="26bb6-133">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="26bb6-133">Request headers</span></span>

<span data-ttu-id="26bb6-134">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="26bb6-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="26bb6-135">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="26bb6-135">Request body</span></span>

<span data-ttu-id="26bb6-136">Brak.</span><span class="sxs-lookup"><span data-stu-id="26bb6-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="26bb6-137">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="26bb6-137">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="26bb6-138">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="26bb6-138">REST response</span></span>

<span data-ttu-id="26bb6-139">Jeśli to się powiedzie, ta metoda zwraca kolekcję kwalifikacji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="26bb6-139">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="26bb6-140">Poniżej przedstawiono przykłady wywołania **Get** na kliencie z kwalifikacją **edukacyjną** .</span><span class="sxs-lookup"><span data-stu-id="26bb6-140">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="26bb6-141">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="26bb6-141">Response success and error codes</span></span>

<span data-ttu-id="26bb6-142">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="26bb6-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="26bb6-143">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="26bb6-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="26bb6-144">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="26bb6-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="26bb6-145">Przykłady odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="26bb6-145">Response examples</span></span>

#### <a name="approved"></a><span data-ttu-id="26bb6-146">Approved (Zatwierdzono)</span><span class="sxs-lookup"><span data-stu-id="26bb6-146">Approved</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "Approved",
        }
    ]
}

```

#### <a name="in-review"></a><span data-ttu-id="26bb6-147">Przegląd</span><span class="sxs-lookup"><span data-stu-id="26bb6-147">In Review</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "InReview",
            "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
        }
    ]
}

```

#### <a name="denied"></a><span data-ttu-id="26bb6-148">Odmowa</span><span class="sxs-lookup"><span data-stu-id="26bb6-148">Denied</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "Denied",
            "vettingReason": "Not an Education Customer", // example Vetting Reason
            "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
        }
    ]
}

```

## <a name="related-articles"></a><span data-ttu-id="26bb6-149">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="26bb6-149">Related articles</span></span>

- [<span data-ttu-id="26bb6-150">Aktualizowanie kwalifikacji klienta</span><span class="sxs-lookup"><span data-stu-id="26bb6-150">Update a customer's qualifications</span></span>](./update-customer-qualification-asynchronous.md)