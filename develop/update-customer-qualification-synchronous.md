---
title: Aktualizowanie kwalifikacji klienta
description: Dowiedz się, jak zaktualizować kwalifikacje klienta za pomocą synchronicznego badania lub weryfikacyjnego, w tym adresu skojarzonego z profilem.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 5047743afdef02033d9494e3d8c16c9ab96b3fe9
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446653"
---
# <a name="update-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="1ca73-103">Aktualizowanie kwalifikacji klienta za pomocą walidacji synchronicznej</span><span class="sxs-lookup"><span data-stu-id="1ca73-103">Update a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="1ca73-104">Dowiedz się, jak synchronicznie aktualizować kwalifikacje klienta za pośrednictwem Partner Center API.</span><span class="sxs-lookup"><span data-stu-id="1ca73-104">Learn how to update a customer's qualifications synchronously via Partner Center APIs.</span></span> <span data-ttu-id="1ca73-105">Aby dowiedzieć się, jak to zrobić asynchronicznie, zobacz Aktualizowanie kwalifikacji klienta za pomocą [walidacji asynchronicznej.](update-customer-qualification-asynchronous.md)</span><span class="sxs-lookup"><span data-stu-id="1ca73-105">To learn how to do this asynchronously, see [Update a customer's qualification via asynchronous validation](update-customer-qualification-asynchronous.md).</span></span>

<span data-ttu-id="1ca73-106">Partner może zaktualizować kwalifikację klienta na "Edukacja" lub "GovernmentCo w chmurze".</span><span class="sxs-lookup"><span data-stu-id="1ca73-106">A partner can update a customer's qualification to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="1ca73-107">Innych wartości, "Brak" i "Nonprofit", nie można ustawić.</span><span class="sxs-lookup"><span data-stu-id="1ca73-107">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ca73-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1ca73-108">Prerequisites</span></span>

- <span data-ttu-id="1ca73-109">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1ca73-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1ca73-110">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1ca73-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="1ca73-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1ca73-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1ca73-112">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="1ca73-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1ca73-113">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="1ca73-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1ca73-114">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="1ca73-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1ca73-115">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="1ca73-115">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1ca73-116">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1ca73-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="1ca73-117">C\#</span><span class="sxs-lookup"><span data-stu-id="1ca73-117">C\#</span></span>

<span data-ttu-id="1ca73-118">Aby zaktualizować kwalifikację klienta do "Edukacja", wywołaj **[Update/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** istniejącego [**klienta.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer)</span><span class="sxs-lookup"><span data-stu-id="1ca73-118">To update a customer's qualification to "Education", call **[Update/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** on an existing  [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).</span></span>

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

<span data-ttu-id="1ca73-119">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="1ca73-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="1ca73-120">**Project:** PartnerSDK.FeatureSamples, **klasa:** CustomerQualificationOperations.cs</span><span class="sxs-lookup"><span data-stu-id="1ca73-120">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerQualificationOperations.cs</span></span>

<span data-ttu-id="1ca73-121">Aby zaktualizować kwalifikację klienta do chmury **GovernmentCo w** przypadku istniejącego klienta bez kwalifikacji, partner musi uwzględnić kod [**weryfikacji klienta**](utility-resources.md#validationcode).</span><span class="sxs-lookup"><span data-stu-id="1ca73-121">To update a customer's qualification to **GovernmentCommunityCloud** on an existing customer without a qualification, the partner is required to include the customer's [**ValidationCode**](utility-resources.md#validationcode).</span></span>

``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```

## <a name="rest-request"></a><span data-ttu-id="1ca73-122">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="1ca73-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1ca73-123">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="1ca73-123">Request syntax</span></span>

| <span data-ttu-id="1ca73-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="1ca73-124">Method</span></span>  | <span data-ttu-id="1ca73-125">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="1ca73-125">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1ca73-126">**PUT**</span><span class="sxs-lookup"><span data-stu-id="1ca73-126">**PUT**</span></span> | <span data-ttu-id="1ca73-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification?code={validationCode} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1ca73-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="1ca73-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="1ca73-128">URI parameter</span></span>

<span data-ttu-id="1ca73-129">Użyj następującego parametru zapytania, aby zaktualizować kwalifikację.</span><span class="sxs-lookup"><span data-stu-id="1ca73-129">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="1ca73-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1ca73-130">Name</span></span>                   | <span data-ttu-id="1ca73-131">Typ</span><span class="sxs-lookup"><span data-stu-id="1ca73-131">Type</span></span> | <span data-ttu-id="1ca73-132">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1ca73-132">Required</span></span> | <span data-ttu-id="1ca73-133">Opis</span><span class="sxs-lookup"><span data-stu-id="1ca73-133">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1ca73-134">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="1ca73-134">**customer-tenant-id**</span></span> | <span data-ttu-id="1ca73-135">GUID</span><span class="sxs-lookup"><span data-stu-id="1ca73-135">GUID</span></span> | <span data-ttu-id="1ca73-136">Tak</span><span class="sxs-lookup"><span data-stu-id="1ca73-136">Yes</span></span>      | <span data-ttu-id="1ca73-137">Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="1ca73-137">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="1ca73-138">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="1ca73-138">**validationCode**</span></span>     | <span data-ttu-id="1ca73-139">int</span><span class="sxs-lookup"><span data-stu-id="1ca73-139">int</span></span>  | <span data-ttu-id="1ca73-140">Nie</span><span class="sxs-lookup"><span data-stu-id="1ca73-140">No</span></span>       | <span data-ttu-id="1ca73-141">Wymagane tylko w przypadku Government Community Cloud.</span><span class="sxs-lookup"><span data-stu-id="1ca73-141">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="1ca73-142">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="1ca73-142">Request headers</span></span>

<span data-ttu-id="1ca73-143">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1ca73-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1ca73-144">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="1ca73-144">Request body</span></span>

<span data-ttu-id="1ca73-145">Wartość całkowita z [**wyliczenia CustomerQualification.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification)</span><span class="sxs-lookup"><span data-stu-id="1ca73-145">The integer value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="1ca73-146">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="1ca73-146">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a><span data-ttu-id="1ca73-147">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="1ca73-147">REST response</span></span>

<span data-ttu-id="1ca73-148">W przypadku powodzenia ta metoda zwraca zaktualizowaną właściwość [**Kwalifikacja**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="1ca73-148">If successful, this method returns updated [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1ca73-149">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1ca73-149">Response success and error codes</span></span>

<span data-ttu-id="1ca73-150">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="1ca73-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1ca73-151">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="1ca73-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1ca73-152">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1ca73-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1ca73-153">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1ca73-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## <a name="related-articles"></a><span data-ttu-id="1ca73-154">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="1ca73-154">Related articles</span></span>

- [<span data-ttu-id="1ca73-155">Pobieranie kwalifikacji klienta</span><span class="sxs-lookup"><span data-stu-id="1ca73-155">Get a customer's qualification</span></span>](./get-customer-qualification-synchronous.md)
- [<span data-ttu-id="1ca73-156">Pobieranie kodów weryfikacyjnych partnera</span><span class="sxs-lookup"><span data-stu-id="1ca73-156">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)
