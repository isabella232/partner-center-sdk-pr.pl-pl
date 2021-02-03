---
title: Zarządzane zasoby usług
description: Usługi zarządzane to usługi, do których partner ma delegowane uprawnienia administratora. Partnerzy mogą zapewnić obsługę żądań i usług plików w imieniu ich usług zarządzanych.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef644ac4d8ae9660cffc9558af33cc27832556c7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767782"
---
# <a name="managed-service-resources"></a><span data-ttu-id="afb23-104">Zarządzane zasoby usług</span><span class="sxs-lookup"><span data-stu-id="afb23-104">Managed service resources</span></span>

<span data-ttu-id="afb23-105">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="afb23-105">**Applies To**</span></span>

- <span data-ttu-id="afb23-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="afb23-106">Partner Center</span></span>
- <span data-ttu-id="afb23-107">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="afb23-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="afb23-108">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="afb23-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="afb23-109">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="afb23-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="afb23-110">Usługi zarządzane to usługi, do których partner ma delegowane uprawnienia administratora.</span><span class="sxs-lookup"><span data-stu-id="afb23-110">Managed services are services to which a partner has delegated admin privileges.</span></span> <span data-ttu-id="afb23-111">Partnerzy mogą zapewnić obsługę żądań i usług plików w imieniu ich usług zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="afb23-111">Partners can provide support for and file service requests on the behalf of their managed services.</span></span>

## <a name="managedservice"></a><span data-ttu-id="afb23-112">ManagedService</span><span class="sxs-lookup"><span data-stu-id="afb23-112">ManagedService</span></span>

<span data-ttu-id="afb23-113">Opisuje usługę zarządzaną.</span><span class="sxs-lookup"><span data-stu-id="afb23-113">Describes a managed service.</span></span>

| <span data-ttu-id="afb23-114">Właściwość</span><span class="sxs-lookup"><span data-stu-id="afb23-114">Property</span></span>   | <span data-ttu-id="afb23-115">Typ</span><span class="sxs-lookup"><span data-stu-id="afb23-115">Type</span></span>                | <span data-ttu-id="afb23-116">Opis</span><span class="sxs-lookup"><span data-stu-id="afb23-116">Description</span></span>                                              |
|------------|---------------------|----------------------------------------------------------|
| <span data-ttu-id="afb23-117">Id</span><span class="sxs-lookup"><span data-stu-id="afb23-117">Id</span></span>         | <span data-ttu-id="afb23-118">ciąg</span><span class="sxs-lookup"><span data-stu-id="afb23-118">string</span></span>              | <span data-ttu-id="afb23-119">Identyfikator usługi zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="afb23-119">The managed service id.</span></span>                                  |
| <span data-ttu-id="afb23-120">Nazwa</span><span class="sxs-lookup"><span data-stu-id="afb23-120">Name</span></span>       | <span data-ttu-id="afb23-121">ciąg</span><span class="sxs-lookup"><span data-stu-id="afb23-121">string</span></span>              | <span data-ttu-id="afb23-122">Nazwa usługi zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="afb23-122">The name of the managed service.</span></span>                         |
| <span data-ttu-id="afb23-123">GroupName</span><span class="sxs-lookup"><span data-stu-id="afb23-123">GroupName</span></span>  | <span data-ttu-id="afb23-124">ciąg</span><span class="sxs-lookup"><span data-stu-id="afb23-124">string</span></span>              | <span data-ttu-id="afb23-125">Nazwa grupy, do której należy usługa.</span><span class="sxs-lookup"><span data-stu-id="afb23-125">The name of the group to which the service belongs.</span></span>      |
| <span data-ttu-id="afb23-126">Linki</span><span class="sxs-lookup"><span data-stu-id="afb23-126">Links</span></span>      | <span data-ttu-id="afb23-127">ManagedServiceLinks</span><span class="sxs-lookup"><span data-stu-id="afb23-127">ManagedServiceLinks</span></span> | <span data-ttu-id="afb23-128">Linki do zasobów odpowiadające usłudze zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="afb23-128">The resource links corresponding to the managed service.</span></span> |
| <span data-ttu-id="afb23-129">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="afb23-129">Attributes</span></span> | <span data-ttu-id="afb23-130">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="afb23-130">ResourceAttributes</span></span>  | <span data-ttu-id="afb23-131">Atrybuty metadanych odpowiadające umowie.</span><span class="sxs-lookup"><span data-stu-id="afb23-131">The metadata attributes corresponding to the agreement.</span></span>  |

