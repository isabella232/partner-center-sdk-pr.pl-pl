---
title: Witryna sklepu internetowego klienta CSP
description: Ten przykładowy kod witryny sieci Web przedstawia roboczy sklep online, który umożliwia klientom kupowanie subskrypcji produktów firmy Microsoft.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bd488b9b9bf2c1df4bebc8513d230a02b06b2ce4
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767741"
---
# <a name="csp-customer-web-storefront"></a><span data-ttu-id="a4024-103">Witryna sklepu internetowego klienta CSP</span><span class="sxs-lookup"><span data-stu-id="a4024-103">CSP customer web storefront</span></span>

<span data-ttu-id="a4024-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="a4024-104">**Applies to:**</span></span>

- <span data-ttu-id="a4024-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="a4024-105">Partner Center</span></span>

> [!NOTE]
> <span data-ttu-id="a4024-106">Ta przykładowa aplikacja dotyczy tylko globalnego wystąpienia Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="a4024-106">This sample app applies only to the global instance of Partner Center.</span></span> <span data-ttu-id="a4024-107">Nie dotyczy Centrum partnerskiego dla Microsoft Cloud Niemiec lub Centrum partnerskiego dla Microsoft Cloud dla instytucji rządowych USA.</span><span class="sxs-lookup"><span data-stu-id="a4024-107">It does not apply to Partner Center for Microsoft Cloud Germany or to Partner Center for Microsoft Cloud for US Government.</span></span>

