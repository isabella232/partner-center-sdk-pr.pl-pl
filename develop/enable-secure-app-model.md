---
title: Włączanie modelu aplikacji zabezpieczonych
description: Zabezpiecz swoje aplikacje Centrum partnerskiego i panelu sterowania.
ms.date: 01/20/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 3e153e1e7d4e38580d8cb39a3996e56365ff5fbe
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768077"
---
# <a name="enabling-the-secure-application-model-framework"></a><span data-ttu-id="4301f-103">Włączanie środowiska modelu aplikacji zabezpieczonej</span><span class="sxs-lookup"><span data-stu-id="4301f-103">Enabling the Secure Application Model framework</span></span>

<span data-ttu-id="4301f-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="4301f-104">**Applies to:**</span></span>

- <span data-ttu-id="4301f-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="4301f-105">Partner Center</span></span>

<span data-ttu-id="4301f-106">Firma Microsoft wprowadza bezpieczną i skalowalną platformę do uwierzytelniania partnerów dostawcy rozwiązań w chmurze (CSP) i dostawców panelu sterowania (CPV) za pomocą Microsoft Azure architekturę uwierzytelniania wieloskładnikowego (MFA).</span><span class="sxs-lookup"><span data-stu-id="4301f-106">Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure multi-factor authentication (MFA) architecture.</span></span>

<span data-ttu-id="4301f-107">Nowy model umożliwia podniesienie poziomu zabezpieczeń dla wywołań integracji z interfejsem API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="4301f-107">You can use the new model to elevate security for Partner Center API integration calls.</span></span> <span data-ttu-id="4301f-108">Pomoże to wszystkim stronom (w tym partnerom Microsoft, CSP i CPVs) na ochronę danych infrastruktury i klientów przed zagrożeniami bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="4301f-108">This will help all parties (including Microsoft, CSP partners, and CPVs) to protect their infrastructure and customer data from security risks.</span></span>

## <a name="scope"></a><span data-ttu-id="4301f-109">Zakres</span><span class="sxs-lookup"><span data-stu-id="4301f-109">Scope</span></span>

<span data-ttu-id="4301f-110">Ten artykuł dotyczy następujących podmiotów:</span><span class="sxs-lookup"><span data-stu-id="4301f-110">This article concerns the following actors:</span></span>

- <span data-ttu-id="4301f-111">Dostawcy oprogramowania panelu sterowania</span><span class="sxs-lookup"><span data-stu-id="4301f-111">CPVs</span></span>
  - <span data-ttu-id="4301f-112">Dostawca oprogramowania panelu sterowania (CPV) to niezależny dostawca oprogramowania, który opracowuje aplikacje, których partnerzy CSP mogą używać do integracji z interfejsami API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="4301f-112">A CPV is an independent software vendor that develops apps for use by CSP partners to integrate with Partner Center APIs.</span></span>
  - <span data-ttu-id="4301f-113">Dostawca CPV nie jest partnerem CSP z bezpośrednim dostępem do pulpitu nawigacyjnego lub interfejsów API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="4301f-113">A CPV isn't a CSP partner with direct access to the Partner Center dashboard or APIs.</span></span>

- <span data-ttu-id="4301f-114">Dostawcy usług kryptograficznych CSP i partnerzy bezpośredniego dostawcy usług kryptograficznych, którzy korzystają z identyfikatora aplikacji + uwierzytelnianie użytkownika i bezpośrednio integrują się z interfejsami API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="4301f-114">CSP indirect providers and CSP direct partners who are using app ID + user authentication and directly integrate with Partner Center APIs.</span></span>

## <a name="security-requirements"></a><span data-ttu-id="4301f-115">Wymagania dotyczące zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="4301f-115">Security requirements</span></span>

<span data-ttu-id="4301f-116">Aby uzyskać szczegółowe informacje na temat wymagań dotyczących zabezpieczeń, zobacz [wymagania dotyczące zabezpieczeń partnerów](/partner-center/partner-security-requirements).</span><span class="sxs-lookup"><span data-stu-id="4301f-116">For details on security requirements, see [Partner Security Requirements](/partner-center/partner-security-requirements).</span></span>

