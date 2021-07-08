---
title: Pobieranie metadanych umowy dla umowy dotyczącej platformy Microsoft Cloud
description: W tym artykule wyjaśniono, jak uzyskać metadane umowy dla Umowa dotycząca platformy Microsoft Cloud.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 2588327e72a13de75eb9e02675edbd535491adc4
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760797"
---
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a><span data-ttu-id="52425-103">Pobieranie metadanych umowy dla umowy dotyczącej platformy Microsoft Cloud</span><span class="sxs-lookup"><span data-stu-id="52425-103">Get agreement metadata for Microsoft Cloud Agreement</span></span>

<span data-ttu-id="52425-104">**Dotyczy:** Partner Center</span><span class="sxs-lookup"><span data-stu-id="52425-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="52425-105">**Nie dotyczy:** Partner Center obsługiwane przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="52425-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="52425-106">Zasób **AgreementMetaData** jest obecnie obsługiwany Partner Center tylko w chmurze publicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="52425-106">The **AgreementMetaData** resource is currently supported by Partner Center in the Microsoft public cloud only.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52425-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="52425-107">Prerequisites</span></span>

- <span data-ttu-id="52425-108">Jeśli używasz zestawu SDK platformy Partner Center .NET, wymagana jest wersja 1.9 lub nowsza.</span><span class="sxs-lookup"><span data-stu-id="52425-108">If you are using the Partner Center .NET SDK, version 1.9 or newer is required.</span></span>

- <span data-ttu-id="52425-109">Jeśli używasz zestawu SDK Partner Center Java, wymagana jest wersja 1.8 lub nowsza.</span><span class="sxs-lookup"><span data-stu-id="52425-109">If you are using the Partner Center Java SDK, version 1.8 or newer is required.</span></span>

