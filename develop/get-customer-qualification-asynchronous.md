---
title: Uzyskiwanie kwalifikacji klienta
description: Dowiedz się, jak za pomocą walidacji asynchronicznej uzyskać kwalifikację klienta za pośrednictwem Partner Center API. Partnerzy mogą używać tego do weryfikowania klientów edukacyjnych.
ms.date: 05/17/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: df605e4d400d29e14fd0b44bef34f88bbc7ca8b2
ms.sourcegitcommit: 7d59c58ee36b217bd5cac089f918059e9dbb8a62
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/19/2021
ms.locfileid: "110027932"
---
# <a name="get-a-customers-qualification-asynchronously"></a><span data-ttu-id="32f82-104">Asynchroniczne uzyskiwanie kwalifikacji klienta</span><span class="sxs-lookup"><span data-stu-id="32f82-104">Get a customer's qualification asynchronously</span></span>

<span data-ttu-id="32f82-105">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="32f82-105">**Applies To**</span></span>

- <span data-ttu-id="32f82-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="32f82-106">Partner Center</span></span>

<span data-ttu-id="32f82-107">Jak asynchronicznie uzyskać kwalifikacje klienta.</span><span class="sxs-lookup"><span data-stu-id="32f82-107">How to get a customer's qualifications asynchronously.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32f82-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="32f82-108">Prerequisites</span></span>

- <span data-ttu-id="32f82-109">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="32f82-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="32f82-110">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="32f82-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="32f82-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="32f82-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="32f82-112">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="32f82-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="32f82-113">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="32f82-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="32f82-114">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="32f82-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="32f82-115">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="32f82-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="32f82-116">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="32f82-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="32f82-117">C\#</span><span class="sxs-lookup"><span data-stu-id="32f82-117">C\#</span></span>

<span data-ttu-id="32f82-118">Aby uzyskać kwalifikacje klienta, wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta.</span><span class="sxs-lookup"><span data-stu-id="32f82-118">To get a customer's qualifications, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="32f82-119">Następnie użyj właściwości [**Kwalifikacja,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) aby pobrać [**interfejs ICustomerQualification.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification)</span><span class="sxs-lookup"><span data-stu-id="32f82-119">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="32f82-120">Na koniec zadzwoń `GetQualifications()` do działu lub , aby pobrać `GetQualificationsAsync()` kwalifikacje klienta.</span><span class="sxs-lookup"><span data-stu-id="32f82-120">Finally, call `GetQualifications()` or `GetQualificationsAsync()` to retrieve the customer's qualifications.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerQualifications = partnerOperations.Customers.ById(customerId).Qualification.GetQualifications();
```

<span data-ttu-id="32f82-121">**Przykład:** [Przykładowa aplikacja konsoli](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="32f82-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="32f82-122">**Projekt**: SdkSamples, **klasa**: GetCustomerQualifications.cs</span><span class="sxs-lookup"><span data-stu-id="32f82-122">**Project**: SdkSamples **Class**: GetCustomerQualifications.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="32f82-123">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="32f82-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="32f82-124">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="32f82-124">Request syntax</span></span>

| <span data-ttu-id="32f82-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="32f82-125">Method</span></span>  | <span data-ttu-id="32f82-126">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="32f82-126">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="32f82-127">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="32f82-127">**GET**</span></span> | <span data-ttu-id="32f82-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="32f82-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="32f82-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="32f82-129">URI parameter</span></span>

<span data-ttu-id="32f82-130">W tej tabeli wymieniono wymagany parametr zapytania w celu uzyskania wszystkich kwalifikacji.</span><span class="sxs-lookup"><span data-stu-id="32f82-130">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="32f82-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="32f82-131">Name</span></span>               | <span data-ttu-id="32f82-132">Typ</span><span class="sxs-lookup"><span data-stu-id="32f82-132">Type</span></span>   | <span data-ttu-id="32f82-133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="32f82-133">Required</span></span> | <span data-ttu-id="32f82-134">Opis</span><span class="sxs-lookup"><span data-stu-id="32f82-134">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="32f82-135">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="32f82-135">**customer-tenant-id**</span></span> | <span data-ttu-id="32f82-136">ciąg</span><span class="sxs-lookup"><span data-stu-id="32f82-136">string</span></span> | <span data-ttu-id="32f82-137">Tak</span><span class="sxs-lookup"><span data-stu-id="32f82-137">Yes</span></span>      | <span data-ttu-id="32f82-138">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="32f82-138">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="32f82-139">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="32f82-139">Request headers</span></span>

<span data-ttu-id="32f82-140">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="32f82-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="32f82-141">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="32f82-141">Request body</span></span>

<span data-ttu-id="32f82-142">Brak.</span><span class="sxs-lookup"><span data-stu-id="32f82-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="32f82-143">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="32f82-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="32f82-144">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="32f82-144">REST response</span></span>

<span data-ttu-id="32f82-145">W przypadku powodzenia ta metoda zwraca kolekcję kwalifikacji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="32f82-145">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="32f82-146">Poniżej przedstawiono przykłady rozmowy **GET** dotyczącej klienta z kwalifikacją **do edukacji.**</span><span class="sxs-lookup"><span data-stu-id="32f82-146">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="32f82-147">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="32f82-147">Response success and error codes</span></span>

<span data-ttu-id="32f82-148">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="32f82-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="32f82-149">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="32f82-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="32f82-150">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="32f82-150">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="32f82-151">Przykłady odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="32f82-151">Response examples</span></span>

#### <a name="approved"></a><span data-ttu-id="32f82-152">Approved (Zatwierdzono)</span><span class="sxs-lookup"><span data-stu-id="32f82-152">Approved</span></span>

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

#### <a name="in-review"></a><span data-ttu-id="32f82-153">Przegląd</span><span class="sxs-lookup"><span data-stu-id="32f82-153">In Review</span></span>

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

#### <a name="denied"></a><span data-ttu-id="32f82-154">Odmowa</span><span class="sxs-lookup"><span data-stu-id="32f82-154">Denied</span></span>

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

#### <a name="state-owned-entity-samples"></a><span data-ttu-id="32f82-155">Przykłady jednostek należących do stanu</span><span class="sxs-lookup"><span data-stu-id="32f82-155">State Owned Entity Samples</span></span>

<span data-ttu-id="32f82-156">**Przykład jednostki należącej do stanu za pośrednictwem posta**</span><span class="sxs-lookup"><span data-stu-id="32f82-156">**State Owned Entity via POST sample**</span></span>

```csharp

