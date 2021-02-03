---
title: Konfigurowanie dostępu do interfejsu API w Centrum partnerskim
description: Skonfiguruj konta do tworzenia w porównaniu z zestawem SDK Centrum partnerskiego i test w piaskownicy integracji.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 873ff2ff9cecbfa92429958d3bfe2aa79fc3ad9a
ms.sourcegitcommit: d5de47c08ba661ba5de4935caa6843d7c2c91710
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/28/2020
ms.locfileid: "97768153"
---
# <a name="set-up-api-access-in-partner-center"></a><span data-ttu-id="a8162-103">Konfigurowanie dostępu do interfejsu API w Centrum partnerskim</span><span class="sxs-lookup"><span data-stu-id="a8162-103">Set up API access in Partner Center</span></span>

<span data-ttu-id="a8162-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="a8162-104">**Applies to:**</span></span>

- <span data-ttu-id="a8162-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="a8162-105">Partner Center</span></span>
- <span data-ttu-id="a8162-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="a8162-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="a8162-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a8162-107">Partner Center for Microsoft Cloud for US Government</span></span>
- <span data-ttu-id="a8162-108">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="a8162-108">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="a8162-109">W tym artykule opisano konta, które należy opracować względem zestawu SDK Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="a8162-109">This article describes the accounts you need to develop against the Partner Center SDK.</span></span> <span data-ttu-id="a8162-110">W tym artykule opisano również sposób tworzenia [konta piaskownicy integracji](#integration-sandbox-account) i testowania w piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="a8162-110">This article also explains how to create an [integration sandbox account](#integration-sandbox-account) and test in the integration sandbox.</span></span>

>[!NOTE]
><span data-ttu-id="a8162-111">Aby uzyskać dostęp do interfejsów API, dzierżawca musi być dzierżawcą dostawcy usług kryptograficznych i musi być dostawcą pośrednim lub bezpośrednim partnerem rozliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="a8162-111">To get access to APIs, your tenant must be a CSP tenant and you must be either an indirect provider or a Direct bill partner.</span></span>

## <a name="account-definitions"></a><span data-ttu-id="a8162-112">Definicje kont</span><span class="sxs-lookup"><span data-stu-id="a8162-112">Account definitions</span></span>

<span data-ttu-id="a8162-113">Aby ułatwić integrację i testowanie integracji interfejsu API, centrum partnerskie obsługuje dwa rodzaje kont:</span><span class="sxs-lookup"><span data-stu-id="a8162-113">To help you integrate and test your API integration, Partner Center supports two kinds of accounts:</span></span>

### <a name="primary-partner-account"></a><span data-ttu-id="a8162-114">Główne konto partnerskie</span><span class="sxs-lookup"><span data-stu-id="a8162-114">Primary Partner account</span></span>

<span data-ttu-id="a8162-115">To konto służy do tworzenia rzeczywistych zamówień dla rzeczywistych klientów.</span><span class="sxs-lookup"><span data-stu-id="a8162-115">This account is where you create real orders for real customers.</span></span> <span data-ttu-id="a8162-116">Jeśli wprowadzisz jakiekolwiek zmiany lub transakcje po zalogowaniu się na koncie podstawowym przy użyciu zestawu SDK Centrum partnerskiego lub interfejsu użytkownika pulpitu nawigacyjnego partnera, będą one traktowane jako oficjalne zamówienia dla rzeczywistych klientów.</span><span class="sxs-lookup"><span data-stu-id="a8162-116">If you make any changes or transactions when you are signed in to the primary account, by using either the Partner Center SDK or the Partner Dashboard UI, they will be treated as official orders for real customers.</span></span> <span data-ttu-id="a8162-117">Zostaną one odzwierciedlone na fakturze, a firma jest odpowiedzialna za płatność za nie.</span><span class="sxs-lookup"><span data-stu-id="a8162-117">They will be reflected in your invoice, and your company is responsible for paying for them.</span></span>

### <a name="integration-sandbox-account"></a><span data-ttu-id="a8162-118">Konto piaskownicy integracji</span><span class="sxs-lookup"><span data-stu-id="a8162-118">Integration sandbox account</span></span>

<span data-ttu-id="a8162-119">To konto służy do testowania kodu i jego integracji z interfejsem API Centrum partnerskiego przed jego wdrożeniem.</span><span class="sxs-lookup"><span data-stu-id="a8162-119">This account is for testing your code and its integration with the Partner Center APIs before you deploy it broadly.</span></span> <span data-ttu-id="a8162-120">Zmiany i transakcje wprowadzone po zalogowaniu się do konta piaskownicy integracji zostaną wyświetlone na fakturze, ale nie musisz uiszczać kwoty faktury.</span><span class="sxs-lookup"><span data-stu-id="a8162-120">Changes and transactions you make when you are signed into the integration sandbox account will appear in your invoice, however, you do not have to pay the invoice amount.</span></span> <span data-ttu-id="a8162-121">Plik PDF faktury będzie miał oświadczenie "nie płacisz".</span><span class="sxs-lookup"><span data-stu-id="a8162-121">Invoice pdf will have a disclaimer as "DO NOT PAY.</span></span> <span data-ttu-id="a8162-122">TO JEST FAKTURA PIASKOWNICY, A ŻADNA AKCJA NIE JEST WYMAGANA.</span><span class="sxs-lookup"><span data-stu-id="a8162-122">THIS IS A SANDBOX INVOICE AND NO ACTION IS REQUIRED."</span></span>

<span data-ttu-id="a8162-123">Konto piaskownicy integracji i konto podstawowe działają niezależnie i nie udostępniają kont administratorów, kont użytkowników, klientów, zamówień, subskrypcji ani innych danych.</span><span class="sxs-lookup"><span data-stu-id="a8162-123">The integration sandbox account and the primary account act independently, and do not share admin accounts, user accounts, customers, orders, subscriptions, or other data.</span></span>

<span data-ttu-id="a8162-124">Piaskownica integracji obsługuje transakcje z ograniczoną liczbą klientów, zamówień, subskrypcji, licencji itd.</span><span class="sxs-lookup"><span data-stu-id="a8162-124">The integration sandbox supports transactions with a limited number of customers, orders, subscriptions, licenses, etc.</span></span>

<span data-ttu-id="a8162-125">Zgodnie z zasadami konta piaskownicy integracji służą wyłącznie do celów testowania integracji.</span><span class="sxs-lookup"><span data-stu-id="a8162-125">By policy, integration sandbox accounts are for integration testing purposes only.</span></span>

<span data-ttu-id="a8162-126">Konto piaskownicy integracji nie istnieje domyślnie.</span><span class="sxs-lookup"><span data-stu-id="a8162-126">By default, there is no integration sandbox account.</span></span> <span data-ttu-id="a8162-127">Jeśli planujesz używać zestawu SDK Centrum partnerskiego, musisz utworzyć go samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="a8162-127">You must create one yourself if you plan to use the Partner Center SDK.</span></span>

## <a name="set-up-your-accounts"></a><span data-ttu-id="a8162-128">Konfigurowanie kont</span><span class="sxs-lookup"><span data-stu-id="a8162-128">Set up your accounts</span></span>

<span data-ttu-id="a8162-129">W tej sekcji opisano sposób konfigurowania konta partnera podstawowego i konta piaskownicy integracji dla zestawu SDK Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="a8162-129">This section describes how to set up a primary Partner account and an integration sandbox account for the Partner Center SDK.</span></span>

### <a name="create-an-integration-sandbox"></a><span data-ttu-id="a8162-130">Tworzenie piaskownicy integracji</span><span class="sxs-lookup"><span data-stu-id="a8162-130">Create an integration sandbox</span></span>

1. <span data-ttu-id="a8162-131">Zaloguj się do pulpitu nawigacyjnego partnera przy użyciu konta administratora globalnego (konta głównego partnera).</span><span class="sxs-lookup"><span data-stu-id="a8162-131">Sign in to Partner Dashboard with a global admin account (your primary Partner account.)</span></span>

2. <span data-ttu-id="a8162-132">Z menu **Ustawienia** (ikona koła zębatego) wybierz pozycję **Ustawienia partnera**.</span><span class="sxs-lookup"><span data-stu-id="a8162-132">From the **Settings** menu (gear icon), choose **Partner settings**.</span></span>

3. <span data-ttu-id="a8162-133">Wybierz kartę **piaskownica integracji** .</span><span class="sxs-lookup"><span data-stu-id="a8162-133">Choose **Integration sandbox** tab.</span></span>

    >[!NOTE]
    ><span data-ttu-id="a8162-134">Jeśli nie widzisz opcji piaskownicy integracji, być może nie masz konta administratora globalnego.</span><span class="sxs-lookup"><span data-stu-id="a8162-134">If you don't see an Integration sandbox option, you might not have a global admin account.</span></span> <span data-ttu-id="a8162-135">Może być również używane konto piaskownicy integracji i piaskownica integracji została już skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="a8162-135">You also might be using an integration sandbox account and an integration sandbox has already been set up.</span></span>

4. <span data-ttu-id="a8162-136">Wprowadź informacje kontaktowe dla konta administratora piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="a8162-136">Enter the contact information for the integration sandbox admin account.</span></span> <span data-ttu-id="a8162-137">Następnie wybierz pozycję **Utwórz konto**.</span><span class="sxs-lookup"><span data-stu-id="a8162-137">Then, choose **Create account**.</span></span> <span data-ttu-id="a8162-138">Poczekaj kilka minut, aż zostanie wyświetlony komunikat z potwierdzeniem, że konto zostało utworzone.</span><span class="sxs-lookup"><span data-stu-id="a8162-138">Wait a few minutes for a confirmation message that the account has been created.</span></span>

5. <span data-ttu-id="a8162-139">Po wyświetleniu komunikatu potwierdzenia Wyloguj się z pulpitu nawigacyjnego partnera.</span><span class="sxs-lookup"><span data-stu-id="a8162-139">After you see the confirmation message, sign out of Partner Dashboard.</span></span>

6. <span data-ttu-id="a8162-140">Zaloguj się ponownie przy użyciu nowego konta administratora piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="a8162-140">Sign back in with your new integration sandbox admin account.</span></span> <span data-ttu-id="a8162-141">Upewnij się, że używasz formatu **username@domain** poświadczeń oraz hasła, które zostało określone.</span><span class="sxs-lookup"><span data-stu-id="a8162-141">Be sure to use the format **username@domain** for your credentials along with the password that you just specified.</span></span>

7. <span data-ttu-id="a8162-142">Wybierz pozycję **Skonfiguruj konto** powyżej **bieżących zadań** , aby zakończyć konfigurację konta piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="a8162-142">Choose **Set Up Account** above **Current Tasks** to complete the sandbox account setup.</span></span>

### <a name="enable-api-access"></a><span data-ttu-id="a8162-143">Włącz dostęp do interfejsu API</span><span class="sxs-lookup"><span data-stu-id="a8162-143">Enable API access</span></span>

<span data-ttu-id="a8162-144">Po skonfigurowaniu konta należy włączyć dostęp do interfejsu API, aby można było używać zestawu SDK centrum partnerskiego z piaskownicą integracji.</span><span class="sxs-lookup"><span data-stu-id="a8162-144">After your account is set up, you must enable API access before you can use the Partner Center SDK with the integration sandbox.</span></span> <span data-ttu-id="a8162-145">Należy włączyć dostęp do interfejsu API oddzielnie dla podstawowego konta partnera i dla konta piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="a8162-145">You need to enable access to the API separately for both your primary Partner account and your integration sandbox account.</span></span>

1. <span data-ttu-id="a8162-146">Zaloguj się do pulpitu nawigacyjnego partnera przy użyciu konta administratora globalnego.</span><span class="sxs-lookup"><span data-stu-id="a8162-146">Sign into Partner Dashboard using a global admin account.</span></span>

2. <span data-ttu-id="a8162-147">Z menu **Ustawienia** (ikona koła zębatego) wybierz pozycję **Ustawienia partnera**.</span><span class="sxs-lookup"><span data-stu-id="a8162-147">From the **Settings** menu (gear icon), select **Partner settings**.</span></span>

3. <span data-ttu-id="a8162-148">Na stronie **Ustawienia konta** wybierz pozycję **Zarządzanie aplikacjami**.</span><span class="sxs-lookup"><span data-stu-id="a8162-148">On the **Account settings** page, choose **App management**.</span></span>

4. <span data-ttu-id="a8162-149">Jeśli nie masz jeszcze istniejącej aplikacji, Dodaj nową aplikację sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a8162-149">If you do not already have an existing app, add a new web app.</span></span> <span data-ttu-id="a8162-150">Jeśli masz istniejącą aplikację sieci Web, wybierz przycisk **Dodaj klucz** .</span><span class="sxs-lookup"><span data-stu-id="a8162-150">If you have an existing web app, choose the **Add key** button.</span></span>

5. <span data-ttu-id="a8162-151">Skopiuj informacje o rejestracji aplikacji, zwłaszcza w **przypadku tworzenia** aplikacji sieci Web i przechowywania ich w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="a8162-151">Copy the app registration information, especially the **Key** if you're creating a web app, and store it in a safe place.</span></span>

6. <span data-ttu-id="a8162-152">Wyloguj się z pulpitu nawigacyjnego partnera.</span><span class="sxs-lookup"><span data-stu-id="a8162-152">Sign out of Partner Dashboard.</span></span>

7. <span data-ttu-id="a8162-153">Zaloguj się ponownie przy użyciu konta piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="a8162-153">Sign back in with your integration sandbox account.</span></span> <span data-ttu-id="a8162-154">Powtórz kroki 2-5, aby włączyć dostęp do interfejsu API w piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="a8162-154">Repeat steps 2-5 to enable API access in the integration sandbox.</span></span>

## <a name="write-and-test-code"></a><span data-ttu-id="a8162-155">Napisz i Testuj kod</span><span class="sxs-lookup"><span data-stu-id="a8162-155">Write and test code</span></span>

<span data-ttu-id="a8162-156">Kod i kod testowy można napisać w piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="a8162-156">You can write code and test code in the integration sandbox.</span></span> <span data-ttu-id="a8162-157">Aby [skonfigurować uwierzytelnianie Centrum partnerskiego](partner-center-authentication.md) za pomocą usługi Azure AD, potrzebne są poniższe informacje.</span><span class="sxs-lookup"><span data-stu-id="a8162-157">You'll need the following information to [set up Partner Center authentication](partner-center-authentication.md) with Azure AD.</span></span>

| <span data-ttu-id="a8162-158">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="a8162-158">Item name</span></span> | <span data-ttu-id="a8162-159">Lokalizacja elementu</span><span class="sxs-lookup"><span data-stu-id="a8162-159">Item location</span></span> |
| --------- | ------------- |
| <span data-ttu-id="a8162-160">Identyfikator aplikacji/klienta</span><span class="sxs-lookup"><span data-stu-id="a8162-160">App ID / Client ID</span></span> | <span data-ttu-id="a8162-161">Z menu **Ustawienia** (ikona koła zębatego) wybierz pozycję **Ustawienia partnera**.</span><span class="sxs-lookup"><span data-stu-id="a8162-161">From the **Settings** menu (gear icon), select **Partner settings**.</span></span> <span data-ttu-id="a8162-162">Na stronie **Ustawienia konta** wybierz pozycję **Zarządzanie aplikacjami**.</span><span class="sxs-lookup"><span data-stu-id="a8162-162">On the **Account settings** page, select **App Management**.</span></span> <span data-ttu-id="a8162-163">Identyfikator aplikacji lub identyfikator klienta jest wyświetlany jako **zarejestrowany identyfikator aplikacji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="a8162-163">The App ID/Client ID is listed as the **Registered application App ID**.</span></span> |
| <span data-ttu-id="a8162-164">Klucz</span><span class="sxs-lookup"><span data-stu-id="a8162-164">Key</span></span> | <span data-ttu-id="a8162-165">Jeśli aplikacja sieci Web została utworzona w sekcji [Włączanie dostępu do interfejsu API](#enable-api-access), jest to klucz zapisany w kroku 5.</span><span class="sxs-lookup"><span data-stu-id="a8162-165">If you created a web app in the section [Enable API access](#enable-api-access), this is the key that you saved in step 5.</span></span> |
| <span data-ttu-id="a8162-166">Domena</span><span class="sxs-lookup"><span data-stu-id="a8162-166">Domain</span></span> | <span data-ttu-id="a8162-167">Domena piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="a8162-167">The domain for the integration sandbox.</span></span> |

## <a name="run-tested-code"></a><span data-ttu-id="a8162-168">Uruchom testowany kod</span><span class="sxs-lookup"><span data-stu-id="a8162-168">Run tested code</span></span>

<span data-ttu-id="a8162-169">Aby korzystać z rozwiązania z rzeczywistymi danymi klienta, musisz zmienić poświadczenia usługi piaskownicy integracji na swoje poświadczenia głównego konta partnera.</span><span class="sxs-lookup"><span data-stu-id="a8162-169">To use your solution with real customer data, you must change from your integration sandbox credentials to your primary Partner account credentials.</span></span>

<span data-ttu-id="a8162-170">Gdy wszystko będzie gotowe do użycia przetestowanego kodu na podstawowym koncie partnerskim, musisz uzyskać token zabezpieczający usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8162-170">When you're ready to use your tested code in your primary Partner account, you must get an Azure AD security token.</span></span> <span data-ttu-id="a8162-171">Ten token zabezpieczający jest oparty na aplikacji Centrum partnerskiego, klucz i domenę (zamiast aplikacji piaskownicy integracji, klucza i domeny).</span><span class="sxs-lookup"><span data-stu-id="a8162-171">This security token is based on your Partner Center app, key and domain (instead of your integration sandbox app, key and domain).</span></span>

1. <span data-ttu-id="a8162-172">Postępuj zgodnie z instrukcjami w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md) , aby uzyskać token zabezpieczający usługi Azure AD przy użyciu poświadczeń podstawowego Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="a8162-172">Follow the steps in [Partner Center authentication](partner-center-authentication.md) to get an Azure AD security token using your primary Partner Center credentials.</span></span> <span data-ttu-id="a8162-173">(Wcześniej zostały wykonane następujące kroki, aby uzyskać token zabezpieczający usługi Azure AD dla piaskownicy integracji).</span><span class="sxs-lookup"><span data-stu-id="a8162-173">(You previously followed these steps to get an Azure AD security token for your integration sandbox.)</span></span>

2. <span data-ttu-id="a8162-174">Zastąp token Security Integration w kodzie nowym tokenem zabezpieczającym dla głównego konta partnera.</span><span class="sxs-lookup"><span data-stu-id="a8162-174">Replace the integration security token in your code with the new security token for your primary Partner account.</span></span>
