---
title: Pobieranie kwalifikacji klienta
description: Dowiedz się, jak za pomocą synchronicznej walidacji uzyskać kwalifikację klienta za pośrednictwem Partner Center API. Partnerzy mogą używać tego do weryfikowania klientów edukacyjnych.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d215ddb105efe3acd1182c4ff4bb25b045b121f0
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446347"
---
# <a name="get-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="e4ee4-104">Uzyskiwanie kwalifikacji klienta za pośrednictwem walidacji synchronicznej</span><span class="sxs-lookup"><span data-stu-id="e4ee4-104">Get a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="e4ee4-105">Dowiedz się, jak synchronicznie uzyskać kwalifikację klienta za pośrednictwem Partner Center API.</span><span class="sxs-lookup"><span data-stu-id="e4ee4-105">Learn how to get a customer's qualification synchronously via Partner Center APIs.</span></span> <span data-ttu-id="e4ee4-106">Aby dowiedzieć się, jak to zrobić asynchronicznie, zobacz Get a customer's qualification via asynchronous validation (Uzyskiwanie [kwalifikacji klienta za pośrednictwem walidacji asynchronicznej).](get-customer-qualification-asynchronous.md)</span><span class="sxs-lookup"><span data-stu-id="e4ee4-106">To learn how to do this asynchronously, see [Get a customer's qualification via asynchronous validation](get-customer-qualification-asynchronous.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4ee4-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e4ee4-107">Prerequisites</span></span>

- <span data-ttu-id="e4ee4-108">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e4ee4-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e4ee4-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e4ee4-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e4ee4-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e4ee4-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e4ee4-111">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="e4ee4-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e4ee4-112">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="e4ee4-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e4ee4-113">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="e4ee4-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e4ee4-114">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="e4ee4-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e4ee4-115">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e4ee4-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="e4ee4-116">C\#</span><span class="sxs-lookup"><span data-stu-id="e4ee4-116">C\#</span></span>

<span data-ttu-id="e4ee4-117">Aby uzyskać kwalifikację klienta, wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta.</span><span class="sxs-lookup"><span data-stu-id="e4ee4-117">To get a customer's qualification, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="e4ee4-118">Następnie użyj właściwości [**Kwalifikacja,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) aby pobrać [**interfejs ICustomerQualification.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification)</span><span class="sxs-lookup"><span data-stu-id="e4ee4-118">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="e4ee4-119">Na koniec [**wywołaj usługę Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) aby pobrać kwalifikację klienta.</span><span class="sxs-lookup"><span data-stu-id="e4ee4-119">Finally, call [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) to retrieve the customer's qualification.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerQualification = partnerOperations.Customers.ById(customerId).Qualification.Get();
```

## <a name="rest-request"></a><span data-ttu-id="e4ee4-120">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="e4ee4-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e4ee4-121">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="e4ee4-121">Request syntax</span></span>

| <span data-ttu-id="e4ee4-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="e4ee4-122">Method</span></span>  | <span data-ttu-id="e4ee4-123">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="e4ee4-123">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e4ee4-124">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="e4ee4-124">**GET**</span></span> | <span data-ttu-id="e4ee4-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualification HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e4ee4-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualification HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e4ee4-126">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="e4ee4-126">URI parameter</span></span>

<span data-ttu-id="e4ee4-127">W tej tabeli wymieniono wymagany parametr zapytania w celu uzyskania wszystkich kwalifikacji.</span><span class="sxs-lookup"><span data-stu-id="e4ee4-127">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="e4ee4-128">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e4ee4-128">Name</span></span>               | <span data-ttu-id="e4ee4-129">Typ</span><span class="sxs-lookup"><span data-stu-id="e4ee4-129">Type</span></span>   | <span data-ttu-id="e4ee4-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e4ee4-130">Required</span></span> | <span data-ttu-id="e4ee4-131">Opis</span><span class="sxs-lookup"><span data-stu-id="e4ee4-131">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="e4ee4-132">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="e4ee4-132">**customer-tenant-id**</span></span> | <span data-ttu-id="e4ee4-133">ciąg</span><span class="sxs-lookup"><span data-stu-id="e4ee4-133">string</span></span> | <span data-ttu-id="e4ee4-134">Tak</span><span class="sxs-lookup"><span data-stu-id="e4ee4-134">Yes</span></span>      | <span data-ttu-id="e4ee4-135">Ciąg w formacie identyfikatora GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="e4ee4-135">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e4ee4-136">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="e4ee4-136">Request headers</span></span>

<span data-ttu-id="e4ee4-137">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e4ee4-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e4ee4-138">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="e4ee4-138">Request body</span></span>

<span data-ttu-id="e4ee4-139">Brak.</span><span class="sxs-lookup"><span data-stu-id="e4ee4-139">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e4ee4-140">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="e4ee4-140">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="e4ee4-141">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="e4ee4-141">REST response</span></span>

<span data-ttu-id="e4ee4-142">W przypadku powodzenia ta metoda zwraca wartość kwalifikacji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e4ee4-142">If successful, this method returns a qualification value in the response body.</span></span>  <span data-ttu-id="e4ee4-143">Poniżej znajduje się przykład rozmowy **GET** dotyczącej klienta z kwalifikacją **edukacyjną.**</span><span class="sxs-lookup"><span data-stu-id="e4ee4-143">Below is an example of the **GET** call on a customer with the **education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e4ee4-144">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e4ee4-144">Response success and error codes</span></span>

<span data-ttu-id="e4ee4-145">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="e4ee4-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e4ee4-146">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="e4ee4-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e4ee4-147">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e4ee4-147">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e4ee4-148">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e4ee4-148">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

    "education"

```

## <a name="related-articles"></a><span data-ttu-id="e4ee4-149">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="e4ee4-149">Related articles</span></span>

- [<span data-ttu-id="e4ee4-150">Aktualizowanie kwalifikacji klienta</span><span class="sxs-lookup"><span data-stu-id="e4ee4-150">Update a customer's qualification</span></span>](./update-customer-qualification-synchronous.md)