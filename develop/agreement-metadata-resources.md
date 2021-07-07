---
title: Zasoby metadanych umowy
description: Kolekcja zasobów AgreementMetadata opisuje typy umów, których partnerzy mogą używać do potwierdzania akceptacji przez klientów.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: b930e3691b9d269ddb8d76ae18b6b26a217123c0
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025635"
---
# <a name="agreement-metadata-resources"></a><span data-ttu-id="b1e24-103">Zasoby metadanych umowy</span><span class="sxs-lookup"><span data-stu-id="b1e24-103">Agreement metadata resources</span></span>

<span data-ttu-id="b1e24-104">**Dotyczy:** Partner Center</span><span class="sxs-lookup"><span data-stu-id="b1e24-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="b1e24-105">**Nie dotyczy:** Partner Center obsługiwane przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b1e24-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b1e24-106">Zasób **AgreementMetaData** jest obecnie obsługiwany Partner Center tylko w chmurze publicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b1e24-106">The **AgreementMetaData** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span> 

<span data-ttu-id="b1e24-107">Kolekcja **AgreementMetaData** udostępnia metadane dotyczące wszystkich typów umów.</span><span class="sxs-lookup"><span data-stu-id="b1e24-107">The **AgreementMetaData** collection provides metadata about all the agreement types.</span></span> <span data-ttu-id="b1e24-108">Partnerzy mogą użyć tej kolekcji, aby potwierdzić akceptację umów przez klienta.</span><span class="sxs-lookup"><span data-stu-id="b1e24-108">Partners can use this collection to provide confirmation of customer acceptance of agreements.</span></span> <span data-ttu-id="b1e24-109">Kolekcja **AgreementMetaData** zwraca metadane dla obu typów umów **(** Umowa dotycząca platformy Microsoft Cloud i **Umowa z Klientem Microsoft**).</span><span class="sxs-lookup"><span data-stu-id="b1e24-109">The **AgreementMetaData** collection returns metadata for both agreement types (**Microsoft Cloud Agreement** and **Microsoft Customer Agreement**).</span></span>

## <a name="agreementmetadata"></a><span data-ttu-id="b1e24-110">AgreementMetaData</span><span class="sxs-lookup"><span data-stu-id="b1e24-110">AgreementMetaData</span></span>

<span data-ttu-id="b1e24-111">Zwrócone metadane umowy obejmują następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="b1e24-111">Agreement metadata returned includes the following properties:</span></span>

| <span data-ttu-id="b1e24-112">Właściwość</span><span class="sxs-lookup"><span data-stu-id="b1e24-112">Property</span></span>      | <span data-ttu-id="b1e24-113">Typ</span><span class="sxs-lookup"><span data-stu-id="b1e24-113">Type</span></span>               | <span data-ttu-id="b1e24-114">Opis</span><span class="sxs-lookup"><span data-stu-id="b1e24-114">Description</span></span>                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| <span data-ttu-id="b1e24-115">templateId</span><span class="sxs-lookup"><span data-stu-id="b1e24-115">templateId</span></span>    | <span data-ttu-id="b1e24-116">ciąg</span><span class="sxs-lookup"><span data-stu-id="b1e24-116">string</span></span>             | <span data-ttu-id="b1e24-117">Unikatowy identyfikator szablonu umowy.</span><span class="sxs-lookup"><span data-stu-id="b1e24-117">Unique identifier of an agreement template.</span></span>                                       |
| <span data-ttu-id="b1e24-118">typ</span><span class="sxs-lookup"><span data-stu-id="b1e24-118">type</span></span>          | <span data-ttu-id="b1e24-119">ciąg</span><span class="sxs-lookup"><span data-stu-id="b1e24-119">string</span></span>             | <span data-ttu-id="b1e24-120">Typ umowy.</span><span class="sxs-lookup"><span data-stu-id="b1e24-120">Agreement type.</span></span> <span data-ttu-id="b1e24-121">Obecnie obsługiwane wartości to **MicrosoftCloudAgreement** i **MicrosoftCustomerAgreement** (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="b1e24-121">Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement** (preview).</span></span> |
| <span data-ttu-id="b1e24-122">agreementLink</span><span class="sxs-lookup"><span data-stu-id="b1e24-122">agreementLink</span></span> | <span data-ttu-id="b1e24-123">ciąg</span><span class="sxs-lookup"><span data-stu-id="b1e24-123">string</span></span>             | <span data-ttu-id="b1e24-124">Adres URL szablonu umowy.</span><span class="sxs-lookup"><span data-stu-id="b1e24-124">URL for the agreement template.</span></span>                                                    |
