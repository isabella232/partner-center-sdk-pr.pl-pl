---
title: Dziennik zmian interfejsu API REST Centrum partnerskiego
description: Ta strona zawiera zmiany w interfejsie API REST Centrum partnerskiego
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: 79359414276a1259117a8f506bbfae4441cdcbed
ms.sourcegitcommit: f8ca3a14a763013fefafd3262d0a740881d1d7b1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/17/2020
ms.locfileid: "97770283"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a><span data-ttu-id="2b319-103">Grudzień 2020 zmiany w interfejsie API REST Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="2b319-103">December 2020 changes to Partner Center REST APIs</span></span>

<span data-ttu-id="2b319-104">Tutaj znajdziesz zmiany w interfejsie API REST Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="2b319-104">Check here for changes to Partner Center REST APIs.</span></span>

## <a name="enhancements-to-education-pricing-eligibility-apis"></a><span data-ttu-id="2b319-105">Ulepszenia dotyczące interfejsów API kwalifikowania się do cen edukacyjnych</span><span class="sxs-lookup"><span data-stu-id="2b319-105">Enhancements to education pricing Eligibility APIs</span></span>



### <a name="what-has-changed"></a><span data-ttu-id="2b319-106">Co się zmieniło?</span><span class="sxs-lookup"><span data-stu-id="2b319-106">What has changed?</span></span>

<span data-ttu-id="2b319-107">Obecnie interfejs API Centrum partnerskiego ma uprawnienia do uzyskiwania kwalifikacji w celu zweryfikowania kwalifikacji klientów edukacyjnych.</span><span class="sxs-lookup"><span data-stu-id="2b319-107">Currently, the Partner Center API has GET and PUT qualifications to verify Education customers’ eligibility.</span></span> <span data-ttu-id="2b319-108">Nie zostaną wprowadzone żadne zmiany w interfejsie API pobierania kwalifikacji.</span><span class="sxs-lookup"><span data-stu-id="2b319-108">There will be no changes to the GET Qualification API.</span></span> <span data-ttu-id="2b319-109">Jednak dodaliśmy przypadek powrotu do interfejsu API UMIESZCZAnia kwalifikacji.</span><span class="sxs-lookup"><span data-stu-id="2b319-109">However, we’ve added a return case to the PUT Qualification API.</span></span>

- <span data-ttu-id="2b319-110">GET-nie zmienia.</span><span class="sxs-lookup"><span data-stu-id="2b319-110">GET - doesn't change.</span></span> [<span data-ttu-id="2b319-111">Bieżący artykuł interfejsu API</span><span class="sxs-lookup"><span data-stu-id="2b319-111">Current API article</span></span>](get-a-customer-s-qualification.md)
- <span data-ttu-id="2b319-112">Przypadek do zwrócenia zostanie dodany.</span><span class="sxs-lookup"><span data-stu-id="2b319-112">PUT - return case will be added.</span></span> [<span data-ttu-id="2b319-113">Bieżący artykuł interfejsu API</span><span class="sxs-lookup"><span data-stu-id="2b319-113">Current API article</span></span>](update-a-customer-s-qualification.md)

<span data-ttu-id="2b319-114">Te interfejsy API zostaną wycofane na koniec lutego 2021, aby zostały zastąpione przez nowe interfejsy API, zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="2b319-114">These APIs will be retired at the end of February 2021, to be replaced by new APIs as described below.</span></span>

### <a name="scenarios-impacted"></a><span data-ttu-id="2b319-115">Wpływ na scenariusze:</span><span class="sxs-lookup"><span data-stu-id="2b319-115">Scenarios impacted:</span></span>

<span data-ttu-id="2b319-116">Kwalifikowanie klientów do cen edukacyjnych na wybranych jednostkach SKU</span><span class="sxs-lookup"><span data-stu-id="2b319-116">Customer eligibility for education pricing on select SKUs</span></span>

### <a name="detail-descriptions"></a><span data-ttu-id="2b319-117">Opisy szczegółów</span><span class="sxs-lookup"><span data-stu-id="2b319-117">Detail descriptions</span></span>