## <a name="secure-application-model"></a><span data-ttu-id="4301f-117">Bezpieczny model aplikacji</span><span class="sxs-lookup"><span data-stu-id="4301f-117">Secure Application Model</span></span>

<span data-ttu-id="4301f-118">Aplikacje Marketplace muszą personifikować uprawnienia partnerów CSP, aby wywoływać interfejsy API firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4301f-118">Marketplace applications need to impersonate CSP partner privileges to call Microsoft APIs.</span></span> <span data-ttu-id="4301f-119">Ataki na te aplikacje poufne mogą prowadzić do naruszenia bezpieczeństwa danych klientów.</span><span class="sxs-lookup"><span data-stu-id="4301f-119">Security attacks on these sensitive applications can lead to the compromise of customer data.</span></span>

<span data-ttu-id="4301f-120">Aby zapoznać się z omówieniem i szczegółami nowej struktury uwierzytelniania, Pobierz dokument [Application Framework bezpiecznego modelu aplikacji](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) .</span><span class="sxs-lookup"><span data-stu-id="4301f-120">For an overview and details of the new authentication framework, download the [Secure Application Model framework](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) document.</span></span> <span data-ttu-id="4301f-121">Ten dokument zawiera zasady i najlepsze rozwiązania, dzięki którym aplikacje Marketplace są trwałe i niezawodne przed naruszeniem zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4301f-121">This document covers principles and best practices to make marketplace applications sustainable and robust from security compromises.</span></span>

## <a name="samples"></a><span data-ttu-id="4301f-122">Samples</span><span class="sxs-lookup"><span data-stu-id="4301f-122">Samples</span></span>

<span data-ttu-id="4301f-123">W poniższych dokumentach i przykładowym kodzie opisano, jak partnerzy mogą wdrożyć bezpieczną strukturę modelu aplikacji:</span><span class="sxs-lookup"><span data-stu-id="4301f-123">The following overview documents and sample code describe how partners can implement the Secure Application Model framework:</span></span>

