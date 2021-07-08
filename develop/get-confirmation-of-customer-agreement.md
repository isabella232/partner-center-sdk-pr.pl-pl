---
title: Pobieranie potwierdzenia akceptacji przez klienta umowy klienta firmy Microsoft
description: W tym artykule wyjaśniono, jak uzyskać potwierdzenie akceptacji przez klienta Umowa z Klientem Microsoft.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 3668a5e510effb533cade311f52513b9a81d40af
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760542"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="ec0b5-103">Pobieranie potwierdzenia akceptacji przez klienta umowy klienta firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="ec0b5-103">Get confirmation of customer acceptance of Microsoft Customer Agreement</span></span>

<span data-ttu-id="ec0b5-104">**Dotyczy:** Partner Center</span><span class="sxs-lookup"><span data-stu-id="ec0b5-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="ec0b5-105">**Nie dotyczy:** Partner Center obsługiwane przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ec0b5-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ec0b5-106">Zasób **Umowy** jest obecnie obsługiwany przez Partner Center tylko w chmurze publicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-106">The **Agreement** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="ec0b5-107">W tym artykule wyjaśniono, jak można pobrać potwierdzenia akceptacji przez klienta Umowa z Klientem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-107">This article explains how you can retrieve confirmation(s) of a customer's acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec0b5-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ec0b5-108">Prerequisites</span></span>

- <span data-ttu-id="ec0b5-109">Jeśli używasz zestawu SDK platformy Partner Center .NET, wymagana jest wersja 1.14 lub nowsza.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-109">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="ec0b5-110">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](./partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ec0b5-110">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="ec0b5-111">Ten scenariusz obsługuje tylko uwierzytelnianie app+user.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-111">This scenario only supports App+User authentication.</span></span>

- <span data-ttu-id="ec0b5-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ec0b5-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ec0b5-113">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="ec0b5-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ec0b5-114">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="ec0b5-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ec0b5-115">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ec0b5-116">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ec0b5-117">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ec0b5-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="net"></a><span data-ttu-id="ec0b5-118">.NET</span><span class="sxs-lookup"><span data-stu-id="ec0b5-118">.NET</span></span>

<span data-ttu-id="ec0b5-119">Aby pobrać wcześniej podane potwierdzenia akceptacji przez klienta:</span><span class="sxs-lookup"><span data-stu-id="ec0b5-119">To retrieve confirmation(s) of customer acceptance that was previously provided:</span></span>

- <span data-ttu-id="ec0b5-120">Użyj **kolekcji IAggregatePartner.Customers** i wywołaj metodę **ById** z określonym identyfikatorem klienta.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-120">Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.</span></span>

- <span data-ttu-id="ec0b5-121">Pobierz właściwość **Agreements** i przefiltruj wyniki, aby Umowa z Klientem Microsoft przez wywołanie **metody ByAgreementType.**</span><span class="sxs-lookup"><span data-stu-id="ec0b5-121">Fetch the **Agreements** property and filter the results to Microsoft Customer Agreement by calling **ByAgreementType** method.</span></span>

- <span data-ttu-id="ec0b5-122">Wywołaj **metodę Get** lub **GetAsync.**</span><span class="sxs-lookup"><span data-stu-id="ec0b5-122">Call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

<span data-ttu-id="ec0b5-123">Kompletny przykład można znaleźć w klasie [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) w projekcie [aplikacji testowej konsoli.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)</span><span class="sxs-lookup"><span data-stu-id="ec0b5-123">A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="ec0b5-124">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="ec0b5-124">REST request</span></span>

<span data-ttu-id="ec0b5-125">Aby pobrać potwierdzenie akceptacji klienta, które zostało podane wcześniej:</span><span class="sxs-lookup"><span data-stu-id="ec0b5-125">To retrieve confirmation of customer acceptance that was previously provided:</span></span>

1. <span data-ttu-id="ec0b5-126">Utwórz żądanie REST, aby pobrać [kolekcję Umowy](./agreement-resources.md) dla klienta.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-126">Create a REST request to retrieve the [Agreements](./agreement-resources.md) collection for the customer.</span></span>

2. <span data-ttu-id="ec0b5-127">Użyj **parametru zapytania agreementType,** aby określać zakres wyników tylko do Umowa z Klientem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-127">Use the **agreementType** query parameter to scope the results to only the Microsoft Customer Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ec0b5-128">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="ec0b5-128">Request syntax</span></span>

<span data-ttu-id="ec0b5-129">Użyj następującej składni żądania:</span><span class="sxs-lookup"><span data-stu-id="ec0b5-129">Use the following request syntax:</span></span>

| <span data-ttu-id="ec0b5-130">Metoda</span><span class="sxs-lookup"><span data-stu-id="ec0b5-130">Method</span></span> | <span data-ttu-id="ec0b5-131">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="ec0b5-131">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ec0b5-132">GET</span><span class="sxs-lookup"><span data-stu-id="ec0b5-132">GET</span></span>    | <span data-ttu-id="ec0b5-133">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements?agreementType={agreement-type} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ec0b5-133">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements?agreementType={agreement-type} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="ec0b5-134">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="ec0b5-134">URI parameters</span></span>

