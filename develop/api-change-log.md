---
title: Dziennik zmian interfejsu API REST Centrum partnerskiego
description: Ta strona zawiera zmiany w interfejsie API REST Centrum partnerskiego
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: b2c2cac36a8bd1bec7aa5bf6e5d1aa73b4779535
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711852"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a><span data-ttu-id="5e646-103">Grudzień 2020 zmiany w interfejsie API REST Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="5e646-103">December 2020 changes to Partner Center REST APIs</span></span>

<span data-ttu-id="5e646-104">Tutaj znajdziesz zmiany w interfejsie API REST Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="5e646-104">Check here for changes to Partner Center REST APIs.</span></span>

## <a name="enhancements-to-education-pricing-eligibility-apis"></a><span data-ttu-id="5e646-105">Ulepszenia dotyczące interfejsów API kwalifikowania się do cen edukacyjnych</span><span class="sxs-lookup"><span data-stu-id="5e646-105">Enhancements to education pricing Eligibility APIs</span></span>



### <a name="what-has-changed"></a><span data-ttu-id="5e646-106">Co się zmieniło?</span><span class="sxs-lookup"><span data-stu-id="5e646-106">What has changed?</span></span>

<span data-ttu-id="5e646-107">Obecnie interfejs API Centrum partnerskiego ma uprawnienia do uzyskiwania kwalifikacji w celu zweryfikowania kwalifikacji klientów edukacyjnych.</span><span class="sxs-lookup"><span data-stu-id="5e646-107">Currently, the Partner Center API has GET and PUT qualifications to verify Education customers’ eligibility.</span></span> <span data-ttu-id="5e646-108">Nie zostaną wprowadzone żadne zmiany w interfejsie API pobierania kwalifikacji.</span><span class="sxs-lookup"><span data-stu-id="5e646-108">There will be no changes to the GET Qualification API.</span></span> <span data-ttu-id="5e646-109">Jednak dodaliśmy przypadek powrotu do interfejsu API UMIESZCZAnia kwalifikacji.</span><span class="sxs-lookup"><span data-stu-id="5e646-109">However, we’ve added a return case to the PUT Qualification API.</span></span>

- <span data-ttu-id="5e646-110">GET-nie zmienia.</span><span class="sxs-lookup"><span data-stu-id="5e646-110">GET - doesn't change.</span></span> [<span data-ttu-id="5e646-111">Bieżący artykuł interfejsu API</span><span class="sxs-lookup"><span data-stu-id="5e646-111">Current API article</span></span>](./get-customer-qualification-synchronous.md)
- <span data-ttu-id="5e646-112">Przypadek do zwrócenia zostanie dodany.</span><span class="sxs-lookup"><span data-stu-id="5e646-112">PUT - return case will be added.</span></span> [<span data-ttu-id="5e646-113">Bieżący artykuł interfejsu API</span><span class="sxs-lookup"><span data-stu-id="5e646-113">Current API article</span></span>](./update-customer-qualification-synchronous.md)

<span data-ttu-id="5e646-114">Te interfejsy API zostaną wycofane na koniec lutego 2021, aby zostały zastąpione przez nowe interfejsy API, zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="5e646-114">These APIs will be retired at the end of February 2021, to be replaced by new APIs as described below.</span></span>

### <a name="scenarios-impacted"></a><span data-ttu-id="5e646-115">Wpływ na scenariusze:</span><span class="sxs-lookup"><span data-stu-id="5e646-115">Scenarios impacted:</span></span>

<span data-ttu-id="5e646-116">Kwalifikowanie klientów do cen edukacyjnych na wybranych jednostkach SKU</span><span class="sxs-lookup"><span data-stu-id="5e646-116">Customer eligibility for education pricing on select SKUs</span></span>

### <a name="detail-descriptions"></a><span data-ttu-id="5e646-117">Opisy szczegółów</span><span class="sxs-lookup"><span data-stu-id="5e646-117">Detail descriptions</span></span>

