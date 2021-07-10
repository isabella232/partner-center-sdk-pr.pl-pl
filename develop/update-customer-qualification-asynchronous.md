---
title: Aktualizowanie kwalifikacji klienta
description: Asynchronicznie aktualizuje kwalifikacje klienta, w tym adres skojarzony z profilem.
ms.date: 03/23/2021
ms.service: partner-dashboard
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: d7dd3593894ce91ddc7b96d604b80153d41d3a67
ms.sourcegitcommit: 51237e7e98d71a7e0590b4d6a4034b6409542126
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/09/2021
ms.locfileid: "113572101"
---
# <a name="update-a-customers-qualifications-asynchronously"></a><span data-ttu-id="35d51-103">Asynchroniczne aktualizowanie kwalifikacji klienta</span><span class="sxs-lookup"><span data-stu-id="35d51-103">Update a customer's qualifications asynchronously</span></span>

<span data-ttu-id="35d51-104">Aktualizuje kwalifikacje klienta asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="35d51-104">Updates a customer's qualifications asynchronously.</span></span>

<span data-ttu-id="35d51-105">Partner może asynchronicznie zaktualizować kwalifikacje klienta tak, aby zawierały "Edukacja" lub "GovernmentCo w chmurze".</span><span class="sxs-lookup"><span data-stu-id="35d51-105">A partner can update a customer's qualifications asynchronously to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="35d51-106">Innych wartości, "Brak" i "Nonprofit", nie można ustawić.</span><span class="sxs-lookup"><span data-stu-id="35d51-106">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35d51-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="35d51-107">Prerequisites</span></span>

- <span data-ttu-id="35d51-108">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="35d51-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="35d51-109">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="35d51-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="35d51-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="35d51-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="35d51-111">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="35d51-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="35d51-112">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="35d51-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="35d51-113">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="35d51-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="35d51-114">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="35d51-114">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="35d51-115">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="35d51-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="35d51-116">C\#</span><span class="sxs-lookup"><span data-stu-id="35d51-116">C\#</span></span>

<span data-ttu-id="35d51-117">Aby utworzyć kwalifikację klienta do "Edukacja", najpierw utwórz obiekt reprezentujący typ kwalifikacji.</span><span class="sxs-lookup"><span data-stu-id="35d51-117">To create a customer's qualification for "Education", first create an object representing the qualification type.</span></span> <span data-ttu-id="35d51-118">Następnie wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu identyfikatora klienta.</span><span class="sxs-lookup"><span data-stu-id="35d51-118">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="35d51-119">Następnie użyj właściwości [**Kwalifikacja,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) aby pobrać [**interfejs ICustomerQualification.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification)</span><span class="sxs-lookup"><span data-stu-id="35d51-119">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="35d51-120">Na koniec wywołaj element lub z `CreateQualifications()` `CreateQualificationsAsync()` obiektem typu kwalifikacji jako parametrem wejściowym.</span><span class="sxs-lookup"><span data-stu-id="35d51-120">Finally, call `CreateQualifications()` or `CreateQualificationsAsync()` with the qualification type object as an input parameter.</span></span>

``` csharp
var qualificationToCreate = "education";    // can also be "StateOwnedEntity" or "GovernmentCommunityCloud". See GCC example below.
var qualificationType = { Qualification = qualificationToCreate };
var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType);
```

