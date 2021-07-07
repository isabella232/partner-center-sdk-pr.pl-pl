---
title: Witryna sklepu internetowego klienta CSP
description: Ten przykładowy kod witryny internetowej przedstawia roboczy sklep online, w ramach który klienci mogą kupować subskrypcje produktów firmy Microsoft.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d68f17d707731f426cb980a566b6478790d3507c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973336"
---
# <a name="csp-customer-web-storefront"></a><span data-ttu-id="98948-103">Witryna sklepu internetowego klienta CSP</span><span class="sxs-lookup"><span data-stu-id="98948-103">CSP customer web storefront</span></span>

<span data-ttu-id="98948-104">**Dotyczy:** Partner Center</span><span class="sxs-lookup"><span data-stu-id="98948-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="98948-105">**Nie dotyczy:** Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="98948-105">**Does not apply to**: Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="98948-106">Ta przykładowa aplikacja ma zastosowanie tylko do globalnego wystąpienia Partner Center.</span><span class="sxs-lookup"><span data-stu-id="98948-106">This sample app applies only to the global instance of Partner Center.</span></span>

<span data-ttu-id="98948-107">Witryna [Partner Center storefront](https://github.com/Microsoft/Partner-Center-Storefront) to  przykładowa witryna internetowa sklepu online, za pomocą których klienci mogą kupować subskrypcje produktów firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="98948-107">The [Partner Center storefront](https://github.com/Microsoft/Partner-Center-Storefront) is a **sample website** for an online store that customers can use to buy subscriptions to Microsoft products.</span></span> <span data-ttu-id="98948-108">Możesz zmodyfikować ten **przykładowy kod** na własny użytek, aby skonfigurować [oferty,](#configure-offers)dodać znakowanie [i](#configure-branding)dodać formę [płatności.](#configure-payment-types)</span><span class="sxs-lookup"><span data-stu-id="98948-108">You can modify this **sample code** for your own use to [configure the offers](#configure-offers), [add branding](#configure-branding), and [add a payment method](#configure-payment-types).</span></span>

## <a name="sample-code"></a><span data-ttu-id="98948-109">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="98948-109">Sample code</span></span>

<span data-ttu-id="98948-110">Pobierz [przykładowy kod Partner Center storefront z](https://github.com/Microsoft/Partner-Center-Storefront) GitHub.</span><span class="sxs-lookup"><span data-stu-id="98948-110">Download the [Partner Center storefront sample code](https://github.com/Microsoft/Partner-Center-Storefront) from GitHub.</span></span>

## <a name="configure-authentication"></a><span data-ttu-id="98948-111">Konfigurowanie uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="98948-111">Configure authentication</span></span>

<span data-ttu-id="98948-112">Przed skompilowanie aplikacji zaktualizuj następujące wartości w pliku Web.config, aby odzwierciedlić informacje uwierzytelniania usługi Azure AD utworzone w ramach [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="98948-112">Before you build the application, update the following values in the Web.config file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="98948-113">Ustawień konta piaskownicy integracji należy używać na wczesnym etapie opracowywania lub do testowania w środowisku produkcyjnym (TiP).</span><span class="sxs-lookup"><span data-stu-id="98948-113">You should use your integration sandbox account settings during early development or for testing in production (TiP).</span></span>

- <span data-ttu-id="98948-114">**partnerCenter.applicationId**</span><span class="sxs-lookup"><span data-stu-id="98948-114">**partnerCenter.applicationId**</span></span>
- <span data-ttu-id="98948-115">**partnerCenter.applicationSecret**</span><span class="sxs-lookup"><span data-stu-id="98948-115">**partnerCenter.applicationSecret**</span></span>
- <span data-ttu-id="98948-116">**partnerCenter.domain**</span><span class="sxs-lookup"><span data-stu-id="98948-116">**partnerCenter.domain**</span></span>
- <span data-ttu-id="98948-117">**webPortal.clientId**</span><span class="sxs-lookup"><span data-stu-id="98948-117">**webPortal.clientId**</span></span>
- <span data-ttu-id="98948-118">**webPortal.clientSecret**</span><span class="sxs-lookup"><span data-stu-id="98948-118">**webPortal.clientSecret**</span></span>
- <span data-ttu-id="98948-119">**webPortal.domain**</span><span class="sxs-lookup"><span data-stu-id="98948-119">**webPortal.domain**</span></span>
- <span data-ttu-id="98948-120">**webPortal.azureStorageConnectionString**</span><span class="sxs-lookup"><span data-stu-id="98948-120">**webPortal.azureStorageConnectionString**</span></span>

## <a name="configure-offers"></a><span data-ttu-id="98948-121">Konfigurowanie ofert</span><span class="sxs-lookup"><span data-stu-id="98948-121">Configure offers</span></span>

<span data-ttu-id="98948-122">Zestaw ofert **(MicrosoftOffer)** można skonfigurować w modelu **OfferCatalogViewModel.**</span><span class="sxs-lookup"><span data-stu-id="98948-122">You can configure the set of offers (**MicrosoftOffer**) in the **OfferCatalogViewModel**.</span></span>

## <a name="configure-branding"></a><span data-ttu-id="98948-123">Konfigurowanie znakowania</span><span class="sxs-lookup"><span data-stu-id="98948-123">Configure branding</span></span>

<span data-ttu-id="98948-124">Ta przykładowa witryna internetowa śledzi następujące informacje o firmie i marce w *witrynach BrandingConfiguration.cs* i *PortalBranding.cs:*</span><span class="sxs-lookup"><span data-stu-id="98948-124">This sample website tracks the following company and brand information in *BrandingConfiguration.cs* and *PortalBranding.cs*:</span></span>

- <span data-ttu-id="98948-125">Nazwa organizacji</span><span class="sxs-lookup"><span data-stu-id="98948-125">Organization name</span></span>
- <span data-ttu-id="98948-126">Logo organizacji</span><span class="sxs-lookup"><span data-stu-id="98948-126">Organization logo</span></span>
- <span data-ttu-id="98948-127">Obraz nagłówka</span><span class="sxs-lookup"><span data-stu-id="98948-127">Header image</span></span>
- <span data-ttu-id="98948-128">Umowa o ochronie prywatności</span><span class="sxs-lookup"><span data-stu-id="98948-128">Privacy agreement</span></span>
- <span data-ttu-id="98948-129">Kontaktowy adres e-mail</span><span class="sxs-lookup"><span data-stu-id="98948-129">Contact email</span></span>
- <span data-ttu-id="98948-130">Numer telefonu kontaktowego</span><span class="sxs-lookup"><span data-stu-id="98948-130">Contact phone number</span></span>
- <span data-ttu-id="98948-131">Adres e-mail pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="98948-131">Support email</span></span>
- <span data-ttu-id="98948-132">Numer telefonu pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="98948-132">Support phone number</span></span>

### <a name="configure-payment-types"></a><span data-ttu-id="98948-133">Konfigurowanie typów płatności</span><span class="sxs-lookup"><span data-stu-id="98948-133">Configure payment types</span></span>

<span data-ttu-id="98948-134">Aplikacja używa obecnie bramy PayPal zaimplementowanej w *payPalGateway.cs.*</span><span class="sxs-lookup"><span data-stu-id="98948-134">The app currently uses a PayPal gateway, implemented in *PayPalGateway.cs*.</span></span>