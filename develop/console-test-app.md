---
title: Aplikacja testowa konsoli
description: Ta aplikacja testowa konsoli zawiera przykładowy kod dla wszystkich scenariuszy obsługiwanych przez Partner Center API. Można go również używać do testowania.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b35167104deeede50107d59fca6112c10dc7b4bf
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974033"
---
# <a name="console-test-app"></a><span data-ttu-id="2352b-104">Aplikacja testowa konsoli</span><span class="sxs-lookup"><span data-stu-id="2352b-104">Console test app</span></span>

<span data-ttu-id="2352b-105">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2352b-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2352b-106">Aplikacja testowa konsoli jest dostarczana w językach C# i Java. Udostępnia przykładowe kody dla wszystkich scenariuszy obsługiwanych przez interfejsy API Partner Center Api.</span><span class="sxs-lookup"><span data-stu-id="2352b-106">The console test app is provided in C# and Java, it provides sample codes for all of the scenarios supported by the Partner Center APIs.</span></span> <span data-ttu-id="2352b-107">Można go również używać do testowania.</span><span class="sxs-lookup"><span data-stu-id="2352b-107">You can also use it for testing.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="2352b-108">Uzyskiwanie kodu</span><span class="sxs-lookup"><span data-stu-id="2352b-108">Get the code</span></span>

<span data-ttu-id="2352b-109">Pobierz przykładowy kod aplikacji testowej konsoli.</span><span class="sxs-lookup"><span data-stu-id="2352b-109">Download the sample code for the console test app.</span></span>

## <a name="net"></a><span data-ttu-id="2352b-110">.NET</span><span class="sxs-lookup"><span data-stu-id="2352b-110">.NET</span></span>

