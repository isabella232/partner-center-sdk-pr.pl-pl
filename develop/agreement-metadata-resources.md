---
title: Zasoby metadanych umowy
description: Kolekcja zasobów AgreementMetadata zawiera informacje o typach umów, które partnerzy mogą wykorzystać w celu potwierdzenia akceptacji klienta.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 36ba2aa2f78552dc9a835168b5bbd5b6a3ce47f3
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767766"
---
# <a name="agreement-metadata-resources"></a><span data-ttu-id="d2142-103">Zasoby metadanych umowy</span><span class="sxs-lookup"><span data-stu-id="d2142-103">Agreement metadata resources</span></span>

<span data-ttu-id="d2142-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="d2142-104">**Applies to:**</span></span>

- <span data-ttu-id="d2142-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="d2142-105">Partner Center</span></span>

<span data-ttu-id="d2142-106">Zasób **AgreementMetaData** jest obecnie obsługiwany przez centrum partnerskie tylko w *chmurze publicznej firmy Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="d2142-106">The **AgreementMetaData** resource is currently supported by Partner Center only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="d2142-107">Ten zasób nie ma zastosowania do:</span><span class="sxs-lookup"><span data-stu-id="d2142-107">This resource isn't applicable to:</span></span>

- <span data-ttu-id="d2142-108">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="d2142-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="d2142-109">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="d2142-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="d2142-110">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d2142-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d2142-111">Kolekcja **AgreementMetaData** zawiera metadane dotyczące wszystkich typów umów.</span><span class="sxs-lookup"><span data-stu-id="d2142-111">The **AgreementMetaData** collection provides metadata about all the agreement types.</span></span> <span data-ttu-id="d2142-112">Partnerzy mogą korzystać z tej kolekcji w celu potwierdzenia akceptacji umów przez klienta.</span><span class="sxs-lookup"><span data-stu-id="d2142-112">Partners can use this collection to provide confirmation of customer acceptance of agreements.</span></span> <span data-ttu-id="d2142-113">Kolekcja **AgreementMetaData** zwraca metadane dla obu typów umów (**Umowa Microsoft Cloud** i **Umowa klienta firmy Microsoft**).</span><span class="sxs-lookup"><span data-stu-id="d2142-113">The **AgreementMetaData** collection returns metadata for both agreement types (**Microsoft Cloud Agreement** and **Microsoft Customer Agreement**).</span></span>

## <a name="agreementmetadata"></a><span data-ttu-id="d2142-114">AgreementMetaData</span><span class="sxs-lookup"><span data-stu-id="d2142-114">AgreementMetaData</span></span>

<span data-ttu-id="d2142-115">Zwrócone metadane umowy obejmują następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="d2142-115">Agreement metadata returned includes the following properties:</span></span>

| <span data-ttu-id="d2142-116">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d2142-116">Property</span></span>      | <span data-ttu-id="d2142-117">Typ</span><span class="sxs-lookup"><span data-stu-id="d2142-117">Type</span></span>               | <span data-ttu-id="d2142-118">Opis</span><span class="sxs-lookup"><span data-stu-id="d2142-118">Description</span></span>                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| <span data-ttu-id="d2142-119">templateId</span><span class="sxs-lookup"><span data-stu-id="d2142-119">templateId</span></span>    | <span data-ttu-id="d2142-120">ciąg</span><span class="sxs-lookup"><span data-stu-id="d2142-120">string</span></span>             | <span data-ttu-id="d2142-121">Unikatowy identyfikator szablonu umowy.</span><span class="sxs-lookup"><span data-stu-id="d2142-121">Unique identifier of an agreement template.</span></span>                                       |
| <span data-ttu-id="d2142-122">typ</span><span class="sxs-lookup"><span data-stu-id="d2142-122">type</span></span>          | <span data-ttu-id="d2142-123">ciąg</span><span class="sxs-lookup"><span data-stu-id="d2142-123">string</span></span>             | <span data-ttu-id="d2142-124">Typ umowy.</span><span class="sxs-lookup"><span data-stu-id="d2142-124">Agreement type.</span></span> <span data-ttu-id="d2142-125">Obecnie obsługiwane wartości to **MicrosoftCloudAgreement** i **MicrosoftCustomerAgreement** (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="d2142-125">Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement** (preview).</span></span> |
| <span data-ttu-id="d2142-126">agreementLink</span><span class="sxs-lookup"><span data-stu-id="d2142-126">agreementLink</span></span> | <span data-ttu-id="d2142-127">ciąg</span><span class="sxs-lookup"><span data-stu-id="d2142-127">string</span></span>             | <span data-ttu-id="d2142-128">Adres URL szablonu umowy.</span><span class="sxs-lookup"><span data-stu-id="d2142-128">URL for the agreement template.</span></span>                                                    |
