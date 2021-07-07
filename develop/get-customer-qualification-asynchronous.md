---
title: Uzyskiwanie kwalifikacji klienta
description: Dowiedz się, jak za pomocą walidacji asynchronicznej uzyskać kwalifikację klienta za pośrednictwem Partner Center API. Partnerzy mogą używać tej funkcji do weryfikowania klientów edukacyjnych.
ms.date: 05/17/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 4795b6e1ad008f9d854dc7efbee0c2099aefa609
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446313"
---
# <a name="get-a-customers-qualification-asynchronously"></a><span data-ttu-id="144fd-104">Asynchroniczne uzyskiwanie kwalifikacji klienta</span><span class="sxs-lookup"><span data-stu-id="144fd-104">Get a customer's qualification asynchronously</span></span>

<span data-ttu-id="144fd-105">Jak asynchronicznie uzyskać kwalifikacje klienta.</span><span class="sxs-lookup"><span data-stu-id="144fd-105">How to get a customer's qualifications asynchronously.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="144fd-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="144fd-106">Prerequisites</span></span>

- <span data-ttu-id="144fd-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="144fd-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="144fd-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="144fd-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="144fd-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="144fd-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="144fd-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="144fd-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="144fd-111">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="144fd-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="144fd-112">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="144fd-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="144fd-113">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="144fd-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="144fd-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="144fd-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="144fd-115">C\#</span><span class="sxs-lookup"><span data-stu-id="144fd-115">C\#</span></span>

<span data-ttu-id="144fd-116">Aby uzyskać kwalifikacje klienta, wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta.</span><span class="sxs-lookup"><span data-stu-id="144fd-116">To get a customer's qualifications, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="144fd-117">Następnie użyj właściwości [**Qualification,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) aby pobrać [**interfejs ICustomerQualification.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification)</span><span class="sxs-lookup"><span data-stu-id="144fd-117">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="144fd-118">Na koniec zadzwoń `GetQualifications()` na numer lub , aby pobrać `GetQualificationsAsync()` kwalifikacje klienta.</span><span class="sxs-lookup"><span data-stu-id="144fd-118">Finally, call `GetQualifications()` or `GetQualificationsAsync()` to retrieve the customer's qualifications.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerQualifications = partnerOperations.Customers.ById(customerId).Qualification.GetQualifications();
```

<span data-ttu-id="144fd-119">**Przykład:** [przykładowa aplikacja konsoli](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="144fd-119">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="144fd-120">**Project:** SdkSamples, **klasa**: GetCustomerQualifications.cs</span><span class="sxs-lookup"><span data-stu-id="144fd-120">**Project**: SdkSamples **Class**: GetCustomerQualifications.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="144fd-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="144fd-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="144fd-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="144fd-122">Request syntax</span></span>

| <span data-ttu-id="144fd-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="144fd-123">Method</span></span>  | <span data-ttu-id="144fd-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="144fd-124">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="144fd-125">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="144fd-125">**GET**</span></span> | <span data-ttu-id="144fd-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="144fd-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="144fd-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="144fd-127">URI parameter</span></span>

<span data-ttu-id="144fd-128">W tej tabeli wymieniono wymagany parametr zapytania w celu uzyskania wszystkich kwalifikacji.</span><span class="sxs-lookup"><span data-stu-id="144fd-128">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="144fd-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="144fd-129">Name</span></span>               | <span data-ttu-id="144fd-130">Typ</span><span class="sxs-lookup"><span data-stu-id="144fd-130">Type</span></span>   | <span data-ttu-id="144fd-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="144fd-131">Required</span></span> | <span data-ttu-id="144fd-132">Opis</span><span class="sxs-lookup"><span data-stu-id="144fd-132">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="144fd-133">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="144fd-133">**customer-tenant-id**</span></span> | <span data-ttu-id="144fd-134">ciąg</span><span class="sxs-lookup"><span data-stu-id="144fd-134">string</span></span> | <span data-ttu-id="144fd-135">Tak</span><span class="sxs-lookup"><span data-stu-id="144fd-135">Yes</span></span>      | <span data-ttu-id="144fd-136">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="144fd-136">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="144fd-137">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="144fd-137">Request headers</span></span>

<span data-ttu-id="144fd-138">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="144fd-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="144fd-139">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="144fd-139">Request body</span></span>

<span data-ttu-id="144fd-140">Brak.</span><span class="sxs-lookup"><span data-stu-id="144fd-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="144fd-141">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="144fd-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="144fd-142">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="144fd-142">REST response</span></span>

<span data-ttu-id="144fd-143">W przypadku powodzenia ta metoda zwraca kolekcję kwalifikacji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="144fd-143">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="144fd-144">Poniżej przedstawiono przykłady rozmowy **GET** dotyczącej klienta z kwalifikacją **do edukacji.**</span><span class="sxs-lookup"><span data-stu-id="144fd-144">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="144fd-145">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="144fd-145">Response success and error codes</span></span>

<span data-ttu-id="144fd-146">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="144fd-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="144fd-147">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="144fd-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="144fd-148">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="144fd-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="144fd-149">Przykłady odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="144fd-149">Response examples</span></span>

#### <a name="approved"></a><span data-ttu-id="144fd-150">Approved (Zatwierdzono)</span><span class="sxs-lookup"><span data-stu-id="144fd-150">Approved</span></span>

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

#### <a name="in-review"></a><span data-ttu-id="144fd-151">Przegląd</span><span class="sxs-lookup"><span data-stu-id="144fd-151">In Review</span></span>

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

#### <a name="denied"></a><span data-ttu-id="144fd-152">Odmowa</span><span class="sxs-lookup"><span data-stu-id="144fd-152">Denied</span></span>

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

#### <a name="state-owned-entity-samples"></a><span data-ttu-id="144fd-153">Przykłady jednostek należących do stanu</span><span class="sxs-lookup"><span data-stu-id="144fd-153">State Owned Entity Samples</span></span>

<span data-ttu-id="144fd-154">**Przykład jednostki należącej do stanu za pośrednictwem posta**</span><span class="sxs-lookup"><span data-stu-id="144fd-154">**State Owned Entity via POST sample**</span></span>

```csharp

//SOE
POST {customer_id}/qualifications
{
“qualification”: “StateOwnedEntity”
}

//

```

<span data-ttu-id="144fd-155">**Jednostka należąca do stanu za pośrednictwem przykładu Pobierz kwalifikacje**</span><span class="sxs-lookup"><span data-stu-id="144fd-155">**State Owned Entity via Get Qualifications sample**</span></span>

```csharp

//SOE:
GET {customer_id}/qualifications
[
    {
        “qualification”: “StateOwnedEntity”
    }
]

```

<span data-ttu-id="144fd-156">**Jednostka należąca do stanu za pośrednictwem get qualifications with Education**</span><span class="sxs-lookup"><span data-stu-id="144fd-156">**State Owned Entity via Get Qualifications with Education**</span></span>

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

<span data-ttu-id="144fd-157">**Jednostka należąca do stanu za pośrednictwem get qualifications with GCC**</span><span class="sxs-lookup"><span data-stu-id="144fd-157">**State Owned Entity via Get Qualifications with GCC**</span></span>

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

## <a name="related-articles"></a><span data-ttu-id="144fd-158">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="144fd-158">Related articles</span></span>

- [<span data-ttu-id="144fd-159">Aktualizowanie kwalifikacji klienta</span><span class="sxs-lookup"><span data-stu-id="144fd-159">Update a customer's qualifications</span></span>](./update-customer-qualification-asynchronous.md)
