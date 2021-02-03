---
title: Relacje zasobów
description: Opisuje zasoby związane z relacjami.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c5701414bd704b375dc23859b920609d5a975d9f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767793"
---
# <a name="relationships-resources"></a><span data-ttu-id="c2489-103">Relacje zasobów</span><span class="sxs-lookup"><span data-stu-id="c2489-103">Relationships resources</span></span>

<span data-ttu-id="c2489-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="c2489-104">**Applies To**</span></span>

- <span data-ttu-id="c2489-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="c2489-105">Partner Center</span></span>

<span data-ttu-id="c2489-106">Opisuje zasoby związane z relacjami.</span><span class="sxs-lookup"><span data-stu-id="c2489-106">Describes resources related to relationships.</span></span>

## <a name="partnerrelationship"></a><span data-ttu-id="c2489-107">PartnerRelationship</span><span class="sxs-lookup"><span data-stu-id="c2489-107">PartnerRelationship</span></span>

<span data-ttu-id="c2489-108">Reprezentuje relację między dwoma partnerami.</span><span class="sxs-lookup"><span data-stu-id="c2489-108">Represents a relationship between two partners.</span></span>

| <span data-ttu-id="c2489-109">Właściwość</span><span class="sxs-lookup"><span data-stu-id="c2489-109">Property</span></span>         | <span data-ttu-id="c2489-110">Typ</span><span class="sxs-lookup"><span data-stu-id="c2489-110">Type</span></span>                                                           | <span data-ttu-id="c2489-111">Opis</span><span class="sxs-lookup"><span data-stu-id="c2489-111">Description</span></span>                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c2489-112">identyfikator</span><span class="sxs-lookup"><span data-stu-id="c2489-112">id</span></span>               | <span data-ttu-id="c2489-113">ciąg</span><span class="sxs-lookup"><span data-stu-id="c2489-113">string</span></span>                                                         | <span data-ttu-id="c2489-114">Identyfikator partnera.</span><span class="sxs-lookup"><span data-stu-id="c2489-114">The partner identifier.</span></span> <span data-ttu-id="c2489-115">Identyfikator partnera określa identyfikator dzierżawcy partnera, który znajduje się w relacji odbiorcy (od).</span><span class="sxs-lookup"><span data-stu-id="c2489-115">The partner identifier specifies the tenant id of the partner who is in the recipient (from) side of the relationship.</span></span> |
| <span data-ttu-id="c2489-116">location</span><span class="sxs-lookup"><span data-stu-id="c2489-116">location</span></span>         | <span data-ttu-id="c2489-117">ciąg</span><span class="sxs-lookup"><span data-stu-id="c2489-117">string</span></span>                                                         | <span data-ttu-id="c2489-118">Lokalizacja partnera.</span><span class="sxs-lookup"><span data-stu-id="c2489-118">The location of the partner.</span></span>                                                                                                                   |
| <span data-ttu-id="c2489-119">mpnId</span><span class="sxs-lookup"><span data-stu-id="c2489-119">mpnId</span></span>            | <span data-ttu-id="c2489-120">ciąg</span><span class="sxs-lookup"><span data-stu-id="c2489-120">string</span></span>                                                         | <span data-ttu-id="c2489-121">Identyfikator Microsoft Partner Network (MPN) partnera.</span><span class="sxs-lookup"><span data-stu-id="c2489-121">The Microsoft Partner Network (MPN) identifier of the partner.</span></span>                                                                                 |
| <span data-ttu-id="c2489-122">name</span><span class="sxs-lookup"><span data-stu-id="c2489-122">name</span></span>             | <span data-ttu-id="c2489-123">ciąg</span><span class="sxs-lookup"><span data-stu-id="c2489-123">string</span></span>                                                         | <span data-ttu-id="c2489-124">Nazwa partnera.</span><span class="sxs-lookup"><span data-stu-id="c2489-124">The name of the partner.</span></span>                                                                                                                       |
| <span data-ttu-id="c2489-125">Atrybut</span><span class="sxs-lookup"><span data-stu-id="c2489-125">relationshipType</span></span> | <span data-ttu-id="c2489-126">ciąg</span><span class="sxs-lookup"><span data-stu-id="c2489-126">string</span></span>                                                         | <span data-ttu-id="c2489-127">Typ relacji.</span><span class="sxs-lookup"><span data-stu-id="c2489-127">The type of relationship.</span></span>                                                                                                                      |
| <span data-ttu-id="c2489-128">stan</span><span class="sxs-lookup"><span data-stu-id="c2489-128">state</span></span>            | <span data-ttu-id="c2489-129">ciąg</span><span class="sxs-lookup"><span data-stu-id="c2489-129">string</span></span>                                                         | <span data-ttu-id="c2489-130">Stan relacji (na przykład `active` ).</span><span class="sxs-lookup"><span data-stu-id="c2489-130">The state of the relationship (for example `active`).</span></span>                                                                                                 |
| <span data-ttu-id="c2489-131">atrybuty</span><span class="sxs-lookup"><span data-stu-id="c2489-131">attributes</span></span>       | [<span data-ttu-id="c2489-132">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="c2489-132">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="c2489-133">Atrybuty metadanych.</span><span class="sxs-lookup"><span data-stu-id="c2489-133">The metadata attributes.</span></span>                                                                                                                       |

## <a name="relationshiprequest"></a><span data-ttu-id="c2489-134">RelationshipRequest</span><span class="sxs-lookup"><span data-stu-id="c2489-134">RelationshipRequest</span></span>

<span data-ttu-id="c2489-135">Określa adres URL, za pomocą którego klient może ustanowić relację z partnerem.</span><span class="sxs-lookup"><span data-stu-id="c2489-135">Provides the URL by which a customer can establish a relationship with a partner.</span></span>

| <span data-ttu-id="c2489-136">Właściwość</span><span class="sxs-lookup"><span data-stu-id="c2489-136">Property</span></span>   | <span data-ttu-id="c2489-137">Typ</span><span class="sxs-lookup"><span data-stu-id="c2489-137">Type</span></span>                                                           | <span data-ttu-id="c2489-138">Opis</span><span class="sxs-lookup"><span data-stu-id="c2489-138">Description</span></span>                   |
|------------|----------------------------------------------------------------|-------------------------------|
| <span data-ttu-id="c2489-139">url</span><span class="sxs-lookup"><span data-stu-id="c2489-139">url</span></span>        | <span data-ttu-id="c2489-140">ciąg</span><span class="sxs-lookup"><span data-stu-id="c2489-140">string</span></span>                                                         | <span data-ttu-id="c2489-141">Adres URL żądania relacji.</span><span class="sxs-lookup"><span data-stu-id="c2489-141">The relationship request URL.</span></span> |
| <span data-ttu-id="c2489-142">atrybuty</span><span class="sxs-lookup"><span data-stu-id="c2489-142">attributes</span></span> | [<span data-ttu-id="c2489-143">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="c2489-143">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="c2489-144">Atrybuty metadanych.</span><span class="sxs-lookup"><span data-stu-id="c2489-144">The metadata attributes.</span></span>      |
