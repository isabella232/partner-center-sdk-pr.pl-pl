---
title: Uwierzytelnianie w Centrum partnerskim
description: Centrum partnerskie używa usługi Azure AD do uwierzytelniania i korzystania z interfejsów API Centrum partnerskiego należy prawidłowo skonfigurować ustawienia uwierzytelniania.
ms.date: 11/13/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.openlocfilehash: 46ef9c6bc151c368281e943b7d24ebc07e34b66d
ms.sourcegitcommit: 64c498d3571f2287305968890578bc7396779621
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/19/2020
ms.locfileid: "97770291"
---
# <a name="partner-center-authentication"></a><span data-ttu-id="bf46f-103">Uwierzytelnianie w Centrum partnerskim</span><span class="sxs-lookup"><span data-stu-id="bf46f-103">Partner Center authentication</span></span>

<span data-ttu-id="bf46f-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="bf46f-104">**Applies to:**</span></span>

- <span data-ttu-id="bf46f-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="bf46f-105">Partner Center</span></span>
- <span data-ttu-id="bf46f-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="bf46f-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="bf46f-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="bf46f-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="bf46f-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="bf46f-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="bf46f-109">Centrum partnerskie w celu uwierzytelniania używa usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bf46f-109">Partner Center uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="bf46f-110">Korzystając z interfejsu API Centrum partnerskiego, zestawu SDK lub modułu programu PowerShell, należy prawidłowo skonfigurować aplikację usługi Azure AD, a następnie zażądać tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="bf46f-110">When interacting with the Partner Center API, SDK, or PowerShell module you must correctly configure an Azure AD application and then request an access token.</span></span> <span data-ttu-id="bf46f-111">Tokeny dostępu uzyskane przy użyciu tylko aplikacji lub uwierzytelnianie użytkownika i aplikacji mogą być używane z centrum partnerskim.</span><span class="sxs-lookup"><span data-stu-id="bf46f-111">Access tokens obtained using app only or app + user authentication can be used with the Partner Center.</span></span> <span data-ttu-id="bf46f-112">Istnieją jednak dwa ważne elementy, które należy wziąć pod uwagę</span><span class="sxs-lookup"><span data-stu-id="bf46f-112">However, there are two important items that need to be considered</span></span>

- <span data-ttu-id="bf46f-113">Użyj uwierzytelniania wieloskładnikowego podczas uzyskiwania dostępu do interfejsu API Centrum partnerskiego przy użyciu aplikacji + uwierzytelnianie użytkowników.</span><span class="sxs-lookup"><span data-stu-id="bf46f-113">Use multi-factor authentication when accessing the Partner Center API using app + user authentication.</span></span> <span data-ttu-id="bf46f-114">Aby uzyskać więcej informacji dotyczących tej zmiany, zobacz [Włączanie bezpiecznego modelu aplikacji](enable-secure-app-model.md).</span><span class="sxs-lookup"><span data-stu-id="bf46f-114">For more information regarding this change, see [Enable secure application model](enable-secure-app-model.md).</span></span>

- <span data-ttu-id="bf46f-115">Nie wszystkie operacje obsługują tylko aplikacje w interfejsie API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="bf46f-115">Not all of the operations the Partner Center API support app only authentication.</span></span> <span data-ttu-id="bf46f-116">Istnieją pewne scenariusze, w których będzie wymagane użycie aplikacji i uwierzytelniania użytkowników.</span><span class="sxs-lookup"><span data-stu-id="bf46f-116">There are certain scenarios where you'll be required to use app + user authentication.</span></span> <span data-ttu-id="bf46f-117">W sekcji *wymagania wstępne* dotyczące każdego [artykułu](scenarios.md)znajdziesz dokumentację zawierającą informacje o tym, czy obsługiwane są tylko aplikacje uwierzytelnianie, aplikacja + uwierzytelnianie użytkownika, czy też oba te elementy.</span><span class="sxs-lookup"><span data-stu-id="bf46f-117">Under the *Prerequisites* heading on each [article](scenarios.md), you'll find documentation that states whether app only authentication, app + user authentication, or both are supported.</span></span>

## <a name="initial-setup"></a><span data-ttu-id="bf46f-118">Początkowa konfiguracja</span><span class="sxs-lookup"><span data-stu-id="bf46f-118">Initial setup</span></span>

1. <span data-ttu-id="bf46f-119">Aby rozpocząć, musisz upewnić się, że masz zarówno konto głównego centrum partnerskiego, jak i konto Centrum partnerskiego usługi piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="bf46f-119">To begin, you need to make sure that you have both a primary Partner Center account, and an integration sandbox Partner Center account.</span></span> <span data-ttu-id="bf46f-120">Aby uzyskać więcej informacji, zobacz [Konfigurowanie kont Centrum partnerskiego na potrzeby dostępu do interfejsu API](set-up-api-access-in-partner-center.md).</span><span class="sxs-lookup"><span data-stu-id="bf46f-120">For more information, see [Set up Partner Center accounts for API access](set-up-api-access-in-partner-center.md).</span></span> <span data-ttu-id="bf46f-121">Zanotuj identyfikator rejestracji i wpis tajny aplikacji usługi Azure AAD (klucz tajny klienta jest wymagany tylko do identyfikacji aplikacji) zarówno dla konta podstawowego, jak i konta piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="bf46f-121">Make note of the Azure AAD App registration ID and Secret (client secret is required for App only identification) for both your primary account and your integration sandbox account.</span></span>

2. <span data-ttu-id="bf46f-122">Zaloguj się do usługi Azure AD z poziomu Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="bf46f-122">Sign in to Azure AD from the Azure portal.</span></span> <span data-ttu-id="bf46f-123">W obszarze **uprawnienia do innych aplikacji** Ustaw uprawnienia dla **systemu Windows Azure Active Directory** na **delegowane uprawnienia**, a następnie wybierz pozycję **dostęp do katalogu jako zalogowany użytkownik** i **Zaloguj się i odczytaj profil użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="bf46f-123">In **permissions to other applications**, set permissions for **Windows Azure Active Directory** to **Delegated Permissions**, and select both **Access the directory as the signed-in user** and **Sign in and read user profile**.</span></span>