<span data-ttu-id="2352b-111">[Pobierz przykładowy kod i](https://go.microsoft.com/fwlink/p/?LinkId=746682) zmodyfikuj go w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="2352b-111">[Download the sample code](https://go.microsoft.com/fwlink/p/?LinkId=746682) and modify it as necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2352b-112">Przed skompilowanie aplikacji zaktualizuj wartości w pliku *App.config,* aby odzwierciedlić informacje uwierzytelniania usługi Azure AD utworzone w ramach [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2352b-112">Before you build the application, update the values in the *App.config* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2352b-113">W szczególności należy używać ustawień konta piaskownicy integracji na wczesnym etapie opracowywania lub do testowania w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="2352b-113">Specifically, you should use your integration sandbox account settings during early development or for testing in production.</span></span>

<span data-ttu-id="2352b-114">W **obszarze ScenarioSettings** w *App.config* można ustawić parametry, które będą automatycznie przekazywane do uruchamianych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="2352b-114">Under **ScenarioSettings** in the *App.config* file, you can set parameters that will be automatically passed into the scenarios that you run.</span></span>

<span data-ttu-id="2352b-115">Aby zmodyfikować listę uruchamianych scenariuszy, przekrzywij wiersze w scenariuszu **IPartnerScenario \[ \] mainScenarios** lub w indywidualnej metodzie **Get Scenarios** znalezionej w *pliku Program.cs.*</span><span class="sxs-lookup"><span data-stu-id="2352b-115">To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.cs* file.</span></span>

## <a name="java"></a><span data-ttu-id="2352b-116">Java</span><span class="sxs-lookup"><span data-stu-id="2352b-116">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="2352b-117">[Pobierz przykładowy kod i](https://go.microsoft.com/fwlink/p/?LinkId=2026887) zmodyfikuj go w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="2352b-117">[Download the sample code](https://go.microsoft.com/fwlink/p/?LinkId=2026887) and modify it as necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2352b-118">Przed skompilowanie aplikacji zaktualizuj wartości w pliku *SamplesConfigurations.jsw* celu odzwierciedlenia informacji uwierzytelniania usługi Azure AD utworzonych podczas [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2352b-118">Before you build the application, update the values in the *SamplesConfigurations.json* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2352b-119">W szczególności należy używać ustawień konta piaskownicy integracji na wczesnym etapie opracowywania lub do testowania w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="2352b-119">Specifically, you should use your integration sandbox account settings during early development or for testing in production.</span></span>

<span data-ttu-id="2352b-120">W **obszarze ScenarioSettings** SamplesConfiguration.js *pliku* można ustawić parametry, które będą automatycznie przekazywane do uruchamianych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="2352b-120">Under **ScenarioSettings** in the *SamplesConfiguration.json* file, you can set parameters that will be automatically passed into the scenarios that you run.</span></span>

<span data-ttu-id="2352b-121">Aby zmodyfikować listę uruchamianych scenariuszy, przekrzywij wiersze w scenariuszu **IPartnerScenario \[ \] mainScenarios** lub w indywidualnej metodzie **Get Scenarios** znalezionej w *pliku Program.java.*</span><span class="sxs-lookup"><span data-stu-id="2352b-121">To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.java* file.</span></span>

## <a name="what-to-change"></a><span data-ttu-id="2352b-122">Co należy zmienić</span><span class="sxs-lookup"><span data-stu-id="2352b-122">What to change</span></span>

<span data-ttu-id="2352b-123">Użyj poniższych list, aby określić, co należy zmienić w przykładowym kodzie.</span><span class="sxs-lookup"><span data-stu-id="2352b-123">Use the following lists to determine what to change or not change in the sample code.</span></span>

### <a name="partnerservicesettings"></a><span data-ttu-id="2352b-124">PartnerServiceSettings</span><span class="sxs-lookup"><span data-stu-id="2352b-124">PartnerServiceSettings</span></span>

<span data-ttu-id="2352b-125">W **przypadku usługi PartnerServiceSettings** nie zmieniaj:</span><span class="sxs-lookup"><span data-stu-id="2352b-125">For **PartnerServiceSettings**, don't change:</span></span>

- <span data-ttu-id="2352b-126">**PartnerServiceApiEndpoint**</span><span class="sxs-lookup"><span data-stu-id="2352b-126">**PartnerServiceApiEndpoint**</span></span>
- <span data-ttu-id="2352b-127">**AuthenticationAuthorityEndpoint**</span><span class="sxs-lookup"><span data-stu-id="2352b-127">**AuthenticationAuthorityEndpoint**</span></span>
- <span data-ttu-id="2352b-128">**GraphEndpoint**</span><span class="sxs-lookup"><span data-stu-id="2352b-128">**GraphEndpoint**</span></span>
- <span data-ttu-id="2352b-129">**CommonDomain**</span><span class="sxs-lookup"><span data-stu-id="2352b-129">**CommonDomain**</span></span>

<span data-ttu-id="2352b-130">Wszystkie te ustawienia są niezbędne do poprawnego działania przykładowych wywołań interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2352b-130">All of these settings are necessary for the sample API calls to properly function.</span></span>

### <a name="userauthentication"></a><span data-ttu-id="2352b-131">UserAuthentication</span><span class="sxs-lookup"><span data-stu-id="2352b-131">UserAuthentication</span></span>

<span data-ttu-id="2352b-132">W **przypadku uwierzytelniania UserAuthentication** należy zmienić:</span><span class="sxs-lookup"><span data-stu-id="2352b-132">For **UserAuthentication**, you're required to change:</span></span>

- <span data-ttu-id="2352b-133">**ApplicationId** (identyfikator Azure Active Directory używany do logowania)</span><span class="sxs-lookup"><span data-stu-id="2352b-133">**ApplicationId** (your Azure Active Directory application ID used for login)</span></span>
- <span data-ttu-id="2352b-134">**UserName** (nazwa użytkownika usługi Active Directory)</span><span class="sxs-lookup"><span data-stu-id="2352b-134">**UserName** (your active directory username)</span></span>
- <span data-ttu-id="2352b-135">**Hasło** (hasło usługi Active Directory).</span><span class="sxs-lookup"><span data-stu-id="2352b-135">**Password** (your active directory password).</span></span>

<span data-ttu-id="2352b-136">Nie zmieniaj:</span><span class="sxs-lookup"><span data-stu-id="2352b-136">Don't change:</span></span>

- <span data-ttu-id="2352b-137">**Adres_Url_Zasobu**</span><span class="sxs-lookup"><span data-stu-id="2352b-137">**ResourceUrl**</span></span>
- <span data-ttu-id="2352b-138">**RedirectUrl**</span><span class="sxs-lookup"><span data-stu-id="2352b-138">**RedirectUrl**</span></span>

### <a name="appauthentication"></a><span data-ttu-id="2352b-139">AppAuthentication</span><span class="sxs-lookup"><span data-stu-id="2352b-139">AppAuthentication</span></span>

<span data-ttu-id="2352b-140">W **przypadku uwierzytelniania AppAuthentication** należy zmienić:</span><span class="sxs-lookup"><span data-stu-id="2352b-140">For **AppAuthentication**, you're required to change:</span></span>

- <span data-ttu-id="2352b-141">**ApplicationId** (identyfikator aplikacji usługi Active Directory używany do logowania do aplikacji)</span><span class="sxs-lookup"><span data-stu-id="2352b-141">**ApplicationId** (your active directory application ID used for application login)</span></span>
- <span data-ttu-id="2352b-142">**ApplicationSecret** (klucz tajny aplikacji usługi Active Directory używany do logowania do aplikacji)</span><span class="sxs-lookup"><span data-stu-id="2352b-142">**ApplicationSecret** (your active directory application secret used for application login)</span></span>
- <span data-ttu-id="2352b-143">**Domena** (domena usługi Active Directory, w której jest hostowana aplikacja)</span><span class="sxs-lookup"><span data-stu-id="2352b-143">**Domain** (your active directory domain on which the application is hosted)</span></span>

### <a name="scenariosettings"></a><span data-ttu-id="2352b-144">ScenarioSettings</span><span class="sxs-lookup"><span data-stu-id="2352b-144">ScenarioSettings</span></span>

<span data-ttu-id="2352b-145">W **przypadku ustawienia ScenarioSettings** nie zmieniaj:</span><span class="sxs-lookup"><span data-stu-id="2352b-145">For **ScenarioSettings**, don't change:</span></span>

- <span data-ttu-id="2352b-146">**CustomerDomainSuffix** (sufiks domeny używany podczas tworzenia nowego klienta)</span><span class="sxs-lookup"><span data-stu-id="2352b-146">**CustomerDomainSuffix** (the domain suffix used when creating a new customer)</span></span>

<span data-ttu-id="2352b-147">Ustawienia opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="2352b-147">Optional settings.</span></span> <span data-ttu-id="2352b-148">W przypadku pozostawionych pustych informacji należy wprowadzić te informacje podczas uruchamiania scenariusza w razie potrzeby):</span><span class="sxs-lookup"><span data-stu-id="2352b-148">If left blank, this information will need to be inputted when running a scenario where necessary):</span></span>

