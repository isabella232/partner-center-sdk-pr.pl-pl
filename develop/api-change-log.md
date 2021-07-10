---
title: Dziennik zmian interfejsu API REST Centrum partnerskiego
description: Ta strona zawiera listę zmian w Partner Center API REST
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: d4f7f034a36a26b6219086ca952b189f7a313ef7
ms.sourcegitcommit: 51237e7e98d71a7e0590b4d6a4034b6409542126
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/09/2021
ms.locfileid: "113571999"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a><span data-ttu-id="e8342-103">Zmiany w interfejsach API REST Partner Center grudniu 2020 r.</span><span class="sxs-lookup"><span data-stu-id="e8342-103">December 2020 changes to Partner Center REST APIs</span></span>

<span data-ttu-id="e8342-104">Sprawdź tutaj, czy nie Partner Center interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="e8342-104">Check here for changes to Partner Center REST APIs.</span></span>

## <a name="enhancements-to-education-pricing-eligibility-apis"></a><span data-ttu-id="e8342-105">Ulepszenia interfejsów API uprawnień do cennika edukacji</span><span class="sxs-lookup"><span data-stu-id="e8342-105">Enhancements to education pricing Eligibility APIs</span></span>



### <a name="what-has-changed"></a><span data-ttu-id="e8342-106">Co się zmieniło?</span><span class="sxs-lookup"><span data-stu-id="e8342-106">What has changed?</span></span>

<span data-ttu-id="e8342-107">Obecnie interfejs API Partner Center ma kwalifikacje GET i PUT w celu zweryfikowania uprawnień klientów z edukacji.</span><span class="sxs-lookup"><span data-stu-id="e8342-107">Currently, the Partner Center API has GET and PUT qualifications to verify Education customers’ eligibility.</span></span> <span data-ttu-id="e8342-108">Interfejs API kwalifikacji GET nie zostanie wprowadzony.</span><span class="sxs-lookup"><span data-stu-id="e8342-108">There will be no changes to the GET Qualification API.</span></span> <span data-ttu-id="e8342-109">Dodaliśmy jednak przypadek zwrotny do interfejsu API kwalifikacji PUT.</span><span class="sxs-lookup"><span data-stu-id="e8342-109">However, we’ve added a return case to the PUT Qualification API.</span></span>

- <span data-ttu-id="e8342-110">GET — nie zmienia się.</span><span class="sxs-lookup"><span data-stu-id="e8342-110">GET - doesn't change.</span></span>
- <span data-ttu-id="e8342-111">PUT — zostanie dodany przypadek zwrotny.</span><span class="sxs-lookup"><span data-stu-id="e8342-111">PUT - return case will be added.</span></span>

<span data-ttu-id="e8342-112">Te interfejsy API zostaną wycofane z końcem lutego 2021 r. i zostaną zastąpione przez nowe interfejsy API, zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="e8342-112">These APIs will be retired at the end of February 2021, to be replaced by new APIs as described below.</span></span>

### <a name="scenarios-impacted"></a><span data-ttu-id="e8342-113">Scenariusze, których to miało wpływ:</span><span class="sxs-lookup"><span data-stu-id="e8342-113">Scenarios impacted:</span></span>

<span data-ttu-id="e8342-114">Kwalifikowalność klientów do cen usług edukacyjnych dla wybranych jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="e8342-114">Customer eligibility for education pricing on select SKUs</span></span>

### <a name="detail-descriptions"></a><span data-ttu-id="e8342-115">Szczegółowe opisy</span><span class="sxs-lookup"><span data-stu-id="e8342-115">Detail descriptions</span></span>

<span data-ttu-id="e8342-116">Zostaną wprowadzone dwa nowe interfejsy API kwalifikacji GET i POST.</span><span class="sxs-lookup"><span data-stu-id="e8342-116">Two new GET and POST Qualifications APIs will be introduced.</span></span> <span data-ttu-id="e8342-117">Nowe interfejsy API będą używać **kwalifikacji,** a nie **kwalifikacji.**</span><span class="sxs-lookup"><span data-stu-id="e8342-117">The new APIs will be using **Qualifications**, not **Qualification**.</span></span> <span data-ttu-id="e8342-118">Interfejsy API będą dostępne do testowania w 2. kwartale roku 2. kwartału.</span><span class="sxs-lookup"><span data-stu-id="e8342-118">The APIs will be available for testing in FY21 Q2.</span></span>

#### <a name="get-qualifications"></a><span data-ttu-id="e8342-119">Kwalifikacje GET</span><span class="sxs-lookup"><span data-stu-id="e8342-119">GET Qualifications</span></span>

```http
GET {customer_id}/qualifications
```

#### <a name="response-example"></a><span data-ttu-id="e8342-120">Przykładowa odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="e8342-120">Response example:</span></span>

```json
{
  "Qualification": "Education",
  "VettingStatus": "Denied",
  "VettingReason": "Not an education customer",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

#### <a name="response-fields"></a><span data-ttu-id="e8342-121">Pola odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="e8342-121">Response fields:</span></span> 

- <span data-ttu-id="e8342-122">Wartości VettingStatus: Approved, Denied, InReview itp.</span><span class="sxs-lookup"><span data-stu-id="e8342-122">VettingStatus values: Approved, Denied, InReview, etc.</span></span>

- <span data-ttu-id="e8342-123">Wartości VettingReason:</span><span class="sxs-lookup"><span data-stu-id="e8342-123">VettingReason values:</span></span>
   - <span data-ttu-id="e8342-124">Nie jest klientem edukacyjnym</span><span class="sxs-lookup"><span data-stu-id="e8342-124">Not an Education Customer</span></span>
   - <span data-ttu-id="e8342-125">Nie ma już klienta edukacyjnego</span><span class="sxs-lookup"><span data-stu-id="e8342-125">No longer an Education Customer</span></span>
   - <span data-ttu-id="e8342-126">Nie jest klientem edukacyjnym — po przeglądzie</span><span class="sxs-lookup"><span data-stu-id="e8342-126">Not an Education Customer - After Review</span></span>
   - <span data-ttu-id="e8342-127">Ograniczony jako klient edukacyjny</span><span class="sxs-lookup"><span data-stu-id="e8342-127">Restricted being an Education Customer</span></span>
   - <span data-ttu-id="e8342-128">Nie jest domeną akademickią</span><span class="sxs-lookup"><span data-stu-id="e8342-128">Not an Academic Domain</span></span>
   - <span data-ttu-id="e8342-129">Biblioteka nie jest kwalifikowana</span><span class="sxs-lookup"><span data-stu-id="e8342-129">Not an eligible Library</span></span>
   - <span data-ttu-id="e8342-130">Nie kwalifikuje się do pomocy</span><span class="sxs-lookup"><span data-stu-id="e8342-130">Not an eligible Museum</span></span>
 
#### <a name="post-qualifications"></a><span data-ttu-id="e8342-131">Kwalifikacje POST</span><span class="sxs-lookup"><span data-stu-id="e8342-131">POST Qualifications</span></span>

```http
POST {customer_id}/qualifications
    [
            "Qualification": "Education"
    ]
```

#### <a name="response-example"></a><span data-ttu-id="e8342-132">Przykładowa odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="e8342-132">Response example:</span></span>

```JSON
{
  "Qualification": "Education",
  "VettingStatus": "InReview",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

## <a name="next-steps"></a><span data-ttu-id="e8342-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e8342-133">Next steps</span></span>

[<span data-ttu-id="e8342-134">Dokumentacja interfejsu API REST Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="e8342-134">Partner Center REST API reference</span></span>](partner-center-rest-api-reference.md)
