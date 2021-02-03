---
title: Pobieranie kwalifikacji klienta
description: Dowiedz się, jak używać walidacji synchronicznej w celu uzyskania kwalifikacji klienta za pośrednictwem interfejsu API Centrum partnerskiego. Partnerzy mogą używać tego do weryfikowania klientów edukacyjnych.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 82812091be9c13d64ac183c37461e3b63b2ec294
ms.sourcegitcommit: 0c98496e972aebe10eba23822aa229125bfc035d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770187"
---
# <a name="get-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="89093-104">Uzyskaj kwalifikację klienta poprzez synchroniczną weryfikację</span><span class="sxs-lookup"><span data-stu-id="89093-104">Get a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="89093-105">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="89093-105">**Applies To**</span></span>

- <span data-ttu-id="89093-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="89093-106">Partner Center</span></span>

<span data-ttu-id="89093-107">Dowiedz się, jak uzyskać kwalifikację klienta synchronicznie za pośrednictwem interfejsów API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="89093-107">Learn how to get a customer's qualification synchronously via Partner Center APIs.</span></span> <span data-ttu-id="89093-108">Aby dowiedzieć się, jak to zrobić asynchronicznie, zobacz artykuł [pobieranie kwalifikacji klienta za pośrednictwem walidacji asynchronicznej](get-customer-qualification-asynchronous.md).</span><span class="sxs-lookup"><span data-stu-id="89093-108">To learn how to do this asynchronously, see [Get a customer's qualification via asynchronous validation](get-customer-qualification-asynchronous.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89093-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="89093-109">Prerequisites</span></span>

- <span data-ttu-id="89093-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="89093-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="89093-111">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89093-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="89093-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="89093-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="89093-113">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="89093-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="89093-114">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="89093-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="89093-115">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="89093-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="89093-116">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="89093-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="89093-117">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="89093-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="89093-118">C\#</span><span class="sxs-lookup"><span data-stu-id="89093-118">C\#</span></span>

<span data-ttu-id="89093-119">Aby uzyskać kwalifikację klienta, wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta.</span><span class="sxs-lookup"><span data-stu-id="89093-119">To get a customer's qualification, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="89093-120">Następnie użyj właściwości [**kwalifikacji**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) do pobrania interfejsu [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) .</span><span class="sxs-lookup"><span data-stu-id="89093-120">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="89093-121">Na koniec Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) , aby pobrać kwalifikację klienta.</span><span class="sxs-lookup"><span data-stu-id="89093-121">Finally, call [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) to retrieve the customer's qualification.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerQualification = partnerOperations.Customers.ById(customerId).Qualification.Get();
```

## <a name="rest-request"></a><span data-ttu-id="89093-122">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="89093-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="89093-123">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="89093-123">Request syntax</span></span>

| <span data-ttu-id="89093-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="89093-124">Method</span></span>  | <span data-ttu-id="89093-125">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="89093-125">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="89093-126">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="89093-126">**GET**</span></span> | <span data-ttu-id="89093-127">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Qualification http/1.1</span><span class="sxs-lookup"><span data-stu-id="89093-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualification HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="89093-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="89093-128">URI parameter</span></span>

<span data-ttu-id="89093-129">Ta tabela zawiera listę wymaganych parametrów zapytania, aby uzyskać wszystkie kwalifikacje.</span><span class="sxs-lookup"><span data-stu-id="89093-129">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="89093-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="89093-130">Name</span></span>               | <span data-ttu-id="89093-131">Typ</span><span class="sxs-lookup"><span data-stu-id="89093-131">Type</span></span>   | <span data-ttu-id="89093-132">Wymagane</span><span class="sxs-lookup"><span data-stu-id="89093-132">Required</span></span> | <span data-ttu-id="89093-133">Opis</span><span class="sxs-lookup"><span data-stu-id="89093-133">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="89093-134">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="89093-134">**customer-tenant-id**</span></span> | <span data-ttu-id="89093-135">ciąg</span><span class="sxs-lookup"><span data-stu-id="89093-135">string</span></span> | <span data-ttu-id="89093-136">Tak</span><span class="sxs-lookup"><span data-stu-id="89093-136">Yes</span></span>      | <span data-ttu-id="89093-137">Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="89093-137">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="89093-138">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="89093-138">Request headers</span></span>

<span data-ttu-id="89093-139">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="89093-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="89093-140">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="89093-140">Request body</span></span>

<span data-ttu-id="89093-141">Brak.</span><span class="sxs-lookup"><span data-stu-id="89093-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="89093-142">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="89093-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="89093-143">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="89093-143">REST response</span></span>

<span data-ttu-id="89093-144">Jeśli to się powiedzie, metoda zwraca wartość kwalifikacji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="89093-144">If successful, this method returns a qualification value in the response body.</span></span>  <span data-ttu-id="89093-145">Poniżej znajduje się przykład wywołania **Get** na kliencie z kwalifikacją **edukacyjną** .</span><span class="sxs-lookup"><span data-stu-id="89093-145">Below is an example of the **GET** call on a customer with the **education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="89093-146">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="89093-146">Response success and error codes</span></span>

<span data-ttu-id="89093-147">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="89093-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="89093-148">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="89093-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="89093-149">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="89093-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="89093-150">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="89093-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

    "education"

```

## <a name="related-articles"></a><span data-ttu-id="89093-151">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="89093-151">Related articles</span></span>

- [<span data-ttu-id="89093-152">Aktualizowanie kwalifikacji klienta</span><span class="sxs-lookup"><span data-stu-id="89093-152">Update a customer's qualification</span></span>](update-a-customer-s-qualification.md)
