---
title: Pobieranie potwierdzenia akceptacji przez klienta umowy klienta firmy Microsoft
description: W tym artykule wyjaśniono, jak uzyskać potwierdzenie akceptacji przez klienta umowy klienta firmy Microsoft.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 55f63311e7bb1857fdc6c4b3d68446674542ba98
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768166"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="4d33e-103">Pobieranie potwierdzenia akceptacji przez klienta umowy klienta firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="4d33e-103">Get confirmation of customer acceptance of Microsoft Customer Agreement</span></span>

<span data-ttu-id="4d33e-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="4d33e-104">**Applies to:**</span></span>

- <span data-ttu-id="4d33e-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="4d33e-105">Partner Center</span></span>

<span data-ttu-id="4d33e-106">Zasób **umowy** jest obecnie obsługiwany przez centrum partnerskie tylko w *chmurze publicznej firmy Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="4d33e-106">The **Agreement** resource is currently supported by Partner Center only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="4d33e-107">Ten zasób nie ma zastosowania do:</span><span class="sxs-lookup"><span data-stu-id="4d33e-107">This resource doesn't apply to:</span></span>

- <span data-ttu-id="4d33e-108">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="4d33e-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="4d33e-109">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="4d33e-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="4d33e-110">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="4d33e-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4d33e-111">W tym artykule wyjaśniono, jak można pobrać potwierdzenia akceptacji umowy klienta firmy Microsoft przez klienta.</span><span class="sxs-lookup"><span data-stu-id="4d33e-111">This article explains how you can retrieve confirmation(s) of a customer's acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d33e-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4d33e-112">Prerequisites</span></span>