- <span data-ttu-id="2352b-149">**CustomerIdToDelete** (identyfikator klienta użyty do usunięcia)</span><span class="sxs-lookup"><span data-stu-id="2352b-149">**CustomerIdToDelete** (the ID of the customer used for deletion)</span></span>
- <span data-ttu-id="2352b-150">**DefaultCustomerId** (identyfikator klienta do użycia w scenariuszach związanych z klientem)</span><span class="sxs-lookup"><span data-stu-id="2352b-150">**DefaultCustomerId** (the customer ID to use in customer-related scenarios)</span></span>
- <span data-ttu-id="2352b-151">**DefaultInvoiceID** (identyfikator faktury do użycia w scenariuszach faktur)</span><span class="sxs-lookup"><span data-stu-id="2352b-151">**DefaultInvoiceID** (the invoice ID to use in invoice scenarios)</span></span>
- <span data-ttu-id="2352b-152">**PartnerMpnId** (identyfikator MPN partnera do użycia w scenariuszach partnerów pośrednich)</span><span class="sxs-lookup"><span data-stu-id="2352b-152">**PartnerMpnId** (the partner MPN ID to use in indirect partner scenarios)</span></span>
- <span data-ttu-id="2352b-153">**DefaultServiceRequestId** (identyfikator żądania obsługi do użycia w scenariuszach żądania obsługi)</span><span class="sxs-lookup"><span data-stu-id="2352b-153">**DefaultServiceRequestId** (the service request ID to use in service request scenarios)</span></span>
- <span data-ttu-id="2352b-154">**DefaultSupportTopicID** (identyfikator tematu pomocy technicznej do użycia w scenariuszach żądania obsługi)</span><span class="sxs-lookup"><span data-stu-id="2352b-154">**DefaultSupportTopicID** (the support topic ID to use in service request scenarios)</span></span>
- <span data-ttu-id="2352b-155">**DefaultOfferID** (identyfikator oferty do użycia w scenariuszach oferty)</span><span class="sxs-lookup"><span data-stu-id="2352b-155">**DefaultOfferID** (the offer ID to use in offer scenarios)</span></span>
- <span data-ttu-id="2352b-156">**DefaultOrderID** (identyfikator zamówienia do użycia w scenariuszach kolejności)</span><span class="sxs-lookup"><span data-stu-id="2352b-156">**DefaultOrderID** (the order ID to use in order scenarios)</span></span>
- <span data-ttu-id="2352b-157">**DefaultSubscriptionID** (identyfikator subskrypcji do użycia w scenariuszach subskrypcji)</span><span class="sxs-lookup"><span data-stu-id="2352b-157">**DefaultSubscriptionID** (the subscription ID to use in subscription scenarios)</span></span>

<span data-ttu-id="2352b-158">Opcjonalnie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="2352b-158">Optional to change.</span></span> <span data-ttu-id="2352b-159">Wszystkie te ustawienia określają liczbę wpisów na stronie podczas pobierania zawartości stronicowej:</span><span class="sxs-lookup"><span data-stu-id="2352b-159">All of these settings specify the amount of entries per page when retrieving paged content:</span></span>

- <span data-ttu-id="2352b-160">**CustomerPageSize**</span><span class="sxs-lookup"><span data-stu-id="2352b-160">**CustomerPageSize**</span></span>
- <span data-ttu-id="2352b-161">**InvoicePageSize**</span><span class="sxs-lookup"><span data-stu-id="2352b-161">**InvoicePageSize**</span></span>
- <span data-ttu-id="2352b-162">**ServiceRequestPageSize**</span><span class="sxs-lookup"><span data-stu-id="2352b-162">**ServiceRequestPageSize**</span></span>
- <span data-ttu-id="2352b-163">**DefaultOfferPageSize**</span><span class="sxs-lookup"><span data-stu-id="2352b-163">**DefaultOfferPageSize**</span></span>
- <span data-ttu-id="2352b-164">**SubscriptionPageSize**</span><span class="sxs-lookup"><span data-stu-id="2352b-164">**SubscriptionPageSize**</span></span>
