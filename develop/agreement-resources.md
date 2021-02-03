---
title: Zasoby umowy
description: Zasób umowy reprezentuje umowę klienta w chmurze firmy Microsoft, która zawiera szczegółowe informacje o certyfikatach dostarczonych przez partnera.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: d964b1c7c6d70814ef68e48f05611ecbb113c8fe
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768554"
---
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a><span data-ttu-id="96cf3-103">Zasoby umowy reprezentujące umowę klienta w chmurze firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="96cf3-103">Agreement resources representing a Microsoft cloud customer agreement</span></span>

<span data-ttu-id="96cf3-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="96cf3-104">**Applies to:**</span></span>

- <span data-ttu-id="96cf3-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="96cf3-105">Partner Center</span></span>

<span data-ttu-id="96cf3-106">Zasób z **umową** jest obecnie obsługiwany przez centrum partnerskie tylko w chmurze publicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="96cf3-106">The **Agreement** resource is currently supported by Partner Center in the Microsoft public cloud only.</span></span> <span data-ttu-id="96cf3-107">Nie dotyczy:</span><span class="sxs-lookup"><span data-stu-id="96cf3-107">It isn't applicable to:</span></span>

- <span data-ttu-id="96cf3-108">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="96cf3-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="96cf3-109">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="96cf3-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="96cf3-110">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="96cf3-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="96cf3-111">Zasób **umowy** reprezentuje umowę klienta w chmurze firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="96cf3-111">The **Agreement** resource represents a Microsoft cloud customer agreement.</span></span>

## <a name="agreement"></a><span data-ttu-id="96cf3-112">Umowa</span><span class="sxs-lookup"><span data-stu-id="96cf3-112">Agreement</span></span>

<span data-ttu-id="96cf3-113">Zasób **umowy** reprezentuje szczegóły certyfikacji dostarczone przez partnera.</span><span class="sxs-lookup"><span data-stu-id="96cf3-113">The **Agreement** resource represents the details of certification provided by the partner.</span></span>

| <span data-ttu-id="96cf3-114">Właściwość</span><span class="sxs-lookup"><span data-stu-id="96cf3-114">Property</span></span>       | <span data-ttu-id="96cf3-115">Typ</span><span class="sxs-lookup"><span data-stu-id="96cf3-115">Type</span></span>   | <span data-ttu-id="96cf3-116">Opis</span><span class="sxs-lookup"><span data-stu-id="96cf3-116">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="96cf3-117">userId</span><span class="sxs-lookup"><span data-stu-id="96cf3-117">userId</span></span>         | <span data-ttu-id="96cf3-118">ciąg</span><span class="sxs-lookup"><span data-stu-id="96cf3-118">string</span></span>                         | <span data-ttu-id="96cf3-119">Identyfikator obiektu zalogowanego użytkownika w dzierżawie partnera, który zapewnia potwierdzenie w imieniu organizacji partnerskiej.</span><span class="sxs-lookup"><span data-stu-id="96cf3-119">Object identifier of the logged-in user in the partner tenant who is providing confirmation on behalf of the partner organization.</span></span> <span data-ttu-id="96cf3-120">W przypadku tworzenia zasobu umowy przy użyciu aplikacji + uwierzytelnianie użytkownika centrum partnerskie automatycznie dziedziczy wartość atrybutu **userId** z tokenu App + User.</span><span class="sxs-lookup"><span data-stu-id="96cf3-120">When using App+User authentication to create an Agreement resource, Partner Center automatically derives the **userId** attribute value from the App+User token.</span></span>                                                                             |
| <span data-ttu-id="96cf3-121">primaryContact</span><span class="sxs-lookup"><span data-stu-id="96cf3-121">primaryContact</span></span> | [<span data-ttu-id="96cf3-122">Kontakt</span><span class="sxs-lookup"><span data-stu-id="96cf3-122">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="96cf3-123">Informacje o użytkowniku z organizacji klienta, które zaakceptowali umowę, w tym:  **FirstName**, **nazwisko**, **adres e-mail** i numer **telefonu** (opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="96cf3-123">Information about the user from the customer organization that accepted the agreement, including:  **firstName**, **lastName**, **email**, and **phoneNumber** (optional).</span></span> |
| <span data-ttu-id="96cf3-124">dateAgreed</span><span class="sxs-lookup"><span data-stu-id="96cf3-124">dateAgreed</span></span>     | <span data-ttu-id="96cf3-125">ciąg w formacie daty i godziny czasu UTC</span><span class="sxs-lookup"><span data-stu-id="96cf3-125">string in UTC date time format</span></span> | <span data-ttu-id="96cf3-126">Data zaakceptowania umowy przez klienta.</span><span class="sxs-lookup"><span data-stu-id="96cf3-126">The date when the customer accepted the agreement.</span></span>                                 |
| <span data-ttu-id="96cf3-127">templateId</span><span class="sxs-lookup"><span data-stu-id="96cf3-127">templateId</span></span>     |<span data-ttu-id="96cf3-128">ciąg</span><span class="sxs-lookup"><span data-stu-id="96cf3-128">string</span></span>                          | <span data-ttu-id="96cf3-129">Unikatowy identyfikator umowy zaakceptowanej przez klienta.</span><span class="sxs-lookup"><span data-stu-id="96cf3-129">Unique identifier of the agreement that the customer accepted.</span></span> |
| <span data-ttu-id="96cf3-130">typ</span><span class="sxs-lookup"><span data-stu-id="96cf3-130">type</span></span>           |<span data-ttu-id="96cf3-131">ciąg</span><span class="sxs-lookup"><span data-stu-id="96cf3-131">string</span></span>                          | <span data-ttu-id="96cf3-132">Typ umowy.</span><span class="sxs-lookup"><span data-stu-id="96cf3-132">Agreement type.</span></span> <span data-ttu-id="96cf3-133">Obecnie obsługiwane wartości to **MicrosoftCloudAgreement** i **MicrosoftCustomerAgreement**.</span><span class="sxs-lookup"><span data-stu-id="96cf3-133">Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement**.</span></span>|
| <span data-ttu-id="96cf3-134">agreementLink</span><span class="sxs-lookup"><span data-stu-id="96cf3-134">agreementLink</span></span>  | <span data-ttu-id="96cf3-135">ciąg</span><span class="sxs-lookup"><span data-stu-id="96cf3-135">string</span></span>                         | <span data-ttu-id="96cf3-136">Adres URL szablonu umowy.</span><span class="sxs-lookup"><span data-stu-id="96cf3-136">URL for the agreement template.</span></span>                                                    |
