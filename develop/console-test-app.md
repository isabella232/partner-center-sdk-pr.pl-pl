---
title: Aplikacja testowa konsoli
description: Ta aplikacja testowa konsoli udostępnia przykładowy kod dla wszystkich scenariuszy obsługiwanych przez interfejsy API Centrum partnerskiego. Można go również użyć do testowania.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e82bac3ccc22d0e7cf898e5b2d2e002c622584ae
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767994"
---
# <a name="console-test-app"></a><span data-ttu-id="0b03a-104">Aplikacja testowa konsoli</span><span class="sxs-lookup"><span data-stu-id="0b03a-104">Console test app</span></span>

<span data-ttu-id="0b03a-105">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="0b03a-105">**Applies to:**</span></span>

- <span data-ttu-id="0b03a-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="0b03a-106">Partner Center</span></span>
- <span data-ttu-id="0b03a-107">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="0b03a-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="0b03a-108">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="0b03a-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="0b03a-109">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0b03a-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0b03a-110">Aplikacja testowa konsoli dostępna w języku C# i Java zawiera przykładowe kody dla wszystkich scenariuszy obsługiwanych przez interfejsy API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="0b03a-110">The console test app is provided in C# and Java, it provides sample codes for all of the scenarios supported by the Partner Center APIs.</span></span> <span data-ttu-id="0b03a-111">Można go również użyć do testowania.</span><span class="sxs-lookup"><span data-stu-id="0b03a-111">You can also use it for testing.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="0b03a-112">Uzyskiwanie kodu</span><span class="sxs-lookup"><span data-stu-id="0b03a-112">Get the code</span></span>

<span data-ttu-id="0b03a-113">Pobierz przykładowy kod dla aplikacji testowej konsoli.</span><span class="sxs-lookup"><span data-stu-id="0b03a-113">Download the sample code for the console test app.</span></span>

## <a name="net"></a><span data-ttu-id="0b03a-114">.NET</span><span class="sxs-lookup"><span data-stu-id="0b03a-114">.NET</span></span>