<span data-ttu-id="a4024-108">Witryna sklepu w [centrum partnerskim](https://github.com/Microsoft/Partner-Center-Storefront) to **Przykładowa Witryna internetowa** dla sklepu online, za pomocą której klienci mogą kupować subskrypcje produktów firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a4024-108">The [Partner Center storefront](https://github.com/Microsoft/Partner-Center-Storefront) is a **sample website** for an online store that customers can use to buy subscriptions to Microsoft products.</span></span> <span data-ttu-id="a4024-109">Możesz zmodyfikować ten **przykładowy kod** do własnych potrzeb, aby [skonfigurować oferty](#configure-offers), [dodać markę](#configure-branding) i [dodać metodę płatności](#configure-payment-types).</span><span class="sxs-lookup"><span data-stu-id="a4024-109">You can modify this **sample code** for your own use to [configure the offers](#configure-offers), [add branding](#configure-branding) and [add a payment method](#configure-payment-types).</span></span>

## <a name="sample-code"></a><span data-ttu-id="a4024-110">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="a4024-110">Sample code</span></span>

<span data-ttu-id="a4024-111">Pobierz [przykładowy kod sklepu Centrum partnerskiego](https://github.com/Microsoft/Partner-Center-Storefront) z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="a4024-111">Download the [Partner Center storefront sample code](https://github.com/Microsoft/Partner-Center-Storefront) from GitHub.</span></span>

## <a name="configure-authentication"></a><span data-ttu-id="a4024-112">Konfigurowanie uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="a4024-112">Configure authentication</span></span>

<span data-ttu-id="a4024-113">Przed skompilowaniem aplikacji zaktualizuj następujące wartości w pliku Web.config w celu odzwierciedlenia informacji o uwierzytelnianiu usługi Azure AD utworzonych w ramach [uwierzytelniania w usłudze Partner Center](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a4024-113">Before you build the application, update the following values in the Web.config file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a4024-114">Podczas wczesnego programowania lub testowania w środowisku produkcyjnym należy używać ustawień konta piaskownicy do integracji.</span><span class="sxs-lookup"><span data-stu-id="a4024-114">You should use your integration sandbox account settings during early development or for testing in production (TiP).</span></span>

- <span data-ttu-id="a4024-115">**partnerCenter. Identyfikator aplikacji**</span><span class="sxs-lookup"><span data-stu-id="a4024-115">**partnerCenter.applicationId**</span></span>
- <span data-ttu-id="a4024-116">**partnerCenter.applicationSecret**</span><span class="sxs-lookup"><span data-stu-id="a4024-116">**partnerCenter.applicationSecret**</span></span>
- <span data-ttu-id="a4024-117">**partnerCenter. domena**</span><span class="sxs-lookup"><span data-stu-id="a4024-117">**partnerCenter.domain**</span></span>
- <span data-ttu-id="a4024-118">**webports. clientId**</span><span class="sxs-lookup"><span data-stu-id="a4024-118">**webPortal.clientId**</span></span>
- <span data-ttu-id="a4024-119">**webports. clientSecret**</span><span class="sxs-lookup"><span data-stu-id="a4024-119">**webPortal.clientSecret**</span></span>
- <span data-ttu-id="a4024-120">**WebPortal. domena**</span><span class="sxs-lookup"><span data-stu-id="a4024-120">**webPortal.domain**</span></span>
- <span data-ttu-id="a4024-121">**webports. azureStorageConnectionString**</span><span class="sxs-lookup"><span data-stu-id="a4024-121">**webPortal.azureStorageConnectionString**</span></span>

## <a name="configure-offers"></a><span data-ttu-id="a4024-122">Konfiguruj oferty</span><span class="sxs-lookup"><span data-stu-id="a4024-122">Configure offers</span></span>

<span data-ttu-id="a4024-123">Zestaw ofert (**MicrosoftOffer**) można skonfigurować w **OfferCatalogViewModel**.</span><span class="sxs-lookup"><span data-stu-id="a4024-123">You can configure the set of offers (**MicrosoftOffer**) in the **OfferCatalogViewModel**.</span></span>

## <a name="configure-branding"></a><span data-ttu-id="a4024-124">Konfigurowanie znakowania</span><span class="sxs-lookup"><span data-stu-id="a4024-124">Configure branding</span></span>

<span data-ttu-id="a4024-125">Ta przykładowa witryna sieci Web śledzi następujące informacje firmowe i markowe w *BrandingConfiguration.cs* i *PortalBranding.cs*:</span><span class="sxs-lookup"><span data-stu-id="a4024-125">This sample website tracks the following company and brand information in *BrandingConfiguration.cs* and *PortalBranding.cs*:</span></span>

- <span data-ttu-id="a4024-126">Nazwa organizacji</span><span class="sxs-lookup"><span data-stu-id="a4024-126">Organization name</span></span>
- <span data-ttu-id="a4024-127">Logo organizacji</span><span class="sxs-lookup"><span data-stu-id="a4024-127">Organization logo</span></span>
- <span data-ttu-id="a4024-128">Obraz nagłówka</span><span class="sxs-lookup"><span data-stu-id="a4024-128">Header image</span></span>
- <span data-ttu-id="a4024-129">Umowa dotycząca prywatności</span><span class="sxs-lookup"><span data-stu-id="a4024-129">Privacy agreement</span></span>
- <span data-ttu-id="a4024-130">Kontaktowy adres e-mail</span><span class="sxs-lookup"><span data-stu-id="a4024-130">Contact email</span></span>
- <span data-ttu-id="a4024-131">Kontaktowy numer telefonu</span><span class="sxs-lookup"><span data-stu-id="a4024-131">Contact phone number</span></span>
- <span data-ttu-id="a4024-132">Adres e-mail pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="a4024-132">Support email</span></span>
- <span data-ttu-id="a4024-133">Numer telefonu pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="a4024-133">Support phone number</span></span>

### <a name="configure-payment-types"></a><span data-ttu-id="a4024-134">Konfigurowanie typów płatności</span><span class="sxs-lookup"><span data-stu-id="a4024-134">Configure payment types</span></span>

<span data-ttu-id="a4024-135">Aplikacja aktualnie używa bramy systemu PayPal zaimplementowaną w *PayPalGateway.cs*.</span><span class="sxs-lookup"><span data-stu-id="a4024-135">The app currently uses a PayPal gateway, implemented in *PayPalGateway.cs*.</span></span>