---
title: Pobieranie metadanych umowy dla umowy dotyczącej platformy Microsoft Cloud
description: W tym artykule wyjaśniono, jak uzyskać metadane umów dla Microsoft Cloud umowy.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c6a404eb38c4c31d3e69bb598872b932d8985529
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768049"
---
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a><span data-ttu-id="9c58d-103">Pobieranie metadanych umowy dla umowy dotyczącej platformy Microsoft Cloud</span><span class="sxs-lookup"><span data-stu-id="9c58d-103">Get agreement metadata for Microsoft Cloud Agreement</span></span>

<span data-ttu-id="9c58d-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="9c58d-104">**Applies To**</span></span>

- <span data-ttu-id="9c58d-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="9c58d-105">Partner Center</span></span>

> [!NOTE]
> <span data-ttu-id="9c58d-106">Zasób **AgreementMetaData** jest obecnie obsługiwany przez centrum partnerskie tylko w chmurze publicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9c58d-106">The **AgreementMetaData** resource is currently supported by Partner Center in the Microsoft public cloud only.</span></span> <span data-ttu-id="9c58d-107">Nie dotyczy:</span><span class="sxs-lookup"><span data-stu-id="9c58d-107">It isn't applicable to:</span></span>
> - <span data-ttu-id="9c58d-108">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="9c58d-108">Partner Center operated by 21Vianet</span></span>
> - <span data-ttu-id="9c58d-109">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="9c58d-109">Partner Center for Microsoft Cloud Germany</span></span>
> - <span data-ttu-id="9c58d-110">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9c58d-110">Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c58d-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9c58d-111">Prerequisites</span></span>

- <span data-ttu-id="9c58d-112">W przypadku korzystania z zestawu SDK platformy .NET w programie Partner Center wymagany jest program w wersji 1,9 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="9c58d-112">If you are using the Partner Center .NET SDK, version 1.9 or newer is required.</span></span>

- <span data-ttu-id="9c58d-113">W przypadku korzystania z zestawu SDK języka Java Centrum partnerskiego wymagana jest wersja 1,8 lub nowsza.</span><span class="sxs-lookup"><span data-stu-id="9c58d-113">If you are using the Partner Center Java SDK, version 1.8 or newer is required.</span></span>