<span data-ttu-id="0b03a-115">[Pobierz przykładowy kod](https://go.microsoft.com/fwlink/p/?LinkId=746682) i zmodyfikuj go w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="0b03a-115">[Download the sample code](https://go.microsoft.com/fwlink/p/?LinkId=746682) and modify it as necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b03a-116">Przed skompilowaniem aplikacji należy zaktualizować wartości w pliku *App.config* w celu odzwierciedlenia informacji o uwierzytelnianiu usługi Azure AD utworzonych w ramach uwierzytelniania w usłudze [Partner Center](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0b03a-116">Before you build the application, update the values in the *App.config* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0b03a-117">W szczególnych przypadkach należy używać ustawień konta piaskownicy integracji podczas wczesnego opracowywania lub testowania w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="0b03a-117">Specifically, you should use your integration sandbox account settings during early development or for testing in production.</span></span>

<span data-ttu-id="0b03a-118">W obszarze **ScenarioSettings** w pliku *App.config* można ustawić parametry, które będą automatycznie przesyłane do wykonywanych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="0b03a-118">Under **ScenarioSettings** in the *App.config* file, you can set parameters that will be automatically passed into the scenarios that you run.</span></span>

<span data-ttu-id="0b03a-119">Aby zmodyfikować listę uruchomionych scenariuszy, należy dodać komentarz do wierszy w **IPartnerScenario \[ \] mainScenarios** lub w poszczególnych metodach **Get scenariusze** znalezionych w pliku *program.cs* .</span><span class="sxs-lookup"><span data-stu-id="0b03a-119">To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.cs* file.</span></span>

## <a name="java"></a><span data-ttu-id="0b03a-120">Java</span><span class="sxs-lookup"><span data-stu-id="0b03a-120">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="0b03a-121">[Pobierz przykładowy kod](https://go.microsoft.com/fwlink/p/?LinkId=2026887) i zmodyfikuj go w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="0b03a-121">[Download the sample code](https://go.microsoft.com/fwlink/p/?LinkId=2026887) and modify it as necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b03a-122">Przed skompilowaniem aplikacji należy zaktualizować wartości w *SamplesConfigurations.jsw* pliku, aby odzwierciedlić informacje o uwierzytelnianiu usługi Azure AD utworzone w ramach uwierzytelniania w usłudze [Partner Center](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0b03a-122">Before you build the application, update the values in the *SamplesConfigurations.json* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0b03a-123">W szczególnych przypadkach należy używać ustawień konta piaskownicy integracji podczas wczesnego opracowywania lub testowania w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="0b03a-123">Specifically, you should use your integration sandbox account settings during early development or for testing in production.</span></span>

<span data-ttu-id="0b03a-124">W obszarze **ScenarioSettings** w pliku *SamplesConfiguration.js* , można ustawić parametry, które będą automatycznie przesyłane do wykonywanych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="0b03a-124">Under **ScenarioSettings** in the *SamplesConfiguration.json* file, you can set parameters that will be automatically passed into the scenarios that you run.</span></span>

<span data-ttu-id="0b03a-125">Aby zmodyfikować listę scenariuszy, które są uruchamiane, Dodaj komentarz do wierszy w **IPartnerScenario \[ \] mainScenarios** lub w poszczególnych metodach **Get scenariusze** , które znajdują się w pliku *program. Java* .</span><span class="sxs-lookup"><span data-stu-id="0b03a-125">To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.java* file.</span></span>

## <a name="what-to-change"></a><span data-ttu-id="0b03a-126">Co należy zmienić</span><span class="sxs-lookup"><span data-stu-id="0b03a-126">What to change</span></span>

<span data-ttu-id="0b03a-127">Użyj poniższych list, aby określić, co zmienić lub nie zmienić w przykładowym kodzie.</span><span class="sxs-lookup"><span data-stu-id="0b03a-127">Use the following lists to determine what to change or not change in the sample code.</span></span>

### <a name="partnerservicesettings"></a><span data-ttu-id="0b03a-128">PartnerServiceSettings</span><span class="sxs-lookup"><span data-stu-id="0b03a-128">PartnerServiceSettings</span></span>

<span data-ttu-id="0b03a-129">W przypadku **PartnerServiceSettings** nie zmieniaj:</span><span class="sxs-lookup"><span data-stu-id="0b03a-129">For **PartnerServiceSettings**, don't change:</span></span>

- <span data-ttu-id="0b03a-130">**PartnerServiceApiEndpoint**</span><span class="sxs-lookup"><span data-stu-id="0b03a-130">**PartnerServiceApiEndpoint**</span></span>
- <span data-ttu-id="0b03a-131">**AuthenticationAuthorityEndpoint**</span><span class="sxs-lookup"><span data-stu-id="0b03a-131">**AuthenticationAuthorityEndpoint**</span></span>
- <span data-ttu-id="0b03a-132">**GraphEndpoint**</span><span class="sxs-lookup"><span data-stu-id="0b03a-132">**GraphEndpoint**</span></span>
- <span data-ttu-id="0b03a-133">**CommonDomain**</span><span class="sxs-lookup"><span data-stu-id="0b03a-133">**CommonDomain**</span></span>

<span data-ttu-id="0b03a-134">Wszystkie te ustawienia są niezbędne, aby przykładowe wywołania interfejsu API działały prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="0b03a-134">All of these settings are necessary for the sample API calls to properly function.</span></span>

### <a name="userauthentication"></a><span data-ttu-id="0b03a-135">UserAuthentication</span><span class="sxs-lookup"><span data-stu-id="0b03a-135">UserAuthentication</span></span>

<span data-ttu-id="0b03a-136">W przypadku **UserAuthentication** wymagane jest zmianę:</span><span class="sxs-lookup"><span data-stu-id="0b03a-136">For **UserAuthentication**, you're required to change:</span></span>

- <span data-ttu-id="0b03a-137">Identyfikator **aplikacji (Azure Active Directory** używany do logowania)</span><span class="sxs-lookup"><span data-stu-id="0b03a-137">**ApplicationId** (your Azure Active Directory application ID used for login)</span></span>
- <span data-ttu-id="0b03a-138">**Nazwa użytkownika** (nazwa użytkownika usługi Active Directory)</span><span class="sxs-lookup"><span data-stu-id="0b03a-138">**UserName** (your active directory username)</span></span>
- <span data-ttu-id="0b03a-139">**Hasło** (hasło usługi Active Directory).</span><span class="sxs-lookup"><span data-stu-id="0b03a-139">**Password** (your active directory password).</span></span>

<span data-ttu-id="0b03a-140">Nie zmieniaj:</span><span class="sxs-lookup"><span data-stu-id="0b03a-140">Don't change:</span></span>

- <span data-ttu-id="0b03a-141">**Adres_Url_Zasobu**</span><span class="sxs-lookup"><span data-stu-id="0b03a-141">**ResourceUrl**</span></span>
- <span data-ttu-id="0b03a-142">**RedirectUrl**</span><span class="sxs-lookup"><span data-stu-id="0b03a-142">**RedirectUrl**</span></span>

### <a name="appauthentication"></a><span data-ttu-id="0b03a-143">AppAuthentication</span><span class="sxs-lookup"><span data-stu-id="0b03a-143">AppAuthentication</span></span>

<span data-ttu-id="0b03a-144">W przypadku **AppAuthentication** wymagane jest zmianę:</span><span class="sxs-lookup"><span data-stu-id="0b03a-144">For **AppAuthentication**, you're required to change:</span></span>

- <span data-ttu-id="0b03a-145">Aplikacja **(identyfikator** aplikacji usługi Active Directory używany do logowania aplikacji)</span><span class="sxs-lookup"><span data-stu-id="0b03a-145">**ApplicationId** (your active directory application ID used for application login)</span></span>
- <span data-ttu-id="0b03a-146">**ApplicationSecret** (klucz tajny aplikacji usługi Active Directory używany do logowania aplikacji)</span><span class="sxs-lookup"><span data-stu-id="0b03a-146">**ApplicationSecret** (your active directory application secret used for application login)</span></span>
- <span data-ttu-id="0b03a-147">**Domena** (domena usługi Active Directory, na której jest hostowana aplikacja)</span><span class="sxs-lookup"><span data-stu-id="0b03a-147">**Domain** (your active directory domain on which the application is hosted)</span></span>

### <a name="scenariosettings"></a><span data-ttu-id="0b03a-148">ScenarioSettings</span><span class="sxs-lookup"><span data-stu-id="0b03a-148">ScenarioSettings</span></span>

<span data-ttu-id="0b03a-149">W przypadku **ScenarioSettings** nie zmieniaj:</span><span class="sxs-lookup"><span data-stu-id="0b03a-149">For **ScenarioSettings**, don't change:</span></span>

- <span data-ttu-id="0b03a-150">**CustomerDomainSuffix** (sufiks domeny używany podczas tworzenia nowego klienta)</span><span class="sxs-lookup"><span data-stu-id="0b03a-150">**CustomerDomainSuffix** (the domain suffix used when creating a new customer)</span></span>

<span data-ttu-id="0b03a-151">Ustawienia opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="0b03a-151">Optional settings.</span></span> <span data-ttu-id="0b03a-152">Jeśli pole pozostanie puste, te informacje będą musiały zostać zwrócone podczas uruchamiania scenariusza, w razie potrzeby):</span><span class="sxs-lookup"><span data-stu-id="0b03a-152">If left blank, this information will need to be inputted when running a scenario where necessary):</span></span>

