---
title: Pobieranie metadanych umowy dla umowy klienta firmy Microsoft
description: W tym artykule wyjaśniono, jak uzyskać metadane umowy dla Umowa z Klientem Microsoft.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: 5c20b317edf16b159050884070683880cf7e45bb
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025724"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a><span data-ttu-id="6cfc3-103">Pobieranie metadanych umowy dla umowy klienta firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="6cfc3-103">Get agreement metadata for the Microsoft Customer Agreement</span></span>

<span data-ttu-id="6cfc3-104">**Dotyczy:** Partner Center</span><span class="sxs-lookup"><span data-stu-id="6cfc3-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="6cfc3-105">**Nie dotyczy:** Partner Center obsługiwane przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6cfc3-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6cfc3-106">Metadane umowy dla Umowa z Klientem Microsoft są obecnie obsługiwane Partner Center tylko w chmurze publicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6cfc3-106">Agreement metadata for Microsoft Customer Agreement is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="6cfc3-107">Musisz pobrać metadane umowy dla Umowa z Klientem Microsoft, aby można było:</span><span class="sxs-lookup"><span data-stu-id="6cfc3-107">You must retrieve the agreement metadata for the Microsoft Customer Agreement before you can:</span></span>

- [<span data-ttu-id="6cfc3-108">Potwierdź zgodę klienta na Umowa z Klientem Microsoft</span><span class="sxs-lookup"><span data-stu-id="6cfc3-108">Confirm a customer's acceptance of the Microsoft Customer Agreement</span></span>](./confirm-customer-consent-customer-agreement.md)
- [<span data-ttu-id="6cfc3-109">Pobieranie linku pobierania dla Umowa z Klientem Microsoft szablonu</span><span class="sxs-lookup"><span data-stu-id="6cfc3-109">Retrieve a download link for the Microsoft Customer Agreement template</span></span>](./download-customer-agreement-template.md)

## <a name="prerequisites"></a><span data-ttu-id="6cfc3-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6cfc3-110">Prerequisites</span></span>

- <span data-ttu-id="6cfc3-111">Jeśli używasz zestawu SDK platformy Partner Center .NET, wymagana jest wersja 1.14 lub nowsza.</span><span class="sxs-lookup"><span data-stu-id="6cfc3-111">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="6cfc3-112">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](./partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6cfc3-112">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="6cfc3-113">Ten scenariusz obsługuje tylko uwierzytelnianie app+user.</span><span class="sxs-lookup"><span data-stu-id="6cfc3-113">This scenario supports App+User authentication only.</span></span>

## <a name="net-version-114-or-newer"></a><span data-ttu-id="6cfc3-114">.NET (wersja 1.14 lub nowsza)</span><span class="sxs-lookup"><span data-stu-id="6cfc3-114">.NET (version 1.14 or newer)</span></span>

<span data-ttu-id="6cfc3-115">Aby pobrać metadane umowy dla Umowa z Klientem Microsoft:</span><span class="sxs-lookup"><span data-stu-id="6cfc3-115">To retrieve the agreement metadata for Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="6cfc3-116">Najpierw pobierz **kolekcję IAggregatePartner.AgreementDetails.**</span><span class="sxs-lookup"><span data-stu-id="6cfc3-116">First, retrieve the **IAggregatePartner.AgreementDetails** collection.</span></span>

2. <span data-ttu-id="6cfc3-117">Wywołaj **metodę ByAgreementType,** aby filtrować kolekcję w Umowa z Klientem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6cfc3-117">Call **ByAgreementType** method to filter the collection to Microsoft Customer Agreement.</span></span>

3. <span data-ttu-id="6cfc3-118">Na koniec wywołaj **metodę Get** lub **GetAsync.**</span><span class="sxs-lookup"><span data-stu-id="6cfc3-118">Finally, call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

<span data-ttu-id="6cfc3-119">Kompletny przykład można znaleźć w klasie [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) w projekcie [aplikacji testowej konsoli.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)</span><span class="sxs-lookup"><span data-stu-id="6cfc3-119">A complete sample can be found in the [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="6cfc3-120">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="6cfc3-120">REST request</span></span>

<span data-ttu-id="6cfc3-121">Aby pobrać metadane umowy dla Umowa z Klientem Microsoft:</span><span class="sxs-lookup"><span data-stu-id="6cfc3-121">To retrieve the agreement metadata for Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="6cfc3-122">Utwórz żądanie REST, aby pobrać [kolekcję AgreementMetaData.](./agreement-metadata-resources.md)</span><span class="sxs-lookup"><span data-stu-id="6cfc3-122">Create a REST request to retrieve the [AgreementMetaData](./agreement-metadata-resources.md) collection.</span></span>

2. <span data-ttu-id="6cfc3-123">Użyj **parametru zapytania agreementType,** aby zawęzać wynik tylko do Umowa z Klientem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6cfc3-123">Use the **agreementType** query parameter to scope the result to only the Microsoft Customer Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6cfc3-124">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="6cfc3-124">Request syntax</span></span>

| <span data-ttu-id="6cfc3-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="6cfc3-125">Method</span></span> | <span data-ttu-id="6cfc3-126">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="6cfc3-126">Request URI</span></span>                                                         |
|--------|---------------------------------------------------------------------|
| <span data-ttu-id="6cfc3-127">GET</span><span class="sxs-lookup"><span data-stu-id="6cfc3-127">GET</span></span>    | <span data-ttu-id="6cfc3-128">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6cfc3-128">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="6cfc3-129">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="6cfc3-129">URI parameters</span></span>

| <span data-ttu-id="6cfc3-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6cfc3-130">Name</span></span>                   | <span data-ttu-id="6cfc3-131">Typ</span><span class="sxs-lookup"><span data-stu-id="6cfc3-131">Type</span></span>     | <span data-ttu-id="6cfc3-132">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6cfc3-132">Required</span></span> | <span data-ttu-id="6cfc3-133">Opis</span><span class="sxs-lookup"><span data-stu-id="6cfc3-133">Description</span></span>                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| <span data-ttu-id="6cfc3-134">typ umowy</span><span class="sxs-lookup"><span data-stu-id="6cfc3-134">agreement-type</span></span> | <span data-ttu-id="6cfc3-135">ciąg</span><span class="sxs-lookup"><span data-stu-id="6cfc3-135">string</span></span> | <span data-ttu-id="6cfc3-136">Nie</span><span class="sxs-lookup"><span data-stu-id="6cfc3-136">No</span></span> | <span data-ttu-id="6cfc3-137">Użyj tego parametru, aby określać zakres odpowiedzi na zapytanie dla określonego typu umowy.</span><span class="sxs-lookup"><span data-stu-id="6cfc3-137">Use this parameter to scope the query response to specific agreement type.</span></span> <span data-ttu-id="6cfc3-138">Obsługiwane wartości to:</span><span class="sxs-lookup"><span data-stu-id="6cfc3-138">The supported values are:</span></span> <br/><br/><span data-ttu-id="6cfc3-139">**MicrosoftCloudAgreement,** który zawiera tylko metadane umowy typu *MicrosoftCloudAgreement*</span><span class="sxs-lookup"><span data-stu-id="6cfc3-139">**MicrosoftCloudAgreement** that includes agreement metadata only of the type *MicrosoftCloudAgreement*</span></span><br/><br/><span data-ttu-id="6cfc3-140">**MicrosoftCustomerAgreement,** który zawiera tylko metadane umowy typu *MicrosoftCustomerAgreement*.</span><span class="sxs-lookup"><span data-stu-id="6cfc3-140">**MicrosoftCustomerAgreement** that includes agreement metadata only of the type *MicrosoftCustomerAgreement*.</span></span><br/><br/><span data-ttu-id="6cfc3-141">**\**_ zwraca wszystkie metadane umowy. (Nie używaj _\* \* _, chyba że kod ma logikę środowiska uruchomieniowego niezbędną do obsługi nieznanych typów umów, ponieważ firma Microsoft może w dowolnym momencie wprowadzić metadane umowy z *nowymi typami umów). <br/> <br/> _* Uwaga:*\* Jeśli parametr URI nie zostanie określony, zapytanie domyślnie będzie mieć wartość **MicrosoftCloudAgreement** w celu zapewnienia zgodności z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="6cfc3-141">**\**_ that returns all agreement metadata. (Don't use _*\**_ unless your code has the necessary runtime logic to handle unfamiliar agreement types because Microsoft may introduce agreement metadata with new agreement types at any time.)<br/><br/> _\* Note:*\* If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="6cfc3-142">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="6cfc3-142">Request headers</span></span>

<span data-ttu-id="6cfc3-143">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6cfc3-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6cfc3-144">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="6cfc3-144">Request body</span></span>

<span data-ttu-id="6cfc3-145">Brak.</span><span class="sxs-lookup"><span data-stu-id="6cfc3-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6cfc3-146">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="6cfc3-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="6cfc3-147">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="6cfc3-147">REST response</span></span>

<span data-ttu-id="6cfc3-148">W przypadku powodzenia ta metoda zwraca kolekcję [ **zasobów AgreementMetaData**](./agreement-metadata-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="6cfc3-148">If successful, this method returns a collection of [**AgreementMetaData** resources](./agreement-metadata-resources.md) in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6cfc3-149">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6cfc3-149">Response success and error codes</span></span>

<span data-ttu-id="6cfc3-150">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="6cfc3-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="6cfc3-151">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="6cfc3-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6cfc3-152">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="6cfc3-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6cfc3-153">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6cfc3-153">Response example</span></span>

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