3. <span data-ttu-id="bf46f-124">W Azure Portal **Dodaj aplikację**.</span><span class="sxs-lookup"><span data-stu-id="bf46f-124">In the Azure portal, **Add application**.</span></span> <span data-ttu-id="bf46f-125">Wyszukaj frazę "Microsoft Partner Center", która jest aplikacją Microsoft Partner Center.</span><span class="sxs-lookup"><span data-stu-id="bf46f-125">Search for "Microsoft Partner Center", which is the Microsoft Partner Center application.</span></span> <span data-ttu-id="bf46f-126">Ustaw **uprawnienia delegowane** na **dostęp do interfejsu API Centrum partnerskiego**.</span><span class="sxs-lookup"><span data-stu-id="bf46f-126">Set the **Delegated Permissions** to **Access Partner Center API**.</span></span> <span data-ttu-id="bf46f-127">Jeśli używasz Centrum partnerskiego do Microsoft Cloud Niemiec lub Centrum partnerskiego dla Microsoft Cloud dla instytucji rządowych USA, ten krok jest obowiązkowy.</span><span class="sxs-lookup"><span data-stu-id="bf46f-127">If you are using Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government, this step is mandatory.</span></span> <span data-ttu-id="bf46f-128">Jeśli używasz wystąpienia globalnego Centrum partnerskiego, ten krok jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="bf46f-128">If you are using Partner Center global instance, this step is optional.</span></span> <span data-ttu-id="bf46f-129">Partnerzy programu CSP mogą użyć funkcji zarządzania aplikacjami w portalu Centrum partnerskiego, aby pominąć ten krok dla wystąpienia globalnego Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="bf46f-129">CSP Partners can use the App Management feature in the Partner Center portal to bypass this step for Partner Center global instance.</span></span>

## <a name="app-only-authentication"></a><span data-ttu-id="bf46f-130">Uwierzytelnianie tylko aplikacji</span><span class="sxs-lookup"><span data-stu-id="bf46f-130">App-only authentication</span></span>

<span data-ttu-id="bf46f-131">Jeśli chcesz użyć uwierzytelniania tylko do aplikacji w celu uzyskania dostępu do interfejsu API REST Centrum partnerskiego, interfejsu API platformy .NET, interfejsu API języka Java lub modułu programu PowerShell, możesz to zrobić, wykonując poniższe instrukcje.</span><span class="sxs-lookup"><span data-stu-id="bf46f-131">If you would like to use app-only authentication to access the Partner Center REST API, .NET API, Java API, or PowerShell module then you can do so by leveraging the following instructions.</span></span>

## <a name="net-app-only-authentication"></a><span data-ttu-id="bf46f-132">.NET (uwierzytelnianie tylko aplikacji)</span><span class="sxs-lookup"><span data-stu-id="bf46f-132">.NET (app-only authentication)</span></span>

```csharp
public static IAggregatePartner GetPartnerCenterTokenUsingAppCredentials()
{
    IPartnerCredentials partnerCredentials =
        PartnerCredentials.Instance.GenerateByApplicationCredentials(
            PartnerApplicationConfiguration.ApplicationId,
            PartnerApplicationConfiguration.ApplicationSecret,
            PartnerApplicationConfiguration.ApplicationDomain);

    // Create operations instance with partnerCredentials.
    return PartnerService.Instance.CreatePartnerOperations(partnerCredentials);
}
```

## <a name="java-app-only-authentication"></a><span data-ttu-id="bf46f-133">Java (uwierzytelnianie tylko w aplikacji)</span><span class="sxs-lookup"><span data-stu-id="bf46f-133">Java (app-only authentication)</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

```java
public IAggregatePartner getAppPartnerOperations()
{
    IPartnerCredentials appCredentials =
        PartnerCredentials.getInstance().generateByApplicationCredentials(
        PartnerApplicationConfiguration.getApplicationId(),
        PartnerApplicationConfiguration.getApplicationSecret(),
        PartnerApplicationConfiguration.getApplicationDomain());

    return PartnerService.getInstance().createPartnerOperations( appCredentials );
}
```

## <a name="rest-app-only-authentication"></a><span data-ttu-id="bf46f-134">REST (uwierzytelnianie tylko w aplikacji)</span><span class="sxs-lookup"><span data-stu-id="bf46f-134">REST (app-only authentication)</span></span>

### <a name="rest-request"></a><span data-ttu-id="bf46f-135">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="bf46f-135">REST request</span></span>

```http
POST https://login.microsoftonline.com/{tenantId}/oauth2/token HTTP/1.1
Accept: application/json
return-client-request-id: true
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Host: login.microsoftonline.com
Content-Length: 194
Expect: 100-continue

resource=https%3A%2F%2Fgraph.windows.net&client_id={client-id-here}&client_secret={client-secret-here}&grant_type=client_credentials
```

### <a name="rest-response"></a><span data-ttu-id="bf46f-136">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="bf46f-136">REST response</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

## <a name="app--user-authentication"></a><span data-ttu-id="bf46f-137">Aplikacja + uwierzytelnianie użytkownika</span><span class="sxs-lookup"><span data-stu-id="bf46f-137">App + User authentication</span></span>