- <span data-ttu-id="0b03a-153">**CustomerIdToDelete** (identyfikator klienta używany do usuwania)</span><span class="sxs-lookup"><span data-stu-id="0b03a-153">**CustomerIdToDelete** (the ID of the customer used for deletion)</span></span>
- <span data-ttu-id="0b03a-154">**DefaultCustomerId** (identyfikator klienta do użycia w scenariuszach związanych z klientem)</span><span class="sxs-lookup"><span data-stu-id="0b03a-154">**DefaultCustomerId** (the customer ID to use in customer-related scenarios)</span></span>
- <span data-ttu-id="0b03a-155">**DefaultInvoiceID** (Identyfikator faktury do użycia w scenariuszach faktur)</span><span class="sxs-lookup"><span data-stu-id="0b03a-155">**DefaultInvoiceID** (the invoice ID to use in invoice scenarios)</span></span>
- <span data-ttu-id="0b03a-156">**PartnerMpnId** (identyfikator MPN partnera, który ma być używany w scenariuszach partnera pośredniego)</span><span class="sxs-lookup"><span data-stu-id="0b03a-156">**PartnerMpnId** (the partner MPN ID to use in indirect partner scenarios)</span></span>
- <span data-ttu-id="0b03a-157">**DefaultServiceRequestId** (Identyfikator żądania obsługi, który ma być używany w scenariuszach żądania obsługi)</span><span class="sxs-lookup"><span data-stu-id="0b03a-157">**DefaultServiceRequestId** (the service request ID to use in service request scenarios)</span></span>
- <span data-ttu-id="0b03a-158">**DefaultSupportTopicID** (identyfikator tematu pomocy technicznej, który ma być używany w scenariuszach żądania obsługi)</span><span class="sxs-lookup"><span data-stu-id="0b03a-158">**DefaultSupportTopicID** (the support topic ID to use in service request scenarios)</span></span>
- <span data-ttu-id="0b03a-159">**DefaultOfferID** (identyfikator oferty do użycia w scenariuszach oferty)</span><span class="sxs-lookup"><span data-stu-id="0b03a-159">**DefaultOfferID** (the offer ID to use in offer scenarios)</span></span>
- <span data-ttu-id="0b03a-160">**DefaultOrderID** (Identyfikator zamówienia do użycia w scenariuszach w kolejności)</span><span class="sxs-lookup"><span data-stu-id="0b03a-160">**DefaultOrderID** (the order ID to use in order scenarios)</span></span>
- <span data-ttu-id="0b03a-161">**DefaultSubscriptionID** (Identyfikator subskrypcji do użycia w scenariuszach subskrypcji)</span><span class="sxs-lookup"><span data-stu-id="0b03a-161">**DefaultSubscriptionID** (the subscription ID to use in subscription scenarios)</span></span>

