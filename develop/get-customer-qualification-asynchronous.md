---
title: Pobierz kwalifikacje klienta
description: Dowiedz się, jak używać walidacji asynchronicznej w celu uzyskania kwalifikacji klienta za pośrednictwem interfejsu API Centrum partnerskiego. Partnerzy mogą używać tego do weryfikowania klientów edukacyjnych.
ms.date: 01/21/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 09801792c059873b9f6b842e99286eda09d38b1a
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030573"
---
# <a name="get-a-customers-qualification-asynchronously"></a><span data-ttu-id="30b4e-104">Zapoznaj się z kwalifikacją klienta asynchronicznie</span><span class="sxs-lookup"><span data-stu-id="30b4e-104">Get a customer's qualification asynchronously</span></span>

<span data-ttu-id="30b4e-105">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="30b4e-105">**Applies To**</span></span>

- <span data-ttu-id="30b4e-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="30b4e-106">Partner Center</span></span>

<span data-ttu-id="30b4e-107">Jak przeprowadzić asynchroniczne pobieranie kwalifikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="30b4e-107">How to get a customer's qualifications asynchronously.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30b4e-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="30b4e-108">Prerequisites</span></span>

- <span data-ttu-id="30b4e-109">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="30b4e-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="30b4e-110">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="30b4e-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="30b4e-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="30b4e-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="30b4e-112">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="30b4e-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="30b4e-113">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="30b4e-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="30b4e-114">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="30b4e-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="30b4e-115">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="30b4e-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="30b4e-116">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="30b4e-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="30b4e-117">C\#</span><span class="sxs-lookup"><span data-stu-id="30b4e-117">C\#</span></span>

<span data-ttu-id="30b4e-118">Aby uzyskać kwalifikacje klienta, wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta.</span><span class="sxs-lookup"><span data-stu-id="30b4e-118">To get a customer's qualifications, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="30b4e-119">Następnie użyj właściwości [**kwalifikacji**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) do pobrania interfejsu [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) .</span><span class="sxs-lookup"><span data-stu-id="30b4e-119">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="30b4e-120">Na koniec Wywołaj `GetQualifications()` lub, `GetQualificationsAsync()` Aby pobrać kwalifikacje klienta.</span><span class="sxs-lookup"><span data-stu-id="30b4e-120">Finally, call `GetQualifications()` or `GetQualificationsAsync()` to retrieve the customer's qualifications.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerQualifications = partnerOperations.Customers.ById(customerId).Qualification.GetQualifications();
```

<span data-ttu-id="30b4e-121">**Przykład**: [Przykładowa aplikacja konsolowa](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="30b4e-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="30b4e-122">**Projekt**: SdkSamples **Class**: GetCustomerQualifications. cs</span><span class="sxs-lookup"><span data-stu-id="30b4e-122">**Project**: SdkSamples **Class**: GetCustomerQualifications.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="30b4e-123">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="30b4e-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="30b4e-124">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="30b4e-124">Request syntax</span></span>

| <span data-ttu-id="30b4e-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="30b4e-125">Method</span></span>  | <span data-ttu-id="30b4e-126">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="30b4e-126">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="30b4e-127">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="30b4e-127">**GET**</span></span> | <span data-ttu-id="30b4e-128">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Qualifications http/1.1</span><span class="sxs-lookup"><span data-stu-id="30b4e-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="30b4e-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="30b4e-129">URI parameter</span></span>

<span data-ttu-id="30b4e-130">Ta tabela zawiera listę wymaganych parametrów zapytania, aby uzyskać wszystkie kwalifikacje.</span><span class="sxs-lookup"><span data-stu-id="30b4e-130">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="30b4e-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30b4e-131">Name</span></span>               | <span data-ttu-id="30b4e-132">Typ</span><span class="sxs-lookup"><span data-stu-id="30b4e-132">Type</span></span>   | <span data-ttu-id="30b4e-133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30b4e-133">Required</span></span> | <span data-ttu-id="30b4e-134">Opis</span><span class="sxs-lookup"><span data-stu-id="30b4e-134">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="30b4e-135">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="30b4e-135">**customer-tenant-id**</span></span> | <span data-ttu-id="30b4e-136">ciąg</span><span class="sxs-lookup"><span data-stu-id="30b4e-136">string</span></span> | <span data-ttu-id="30b4e-137">Tak</span><span class="sxs-lookup"><span data-stu-id="30b4e-137">Yes</span></span>      | <span data-ttu-id="30b4e-138">Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="30b4e-138">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="30b4e-139">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="30b4e-139">Request headers</span></span>

<span data-ttu-id="30b4e-140">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="30b4e-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="30b4e-141">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="30b4e-141">Request body</span></span>

<span data-ttu-id="30b4e-142">Brak.</span><span class="sxs-lookup"><span data-stu-id="30b4e-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="30b4e-143">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="30b4e-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="30b4e-144">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="30b4e-144">REST response</span></span>

<span data-ttu-id="30b4e-145">Jeśli to się powiedzie, ta metoda zwraca kolekcję kwalifikacji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="30b4e-145">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="30b4e-146">Poniżej przedstawiono przykłady wywołania **Get** na kliencie z kwalifikacją **edukacyjną** .</span><span class="sxs-lookup"><span data-stu-id="30b4e-146">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="30b4e-147">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="30b4e-147">Response success and error codes</span></span>

<span data-ttu-id="30b4e-148">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="30b4e-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="30b4e-149">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="30b4e-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="30b4e-150">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="30b4e-150">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="30b4e-151">Przykłady odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="30b4e-151">Response examples</span></span>

#### <a name="approved"></a><span data-ttu-id="30b4e-152">Approved (Zatwierdzono)</span><span class="sxs-lookup"><span data-stu-id="30b4e-152">Approved</span></span>

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

#### <a name="in-review"></a><span data-ttu-id="30b4e-153">Przegląd</span><span class="sxs-lookup"><span data-stu-id="30b4e-153">In Review</span></span>

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

#### <a name="denied"></a><span data-ttu-id="30b4e-154">Odmowa</span><span class="sxs-lookup"><span data-stu-id="30b4e-154">Denied</span></span>

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

## <a name="related-articles"></a><span data-ttu-id="30b4e-155">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="30b4e-155">Related articles</span></span>

- [<span data-ttu-id="30b4e-156">Aktualizowanie kwalifikacji klienta</span><span class="sxs-lookup"><span data-stu-id="30b4e-156">Update a customer's qualifications</span></span>](./update-customer-qualification-asynchronous.md)
