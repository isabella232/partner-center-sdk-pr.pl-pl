---
title: Włączanie modelu aplikacji zabezpieczonych
description: Zabezpieczanie aplikacji Partner Center i panelu sterowania.
ms.date: 01/20/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 5d35c0512ba8edcf3742ee69d38c699a9a8c16d2
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906402"
---
# <a name="enabling-the-secure-application-model-framework"></a><span data-ttu-id="1730a-103">Włączanie środowiska modelu aplikacji zabezpieczonej</span><span class="sxs-lookup"><span data-stu-id="1730a-103">Enabling the Secure Application Model framework</span></span>

<span data-ttu-id="1730a-104">Firma Microsoft wprowadza bezpieczną, skalowalną platformę do uwierzytelniania partnerów dostawców rozwiązań w chmurze (CSP) i dostawców panelu sterowania (CPV) za pośrednictwem architektury Microsoft Azure Active Directory Multi-Factor Authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="1730a-104">Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure Active Directory Multi-Factor Authentication (MFA) architecture.</span></span>

<span data-ttu-id="1730a-105">Nowy model umożliwia podnieść poziom zabezpieczeń dla wywołań integracji Partner Center API.</span><span class="sxs-lookup"><span data-stu-id="1730a-105">You can use the new model to elevate security for Partner Center API integration calls.</span></span> <span data-ttu-id="1730a-106">Pomoże to wszystkim stronom (w tym partnerom programu CSP i partnerom CSP) chronić infrastrukturę i dane klientów przed zagrożeniami bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="1730a-106">This will help all parties (including Microsoft, CSP partners, and CPVs) to protect their infrastructure and customer data from security risks.</span></span>

## <a name="scope"></a><span data-ttu-id="1730a-107">Zakres</span><span class="sxs-lookup"><span data-stu-id="1730a-107">Scope</span></span>

<span data-ttu-id="1730a-108">Ten artykuł dotyczy następujących aktorów:</span><span class="sxs-lookup"><span data-stu-id="1730a-108">This article concerns the following actors:</span></span>

- <span data-ttu-id="1730a-109">Dostawcy oprogramowania panelu sterowania</span><span class="sxs-lookup"><span data-stu-id="1730a-109">CPVs</span></span>
  - <span data-ttu-id="1730a-110">Dostawca oprogramowania panelu sterowania (CPV) to niezależny dostawca oprogramowania, który opracowuje aplikacje, których partnerzy CSP mogą używać do integracji z interfejsami API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="1730a-110">A CPV is an independent software vendor that develops apps for use by CSP partners to integrate with Partner Center APIs.</span></span>
  - <span data-ttu-id="1730a-111">Dostawca CPV nie jest partnerem CSP z bezpośrednim dostępem do pulpitu nawigacyjnego lub interfejsów API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="1730a-111">A CPV isn't a CSP partner with direct access to the Partner Center dashboard or APIs.</span></span>

- <span data-ttu-id="1730a-112">Dostawcy pośredni dostawcy CSP i bezpośredni partnerzy programu CSP, którzy korzystają z identyfikatora aplikacji i uwierzytelniania użytkowników oraz bezpośrednio integrują się z Partner Center API.</span><span class="sxs-lookup"><span data-stu-id="1730a-112">CSP indirect providers and CSP direct partners who are using app ID + user authentication and directly integrate with Partner Center APIs.</span></span>

## <a name="security-requirements"></a><span data-ttu-id="1730a-113">Wymagania dotyczące zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="1730a-113">Security requirements</span></span>

<span data-ttu-id="1730a-114">Aby uzyskać szczegółowe informacje na temat wymagań dotyczących zabezpieczeń, zobacz [Partner Security Requirements (Wymagania dotyczące zabezpieczeń partnerów).](/partner-center/partner-security-requirements)</span><span class="sxs-lookup"><span data-stu-id="1730a-114">For details on security requirements, see [Partner Security Requirements](/partner-center/partner-security-requirements).</span></span>

## <a name="secure-application-model"></a><span data-ttu-id="1730a-115">model aplikacji zabezpieczonych</span><span class="sxs-lookup"><span data-stu-id="1730a-115">Secure Application Model</span></span>

<span data-ttu-id="1730a-116">Aplikacje z witryny Marketplace muszą personifikować uprawnienia partnera CSP w celu wywołania interfejsów API firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1730a-116">Marketplace applications need to impersonate CSP partner privileges to call Microsoft APIs.</span></span> <span data-ttu-id="1730a-117">Ataki na zabezpieczenia tych poufnych aplikacji mogą prowadzić do naruszenia danych klientów.</span><span class="sxs-lookup"><span data-stu-id="1730a-117">Security attacks on these sensitive applications can lead to the compromise of customer data.</span></span>

