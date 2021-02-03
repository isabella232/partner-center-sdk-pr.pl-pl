---
title: Zasoby TransferEligibility
description: Partner tworzy transfer, gdy klient chce przenieść swoją subskrypcję do innego partnera.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dcac5724a1f708bc540a3aac7ce74b2eda60a296
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767849"
---
# <a name="transfereligibility-resources"></a><span data-ttu-id="54bf6-103">Zasoby TransferEligibility</span><span class="sxs-lookup"><span data-stu-id="54bf6-103">TransferEligibility resources</span></span>

<span data-ttu-id="54bf6-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="54bf6-104">**Applies to:**</span></span>

- <span data-ttu-id="54bf6-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="54bf6-105">Partner Center</span></span>

<span data-ttu-id="54bf6-106">Partner tworzy transfer, gdy klient chce przenieść swoją subskrypcję do innego partnera.</span><span class="sxs-lookup"><span data-stu-id="54bf6-106">A partner creates a transfer when a customer wants their subscription with the partner to be transferred to another partner.</span></span>

## <a name="transfereligibility"></a><span data-ttu-id="54bf6-107">TransferEligibility</span><span class="sxs-lookup"><span data-stu-id="54bf6-107">TransferEligibility</span></span>

<span data-ttu-id="54bf6-108">Opisuje transferEligibility.</span><span class="sxs-lookup"><span data-stu-id="54bf6-108">Describes a transferEligibility.</span></span>

| <span data-ttu-id="54bf6-109">Właściwość</span><span class="sxs-lookup"><span data-stu-id="54bf6-109">Property</span></span>              | <span data-ttu-id="54bf6-110">Typ</span><span class="sxs-lookup"><span data-stu-id="54bf6-110">Type</span></span>             | <span data-ttu-id="54bf6-111">Opis</span><span class="sxs-lookup"><span data-stu-id="54bf6-111">Description</span></span>                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="54bf6-112">identyfikator</span><span class="sxs-lookup"><span data-stu-id="54bf6-112">id</span></span>                    | <span data-ttu-id="54bf6-113">ciąg</span><span class="sxs-lookup"><span data-stu-id="54bf6-113">string</span></span>           | <span data-ttu-id="54bf6-114">Identyfikator subskrypcji klienta.</span><span class="sxs-lookup"><span data-stu-id="54bf6-114">The customer's subscription identifier.</span></span>                                                  |
| <span data-ttu-id="54bf6-115">nie kwalifikuj</span><span class="sxs-lookup"><span data-stu-id="54bf6-115">isEligible</span></span>            | <span data-ttu-id="54bf6-116">bool</span><span class="sxs-lookup"><span data-stu-id="54bf6-116">bool</span></span>             | <span data-ttu-id="54bf6-117">Wskazuje, czy subskrypcja kwalifikuje się do przeniesienia.</span><span class="sxs-lookup"><span data-stu-id="54bf6-117">Indicates whether the subscription is eligible for the transfer.</span></span>                         |
| <span data-ttu-id="54bf6-118">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="54bf6-118">Reason</span></span>                | <span data-ttu-id="54bf6-119">ciąg</span><span class="sxs-lookup"><span data-stu-id="54bf6-119">string</span></span>           | <span data-ttu-id="54bf6-120">Właściwość przyczyna wyjaśnia, dlaczego subskrypcja nie kwalifikuje się do przeniesienia.</span><span class="sxs-lookup"><span data-stu-id="54bf6-120">The reason property explains why the subscription isn't eligible for transfer.</span></span> |