<span data-ttu-id="5e646-118">Zostaną wprowadzone dwa nowe interfejsy API pobierania i ZAMIESZCZAnia kwalifikacji.</span><span class="sxs-lookup"><span data-stu-id="5e646-118">Two new GET and POST Qualifications APIs will be introduced.</span></span> <span data-ttu-id="5e646-119">Nowe interfejsy API będą korzystać z **kwalifikacji**, a nie **kwalifikacji**.</span><span class="sxs-lookup"><span data-stu-id="5e646-119">The new APIs will be using **Qualifications**, not **Qualification**.</span></span> <span data-ttu-id="5e646-120">Interfejsy API będą dostępne do testowania w FY21 Q2.</span><span class="sxs-lookup"><span data-stu-id="5e646-120">The APIs will be available for testing in FY21 Q2.</span></span>

#### <a name="get-qualifications"></a><span data-ttu-id="5e646-121">Pobierz kwalifikacje</span><span class="sxs-lookup"><span data-stu-id="5e646-121">GET Qualifications</span></span>

```http
GET {customer_id}/qualifications
```

#### <a name="response-example"></a><span data-ttu-id="5e646-122">Przykładowa odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="5e646-122">Response example:</span></span>

```json
{
  "Qualification": "Education",
  "VettingStatus": "Denied",
  "VettingReason": "Not an education customer",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

#### <a name="response-fields"></a><span data-ttu-id="5e646-123">Pola odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="5e646-123">Response fields:</span></span> 

- <span data-ttu-id="5e646-124">VettingStatus wartości: zatwierdzone, odrzucone, Nieprzejrzane itp.</span><span class="sxs-lookup"><span data-stu-id="5e646-124">VettingStatus values: Approved, Denied, InReview, etc.</span></span>

- <span data-ttu-id="5e646-125">VettingReason wartości:</span><span class="sxs-lookup"><span data-stu-id="5e646-125">VettingReason values:</span></span>
   - <span data-ttu-id="5e646-126">Nie jest to klient edukacyjny</span><span class="sxs-lookup"><span data-stu-id="5e646-126">Not an Education Customer</span></span>
   - <span data-ttu-id="5e646-127">Nie jest już klientem edukacyjnym</span><span class="sxs-lookup"><span data-stu-id="5e646-127">No longer an Education Customer</span></span>
   - <span data-ttu-id="5e646-128">Nie jest to klient edukacyjny — po przeprowadzeniu przeglądu</span><span class="sxs-lookup"><span data-stu-id="5e646-128">Not an Education Customer - After Review</span></span>
   - <span data-ttu-id="5e646-129">Ograniczony jako klient edukacyjny</span><span class="sxs-lookup"><span data-stu-id="5e646-129">Restricted being an Education Customer</span></span>
   - <span data-ttu-id="5e646-130">Nie jest to domena edukacyjna</span><span class="sxs-lookup"><span data-stu-id="5e646-130">Not an Academic Domain</span></span>
   - <span data-ttu-id="5e646-131">To nie jest kwalifikująca się biblioteka</span><span class="sxs-lookup"><span data-stu-id="5e646-131">Not an eligible Library</span></span>
   - <span data-ttu-id="5e646-132">Nie kwalifikuje się muzeów</span><span class="sxs-lookup"><span data-stu-id="5e646-132">Not an eligible Museum</span></span>
 
#### <a name="post-qualifications"></a><span data-ttu-id="5e646-133">Ogłoś kwalifikacje</span><span class="sxs-lookup"><span data-stu-id="5e646-133">POST Qualifications</span></span>

```http
POST {customer_id}/qualifications
    [
            "Qualification": "Education"
    ]
```

#### <a name="response-example"></a><span data-ttu-id="5e646-134">Przykładowa odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="5e646-134">Response example:</span></span>

```JSON
{
  "Qualification": "Education",
  "VettingStatus": "InReview",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

## <a name="next-steps"></a><span data-ttu-id="5e646-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5e646-135">Next steps</span></span>

[<span data-ttu-id="5e646-136">Dokumentacja interfejsu API REST Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="5e646-136">Partner Center REST API reference</span></span>](partner-center-rest-api-reference.md)