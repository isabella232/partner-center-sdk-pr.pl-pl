---
title: Pobieranie metadanych umowy dla umowy klienta firmy Microsoft
description: W tym artykule wyjaśniono, jak uzyskać metadane umów dla umowy klienta firmy Microsoft.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: c3ebecc51859c9d2240d319d823f7e555eaecc27
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768162"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a><span data-ttu-id="4caa1-103">Pobieranie metadanych umowy dla umowy klienta firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="4caa1-103">Get agreement metadata for the Microsoft Customer Agreement</span></span>

<span data-ttu-id="4caa1-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="4caa1-104">**Applies to:**</span></span>

- <span data-ttu-id="4caa1-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="4caa1-105">Partner Center</span></span>

<span data-ttu-id="4caa1-106">Metadane umowy dla umowy klienta firmy Microsoft są obecnie obsługiwane przez centrum partnerskie tylko w *chmurze publicznej firmy Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="4caa1-106">Agreement metadata for Microsoft Customer Agreement is currently supported by Partner Center only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="4caa1-107">Nie dotyczy:</span><span class="sxs-lookup"><span data-stu-id="4caa1-107">It doesn't apply to:</span></span>

- <span data-ttu-id="4caa1-108">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="4caa1-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="4caa1-109">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="4caa1-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="4caa1-110">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="4caa1-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4caa1-111">Przed rozpoczęciem można pobrać metadane umów licencyjnych firmy Microsoft:</span><span class="sxs-lookup"><span data-stu-id="4caa1-111">You must retrieve the agreement metadata for the Microsoft Customer Agreement before you can:</span></span>