- <span data-ttu-id="9c58d-114">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](./partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9c58d-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="9c58d-115">Ten scenariusz obsługuje uwierzytelnianie aplikacji i użytkowników..</span><span class="sxs-lookup"><span data-stu-id="9c58d-115">This scenario supports app + user authentication..</span></span>

## <a name="net-version-114-or-newer"></a><span data-ttu-id="9c58d-116">.NET (wersja 1,14 lub nowsza)</span><span class="sxs-lookup"><span data-stu-id="9c58d-116">.NET (version 1.14 or newer)</span></span>

<span data-ttu-id="9c58d-117">Aby pobrać metadane umowy dla Microsoft Cloud umowy:</span><span class="sxs-lookup"><span data-stu-id="9c58d-117">To retrieve the agreement metadata for Microsoft Cloud Agreement:</span></span>

1. <span data-ttu-id="9c58d-118">Najpierw pobierz kolekcję **IAggregatePartner. AgreementDetails** .</span><span class="sxs-lookup"><span data-stu-id="9c58d-118">First, retrieve the **IAggregatePartner.AgreementDetails** collection.</span></span>

2. <span data-ttu-id="9c58d-119">Wywołaj metodę **ByAgreementType** , aby odfiltrować kolekcję do umowy Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="9c58d-119">Call **ByAgreementType** method to filter the collection to Microsoft Cloud Agreement.</span></span>

3. <span data-ttu-id="9c58d-120">Na koniec Wywołaj metodę **Get** lub **GetAsync** .</span><span class="sxs-lookup"><span data-stu-id="9c58d-120">Finally, call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

<span data-ttu-id="9c58d-121">Pełny przykład można znaleźć w klasie [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) z projektu [aplikacji testowej konsoli](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .</span><span class="sxs-lookup"><span data-stu-id="9c58d-121">A complete sample can be found in the [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="net-version-19---113"></a><span data-ttu-id="9c58d-122">.NET (wersja 1,9-1,13)</span><span class="sxs-lookup"><span data-stu-id="9c58d-122">.NET (version 1.9 - 1.13)</span></span>

<span data-ttu-id="9c58d-123">Aby pobrać metadane umów dla Microsoft Cloud umowy:</span><span class="sxs-lookup"><span data-stu-id="9c58d-123">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="9c58d-124">Najpierw pobierz kolekcję **IAggregatePartner. AgreementDetails** , a następnie wywołaj metody **Get** lub **GetAsync** .</span><span class="sxs-lookup"><span data-stu-id="9c58d-124">First retrieve the **IAggregatePartner.AgreementDetails** collection and then call the **Get** or **GetAsync** methods.</span></span> <span data-ttu-id="9c58d-125">Następnie wyszukaj element w kolekcji, który odpowiada umowie Microsoft Cloud:</span><span class="sxs-lookup"><span data-stu-id="9c58d-125">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a><span data-ttu-id="9c58d-126">Java</span><span class="sxs-lookup"><span data-stu-id="9c58d-126">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="9c58d-127">Aby pobrać metadane umów dla Microsoft Cloud umowy:</span><span class="sxs-lookup"><span data-stu-id="9c58d-127">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="9c58d-128">Najpierw wywołaj funkcję **IAggregatePartner. getAgreementDetails** , a następnie wywołaj funkcję **Get** .</span><span class="sxs-lookup"><span data-stu-id="9c58d-128">First call the **IAggregatePartner.getAgreementDetails** function and then call the **get** function.</span></span> <span data-ttu-id="9c58d-129">Następnie wyszukaj element w kolekcji, który odpowiada umowie Microsoft Cloud:</span><span class="sxs-lookup"><span data-stu-id="9c58d-129">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

```java
// IAggregatePartner partnerOperations;

ResourceCollection<AgreementMetaData> agreements = partnerOperations.getAgreements().get();

AgreementMetaData microsoftCloudAgreement;

for (AgreementMetaData metadata : agreements)
{
    if(metadata.getAgreementType() == AgreementType.MicrosoftCloudAgreement)
    {
        microsoftCloudAgreement = metadata;
    }
}
```

<span data-ttu-id="9c58d-130">Pełny przykład można znaleźć w klasie [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) z projektu [aplikacji testowej konsoli](https://github.com/Microsoft/Partner-Center-Java-Samples) .</span><span class="sxs-lookup"><span data-stu-id="9c58d-130">A complete sample can be found in the [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.</span></span>

## <a name="powershell"></a><span data-ttu-id="9c58d-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c58d-131">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="9c58d-132">Aby pobrać metadane umów dla Microsoft Cloud umowy:</span><span class="sxs-lookup"><span data-stu-id="9c58d-132">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="9c58d-133">Użyj polecenia [**Get-PartnerAgreementDetail**](/powershell/module/partnercenter/get-partneragreementdetail) .</span><span class="sxs-lookup"><span data-stu-id="9c58d-133">Use the [**Get-PartnerAgreementDetail**](/powershell/module/partnercenter/get-partneragreementdetail) command.</span></span> <span data-ttu-id="9c58d-134">Następnie wyszukaj element w kolekcji, który odpowiada umowie Microsoft Cloud:</span><span class="sxs-lookup"><span data-stu-id="9c58d-134">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest-request"></a><span data-ttu-id="9c58d-135">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="9c58d-135">REST request</span></span>

<span data-ttu-id="9c58d-136">Aby pobrać metadane umowy Microsoft Cloud, najpierw Utwórz żądanie REST w celu pobrania kolekcji **AgreementMetaData** .</span><span class="sxs-lookup"><span data-stu-id="9c58d-136">To retrieve agreement metadata for Microsoft Cloud Agreement, first create a REST Request to retrieve the **AgreementMetaData** collection.</span></span> <span data-ttu-id="9c58d-137">Następnie wyszukaj element w kolekcji, który odpowiada umowie Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="9c58d-137">Then search for the item in the collection which corresponds to the Microsoft Cloud Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9c58d-138">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="9c58d-138">Request syntax</span></span>

| <span data-ttu-id="9c58d-139">Metoda</span><span class="sxs-lookup"><span data-stu-id="9c58d-139">Method</span></span> | <span data-ttu-id="9c58d-140">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="9c58d-140">Request URI</span></span>                                                         |
|--------|---------------------------------------------------------------------|
| <span data-ttu-id="9c58d-141">GET</span><span class="sxs-lookup"><span data-stu-id="9c58d-141">GET</span></span>    | <span data-ttu-id="9c58d-142">[*\{ BASEURL \}*](partner-center-rest-urls.md)/V1/Agreements http/1.1</span><span class="sxs-lookup"><span data-stu-id="9c58d-142">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreements HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9c58d-143">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="9c58d-143">Request headers</span></span>

<span data-ttu-id="9c58d-144">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9c58d-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9c58d-145">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="9c58d-145">Request body</span></span>

<span data-ttu-id="9c58d-146">Brak.</span><span class="sxs-lookup"><span data-stu-id="9c58d-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9c58d-147">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="9c58d-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="9c58d-148">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="9c58d-148">REST response</span></span>

<span data-ttu-id="9c58d-149">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów **AgreementMetaData** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="9c58d-149">If successful, this method returns a collection of **AgreementMetaData** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9c58d-150">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9c58d-150">Response success and error codes</span></span>

<span data-ttu-id="9c58d-151">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="9c58d-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9c58d-152">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="9c58d-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9c58d-153">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9c58d-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9c58d-154">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9c58d-154">Response example</span></span>

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
            "templateId": "998b88de-aa99-4388-a42c-1b3517d49490",
            "agreementType": "MicrosoftCloudAgreement",
            "agreementLink": "https://docs.microsoft.com/partner-center/agreements",
            "versionRank": 0
        }
    ],
    "links": {
        "self": {
            "uri": "/agreements",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

<span data-ttu-id="9c58d-155">Aby zidentyfikować zasób w odpowiedzi, który odpowiada umowie Microsoft Cloud, poszukaj zasobu, którego właściwość **agreementtype** ma wartość "MicrosoftCloudAgreement".</span><span class="sxs-lookup"><span data-stu-id="9c58d-155">To identify the resource in the response which corresponds to the Microsoft Cloud Agreement, look for the resource whose **agreementType** property has value "MicrosoftCloudAgreement".</span></span>
