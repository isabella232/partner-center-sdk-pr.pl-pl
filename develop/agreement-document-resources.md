---
title: Umowa z zasobami dokumentów
description: Zasób AgreementDocument to dokument umowy firmy Microsoft do pobrania i wersji zapoznawczej. Jest ona obsługiwana przez Partner Center w chmurze publicznej firmy Microsoft.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 1a81da4f75594f241669db831125bd437872561c
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025670"
---
# <a name="agreement-document-resources-supported-by-partner-center-in-the-microsoft-public-cloud"></a><span data-ttu-id="9135a-104">Umowa z zasobami dokumentów obsługiwanymi Partner Center w chmurze publicznej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="9135a-104">Agreement document resources supported by Partner Center in the Microsoft public cloud</span></span>

<span data-ttu-id="9135a-105">**Dotyczy:** Partner Center</span><span class="sxs-lookup"><span data-stu-id="9135a-105">**Applies to**: Partner Center</span></span>

<span data-ttu-id="9135a-106">**Nie dotyczy:** Partner Center obsługiwane przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9135a-106">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9135a-107">Zasób **AgreementDocument** jest obecnie obsługiwany Partner Center tylko w chmurze publicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9135a-107">The **AgreementDocument** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="9135a-108">Zasób **AgreementDocument** reprezentuje dokument umowy firmy Microsoft, który jest dostępny do podglądu i pobrania.</span><span class="sxs-lookup"><span data-stu-id="9135a-108">The **AgreementDocument** resource represents a Microsoft agreement document that is available for preview and download.</span></span>

## <a name="agreementdocument"></a><span data-ttu-id="9135a-109">AgreementDocument</span><span class="sxs-lookup"><span data-stu-id="9135a-109">AgreementDocument</span></span>

<span data-ttu-id="9135a-110">Zasób **AgreementDocument** zawiera następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="9135a-110">An **AgreementDocument** resource includes the following properties:</span></span>

| <span data-ttu-id="9135a-111">Właściwość</span><span class="sxs-lookup"><span data-stu-id="9135a-111">Property</span></span>       | <span data-ttu-id="9135a-112">Typ</span><span class="sxs-lookup"><span data-stu-id="9135a-112">Type</span></span>   | <span data-ttu-id="9135a-113">Opis</span><span class="sxs-lookup"><span data-stu-id="9135a-113">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9135a-114">country</span><span class="sxs-lookup"><span data-stu-id="9135a-114">country</span></span> | <span data-ttu-id="9135a-115">ciąg</span><span class="sxs-lookup"><span data-stu-id="9135a-115">string</span></span> | <span data-ttu-id="9135a-116">Kraj lub rynek, do którego ma zastosowanie ten dokument.</span><span class="sxs-lookup"><span data-stu-id="9135a-116">The country or market to which this document applies.</span></span> |
| <span data-ttu-id="9135a-117">language</span><span class="sxs-lookup"><span data-stu-id="9135a-117">language</span></span> | <span data-ttu-id="9135a-118">ciąg</span><span class="sxs-lookup"><span data-stu-id="9135a-118">string</span></span> | <span data-ttu-id="9135a-119">Język, w którym zlokalizowany jest ten dokument.</span><span class="sxs-lookup"><span data-stu-id="9135a-119">The language in which this document is localized.</span></span> |
| <span data-ttu-id="9135a-120">displayUri</span><span class="sxs-lookup"><span data-stu-id="9135a-120">displayUri</span></span> | <span data-ttu-id="9135a-121">ciąg</span><span class="sxs-lookup"><span data-stu-id="9135a-121">string</span></span> | <span data-ttu-id="9135a-122">Link do podglądu dokumentu umowy w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="9135a-122">A link to preview the agreement document in a browser.</span></span>  |
| <span data-ttu-id="9135a-123">downloadUri</span><span class="sxs-lookup"><span data-stu-id="9135a-123">downloadUri</span></span> |<span data-ttu-id="9135a-124">ciąg</span><span class="sxs-lookup"><span data-stu-id="9135a-124">string</span></span> | <span data-ttu-id="9135a-125">Link do pobrania dokumentu umowy (w Microsoft Word formacie).</span><span class="sxs-lookup"><span data-stu-id="9135a-125">A link to download the agreement document (in Microsoft Word format).</span></span> |