<span data-ttu-id="ec0b5-135">W żądaniu można użyć następujących parametrów URI:</span><span class="sxs-lookup"><span data-stu-id="ec0b5-135">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="ec0b5-136">Nazwa</span><span class="sxs-lookup"><span data-stu-id="ec0b5-136">Name</span></span>             | <span data-ttu-id="ec0b5-137">Typ</span><span class="sxs-lookup"><span data-stu-id="ec0b5-137">Type</span></span> | <span data-ttu-id="ec0b5-138">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ec0b5-138">Required</span></span> | <span data-ttu-id="ec0b5-139">Opis</span><span class="sxs-lookup"><span data-stu-id="ec0b5-139">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="ec0b5-140">identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="ec0b5-140">customer-tenant-id</span></span> | <span data-ttu-id="ec0b5-141">GUID</span><span class="sxs-lookup"><span data-stu-id="ec0b5-141">GUID</span></span> | <span data-ttu-id="ec0b5-142">Tak</span><span class="sxs-lookup"><span data-stu-id="ec0b5-142">Yes</span></span> | <span data-ttu-id="ec0b5-143">Wartość to identyfikator GUID sformatowany **jako CustomerTenantId,** który umożliwia określenie klienta.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-143">The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer.</span></span> |
| <span data-ttu-id="ec0b5-144">typ umowy</span><span class="sxs-lookup"><span data-stu-id="ec0b5-144">agreement-type</span></span> | <span data-ttu-id="ec0b5-145">ciąg</span><span class="sxs-lookup"><span data-stu-id="ec0b5-145">string</span></span> | <span data-ttu-id="ec0b5-146">Nie</span><span class="sxs-lookup"><span data-stu-id="ec0b5-146">No</span></span> | <span data-ttu-id="ec0b5-147">Ten parametr zwraca wszystkie metadane umowy.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-147">This parameter returns all agreement metadata.</span></span> <span data-ttu-id="ec0b5-148">Użyj tego parametru, aby określać zakres odpowiedzi na zapytanie dla określonego typu umowy.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-148">Use this parameter to scope the query response to specific agreement type.</span></span> <span data-ttu-id="ec0b5-149">Obsługiwane wartości to:</span><span class="sxs-lookup"><span data-stu-id="ec0b5-149">The supported values are:</span></span> <br/><br/> <span data-ttu-id="ec0b5-150">**MicrosoftCloudAgreement,** który zawiera tylko metadane umowy typu *MicrosoftCloudAgreement*.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-150">**MicrosoftCloudAgreement** that only includes agreement metadata of the type *MicrosoftCloudAgreement*.</span></span><br/><br/> <span data-ttu-id="ec0b5-151">**MicrosoftCustomerAgreement,** który zawiera tylko metadane umowy typu *MicrosoftCustomerAgreement*.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-151">**MicrosoftCustomerAgreement** that only includes agreement metadata of the type *MicrosoftCustomerAgreement*.</span></span><br/><br/> <span data-ttu-id="ec0b5-152">**\**_ zwraca wszystkie metadane umowy. (Nie używaj _\* \* \*_, chyba że kod ma logikę niezbędną do obsługi nieoczekiwanych typów umów). <br/> <br/> _\* Uwaga:*\* Jeśli parametr URI nie zostanie określony, zapytanie domyślnie będzie mieć wartość **MicrosoftCloudAgreement** w celu zapewnienia zgodności z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-152">**\**_ that returns all agreement metadata. (Don't use _*\**_ unless your code has the necessary logic to handle unexpected agreement types.)<br/><br/> _\* Note:*\* If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.</span></span> <span data-ttu-id="ec0b5-153">Firma Microsoft może wprowadzać metadane umowy z nowymi typami umów w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-153">Microsoft may introduce agreement metadata with new agreement types at any time.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="ec0b5-154">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="ec0b5-154">Request headers</span></span>

<span data-ttu-id="ec0b5-155">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ec0b5-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ec0b5-156">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="ec0b5-156">Request body</span></span>

<span data-ttu-id="ec0b5-157">Brak.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ec0b5-158">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="ec0b5-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="ec0b5-159">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="ec0b5-159">REST response</span></span>

<span data-ttu-id="ec0b5-160">W przypadku powodzenia ta metoda zwraca kolekcję zasobów **umowy** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-160">If successful, this method returns a collection of **Agreement** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ec0b5-161">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ec0b5-161">Response success and error codes</span></span>

<span data-ttu-id="ec0b5-162">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="ec0b5-163">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ec0b5-164">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ec0b5-164">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ec0b5-165">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ec0b5-165">Response example</span></span>

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
