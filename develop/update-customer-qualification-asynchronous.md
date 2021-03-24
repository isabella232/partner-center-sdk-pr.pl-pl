---
title: Aktualizowanie kwalifikacji klienta
description: Program aktualizuje kwalifikacje klienta asynchronicznie, w tym adres skojarzony z profilem.
ms.date: 03/23/2021
ms.service: partner-dashboard
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 7606eeaac4df158ec0fad6ffd4e565bb250f448e
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030610"
---
# <a name="update-a-customers-qualifications-asynchronously"></a><span data-ttu-id="9a7f2-103">Aktualizowanie kwalifikacji klienta asynchronicznie</span><span class="sxs-lookup"><span data-stu-id="9a7f2-103">Update a customer's qualifications asynchronously</span></span>

<span data-ttu-id="9a7f2-104">Aktualizuje kwalifikacje klienta asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="9a7f2-104">Updates a customer's qualifications asynchronously.</span></span>

<span data-ttu-id="9a7f2-105">Partner może zaktualizować kwalifikacje klienta asynchronicznie do "Education" lub "GovernmentCommunityCloud".</span><span class="sxs-lookup"><span data-stu-id="9a7f2-105">A partner can update a customer's qualifications asynchronously to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="9a7f2-106">Nie można ustawić innych wartości, "none" i "non profit".</span><span class="sxs-lookup"><span data-stu-id="9a7f2-106">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a7f2-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9a7f2-107">Prerequisites</span></span>

- <span data-ttu-id="9a7f2-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9a7f2-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9a7f2-109">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9a7f2-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="9a7f2-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9a7f2-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9a7f2-111">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="9a7f2-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9a7f2-112">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="9a7f2-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9a7f2-113">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="9a7f2-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9a7f2-114">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="9a7f2-114">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9a7f2-115">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9a7f2-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="9a7f2-116">C\#</span><span class="sxs-lookup"><span data-stu-id="9a7f2-116">C\#</span></span>

<span data-ttu-id="9a7f2-117">Aby utworzyć kwalifikację klienta dla "edukacji", najpierw Utwórz obiekt reprezentujący typ kwalifikacji.</span><span class="sxs-lookup"><span data-stu-id="9a7f2-117">To create a customer's qualification for "Education", first create an object representing the qualification type.</span></span> <span data-ttu-id="9a7f2-118">Następnie Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta.</span><span class="sxs-lookup"><span data-stu-id="9a7f2-118">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="9a7f2-119">Następnie użyj właściwości [**kwalifikacji**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) do pobrania interfejsu [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) .</span><span class="sxs-lookup"><span data-stu-id="9a7f2-119">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="9a7f2-120">Na koniec Wywołaj `CreateQualifications()` lub `CreateQualificationsAsync()` z obiektem typu kwalifikacji jako parametr wejściowy.</span><span class="sxs-lookup"><span data-stu-id="9a7f2-120">Finally, call `CreateQualifications()` or `CreateQualificationsAsync()` with the qualification type object as an input parameter.</span></span>

``` csharp
var qualificationType = { Qualification = "education" };
var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType);
```