- <span data-ttu-id="52425-110">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](./partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="52425-110">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="52425-111">Ten scenariusz obsługuje uwierzytelnianie aplikacji i użytkowników.</span><span class="sxs-lookup"><span data-stu-id="52425-111">This scenario supports app + user authentication.</span></span>

## <a name="net-version-114-or-newer"></a><span data-ttu-id="52425-112">.NET (wersja 1.14 lub nowsza)</span><span class="sxs-lookup"><span data-stu-id="52425-112">.NET (version 1.14 or newer)</span></span>

<span data-ttu-id="52425-113">Aby pobrać metadane umowy dla Umowa dotycząca platformy Microsoft Cloud:</span><span class="sxs-lookup"><span data-stu-id="52425-113">To retrieve the agreement metadata for Microsoft Cloud Agreement:</span></span>

1. <span data-ttu-id="52425-114">Najpierw pobierz **kolekcję IAggregatePartner.AgreementDetails.**</span><span class="sxs-lookup"><span data-stu-id="52425-114">First, retrieve the **IAggregatePartner.AgreementDetails** collection.</span></span>

2. <span data-ttu-id="52425-115">Wywołaj **metodę ByAgreementType,** aby filtrować kolekcję w Umowa dotycząca platformy Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="52425-115">Call **ByAgreementType** method to filter the collection to Microsoft Cloud Agreement.</span></span>

3. <span data-ttu-id="52425-116">Na koniec wywołaj **metodę Get** lub **GetAsync.**</span><span class="sxs-lookup"><span data-stu-id="52425-116">Finally, call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

<span data-ttu-id="52425-117">Kompletny przykład można znaleźć w klasie [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) w projekcie [aplikacji testowej konsoli.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)</span><span class="sxs-lookup"><span data-stu-id="52425-117">A complete sample can be found in the [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="net-version-19---113"></a><span data-ttu-id="52425-118">.NET (wersja 1.9–1.13)</span><span class="sxs-lookup"><span data-stu-id="52425-118">.NET (version 1.9 - 1.13)</span></span>

<span data-ttu-id="52425-119">Aby pobrać metadane umowy dla Umowa dotycząca platformy Microsoft Cloud:</span><span class="sxs-lookup"><span data-stu-id="52425-119">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="52425-120">Najpierw pobierz **kolekcję IAggregatePartner.AgreementDetails,** a następnie wywołaj metody **Get** lub **GetAsync.**</span><span class="sxs-lookup"><span data-stu-id="52425-120">First retrieve the **IAggregatePartner.AgreementDetails** collection and then call the **Get** or **GetAsync** methods.</span></span> <span data-ttu-id="52425-121">Następnie wyszukaj element w kolekcji, który odpowiada wartości Umowa dotycząca platformy Microsoft Cloud:</span><span class="sxs-lookup"><span data-stu-id="52425-121">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a><span data-ttu-id="52425-122">Java</span><span class="sxs-lookup"><span data-stu-id="52425-122">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="52425-123">Aby pobrać metadane umowy dla Umowa dotycząca platformy Microsoft Cloud:</span><span class="sxs-lookup"><span data-stu-id="52425-123">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="52425-124">Najpierw wywołaj **funkcję IAggregatePartner.getAgreementDetails,** a następnie wywołaj **funkcję get.**</span><span class="sxs-lookup"><span data-stu-id="52425-124">First call the **IAggregatePartner.getAgreementDetails** function and then call the **get** function.</span></span> <span data-ttu-id="52425-125">Następnie wyszukaj element w kolekcji, który odpowiada wartości Umowa dotycząca platformy Microsoft Cloud:</span><span class="sxs-lookup"><span data-stu-id="52425-125">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

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

<span data-ttu-id="52425-126">Kompletny przykład można znaleźć w klasie [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) w projekcie [aplikacji testowej konsoli.](https://github.com/Microsoft/Partner-Center-Java-Samples)</span><span class="sxs-lookup"><span data-stu-id="52425-126">A complete sample can be found in the [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.</span></span>

## <a name="powershell"></a><span data-ttu-id="52425-127">PowerShell</span><span class="sxs-lookup"><span data-stu-id="52425-127">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="52425-128">Aby pobrać metadane umowy dla Umowa dotycząca platformy Microsoft Cloud:</span><span class="sxs-lookup"><span data-stu-id="52425-128">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="52425-129">Użyj polecenia [**Get-PartnerAgreementDetail.**](/powershell/module/partnercenter/get-partneragreementdetail)</span><span class="sxs-lookup"><span data-stu-id="52425-129">Use the [**Get-PartnerAgreementDetail**](/powershell/module/partnercenter/get-partneragreementdetail) command.</span></span> <span data-ttu-id="52425-130">Następnie wyszukaj element w kolekcji, który odpowiada wartości Umowa dotycząca platformy Microsoft Cloud:</span><span class="sxs-lookup"><span data-stu-id="52425-130">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest-request"></a><span data-ttu-id="52425-131">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="52425-131">REST request</span></span>

<span data-ttu-id="52425-132">Aby pobrać metadane umowy dla Umowa dotycząca platformy Microsoft Cloud, najpierw utwórz żądanie REST w celu pobrania **kolekcji AgreementMetaData.**</span><span class="sxs-lookup"><span data-stu-id="52425-132">To retrieve agreement metadata for Microsoft Cloud Agreement, first create a REST Request to retrieve the **AgreementMetaData** collection.</span></span> <span data-ttu-id="52425-133">Następnie wyszukaj element w kolekcji, który odpowiada wartości Umowa dotycząca platformy Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="52425-133">Then search for the item in the collection that corresponds to the Microsoft Cloud Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="52425-134">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="52425-134">Request syntax</span></span>

| <span data-ttu-id="52425-135">Metoda</span><span class="sxs-lookup"><span data-stu-id="52425-135">Method</span></span> | <span data-ttu-id="52425-136">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="52425-136">Request URI</span></span>                                                         |
|--------|---------------------------------------------------------------------|
| <span data-ttu-id="52425-137">GET</span><span class="sxs-lookup"><span data-stu-id="52425-137">GET</span></span>    | <span data-ttu-id="52425-138">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="52425-138">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreements HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="52425-139">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="52425-139">Request headers</span></span>

<span data-ttu-id="52425-140">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="52425-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="52425-141">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="52425-141">Request body</span></span>

<span data-ttu-id="52425-142">Brak.</span><span class="sxs-lookup"><span data-stu-id="52425-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="52425-143">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="52425-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="52425-144">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="52425-144">REST response</span></span>

<span data-ttu-id="52425-145">W przypadku powodzenia ta metoda zwraca kolekcję **zasobów AgreementMetaData** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="52425-145">If successful, this method returns a collection of **AgreementMetaData** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="52425-146">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="52425-146">Response success and error codes</span></span>

<span data-ttu-id="52425-147">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="52425-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="52425-148">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="52425-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="52425-149">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="52425-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="52425-150">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="52425-150">Response example</span></span>

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

<span data-ttu-id="52425-151">Aby zidentyfikować zasób w odpowiedzi, który odpowiada właściwości Umowa dotycząca platformy Microsoft Cloud, poszukaj zasobu, którego właściwość **agreementType** ma wartość "MicrosoftCloudAgreement".</span><span class="sxs-lookup"><span data-stu-id="52425-151">To identify the resource in the response that corresponds to the Microsoft Cloud Agreement, look for the resource whose **agreementType** property has value "MicrosoftCloudAgreement".</span></span>
