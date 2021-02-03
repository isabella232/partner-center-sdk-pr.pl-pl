---
title: Zasoby dokumentu umowy
description: Zasób AgreementDocument jest dokumentem umowy firmy Microsoft na potrzeby wersji zapoznawczej i pobierania. Jest ona obsługiwana przez centrum partnerskie w chmurze publicznej firmy Microsoft.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 4805d25b0838bf922b81bebd998810c3f6a809c3
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768561"
---
# <a name="agreement-document-resources-supported-by-partner-center-in-the-microsoft-public-cloud"></a><span data-ttu-id="845e3-104">Zasoby dokumentu umowy obsługiwane przez centrum partnerskie w chmurze publicznej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="845e3-104">Agreement document resources supported by Partner Center in the Microsoft public cloud</span></span>

<span data-ttu-id="845e3-105">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="845e3-105">**Applies to:**</span></span>

- <span data-ttu-id="845e3-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="845e3-106">Partner Center</span></span>

<span data-ttu-id="845e3-107">Zasób **AgreementDocument** jest obecnie obsługiwany przez centrum partnerskie tylko w *chmurze publicznej firmy Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="845e3-107">The **AgreementDocument** resource is currently supported by Partner Center only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="845e3-108">Ten zasób nie ma zastosowania do:</span><span class="sxs-lookup"><span data-stu-id="845e3-108">This resource not applicable to:</span></span>

- <span data-ttu-id="845e3-109">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="845e3-109">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="845e3-110">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="845e3-110">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="845e3-111">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="845e3-111">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="845e3-112">Zasób **AgreementDocument** reprezentuje dokument umowy Microsoft, który jest dostępny do zaprezentowania i pobrania.</span><span class="sxs-lookup"><span data-stu-id="845e3-112">The **AgreementDocument** resource represents a Microsoft agreement document that is available for preview and download.</span></span>

## <a name="agreementdocument"></a><span data-ttu-id="845e3-113">AgreementDocument</span><span class="sxs-lookup"><span data-stu-id="845e3-113">AgreementDocument</span></span>

<span data-ttu-id="845e3-114">Zasób **AgreementDocument** zawiera następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="845e3-114">An **AgreementDocument** resource includes the following properties:</span></span>

| <span data-ttu-id="845e3-115">Właściwość</span><span class="sxs-lookup"><span data-stu-id="845e3-115">Property</span></span>       | <span data-ttu-id="845e3-116">Typ</span><span class="sxs-lookup"><span data-stu-id="845e3-116">Type</span></span>   | <span data-ttu-id="845e3-117">Opis</span><span class="sxs-lookup"><span data-stu-id="845e3-117">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="845e3-118">country</span><span class="sxs-lookup"><span data-stu-id="845e3-118">country</span></span> | <span data-ttu-id="845e3-119">ciąg</span><span class="sxs-lookup"><span data-stu-id="845e3-119">string</span></span> | <span data-ttu-id="845e3-120">Kraj lub rynek, do którego odnosi się ten dokument.</span><span class="sxs-lookup"><span data-stu-id="845e3-120">The country or market to which this document applies.</span></span> |
| <span data-ttu-id="845e3-121">language</span><span class="sxs-lookup"><span data-stu-id="845e3-121">language</span></span> | <span data-ttu-id="845e3-122">ciąg</span><span class="sxs-lookup"><span data-stu-id="845e3-122">string</span></span> | <span data-ttu-id="845e3-123">Język, w którym znajduje się ten dokument.</span><span class="sxs-lookup"><span data-stu-id="845e3-123">The language in which this document is localized.</span></span> |
| <span data-ttu-id="845e3-124">displayUri</span><span class="sxs-lookup"><span data-stu-id="845e3-124">displayUri</span></span> | <span data-ttu-id="845e3-125">ciąg</span><span class="sxs-lookup"><span data-stu-id="845e3-125">string</span></span> | <span data-ttu-id="845e3-126">Link umożliwiający wyświetlenie podglądu dokumentu umowy w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="845e3-126">A link to preview the agreement document in a browser.</span></span>  |
| <span data-ttu-id="845e3-127">downloadUri</span><span class="sxs-lookup"><span data-stu-id="845e3-127">downloadUri</span></span> |<span data-ttu-id="845e3-128">ciąg</span><span class="sxs-lookup"><span data-stu-id="845e3-128">string</span></span> | <span data-ttu-id="845e3-129">Link umożliwiający pobranie dokumentu umowy (w formacie programu Microsoft Word).</span><span class="sxs-lookup"><span data-stu-id="845e3-129">A link to download the agreement document (in Microsoft Word format).</span></span> |