<span data-ttu-id="9a7f2-121">**Przykład**: [Przykładowa aplikacja konsolowa](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="9a7f2-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="9a7f2-122">**Projekt**: SdkSamples **Class**: CreateCustomerQualification. cs</span><span class="sxs-lookup"><span data-stu-id="9a7f2-122">**Project**: SdkSamples **Class**: CreateCustomerQualification.cs</span></span>

<span data-ttu-id="9a7f2-123">Aby zaktualizować kwalifikację klienta do **GovernmentCommunityCloud** na istniejącym kliencie bez kwalifikacji, partner jest również zobowiązany do uwzględnienia [**ValidationCode**](utility-resources.md#validationcode)klienta.</span><span class="sxs-lookup"><span data-stu-id="9a7f2-123">To update a customer's qualification to **GovernmentCommunityCloud** on an existing customer without a qualification, the partner is also required to include the customer's [**ValidationCode**](utility-resources.md#validationcode).</span></span> <span data-ttu-id="9a7f2-124">Najpierw Utwórz obiekt reprezentujący typ kwalifikacji.</span><span class="sxs-lookup"><span data-stu-id="9a7f2-124">First, create an object representing the qualification type.</span></span> <span data-ttu-id="9a7f2-125">Następnie Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta.</span><span class="sxs-lookup"><span data-stu-id="9a7f2-125">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="9a7f2-126">Następnie użyj właściwości [**kwalifikacji**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) do pobrania interfejsu [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) .</span><span class="sxs-lookup"><span data-stu-id="9a7f2-126">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="9a7f2-127">Na koniec Wywołaj `CreateQualifications()` lub `CreateQualificationsAsync()` z obiektem typu kwalifikacji i kodem sprawdzania poprawności jako parametry wejściowe.</span><span class="sxs-lookup"><span data-stu-id="9a7f2-127">Finally, call `CreateQualifications()` or `CreateQualificationsAsync()` with the qualification type object and the validation code as input parameters.</span></span>

``` csharp
// GCC validation is type ValidationCode
var qualificationType = { Qualification = "GovernmentCommunityCloud" };
var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType, gccValidation);
```

<span data-ttu-id="9a7f2-128">**Przykład**: [Przykładowa aplikacja konsolowa](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="9a7f2-128">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="9a7f2-129">**Projekt**: SdkSamples **Class**: CreateCustomerQualificationWithGCC. cs</span><span class="sxs-lookup"><span data-stu-id="9a7f2-129">**Project**: SdkSamples **Class**: CreateCustomerQualificationWithGCC.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9a7f2-130">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="9a7f2-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9a7f2-131">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="9a7f2-131">Request syntax</span></span>

| <span data-ttu-id="9a7f2-132">Metoda</span><span class="sxs-lookup"><span data-stu-id="9a7f2-132">Method</span></span>  | <span data-ttu-id="9a7f2-133">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="9a7f2-133">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a7f2-134">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="9a7f2-134">**POST**</span></span> | <span data-ttu-id="9a7f2-135">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer_ID}/Qualifications? Code = {VALIDATIONCODE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="9a7f2-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9a7f2-136">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="9a7f2-136">URI parameter</span></span>

<span data-ttu-id="9a7f2-137">Użyj następującego parametru zapytania, aby zaktualizować kwalifikacje.</span><span class="sxs-lookup"><span data-stu-id="9a7f2-137">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="9a7f2-138">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9a7f2-138">Name</span></span>                   | <span data-ttu-id="9a7f2-139">Typ</span><span class="sxs-lookup"><span data-stu-id="9a7f2-139">Type</span></span> | <span data-ttu-id="9a7f2-140">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9a7f2-140">Required</span></span> | <span data-ttu-id="9a7f2-141">Opis</span><span class="sxs-lookup"><span data-stu-id="9a7f2-141">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a7f2-142">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="9a7f2-142">**customer-tenant-id**</span></span> | <span data-ttu-id="9a7f2-143">GUID</span><span class="sxs-lookup"><span data-stu-id="9a7f2-143">GUID</span></span> | <span data-ttu-id="9a7f2-144">Tak</span><span class="sxs-lookup"><span data-stu-id="9a7f2-144">Yes</span></span>      | <span data-ttu-id="9a7f2-145">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="9a7f2-145">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="9a7f2-146">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="9a7f2-146">**validationCode**</span></span>     | <span data-ttu-id="9a7f2-147">int</span><span class="sxs-lookup"><span data-stu-id="9a7f2-147">int</span></span>  | <span data-ttu-id="9a7f2-148">Nie</span><span class="sxs-lookup"><span data-stu-id="9a7f2-148">No</span></span>       | <span data-ttu-id="9a7f2-149">Wymagany tylko w przypadku chmury społecznościowej dla instytucji rządowych.</span><span class="sxs-lookup"><span data-stu-id="9a7f2-149">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="9a7f2-150">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="9a7f2-150">Request headers</span></span>

<span data-ttu-id="9a7f2-151">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9a7f2-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9a7f2-152">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="9a7f2-152">Request body</span></span>

<span data-ttu-id="9a7f2-153">W tej tabeli opisano obiekt kwalifikacji w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="9a7f2-153">This table describes the qualification object in the request body.</span></span>

<span data-ttu-id="9a7f2-154">Właściwość</span><span class="sxs-lookup"><span data-stu-id="9a7f2-154">Property</span></span> | <span data-ttu-id="9a7f2-155">Typ</span><span class="sxs-lookup"><span data-stu-id="9a7f2-155">Type</span></span> | <span data-ttu-id="9a7f2-156">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9a7f2-156">Required</span></span> | <span data-ttu-id="9a7f2-157">Opis</span><span class="sxs-lookup"><span data-stu-id="9a7f2-157">Description</span></span>
-------- | ---- | -------- | -----------
<span data-ttu-id="9a7f2-158">Kwalifikacja</span><span class="sxs-lookup"><span data-stu-id="9a7f2-158">Qualification</span></span> | <span data-ttu-id="9a7f2-159">ciąg</span><span class="sxs-lookup"><span data-stu-id="9a7f2-159">string</span></span> | <span data-ttu-id="9a7f2-160">Tak</span><span class="sxs-lookup"><span data-stu-id="9a7f2-160">Yes</span></span> | <span data-ttu-id="9a7f2-161">Wartość ciągu z wyliczenia [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) .</span><span class="sxs-lookup"><span data-stu-id="9a7f2-161">The string value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="9a7f2-162">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="9a7f2-162">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

{
    "Qualification": "Education"
}

```

## <a name="rest-response"></a><span data-ttu-id="9a7f2-163">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="9a7f2-163">REST response</span></span>

<span data-ttu-id="9a7f2-164">Jeśli to się powiedzie, metoda zwraca obiekt kwalifikacji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="9a7f2-164">If successful, this method returns a qualifications object in the response body.</span></span> <span data-ttu-id="9a7f2-165">Poniżej znajduje się przykład wywołania **post** na kliencie (z wcześniejszą kwalifikacją dla **braku**) z kwalifikacją **edukacyjną** .</span><span class="sxs-lookup"><span data-stu-id="9a7f2-165">Below is an example of the **POST** call on a customer (with a previous qualification of **None**) with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9a7f2-166">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9a7f2-166">Response success and error codes</span></span>

<span data-ttu-id="9a7f2-167">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="9a7f2-167">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9a7f2-168">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="9a7f2-168">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9a7f2-169">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9a7f2-169">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9a7f2-170">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9a7f2-170">Response example</span></span>

```http
HTTP/1.1 201 CREATED
Content-Length: 29
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualification": "Education",
    "vettingStatus": "InReview",
    "vettingCreateDate": "2020-12-04T20:54:24Z" // UTC
}
```

## <a name="related-articles"></a><span data-ttu-id="9a7f2-171">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="9a7f2-171">Related articles</span></span>

- [<span data-ttu-id="9a7f2-172">Pobierz kwalifikacje klienta</span><span class="sxs-lookup"><span data-stu-id="9a7f2-172">Get a customer's qualifications</span></span>](./get-customer-qualification-asynchronous.md)
- [<span data-ttu-id="9a7f2-173">Pobieranie kodów weryfikacyjnych partnera</span><span class="sxs-lookup"><span data-stu-id="9a7f2-173">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)
