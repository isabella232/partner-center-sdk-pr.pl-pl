---
title: Przenoszenie zasobów uprawnień
description: Partner może utworzyć przeniesienie, gdy klient zażąda, aby jego subskrypcja została przeniesiona do innego partnera.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8f121d499abffb4c4dda688c2a91c25f83d2e863
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530212"
---
# <a name="transfereligibility-resources"></a><span data-ttu-id="4e106-103">Przenoszenie zasobów uprawnień</span><span class="sxs-lookup"><span data-stu-id="4e106-103">TransferEligibility resources</span></span>

<span data-ttu-id="4e106-104">Partner może utworzyć przeniesienie, gdy klient zażąda, aby jego subskrypcja została przeniesiona do innego partnera.</span><span class="sxs-lookup"><span data-stu-id="4e106-104">A partner can create a transfer when a customer requests their subscription with the partner to be transferred to another partner.</span></span> <span data-ttu-id="4e106-105">Użyj uprawnienia do przeniesienia, aby sprawdzić, czy subskrypcja kwalifikuje się do przeniesienia.</span><span class="sxs-lookup"><span data-stu-id="4e106-105">Use TransferEligibility to check whether a subscription is eligible to be transferred.</span></span>

## <a name="transfereligibility"></a><span data-ttu-id="4e106-106">Uprawnienia do przeniesienia</span><span class="sxs-lookup"><span data-stu-id="4e106-106">TransferEligibility</span></span>

<span data-ttu-id="4e106-107">Opisuje uprawnienie do przeniesienia.</span><span class="sxs-lookup"><span data-stu-id="4e106-107">Describes a transferEligibility.</span></span>

| <span data-ttu-id="4e106-108">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4e106-108">Property</span></span>              | <span data-ttu-id="4e106-109">Typ</span><span class="sxs-lookup"><span data-stu-id="4e106-109">Type</span></span>             | <span data-ttu-id="4e106-110">Opis</span><span class="sxs-lookup"><span data-stu-id="4e106-110">Description</span></span>                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="4e106-111">identyfikator</span><span class="sxs-lookup"><span data-stu-id="4e106-111">id</span></span>                    | <span data-ttu-id="4e106-112">ciąg</span><span class="sxs-lookup"><span data-stu-id="4e106-112">string</span></span>           | <span data-ttu-id="4e106-113">Identyfikator subskrypcji klienta.</span><span class="sxs-lookup"><span data-stu-id="4e106-113">The customer's subscription identifier.</span></span>                                                  |
| <span data-ttu-id="4e106-114">isEligible</span><span class="sxs-lookup"><span data-stu-id="4e106-114">isEligible</span></span>            | <span data-ttu-id="4e106-115">bool</span><span class="sxs-lookup"><span data-stu-id="4e106-115">bool</span></span>             | <span data-ttu-id="4e106-116">Wskazuje, czy subskrypcja kwalifikuje się do przeniesienia.</span><span class="sxs-lookup"><span data-stu-id="4e106-116">Indicates whether the subscription is eligible for the transfer.</span></span>                         |
| <span data-ttu-id="4e106-117">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="4e106-117">Reason</span></span>                | <span data-ttu-id="4e106-118">ciąg</span><span class="sxs-lookup"><span data-stu-id="4e106-118">string</span></span>           | <span data-ttu-id="4e106-119">Właściwość przyczyny wyjaśnia, dlaczego subskrypcja nie kwalifikuje się do przeniesienia.</span><span class="sxs-lookup"><span data-stu-id="4e106-119">The reason property explains why the subscription isn't eligible for transfer.</span></span> |