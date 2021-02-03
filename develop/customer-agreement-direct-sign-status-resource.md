---
title: Stan bezpośredniej rejestracji (bezpośredniego akceptacji) umowy klienta.
description: Zasób DirectSignedCustomerAgreementStatus reprezentuje stan bezpośredniej rejestracji (bezpośrednie zatwierdzenie) umowy klienta.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 9c4fd12ac3319057f3c4034aa0c8d93dcda726c6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767738"
---
# <a name="direct-signing-direct-acceptance-status-of-a-customer-agreement"></a><span data-ttu-id="fc787-103">Status bezpośredniej rejestracji (bezpośredniej akceptacji) umowy klienta</span><span class="sxs-lookup"><span data-stu-id="fc787-103">Direct signing (direct acceptance) status of a customer agreement</span></span>

<span data-ttu-id="fc787-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="fc787-104">**Applies to:**</span></span>

- <span data-ttu-id="fc787-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="fc787-105">Partner Center</span></span>

<span data-ttu-id="fc787-106">Zasób **DirectSignedCustomerAgreementStatus** jest obecnie obsługiwany przez centrum partnerskie tylko w chmurze publicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fc787-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="fc787-107">Ten zasób *nie ma zastosowania* do:</span><span class="sxs-lookup"><span data-stu-id="fc787-107">This resource is *not applicable* to:</span></span>

- <span data-ttu-id="fc787-108">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="fc787-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="fc787-109">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="fc787-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="fc787-110">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="fc787-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="fc787-111">Zasób **DirectSignedCustomerAgreementStatus** reprezentuje stan bezpośredniego akceptacji umowy klienta.</span><span class="sxs-lookup"><span data-stu-id="fc787-111">The **DirectSignedCustomerAgreementStatus** resource represents the status of the direct acceptance of a customer agreement.</span></span>

## <a name="directsignedcustomeragreementstatus"></a><span data-ttu-id="fc787-112">DirectSignedCustomerAgreementStatus</span><span class="sxs-lookup"><span data-stu-id="fc787-112">DirectSignedCustomerAgreementStatus</span></span>

<span data-ttu-id="fc787-113">Zasób **DirectSignedCustomerAgreementStatus** zawiera następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="fc787-113">A **DirectSignedCustomerAgreementStatus** resource includes the following properties:</span></span>

| <span data-ttu-id="fc787-114">Właściwość</span><span class="sxs-lookup"><span data-stu-id="fc787-114">Property</span></span>       | <span data-ttu-id="fc787-115">Typ</span><span class="sxs-lookup"><span data-stu-id="fc787-115">Type</span></span>   | <span data-ttu-id="fc787-116">Opis</span><span class="sxs-lookup"><span data-stu-id="fc787-116">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fc787-117">IsSigned</span><span class="sxs-lookup"><span data-stu-id="fc787-117">isSigned</span></span> | <span data-ttu-id="fc787-118">boolean</span><span class="sxs-lookup"><span data-stu-id="fc787-118">boolean</span></span> | <span data-ttu-id="fc787-119">Wskazuje, czy umowa klienta została bezpośrednio podpisana (zaakceptowana) przez klienta.</span><span class="sxs-lookup"><span data-stu-id="fc787-119">Indicates if the customer agreement has been directly signed (accepted) by the customer.</span></span> |
