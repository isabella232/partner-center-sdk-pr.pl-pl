---
title: Pobieranie kwalifikacji klienta
description: Dowiedz się, jak używać walidacji synchronicznej w celu uzyskania kwalifikacji klienta za pośrednictwem interfejsu API Centrum partnerskiego. Partnerzy mogą używać tego do weryfikowania klientów edukacyjnych.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e39ace3b598736abed6ab22021a8b93d473486a3
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711894"
---
# <a name="get-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="108ee-104">Uzyskaj kwalifikację klienta poprzez synchroniczną weryfikację</span><span class="sxs-lookup"><span data-stu-id="108ee-104">Get a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="108ee-105">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="108ee-105">**Applies To**</span></span>

- <span data-ttu-id="108ee-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="108ee-106">Partner Center</span></span>

<span data-ttu-id="108ee-107">Dowiedz się, jak uzyskać kwalifikację klienta synchronicznie za pośrednictwem interfejsów API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="108ee-107">Learn how to get a customer's qualification synchronously via Partner Center APIs.</span></span> <span data-ttu-id="108ee-108">Aby dowiedzieć się, jak to zrobić asynchronicznie, zobacz artykuł [pobieranie kwalifikacji klienta za pośrednictwem walidacji asynchronicznej](get-customer-qualification-asynchronous.md).</span><span class="sxs-lookup"><span data-stu-id="108ee-108">To learn how to do this asynchronously, see [Get a customer's qualification via asynchronous validation](get-customer-qualification-asynchronous.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="108ee-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="108ee-109">Prerequisites</span></span>

- <span data-ttu-id="108ee-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="108ee-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="108ee-111">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="108ee-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="108ee-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="108ee-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="108ee-113">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="108ee-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="108ee-114">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="108ee-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="108ee-115">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="108ee-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="108ee-116">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="108ee-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="108ee-117">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="108ee-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="108ee-118">C\#</span><span class="sxs-lookup"><span data-stu-id="108ee-118">C\#</span></span>

<span data-ttu-id="108ee-119">Aby uzyskać kwalifikację klienta, wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta.</span><span class="sxs-lookup"><span data-stu-id="108ee-119">To get a customer's qualification, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="108ee-120">Następnie użyj właściwości [**kwalifikacji**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) do pobrania interfejsu [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) .</span><span class="sxs-lookup"><span data-stu-id="108ee-120">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="108ee-121">Na koniec Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) , aby pobrać kwalifikację klienta.</span><span class="sxs-lookup"><span data-stu-id="108ee-121">Finally, call [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) to retrieve the customer's qualification.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerQualification = partnerOperations.Customers.ById(customerId).Qualification.Get();
```

## <a name="rest-request"></a><span data-ttu-id="108ee-122">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="108ee-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="108ee-123">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="108ee-123">Request syntax</span></span>

| <span data-ttu-id="108ee-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="108ee-124">Method</span></span>  | <span data-ttu-id="108ee-125">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="108ee-125">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="108ee-126">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="108ee-126">**GET**</span></span> | <span data-ttu-id="108ee-127">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Qualification http/1.1</span><span class="sxs-lookup"><span data-stu-id="108ee-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualification HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="108ee-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="108ee-128">URI parameter</span></span>

<span data-ttu-id="108ee-129">Ta tabela zawiera listę wymaganych parametrów zapytania, aby uzyskać wszystkie kwalifikacje.</span><span class="sxs-lookup"><span data-stu-id="108ee-129">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="108ee-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="108ee-130">Name</span></span>               | <span data-ttu-id="108ee-131">Typ</span><span class="sxs-lookup"><span data-stu-id="108ee-131">Type</span></span>   | <span data-ttu-id="108ee-132">Wymagane</span><span class="sxs-lookup"><span data-stu-id="108ee-132">Required</span></span> | <span data-ttu-id="108ee-133">Opis</span><span class="sxs-lookup"><span data-stu-id="108ee-133">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="108ee-134">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="108ee-134">**customer-tenant-id**</span></span> | <span data-ttu-id="108ee-135">ciąg</span><span class="sxs-lookup"><span data-stu-id="108ee-135">string</span></span> | <span data-ttu-id="108ee-136">Tak</span><span class="sxs-lookup"><span data-stu-id="108ee-136">Yes</span></span>      | <span data-ttu-id="108ee-137">Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="108ee-137">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="108ee-138">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="108ee-138">Request headers</span></span>

<span data-ttu-id="108ee-139">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="108ee-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="108ee-140">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="108ee-140">Request body</span></span>

<span data-ttu-id="108ee-141">Brak.</span><span class="sxs-lookup"><span data-stu-id="108ee-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="108ee-142">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="108ee-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="108ee-143">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="108ee-143">REST response</span></span>

<span data-ttu-id="108ee-144">Jeśli to się powiedzie, metoda zwraca wartość kwalifikacji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="108ee-144">If successful, this method returns a qualification value in the response body.</span></span>  <span data-ttu-id="108ee-145">Poniżej znajduje się przykład wywołania **Get** na kliencie z kwalifikacją **edukacyjną** .</span><span class="sxs-lookup"><span data-stu-id="108ee-145">Below is an example of the **GET** call on a customer with the **education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="108ee-146">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="108ee-146">Response success and error codes</span></span>

<span data-ttu-id="108ee-147">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="108ee-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="108ee-148">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="108ee-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="108ee-149">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="108ee-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="108ee-150">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="108ee-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

    "education"

```

## <a name="related-articles"></a><span data-ttu-id="108ee-151">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="108ee-151">Related articles</span></span>

- [<span data-ttu-id="108ee-152">Aktualizowanie kwalifikacji klienta</span><span class="sxs-lookup"><span data-stu-id="108ee-152">Update a customer's qualification</span></span>](./update-customer-qualification-synchronous.md)