<span data-ttu-id="35d51-121">**Przykład:** [Przykładowa aplikacja konsoli](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="35d51-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="35d51-122">**Project:** SdkSamples, **klasa**: CreateCustomerQualification.cs</span><span class="sxs-lookup"><span data-stu-id="35d51-122">**Project**: SdkSamples **Class**: CreateCustomerQualification.cs</span></span>

<span data-ttu-id="35d51-123">Aby zaktualizować kwalifikację klienta do chmury **GovernmentCo w** przypadku istniejącego klienta bez kwalifikacji, partner musi również uwzględnić kod [**weryfikacji klienta**](utility-resources.md#validationcode).</span><span class="sxs-lookup"><span data-stu-id="35d51-123">To update a customer's qualification to **GovernmentCommunityCloud** on an existing customer without a qualification, the partner is also required to include the customer's [**ValidationCode**](utility-resources.md#validationcode).</span></span> <span data-ttu-id="35d51-124">Najpierw utwórz obiekt reprezentujący typ kwalifikacji.</span><span class="sxs-lookup"><span data-stu-id="35d51-124">First, create an object representing the qualification type.</span></span> <span data-ttu-id="35d51-125">Następnie wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu identyfikatora klienta.</span><span class="sxs-lookup"><span data-stu-id="35d51-125">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="35d51-126">Następnie użyj właściwości [**Kwalifikacja,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) aby pobrać [**interfejs ICustomerQualification.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification)</span><span class="sxs-lookup"><span data-stu-id="35d51-126">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="35d51-127">Na koniec wywołaj `CreateQualifications()` parametr lub `CreateQualificationsAsync()` z obiektem typu kwalifikacji i kodem walidacji jako parametrami wejściowymi.</span><span class="sxs-lookup"><span data-stu-id="35d51-127">Finally, call `CreateQualifications()` or `CreateQualificationsAsync()` with the qualification type object and the validation code as input parameters.</span></span>

``` csharp
// GCC validation is type ValidationCode
var qualificationType = { Qualification = "GovernmentCommunityCloud" };
var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType, gccValidation);
```

<span data-ttu-id="35d51-128">**Przykład:** [Przykładowa aplikacja konsoli](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="35d51-128">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="35d51-129">**Project:** SdkSamples, **klasa**: CreateCustomerQualificationWithGCC.cs</span><span class="sxs-lookup"><span data-stu-id="35d51-129">**Project**: SdkSamples **Class**: CreateCustomerQualificationWithGCC.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="35d51-130">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="35d51-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="35d51-131">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="35d51-131">Request syntax</span></span>

| <span data-ttu-id="35d51-132">Metoda</span><span class="sxs-lookup"><span data-stu-id="35d51-132">Method</span></span>  | <span data-ttu-id="35d51-133">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="35d51-133">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="35d51-134">**Post**</span><span class="sxs-lookup"><span data-stu-id="35d51-134">**POST**</span></span> | <span data-ttu-id="35d51-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="35d51-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="35d51-136">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="35d51-136">URI parameter</span></span>

<span data-ttu-id="35d51-137">Użyj następującego parametru zapytania, aby zaktualizować kwalifikację.</span><span class="sxs-lookup"><span data-stu-id="35d51-137">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="35d51-138">Nazwa</span><span class="sxs-lookup"><span data-stu-id="35d51-138">Name</span></span>                   | <span data-ttu-id="35d51-139">Typ</span><span class="sxs-lookup"><span data-stu-id="35d51-139">Type</span></span> | <span data-ttu-id="35d51-140">Wymagane</span><span class="sxs-lookup"><span data-stu-id="35d51-140">Required</span></span> | <span data-ttu-id="35d51-141">Opis</span><span class="sxs-lookup"><span data-stu-id="35d51-141">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="35d51-142">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="35d51-142">**customer-tenant-id**</span></span> | <span data-ttu-id="35d51-143">GUID</span><span class="sxs-lookup"><span data-stu-id="35d51-143">GUID</span></span> | <span data-ttu-id="35d51-144">Tak</span><span class="sxs-lookup"><span data-stu-id="35d51-144">Yes</span></span>      | <span data-ttu-id="35d51-145">Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="35d51-145">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="35d51-146">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="35d51-146">**validationCode**</span></span>     | <span data-ttu-id="35d51-147">int</span><span class="sxs-lookup"><span data-stu-id="35d51-147">int</span></span>  | <span data-ttu-id="35d51-148">Nie</span><span class="sxs-lookup"><span data-stu-id="35d51-148">No</span></span>       | <span data-ttu-id="35d51-149">Wymagane tylko w przypadku Government Community Cloud.</span><span class="sxs-lookup"><span data-stu-id="35d51-149">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="35d51-150">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="35d51-150">Request headers</span></span>

<span data-ttu-id="35d51-151">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="35d51-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="35d51-152">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="35d51-152">Request body</span></span>

<span data-ttu-id="35d51-153">W tej tabeli opisano obiekt kwalifikacji w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="35d51-153">This table describes the qualification object in the request body.</span></span>

<span data-ttu-id="35d51-154">Właściwość</span><span class="sxs-lookup"><span data-stu-id="35d51-154">Property</span></span> | <span data-ttu-id="35d51-155">Typ</span><span class="sxs-lookup"><span data-stu-id="35d51-155">Type</span></span> | <span data-ttu-id="35d51-156">Wymagane</span><span class="sxs-lookup"><span data-stu-id="35d51-156">Required</span></span> | <span data-ttu-id="35d51-157">Opis</span><span class="sxs-lookup"><span data-stu-id="35d51-157">Description</span></span>
-------- | ---- | -------- | -----------
<span data-ttu-id="35d51-158">Kwalifikacja</span><span class="sxs-lookup"><span data-stu-id="35d51-158">Qualification</span></span> | <span data-ttu-id="35d51-159">ciąg</span><span class="sxs-lookup"><span data-stu-id="35d51-159">string</span></span> | <span data-ttu-id="35d51-160">Tak</span><span class="sxs-lookup"><span data-stu-id="35d51-160">Yes</span></span> | <span data-ttu-id="35d51-161">Wartość ciągu z [**wyli roku CustomerQualification.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification)</span><span class="sxs-lookup"><span data-stu-id="35d51-161">The string value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="35d51-162">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="35d51-162">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="35d51-163">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="35d51-163">REST response</span></span>

<span data-ttu-id="35d51-164">W przypadku powodzenia ta metoda zwraca obiekt kwalifikacji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="35d51-164">If successful, this method returns a qualifications object in the response body.</span></span> <span data-ttu-id="35d51-165">Poniżej znajduje się przykład rozmowy **POST** dotyczącej klienta (z wcześniejszą kwalifikacją **Brak)** z **kwalifikacją edukacja.**</span><span class="sxs-lookup"><span data-stu-id="35d51-165">Below is an example of the **POST** call on a customer (with a previous qualification of **None**) with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="35d51-166">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="35d51-166">Response success and error codes</span></span>

<span data-ttu-id="35d51-167">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="35d51-167">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="35d51-168">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="35d51-168">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="35d51-169">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="35d51-169">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="35d51-170">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="35d51-170">Response example</span></span>

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

## <a name="related-articles"></a><span data-ttu-id="35d51-171">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="35d51-171">Related articles</span></span>

- [<span data-ttu-id="35d51-172">Uzyskiwanie kwalifikacji klienta</span><span class="sxs-lookup"><span data-stu-id="35d51-172">Get a customer's qualifications</span></span>](./get-customer-qualification-asynchronous.md)
- [<span data-ttu-id="35d51-173">Pobieranie kodów weryfikacyjnych partnera</span><span class="sxs-lookup"><span data-stu-id="35d51-173">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)
