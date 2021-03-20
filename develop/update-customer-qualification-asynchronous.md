---
title: Aktualizowanie kwalifikacji klienta
description: Dowiedz się, jak zaktualizować kwalifikacje klienta za pośrednictwem funkcji osłaniania asynchronicznego lub przed sprawdzeniem, w tym adres skojarzony z profilem.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 703585eeaba93b6d7a510a3174a78a28f22e1510
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711937"
---
# <a name="update-a-customers-qualifications-asynchronously"></a><span data-ttu-id="67986-103">Aktualizowanie kwalifikacji klienta asynchronicznie</span><span class="sxs-lookup"><span data-stu-id="67986-103">Update a customer's qualifications asynchronously</span></span>

<span data-ttu-id="67986-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="67986-104">**Applies To**</span></span>

- <span data-ttu-id="67986-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="67986-105">Partner Center</span></span>

<span data-ttu-id="67986-106">Dowiedz się, jak aktualizować kwalifikacje klienta asynchronicznie za pośrednictwem interfejsów API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="67986-106">Learn how to update a customer's qualifications asynchronously via Partner Center APIs.</span></span> <span data-ttu-id="67986-107">Aby dowiedzieć się, jak to zrobić synchronicznie, zobacz [Aktualizowanie kwalifikacji klienta za pośrednictwem walidacji synchronicznej](update-customer-qualification-synchronous.md).</span><span class="sxs-lookup"><span data-stu-id="67986-107">To learn how to do this synchronously, see [Update a customer's qualification via synchronous validation](update-customer-qualification-synchronous.md).</span></span>

<span data-ttu-id="67986-108">Partner może zaktualizować kwalifikacje klienta asynchronicznie do "Education" lub "GovernmentCommunityCloud".</span><span class="sxs-lookup"><span data-stu-id="67986-108">A partner can update a customer's qualifications asynchronously to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="67986-109">Nie można ustawić innych wartości, "none" i "non profit".</span><span class="sxs-lookup"><span data-stu-id="67986-109">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67986-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="67986-110">Prerequisites</span></span>

- <span data-ttu-id="67986-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="67986-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="67986-112">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="67986-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="67986-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="67986-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="67986-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="67986-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="67986-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="67986-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="67986-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="67986-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="67986-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="67986-117">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="67986-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="67986-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="67986-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="67986-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="67986-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="67986-120">Request syntax</span></span>

| <span data-ttu-id="67986-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="67986-121">Method</span></span>  | <span data-ttu-id="67986-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="67986-122">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="67986-123">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="67986-123">**POST**</span></span> | <span data-ttu-id="67986-124">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer_ID}/Qualifications? Code = {VALIDATIONCODE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="67986-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="67986-125">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="67986-125">URI parameter</span></span>

<span data-ttu-id="67986-126">Użyj następującego parametru zapytania, aby zaktualizować kwalifikacje.</span><span class="sxs-lookup"><span data-stu-id="67986-126">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="67986-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="67986-127">Name</span></span>                   | <span data-ttu-id="67986-128">Typ</span><span class="sxs-lookup"><span data-stu-id="67986-128">Type</span></span> | <span data-ttu-id="67986-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="67986-129">Required</span></span> | <span data-ttu-id="67986-130">Opis</span><span class="sxs-lookup"><span data-stu-id="67986-130">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="67986-131">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="67986-131">**customer-tenant-id**</span></span> | <span data-ttu-id="67986-132">GUID</span><span class="sxs-lookup"><span data-stu-id="67986-132">GUID</span></span> | <span data-ttu-id="67986-133">Tak</span><span class="sxs-lookup"><span data-stu-id="67986-133">Yes</span></span>      | <span data-ttu-id="67986-134">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="67986-134">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="67986-135">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="67986-135">**validationCode**</span></span>     | <span data-ttu-id="67986-136">int</span><span class="sxs-lookup"><span data-stu-id="67986-136">int</span></span>  | <span data-ttu-id="67986-137">Nie</span><span class="sxs-lookup"><span data-stu-id="67986-137">No</span></span>       | <span data-ttu-id="67986-138">Wymagany tylko w przypadku chmury społecznościowej dla instytucji rządowych.</span><span class="sxs-lookup"><span data-stu-id="67986-138">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="67986-139">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="67986-139">Request headers</span></span>

<span data-ttu-id="67986-140">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="67986-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="67986-141">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="67986-141">Request body</span></span>

<span data-ttu-id="67986-142">Wartość całkowita z wyliczenia [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) .</span><span class="sxs-lookup"><span data-stu-id="67986-142">The integer value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="67986-143">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="67986-143">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a><span data-ttu-id="67986-144">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="67986-144">REST response</span></span>

<span data-ttu-id="67986-145">Jeśli to się powiedzie, metoda zwraca obiekt kwalifikacji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="67986-145">If successful, this method returns a qualifications object in the response body.</span></span> <span data-ttu-id="67986-146">Poniżej znajduje się przykład wywołania **post** na kliencie (z wcześniejszą kwalifikacją dla **braku**) z kwalifikacją **edukacyjną** .</span><span class="sxs-lookup"><span data-stu-id="67986-146">Below is an example of the **POST** call on a customer (with a previous qualification of **None**) with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="67986-147">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="67986-147">Response success and error codes</span></span>

<span data-ttu-id="67986-148">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="67986-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="67986-149">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="67986-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="67986-150">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="67986-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="67986-151">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="67986-151">Response example</span></span>

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

## <a name="related-articles"></a><span data-ttu-id="67986-152">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="67986-152">Related articles</span></span>

- [<span data-ttu-id="67986-153">Pobierz kwalifikacje klienta</span><span class="sxs-lookup"><span data-stu-id="67986-153">Get a customer's qualifications</span></span>](./get-customer-qualification-asynchronous.md)
- [<span data-ttu-id="67986-154">Pobieranie kodów weryfikacyjnych partnera</span><span class="sxs-lookup"><span data-stu-id="67986-154">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)