<span data-ttu-id="1730a-118">Aby uzyskać omówienie i szczegóły nowej struktury uwierzytelniania, pobierz [dokument model aplikacji zabezpieczonych framework.](https://assetsprod.microsoft.com/secure-application-model-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="1730a-118">For an overview and details of the new authentication framework, download the [Secure Application Model framework](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) document.</span></span> <span data-ttu-id="1730a-119">Ten dokument zawiera zasady i najlepsze rozwiązania, dzięki których aplikacje na platformie handlowej będą trwałe i odporne na naruszenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="1730a-119">This document covers principles and best practices to make marketplace applications sustainable and robust from security compromises.</span></span>

## <a name="samples"></a><span data-ttu-id="1730a-120">Samples</span><span class="sxs-lookup"><span data-stu-id="1730a-120">Samples</span></span>

<span data-ttu-id="1730a-121">W poniższych dokumentach z omówieniem i przykładowym kodzie opisano, jak partnerzy mogą zaimplementować model aplikacji zabezpieczonych platformę:</span><span class="sxs-lookup"><span data-stu-id="1730a-121">The following overview documents and sample code describe how partners can implement the Secure Application Model framework:</span></span>

- [<span data-ttu-id="1730a-122">Dokument z omówieniem protokołu CPV</span><span class="sxs-lookup"><span data-stu-id="1730a-122">CPV overview document</span></span>](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [<span data-ttu-id="1730a-123">Dokument z omówieniem programu CSP</span><span class="sxs-lookup"><span data-stu-id="1730a-123">CSP overview document</span></span>](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [<span data-ttu-id="1730a-124">Przykłady dla .NET</span><span class="sxs-lookup"><span data-stu-id="1730a-124">.NET Samples</span></span>](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [<span data-ttu-id="1730a-125">Przykłady dla języka Java</span><span class="sxs-lookup"><span data-stu-id="1730a-125">Java Samples</span></span>](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [<span data-ttu-id="1730a-126">Instrukcje i przykłady DOTYCZĄCE REST</span><span class="sxs-lookup"><span data-stu-id="1730a-126">REST instructions and samples</span></span>](#rest)
- [<span data-ttu-id="1730a-127">Instrukcje i przykłady programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="1730a-127">PowerShell instructions and samples</span></span>](#powershell)

## <a name="rest"></a><span data-ttu-id="1730a-128">REST</span><span class="sxs-lookup"><span data-stu-id="1730a-128">REST</span></span>

<span data-ttu-id="1730a-129">Aby wykonać wywołania REST za pomocą model aplikacji zabezpieczonych z przykładowym kodem, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1730a-129">To to make REST calls with the Secure Application Model framework with sample code, follow these steps:</span></span>

1. [<span data-ttu-id="1730a-130">Tworzenie aplikacji internetowej</span><span class="sxs-lookup"><span data-stu-id="1730a-130">Create a web app</span></span>](#create-a-web-app)

2. [<span data-ttu-id="1730a-131">Uzyskiwanie kodu autoryzacji</span><span class="sxs-lookup"><span data-stu-id="1730a-131">Get an authorization code</span></span>](#get-authorization-code)

3. [<span data-ttu-id="1730a-132">Uzyskiwanie tokenu odświeżania</span><span class="sxs-lookup"><span data-stu-id="1730a-132">Get a refresh token</span></span>](#get-refresh-token)

4. [<span data-ttu-id="1730a-133">Pobranie tokenu dostępu</span><span class="sxs-lookup"><span data-stu-id="1730a-133">Get an access token</span></span>](#get-access-token)

5. [<span data-ttu-id="1730a-134">Wykonywanie wywołania interfejsu API Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="1730a-134">Make a Partner Center API call</span></span>](#make-partner-center-api-calls)

> [!TIP]
> <span data-ttu-id="1730a-135">Możesz użyć modułu Partner Center PowerShell, aby uzyskać kod autoryzacji i token odświeżania.</span><span class="sxs-lookup"><span data-stu-id="1730a-135">You can use the Partner Center PowerShell module to get an authorization code and a refresh token.</span></span> <span data-ttu-id="1730a-136">Tę opcję można wybrać w miejsce kroków 2 i 3.</span><span class="sxs-lookup"><span data-stu-id="1730a-136">You can choose this option in place of steps 2 and 3.</span></span> <span data-ttu-id="1730a-137">Aby uzyskać więcej informacji, zobacz sekcję [programu PowerShell i przykłady](#powershell).</span><span class="sxs-lookup"><span data-stu-id="1730a-137">For more information, see the [PowerShell section and examples](#powershell).</span></span>

### <a name="create-a-web-app"></a><span data-ttu-id="1730a-138">Tworzenie aplikacji internetowej</span><span class="sxs-lookup"><span data-stu-id="1730a-138">Create a web app</span></span>

<span data-ttu-id="1730a-139">Przed wykonaniem wywołań REST należy utworzyć i zarejestrować aplikację internetową Partner Center aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="1730a-139">You must create and register a web app in Partner Center before making REST calls.</span></span>

1. <span data-ttu-id="1730a-140">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1730a-140">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="1730a-141">Utwórz aplikację Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1730a-141">Create an Azure Active Directory (Azure AD) app.</span></span>

3. <span data-ttu-id="1730a-142">Nadaj delegowane uprawnienia aplikacji do następujących zasobów, w zależności od *wymagań aplikacji.*</span><span class="sxs-lookup"><span data-stu-id="1730a-142">Give delegated application permissions to the following resources, *depending on your application's requirements*.</span></span> <span data-ttu-id="1730a-143">W razie potrzeby możesz dodać więcej delegowanych uprawnień do zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1730a-143">If necessary, you can add more delegated permissions for application resources.</span></span>

   1. <span data-ttu-id="1730a-144">**Microsoft Partner Center** (niektóre dzierżawy pokazują to jako **SampleBECApp**)</span><span class="sxs-lookup"><span data-stu-id="1730a-144">**Microsoft Partner Center** (some tenants show this as **SampleBECApp**)</span></span>

   2. <span data-ttu-id="1730a-145">**Interfejsy API usługi Azure Management** (jeśli planujesz wywołać interfejsy API platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="1730a-145">**Azure Management APIs** (if you are planning to call Azure APIs)</span></span>

   3. <span data-ttu-id="1730a-146">**Windows Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="1730a-146">**Windows Azure Active Directory**</span></span>

4. <span data-ttu-id="1730a-147">Upewnij się, że adres URL strony głównej aplikacji jest ustawiony na punkt końcowy, w którym działa żywa aplikacja internetowa.</span><span class="sxs-lookup"><span data-stu-id="1730a-147">Make sure that the home URL of your app is set to an endpoint where a live web app is running.</span></span> <span data-ttu-id="1730a-148">Ta aplikacja musi zaakceptować kod [autoryzacji z](#get-authorization-code) wywołania logowania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1730a-148">This app will need to accept the [authorization code](#get-authorization-code) from the Azure AD login call.</span></span> <span data-ttu-id="1730a-149">Na przykład w przykładowym kodzie w [poniższej sekcji](#get-authorization-code)aplikacja internetowa działa pod następującym kodem: `https://localhost:44395/` .</span><span class="sxs-lookup"><span data-stu-id="1730a-149">For example, in the example code in [the following section](#get-authorization-code), the web app is running at `https://localhost:44395/`.</span></span>

5. <span data-ttu-id="1730a-150">Zwróć uwagę na następujące informacje z ustawień aplikacji internetowej w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="1730a-150">Note the following information from your web app's settings in Azure AD:</span></span>

   - <span data-ttu-id="1730a-151">Identyfikator aplikacji</span><span class="sxs-lookup"><span data-stu-id="1730a-151">Application ID</span></span>
   - <span data-ttu-id="1730a-152">Klucz tajny aplikacji</span><span class="sxs-lookup"><span data-stu-id="1730a-152">Application secret</span></span>

> [!NOTE]
> <span data-ttu-id="1730a-153">Zaleca się używanie [certyfikatu jako tajnego certyfikatu aplikacji.](/azure/active-directory/develop/active-directory-certificate-credentials)</span><span class="sxs-lookup"><span data-stu-id="1730a-153">It is recommended to [use a certificate as your application secret](/azure/active-directory/develop/active-directory-certificate-credentials).</span></span> <span data-ttu-id="1730a-154">Można jednak również utworzyć klucz aplikacji w Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1730a-154">However, you can also create an application key in the Azure portal.</span></span> <span data-ttu-id="1730a-155">Przykładowy kod w [poniższej sekcji](#get-authorization-code) używa klucza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1730a-155">The sample code in [the following section](#get-authorization-code) uses an application key.</span></span>

### <a name="get-authorization-code"></a><span data-ttu-id="1730a-156">Uzyskiwanie kodu autoryzacji</span><span class="sxs-lookup"><span data-stu-id="1730a-156">Get authorization code</span></span>

<span data-ttu-id="1730a-157">Musisz uzyskać kod autoryzacji dla aplikacji internetowej do zaakceptowania z wywołania logowania usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="1730a-157">You must get an authorization code for your web app to accept from the Azure AD login call:</span></span>

1. <span data-ttu-id="1730a-158">Zaloguj się do usługi Azure AD pod następującym adresem URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) .</span><span class="sxs-lookup"><span data-stu-id="1730a-158">Log in to Azure AD at the following URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1).</span></span> <span data-ttu-id="1730a-159">Pamiętaj, aby zalogować się przy użyciu konta użytkownika, z którego będą Partner Center interfejsu API (na przykład agenta administracyjnego lub konta agenta sprzedaży).</span><span class="sxs-lookup"><span data-stu-id="1730a-159">Be sure to log in with the user account from which you will make Partner Center API calls (such as an admin agent or sales agent account).</span></span>

2. <span data-ttu-id="1730a-160">Zastąp **identyfikator application-id** identyfikatorem aplikacji usługi Azure AD (identyfikatorem GUID).</span><span class="sxs-lookup"><span data-stu-id="1730a-160">Replace **Application-Id** with your Azure AD app ID (GUID).</span></span>

3. <span data-ttu-id="1730a-161">Po wyświetleniu monitu zaloguj się przy użyciu konta użytkownika ze skonfigurowaną usługą MFA.</span><span class="sxs-lookup"><span data-stu-id="1730a-161">When prompted, log in with your user account with MFA configured.</span></span>

4. <span data-ttu-id="1730a-162">Po wyświetleniu monitu wprowadź dodatkowe informacje uwierzytelniania wieloskładnikowego (numer telefonu lub adres e-mail), aby zweryfikować logowanie.</span><span class="sxs-lookup"><span data-stu-id="1730a-162">When prompted, enter additional MFA information (phone number or email address) to verify your login.</span></span>

5. <span data-ttu-id="1730a-163">Po zalogowaniu przeglądarka przekieruje wywołanie do punktu końcowego aplikacji internetowej przy użyciu kodu autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="1730a-163">After you are logged in, the browser will redirect the call to your web app endpoint with your authorization code.</span></span> <span data-ttu-id="1730a-164">Na przykład poniższy przykładowy kod przekierowuje do `https://localhost:44395/` .</span><span class="sxs-lookup"><span data-stu-id="1730a-164">For example, the following sample code redirects to `https://localhost:44395/`.</span></span>

#### <a name="authorization-code-call-trace"></a><span data-ttu-id="1730a-165">Śledzenie wywołania kodu autoryzacji</span><span class="sxs-lookup"><span data-stu-id="1730a-165">Authorization code call trace</span></span>

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

### <a name="get-refresh-token"></a><span data-ttu-id="1730a-166">Uzyskiwanie tokenu odświeżania</span><span class="sxs-lookup"><span data-stu-id="1730a-166">Get refresh token</span></span>

<span data-ttu-id="1730a-167">Następnie należy użyć kodu autoryzacji, aby uzyskać token odświeżania:</span><span class="sxs-lookup"><span data-stu-id="1730a-167">You must then use your authorization code to get a refresh token:</span></span>

1. <span data-ttu-id="1730a-168">Wywołaj wywołanie POST do punktu końcowego logowania usługi Azure AD `https://login.microsoftonline.com/CSPTenantID/oauth2/token` przy użyciu kodu autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="1730a-168">Make a POST call to the Azure AD login endpoint `https://login.microsoftonline.com/CSPTenantID/oauth2/token` with the authorization code.</span></span> <span data-ttu-id="1730a-169">Aby uzyskać przykład, zobacz następujące [przykładowe wywołanie](#sample-refresh-call).</span><span class="sxs-lookup"><span data-stu-id="1730a-169">For an example, see the following [sample call](#sample-refresh-call).</span></span>

2. <span data-ttu-id="1730a-170">Zwróć uwagę na zwracany token odświeżania.</span><span class="sxs-lookup"><span data-stu-id="1730a-170">Note the refresh token that is returned.</span></span>

3. <span data-ttu-id="1730a-171">Przechowuj token odświeżania w Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1730a-171">Store the refresh token in Azure Key Vault.</span></span> <span data-ttu-id="1730a-172">Aby uzyskać więcej informacji, zobacz [dokumentację Key Vault API.](/rest/api/keyvault/)</span><span class="sxs-lookup"><span data-stu-id="1730a-172">For more information, see the [Key Vault API documentation](/rest/api/keyvault/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1730a-173">Token odświeżania musi być [przechowywany jako wpis tajny](/rest/api/keyvault/setsecret/setsecret) w usłudze Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1730a-173">The refresh token must be [stored as a secret](/rest/api/keyvault/setsecret/setsecret) in Key Vault.</span></span>

#### <a name="sample-refresh-call"></a><span data-ttu-id="1730a-174">Przykładowe wywołanie odświeżania</span><span class="sxs-lookup"><span data-stu-id="1730a-174">Sample refresh call</span></span>

<span data-ttu-id="1730a-175">Żądanie symbolu zastępczego:</span><span class="sxs-lookup"><span data-stu-id="1730a-175">Placeholder request:</span></span>

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 966
Expect: 100-continue
```

<span data-ttu-id="1730a-176">Treść żądania:</span><span class="sxs-lookup"><span data-stu-id="1730a-176">Request body:</span></span>

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id&client_secret=Application-Secret&grant_type=authorization_code&code=AuthorizationCodeValue
```

<span data-ttu-id="1730a-177">Odpowiedź symbolu zastępczego:</span><span class="sxs-lookup"><span data-stu-id="1730a-177">Placeholder response:</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

<span data-ttu-id="1730a-178">Treść odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="1730a-178">Response body:</span></span>

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a><span data-ttu-id="1730a-179">Uzyskiwanie tokenu dostępu</span><span class="sxs-lookup"><span data-stu-id="1730a-179">Get access token</span></span>

<span data-ttu-id="1730a-180">Aby można było wykonać wywołania do interfejsów API usługi Partner Center, należy uzyskać token dostępu.</span><span class="sxs-lookup"><span data-stu-id="1730a-180">You must obtain an access token before you can make calls to the Partner Center APIs.</span></span> <span data-ttu-id="1730a-181">Aby uzyskać token dostępu, należy użyć tokenu odświeżania, ponieważ tokeny dostępu zazwyczaj mają bardzo ograniczony okres istnienia (na przykład mniej niż godzinę).</span><span class="sxs-lookup"><span data-stu-id="1730a-181">You must use a refresh token to obtain an access token because access tokens generally have a very limited lifetime (for example, less than an hour).</span></span>

<span data-ttu-id="1730a-182">Żądanie symbolu zastępczego:</span><span class="sxs-lookup"><span data-stu-id="1730a-182">Placeholder request:</span></span>

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 1212
Expect: 100-continue
```

<span data-ttu-id="1730a-183">Treść żądania:</span><span class="sxs-lookup"><span data-stu-id="1730a-183">Request body:</span></span>

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id &client_secret= Application-Secret&grant_type=refresh_token&refresh_token=RefreshTokenVlaue&scope=openid
```

<span data-ttu-id="1730a-184">Odpowiedź symbolu zastępczego:</span><span class="sxs-lookup"><span data-stu-id="1730a-184">Placeholder response:</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

<span data-ttu-id="1730a-185">Treść odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="1730a-185">Response body:</span></span>

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a><span data-ttu-id="1730a-186">Wywołania Partner Center API</span><span class="sxs-lookup"><span data-stu-id="1730a-186">Make Partner Center API calls</span></span>

<span data-ttu-id="1730a-187">Aby wywołać interfejsy API Partner Center dostępu, należy użyć tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1730a-187">You must use your access token to call the Partner Center APIs.</span></span> <span data-ttu-id="1730a-188">Zobacz następujące przykładowe wywołanie.</span><span class="sxs-lookup"><span data-stu-id="1730a-188">See the following example call.</span></span>

#### <a name="example-partner-center-api-call"></a><span data-ttu-id="1730a-189">Przykład wywołania Partner Center API</span><span class="sxs-lookup"><span data-stu-id="1730a-189">Example Partner Center API call</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a><span data-ttu-id="1730a-190">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1730a-190">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="1730a-191">Możesz użyć modułu Partner Center [PowerShell,](https://www.powershellgallery.com/packages/PartnerCenter) aby zmniejszyć wymaganą infrastrukturę do wymiany kodu autoryzacji na token dostępu.</span><span class="sxs-lookup"><span data-stu-id="1730a-191">You can use the [Partner Center PowerShell module](https://www.powershellgallery.com/packages/PartnerCenter) to reduce the required infrastructure to exchange an authorization code for an access token.</span></span> <span data-ttu-id="1730a-192">Ta metoda jest opcjonalna do tworzenia [Partner Center REST.](#rest)</span><span class="sxs-lookup"><span data-stu-id="1730a-192">This method is optional for making [Partner Center REST calls](#rest).</span></span>

<span data-ttu-id="1730a-193">Aby uzyskać więcej informacji na temat tego procesu, zobacz [dokumentację dotyczącą bezpiecznego model aplikacji](/powershell/partnercenter/secure-app-model) PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1730a-193">For more information on this process, see [Secure App Model](/powershell/partnercenter/secure-app-model) PowerShell documentation.</span></span>

1. <span data-ttu-id="1730a-194">Zainstaluj usługę Azure AD i Partner Center programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1730a-194">Install the Azure AD and Partner Center PowerShell modules.</span></span>

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. <span data-ttu-id="1730a-195">Użyj polecenia **[New-PartnerAccessToken,](/powershell/module/partnercenter/new-partneraccesstoken)** aby wykonać proces wyrażania zgody i przechwycić wymagany token odświeżania.</span><span class="sxs-lookup"><span data-stu-id="1730a-195">Use the **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** command to perform the consent process and capture the required refresh token.</span></span>

    ```powershell
    $credential = Get-Credential

    New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > <span data-ttu-id="1730a-196">Parametr **ServicePrincipal** jest używany z poleceniem **New-PartnerAccessToken,** ponieważ jest używana aplikacja usługi Azure AD o typie **Internet/interfejs API.**</span><span class="sxs-lookup"><span data-stu-id="1730a-196">The **ServicePrincipal** parameter is used with the **New-PartnerAccessToken** command because an Azure AD app with a type of **Web/API** is being used.</span></span> <span data-ttu-id="1730a-197">Ten typ aplikacji wymaga, aby identyfikator klienta i wpis tajny zostały uwzględnione w żądaniu tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1730a-197">This type of app requires that a client identifier and secret be included in the access token request.</span></span> <span data-ttu-id="1730a-198">Po **wywołaniu polecenia Get-Credential** zostanie wyświetlony monit o wprowadzenie nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="1730a-198">When the **Get-Credential** command is invoked, you will be prompted to enter a username and password.</span></span> <span data-ttu-id="1730a-199">Wprowadź identyfikator aplikacji jako nazwę użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1730a-199">Enter the application identifier as the username.</span></span> <span data-ttu-id="1730a-200">Wprowadź wpis tajny aplikacji jako hasło.</span><span class="sxs-lookup"><span data-stu-id="1730a-200">Enter the application secret as the password.</span></span> <span data-ttu-id="1730a-201">Po **wywołaniu polecenia New-PartnerAccessToken** zostanie ponownie wyświetlony monit o wprowadzenie poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="1730a-201">When the **New-PartnerAccessToken** command is invoked, you will be prompted to enter credentials again.</span></span> <span data-ttu-id="1730a-202">Wprowadź poświadczenia dla używanego konta usługi.</span><span class="sxs-lookup"><span data-stu-id="1730a-202">Enter the credentials for the service account that you are using.</span></span> <span data-ttu-id="1730a-203">To konto usługi powinno być kontem partnera z odpowiednimi uprawnieniami.</span><span class="sxs-lookup"><span data-stu-id="1730a-203">This service account should be a partner account with appropriate permissions.</span></span>

3. <span data-ttu-id="1730a-204">Skopiuj wartość tokenu odświeżania.</span><span class="sxs-lookup"><span data-stu-id="1730a-204">Copy the refresh token value.</span></span>

    ```powershell
    $token.RefreshToken | clip
    ```

<span data-ttu-id="1730a-205">Wartość tokenu odświeżania należy przechowywać w bezpiecznym repozytorium, takim jak Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1730a-205">You should store the refresh token value in a secure repository, such as Azure Key Vault.</span></span> <span data-ttu-id="1730a-206">Aby uzyskać więcej informacji na temat wykorzystania modułu bezpiecznej aplikacji przy użyciu programu PowerShell, zobacz artykuł [Uwierzytelnianie wieloskładnikowe.](/powershell/partnercenter/multi-factor-auth)</span><span class="sxs-lookup"><span data-stu-id="1730a-206">For more information on how to leverage the secure application module with PowerShell, see the [multi-factor authentication](/powershell/partnercenter/multi-factor-auth) article.</span></span>