## <a name="managedservicelinks"></a><span data-ttu-id="afb23-132">ManagedServiceLinks</span><span class="sxs-lookup"><span data-stu-id="afb23-132">ManagedServiceLinks</span></span>

<span data-ttu-id="afb23-133">Zawiera linki zezwalające partnerowi z delegowanymi uprawnieniami administratora w celu zapewnienia pomocy technicznej dla usługi.</span><span class="sxs-lookup"><span data-stu-id="afb23-133">Contains the links that allow the partner with delegated admin permissions to provide support for the service.</span></span>

| <span data-ttu-id="afb23-134">Właściwość</span><span class="sxs-lookup"><span data-stu-id="afb23-134">Property</span></span>      | <span data-ttu-id="afb23-135">Typ</span><span class="sxs-lookup"><span data-stu-id="afb23-135">Type</span></span> | <span data-ttu-id="afb23-136">Opis</span><span class="sxs-lookup"><span data-stu-id="afb23-136">Description</span></span>                 |
|---------------|------|-----------------------------|
| <span data-ttu-id="afb23-137">AdminService</span><span class="sxs-lookup"><span data-stu-id="afb23-137">AdminService</span></span>  | <span data-ttu-id="afb23-138">Łącze</span><span class="sxs-lookup"><span data-stu-id="afb23-138">Link</span></span> | <span data-ttu-id="afb23-139">Identyfikator URI usługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="afb23-139">The admin service URI.</span></span>      |
| <span data-ttu-id="afb23-140">Servicehealth</span><span class="sxs-lookup"><span data-stu-id="afb23-140">ServiceHealth</span></span> | <span data-ttu-id="afb23-141">Łącze</span><span class="sxs-lookup"><span data-stu-id="afb23-141">Link</span></span> | <span data-ttu-id="afb23-142">Identyfikator URI kondycji usługi.</span><span class="sxs-lookup"><span data-stu-id="afb23-142">The service health URI.</span></span>     |
| <span data-ttu-id="afb23-143">Servicebilet</span><span class="sxs-lookup"><span data-stu-id="afb23-143">ServiceTicket</span></span> | <span data-ttu-id="afb23-144">Łącze</span><span class="sxs-lookup"><span data-stu-id="afb23-144">Link</span></span> | <span data-ttu-id="afb23-145">Identyfikator URI biletu usługi.</span><span class="sxs-lookup"><span data-stu-id="afb23-145">The service ticket URI.</span></span>     |
| <span data-ttu-id="afb23-146">Self</span><span class="sxs-lookup"><span data-stu-id="afb23-146">Self</span></span>          | <span data-ttu-id="afb23-147">Łącze</span><span class="sxs-lookup"><span data-stu-id="afb23-147">Link</span></span> | <span data-ttu-id="afb23-148">Własny identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="afb23-148">The self URI.</span></span>               |
| <span data-ttu-id="afb23-149">Następne</span><span class="sxs-lookup"><span data-stu-id="afb23-149">Next</span></span>          | <span data-ttu-id="afb23-150">Łącze</span><span class="sxs-lookup"><span data-stu-id="afb23-150">Link</span></span> | <span data-ttu-id="afb23-151">Następna strona elementów.</span><span class="sxs-lookup"><span data-stu-id="afb23-151">The next page of items.</span></span>     |
| <span data-ttu-id="afb23-152">Poprzednie</span><span class="sxs-lookup"><span data-stu-id="afb23-152">Previous</span></span>      | <span data-ttu-id="afb23-153">Łącze</span><span class="sxs-lookup"><span data-stu-id="afb23-153">Link</span></span> | <span data-ttu-id="afb23-154">Poprzednia strona elementów.</span><span class="sxs-lookup"><span data-stu-id="afb23-154">The previous page of items.</span></span> |

