---
title: Zasoby zasad samoobsługi
description: Partner ustawia zasady samoobsługi dla klienta.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e44581b805e076132984b67280699314e274ca94
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446721"
---
# <a name="selfservepolicy-resource"></a><span data-ttu-id="a35eb-103">Zasób SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="a35eb-103">SelfServePolicy resource</span></span>

<span data-ttu-id="a35eb-104">Partner ustawia zasady samoobsługi dla klienta.</span><span class="sxs-lookup"><span data-stu-id="a35eb-104">A partner sets self serve policies for a customer.</span></span>

## <a name="selfservepolicy"></a><span data-ttu-id="a35eb-105">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="a35eb-105">SelfServePolicy</span></span>

<span data-ttu-id="a35eb-106">Opisuje koszyk.</span><span class="sxs-lookup"><span data-stu-id="a35eb-106">Describes a cart.</span></span>

| <span data-ttu-id="a35eb-107">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a35eb-107">Property</span></span>              | <span data-ttu-id="a35eb-108">Typ</span><span class="sxs-lookup"><span data-stu-id="a35eb-108">Type</span></span>             | <span data-ttu-id="a35eb-109">Opis</span><span class="sxs-lookup"><span data-stu-id="a35eb-109">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a35eb-110">identyfikator</span><span class="sxs-lookup"><span data-stu-id="a35eb-110">id</span></span>                    | <span data-ttu-id="a35eb-111">ciąg</span><span class="sxs-lookup"><span data-stu-id="a35eb-111">string</span></span>           | <span data-ttu-id="a35eb-112">Identyfikator zasad samoobsługi, który jest dostarczany po pomyślnym utworzeniu zasad samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="a35eb-112">A self-serve policy identifier that is supplied upon successful creation of the self serve policy.</span></span>     |
| <span data-ttu-id="a35eb-113">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="a35eb-113">SelfServeEntity</span></span>       | <span data-ttu-id="a35eb-114">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="a35eb-114">SelfServeEntity</span></span>  | <span data-ttu-id="a35eb-115">Jednostka samoobsługowa, która ma udzielany dostęp.</span><span class="sxs-lookup"><span data-stu-id="a35eb-115">The self serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="a35eb-116">Grantor</span><span class="sxs-lookup"><span data-stu-id="a35eb-116">Grantor</span></span>               | <span data-ttu-id="a35eb-117">Grantor</span><span class="sxs-lookup"><span data-stu-id="a35eb-117">Grantor</span></span>          | <span data-ttu-id="a35eb-118">Grantor, który udziela dostępu.</span><span class="sxs-lookup"><span data-stu-id="a35eb-118">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="a35eb-119">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="a35eb-119">Permissions</span></span>           | <span data-ttu-id="a35eb-120">Tablica uprawnień</span><span class="sxs-lookup"><span data-stu-id="a35eb-120">Array of Permission</span></span>| <span data-ttu-id="a35eb-121">Tablica [zasobów](#permission) uprawnień.</span><span class="sxs-lookup"><span data-stu-id="a35eb-121">An Array of [Permission](#permission) resources.</span></span>                                                                     |

## <a name="selfserveentity"></a><span data-ttu-id="a35eb-122">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="a35eb-122">SelfServeEntity</span></span>

<span data-ttu-id="a35eb-123">Reprezentuje jednostkę, która ma przyznane uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="a35eb-123">Represents the entity being granted permissions.</span></span>

| <span data-ttu-id="a35eb-124">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a35eb-124">Property</span></span>             | <span data-ttu-id="a35eb-125">Typ</span><span class="sxs-lookup"><span data-stu-id="a35eb-125">Type</span></span>|<span data-ttu-id="a35eb-126">Opis</span><span class="sxs-lookup"><span data-stu-id="a35eb-126">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="a35eb-127">SelfServeEntityType</span><span class="sxs-lookup"><span data-stu-id="a35eb-127">SelfServeEntityType</span></span>  | <span data-ttu-id="a35eb-128">ciąg</span><span class="sxs-lookup"><span data-stu-id="a35eb-128">string</span></span>                           | <span data-ttu-id="a35eb-129">Jednostka, do których jest udzielany dostęp, zaakceptowane wartości: Klient.</span><span class="sxs-lookup"><span data-stu-id="a35eb-129">The entity being granted access, accepted values: Customer.</span></span>                                 |
| <span data-ttu-id="a35eb-130">TenantID</span><span class="sxs-lookup"><span data-stu-id="a35eb-130">TenantID</span></span>             | <span data-ttu-id="a35eb-131">ciąg</span><span class="sxs-lookup"><span data-stu-id="a35eb-131">string</span></span>                           | <span data-ttu-id="a35eb-132">Identyfikator dzierżawy jednostki, do których jest udzielany dostęp.</span><span class="sxs-lookup"><span data-stu-id="a35eb-132">The tenant identifier of the entity being granted access.</span></span>                                   |

## <a name="grantor"></a><span data-ttu-id="a35eb-133">Grantor</span><span class="sxs-lookup"><span data-stu-id="a35eb-133">Grantor</span></span>

<span data-ttu-id="a35eb-134">Reprezentuje grantor udzielanie uprawnień.</span><span class="sxs-lookup"><span data-stu-id="a35eb-134">Represents the grantor granting the permissions.</span></span>

| <span data-ttu-id="a35eb-135">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a35eb-135">Property</span></span>             | <span data-ttu-id="a35eb-136">Typ</span><span class="sxs-lookup"><span data-stu-id="a35eb-136">Type</span></span>|<span data-ttu-id="a35eb-137">Opis</span><span class="sxs-lookup"><span data-stu-id="a35eb-137">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="a35eb-138">GrantorType</span><span class="sxs-lookup"><span data-stu-id="a35eb-138">GrantorType</span></span>          | <span data-ttu-id="a35eb-139">ciąg</span><span class="sxs-lookup"><span data-stu-id="a35eb-139">string</span></span>                           | <span data-ttu-id="a35eb-140">Grantor, który udziela dostępu, zaakceptowane wartości: BillToPartner.</span><span class="sxs-lookup"><span data-stu-id="a35eb-140">The grantor granting access, accepted values: BillToPartner.</span></span>                               |
| <span data-ttu-id="a35eb-141">TenantID</span><span class="sxs-lookup"><span data-stu-id="a35eb-141">TenantID</span></span>             | <span data-ttu-id="a35eb-142">ciąg</span><span class="sxs-lookup"><span data-stu-id="a35eb-142">string</span></span>                           | <span data-ttu-id="a35eb-143">Identyfikator dzierżawy jednostki, która udziela dostępu.</span><span class="sxs-lookup"><span data-stu-id="a35eb-143">The tenant identifier of the entity granting access.</span></span>                                       |


## <a name="permission"></a><span data-ttu-id="a35eb-144">Uprawnienie</span><span class="sxs-lookup"><span data-stu-id="a35eb-144">Permission</span></span>

<span data-ttu-id="a35eb-145">Reprezentuje uprawnienie w zasadach samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="a35eb-145">Represents a permission in the self serve policy.</span></span>

| <span data-ttu-id="a35eb-146">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a35eb-146">Property</span></span>             | <span data-ttu-id="a35eb-147">Typ</span><span class="sxs-lookup"><span data-stu-id="a35eb-147">Type</span></span>|<span data-ttu-id="a35eb-148">Opis</span><span class="sxs-lookup"><span data-stu-id="a35eb-148">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="a35eb-149">Zasób</span><span class="sxs-lookup"><span data-stu-id="a35eb-149">Resource</span></span>             | <span data-ttu-id="a35eb-150">ciąg</span><span class="sxs-lookup"><span data-stu-id="a35eb-150">string</span></span>                           | <span data-ttu-id="a35eb-151">Udzielany jest również dostęp do zasobów: AzureReservedInstances.</span><span class="sxs-lookup"><span data-stu-id="a35eb-151">The resource access is being granted too: AzureReservedInstances.</span></span>                          |
| <span data-ttu-id="a35eb-152">Akcja</span><span class="sxs-lookup"><span data-stu-id="a35eb-152">Action</span></span>               | <span data-ttu-id="a35eb-153">ciąg</span><span class="sxs-lookup"><span data-stu-id="a35eb-153">string</span></span>                           | <span data-ttu-id="a35eb-154">Udzielany jest dostęp do akcji: Zakup</span><span class="sxs-lookup"><span data-stu-id="a35eb-154">The action access is being granted for: Purchase</span></span>                                           |
