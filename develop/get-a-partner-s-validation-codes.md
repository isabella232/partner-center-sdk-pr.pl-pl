---
title: Pobierz kody weryfikacyjne w chmurze dla instytucji rządowych w społeczności partnerów
description: Jak uzyskać kody weryfikacji w chmurze dla instytucji rządowych w społeczności partnerów.
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: d84a3d3c69d835e42565c4e6f1edb06ab338340a
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768065"
---
# <a name="get-a-partners-validation-codes"></a><span data-ttu-id="269cb-103">Pobieranie kodów weryfikacyjnych partnera</span><span class="sxs-lookup"><span data-stu-id="269cb-103">Get a partner's validation codes</span></span>

<span data-ttu-id="269cb-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="269cb-104">**Applies To**</span></span>

- <span data-ttu-id="269cb-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="269cb-105">Partner Center</span></span>

<span data-ttu-id="269cb-106">Jak uzyskać kolekcję kodów weryfikacji w chmurze dla instytucji rządowych w społeczności partnerów.</span><span class="sxs-lookup"><span data-stu-id="269cb-106">How to get a collection of a partner's Government Community Cloud validation codes.</span></span> <span data-ttu-id="269cb-107">Kod weryfikacyjny jest wymagany do utworzenia klienta w chmurze społeczności dla instytucji rządowych.</span><span class="sxs-lookup"><span data-stu-id="269cb-107">A validation code is required to create a customer in the government community cloud.</span></span>

<span data-ttu-id="269cb-108">Jeśli interesuje Cię organizację lub organizację klientów zatwierdzoną dla programu Office 365 dla instytucji rządowych w ramach programu CSP dla dostawców usług kryptograficznych, zobacz [Office 365 Administracja dotycząca partnerów CSP i kryteria kwalifikujące klienta/Partner-Center/CSP-współpracy w zatoce-Validate).</span><span class="sxs-lookup"><span data-stu-id="269cb-108">If you are interested in having your organization or your customers organization approved for Office 365 Government GCC for CSP, please see [Office 365 Government GCC for CSP Partner and Customer Eligibility Criteria/partner-center/csp-gcc-validate).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="269cb-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="269cb-109">Prerequisites</span></span>

- <span data-ttu-id="269cb-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="269cb-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="269cb-111">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="269cb-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="269cb-112">Potwierdzenie weryfikacji po wypełnieniu [formularza.](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner)</span><span class="sxs-lookup"><span data-stu-id="269cb-112">Confirmed validation after filling out form [here](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner).</span></span>

- <span data-ttu-id="269cb-113">Klient bez kwalifikacji.</span><span class="sxs-lookup"><span data-stu-id="269cb-113">A customer without a qualification.</span></span>

## <a name="c"></a><span data-ttu-id="269cb-114">C\#</span><span class="sxs-lookup"><span data-stu-id="269cb-114">C\#</span></span>

<span data-ttu-id="269cb-115">Aby uzyskać listę wszystkich kodów weryfikacyjnych partnera, wywołaj **GetValidationCodes**.</span><span class="sxs-lookup"><span data-stu-id="269cb-115">To get a list of all of a partner's validation codes, call **GetValidationCodes**.</span></span>

``` csharp
// create the partner operations
IAggregatePartner partnerOperations = PartnerService.Instance.CreatePartnerOperations(credentials);

var gccValidations = partnerOperations.Validations.GetValidationCodes();
```

## <a name="rest-request"></a><span data-ttu-id="269cb-116">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="269cb-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="269cb-117">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="269cb-117">Request syntax</span></span>

| <span data-ttu-id="269cb-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="269cb-118">Method</span></span>  | <span data-ttu-id="269cb-119">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="269cb-119">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="269cb-120">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="269cb-120">**GET**</span></span> | <span data-ttu-id="269cb-121">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/All/validations http/1.1</span><span class="sxs-lookup"><span data-stu-id="269cb-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/all/validations HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="269cb-122">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="269cb-122">Request headers</span></span>

<span data-ttu-id="269cb-123">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="269cb-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="269cb-124">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="269cb-124">Request body</span></span>

<span data-ttu-id="269cb-125">Brak.</span><span class="sxs-lookup"><span data-stu-id="269cb-125">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="269cb-126">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="269cb-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/all/validations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3
```

## <a name="rest-response"></a><span data-ttu-id="269cb-127">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="269cb-127">REST response</span></span>

<span data-ttu-id="269cb-128">Jeśli to się powiedzie, metoda zwraca listę zasobów [**ValidationCode**](utility-resources.md#validationcode) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="269cb-128">If successful, this method returns a list of [**ValidationCode**](utility-resources.md#validationcode) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="269cb-129">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="269cb-129">Response success and error codes</span></span>

<span data-ttu-id="269cb-130">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="269cb-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="269cb-131">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="269cb-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="269cb-132">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="269cb-132">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="269cb-133">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="269cb-133">Response example</span></span>

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
