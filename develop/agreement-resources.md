---
title: Zasoby umowy
description: Zasób Umowa reprezentuje umowę klienta chmury firmy Microsoft ze szczegółami certyfikacji dostarczonymi przez partnera.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 5fa196e711d9ff899b61ba20e75edd92749165e5
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025625"
---
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a><span data-ttu-id="94f07-103">Zasoby umowy reprezentujące umowę klienta chmury firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="94f07-103">Agreement resources representing a Microsoft cloud customer agreement</span></span>

<span data-ttu-id="94f07-104">**Dotyczy:** Partner Center</span><span class="sxs-lookup"><span data-stu-id="94f07-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="94f07-105">**Nie dotyczy:** Partner Center obsługiwane przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="94f07-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="94f07-106">Zasób **Umowy** jest obecnie obsługiwany przez Partner Center tylko w chmurze publicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="94f07-106">The **Agreement** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="94f07-107">Zasób **Umowa** reprezentuje umowę klienta chmury firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="94f07-107">The **Agreement** resource represents a Microsoft cloud customer agreement.</span></span>

## <a name="agreement"></a><span data-ttu-id="94f07-108">Umowa</span><span class="sxs-lookup"><span data-stu-id="94f07-108">Agreement</span></span>

<span data-ttu-id="94f07-109">**Zasób** Umowa reprezentuje szczegóły certyfikacji dostarczone przez partnera.</span><span class="sxs-lookup"><span data-stu-id="94f07-109">The **Agreement** resource represents the details of certification provided by the partner.</span></span>

| <span data-ttu-id="94f07-110">Właściwość</span><span class="sxs-lookup"><span data-stu-id="94f07-110">Property</span></span>       | <span data-ttu-id="94f07-111">Typ</span><span class="sxs-lookup"><span data-stu-id="94f07-111">Type</span></span>   | <span data-ttu-id="94f07-112">Opis</span><span class="sxs-lookup"><span data-stu-id="94f07-112">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="94f07-113">userId</span><span class="sxs-lookup"><span data-stu-id="94f07-113">userId</span></span>         | <span data-ttu-id="94f07-114">ciąg</span><span class="sxs-lookup"><span data-stu-id="94f07-114">string</span></span>                         | <span data-ttu-id="94f07-115">Identyfikator obiektu zalogowanego użytkownika w dzierżawie partnera, który zapewnia potwierdzenie w imieniu organizacji partnerskiej.</span><span class="sxs-lookup"><span data-stu-id="94f07-115">Object identifier of the logged-in user in the partner tenant who is providing confirmation on behalf of the partner organization.</span></span> <span data-ttu-id="94f07-116">W przypadku tworzenia zasobu umowy przy użyciu uwierzytelniania App+User Partner Center automatycznie pobiera wartość atrybutu **userId** z tokenu App+User.</span><span class="sxs-lookup"><span data-stu-id="94f07-116">When using App+User authentication to create an Agreement resource, Partner Center automatically derives the **userId** attribute value from the App+User token.</span></span>                                                                             |
| <span data-ttu-id="94f07-117">primaryContact</span><span class="sxs-lookup"><span data-stu-id="94f07-117">primaryContact</span></span> | [<span data-ttu-id="94f07-118">Kontakt</span><span class="sxs-lookup"><span data-stu-id="94f07-118">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="94f07-119">Informacje o użytkowniku z organizacji klienta, który zaakceptował umowę, w tym:  **firstName,** **lastName,** **email** i **phoneNumber** (opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="94f07-119">Information about the user from the customer organization that accepted the agreement, including:  **firstName**, **lastName**, **email**, and **phoneNumber** (optional).</span></span> |
| <span data-ttu-id="94f07-120">dateAgreed</span><span class="sxs-lookup"><span data-stu-id="94f07-120">dateAgreed</span></span>     | <span data-ttu-id="94f07-121">ciąg w formacie daty i czasu UTC</span><span class="sxs-lookup"><span data-stu-id="94f07-121">string in UTC date time format</span></span> | <span data-ttu-id="94f07-122">Data zaakceptowania umowy przez klienta.</span><span class="sxs-lookup"><span data-stu-id="94f07-122">The date when the customer accepted the agreement.</span></span>                                 |
| <span data-ttu-id="94f07-123">templateId</span><span class="sxs-lookup"><span data-stu-id="94f07-123">templateId</span></span>     |<span data-ttu-id="94f07-124">ciąg</span><span class="sxs-lookup"><span data-stu-id="94f07-124">string</span></span>                          | <span data-ttu-id="94f07-125">Unikatowy identyfikator umowy zaakceptowanej przez klienta.</span><span class="sxs-lookup"><span data-stu-id="94f07-125">Unique identifier of the agreement that the customer accepted.</span></span> |
| <span data-ttu-id="94f07-126">typ</span><span class="sxs-lookup"><span data-stu-id="94f07-126">type</span></span>           |<span data-ttu-id="94f07-127">ciąg</span><span class="sxs-lookup"><span data-stu-id="94f07-127">string</span></span>                          | <span data-ttu-id="94f07-128">Typ umowy.</span><span class="sxs-lookup"><span data-stu-id="94f07-128">Agreement type.</span></span> <span data-ttu-id="94f07-129">Obecnie obsługiwane wartości to **MicrosoftCloudAgreement** i **MicrosoftCustomerAgreement.**</span><span class="sxs-lookup"><span data-stu-id="94f07-129">Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement**.</span></span>|
| <span data-ttu-id="94f07-130">agreementLink</span><span class="sxs-lookup"><span data-stu-id="94f07-130">agreementLink</span></span>  | <span data-ttu-id="94f07-131">ciąg</span><span class="sxs-lookup"><span data-stu-id="94f07-131">string</span></span>                         | <span data-ttu-id="94f07-132">Adres URL szablonu umowy.</span><span class="sxs-lookup"><span data-stu-id="94f07-132">URL for the agreement template.</span></span>                                                    |
