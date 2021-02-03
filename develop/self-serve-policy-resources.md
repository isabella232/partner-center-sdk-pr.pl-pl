---
title: Samoobsługowe zasoby zasad
description: Partner ustawia zasady samoobsługowe dla klienta.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 04daf6aaeb69153c4139941188f53dbab8979969
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767842"
---
# <a name="selfservepolicy-resource"></a><span data-ttu-id="8bcd7-103">Zasób SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="8bcd7-103">SelfServePolicy resource</span></span>

<span data-ttu-id="8bcd7-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="8bcd7-104">**Applies to:**</span></span>

- <span data-ttu-id="8bcd7-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="8bcd7-105">Partner Center</span></span>

<span data-ttu-id="8bcd7-106">Partner ustawia zasady samoobsługowe dla klienta.</span><span class="sxs-lookup"><span data-stu-id="8bcd7-106">A partner sets self serve policies for a customer.</span></span>

## <a name="selfservepolicy"></a><span data-ttu-id="8bcd7-107">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="8bcd7-107">SelfServePolicy</span></span>

<span data-ttu-id="8bcd7-108">Opisuje koszyk.</span><span class="sxs-lookup"><span data-stu-id="8bcd7-108">Describes a cart.</span></span>

| <span data-ttu-id="8bcd7-109">Właściwość</span><span class="sxs-lookup"><span data-stu-id="8bcd7-109">Property</span></span>              | <span data-ttu-id="8bcd7-110">Typ</span><span class="sxs-lookup"><span data-stu-id="8bcd7-110">Type</span></span>             | <span data-ttu-id="8bcd7-111">Opis</span><span class="sxs-lookup"><span data-stu-id="8bcd7-111">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8bcd7-112">identyfikator</span><span class="sxs-lookup"><span data-stu-id="8bcd7-112">id</span></span>                    | <span data-ttu-id="8bcd7-113">ciąg</span><span class="sxs-lookup"><span data-stu-id="8bcd7-113">string</span></span>           | <span data-ttu-id="8bcd7-114">Samoobsługowy identyfikator zasad, który jest dostarczany po pomyślnym utworzeniu zasad samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="8bcd7-114">A self serve policy identifier that is supplied upon successful creation of the self serve policy.</span></span>     |
| <span data-ttu-id="8bcd7-115">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="8bcd7-115">SelfServeEntity</span></span>       | <span data-ttu-id="8bcd7-116">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="8bcd7-116">SelfServeEntity</span></span>  | <span data-ttu-id="8bcd7-117">Jednostka samoobsługi, do której uzyskuje się dostęp.</span><span class="sxs-lookup"><span data-stu-id="8bcd7-117">The self serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="8bcd7-118">Użytkownik udzielający uprawnienia</span><span class="sxs-lookup"><span data-stu-id="8bcd7-118">Grantor</span></span>               | <span data-ttu-id="8bcd7-119">Użytkownik udzielający uprawnienia</span><span class="sxs-lookup"><span data-stu-id="8bcd7-119">Grantor</span></span>          | <span data-ttu-id="8bcd7-120">Użytkownik udzielający uprawnienia udzielający dostępu.</span><span class="sxs-lookup"><span data-stu-id="8bcd7-120">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="8bcd7-121">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="8bcd7-121">Permissions</span></span>           | <span data-ttu-id="8bcd7-122">Tablica uprawnień</span><span class="sxs-lookup"><span data-stu-id="8bcd7-122">Array of Permission</span></span>| <span data-ttu-id="8bcd7-123">Tablica zasobów [uprawnień](#permission) .</span><span class="sxs-lookup"><span data-stu-id="8bcd7-123">An Array of [Permission](#permission) resources.</span></span>                                                                     |

## <a name="selfserveentity"></a><span data-ttu-id="8bcd7-124">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="8bcd7-124">SelfServeEntity</span></span>

<span data-ttu-id="8bcd7-125">Reprezentuje przyznany obiekt uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="8bcd7-125">Represents the entity being granted permissions.</span></span>

| <span data-ttu-id="8bcd7-126">Właściwość</span><span class="sxs-lookup"><span data-stu-id="8bcd7-126">Property</span></span>             | <span data-ttu-id="8bcd7-127">Typ</span><span class="sxs-lookup"><span data-stu-id="8bcd7-127">Type</span></span>|<span data-ttu-id="8bcd7-128">Opis</span><span class="sxs-lookup"><span data-stu-id="8bcd7-128">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="8bcd7-129">SelfServeEntityType</span><span class="sxs-lookup"><span data-stu-id="8bcd7-129">SelfServeEntityType</span></span>  | <span data-ttu-id="8bcd7-130">ciąg</span><span class="sxs-lookup"><span data-stu-id="8bcd7-130">string</span></span>                           | <span data-ttu-id="8bcd7-131">Jednostka, której udzielono dostępu, zaakceptowanych wartości: klient.</span><span class="sxs-lookup"><span data-stu-id="8bcd7-131">The entity being granted access, accepted values: Customer.</span></span>                                 |
| <span data-ttu-id="8bcd7-132">TenantID</span><span class="sxs-lookup"><span data-stu-id="8bcd7-132">TenantID</span></span>             | <span data-ttu-id="8bcd7-133">ciąg</span><span class="sxs-lookup"><span data-stu-id="8bcd7-133">string</span></span>                           | <span data-ttu-id="8bcd7-134">Identyfikator dzierżawy jednostki, której udzielono dostępu.</span><span class="sxs-lookup"><span data-stu-id="8bcd7-134">The tenant identifier of the entity being granted access.</span></span>                                   |

## <a name="grantor"></a><span data-ttu-id="8bcd7-135">Użytkownik udzielający uprawnienia</span><span class="sxs-lookup"><span data-stu-id="8bcd7-135">Grantor</span></span>

<span data-ttu-id="8bcd7-136">Reprezentuje użytkownik udzielający uprawnienia przyznającą uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="8bcd7-136">Represents the grantor granting the permissions.</span></span>

| <span data-ttu-id="8bcd7-137">Właściwość</span><span class="sxs-lookup"><span data-stu-id="8bcd7-137">Property</span></span>             | <span data-ttu-id="8bcd7-138">Typ</span><span class="sxs-lookup"><span data-stu-id="8bcd7-138">Type</span></span>|<span data-ttu-id="8bcd7-139">Opis</span><span class="sxs-lookup"><span data-stu-id="8bcd7-139">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="8bcd7-140">GrantorType</span><span class="sxs-lookup"><span data-stu-id="8bcd7-140">GrantorType</span></span>          | <span data-ttu-id="8bcd7-141">ciąg</span><span class="sxs-lookup"><span data-stu-id="8bcd7-141">string</span></span>                           | <span data-ttu-id="8bcd7-142">Użytkownik udzielający uprawnienia udzielanie dostępu, zaakceptowane wartości: BillToPartner.</span><span class="sxs-lookup"><span data-stu-id="8bcd7-142">The grantor granting access, accepted values: BillToPartner.</span></span>                               |
| <span data-ttu-id="8bcd7-143">TenantID</span><span class="sxs-lookup"><span data-stu-id="8bcd7-143">TenantID</span></span>             | <span data-ttu-id="8bcd7-144">ciąg</span><span class="sxs-lookup"><span data-stu-id="8bcd7-144">string</span></span>                           | <span data-ttu-id="8bcd7-145">Identyfikator dzierżawy jednostki, która udziela dostępu.</span><span class="sxs-lookup"><span data-stu-id="8bcd7-145">The tenant identifier of the entity granting access.</span></span>                                       |


## <a name="permission"></a><span data-ttu-id="8bcd7-146">Uprawnienie</span><span class="sxs-lookup"><span data-stu-id="8bcd7-146">Permission</span></span>

<span data-ttu-id="8bcd7-147">Reprezentuje uprawnienie w zasadach samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="8bcd7-147">Represents a permission in the self serve policy.</span></span>

| <span data-ttu-id="8bcd7-148">Właściwość</span><span class="sxs-lookup"><span data-stu-id="8bcd7-148">Property</span></span>             | <span data-ttu-id="8bcd7-149">Typ</span><span class="sxs-lookup"><span data-stu-id="8bcd7-149">Type</span></span>|<span data-ttu-id="8bcd7-150">Opis</span><span class="sxs-lookup"><span data-stu-id="8bcd7-150">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="8bcd7-151">Zasób</span><span class="sxs-lookup"><span data-stu-id="8bcd7-151">Resource</span></span>             | <span data-ttu-id="8bcd7-152">ciąg</span><span class="sxs-lookup"><span data-stu-id="8bcd7-152">string</span></span>                           | <span data-ttu-id="8bcd7-153">Dostęp do zasobu jest przyznany zbyt: AzureReservedInstances.</span><span class="sxs-lookup"><span data-stu-id="8bcd7-153">The resource access is being granted too: AzureReservedInstances.</span></span>                          |
| <span data-ttu-id="8bcd7-154">Akcja</span><span class="sxs-lookup"><span data-stu-id="8bcd7-154">Action</span></span>               | <span data-ttu-id="8bcd7-155">ciąg</span><span class="sxs-lookup"><span data-stu-id="8bcd7-155">string</span></span>                           | <span data-ttu-id="8bcd7-156">Przyznano dostęp do akcji dla: zakup</span><span class="sxs-lookup"><span data-stu-id="8bcd7-156">The action access is being granted for: Purchase</span></span>                                           |
