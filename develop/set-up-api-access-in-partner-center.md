---
title: Konfigurowanie dostępu do interfejsu API w Centrum partnerskim
description: Skonfiguruj konta do testowania na zestaw SDK Centrum partnerskiego i testowania w piaskownicy integracji.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: db7d9bba34abadc907910c68c4a5583ed1f530f4
ms.sourcegitcommit: de1e68545d37d7fa1862788f7fa8c84a9c4f2795
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/16/2021
ms.locfileid: "114282103"
---
# <a name="set-up-api-access-in-partner-center"></a><span data-ttu-id="4939d-103">Konfigurowanie dostępu do interfejsu API w Centrum partnerskim</span><span class="sxs-lookup"><span data-stu-id="4939d-103">Set up API access in Partner Center</span></span>

<span data-ttu-id="4939d-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center dla Microsoft Cloud for US Government | Partner Center for Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="4939d-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud for US Government | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="4939d-105">W tym artykule opisano konta, które należy opracować w zestaw SDK Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="4939d-105">This article describes the accounts you need to develop against the Partner Center SDK.</span></span> <span data-ttu-id="4939d-106">W tym artykule wyjaśniono również, jak utworzyć konto piaskownicy [integracji i](#integration-sandbox-account) przetestować je w piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="4939d-106">This article also explains how to create an [integration sandbox account](#integration-sandbox-account) and test in the integration sandbox.</span></span>

>[!NOTE]
><span data-ttu-id="4939d-107">Aby uzyskać dostęp do interfejsów API, dzierżawa musi być dzierżawą dostawcy usług w chmurze i musisz być dostawcą pośrednim lub partnerem z rozliczeniami bezpośrednimi.</span><span class="sxs-lookup"><span data-stu-id="4939d-107">To get access to APIs, your tenant must be a CSP tenant and you must be either an indirect provider or a Direct bill partner.</span></span>

## <a name="account-definitions"></a><span data-ttu-id="4939d-108">Definicje kont</span><span class="sxs-lookup"><span data-stu-id="4939d-108">Account definitions</span></span>

<span data-ttu-id="4939d-109">Aby ułatwić integrację i testowanie integracji interfejsu API, Partner Center obsługuje dwa rodzaje kont:</span><span class="sxs-lookup"><span data-stu-id="4939d-109">To help you integrate and test your API integration, Partner Center supports two kinds of accounts:</span></span>

### <a name="primary-partner-account"></a><span data-ttu-id="4939d-110">Konto podstawowego partnera</span><span class="sxs-lookup"><span data-stu-id="4939d-110">Primary Partner account</span></span>

<span data-ttu-id="4939d-111">To konto umożliwia tworzenie rzeczywistych zamówień dla rzeczywistych klientów.</span><span class="sxs-lookup"><span data-stu-id="4939d-111">This account is where you create real orders for real customers.</span></span> <span data-ttu-id="4939d-112">Jeśli po zalogowaniu się na konto podstawowe zostaną wprowadzone jakiekolwiek zmiany lub transakcje przy użyciu interfejsu użytkownika pulpitu nawigacyjnego partnera lub usługi zestaw SDK Centrum partnerskiego, będą one traktowane jako oficjalne zamówienia dla rzeczywistych klientów.</span><span class="sxs-lookup"><span data-stu-id="4939d-112">If you make any changes or transactions when you are signed in to the primary account, by using either the Partner Center SDK or the Partner Dashboard UI, they will be treated as official orders for real customers.</span></span> <span data-ttu-id="4939d-113">Zostaną one odzwierciedlone na fakturze, a Twoja firma jest odpowiedzialna za ich opłacenie.</span><span class="sxs-lookup"><span data-stu-id="4939d-113">They will be reflected in your invoice, and your company is responsible for paying for them.</span></span>

### <a name="integration-sandbox-account"></a><span data-ttu-id="4939d-114">Konto piaskownicy integracji</span><span class="sxs-lookup"><span data-stu-id="4939d-114">Integration sandbox account</span></span>

<span data-ttu-id="4939d-115">To konto jest do testowania kodu i jego integracji z interfejsami API Partner Center przed szerokim wdrożeniem.</span><span class="sxs-lookup"><span data-stu-id="4939d-115">This account is for testing your code and its integration with the Partner Center APIs before you deploy it broadly.</span></span> <span data-ttu-id="4939d-116">Zmiany i transakcje wprowadzone po zalogowaniu się do konta piaskownicy integracji pojawią się na fakturze, jednak nie trzeba płacić kwoty faktury.</span><span class="sxs-lookup"><span data-stu-id="4939d-116">Changes and transactions you make when you are signed into the integration sandbox account will appear in your invoice, however, you do not have to pay the invoice amount.</span></span> <span data-ttu-id="4939d-117">Faktura w formacie PDF będzie mieć zastrzeżenia "NIE PŁAĆ.</span><span class="sxs-lookup"><span data-stu-id="4939d-117">Invoice pdf will have a disclaimer as "DO NOT PAY.</span></span> <span data-ttu-id="4939d-118">JEST TO FAKTURA PIASKOWNICY I NIE JEST WYMAGANA ŻADNA AKCJA".</span><span class="sxs-lookup"><span data-stu-id="4939d-118">THIS IS A SANDBOX INVOICE AND NO ACTION IS REQUIRED."</span></span>

<span data-ttu-id="4939d-119">Konto piaskownicy integracji i konto podstawowe działają niezależnie i nie współdzielą kont administratorów, kont użytkowników, klientów, zamówień, subskrypcji ani innych danych.</span><span class="sxs-lookup"><span data-stu-id="4939d-119">The integration sandbox account and the primary account act independently, and do not share admin accounts, user accounts, customers, orders, subscriptions, or other data.</span></span>

<span data-ttu-id="4939d-120">Piaskownica integracji obsługuje transakcje z ograniczoną liczbą klientów, zamówień, subskrypcji, licencji itp.</span><span class="sxs-lookup"><span data-stu-id="4939d-120">The integration sandbox supports transactions with a limited number of customers, orders, subscriptions, licenses, etc.</span></span>

<span data-ttu-id="4939d-121">Według zasad konta piaskownicy integracji są tylko do celów testowania integracji.</span><span class="sxs-lookup"><span data-stu-id="4939d-121">By policy, integration sandbox accounts are for integration testing purposes only.</span></span>

<span data-ttu-id="4939d-122">Konto piaskownicy integracji nie istnieje domyślnie.</span><span class="sxs-lookup"><span data-stu-id="4939d-122">By default, there is no integration sandbox account.</span></span> <span data-ttu-id="4939d-123">Musisz utworzyć go samodzielnie, jeśli zamierzasz używać zestaw SDK Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="4939d-123">You must create one yourself if you plan to use the Partner Center SDK.</span></span>

## <a name="set-up-your-accounts"></a><span data-ttu-id="4939d-124">Konfigurowanie kont</span><span class="sxs-lookup"><span data-stu-id="4939d-124">Set up your accounts</span></span>

<span data-ttu-id="4939d-125">W tej sekcji opisano sposób skonfigurowania podstawowego konta partnera i konta piaskownicy integracji dla zestaw SDK Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="4939d-125">This section describes how to set up a primary Partner account and an integration sandbox account for the Partner Center SDK.</span></span>

### <a name="create-an-integration-sandbox"></a><span data-ttu-id="4939d-126">Tworzenie piaskownicy integracji</span><span class="sxs-lookup"><span data-stu-id="4939d-126">Create an integration sandbox</span></span>

1. <span data-ttu-id="4939d-127">Zaloguj się do pulpitu nawigacyjnego partnera przy użyciu konta administratora globalnego (podstawowego konta partnera).</span><span class="sxs-lookup"><span data-stu-id="4939d-127">Sign in to Partner Dashboard with a global admin account (your primary Partner account.)</span></span>

2. <span data-ttu-id="4939d-128">W menu **Ustawienia** (ikona koła zębatego) wybierz **pozycję Ustawienia konta.**</span><span class="sxs-lookup"><span data-stu-id="4939d-128">From the **Settings** menu (gear icon), choose **Account settings**.</span></span>

3. <span data-ttu-id="4939d-129">Wybierz **kartę Piaskownica integracji.**</span><span class="sxs-lookup"><span data-stu-id="4939d-129">Choose **Integration sandbox** tab.</span></span>

    >[!NOTE]
    ><span data-ttu-id="4939d-130">Jeśli nie widzisz opcji Piaskownica integracji, możesz nie mieć konta administratora globalnego.</span><span class="sxs-lookup"><span data-stu-id="4939d-130">If you don't see an Integration sandbox option, you might not have a global admin account.</span></span> <span data-ttu-id="4939d-131">Być może korzystasz również z konta piaskownicy integracji, a piaskownica integracji została już ustawiona.</span><span class="sxs-lookup"><span data-stu-id="4939d-131">You also might be using an integration sandbox account and an integration sandbox has already been set up.</span></span>

4. <span data-ttu-id="4939d-132">Wprowadź informacje kontaktowe dla konta administratora piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="4939d-132">Enter the contact information for the integration sandbox admin account.</span></span> <span data-ttu-id="4939d-133">Następnie wybierz pozycję **Utwórz konto.**</span><span class="sxs-lookup"><span data-stu-id="4939d-133">Then, choose **Create account**.</span></span> <span data-ttu-id="4939d-134">Poczekaj kilka minut na komunikat potwierdzający, że konto zostało utworzone.</span><span class="sxs-lookup"><span data-stu-id="4939d-134">Wait a few minutes for a confirmation message that the account has been created.</span></span>

5. <span data-ttu-id="4939d-135">Po wyświetleniu komunikatu z potwierdzeniem wyloguj się z pulpitu nawigacyjnego partnera.</span><span class="sxs-lookup"><span data-stu-id="4939d-135">After you see the confirmation message, sign out of Partner Dashboard.</span></span>

6. <span data-ttu-id="4939d-136">Zaloguj się ponownie przy użyciu nowego konta administratora piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="4939d-136">Sign back in with your new integration sandbox admin account.</span></span> <span data-ttu-id="4939d-137">Upewnij się, że używasz **username@domain** formatu swoich poświadczeń wraz z określonym hasłem.</span><span class="sxs-lookup"><span data-stu-id="4939d-137">Be sure to use the format **username@domain** for your credentials along with the password that you specified.</span></span>

7. <span data-ttu-id="4939d-138">Wybierz **pozycję Skonfiguruj konto powyżej** **bieżącego zadania,** aby ukończyć konfigurowanie konta piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="4939d-138">Choose **Set Up Account** above **Current Tasks** to complete the sandbox account setup.</span></span>

### <a name="enable-api-access"></a><span data-ttu-id="4939d-139">Włączanie dostępu do interfejsu API</span><span class="sxs-lookup"><span data-stu-id="4939d-139">Enable API access</span></span>

<span data-ttu-id="4939d-140">Po skonfigurowaniu konta należy włączyć dostęp do interfejsu API, aby można było używać zestawu SDK centrum partnerskiego z piaskownicą integracji.</span><span class="sxs-lookup"><span data-stu-id="4939d-140">After your account is set up, you must enable API access before you can use the Partner Center SDK with the integration sandbox.</span></span> <span data-ttu-id="4939d-141">Należy włączyć dostęp do interfejsu API oddzielnie dla podstawowego konta partnera i dla konta piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="4939d-141">You need to enable access to the API separately for both your primary Partner account and your integration sandbox account.</span></span>

1. <span data-ttu-id="4939d-142">Zaloguj się do pulpitu nawigacyjnego partnera przy użyciu konta administratora globalnego.</span><span class="sxs-lookup"><span data-stu-id="4939d-142">Sign into Partner Dashboard using a global admin account.</span></span>

2. <span data-ttu-id="4939d-143">W menu **Ustawienia** (ikona koła zębatego) wybierz **pozycję Ustawienia konta.**</span><span class="sxs-lookup"><span data-stu-id="4939d-143">From the **Settings** menu (gear icon), select **Account settings**.</span></span>

3. <span data-ttu-id="4939d-144">Na stronie **Ustawienia konta** wybierz pozycję **Zarządzanie aplikacją.**</span><span class="sxs-lookup"><span data-stu-id="4939d-144">On the **Account settings** page, choose **App management**.</span></span>

4. <span data-ttu-id="4939d-145">Jeśli nie masz jeszcze istniejącej aplikacji, dodaj nową aplikację internetową.</span><span class="sxs-lookup"><span data-stu-id="4939d-145">If you do not already have an existing app, add a new web app.</span></span> <span data-ttu-id="4939d-146">Jeśli masz istniejącą aplikację internetową, wybierz **przycisk Dodaj** klucz.</span><span class="sxs-lookup"><span data-stu-id="4939d-146">If you have an existing web app, choose the **Add key** button.</span></span>

5. <span data-ttu-id="4939d-147">Skopiuj informacje o rejestracji  aplikacji, zwłaszcza klucz, jeśli tworzysz aplikację internetową, i przechowuj ją w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="4939d-147">Copy the app registration information, especially the **Key** if you're creating a web app, and store it in a safe place.</span></span>

6. <span data-ttu-id="4939d-148">Wyloguj się z pulpitu nawigacyjnego partnera.</span><span class="sxs-lookup"><span data-stu-id="4939d-148">Sign out of Partner Dashboard.</span></span>

7. <span data-ttu-id="4939d-149">Zaloguj się ponownie przy użyciu konta piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="4939d-149">Sign back in with your integration sandbox account.</span></span> <span data-ttu-id="4939d-150">Powtórz kroki 2–5, aby włączyć dostęp do interfejsu API w piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="4939d-150">Repeat steps 2-5 to enable API access in the integration sandbox.</span></span>

## <a name="write-and-test-code"></a><span data-ttu-id="4939d-151">Pisanie i testowanie kodu</span><span class="sxs-lookup"><span data-stu-id="4939d-151">Write and test code</span></span>

<span data-ttu-id="4939d-152">Kod i kod testowy można napisać w piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="4939d-152">You can write code and test code in the integration sandbox.</span></span> <span data-ttu-id="4939d-153">Poniższe informacje są potrzebne do skonfigurowania uwierzytelniania Partner Center [usłudze](partner-center-authentication.md) Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4939d-153">You'll need the following information to [set up Partner Center authentication](partner-center-authentication.md) with Azure AD.</span></span>

| <span data-ttu-id="4939d-154">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="4939d-154">Item name</span></span> | <span data-ttu-id="4939d-155">Lokalizacja elementu</span><span class="sxs-lookup"><span data-stu-id="4939d-155">Item location</span></span> |
| --------- | ------------- |
| <span data-ttu-id="4939d-156">Identyfikator aplikacji/identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="4939d-156">App ID / Client ID</span></span> | <span data-ttu-id="4939d-157">W menu **Ustawienia** (ikona koła zębatego) wybierz **pozycję Ustawienia konta.**</span><span class="sxs-lookup"><span data-stu-id="4939d-157">From the **Settings** menu (gear icon), select **Account settings**.</span></span> <span data-ttu-id="4939d-158">Na stronie **Ustawienia konta** wybierz pozycję **Zarządzanie aplikacją.**</span><span class="sxs-lookup"><span data-stu-id="4939d-158">On the **Account settings** page, select **App Management**.</span></span> <span data-ttu-id="4939d-159">Identyfikator aplikacji/identyfikator klienta jest wymieniony jako **identyfikator zarejestrowanej aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="4939d-159">The App ID/Client ID is listed as the **Registered application App ID**.</span></span> |
| <span data-ttu-id="4939d-160">Klucz</span><span class="sxs-lookup"><span data-stu-id="4939d-160">Key</span></span> | <span data-ttu-id="4939d-161">Jeśli aplikacja internetowa została utworzona w sekcji Włączanie dostępu [do interfejsu API](#enable-api-access), jest to klucz zapisany w kroku 5.</span><span class="sxs-lookup"><span data-stu-id="4939d-161">If you created a web app in the section [Enable API access](#enable-api-access), this is the key that you saved in step 5.</span></span> |
| <span data-ttu-id="4939d-162">Domena</span><span class="sxs-lookup"><span data-stu-id="4939d-162">Domain</span></span> | <span data-ttu-id="4939d-163">Domena piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="4939d-163">The domain for the integration sandbox.</span></span> |

## <a name="run-tested-code"></a><span data-ttu-id="4939d-164">Uruchamianie przetestowanych kodów</span><span class="sxs-lookup"><span data-stu-id="4939d-164">Run tested code</span></span>

<span data-ttu-id="4939d-165">Aby korzystać z rozwiązania z rzeczywistymi danymi klienta, należy zmienić poświadczenia piaskownicy integracji na poświadczenia podstawowego konta partnera.</span><span class="sxs-lookup"><span data-stu-id="4939d-165">To use your solution with real customer data, you must change from your integration sandbox credentials to your primary Partner account credentials.</span></span>

<span data-ttu-id="4939d-166">Gdy wszystko będzie gotowe do użycia przetestowanych kodów na podstawowym koncie partnera, musisz uzyskać token zabezpieczający usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4939d-166">When you're ready to use your tested code in your primary Partner account, you must get an Azure AD security token.</span></span> <span data-ttu-id="4939d-167">Ten token zabezpieczający jest oparty na Partner Center, kluczu i domenie (zamiast aplikacji, klucza i domeny piaskownicy integracji).</span><span class="sxs-lookup"><span data-stu-id="4939d-167">This security token is based on your Partner Center app, key, and domain (instead of your integration sandbox app, key, and domain).</span></span>

1. <span data-ttu-id="4939d-168">Postępuj zgodnie z instrukcjami [Partner Center uwierzytelniania,](partner-center-authentication.md) aby uzyskać token zabezpieczający usługi Azure AD przy użyciu poświadczeń Partner Center podstawowego.</span><span class="sxs-lookup"><span data-stu-id="4939d-168">Follow the steps in [Partner Center authentication](partner-center-authentication.md) to get an Azure AD security token using your primary Partner Center credentials.</span></span> <span data-ttu-id="4939d-169">(Wcześniej zostały one opisane w celu uzyskania tokenu zabezpieczającego usługi Azure AD dla piaskownicy integracji).</span><span class="sxs-lookup"><span data-stu-id="4939d-169">(You previously followed these steps to get an Azure AD security token for your integration sandbox.)</span></span>

2. <span data-ttu-id="4939d-170">Zastąp token zabezpieczeń integracji w kodzie nowym tokenem zabezpieczającym dla podstawowego konta partnera.</span><span class="sxs-lookup"><span data-stu-id="4939d-170">Replace the integration security token in your code with the new security token for your primary Partner account.</span></span>