<span data-ttu-id="bf46f-138">Historycznie [Przydziel poświadczenia hasła właściciela zasobu](https://tools.ietf.org/html/rfc6749#section-4.3) , aby zażądać tokenu dostępu do użycia w module interfejsu API REST Centrum partnerskiego, interfejsu API platformy .NET, interfejsu API języka Java lub modułu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bf46f-138">Historically the [resource owner password credentials grant](https://tools.ietf.org/html/rfc6749#section-4.3) has been used to request an access token for use with the Partner Center REST API, .NET API, Java API, or PowerShell module.</span></span> <span data-ttu-id="bf46f-139">Ta metoda została użyta do żądania tokenu dostępu z Azure Active Directory przy użyciu identyfikatora klienta i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bf46f-139">That method was used to request an access token from Azure Active Directory using a client identifier and user credentials.</span></span> <span data-ttu-id="bf46f-140">Jednak takie podejście przestanie działać, ponieważ centrum partnerskie wymaga uwierzytelniania wieloskładnikowego w przypadku korzystania z aplikacji i uwierzytelniania użytkowników.</span><span class="sxs-lookup"><span data-stu-id="bf46f-140">However, this approach will no longer work because Partner Center requires multi-factor authentication, when using app + user authentication.</span></span> <span data-ttu-id="bf46f-141">Aby zapewnić zgodność z tym wymaganiem, firma Microsoft wprowadziła bezpieczną, skalowalną platformę do uwierzytelniania partnerów dostawcy rozwiązań w chmurze (CSP) i dostawców panelu sterowania (CPV) przy użyciu uwierzytelniania wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="bf46f-141">To comply with this requirement Microsoft has introduced a secure, scalable framework for authenticating Cloud Solution Provider (CSP) partners and control panel vendors (CPV) using multi-factor authentication.</span></span> <span data-ttu-id="bf46f-142">Ta struktura jest znana jako bezpieczny model aplikacji i składa się z procesu wyrażania zgody oraz żądania tokenu dostępu przy użyciu tokenu odświeżania.</span><span class="sxs-lookup"><span data-stu-id="bf46f-142">This framework is known as the Secure Application Model, and it is composed of a consent process and a request for an access token using a refresh token.</span></span>

### <a name="partner-consent"></a><span data-ttu-id="bf46f-143">Zgoda partnera</span><span class="sxs-lookup"><span data-stu-id="bf46f-143">Partner consent</span></span>

<span data-ttu-id="bf46f-144">Proces zgody partnera to interaktywny proces, w którym partner uwierzytelnia się przy użyciu uwierzytelniania wieloskładnikowego, jest wysyłany do aplikacji, a token odświeżania jest przechowywany w bezpiecznym repozytorium, takim jak Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="bf46f-144">The partner consent process is an interactive process where the partner authenticates using multi-factor authentication, consents to the application, and a refresh token is stored in a secure repository such as Azure Key Vault.</span></span> <span data-ttu-id="bf46f-145">Zalecamy, aby dla tego procesu używać dedykowanego konta do celów związanych z integracją.</span><span class="sxs-lookup"><span data-stu-id="bf46f-145">We recommend that a dedicated account for integration purposes be used for this process.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf46f-146">Należy włączyć odpowiednie rozwiązanie do uwierzytelniania wieloskładnikowego dla konta usługi używanego w procesie zgody partnera.</span><span class="sxs-lookup"><span data-stu-id="bf46f-146">The appropriate multi-factor authentication solution should be enabled for the service account used in the partner consent process.</span></span> <span data-ttu-id="bf46f-147">Jeśli nie, wynikowy token odświeżania nie będzie zgodny z wymaganiami dotyczącymi zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="bf46f-147">If it isn't then the resulting refresh token will not be compliant with security requirements.</span></span>

### <a name="samples-for-app--user-authentication"></a><span data-ttu-id="bf46f-148">Przykłady dla aplikacji i uwierzytelniania użytkowników</span><span class="sxs-lookup"><span data-stu-id="bf46f-148">Samples for App + User authentication</span></span>

<span data-ttu-id="bf46f-149">Proces zgody partnera można wykonać na wiele sposobów.</span><span class="sxs-lookup"><span data-stu-id="bf46f-149">The partner consent process can be performed in a number of ways.</span></span> <span data-ttu-id="bf46f-150">Aby pomóc partnerom zrozumieć, jak wykonać każdą wymaganą operację, opracowano następujące przykłady.</span><span class="sxs-lookup"><span data-stu-id="bf46f-150">To help partners understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="bf46f-151">W przypadku zaimplementowania odpowiedniego rozwiązania w środowisku należy opracować rozwiązanie, które jest zgodne ze standardami kodowania i zasadami zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="bf46f-151">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-appuser-authentication"></a><span data-ttu-id="bf46f-152">.NET (aplikacja + uwierzytelnianie użytkownika)</span><span class="sxs-lookup"><span data-stu-id="bf46f-152">.NET (app+user authentication)</span></span>

<span data-ttu-id="bf46f-153">Przykładowy projekt [zgody partnera](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) pokazuje, jak używać witryny sieci Web opracowanej przy użyciu ASP.NET do przechwytywania zgody, żądania tokenu odświeżania i bezpiecznego przechowywania w Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="bf46f-153">The [partner consent](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using ASP.NET to capture consent, request a refresh token, and securely store it in Azure Key Vault.</span></span> <span data-ttu-id="bf46f-154">Wykonaj następujące kroki, aby utworzyć wymagane wymagania wstępne dla tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="bf46f-154">Perform the following steps to create the required prerequisites for this sample.</span></span>

1. <span data-ttu-id="bf46f-155">Utwórz wystąpienie Azure Key Vault przy użyciu Azure Portal lub następujących poleceń programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bf46f-155">Create an instance of Azure Key Vault using the Azure portal or the following PowerShell commands.</span></span> <span data-ttu-id="bf46f-156">Przed wykonaniem polecenia należy koniecznie zmodyfikować wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="bf46f-156">Before executing the command, be sure to modify the parameter values accordingly.</span></span> <span data-ttu-id="bf46f-157">Nazwa magazynu musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="bf46f-157">The vault name must be unique.</span></span>

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    <span data-ttu-id="bf46f-158">Aby uzyskać więcej informacji na temat tworzenia Azure Key Vault, zobacz [Szybki Start: Ustawianie i pobieranie klucza tajnego z Azure Key Vault przy użyciu Azure Portal](/azure/key-vault/quick-create-portal) lub [szybkiego startu: Ustaw i Pobierz klucz tajny z Azure Key Vault przy użyciu programu PowerShell](/azure/key-vault/quick-create-powershell).</span><span class="sxs-lookup"><span data-stu-id="bf46f-158">For more information about creating an Azure Key Vault, see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](/azure/key-vault/quick-create-powershell).</span></span> <span data-ttu-id="bf46f-159">Następnie ustaw i Pobierz wpis tajny.</span><span class="sxs-lookup"><span data-stu-id="bf46f-159">Then set and retrieve a secret.</span></span>

2. <span data-ttu-id="bf46f-160">Utwórz aplikację usługi Azure AD i klucz przy użyciu Azure Portal lub następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="bf46f-160">Create an Azure AD Application and a key using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    <span data-ttu-id="bf46f-161">Pamiętaj, aby zanotować identyfikator aplikacji i wartości klucza tajnego, ponieważ zostaną one użyte w poniższych krokach.</span><span class="sxs-lookup"><span data-stu-id="bf46f-161">Be sure to make note of the application identifier and secret values because they'll be used in the steps below.</span></span>

3. <span data-ttu-id="bf46f-162">Przyznaj nowo utworzone aplikacje usługi Azure AD za pomocą Azure Portal lub następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="bf46f-162">Grant the newly create Azure AD application the read secrets permissions using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. <span data-ttu-id="bf46f-163">Utwórz aplikację usługi Azure AD, która jest skonfigurowana dla Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="bf46f-163">Create an Azure AD application that is configured for Partner Center.</span></span> <span data-ttu-id="bf46f-164">Wykonaj poniższe czynności, aby wykonać ten krok.</span><span class="sxs-lookup"><span data-stu-id="bf46f-164">Perform the following actions to complete this step.</span></span>

    - <span data-ttu-id="bf46f-165">Przejdź do funkcji [zarządzania aplikacjami](https://partner.microsoft.com/pcv/apiintegration/appmanagement) na pulpicie nawigacyjnym Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="bf46f-165">Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard</span></span>
    - <span data-ttu-id="bf46f-166">Kliknij pozycję *Dodaj nową aplikację sieci Web* , aby utworzyć nową aplikację usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf46f-166">Click *Add new web app* to create a new Azure AD application.</span></span>

    <span data-ttu-id="bf46f-167">Upewnij się, że zostały udokumentowane *identyfikatory aplikacji*, \* identyfikator konta \* \* i wartości *klucza* , ponieważ zostaną one użyte w poniższych krokach.</span><span class="sxs-lookup"><span data-stu-id="bf46f-167">Be sure to document the *App ID*, \*Account ID\*\*, and *Key* values because they'll be used in the steps below.</span></span>

5. <span data-ttu-id="bf46f-168">Sklonuj repozytorium [partnerskie — przykłady](https://github.com/Microsoft/Partner-Center-DotNet-Samples) dla tego programu przy użyciu programu Visual Studio lub poniższego polecenia.</span><span class="sxs-lookup"><span data-stu-id="bf46f-168">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command.</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. <span data-ttu-id="bf46f-169">Otwórz projekt *PartnerConsent* znaleziony w `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogu.</span><span class="sxs-lookup"><span data-stu-id="bf46f-169">Open the *PartnerConsent* project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

7. <span data-ttu-id="bf46f-170">Wypełnij ustawienia aplikacji Znalezione w [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)</span><span class="sxs-lookup"><span data-stu-id="bf46f-170">Populate the application settings found in the [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)</span></span>

    ```xml
    <!-- AppID that represents CSP application -->
    <add key="ida:CSPApplicationId" value="" />
    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CSPApplicationSecret" value="" />

    <!--
        Endpoint address for the instance of Azure KeyVault. This is
        the DNS Name for the instance of Key Vault that you provisioned.
     -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- App ID that is given access for KeyVault to store refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate
        to your environment. The following application secret is for sample
        application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="bf46f-171">Informacje poufne, takie jak wpisy tajne aplikacji, nie powinny być przechowywane w plikach konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bf46f-171">Sensitive information such as application secrets should not be stored in configuration files.</span></span> <span data-ttu-id="bf46f-172">Zostało to zrobione w tym miejscu, ponieważ jest to przykładowa aplikacja.</span><span class="sxs-lookup"><span data-stu-id="bf46f-172">It was done here because this is a sample application.</span></span> <span data-ttu-id="bf46f-173">W przypadku aplikacji produkcyjnej zdecydowanie zalecamy użycie uwierzytelniania opartego na certyfikatach.</span><span class="sxs-lookup"><span data-stu-id="bf46f-173">With your production application we strongly recommend that you use certificate-based authentication.</span></span> <span data-ttu-id="bf46f-174">Aby uzyskać więcej informacji, zobacz [poświadczenia certyfikatu na potrzeby uwierzytelniania aplikacji]( /azure/active-directory/develop/active-directory-certificate-credentials).</span><span class="sxs-lookup"><span data-stu-id="bf46f-174">For more information, see [Certificate credentials for application authentication]( /azure/active-directory/develop/active-directory-certificate-credentials).</span></span>

8. <span data-ttu-id="bf46f-175">Po uruchomieniu tego przykładowego projektu zostanie wyświetlony monit o uwierzytelnienie.</span><span class="sxs-lookup"><span data-stu-id="bf46f-175">When you run this sample project, it will prompt you for authentication.</span></span> <span data-ttu-id="bf46f-176">Po pomyślnym uwierzytelnieniu token dostępu jest zaproszony z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf46f-176">After successfully authenticating, an access token is requested from Azure AD.</span></span> <span data-ttu-id="bf46f-177">Informacje zwracane z usługi Azure AD obejmują token odświeżania, który jest przechowywany w skonfigurowanym wystąpieniu Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="bf46f-177">The information returned from Azure AD includes a refresh token that is stored in the configured instance of Azure Key Vault.</span></span>

## <a name="java-appuser-authentication"></a><span data-ttu-id="bf46f-178">Java (uwierzytelnianie aplikacji i użytkowników)</span><span class="sxs-lookup"><span data-stu-id="bf46f-178">Java (app+user authentication)</span></span>

<span data-ttu-id="bf46f-179">Przykładowy projekt [zgody partnera](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) pokazuje, jak używać witryny sieci Web opracowanej przy użyciu JSP do przechwytywania zgody, żądania tokenu odświeżania i bezpiecznego magazynu w Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="bf46f-179">The [partner consent](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using JSP to capture consent, request a refresh token, and secure store in Azure Key Vault.</span></span> <span data-ttu-id="bf46f-180">Wykonaj poniższe czynności, aby utworzyć wymagane wymagania wstępne dla tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="bf46f-180">Perform the following to create the required prerequisites for this sample.</span></span>

1. <span data-ttu-id="bf46f-181">Utwórz wystąpienie Azure Key Vault przy użyciu Azure Portal lub następujących poleceń programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bf46f-181">Create an instance of Azure Key Vault using the Azure portal or the following PowerShell commands.</span></span> <span data-ttu-id="bf46f-182">Przed wykonaniem polecenia należy koniecznie zmodyfikować wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="bf46f-182">Before executing the command, be sure to modify the parameter values accordingly.</span></span> <span data-ttu-id="bf46f-183">Nazwa magazynu musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="bf46f-183">The vault name must be unique.</span></span>

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    <span data-ttu-id="bf46f-184">Aby uzyskać więcej informacji na temat tworzenia Azure Key Vault, zobacz [Szybki Start: Ustawianie i pobieranie klucza tajnego z Azure Key Vault przy użyciu Azure Portal](/azure/key-vault/quick-create-portal) lub [szybkiego startu: Ustaw i Pobierz klucz tajny z Azure Key Vault przy użyciu programu PowerShell](/azure/key-vault/quick-create-powershell).</span><span class="sxs-lookup"><span data-stu-id="bf46f-184">For more information about creating an Azure Key Vault, see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](/azure/key-vault/quick-create-powershell).</span></span>

2. <span data-ttu-id="bf46f-185">Utwórz aplikację usługi Azure AD i klucz przy użyciu Azure Portal lub następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="bf46f-185">Create an Azure AD Application and a key using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    <span data-ttu-id="bf46f-186">Upewnij się, że zostały udokumentowane identyfikatory aplikacji i wartości tajne, ponieważ zostaną one użyte w poniższych krokach.</span><span class="sxs-lookup"><span data-stu-id="bf46f-186">Be sure to document the application identifier and secret values because they'll be used in the steps below.</span></span>

3. <span data-ttu-id="bf46f-187">Przyznaj nowo utworzoną aplikację usługi Azure AD uprawnienia Odczyt wpisów tajnych przy użyciu Azure Portal lub następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="bf46f-187">Grant the newly created Azure AD application the read secrets permissions using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. <span data-ttu-id="bf46f-188">Utwórz aplikację usługi Azure AD, która jest skonfigurowana dla Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="bf46f-188">Create an Azure AD application that is configured for Partner Center.</span></span> <span data-ttu-id="bf46f-189">Aby ukończyć ten krok, wykonaj następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="bf46f-189">Perform the following to complete this step.</span></span>

    - <span data-ttu-id="bf46f-190">Przejdź do funkcji [zarządzania aplikacjami](https://partner.microsoft.com/pcv/apiintegration/appmanagement) na pulpicie nawigacyjnym Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="bf46f-190">Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard</span></span>
    - <span data-ttu-id="bf46f-191">Kliknij pozycję *Dodaj nową aplikację sieci Web* , aby utworzyć nową aplikację usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf46f-191">Click *Add new web app* to create a new Azure AD application.</span></span>

    <span data-ttu-id="bf46f-192">Upewnij się, że zostały udokumentowane *identyfikatory aplikacji*, \* identyfikator konta \* \* i wartości *klucza* , ponieważ zostaną one użyte w poniższych krokach.</span><span class="sxs-lookup"><span data-stu-id="bf46f-192">Be sure to document the *App ID*, \*Account ID\*\*, and *Key* values because they'll be used in the steps below.</span></span>

5. <span data-ttu-id="bf46f-193">Sklonuj repozytorium [partnerskie-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) przy użyciu następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="bf46f-193">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. <span data-ttu-id="bf46f-194">Otwórz projekt *PartnerConsent* znaleziony w `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogu.</span><span class="sxs-lookup"><span data-stu-id="bf46f-194">Open the *PartnerConsent* project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

7. <span data-ttu-id="bf46f-195">Wypełnij ustawienia aplikacji Znalezione w pliku [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml)</span><span class="sxs-lookup"><span data-stu-id="bf46f-195">Populate the application settings found in the [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) file</span></span>

    ```xml
    <filter>
        <filter-name>AuthenticationFilter</filter-name>
        <filter-class>com.microsoft.store.samples.partnerconsent.security.AuthenticationFilter</filter-class>
        <init-param>
            <param-name>client_id</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>client_secret</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_base_url</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_client_id</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_client_secret</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_certifcate_path</param-name>
            <param-value></param-value>
        </init-param>
    </filter>
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="bf46f-196">Informacje poufne, takie jak wpisy tajne aplikacji, nie powinny być przechowywane w plikach konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bf46f-196">Sensitive information such as application secrets should not be stored in configurations files.</span></span> <span data-ttu-id="bf46f-197">Zostało to zrobione w tym miejscu, ponieważ jest to przykładowa aplikacja.</span><span class="sxs-lookup"><span data-stu-id="bf46f-197">It was done here because this is a sample application.</span></span> <span data-ttu-id="bf46f-198">Zdecydowanie zalecamy używanie uwierzytelniania opartego na certyfikatach w aplikacji produkcyjnej.</span><span class="sxs-lookup"><span data-stu-id="bf46f-198">With your production application, we strongly recommend that you use certificate based authenticate.</span></span> <span data-ttu-id="bf46f-199">Aby uzyskać więcej informacji, zobacz [Key Vault uwierzytelnianie certyfikatu](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).</span><span class="sxs-lookup"><span data-stu-id="bf46f-199">For more information, see [Key Vault Certificate authentication](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).</span></span>

8. <span data-ttu-id="bf46f-200">Po uruchomieniu tego przykładowego projektu zostanie wyświetlony monit o uwierzytelnienie.</span><span class="sxs-lookup"><span data-stu-id="bf46f-200">When you run this sample project, it will prompt you for authentication.</span></span> <span data-ttu-id="bf46f-201">Po pomyślnym uwierzytelnieniu token dostępu jest zaproszony z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf46f-201">After successfully authenticating, an access token is requested from Azure AD.</span></span> <span data-ttu-id="bf46f-202">Informacje zwracane z usługi Azure AD obejmują token odświeżania, który jest przechowywany w skonfigurowanym wystąpieniu Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="bf46f-202">The information returned from Azure AD includes a refresh token that is stored in the configured instance of Azure Key Vault.</span></span>

## <a name="cloud-solution-provider-authentication"></a><span data-ttu-id="bf46f-203">Uwierzytelnianie dostawcy rozwiązań w chmurze</span><span class="sxs-lookup"><span data-stu-id="bf46f-203">Cloud Solution Provider authentication</span></span>

<span data-ttu-id="bf46f-204">Partnerzy dostawcy rozwiązań w chmurze mogą używać tokenu odświeżania uzyskanego w ramach procesu [zgody partnera](#partner-consent) .</span><span class="sxs-lookup"><span data-stu-id="bf46f-204">Cloud Solution Provider partners can use the refresh token obtained through the [partner consent](#partner-consent) process.</span></span>

### <a name="samples-for-cloud-solution-provider-authentication"></a><span data-ttu-id="bf46f-205">Przykłady uwierzytelniania dostawcy rozwiązań w chmurze</span><span class="sxs-lookup"><span data-stu-id="bf46f-205">Samples for Cloud Solution Provider authentication</span></span>

<span data-ttu-id="bf46f-206">Aby pomóc partnerom zrozumieć, jak wykonać każdą wymaganą operację, opracowano następujące przykłady.</span><span class="sxs-lookup"><span data-stu-id="bf46f-206">To help partners understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="bf46f-207">W przypadku zaimplementowania odpowiedniego rozwiązania w środowisku należy opracować rozwiązanie, które jest zgodne ze standardami kodowania i zasadami zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="bf46f-207">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-csp-authentication"></a><span data-ttu-id="bf46f-208">.NET (uwierzytelnianie CSP)</span><span class="sxs-lookup"><span data-stu-id="bf46f-208">.NET (CSP authentication)</span></span>

1. <span data-ttu-id="bf46f-209">Jeśli jeszcze tego nie zrobiono, wykonaj [proces zgody partnera](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="bf46f-209">If you have not already done so, perform the [partner consent process](#partner-consent).</span></span>

2. <span data-ttu-id="bf46f-210">Klonowanie repozytorium z [przykładem partnera](https://github.com/Microsoft/Partner-Center-DotNet-Samples) z użyciem programu Visual Studio lub następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="bf46f-210">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. <span data-ttu-id="bf46f-211">Otwórz `CSPApplication` projekt znaleziony w `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogu.</span><span class="sxs-lookup"><span data-stu-id="bf46f-211">Open the `CSPApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="bf46f-212">Aktualizacja ustawień aplikacji znalezionych w pliku [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) .</span><span class="sxs-lookup"><span data-stu-id="bf46f-212">Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) file.</span></span>

    ```xml
    <!-- AppID that represents CSP application -->
    <add key="ida:CSPApplicationId" value="" />
    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CSPApplicationSecret" value="" />

    <!-- Endpoint address for the instance of Azure KeyVault -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- AppID that is given access for keyvault to store the refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

5. <span data-ttu-id="bf46f-213">Ustaw odpowiednie wartości zmiennych **PartnerId** i **CustomerID** znalezionych w pliku [program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) .</span><span class="sxs-lookup"><span data-stu-id="bf46f-213">Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) file.</span></span>

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. <span data-ttu-id="bf46f-214">Po uruchomieniu tego przykładowego projektu uzyskuje token odświeżania uzyskany podczas procesu wyrażania zgody partnera.</span><span class="sxs-lookup"><span data-stu-id="bf46f-214">When you run this sample project, it obtains the refresh token obtained during the partner consent process.</span></span> <span data-ttu-id="bf46f-215">Następnie żąda tokenu dostępu do współdziałania z zestawem SDK Centrum partnerskiego w imieniu partnera.</span><span class="sxs-lookup"><span data-stu-id="bf46f-215">Then, it requests an access token to interact with the Partner Center SDK on the partner's behalf.</span></span> <span data-ttu-id="bf46f-216">Na koniec żąda tokenu dostępu do współpracy z Microsoft Graph w imieniu określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="bf46f-216">Finally, it requests an access token to interact with Microsoft Graph on behalf of the specified customer.</span></span>

## <a name="java-csp-authentication"></a><span data-ttu-id="bf46f-217">Java (uwierzytelnianie CSP)</span><span class="sxs-lookup"><span data-stu-id="bf46f-217">Java (CSP authentication)</span></span>

1. <span data-ttu-id="bf46f-218">Jeśli jeszcze tego nie zrobiono, wykonaj [proces zgody partnera](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="bf46f-218">If you have not done so already, perform the [partner consent process](#partner-consent).</span></span>

2. <span data-ttu-id="bf46f-219">Sklonuj repozytorium [partner-Sample-Java-przykłady](https://github.com/Microsoft/Partner-Center-Java-Samples) przy użyciu programu Visual Studio lub następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="bf46f-219">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. <span data-ttu-id="bf46f-220">Otwórz `cspsample` projekt znaleziony w `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogu.</span><span class="sxs-lookup"><span data-stu-id="bf46f-220">Open the `cspsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="bf46f-221">Zaktualizuj ustawienia aplikacji Znalezione w pliku [Application. Properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) .</span><span class="sxs-lookup"><span data-stu-id="bf46f-221">Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) file.</span></span>

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. <span data-ttu-id="bf46f-222">Po uruchomieniu tego przykładowego projektu uzyskuje token odświeżania uzyskany podczas procesu wyrażania zgody partnera.</span><span class="sxs-lookup"><span data-stu-id="bf46f-222">When you run this sample project, it obtains the refresh token obtained during the partner consent process.</span></span> <span data-ttu-id="bf46f-223">Następnie żąda tokenu dostępu do współdziałania z zestawem SDK Centrum partnerskiego w imieniu partnera.</span><span class="sxs-lookup"><span data-stu-id="bf46f-223">Then, it requests an access token to interact with the Partner Center SDK on the partner's behalf.</span></span>

6. <span data-ttu-id="bf46f-224">Opcjonalne — Usuń komentarz z wywołań funkcji *RunAzureTask* i *RunGraphTask* , jeśli chcesz zobaczyć, jak korzystać z Azure Resource Manager i Microsoft Graph w imieniu klienta.</span><span class="sxs-lookup"><span data-stu-id="bf46f-224">Optional - uncomment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with Azure Resource Manager and Microsoft Graph on behalf of the customer.</span></span>

## <a name="control-panel-provider-authentication"></a><span data-ttu-id="bf46f-225">Uwierzytelnianie dostawcy panelu sterowania</span><span class="sxs-lookup"><span data-stu-id="bf46f-225">Control Panel Provider authentication</span></span>

<span data-ttu-id="bf46f-226">Dostawcy panelu sterowania muszą mieć wszystkich partnerów, którzy obsługują proces [wyrażania zgody partnera](#partner-consent) .</span><span class="sxs-lookup"><span data-stu-id="bf46f-226">Control panel vendors need to have each partner they support perform the [partner consent](#partner-consent) process.</span></span> <span data-ttu-id="bf46f-227">Po ukończeniu token odświeżania uzyskany za pomocą tego procesu jest używany w celu uzyskania dostępu do interfejsu API REST Centrum partnerskiego i interfejsu API platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="bf46f-227">Once that is completed the refresh token obtained through that process is used to access the Partner Center REST API and .NET API.</span></span>

### <a name="samples-for-cloud-panel-provider-authentication"></a><span data-ttu-id="bf46f-228">Przykłady uwierzytelniania dostawcy w panelu Cloud</span><span class="sxs-lookup"><span data-stu-id="bf46f-228">Samples for Cloud Panel Provider authentication</span></span>

<span data-ttu-id="bf46f-229">Aby ułatwić dostawcom panelu sterowania zrozumienie, jak wykonać każdą wymaganą operację, opracowano następujące przykłady.</span><span class="sxs-lookup"><span data-stu-id="bf46f-229">To help control panel vendors understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="bf46f-230">W przypadku zaimplementowania odpowiedniego rozwiązania w środowisku należy opracować rozwiązanie, które jest zgodne ze standardami kodowania i zasadami zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="bf46f-230">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-cpv-authentication"></a><span data-ttu-id="bf46f-231">.NET (uwierzytelnianie CPV)</span><span class="sxs-lookup"><span data-stu-id="bf46f-231">.NET (CPV authentication)</span></span>

1. <span data-ttu-id="bf46f-232">Utwórz i Wdróż proces dla partnerów dostawcy rozwiązań w chmurze, aby zapewnić odpowiednią zgodę.</span><span class="sxs-lookup"><span data-stu-id="bf46f-232">Develop and deploy a process for Cloud Solution Provider partners to provide the appropriate consent.</span></span> <span data-ttu-id="bf46f-233">Aby uzyskać więcej informacji, zobacz temat [zgody partnera](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="bf46f-233">For more information an example, see [partner consent](#partner-consent).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="bf46f-234">Nie należy przechowywać poświadczeń użytkownika od partnera dostawcy rozwiązań w chmurze.</span><span class="sxs-lookup"><span data-stu-id="bf46f-234">User credentials from a Cloud Solution Provider partner should not be stored.</span></span> <span data-ttu-id="bf46f-235">Token odświeżania uzyskany przez proces wyrażania zgody partnera powinien być przechowywany i używany do żądania tokenów dostępu w celu współpracy z dowolnym interfejsem API firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bf46f-235">The refresh token obtained through the partner consent process should be stored and used to request access tokens for interacting with any Microsoft API.</span></span>

2. <span data-ttu-id="bf46f-236">Klonowanie repozytorium z [przykładem partnera](https://github.com/Microsoft/Partner-Center-DotNet-Samples) z użyciem programu Visual Studio lub następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="bf46f-236">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. <span data-ttu-id="bf46f-237">Otwórz `CPVApplication` projekt znaleziony w `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogu.</span><span class="sxs-lookup"><span data-stu-id="bf46f-237">Open the `CPVApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="bf46f-238">Aktualizacja ustawień aplikacji znalezionych w pliku [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) .</span><span class="sxs-lookup"><span data-stu-id="bf46f-238">Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) file.</span></span>

    ```xml
    <!-- AppID that represents Control panel vendor application -->
    <add key="ida:CPVApplicationId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CPVApplicationSecret" value="" />

    <!-- Endpoint address for the instance of Azure KeyVault -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- AppID that is given access for keyvault to store the refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

5. <span data-ttu-id="bf46f-239">Ustaw odpowiednie wartości zmiennych **PartnerId** i **CustomerID** znalezionych w pliku [program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) .</span><span class="sxs-lookup"><span data-stu-id="bf46f-239">Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) file.</span></span>

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. <span data-ttu-id="bf46f-240">Po uruchomieniu tego przykładowego projektu zostanie uzyskany token odświeżania dla określonego partnera.</span><span class="sxs-lookup"><span data-stu-id="bf46f-240">When you run this sample project, it obtains the refresh token for the specified partner.</span></span> <span data-ttu-id="bf46f-241">Następnie żąda tokenu dostępu, aby uzyskać dostęp do Centrum partnerskiego i grafu usługi Azure AD w imieniu partnera.</span><span class="sxs-lookup"><span data-stu-id="bf46f-241">Then, it requests an access token to access Partner Center and Azure AD Graph on behalf of the partner.</span></span> <span data-ttu-id="bf46f-242">Następne zadanie, które wykonuje, to usunięcie i utworzenie dotacji do dzierżawy klienta.</span><span class="sxs-lookup"><span data-stu-id="bf46f-242">The next task it performs is the deletion and creation of permission grants into the customer tenant.</span></span> <span data-ttu-id="bf46f-243">Ponieważ nie istnieje żadna relacja między dostawcą panelu sterowania a klientem, te uprawnienia należy dodać przy użyciu interfejsu API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="bf46f-243">Since there's no relationship between the control panel vendor and the customer, these permissions need to be added using the Partner Center API.</span></span> <span data-ttu-id="bf46f-244">Poniższy przykład pokazuje, jak to zrobić.</span><span class="sxs-lookup"><span data-stu-id="bf46f-244">The following example shows how to accomplish that.</span></span>

    ```csharp
    JObject contents = new JObject
    {
        // Provide your application display name
        ["displayName"] = "CPV Marketplace",

        // Provide your application id
        ["applicationId"] = CPVApplicationId,

        // Provide your application grants
        ["applicationGrants"] = new JArray(
            JObject.Parse("{\"enterpriseApplicationId\": \"00000002-0000-0000-c000-000000000000\", \"scope\":\"Domain.ReadWrite.All,User.ReadWrite.All,Directory.Read.All\"}"), // for Azure AD Graph access,  Directory.Read.All
            JObject.Parse("{\"enterpriseApplicationId\": \"797f4846-ba00-4fd7-ba43-dac1f8f63013\", \"scope\":\"user_impersonation\"}")) // for Azure Resource Manager access
    };

    /**
     * The following steps have to be performed once per customer tenant if your application is
     * a control panel vendor application and requires customer tenant Azure AD Graph access.
     **/

    // delete the previous grant into customer tenant
    JObject consentDeletion = await ApiCalls.DeleteAsync(
        tokenPartnerResult.Item1,
        string.Format("https://api.partnercenter.microsoft.com/v1/customers/{0}/applicationconsents/{1}", CustomerId, CPVApplicationId));

    // create new grants for the application given the setting in application grants payload.
    JObject consentCreation = await ApiCalls.PostAsync(
        tokenPartnerResult.Item1,
        string.Format("https://api.partnercenter.microsoft.com/v1/customers/{0}/applicationconsents", CustomerId),
        contents.ToString());
    ```

<span data-ttu-id="bf46f-245">Po nawiązaniu tych uprawnień przykład wykonuje operacje przy użyciu programu Azure AD Graph w imieniu klienta.</span><span class="sxs-lookup"><span data-stu-id="bf46f-245">After these permissions have been established, the sample performs operations using Azure AD Graph on behalf of the customer.</span></span>

## <a name="java-cpv-authentication"></a><span data-ttu-id="bf46f-246">Java (uwierzytelnianie CPV)</span><span class="sxs-lookup"><span data-stu-id="bf46f-246">Java (CPV authentication)</span></span>

1. <span data-ttu-id="bf46f-247">Utwórz i Wdróż proces dla partnerów dostawcy rozwiązań w chmurze, aby zapewnić odpowiednią zgodę.</span><span class="sxs-lookup"><span data-stu-id="bf46f-247">Develop and deploy a process for Cloud Solution Provider partners to provide the appropriate consent.</span></span> <span data-ttu-id="bf46f-248">Aby uzyskać więcej informacji i zapoznać się z przykładem, zapoznaj się z tematem [zgody partnera](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="bf46f-248">For more information and an example, see the [partner consent](#partner-consent).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="bf46f-249">Nie należy przechowywać poświadczeń użytkownika od partnera dostawcy rozwiązań w chmurze.</span><span class="sxs-lookup"><span data-stu-id="bf46f-249">User credentials from a Cloud Solution Provider partner should not be stored.</span></span> <span data-ttu-id="bf46f-250">Token odświeżania uzyskany przez proces wyrażania zgody partnera powinien być przechowywany i używany do żądania tokenów dostępu w celu współpracy z dowolnym interfejsem API firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bf46f-250">The refresh token obtained through the partner consent process should be stored and used to request access tokens for interacting with any Microsoft API.</span></span>

2. <span data-ttu-id="bf46f-251">Sklonuj repozytorium [partnerskie-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) przy użyciu następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="bf46f-251">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. <span data-ttu-id="bf46f-252">Otwórz `cpvsample` projekt znaleziony w `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogu.</span><span class="sxs-lookup"><span data-stu-id="bf46f-252">Open the `cpvsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="bf46f-253">Zaktualizuj ustawienia aplikacji Znalezione w pliku [Application. Properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) .</span><span class="sxs-lookup"><span data-stu-id="bf46f-253">Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) file.</span></span>

    ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    partnercenter.displayName=
    ```

    <span data-ttu-id="bf46f-254">Wartość `partnercenter.displayName` powinna być nazwą wyświetlaną aplikacji Marketplace.</span><span class="sxs-lookup"><span data-stu-id="bf46f-254">The value for the `partnercenter.displayName` should be the display name of your marketplace application.</span></span>

5. <span data-ttu-id="bf46f-255">Ustaw odpowiednie wartości zmiennych **partnerId** i **customerId** znalezionych w pliku [program. Java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) .</span><span class="sxs-lookup"><span data-stu-id="bf46f-255">Set the appropriate values for the **partnerId** and **customerId** variables found in the [Program.java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) file.</span></span>

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. <span data-ttu-id="bf46f-256">Po uruchomieniu tego przykładowego projektu zostanie uzyskany token odświeżania dla określonego partnera.</span><span class="sxs-lookup"><span data-stu-id="bf46f-256">When you run this sample project, it obtains the refresh token for the specified partner.</span></span> <span data-ttu-id="bf46f-257">Następnie żąda tokenu dostępu, aby uzyskać dostęp do Centrum partnerskiego w imieniu partnera.</span><span class="sxs-lookup"><span data-stu-id="bf46f-257">Then, it requests an access token to access Partner Center on behalf of the partner.</span></span> <span data-ttu-id="bf46f-258">Następne zadanie, które wykonuje, to usunięcie i utworzenie dotacji do dzierżawy klienta.</span><span class="sxs-lookup"><span data-stu-id="bf46f-258">The next task it performs is the deletion and creation of permission grants into the customer tenant.</span></span> <span data-ttu-id="bf46f-259">Ponieważ nie istnieje żadna relacja między dostawcą panelu sterowania a klientem, te uprawnienia należy dodać przy użyciu interfejsu API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="bf46f-259">Since there's no relationship between the control panel vendor and the customer, these permissions need to be added using the Partner Center API.</span></span> <span data-ttu-id="bf46f-260">Poniższy przykład pokazuje, jak przyznać uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="bf46f-260">The following example shows how to grant the permissions.</span></span>

    ```java
    ApplicationGrant azureAppGrant = new ApplicationGrant();

    azureAppGrant.setEnterpriseApplication("797f4846-ba00-4fd7-ba43-dac1f8f63013");
    azureAppGrant.setScope("user_impersonation");

    ApplicationGrant graphAppGrant = new ApplicationGrant();

    graphAppGrant.setEnterpriseApplication("00000002-0000-0000-c000-000000000000");
    graphAppGrant.setScope("Domain.ReadWrite.All,User.ReadWrite.All,Directory.Read.All");

    ApplicationConsent consent = new ApplicationConsent();

    consent.setApplicationGrants(Arrays.asList(azureAppGrant, graphAppGrant));
    consent.setApplicationId(properties.getProperty(PropertyName.PARTNER_CENTER_CLIENT_ID));
    consent.setDisplayName(properties.getProperty(PropertyName.PARTNER_CENTER_DISPLAY_NAME));

    // Deletes the existing grant into the customer it is present.
    partnerOperations.getServiceClient().delete(
        partnerOperations,
        new TypeReference<ApplicationConsent>(){},
        MessageFormat.format(
            "customers/{0}/applicationconsents/{1}",
            customerId,
            properties.getProperty(PropertyName.PARTNER_CENTER_CLIENT_ID)));

    // Consent to the defined applications and the respective scopes.
    partnerOperations.getServiceClient().post(
        partnerOperations,
        new TypeReference<ApplicationConsent>(){},
        MessageFormat.format(
            "customers/{0}/applicationconsents",
            customerId),
        consent);
    ```

<span data-ttu-id="bf46f-261">Usuń komentarz z wywołań funkcji *RunAzureTask* i *RunGraphTask* , jeśli chcesz zobaczyć, jak korzystać z Azure Resource Manager i Microsoft Graph w imieniu klienta.</span><span class="sxs-lookup"><span data-stu-id="bf46f-261">Uncomment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with Azure Resource Manager and Microsoft Graph on behalf of the customer.</span></span>