- <span data-ttu-id="4d33e-113">W przypadku korzystania z zestawu SDK platformy .NET w programie Partner Center wymagany jest program w wersji 1,14 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="4d33e-113">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="4d33e-114">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](./partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4d33e-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="4d33e-115">Ten scenariusz obsługuje tylko uwierzytelnianie aplikacji i użytkowników.</span><span class="sxs-lookup"><span data-stu-id="4d33e-115">This scenario only supports App+User authentication.</span></span>

- <span data-ttu-id="4d33e-116">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4d33e-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4d33e-117">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="4d33e-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4d33e-118">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="4d33e-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4d33e-119">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="4d33e-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4d33e-120">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="4d33e-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4d33e-121">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4d33e-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="net"></a><span data-ttu-id="4d33e-122">.NET</span><span class="sxs-lookup"><span data-stu-id="4d33e-122">.NET</span></span>

<span data-ttu-id="4d33e-123">Aby pobrać potwierdzenia, które zostały wcześniej dostarczone przez klienta:</span><span class="sxs-lookup"><span data-stu-id="4d33e-123">To retrieve confirmation(s) of customer acceptance that was previously provided:</span></span>

- <span data-ttu-id="4d33e-124">Użyj metody **IAggregatePartner. Customers** i Wywołaj metodę **ById** z określonym identyfikatorem klienta.</span><span class="sxs-lookup"><span data-stu-id="4d33e-124">Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.</span></span>

- <span data-ttu-id="4d33e-125">Pobierz Właściwość **Agreements** i przefiltruj wyniki do umowy klienta firmy Microsoft przez wywołanie metody **ByAgreementType** .</span><span class="sxs-lookup"><span data-stu-id="4d33e-125">Fetch the **Agreements** property and filter the results to Microsoft Customer Agreement by calling **ByAgreementType** method.</span></span>

- <span data-ttu-id="4d33e-126">Wywoływanie metody **Get** lub **GetAsync** .</span><span class="sxs-lookup"><span data-stu-id="4d33e-126">Call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

<span data-ttu-id="4d33e-127">Pełny przykład można znaleźć w klasie [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) z projektu [aplikacji testowej konsoli](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .</span><span class="sxs-lookup"><span data-stu-id="4d33e-127">A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="4d33e-128">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="4d33e-128">REST request</span></span>

<span data-ttu-id="4d33e-129">Aby pobrać potwierdzenie przyjęcia przez klienta wcześniej dostarczonego:</span><span class="sxs-lookup"><span data-stu-id="4d33e-129">To retrieve confirmation of customer acceptance that was previously provided:</span></span>

1. <span data-ttu-id="4d33e-130">Utwórz żądanie REST w celu pobrania kolekcji [umów](./agreement-resources.md) dla klienta.</span><span class="sxs-lookup"><span data-stu-id="4d33e-130">Create a REST request to retrieve the [Agreements](./agreement-resources.md) collection for the customer.</span></span>

2. <span data-ttu-id="4d33e-131">Użyj parametru **querytype** , aby ograniczyć wyniki do umowy klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4d33e-131">Use the **agreementType** query parameter to scope the results to only the Microsoft Customer Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4d33e-132">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="4d33e-132">Request syntax</span></span>

<span data-ttu-id="4d33e-133">Użyj następującej składni żądania:</span><span class="sxs-lookup"><span data-stu-id="4d33e-133">Use the following request syntax:</span></span>

| <span data-ttu-id="4d33e-134">Metoda</span><span class="sxs-lookup"><span data-stu-id="4d33e-134">Method</span></span> | <span data-ttu-id="4d33e-135">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="4d33e-135">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4d33e-136">GET</span><span class="sxs-lookup"><span data-stu-id="4d33e-136">GET</span></span>    | <span data-ttu-id="4d33e-137">[*\{ baseURL \}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Agreements? agreementtype = {Agreement-Type} http/1.1</span><span class="sxs-lookup"><span data-stu-id="4d33e-137">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements?agreementType={agreement-type} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="4d33e-138">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="4d33e-138">URI parameters</span></span>

<span data-ttu-id="4d33e-139">Z żądaniem można użyć następujących parametrów URI:</span><span class="sxs-lookup"><span data-stu-id="4d33e-139">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="4d33e-140">Nazwa</span><span class="sxs-lookup"><span data-stu-id="4d33e-140">Name</span></span>             | <span data-ttu-id="4d33e-141">Typ</span><span class="sxs-lookup"><span data-stu-id="4d33e-141">Type</span></span> | <span data-ttu-id="4d33e-142">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4d33e-142">Required</span></span> | <span data-ttu-id="4d33e-143">Opis</span><span class="sxs-lookup"><span data-stu-id="4d33e-143">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="4d33e-144">Identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="4d33e-144">customer-tenant-id</span></span> | <span data-ttu-id="4d33e-145">GUID</span><span class="sxs-lookup"><span data-stu-id="4d33e-145">GUID</span></span> | <span data-ttu-id="4d33e-146">Tak</span><span class="sxs-lookup"><span data-stu-id="4d33e-146">Yes</span></span> | <span data-ttu-id="4d33e-147">Wartość jest identyfikatorem GUID w formacie **CustomerTenantId** , który umożliwia określenie klienta.</span><span class="sxs-lookup"><span data-stu-id="4d33e-147">The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer.</span></span> |
| <span data-ttu-id="4d33e-148">typ umowy</span><span class="sxs-lookup"><span data-stu-id="4d33e-148">agreement-type</span></span> | <span data-ttu-id="4d33e-149">ciąg</span><span class="sxs-lookup"><span data-stu-id="4d33e-149">string</span></span> | <span data-ttu-id="4d33e-150">Nie</span><span class="sxs-lookup"><span data-stu-id="4d33e-150">No</span></span> | <span data-ttu-id="4d33e-151">Ten parametr zwraca wszystkie metadane umowy.</span><span class="sxs-lookup"><span data-stu-id="4d33e-151">This parameter returns all agreement metadata.</span></span> <span data-ttu-id="4d33e-152">Użyj tego parametru, aby ograniczyć odpowiedź zapytania do określonego typu umowy.</span><span class="sxs-lookup"><span data-stu-id="4d33e-152">Use this parameter to scope the query response to specific agreement type.</span></span> <span data-ttu-id="4d33e-153">Obsługiwane są następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="4d33e-153">The supported values are:</span></span> <br/><br/> <span data-ttu-id="4d33e-154">**MicrosoftCloudAgreement** , który zawiera tylko metadane umów typu *MicrosoftCloudAgreement*.</span><span class="sxs-lookup"><span data-stu-id="4d33e-154">**MicrosoftCloudAgreement** that only includes agreement metadata of the type *MicrosoftCloudAgreement*.</span></span><br/><br/> <span data-ttu-id="4d33e-155">**MicrosoftCustomerAgreement** , który zawiera tylko metadane umów typu *MicrosoftCustomerAgreement*.</span><span class="sxs-lookup"><span data-stu-id="4d33e-155">**MicrosoftCustomerAgreement** that only includes agreement metadata of the type *MicrosoftCustomerAgreement*.</span></span><br/><br/> <span data-ttu-id="4d33e-156">**\*** zwraca wszystkie metadane umowy.</span><span class="sxs-lookup"><span data-stu-id="4d33e-156">**\*** that returns all agreement metadata.</span></span> <span data-ttu-id="4d33e-157">(Nie używaj **\*** , chyba że kod ma niezbędną logikę do obsługi nieoczekiwanych typów umowy).</span><span class="sxs-lookup"><span data-stu-id="4d33e-157">(Don't use **\*** unless your code has the necessary logic to handle unexpected agreement types.)</span></span><br/><br/> <span data-ttu-id="4d33e-158">**Uwaga:** Jeśli parametr URI nie jest określony, zapytanie jest domyślnie **MicrosoftCloudAgreement** w celu zapewnienia zgodności z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="4d33e-158">**Note:** If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.</span></span> <span data-ttu-id="4d33e-159">Firma Microsoft może w dowolnym momencie wprowadzać metadane umów z nowymi typami umów.</span><span class="sxs-lookup"><span data-stu-id="4d33e-159">Microsoft may introduce agreement metadata with new agreement types at any time.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="4d33e-160">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="4d33e-160">Request headers</span></span>

<span data-ttu-id="4d33e-161">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4d33e-161">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4d33e-162">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="4d33e-162">Request body</span></span>

<span data-ttu-id="4d33e-163">Brak.</span><span class="sxs-lookup"><span data-stu-id="4d33e-163">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4d33e-164">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="4d33e-164">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="4d33e-165">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="4d33e-165">REST response</span></span>

<span data-ttu-id="4d33e-166">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów **umowy** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="4d33e-166">If successful, this method returns a collection of **Agreement** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4d33e-167">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4d33e-167">Response success and error codes</span></span>

<span data-ttu-id="4d33e-168">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="4d33e-168">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="4d33e-169">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="4d33e-169">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4d33e-170">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4d33e-170">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4d33e-171">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4d33e-171">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 2,
    "items":
    [
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-26T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-27T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        }
    ]
}
```
