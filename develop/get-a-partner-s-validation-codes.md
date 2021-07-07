---
title: Uzyskiwanie kodów weryfikacyjnych Government Community Cloud partnera
description: Jak uzyskać kody weryfikacji Government Community Cloud partnera.
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: 04bccf587628337004a5825b534048945f791839
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873874"
---
# <a name="get-a-partners-validation-codes"></a><span data-ttu-id="72a10-103">Pobieranie kodów weryfikacyjnych partnera</span><span class="sxs-lookup"><span data-stu-id="72a10-103">Get a partner's validation codes</span></span>

<span data-ttu-id="72a10-104">W tym artykule opisano sposób pobierania kolekcji kodów weryfikacji Government Community Cloud partnera.</span><span class="sxs-lookup"><span data-stu-id="72a10-104">This article describes how to get a collection of a partner's Government Community Cloud validation codes.</span></span> <span data-ttu-id="72a10-105">Kod weryfikacyjny jest wymagany do utworzenia klienta w chmurze społeczności instytucji rządowych.</span><span class="sxs-lookup"><span data-stu-id="72a10-105">A validation code is required to create a customer in the government community cloud.</span></span>

<span data-ttu-id="72a10-106">Jeśli interesuje Cię zatwierdzenie organizacji lub organizacji klienta w programie Office 365 dla instytucji rządowych GCC dla programu CSP, zobacz Office 365 dla instytucji rządowych GCC for [CSP Partner and Customer eligibility criteria](/partner-center/csp-gcc-validate)(Kryteria kwalifikowalności klientów i partnerów programu CSP).</span><span class="sxs-lookup"><span data-stu-id="72a10-106">If you are interested in having your organization or your customer's organization approved for Office 365 Government GCC for CSP, see [Office 365 Government GCC for CSP Partner and Customer eligibility criteria](/partner-center/csp-gcc-validate).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72a10-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="72a10-107">Prerequisites</span></span>

- <span data-ttu-id="72a10-108">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="72a10-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="72a10-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="72a10-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="72a10-110">Potwierdzenie weryfikacji po wypełnieniu formularza [tutaj.](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner)</span><span class="sxs-lookup"><span data-stu-id="72a10-110">Confirmed validation after filling out form [here](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner).</span></span>

- <span data-ttu-id="72a10-111">Klient bez kwalifikacji.</span><span class="sxs-lookup"><span data-stu-id="72a10-111">A customer without a qualification.</span></span>

## <a name="c"></a><span data-ttu-id="72a10-112">C\#</span><span class="sxs-lookup"><span data-stu-id="72a10-112">C\#</span></span>

<span data-ttu-id="72a10-113">Aby uzyskać listę wszystkich kodów weryfikacji partnera, wywołaj metody **GetValidationCodes.**</span><span class="sxs-lookup"><span data-stu-id="72a10-113">To get a list of all of a partner's validation codes, call **GetValidationCodes**.</span></span>

``` csharp
// create the partner operations
IAggregatePartner partnerOperations = PartnerService.Instance.CreatePartnerOperations(credentials);

var gccValidations = partnerOperations.Validations.GetValidationCodes();
```

## <a name="rest-request"></a><span data-ttu-id="72a10-114">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="72a10-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="72a10-115">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="72a10-115">Request syntax</span></span>

| <span data-ttu-id="72a10-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="72a10-116">Method</span></span>  | <span data-ttu-id="72a10-117">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="72a10-117">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="72a10-118">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="72a10-118">**GET**</span></span> | <span data-ttu-id="72a10-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/all/validations HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="72a10-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/all/validations HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="72a10-120">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="72a10-120">Request headers</span></span>

<span data-ttu-id="72a10-121">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="72a10-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="72a10-122">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="72a10-122">Request body</span></span>

<span data-ttu-id="72a10-123">Brak.</span><span class="sxs-lookup"><span data-stu-id="72a10-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="72a10-124">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="72a10-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/all/validations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3
```

## <a name="rest-response"></a><span data-ttu-id="72a10-125">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="72a10-125">REST response</span></span>

<span data-ttu-id="72a10-126">W przypadku powodzenia ta metoda zwraca listę zasobów [**ValidationCode**](utility-resources.md#validationcode) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="72a10-126">If successful, this method returns a list of [**ValidationCode**](utility-resources.md#validationcode) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="72a10-127">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="72a10-127">Response success and error codes</span></span>

<span data-ttu-id="72a10-128">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="72a10-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="72a10-129">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="72a10-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="72a10-130">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="72a10-130">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="72a10-131">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="72a10-131">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 434
Content-Type: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3

[
  {
    "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d",
    "organizationName": "Contoso, Inc.",
    "validationId": "12345",
    "maxCreates": 5,
    "remainingCreates": 4,
    "eTag": "W/\"datetime'2018-10-10T18%3A49%3A58.727348Z'\""
  },
  {
    "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d",
    "organizationName": "Contoso, Inc. Finance Department",
    "validationId": "987654",
    "maxCreates": 5,
    "remainingCreates": 5,
    "eTag": "W/\"datetime'2018-10-19T17%3A51%3A45.6584512Z'\""
  }
]
```