<span data-ttu-id="0b03a-162">Opcjonalne, aby zmienić.</span><span class="sxs-lookup"><span data-stu-id="0b03a-162">Optional to change.</span></span> <span data-ttu-id="0b03a-163">Wszystkie te ustawienia określają liczbę wpisów na stronie podczas pobierania zawartości stronicowanej:</span><span class="sxs-lookup"><span data-stu-id="0b03a-163">All of these settings specify the amount of entries per page when retrieving paged content:</span></span>

- <span data-ttu-id="0b03a-164">**CustomerPageSize**</span><span class="sxs-lookup"><span data-stu-id="0b03a-164">**CustomerPageSize**</span></span>
- <span data-ttu-id="0b03a-165">**InvoicePageSize**</span><span class="sxs-lookup"><span data-stu-id="0b03a-165">**InvoicePageSize**</span></span>
- <span data-ttu-id="0b03a-166">**ServiceRequestPageSize**</span><span class="sxs-lookup"><span data-stu-id="0b03a-166">**ServiceRequestPageSize**</span></span>
- <span data-ttu-id="0b03a-167">**DefaultOfferPageSize**</span><span class="sxs-lookup"><span data-stu-id="0b03a-167">**DefaultOfferPageSize**</span></span>
- <span data-ttu-id="0b03a-168">**SubscriptionPageSize**</span><span class="sxs-lookup"><span data-stu-id="0b03a-168">**SubscriptionPageSize**</span></span>
