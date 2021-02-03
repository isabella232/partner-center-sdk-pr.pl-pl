---
title: Aktualizowanie kwalifikacji klienta
description: Dowiedz się, jak aktualizować kwalifikacje klienta za pośrednictwem synchronicznych ekranów lub przed sprawdzeniem, w tym adres skojarzony z profilem.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 7faab68d20c698f5b040a76f4776dbdf14180640
ms.sourcegitcommit: 0c98496e972aebe10eba23822aa229125bfc035d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770204"
---
# <a name="update-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="dfe33-103">Aktualizowanie kwalifikacji klienta poprzez weryfikację synchroniczną</span><span class="sxs-lookup"><span data-stu-id="dfe33-103">Update a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="dfe33-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="dfe33-104">**Applies To**</span></span>

- <span data-ttu-id="dfe33-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="dfe33-105">Partner Center</span></span>

<span data-ttu-id="dfe33-106">Dowiedz się, jak aktualizować kwalifikacje klienta synchronicznie za pośrednictwem interfejsów API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="dfe33-106">Learn how to update a customer's qualifications synchronously via Partner Center APIs.</span></span> <span data-ttu-id="dfe33-107">Aby dowiedzieć się, jak to zrobić asynchronicznie, zobacz [Aktualizowanie kwalifikacji klienta za pośrednictwem walidacji asynchronicznej](update-customer-qualification-asynchronous.md).</span><span class="sxs-lookup"><span data-stu-id="dfe33-107">To learn how to do this asynchronously, see [Update a customer's qualification via asynchronous validation](update-customer-qualification-asynchronous.md).</span></span>

<span data-ttu-id="dfe33-108">Partner może zaktualizować kwalifikację klienta pod kątem "edukacji" lub "GovernmentCommunityCloud".</span><span class="sxs-lookup"><span data-stu-id="dfe33-108">A partner can update a customer's qualification to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="dfe33-109">Nie można ustawić innych wartości, "none" i "non profit".</span><span class="sxs-lookup"><span data-stu-id="dfe33-109">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dfe33-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dfe33-110">Prerequisites</span></span>

- <span data-ttu-id="dfe33-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="dfe33-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="dfe33-112">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dfe33-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="dfe33-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="dfe33-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="dfe33-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="dfe33-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="dfe33-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="dfe33-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="dfe33-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="dfe33-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="dfe33-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="dfe33-117">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="dfe33-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="dfe33-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="dfe33-119">C\#</span><span class="sxs-lookup"><span data-stu-id="dfe33-119">C\#</span></span>

<span data-ttu-id="dfe33-120">Aby zaktualizować kwalifikację klienta do "edukacji", wywołaj polecenie **[Update/dotnet/API/Microsoft. Store. partnercenter. kwalifikacja. icustomerqualification. Update)** na istniejącym  [**kliencie**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).</span><span class="sxs-lookup"><span data-stu-id="dfe33-120">To update a customer's qualification to "Education", call **[Update/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** on an existing  [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).</span></span>

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

<span data-ttu-id="dfe33-121">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="dfe33-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="dfe33-122">**Project**: PartnerSDK. FeatureSamples **Klasa**: CustomerQualificationOperations.cs</span><span class="sxs-lookup"><span data-stu-id="dfe33-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerQualificationOperations.cs</span></span>

