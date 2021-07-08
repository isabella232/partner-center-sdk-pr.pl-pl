---
title: Zasoby usługi zarządzanej
description: Usługi zarządzane to usługi, do których partner ma delegowane uprawnienia administratora. Partnerzy mogą zapewniać obsługę żądań obsługi i plików w imieniu swoich zarządzanych usług.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 582efe75fd18a9174dd5dc173c290bee25443ee9
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548128"
---
# <a name="managed-service-resources"></a><span data-ttu-id="c470c-104">Zasoby usługi zarządzanej</span><span class="sxs-lookup"><span data-stu-id="c470c-104">Managed service resources</span></span>

<span data-ttu-id="c470c-105">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="c470c-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c470c-106">Usługi zarządzane to usługi, do których partner ma delegowane uprawnienia administratora.</span><span class="sxs-lookup"><span data-stu-id="c470c-106">Managed services are services to which a partner has delegated admin privileges.</span></span> <span data-ttu-id="c470c-107">Partnerzy mogą zapewniać obsługę żądań obsługi i plików w imieniu swoich zarządzanych usług.</span><span class="sxs-lookup"><span data-stu-id="c470c-107">Partners can provide support for and file service requests on the behalf of their managed services.</span></span>

## <a name="managedservice"></a><span data-ttu-id="c470c-108">ManagedService (Usługa zarządzana)</span><span class="sxs-lookup"><span data-stu-id="c470c-108">ManagedService</span></span>

<span data-ttu-id="c470c-109">Opisuje usługę zarządzaną.</span><span class="sxs-lookup"><span data-stu-id="c470c-109">Describes a managed service.</span></span>

| <span data-ttu-id="c470c-110">Właściwość</span><span class="sxs-lookup"><span data-stu-id="c470c-110">Property</span></span>   | <span data-ttu-id="c470c-111">Typ</span><span class="sxs-lookup"><span data-stu-id="c470c-111">Type</span></span>                | <span data-ttu-id="c470c-112">Opis</span><span class="sxs-lookup"><span data-stu-id="c470c-112">Description</span></span>                                              |
|------------|---------------------|----------------------------------------------------------|
| <span data-ttu-id="c470c-113">Id</span><span class="sxs-lookup"><span data-stu-id="c470c-113">Id</span></span>         | <span data-ttu-id="c470c-114">ciąg</span><span class="sxs-lookup"><span data-stu-id="c470c-114">string</span></span>              | <span data-ttu-id="c470c-115">Identyfikator usługi zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="c470c-115">The managed service ID.</span></span>                                  |
| <span data-ttu-id="c470c-116">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c470c-116">Name</span></span>       | <span data-ttu-id="c470c-117">ciąg</span><span class="sxs-lookup"><span data-stu-id="c470c-117">string</span></span>              | <span data-ttu-id="c470c-118">Nazwa usługi zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="c470c-118">The name of the managed service.</span></span>                         |
| <span data-ttu-id="c470c-119">Groupname</span><span class="sxs-lookup"><span data-stu-id="c470c-119">GroupName</span></span>  | <span data-ttu-id="c470c-120">ciąg</span><span class="sxs-lookup"><span data-stu-id="c470c-120">string</span></span>              | <span data-ttu-id="c470c-121">Nazwa grupy, do której należy usługa.</span><span class="sxs-lookup"><span data-stu-id="c470c-121">The name of the group to which the service belongs.</span></span>      |
| <span data-ttu-id="c470c-122">Linki</span><span class="sxs-lookup"><span data-stu-id="c470c-122">Links</span></span>      | <span data-ttu-id="c470c-123">ManagedServiceLinks</span><span class="sxs-lookup"><span data-stu-id="c470c-123">ManagedServiceLinks</span></span> | <span data-ttu-id="c470c-124">Linki zasobów odpowiadające usłudze zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="c470c-124">The resource links corresponding to the managed service.</span></span> |
| <span data-ttu-id="c470c-125">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="c470c-125">Attributes</span></span> | <span data-ttu-id="c470c-126">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="c470c-126">ResourceAttributes</span></span>  | <span data-ttu-id="c470c-127">Atrybuty metadanych odpowiadające umowie.</span><span class="sxs-lookup"><span data-stu-id="c470c-127">The metadata attributes corresponding to the agreement.</span></span>  |