<span data-ttu-id="2b319-118">Zostaną wprowadzone dwa nowe interfejsy API pobierania i ZAMIESZCZAnia kwalifikacji.</span><span class="sxs-lookup"><span data-stu-id="2b319-118">Two new GET and POST Qualifications APIs will be introduced.</span></span> <span data-ttu-id="2b319-119">Nowe interfejsy API będą korzystać z **kwalifikacji**, a nie **kwalifikacji**.</span><span class="sxs-lookup"><span data-stu-id="2b319-119">The new APIs will be using **Qualifications**, not **Qualification**.</span></span> <span data-ttu-id="2b319-120">Interfejsy API będą dostępne do testowania w FY21 Q2.</span><span class="sxs-lookup"><span data-stu-id="2b319-120">The APIs will be available for testing in FY21 Q2.</span></span>

#### <a name="get-qualifications"></a><span data-ttu-id="2b319-121">Pobierz kwalifikacje</span><span class="sxs-lookup"><span data-stu-id="2b319-121">GET Qualifications</span></span>

```http
GET {customer_id}/qualifications
```

#### <a name="response-example"></a><span data-ttu-id="2b319-122">Przykładowa odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="2b319-122">Response example:</span></span>

```json
{
  "Qualification": "Education",
  "VettingStatus": "Denied",
  "VettingReason": "Not an education customer",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

#### <a name="response-fields"></a><span data-ttu-id="2b319-123">Pola odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="2b319-123">Response fields:</span></span> 

- <span data-ttu-id="2b319-124">VettingStatus wartości: zatwierdzone, odrzucone, Nieprzejrzane itp.</span><span class="sxs-lookup"><span data-stu-id="2b319-124">VettingStatus values: Approved, Denied, InReview, etc.</span></span>

- <span data-ttu-id="2b319-125">VettingReason wartości:</span><span class="sxs-lookup"><span data-stu-id="2b319-125">VettingReason values:</span></span>
   - <span data-ttu-id="2b319-126">Nie jest to klient edukacyjny</span><span class="sxs-lookup"><span data-stu-id="2b319-126">Not an Education Customer</span></span>
   - <span data-ttu-id="2b319-127">Nie jest już klientem edukacyjnym</span><span class="sxs-lookup"><span data-stu-id="2b319-127">No longer an Education Customer</span></span>
   - <span data-ttu-id="2b319-128">Nie jest to klient edukacyjny — po przeprowadzeniu przeglądu</span><span class="sxs-lookup"><span data-stu-id="2b319-128">Not an Education Customer - After Review</span></span>
   - <span data-ttu-id="2b319-129">Ograniczony jako klient edukacyjny</span><span class="sxs-lookup"><span data-stu-id="2b319-129">Restricted being an Education Customer</span></span>
   - <span data-ttu-id="2b319-130">Nie jest to domena edukacyjna</span><span class="sxs-lookup"><span data-stu-id="2b319-130">Not an Academic Domain</span></span>
   - <span data-ttu-id="2b319-131">To nie jest kwalifikująca się biblioteka</span><span class="sxs-lookup"><span data-stu-id="2b319-131">Not an eligible Library</span></span>
   - <span data-ttu-id="2b319-132">Nie kwalifikuje się muzeów</span><span class="sxs-lookup"><span data-stu-id="2b319-132">Not an eligible Museum</span></span>
 
#### <a name="post-qualifications"></a><span data-ttu-id="2b319-133">Ogłoś kwalifikacje</span><span class="sxs-lookup"><span data-stu-id="2b319-133">POST Qualifications</span></span>

```http
POST {customer_id}/qualifications
    [
            "Qualification": "Education"
    ]
```

#### <a name="response-example"></a><span data-ttu-id="2b319-134">Przykładowa odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="2b319-134">Response example:</span></span>

```JSON
{
  "Qualification": "Education",
  "VettingStatus": "InReview",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

## <a name="next-steps"></a><span data-ttu-id="2b319-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2b319-135">Next steps</span></span>

[<span data-ttu-id="2b319-136">Dokumentacja interfejsu API REST Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="2b319-136">Partner Center REST API reference</span></span>](partner-center-rest-api-reference.md)