//SOE
POST {customer_id}/qualifications
{
“qualification”: “StateOwnedEntity”
}

//

```

<span data-ttu-id="32f82-157">**Jednostka należąca do stanu za pośrednictwem przykładu Pobierz kwalifikacje**</span><span class="sxs-lookup"><span data-stu-id="32f82-157">**State Owned Entity via Get Qualifications sample**</span></span>

```csharp

//SOE:
GET {customer_id}/qualifications
[
    {
        “qualification”: “StateOwnedEntity”
    }
]

```

<span data-ttu-id="32f82-158">**Jednostka należąca do stanu za pośrednictwem get qualifications with Education**</span><span class="sxs-lookup"><span data-stu-id="32f82-158">**State Owned Entity via Get Qualifications with Education**</span></span>

```csharp

GET {customer_id}/qualifications
[
    {
        “qualification”: “Education”,
        “vettingStatus”: “Approved”
    },
{
        “qualification”: “StateOwnedEntity”
    }
]

```

<span data-ttu-id="32f82-159">**Jednostka należąca do stanu za pośrednictwem get qualifications with GCC**</span><span class="sxs-lookup"><span data-stu-id="32f82-159">**State Owned Entity via Get Qualifications with GCC**</span></span>

```csharp

GET {customer_id}/qualifications
[
    {
        “qualification”: “GovernmentCommunityCloud”,
        “vettingStatus”: “Approved”,
        “vettingCreateDate”: “2021-05-06T19:59:56.6832021+00:00”
    },
{
        “qualification”: “StateOwnedEntity”
    }
]

```

## <a name="related-articles"></a><span data-ttu-id="32f82-160">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="32f82-160">Related articles</span></span>

- [<span data-ttu-id="32f82-161">Aktualizowanie kwalifikacji klienta</span><span class="sxs-lookup"><span data-stu-id="32f82-161">Update a customer's qualifications</span></span>](./update-customer-qualification-asynchronous.md)