<span data-ttu-id="dfe33-123">Aby zaktualizować kwalifikację klienta do **GovernmentCommunityCloud** na istniejącym kliencie bez kwalifikacji.</span><span class="sxs-lookup"><span data-stu-id="dfe33-123">To update a customer's qualification to **GovernmentCommunityCloud** on an existing customer without a qualification.</span></span>  <span data-ttu-id="dfe33-124">Partner jest również zobowiązany do uwzględnienia [**ValidationCode**](utility-resources.md#validationcode)klienta.</span><span class="sxs-lookup"><span data-stu-id="dfe33-124">The partner is also are required to include the customer's [**ValidationCode**](utility-resources.md#validationcode).</span></span>

``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```

## <a name="rest-request"></a><span data-ttu-id="dfe33-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="dfe33-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dfe33-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="dfe33-126">Request syntax</span></span>

| <span data-ttu-id="dfe33-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="dfe33-127">Method</span></span>  | <span data-ttu-id="dfe33-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="dfe33-128">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="dfe33-129">**PUT**</span><span class="sxs-lookup"><span data-stu-id="dfe33-129">**PUT**</span></span> | <span data-ttu-id="dfe33-130">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer_ID}/Qualification? Code = {VALIDATIONCODE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="dfe33-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="dfe33-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="dfe33-131">URI parameter</span></span>

<span data-ttu-id="dfe33-132">Użyj następującego parametru zapytania, aby zaktualizować kwalifikacje.</span><span class="sxs-lookup"><span data-stu-id="dfe33-132">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="dfe33-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dfe33-133">Name</span></span>                   | <span data-ttu-id="dfe33-134">Typ</span><span class="sxs-lookup"><span data-stu-id="dfe33-134">Type</span></span> | <span data-ttu-id="dfe33-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dfe33-135">Required</span></span> | <span data-ttu-id="dfe33-136">Opis</span><span class="sxs-lookup"><span data-stu-id="dfe33-136">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="dfe33-137">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="dfe33-137">**customer-tenant-id**</span></span> | <span data-ttu-id="dfe33-138">GUID</span><span class="sxs-lookup"><span data-stu-id="dfe33-138">GUID</span></span> | <span data-ttu-id="dfe33-139">Tak</span><span class="sxs-lookup"><span data-stu-id="dfe33-139">Yes</span></span>      | <span data-ttu-id="dfe33-140">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="dfe33-140">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="dfe33-141">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="dfe33-141">**validationCode**</span></span>     | <span data-ttu-id="dfe33-142">int</span><span class="sxs-lookup"><span data-stu-id="dfe33-142">int</span></span>  | <span data-ttu-id="dfe33-143">Nie</span><span class="sxs-lookup"><span data-stu-id="dfe33-143">No</span></span>       | <span data-ttu-id="dfe33-144">Wymagany tylko w przypadku chmury społecznościowej dla instytucji rządowych.</span><span class="sxs-lookup"><span data-stu-id="dfe33-144">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="dfe33-145">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="dfe33-145">Request headers</span></span>

<span data-ttu-id="dfe33-146">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="dfe33-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="dfe33-147">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="dfe33-147">Request body</span></span>

<span data-ttu-id="dfe33-148">Wartość całkowita z wyliczenia [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) .</span><span class="sxs-lookup"><span data-stu-id="dfe33-148">The integer value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="dfe33-149">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="dfe33-149">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a><span data-ttu-id="dfe33-150">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="dfe33-150">REST response</span></span>

<span data-ttu-id="dfe33-151">Jeśli to się powiedzie, ta metoda zwraca zaktualizowaną Właściwość [**kwalifikacji**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="dfe33-151">If successful, this method returns updated [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dfe33-152">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="dfe33-152">Response success and error codes</span></span>

<span data-ttu-id="dfe33-153">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="dfe33-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dfe33-154">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="dfe33-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="dfe33-155">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="dfe33-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="dfe33-156">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="dfe33-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## <a name="related-articles"></a><span data-ttu-id="dfe33-157">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="dfe33-157">Related articles</span></span>

- [<span data-ttu-id="dfe33-158">Pobieranie kwalifikacji klienta</span><span class="sxs-lookup"><span data-stu-id="dfe33-158">Get a customer's qualification</span></span>](get-a-customer-s-qualification.md)
- [<span data-ttu-id="dfe33-159">Pobieranie kodów weryfikacyjnych partnera</span><span class="sxs-lookup"><span data-stu-id="dfe33-159">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)