- [<span data-ttu-id="4301f-124">Dokument omówienia CPV</span><span class="sxs-lookup"><span data-stu-id="4301f-124">CPV overview document</span></span>](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [<span data-ttu-id="4301f-125">Dokument omówienia CSP</span><span class="sxs-lookup"><span data-stu-id="4301f-125">CSP overview document</span></span>](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [<span data-ttu-id="4301f-126">Przykłady dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="4301f-126">.NET Samples</span></span>](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [<span data-ttu-id="4301f-127">Przykłady dla języka Java</span><span class="sxs-lookup"><span data-stu-id="4301f-127">Java Samples</span></span>](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [<span data-ttu-id="4301f-128">Instrukcje i przykłady REST</span><span class="sxs-lookup"><span data-stu-id="4301f-128">REST instructions and samples</span></span>](#rest)
- [<span data-ttu-id="4301f-129">Instrukcje i przykłady dotyczące programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="4301f-129">PowerShell instructions and samples</span></span>](#powershell)

## <a name="rest"></a><span data-ttu-id="4301f-130">REST</span><span class="sxs-lookup"><span data-stu-id="4301f-130">REST</span></span>

<span data-ttu-id="4301f-131">Aby wykonać wywołania REST w środowisku bezpiecznego modelu aplikacji z przykładowym kodem, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4301f-131">To to make REST calls with the Secure Application Model framework with sample code, follow these steps:</span></span>

1. [<span data-ttu-id="4301f-132">Tworzenie aplikacji internetowej</span><span class="sxs-lookup"><span data-stu-id="4301f-132">Create a web app</span></span>](#create-a-web-app)

2. [<span data-ttu-id="4301f-133">Pobieranie kodu autoryzacji</span><span class="sxs-lookup"><span data-stu-id="4301f-133">Get an authorization code</span></span>](#get-authorization-code)

3. [<span data-ttu-id="4301f-134">Pobierz token odświeżania</span><span class="sxs-lookup"><span data-stu-id="4301f-134">Get a refresh token</span></span>](#get-refresh-token)

4. [<span data-ttu-id="4301f-135">Pobranie tokenu dostępu</span><span class="sxs-lookup"><span data-stu-id="4301f-135">Get an access token</span></span>](#get-access-token)

5. [<span data-ttu-id="4301f-136">Wykonywanie wywołania interfejsu API Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="4301f-136">Make a Partner Center API call</span></span>](#make-partner-center-api-calls)

> [!TIP]
> <span data-ttu-id="4301f-137">Możesz użyć modułu programu PowerShell Centrum partnerskiego, aby uzyskać kod autoryzacji i token odświeżenia.</span><span class="sxs-lookup"><span data-stu-id="4301f-137">You can use the Partner Center PowerShell module to get an authorization code and a refresh token.</span></span> <span data-ttu-id="4301f-138">Możesz wybrać tę opcję zamiast kroków 2 i 3.</span><span class="sxs-lookup"><span data-stu-id="4301f-138">You can choose this option in place of steps 2 and 3.</span></span> <span data-ttu-id="4301f-139">Aby uzyskać więcej informacji, zapoznaj się z [sekcją i przykładami programu PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="4301f-139">For more information, see the [PowerShell section and examples](#powershell).</span></span>

### <a name="create-a-web-app"></a><span data-ttu-id="4301f-140">Tworzenie aplikacji internetowej</span><span class="sxs-lookup"><span data-stu-id="4301f-140">Create a web app</span></span>

<span data-ttu-id="4301f-141">Przed włączeniem wywołań REST należy utworzyć i zarejestrować aplikację sieci Web w centrum partnerskim.</span><span class="sxs-lookup"><span data-stu-id="4301f-141">You must create and register a web app in Partner Center before making REST calls.</span></span>

1. <span data-ttu-id="4301f-142">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4301f-142">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="4301f-143">Utwórz aplikację Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4301f-143">Create an Azure Active Directory (Azure AD) app.</span></span>

3. <span data-ttu-id="4301f-144">Przyznaj delegowane uprawnienia aplikacji do następujących zasobów, w *zależności od wymagań aplikacji*.</span><span class="sxs-lookup"><span data-stu-id="4301f-144">Give delegated application permissions to the following resources, *depending on your application's requirements*.</span></span> <span data-ttu-id="4301f-145">W razie potrzeby można dodać bardziej delegowane uprawnienia dla zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4301f-145">If necessary, you can add more delegated permissions for application resources.</span></span>

   1. <span data-ttu-id="4301f-146">**Centrum partnerskie firmy Microsoft** (w przypadku niektórych dzierżawców jest to **SampleBECApp**)</span><span class="sxs-lookup"><span data-stu-id="4301f-146">**Microsoft Partner Center** (some tenants show this as **SampleBECApp**)</span></span>

   2. <span data-ttu-id="4301f-147">**Interfejsy API zarządzania platformy Azure** (Jeśli planujesz wywołać interfejsy API platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="4301f-147">**Azure Management APIs** (if you are planning to call Azure APIs)</span></span>

   3. <span data-ttu-id="4301f-148">**Windows Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="4301f-148">**Windows Azure Active Directory**</span></span>

4. <span data-ttu-id="4301f-149">Upewnij się, że adres URL strony głównej aplikacji jest ustawiony na punkt końcowy, w którym jest uruchomiona działająca aplikacja sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4301f-149">Make sure that the home URL of your app is set to an endpoint where a live web app is running.</span></span> <span data-ttu-id="4301f-150">Ta aplikacja będzie musiała przyjąć [kod autoryzacji](#get-authorization-code) z wywołania logowania do usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4301f-150">This app will need to accept the [authorization code](#get-authorization-code) from the Azure AD login call.</span></span> <span data-ttu-id="4301f-151">Na przykład w przykładowym kodzie w [poniższej sekcji](#get-authorization-code)aplikacja sieci Web działa w systemie `https://localhost:44395/` .</span><span class="sxs-lookup"><span data-stu-id="4301f-151">For example, in the example code in [the following section](#get-authorization-code), the web app is running at `https://localhost:44395/`.</span></span>

5. <span data-ttu-id="4301f-152">Zwróć uwagę na następujące informacje z ustawień aplikacji sieci Web w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="4301f-152">Note the following information from your web app's settings in Azure AD:</span></span>

   - <span data-ttu-id="4301f-153">Identyfikator aplikacji</span><span class="sxs-lookup"><span data-stu-id="4301f-153">Application ID</span></span>
   - <span data-ttu-id="4301f-154">Klucz tajny aplikacji</span><span class="sxs-lookup"><span data-stu-id="4301f-154">Application secret</span></span>

> [!NOTE]
> <span data-ttu-id="4301f-155">Zalecane jest [użycie certyfikatu jako klucza tajnego aplikacji](/azure/active-directory/develop/active-directory-certificate-credentials).</span><span class="sxs-lookup"><span data-stu-id="4301f-155">It is recommended to [use a certificate as your application secret](/azure/active-directory/develop/active-directory-certificate-credentials).</span></span> <span data-ttu-id="4301f-156">Można jednak również utworzyć klucz aplikacji w Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4301f-156">However, you can also create an application key in the Azure portal.</span></span> <span data-ttu-id="4301f-157">Przykładowy kod w [poniższej sekcji](#get-authorization-code) używa klucza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4301f-157">The sample code in [the following section](#get-authorization-code) uses an application key.</span></span>

### <a name="get-authorization-code"></a><span data-ttu-id="4301f-158">Uzyskiwanie kodu autoryzacji</span><span class="sxs-lookup"><span data-stu-id="4301f-158">Get authorization code</span></span>

<span data-ttu-id="4301f-159">Musisz uzyskać kod autoryzacji dla aplikacji sieci Web, aby akceptować dane z wywołania logowania usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="4301f-159">You must get an authorization code for your web app to accept from the Azure AD login call:</span></span>

1. <span data-ttu-id="4301f-160">Zaloguj się do usługi Azure AD pod następującym adresem URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) .</span><span class="sxs-lookup"><span data-stu-id="4301f-160">Log in to Azure AD at the following URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1).</span></span> <span data-ttu-id="4301f-161">Pamiętaj, aby zalogować się przy użyciu konta użytkownika, z którego będą nawiązywane wywołania interfejsu API centrum partnera (takie jak Agent administracyjny lub konto agenta sprzedaży).</span><span class="sxs-lookup"><span data-stu-id="4301f-161">Be sure to log in with the user account from which you will make Partner Center API calls (such as an admin agent or sales agent account).</span></span>

2. <span data-ttu-id="4301f-162">Zamień **Identyfikator aplikacji** na identyfikator aplikacji usługi Azure AD (GUID).</span><span class="sxs-lookup"><span data-stu-id="4301f-162">Replace **Application-Id** with your Azure AD app ID (GUID).</span></span>

3. <span data-ttu-id="4301f-163">Po wyświetleniu monitu zaloguj się przy użyciu konta użytkownika z skonfigurowanym uwierzytelnianiem MFA.</span><span class="sxs-lookup"><span data-stu-id="4301f-163">When prompted, log in with your user account with MFA configured.</span></span>

4. <span data-ttu-id="4301f-164">Po wyświetleniu monitu wprowadź dodatkowe informacje MFA (numer telefonu lub adres e-mail), aby zweryfikować dane logowania.</span><span class="sxs-lookup"><span data-stu-id="4301f-164">When prompted, enter additional MFA information (phone number or email address) to verify your login.</span></span>

5. <span data-ttu-id="4301f-165">Po zalogowaniu przeglądarka przekieruje wywołanie do punktu końcowego aplikacji sieci Web przy użyciu kodu autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="4301f-165">After you are logged in, the browser will redirect the call to your web app endpoint with your authorization code.</span></span> <span data-ttu-id="4301f-166">Na przykład poniższy przykładowy kod przekierowuje do `https://localhost:44395/` .</span><span class="sxs-lookup"><span data-stu-id="4301f-166">For example, the following sample code redirects to `https://localhost:44395/`.</span></span>

#### <a name="authorization-code-call-trace"></a><span data-ttu-id="4301f-167">Śledzenie wywołań kodu autoryzacji</span><span class="sxs-lookup"><span data-stu-id="4301f-167">Authorization code call trace</span></span>

```http
POST https://localhost:44395/ HTTP/1.1
Origin: https://login.microsoftonline.com
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Referrer: https://login.microsoftonline.com/kmsi
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Cookie: OpenIdConnect.nonce.hOMjjrivcxzuI4YqAw4uYC%2F%2BILFk4%2FCx3kHTHP3lBvA%3D=dHVyRXdlbk9WVUZFdlFONVdiY01nNEpUc0JRR0RiYWFLTHhQYlRGNl9VeXJqNjdLTGV3cFpIWFg1YmpnWVdQUURtN0dvMkdHS2kzTm02NGdQS09veVNEbTZJMDk1TVVNYkczYmstQmlKUzFQaTBFMEdhNVJGVHlES2d3WGlCSlVlN1c2UE9sd2kzckNrVGN2RFNULWdHY2JET3RDQUxSaXRfLXZQdG00RnlUM0E1TUo1YWNKOWxvQXRwSkhRYklQbmZUV3d3eHVfNEpMUUthMFlQUFgzS01RS2NvMXYtbnV4UVJOYkl4TTN0cw%3D%3D

code=AuthorizationCodeValue&id_token=IdTokenValue&<rest of properties for state>
```

### <a name="get-refresh-token"></a><span data-ttu-id="4301f-168">Pobierz token odświeżania</span><span class="sxs-lookup"><span data-stu-id="4301f-168">Get refresh token</span></span>

<span data-ttu-id="4301f-169">Aby uzyskać token odświeżenia, należy użyć kodu autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="4301f-169">You must then use your authorization code to get a refresh token:</span></span>

1. <span data-ttu-id="4301f-170">Wprowadź wywołanie POST do punktu końcowego logowania usługi Azure AD `https://login.microsoftonline.com/CSPTenantID/oauth2/token` przy użyciu kodu autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="4301f-170">Make a POST call to the Azure AD login endpoint `https://login.microsoftonline.com/CSPTenantID/oauth2/token` with the authorization code.</span></span> <span data-ttu-id="4301f-171">Aby zapoznać się z przykładem, zobacz następujące [przykładowe wywołanie](#sample-refresh-call).</span><span class="sxs-lookup"><span data-stu-id="4301f-171">For an example, see the following [sample call](#sample-refresh-call).</span></span>

2. <span data-ttu-id="4301f-172">Zwróć uwagę na zwracany token odświeżania.</span><span class="sxs-lookup"><span data-stu-id="4301f-172">Note the refresh token that is returned.</span></span>

3. <span data-ttu-id="4301f-173">Przechowuj token odświeżania w Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4301f-173">Store the refresh token in Azure Key Vault.</span></span> <span data-ttu-id="4301f-174">Aby uzyskać więcej informacji, zobacz [dokumentację interfejsu API Key Vault](/rest/api/keyvault/).</span><span class="sxs-lookup"><span data-stu-id="4301f-174">For more information, see the [Key Vault API documentation](/rest/api/keyvault/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4301f-175">Token odświeżania musi być [przechowywany jako wpis tajny](/rest/api/keyvault/setsecret/setsecret) w usłudze Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4301f-175">The refresh token must be [stored as a secret](/rest/api/keyvault/setsecret/setsecret) in Key Vault.</span></span>

#### <a name="sample-refresh-call"></a><span data-ttu-id="4301f-176">Przykładowe wywołanie odświeżania</span><span class="sxs-lookup"><span data-stu-id="4301f-176">Sample refresh call</span></span>

<span data-ttu-id="4301f-177">Żądanie symbolu zastępczego:</span><span class="sxs-lookup"><span data-stu-id="4301f-177">Placeholder request:</span></span>

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 966
Expect: 100-continue
```

<span data-ttu-id="4301f-178">Treść żądania:</span><span class="sxs-lookup"><span data-stu-id="4301f-178">Request body:</span></span>

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id&client_secret=Application-Secret&grant_type=authorization_code&code=AuthorizationCodeValue
```

<span data-ttu-id="4301f-179">Odpowiedź symbolu zastępczego:</span><span class="sxs-lookup"><span data-stu-id="4301f-179">Placeholder response:</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

<span data-ttu-id="4301f-180">Treść odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="4301f-180">Response body:</span></span>

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a><span data-ttu-id="4301f-181">Uzyskaj token dostępu</span><span class="sxs-lookup"><span data-stu-id="4301f-181">Get access token</span></span>

<span data-ttu-id="4301f-182">Aby umożliwić wywoływanie interfejsów API Centrum partnerskiego, należy uzyskać token dostępu.</span><span class="sxs-lookup"><span data-stu-id="4301f-182">You must obtain an access token before you can make calls to the Partner Center APIs.</span></span> <span data-ttu-id="4301f-183">Aby uzyskać token dostępu, należy użyć tokenu odświeżania, ponieważ token dostępu zwykle ma bardzo ograniczony okres istnienia (na przykład krótszy niż godzina).</span><span class="sxs-lookup"><span data-stu-id="4301f-183">You must use a refresh token to obtain an access token because access token generally have a very limited lifetime (for example, less than an hour).</span></span>

<span data-ttu-id="4301f-184">Żądanie symbolu zastępczego:</span><span class="sxs-lookup"><span data-stu-id="4301f-184">Placeholder request:</span></span>

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 1212
Expect: 100-continue
```

<span data-ttu-id="4301f-185">Treść żądania:</span><span class="sxs-lookup"><span data-stu-id="4301f-185">Request body:</span></span>

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id &client_secret= Application-Secret&grant_type=refresh_token&refresh_token=RefreshTokenVlaue&scope=openid
```

<span data-ttu-id="4301f-186">Odpowiedź symbolu zastępczego:</span><span class="sxs-lookup"><span data-stu-id="4301f-186">Placeholder response:</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

<span data-ttu-id="4301f-187">Treść odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="4301f-187">Response body:</span></span>

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a><span data-ttu-id="4301f-188">Tworzenie wywołań interfejsu API Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="4301f-188">Make Partner Center API calls</span></span>

<span data-ttu-id="4301f-189">Musisz użyć tokenu dostępu, aby wywołać interfejsy API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="4301f-189">You must use your access token to call the Partner Center APIs.</span></span> <span data-ttu-id="4301f-190">Zobacz poniższe przykładowe wywołanie.</span><span class="sxs-lookup"><span data-stu-id="4301f-190">See the following example call.</span></span>

#### <a name="example-partner-center-api-call"></a><span data-ttu-id="4301f-191">Przykład wywołania interfejsu API Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="4301f-191">Example Partner Center API call</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a><span data-ttu-id="4301f-192">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4301f-192">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="4301f-193">Możesz użyć [modułu programu PowerShell Centrum partnerskiego](https://www.powershellgallery.com/packages/PartnerCenter) , aby zmniejszyć wymaganą infrastrukturę do wymiany kodu autoryzacji dla tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="4301f-193">You can use the [Partner Center PowerShell module](https://www.powershellgallery.com/packages/PartnerCenter) to reduce the required infrastructure to exchange an authorization code for an access token.</span></span> <span data-ttu-id="4301f-194">Ta metoda jest opcjonalna w przypadku tworzenia [wywołań REST Centrum partnerskiego](#rest).</span><span class="sxs-lookup"><span data-stu-id="4301f-194">This method is optional for making [Partner Center REST calls](#rest).</span></span>

<span data-ttu-id="4301f-195">Aby uzyskać więcej informacji na temat tego procesu, zobacz [Secure App model](/powershell/partnercenter/secure-app-model) programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4301f-195">For more information on this process, see [Secure App Model](/powershell/partnercenter/secure-app-model) PowerShell documentation.</span></span>

1. <span data-ttu-id="4301f-196">Zainstaluj moduły Azure AD i centrum partnerskie programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4301f-196">Install the Azure AD and Partner Center PowerShell modules.</span></span>

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. <span data-ttu-id="4301f-197">Użyj polecenia **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** w celu przeprowadzenia procesu wyrażania zgody i przechwycenia wymaganego tokenu odświeżania.</span><span class="sxs-lookup"><span data-stu-id="4301f-197">Use the **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** command to perform the consent process and capture the required refresh token.</span></span>

    ```powershell
    $credential = Get-Credential

    New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > <span data-ttu-id="4301f-198">Parametr **serviceprincipal** jest używany z poleceniem **New-PartnerAccessToken** , ponieważ jest używana aplikacja usługi Azure AD z typem **sieci Web/API** .</span><span class="sxs-lookup"><span data-stu-id="4301f-198">The **ServicePrincipal** parameter is used with the **New-PartnerAccessToken** command because an Azure AD app with a type of **Web/API** is being used.</span></span> <span data-ttu-id="4301f-199">Ten typ aplikacji wymaga, aby identyfikator klienta i klucz tajny zostały uwzględnione w żądaniu tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="4301f-199">This type of app requires that a client identifier and secret be included in the access token request.</span></span> <span data-ttu-id="4301f-200">Po wywołaniu polecenia **Get-Credential** zostanie wyświetlony monit o podanie nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="4301f-200">When the **Get-Credential** command is invoked, you will be prompted to enter a username and password.</span></span> <span data-ttu-id="4301f-201">Wprowadź identyfikator aplikacji jako nazwę użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4301f-201">Enter the application identifier as the username.</span></span> <span data-ttu-id="4301f-202">Wprowadź klucz tajny aplikacji jako hasło.</span><span class="sxs-lookup"><span data-stu-id="4301f-202">Enter the application secret as the password.</span></span> <span data-ttu-id="4301f-203">Po wywołaniu polecenia **New-PartnerAccessToken** zostanie wyświetlony monit o ponowne wprowadzenie poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="4301f-203">When the **New-PartnerAccessToken** command is invoked, you will be prompted to enter credentials again.</span></span> <span data-ttu-id="4301f-204">Wprowadź poświadczenia dla konta usługi, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="4301f-204">Enter the credentials for the service account that you are using.</span></span> <span data-ttu-id="4301f-205">To konto usługi powinno być kontem partnerskim z odpowiednimi uprawnieniami.</span><span class="sxs-lookup"><span data-stu-id="4301f-205">This service account should be a partner account with appropriate permissions.</span></span>

3. <span data-ttu-id="4301f-206">Skopiuj wartość tokenu odświeżania.</span><span class="sxs-lookup"><span data-stu-id="4301f-206">Copy the refresh token value.</span></span>

    ```powershell
    $token.RefreshToken | clip
    ```

<span data-ttu-id="4301f-207">Wartość tokenu odświeżania należy przechowywać w bezpiecznym repozytorium, takim jak Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4301f-207">You should store the refresh token value in a secure repository, such as Azure Key Vault.</span></span> <span data-ttu-id="4301f-208">Aby uzyskać więcej informacji na temat korzystania z bezpiecznego modułu aplikacji za pomocą programu PowerShell, zobacz artykuł dotyczący usługi [uwierzytelniania wieloskładnikowego](/powershell/partnercenter/multi-factor-auth) .</span><span class="sxs-lookup"><span data-stu-id="4301f-208">For more information on how to leverage the secure application module with PowerShell, see the [multi-factor authentication](/powershell/partnercenter/multi-factor-auth) article.</span></span>