- [<span data-ttu-id="4caa1-112">Potwierdzanie akceptacji umowy klienta firmy Microsoft przez klienta</span><span class="sxs-lookup"><span data-stu-id="4caa1-112">Confirm a customer's acceptance of the Microsoft Customer Agreement</span></span>](./confirm-customer-consent-customer-agreement.md)
- [<span data-ttu-id="4caa1-113">Pobierz link pobierania dla szablonu umowy klienta firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="4caa1-113">Retrieve a download link for the Microsoft Customer Agreement template</span></span>](./download-customer-agreement-template.md)

## <a name="prerequisites"></a><span data-ttu-id="4caa1-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4caa1-114">Prerequisites</span></span>

- <span data-ttu-id="4caa1-115">W przypadku korzystania z zestawu SDK platformy .NET w programie Partner Center wymagany jest program w wersji 1,14 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="4caa1-115">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="4caa1-116">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](./partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4caa1-116">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="4caa1-117">Ten scenariusz obsługuje tylko uwierzytelnianie aplikacji i użytkowników.</span><span class="sxs-lookup"><span data-stu-id="4caa1-117">This scenario supports App+User authentication only.</span></span>

## <a name="net-version-114-or-newer"></a><span data-ttu-id="4caa1-118">.NET (wersja 1,14 lub nowsza)</span><span class="sxs-lookup"><span data-stu-id="4caa1-118">.NET (version 1.14 or newer)</span></span>

<span data-ttu-id="4caa1-119">Aby pobrać metadane umowy dla umowy klienta firmy Microsoft:</span><span class="sxs-lookup"><span data-stu-id="4caa1-119">To retrieve the agreement metadata for Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="4caa1-120">Najpierw pobierz kolekcję **IAggregatePartner. AgreementDetails** .</span><span class="sxs-lookup"><span data-stu-id="4caa1-120">First, retrieve the **IAggregatePartner.AgreementDetails** collection.</span></span>

2. <span data-ttu-id="4caa1-121">Wywołaj metodę **ByAgreementType** , aby odfiltrować kolekcję do umowy klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4caa1-121">Call **ByAgreementType** method to filter the collection to Microsoft Customer Agreement.</span></span>

3. <span data-ttu-id="4caa1-122">Na koniec Wywołaj metodę **Get** lub **GetAsync** .</span><span class="sxs-lookup"><span data-stu-id="4caa1-122">Finally, call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

<span data-ttu-id="4caa1-123">Pełny przykład można znaleźć w klasie [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) z projektu [aplikacji testowej konsoli](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .</span><span class="sxs-lookup"><span data-stu-id="4caa1-123">A complete sample can be found in the [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="4caa1-124">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="4caa1-124">REST request</span></span>

<span data-ttu-id="4caa1-125">Aby pobrać metadane umowy dla umowy klienta firmy Microsoft:</span><span class="sxs-lookup"><span data-stu-id="4caa1-125">To retrieve the agreement metadata for Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="4caa1-126">Utwórz żądanie REST w celu pobrania kolekcji [AgreementMetaData](./agreement-metadata-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="4caa1-126">Create a REST request to retrieve the [AgreementMetaData](./agreement-metadata-resources.md) collection.</span></span>

2. <span data-ttu-id="4caa1-127">Użyj parametru **querytype** , aby ograniczyć wynik do umowy klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4caa1-127">Use the **agreementType** query parameter to scope the result to only the Microsoft Customer Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4caa1-128">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="4caa1-128">Request syntax</span></span>

| <span data-ttu-id="4caa1-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="4caa1-129">Method</span></span> | <span data-ttu-id="4caa1-130">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="4caa1-130">Request URI</span></span>                                                         |
|--------|---------------------------------------------------------------------|
| <span data-ttu-id="4caa1-131">GET</span><span class="sxs-lookup"><span data-stu-id="4caa1-131">GET</span></span>    | <span data-ttu-id="4caa1-132">[*\{ baseURL \}*](partner-center-rest-urls.md)/V1/Agreements? agreementtype = {Agreement-Type} http/1.1</span><span class="sxs-lookup"><span data-stu-id="4caa1-132">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="4caa1-133">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="4caa1-133">URI parameters</span></span>

| <span data-ttu-id="4caa1-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="4caa1-134">Name</span></span>                   | <span data-ttu-id="4caa1-135">Typ</span><span class="sxs-lookup"><span data-stu-id="4caa1-135">Type</span></span>     | <span data-ttu-id="4caa1-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4caa1-136">Required</span></span> | <span data-ttu-id="4caa1-137">Opis</span><span class="sxs-lookup"><span data-stu-id="4caa1-137">Description</span></span>                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| <span data-ttu-id="4caa1-138">typ umowy</span><span class="sxs-lookup"><span data-stu-id="4caa1-138">agreement-type</span></span> | <span data-ttu-id="4caa1-139">ciąg</span><span class="sxs-lookup"><span data-stu-id="4caa1-139">string</span></span> | <span data-ttu-id="4caa1-140">Nie</span><span class="sxs-lookup"><span data-stu-id="4caa1-140">No</span></span> | <span data-ttu-id="4caa1-141">Użyj tego parametru, aby ograniczyć odpowiedź zapytania do określonego typu umowy.</span><span class="sxs-lookup"><span data-stu-id="4caa1-141">Use this parameter to scope the query response to specific agreement type.</span></span> <span data-ttu-id="4caa1-142">Obsługiwane są następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="4caa1-142">The supported values are:</span></span> <br/><br/><span data-ttu-id="4caa1-143">**MicrosoftCloudAgreement** obejmujący metadane umów tylko typu *MicrosoftCloudAgreement*</span><span class="sxs-lookup"><span data-stu-id="4caa1-143">**MicrosoftCloudAgreement** that includes agreement metadata only of the type *MicrosoftCloudAgreement*</span></span><br/><br/><span data-ttu-id="4caa1-144">**MicrosoftCustomerAgreement** obejmujący metadane umów tylko typu *MicrosoftCustomerAgreement*.</span><span class="sxs-lookup"><span data-stu-id="4caa1-144">**MicrosoftCustomerAgreement** that includes agreement metadata only of the type *MicrosoftCustomerAgreement*.</span></span><br/><br/><span data-ttu-id="4caa1-145">**\*** zwraca wszystkie metadane umowy.</span><span class="sxs-lookup"><span data-stu-id="4caa1-145">**\*** that returns all agreement metadata.</span></span> <span data-ttu-id="4caa1-146">(Nie używaj **\*** , chyba że Twój kod ma niezbędną logikę uruchomieniową do obsługi nieznanych typów umów, ponieważ firma Microsoft może w dowolnym czasie wprowadzić metadane umów z nowymi typami umów).</span><span class="sxs-lookup"><span data-stu-id="4caa1-146">(Don't use **\*** unless your code has the necessary runtime logic to handle unfamiliar agreement types because Microsoft may introduce agreement metadata with new agreement types at any time.)</span></span><br/><br/> <span data-ttu-id="4caa1-147">**Uwaga:** Jeśli parametr URI nie jest określony, zapytanie jest domyślnie **MicrosoftCloudAgreement** w celu zapewnienia zgodności z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="4caa1-147">**Note:** If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="4caa1-148">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="4caa1-148">Request headers</span></span>

<span data-ttu-id="4caa1-149">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4caa1-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4caa1-150">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="4caa1-150">Request body</span></span>

<span data-ttu-id="4caa1-151">Brak.</span><span class="sxs-lookup"><span data-stu-id="4caa1-151">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4caa1-152">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="4caa1-152">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="4caa1-153">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="4caa1-153">REST response</span></span>

<span data-ttu-id="4caa1-154">Jeśli to się powiedzie, ta metoda zwraca kolekcję [zasobów **AgreementMetaData**](./agreement-metadata-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="4caa1-154">If successful, this method returns a collection of [**AgreementMetaData** resources](./agreement-metadata-resources.md) in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4caa1-155">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4caa1-155">Response success and error codes</span></span>

<span data-ttu-id="4caa1-156">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="4caa1-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="4caa1-157">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="4caa1-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4caa1-158">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4caa1-158">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4caa1-159">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4caa1-159">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 1,
    "items": [
        {
            "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
            "agreementType": "MicrosoftCustomerAgreement",
            "agreementLink": "https://aka.ms/customeragreement",
            "versionRank": 0
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