## <a name="managedservicelinks"></a><span data-ttu-id="c470c-128">ManagedServiceLinks</span><span class="sxs-lookup"><span data-stu-id="c470c-128">ManagedServiceLinks</span></span>

<span data-ttu-id="c470c-129">Zawiera linki, które umożliwiają partnerowi z delegowanymi uprawnieniami administratora zapewnienie obsługi usługi.</span><span class="sxs-lookup"><span data-stu-id="c470c-129">Contains the links that allow the partner with delegated admin permissions to provide support for the service.</span></span>

| <span data-ttu-id="c470c-130">Właściwość</span><span class="sxs-lookup"><span data-stu-id="c470c-130">Property</span></span>      | <span data-ttu-id="c470c-131">Typ</span><span class="sxs-lookup"><span data-stu-id="c470c-131">Type</span></span> | <span data-ttu-id="c470c-132">Opis</span><span class="sxs-lookup"><span data-stu-id="c470c-132">Description</span></span>                 |
|---------------|------|-----------------------------|
| <span data-ttu-id="c470c-133">Usługa administracyjna</span><span class="sxs-lookup"><span data-stu-id="c470c-133">AdminService</span></span>  | <span data-ttu-id="c470c-134">Link</span><span class="sxs-lookup"><span data-stu-id="c470c-134">Link</span></span> | <span data-ttu-id="c470c-135">URI usługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="c470c-135">The admin service URI.</span></span>      |
| <span data-ttu-id="c470c-136">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="c470c-136">ServiceHealth</span></span> | <span data-ttu-id="c470c-137">Link</span><span class="sxs-lookup"><span data-stu-id="c470c-137">Link</span></span> | <span data-ttu-id="c470c-138">URI kondycji usługi.</span><span class="sxs-lookup"><span data-stu-id="c470c-138">The service health URI.</span></span>     |
| <span data-ttu-id="c470c-139">ServiceTicket</span><span class="sxs-lookup"><span data-stu-id="c470c-139">ServiceTicket</span></span> | <span data-ttu-id="c470c-140">Link</span><span class="sxs-lookup"><span data-stu-id="c470c-140">Link</span></span> | <span data-ttu-id="c470c-141">URI biletu usługi.</span><span class="sxs-lookup"><span data-stu-id="c470c-141">The service ticket URI.</span></span>     |
| <span data-ttu-id="c470c-142">Self</span><span class="sxs-lookup"><span data-stu-id="c470c-142">Self</span></span>          | <span data-ttu-id="c470c-143">Link</span><span class="sxs-lookup"><span data-stu-id="c470c-143">Link</span></span> | <span data-ttu-id="c470c-144">Samodzielnego URI.</span><span class="sxs-lookup"><span data-stu-id="c470c-144">The self-URI.</span></span>               |
| <span data-ttu-id="c470c-145">Następne</span><span class="sxs-lookup"><span data-stu-id="c470c-145">Next</span></span>          | <span data-ttu-id="c470c-146">Link</span><span class="sxs-lookup"><span data-stu-id="c470c-146">Link</span></span> | <span data-ttu-id="c470c-147">Następna strona elementów.</span><span class="sxs-lookup"><span data-stu-id="c470c-147">The next page of items.</span></span>     |
| <span data-ttu-id="c470c-148">Poprzednie</span><span class="sxs-lookup"><span data-stu-id="c470c-148">Previous</span></span>      | <span data-ttu-id="c470c-149">Link</span><span class="sxs-lookup"><span data-stu-id="c470c-149">Link</span></span> | <span data-ttu-id="c470c-150">Poprzednia strona elementów.</span><span class="sxs-lookup"><span data-stu-id="c470c-150">The previous page of items.</span></span> |

