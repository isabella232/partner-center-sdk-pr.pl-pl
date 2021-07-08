---
title: Uwierzytelnianie w Centrum partnerskim
description: Partner Center używa usługi Azure AD do uwierzytelniania, a aby korzystać z interfejsów API Partner Center, należy poprawnie skonfigurować ustawienia uwierzytelniania.
ms.date: 11/13/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.openlocfilehash: e54feba7ea727bb7f7eff8de76dcdf28c8a453ee
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548077"
---
# <a name="partner-center-authentication"></a><span data-ttu-id="b0cc6-103">Uwierzytelnianie w Centrum partnerskim</span><span class="sxs-lookup"><span data-stu-id="b0cc6-103">Partner Center authentication</span></span>

<span data-ttu-id="b0cc6-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b0cc6-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b0cc6-105">Centrum partnerskie w celu uwierzytelniania używa usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-105">Partner Center uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="b0cc6-106">Korzystając z interfejsu API Centrum partnerskiego, zestawu SDK lub modułu programu PowerShell, należy prawidłowo skonfigurować aplikację usługi Azure AD, a następnie zażądać tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-106">When interacting with the Partner Center API, SDK, or PowerShell module you must correctly configure an Azure AD application and then request an access token.</span></span> <span data-ttu-id="b0cc6-107">Tokeny dostępu uzyskane tylko przy użyciu aplikacji lub uwierzytelniania aplikacji i użytkownika mogą być używane z Partner Center.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-107">Access tokens obtained using app only or app + user authentication can be used with the Partner Center.</span></span> <span data-ttu-id="b0cc6-108">Istnieją jednak dwa ważne elementy, które należy rozważyć</span><span class="sxs-lookup"><span data-stu-id="b0cc6-108">However, there are two important items that need to be considered</span></span>

- <span data-ttu-id="b0cc6-109">Użyj uwierzytelniania wieloskładnikowego podczas uzyskiwania dostępu do interfejsu API Partner Center przy użyciu uwierzytelniania aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-109">Use multi-factor authentication when accessing the Partner Center API using app + user authentication.</span></span> <span data-ttu-id="b0cc6-110">Aby uzyskać więcej informacji na temat tej zmiany, zobacz [Włączanie bezpiecznego modelu aplikacji](enable-secure-app-model.md).</span><span class="sxs-lookup"><span data-stu-id="b0cc6-110">For more information regarding this change, see [Enable secure application model](enable-secure-app-model.md).</span></span>

- <span data-ttu-id="b0cc6-111">Nie wszystkie operacje interfejsu API Partner Center obsługują tylko uwierzytelnianie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-111">Not all of the operations the Partner Center API support app only authentication.</span></span> <span data-ttu-id="b0cc6-112">Istnieją pewne scenariusze, w których konieczne będzie użycie uwierzytelniania aplikacji i użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-112">There are certain scenarios where you'll be required to use app + user authentication.</span></span> <span data-ttu-id="b0cc6-113">W *nagłówku Wymagania* [](scenarios.md)wstępne każdego artykułu znajduje się dokumentacja z pytaniem, czy obsługiwane jest tylko uwierzytelnianie aplikacji, aplikacja i uwierzytelnianie użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-113">Under the *Prerequisites* heading on each [article](scenarios.md), you'll find documentation that states whether app only authentication, app + user authentication, or both are supported.</span></span>

## <a name="initial-setup"></a><span data-ttu-id="b0cc6-114">Konfiguracja początkowa</span><span class="sxs-lookup"><span data-stu-id="b0cc6-114">Initial setup</span></span>

1. <span data-ttu-id="b0cc6-115">Aby rozpocząć, upewnij się, że masz zarówno konto podstawowe, Partner Center, jak i piaskownicę integracji Partner Center konto.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-115">To begin, you need to make sure that you have both a primary Partner Center account, and an integration sandbox Partner Center account.</span></span> <span data-ttu-id="b0cc6-116">Aby uzyskać więcej informacji, zobacz [Konfigurowanie kont Partner Center dostępu do interfejsu API.](set-up-api-access-in-partner-center.md)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-116">For more information, see [Set up Partner Center accounts for API access](set-up-api-access-in-partner-center.md).</span></span> <span data-ttu-id="b0cc6-117">Zanotuj identyfikator rejestracji aplikacji usługi Azure AAD i wpis tajny (klucz tajny klienta jest wymagany do identyfikacji tylko aplikacji) zarówno dla konta podstawowego, jak i konta piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-117">Make note of the Azure AAD App registration ID and Secret (client secret is required for App only identification) for both your primary account and your integration sandbox account.</span></span>

2. <span data-ttu-id="b0cc6-118">Zaloguj się do usługi Azure AD z Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-118">Sign in to Azure AD from the Azure portal.</span></span> <span data-ttu-id="b0cc6-119">W **uprawnieniach** do innych  aplikacji ustaw uprawnienia dla Windows Azure Active Directory na  uprawnienia delegowane **i** wybierz pozycję Uzyskaj dostęp do katalogu jako zalogowany użytkownik, a następnie pozycję Zaloguj się i odczytaj **profil użytkownika.**</span><span class="sxs-lookup"><span data-stu-id="b0cc6-119">In **permissions to other applications**, set permissions for **Windows Azure Active Directory** to **Delegated Permissions**, and select both **Access the directory as the signed-in user** and **Sign in and read user profile**.</span></span>

3. <span data-ttu-id="b0cc6-120">W Azure Portal dodaj **aplikację**.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-120">In the Azure portal, **Add application**.</span></span> <span data-ttu-id="b0cc6-121">Wyszukaj "Microsoft Partner Center", czyli aplikację microsoft Partner Center.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-121">Search for "Microsoft Partner Center", which is the Microsoft Partner Center application.</span></span> <span data-ttu-id="b0cc6-122">Ustaw uprawnienia **delegowane na** dostęp **do Partner Center API.**</span><span class="sxs-lookup"><span data-stu-id="b0cc6-122">Set the **Delegated Permissions** to **Access Partner Center API**.</span></span> <span data-ttu-id="b0cc6-123">Jeśli korzystasz z usługi Partner Center Microsoft Cloud w Niemczech lub Partner Center for Microsoft Cloud for US Government, ten krok jest obowiązkowy.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-123">If you are using Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government, this step is mandatory.</span></span> <span data-ttu-id="b0cc6-124">Jeśli używasz Partner Center globalnego, ten krok jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-124">If you are using Partner Center global instance, this step is optional.</span></span> <span data-ttu-id="b0cc6-125">Partnerzy CSP mogą użyć funkcji zarządzania aplikacją w portalu Partner Center, aby pominąć ten krok dla Partner Center wystąpienia globalnego.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-125">CSP Partners can use the App Management feature in the Partner Center portal to bypass this step for Partner Center global instance.</span></span>

## <a name="app-only-authentication"></a><span data-ttu-id="b0cc6-126">Uwierzytelnianie tylko aplikacji</span><span class="sxs-lookup"><span data-stu-id="b0cc6-126">App-only authentication</span></span>

<span data-ttu-id="b0cc6-127">Jeśli chcesz użyć uwierzytelniania tylko aplikacji w celu uzyskania dostępu do interfejsu API REST platformy Partner Center, interfejsu API .NET, interfejsu API języka Java lub modułu programu PowerShell, możesz to zrobić, korzystając z poniższych instrukcji.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-127">If you would like to use app-only authentication to access the Partner Center REST API, .NET API, Java API, or PowerShell module then you can do so by using the following instructions.</span></span>

## <a name="net-app-only-authentication"></a><span data-ttu-id="b0cc6-128">.NET (uwierzytelnianie tylko aplikacji)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-128">.NET (app-only authentication)</span></span>

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

## <a name="java-app-only-authentication"></a><span data-ttu-id="b0cc6-129">Java (uwierzytelnianie tylko dla aplikacji)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-129">Java (app-only authentication)</span></span>

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

## <a name="rest-app-only-authentication"></a><span data-ttu-id="b0cc6-130">REST (uwierzytelnianie tylko aplikacji)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-130">REST (app-only authentication)</span></span>

### <a name="rest-request"></a><span data-ttu-id="b0cc6-131">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="b0cc6-131">REST request</span></span>

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

### <a name="rest-response"></a><span data-ttu-id="b0cc6-132">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="b0cc6-132">REST response</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

## <a name="app--user-authentication"></a><span data-ttu-id="b0cc6-133">Uwierzytelnianie aplikacji i użytkownika</span><span class="sxs-lookup"><span data-stu-id="b0cc6-133">App + User authentication</span></span>

<span data-ttu-id="b0cc6-134">W przeszłości [](https://tools.ietf.org/html/rfc6749#section-4.3) do żądania tokenu dostępu do użycia z interfejsem API REST usługi Partner Center, interfejsem API .NET, interfejsem API języka Java lub modułem programu PowerShell były używane poświadczenia hasła właściciela zasobu.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-134">Historically, the [resource owner password credentials grant](https://tools.ietf.org/html/rfc6749#section-4.3) has been used to request an access token for use with the Partner Center REST API, .NET API, Java API, or PowerShell module.</span></span> <span data-ttu-id="b0cc6-135">Ta metoda została użyta do żądania tokenu dostępu od Azure Active Directory przy użyciu identyfikatora klienta i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-135">That method was used to request an access token from Azure Active Directory using a client identifier and user credentials.</span></span> <span data-ttu-id="b0cc6-136">Jednak to podejście nie będzie już działać, ponieważ Partner Center uwierzytelniania wieloskładnikowego w przypadku korzystania z uwierzytelniania aplikacji i użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-136">However, this approach will no longer work because Partner Center requires multi-factor authentication, when using app + user authentication.</span></span> <span data-ttu-id="b0cc6-137">Aby spełnić to wymaganie, firma Microsoft wprowadziła bezpieczną, skalowalną platformę do uwierzytelniania partnerów programu Dostawca rozwiązań w chmurze (CSP) i dostawców panelu sterowania (CPV) przy użyciu uwierzytelniania wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-137">To comply with this requirement Microsoft has introduced a secure, scalable framework for authenticating Cloud Solution Provider (CSP) partners and control panel vendors (CPV) using multi-factor authentication.</span></span> <span data-ttu-id="b0cc6-138">Ta framework jest znana jako model aplikacji zabezpieczonych i składa się z procesu wyrażania zgody oraz żądania tokenu dostępu przy użyciu tokenu odświeżania.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-138">This framework is known as the Secure Application Model, and it is composed of a consent process and a request for an access token using a refresh token.</span></span>

### <a name="partner-consent"></a><span data-ttu-id="b0cc6-139">Zgoda partnera</span><span class="sxs-lookup"><span data-stu-id="b0cc6-139">Partner consent</span></span>

<span data-ttu-id="b0cc6-140">Proces wyrażania zgody przez partnera to interaktywny proces, w którym partner uwierzytelnia się przy użyciu uwierzytelniania wieloskładnikowego, wyraża zgodę na aplikację, a token odświeżania jest przechowywany w bezpiecznym repozytorium, takim jak Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-140">The partner consent process is an interactive process where the partner authenticates using multi-factor authentication, consents to the application, and a refresh token is stored in a secure repository such as Azure Key Vault.</span></span> <span data-ttu-id="b0cc6-141">W tym procesie zaleca się użycie dedykowanego konta na potrzeby integracji.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-141">We recommend that a dedicated account for integration purposes be used for this process.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0cc6-142">Dla konta usługi używanego w procesie wyrażania zgody partnera należy włączyć odpowiednie rozwiązanie uwierzytelniania wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-142">The appropriate multi-factor authentication solution should be enabled for the service account used in the partner consent process.</span></span> <span data-ttu-id="b0cc6-143">Jeśli tak nie jest, wynikowy token odświeżania nie będzie zgodny z wymaganiami bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-143">If it isn't then the resulting refresh token will not be compliant with security requirements.</span></span>

### <a name="samples-for-app--user-authentication"></a><span data-ttu-id="b0cc6-144">Przykłady uwierzytelniania aplikacji i użytkowników</span><span class="sxs-lookup"><span data-stu-id="b0cc6-144">Samples for App + User authentication</span></span>

<span data-ttu-id="b0cc6-145">Proces wyrażania zgody przez partnera może być wykonywany na wiele sposobów.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-145">The partner consent process can be performed in a number of ways.</span></span> <span data-ttu-id="b0cc6-146">Aby pomóc partnerom zrozumieć, jak wykonać każdą wymaganą operację, opracowaliśmy następujące przykłady.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-146">To help partners understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="b0cc6-147">Podczas wdrażania odpowiedniego rozwiązania w środowisku ważne jest, aby opracować rozwiązanie, które jest skargą ze standardami kodowania i zasadami zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-147">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-appuser-authentication"></a><span data-ttu-id="b0cc6-148">.NET (uwierzytelnianie aplikacji i użytkowników)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-148">.NET (app+user authentication)</span></span>

<span data-ttu-id="b0cc6-149">Przykładowy [projekt zgody](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) partnera pokazuje, jak korzystać z witryny internetowej opracowanej przy użyciu usługi ASP.NET do przechwytywania zgody, żądania tokenu odświeżania i bezpiecznego przechowywania ich w Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-149">The [partner consent](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using ASP.NET to capture consent, request a refresh token, and securely store it in Azure Key Vault.</span></span> <span data-ttu-id="b0cc6-150">Wykonaj poniższe kroki, aby utworzyć wymagane wymagania wstępne dla tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-150">Perform the following steps to create the required prerequisites for this sample.</span></span>

1. <span data-ttu-id="b0cc6-151">Utwórz wystąpienie klasy Azure Key Vault za pomocą Azure Portal lub następujących poleceń programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-151">Create an instance of Azure Key Vault using the Azure portal or the following PowerShell commands.</span></span> <span data-ttu-id="b0cc6-152">Przed wykonaniem polecenia należy odpowiednio zmodyfikować wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-152">Before executing the command, be sure to modify the parameter values accordingly.</span></span> <span data-ttu-id="b0cc6-153">Nazwa magazynu musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-153">The vault name must be unique.</span></span>

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    <span data-ttu-id="b0cc6-154">Aby uzyskać więcej informacji na temat tworzenia konta usługi Azure Key Vault, zobacz Szybki [start:](/azure/key-vault/quick-create-portal) ustawianie i pobieranie informacji tajnych z usługi Azure Key Vault przy użyciu programu Azure Portal lub Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell (Szybki start: ustawianie i pobieranie informacji tajnych z usługi Azure Key Vault przy użyciu programu [PowerShell).](/azure/key-vault/quick-create-powershell)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-154">For more information about creating an Azure Key Vault, see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](/azure/key-vault/quick-create-powershell).</span></span> <span data-ttu-id="b0cc6-155">Następnie ustaw i pobierz klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-155">Then set and retrieve a secret.</span></span>

2. <span data-ttu-id="b0cc6-156">Utwórz aplikację usługi Azure AD i klucz przy użyciu Azure Portal lub poniższych poleceń.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-156">Create an Azure AD Application and a key using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    <span data-ttu-id="b0cc6-157">Pamiętaj, aby zanotować identyfikator aplikacji i wartości tajnych, ponieważ będą one używane w poniższych krokach.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-157">Be sure to make note of the application identifier and secret values because they'll be used in the steps below.</span></span>

3. <span data-ttu-id="b0cc6-158">Przyznaj nowo utworzonej aplikacji usługi Azure AD uprawnienia do odczytu wpisów tajnych przy użyciu Azure Portal lub poniższych poleceń.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-158">Grant the newly create Azure AD application the read secrets permissions using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. <span data-ttu-id="b0cc6-159">Utwórz aplikację usługi Azure AD skonfigurowaną dla Partner Center.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-159">Create an Azure AD application that is configured for Partner Center.</span></span> <span data-ttu-id="b0cc6-160">Aby wykonać ten krok, wykonaj następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-160">Perform the following actions to complete this step.</span></span>

    - <span data-ttu-id="b0cc6-161">Przejdź do funkcji [zarządzania aplikacją](https://partner.microsoft.com/pcv/apiintegration/appmanagement) pulpitu nawigacyjnego Partner Center Aplikacji</span><span class="sxs-lookup"><span data-stu-id="b0cc6-161">Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard</span></span>
    - <span data-ttu-id="b0cc6-162">Wybierz *pozycję Dodaj nową aplikację internetową,* aby utworzyć nową aplikację usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-162">Select *Add new web app* to create a new Azure AD application.</span></span>

    <span data-ttu-id="b0cc6-163">Pamiętaj, aby udokumentować wartości *Identyfikator*  aplikacji, *Identyfikator konta*\* i Klucz, ponieważ będą one używane w poniższych krokach.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-163">Be sure to document the *App ID*, \*Account ID\*\*, and *Key* values because they'll be used in the steps below.</span></span>

5. <span data-ttu-id="b0cc6-164">[Sklonuj repozytorium Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) przy użyciu Visual Studio lub następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-164">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command.</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. <span data-ttu-id="b0cc6-165">Otwórz projekt *PartnerConsent* znaleziony w `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogu .</span><span class="sxs-lookup"><span data-stu-id="b0cc6-165">Open the *PartnerConsent* project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

7. <span data-ttu-id="b0cc6-166">Wypełnij ustawienia aplikacji znalezione [](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config) wweb.config</span><span class="sxs-lookup"><span data-stu-id="b0cc6-166">Populate the application settings found in the [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)</span></span>

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
    > <span data-ttu-id="b0cc6-167">Poufne informacje, takie jak wpisy tajne aplikacji, nie powinny być przechowywane w plikach konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-167">Sensitive information such as application secrets should not be stored in configuration files.</span></span> <span data-ttu-id="b0cc6-168">Zostało to zrobione w tym miejscu, ponieważ jest to przykładowa aplikacja.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-168">It was done here because this is a sample application.</span></span> <span data-ttu-id="b0cc6-169">W przypadku aplikacji produkcyjnej zdecydowanie zalecamy użycie uwierzytelniania opartego na certyfikatach.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-169">With your production application we strongly recommend that you use certificate-based authentication.</span></span> <span data-ttu-id="b0cc6-170">Aby uzyskać więcej informacji, zobacz [Poświadczenia certyfikatu do uwierzytelniania aplikacji.]( /azure/active-directory/develop/active-directory-certificate-credentials)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-170">For more information, see [Certificate credentials for application authentication]( /azure/active-directory/develop/active-directory-certificate-credentials).</span></span>

8. <span data-ttu-id="b0cc6-171">Po uruchomieniu tego przykładowego projektu zostanie wyświetlony monit o uwierzytelnienie.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-171">When you run this sample project, it will prompt you for authentication.</span></span> <span data-ttu-id="b0cc6-172">Po pomyślnym uwierzytelnieniu z usługi Azure AD jest żądany token dostępu.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-172">After successfully authenticating, an access token is requested from Azure AD.</span></span> <span data-ttu-id="b0cc6-173">Informacje zwrócone z usługi Azure AD obejmują token odświeżania, który jest przechowywany w skonfigurowanym wystąpieniu Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-173">The information returned from Azure AD includes a refresh token that is stored in the configured instance of Azure Key Vault.</span></span>

## <a name="java-appuser-authentication"></a><span data-ttu-id="b0cc6-174">Java (uwierzytelnianie aplikacji i użytkowników)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-174">Java (app+user authentication)</span></span>

<span data-ttu-id="b0cc6-175">Przykładowy [projekt zgody](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) partnera pokazuje, jak korzystać z witryny internetowej opracowanej przy użyciu programu JSP w celu przechwycenia zgody, zażądania tokenu odświeżania i bezpiecznego magazynu w Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-175">The [partner consent](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using JSP to capture consent, request a refresh token, and secure store in Azure Key Vault.</span></span> <span data-ttu-id="b0cc6-176">Wykonaj następujące czynności, aby utworzyć wymagane wymagania wstępne dla tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-176">Perform the following to create the required prerequisites for this sample.</span></span>

1. <span data-ttu-id="b0cc6-177">Utwórz wystąpienie klasy Azure Key Vault za pomocą Azure Portal lub następujących poleceń programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-177">Create an instance of Azure Key Vault using the Azure portal or the following PowerShell commands.</span></span> <span data-ttu-id="b0cc6-178">Przed wykonaniem polecenia należy odpowiednio zmodyfikować wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-178">Before executing the command, be sure to modify the parameter values accordingly.</span></span> <span data-ttu-id="b0cc6-179">Nazwa magazynu musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-179">The vault name must be unique.</span></span>

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    <span data-ttu-id="b0cc6-180">Aby uzyskać więcej informacji na temat tworzenia konta usługi Azure Key Vault, zobacz Szybki [start:](/azure/key-vault/quick-create-portal) ustawianie i pobieranie informacji tajnych z usługi Azure Key Vault przy użyciu programu Azure Portal lub Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell (Szybki start: ustawianie i pobieranie informacji tajnych z usługi Azure Key Vault przy użyciu programu [PowerShell).](/azure/key-vault/quick-create-powershell)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-180">For more information about creating an Azure Key Vault, see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](/azure/key-vault/quick-create-powershell).</span></span>

2. <span data-ttu-id="b0cc6-181">Utwórz aplikację usługi Azure AD i klucz przy użyciu Azure Portal lub poniższych poleceń.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-181">Create an Azure AD Application and a key using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    <span data-ttu-id="b0cc6-182">Pamiętaj, aby udokumentować identyfikator aplikacji i wartości klucza tajnego, ponieważ będą one używane w poniższych krokach.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-182">Be sure to document the application identifier and secret values because they'll be used in the steps below.</span></span>

3. <span data-ttu-id="b0cc6-183">Przyznaj nowo utworzonej aplikacji usługi Azure AD uprawnienia do odczytu wpisów tajnych przy użyciu Azure Portal lub poniższych poleceń.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-183">Grant the newly created Azure AD application the read secrets permissions using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. <span data-ttu-id="b0cc6-184">Utwórz aplikację usługi Azure AD skonfigurowaną dla Partner Center.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-184">Create an Azure AD application that is configured for Partner Center.</span></span> <span data-ttu-id="b0cc6-185">Wykonaj następujące czynności, aby ukończyć ten krok.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-185">Perform the following to complete this step.</span></span>

    - <span data-ttu-id="b0cc6-186">Przejdź do funkcji [zarządzania aplikacją](https://partner.microsoft.com/pcv/apiintegration/appmanagement) pulpitu nawigacyjnego Partner Center Aplikacji</span><span class="sxs-lookup"><span data-stu-id="b0cc6-186">Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard</span></span>
    - <span data-ttu-id="b0cc6-187">Wybierz *pozycję Dodaj nową aplikację internetową,* aby utworzyć nową aplikację usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-187">Select *Add new web app* to create a new Azure AD application.</span></span>

    <span data-ttu-id="b0cc6-188">Pamiętaj, aby udokumentować wartości *Identyfikator*  aplikacji, *Identyfikator konta*\* i Klucz, ponieważ będą one używane w poniższych krokach.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-188">Be sure to document the *App ID*, \*Account ID\*\*, and *Key* values because they'll be used in the steps below.</span></span>

5. <span data-ttu-id="b0cc6-189">[Sklonuj repozytorium Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) za pomocą następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="b0cc6-189">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. <span data-ttu-id="b0cc6-190">Otwórz projekt *PartnerConsent* znaleziony w `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogu .</span><span class="sxs-lookup"><span data-stu-id="b0cc6-190">Open the *PartnerConsent* project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

7. <span data-ttu-id="b0cc6-191">Wypełnij ustawienia aplikacji znalezione w pliku [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) aplikacji</span><span class="sxs-lookup"><span data-stu-id="b0cc6-191">Populate the application settings found in the [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) file</span></span>

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
    > <span data-ttu-id="b0cc6-192">Poufne informacje, takie jak wpisy tajne aplikacji, nie powinny być przechowywane w plikach konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-192">Sensitive information such as application secrets should not be stored in configurations files.</span></span> <span data-ttu-id="b0cc6-193">Zostało to zrobione w tym miejscu, ponieważ jest to przykładowa aplikacja.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-193">It was done here because this is a sample application.</span></span> <span data-ttu-id="b0cc6-194">W przypadku aplikacji produkcyjnej zdecydowanie zalecamy użycie uwierzytelniania opartego na certyfikatach.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-194">With your production application, we strongly recommend that you use certificate based authenticate.</span></span> <span data-ttu-id="b0cc6-195">Aby uzyskać więcej informacji, zobacz [Key Vault Uwierzytelnianie certyfikatu.](https://github.com/Azure-Samples/key-vault-java-certificate-authentication)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-195">For more information, see [Key Vault Certificate authentication](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).</span></span>

8. <span data-ttu-id="b0cc6-196">Po uruchomieniu tego przykładowego projektu zostanie wyświetlony monit o uwierzytelnienie.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-196">When you run this sample project, it will prompt you for authentication.</span></span> <span data-ttu-id="b0cc6-197">Po pomyślnym uwierzytelnieniu z usługi Azure AD jest żądany token dostępu.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-197">After successfully authenticating, an access token is requested from Azure AD.</span></span> <span data-ttu-id="b0cc6-198">Informacje zwrócone z usługi Azure AD obejmują token odświeżania, który jest przechowywany w skonfigurowanym wystąpieniu Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-198">The information returned from Azure AD includes a refresh token that is stored in the configured instance of Azure Key Vault.</span></span>

## <a name="cloud-solution-provider-authentication"></a><span data-ttu-id="b0cc6-199">Dostawca rozwiązań w chmurze uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="b0cc6-199">Cloud Solution Provider authentication</span></span>

<span data-ttu-id="b0cc6-200">Dostawca rozwiązań w chmurze mogą używać tokenu odświeżania uzyskanego w procesie [wyrażania zgody](#partner-consent) przez partnera.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-200">Cloud Solution Provider partners can use the refresh token obtained through the [partner consent](#partner-consent) process.</span></span>

### <a name="samples-for-cloud-solution-provider-authentication"></a><span data-ttu-id="b0cc6-201">Przykłady uwierzytelniania Dostawca rozwiązań w chmurze danych</span><span class="sxs-lookup"><span data-stu-id="b0cc6-201">Samples for Cloud Solution Provider authentication</span></span>

<span data-ttu-id="b0cc6-202">Aby pomóc partnerom zrozumieć, jak wykonać każdą wymaganą operację, opracowaliśmy następujące przykłady.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-202">To help partners understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="b0cc6-203">Podczas wdrażania odpowiedniego rozwiązania w środowisku ważne jest, aby opracować rozwiązanie, które jest zgodnie ze standardami kodowania i zasadami zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-203">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-csp-authentication"></a><span data-ttu-id="b0cc6-204">.NET (uwierzytelnianie CSP)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-204">.NET (CSP authentication)</span></span>

1. <span data-ttu-id="b0cc6-205">Jeśli jeszcze tego nie zrobiono, wykonaj proces [zgody partnera.](#partner-consent)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-205">If you have not already done so, perform the [partner consent process](#partner-consent).</span></span>

2. <span data-ttu-id="b0cc6-206">[Sklonuj repozytorium Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) przy użyciu Visual Studio lub następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="b0cc6-206">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. <span data-ttu-id="b0cc6-207">Otwórz `CSPApplication` projekt znaleziony w `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogu .</span><span class="sxs-lookup"><span data-stu-id="b0cc6-207">Open the `CSPApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="b0cc6-208">Zaktualizuj ustawienia aplikacji znalezione w [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-208">Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) file.</span></span>

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

5. <span data-ttu-id="b0cc6-209">Ustaw odpowiednie wartości zmiennych **PartnerId** i **CustomerId** znalezionych w [pliku Program.cs.](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-209">Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) file.</span></span>

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. <span data-ttu-id="b0cc6-210">Po uruchomieniu tego przykładowego projektu uzyskuje on token odświeżania uzyskany podczas procesu wyrażania zgody przez partnera.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-210">When you run this sample project, it obtains the refresh token obtained during the partner consent process.</span></span> <span data-ttu-id="b0cc6-211">Następnie żąda tokenu dostępu do interakcji z zestaw SDK Centrum partnerskiego w imieniu partnera.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-211">Then, it requests an access token to interact with the Partner Center SDK on the partner's behalf.</span></span> <span data-ttu-id="b0cc6-212">Na koniec żąda tokenu dostępu do interakcji z Graph Microsoft w imieniu określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-212">Finally, it requests an access token to interact with Microsoft Graph on behalf of the specified customer.</span></span>

## <a name="java-csp-authentication"></a><span data-ttu-id="b0cc6-213">Java (uwierzytelnianie CSP)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-213">Java (CSP authentication)</span></span>

1. <span data-ttu-id="b0cc6-214">Jeśli jeszcze tego nie zrobiono, wykonaj proces [wyrażania zgody przez partnera.](#partner-consent)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-214">If you have not done so already, perform the [partner consent process](#partner-consent).</span></span>

2. <span data-ttu-id="b0cc6-215">[Sklonuj repozytorium Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) przy użyciu Visual Studio lub następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="b0cc6-215">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. <span data-ttu-id="b0cc6-216">Otwórz `cspsample` projekt znaleziony w `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogu .</span><span class="sxs-lookup"><span data-stu-id="b0cc6-216">Open the `cspsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="b0cc6-217">Zaktualizuj ustawienia aplikacji znalezione w pliku [application.properties.](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-217">Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) file.</span></span>

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. <span data-ttu-id="b0cc6-218">Po uruchomieniu tego przykładowego projektu uzyskuje on token odświeżania uzyskany podczas procesu wyrażania zgody przez partnera.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-218">When you run this sample project, it obtains the refresh token obtained during the partner consent process.</span></span> <span data-ttu-id="b0cc6-219">Następnie żąda tokenu dostępu do interakcji z zestaw SDK Centrum partnerskiego w imieniu partnera.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-219">Then, it requests an access token to interact with the Partner Center SDK on the partner's behalf.</span></span>

6. <span data-ttu-id="b0cc6-220">Opcjonalnie — cokłoń wywołania funkcji *RunAzureTask* i *RunGraphTask,* jeśli chcesz zobaczyć, jak wchodzić w interakcje z usługami Azure Resource Manager i Microsoft Graph w imieniu klienta.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-220">Optional - uncomment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with Azure Resource Manager and Microsoft Graph on behalf of the customer.</span></span>

## <a name="control-panel-provider-authentication"></a><span data-ttu-id="b0cc6-221">Panel sterowania uwierzytelniania dostawcy</span><span class="sxs-lookup"><span data-stu-id="b0cc6-221">Control Panel Provider authentication</span></span>

<span data-ttu-id="b0cc6-222">Dostawcy panelu sterowania muszą mieć każdego partnera, który obsługują, w procesie [wyrażania przez nich](#partner-consent) zgody.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-222">Control panel vendors need to have each partner they support perform the [partner consent](#partner-consent) process.</span></span> <span data-ttu-id="b0cc6-223">Po zakończeniu token odświeżania uzyskany w ramach tego procesu jest używany do uzyskiwania dostępu do interfejsu API REST Partner Center api .NET.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-223">Once that is completed the refresh token obtained through that process is used to access the Partner Center REST API and .NET API.</span></span>

### <a name="samples-for-cloud-panel-provider-authentication"></a><span data-ttu-id="b0cc6-224">Przykłady uwierzytelniania dostawcy paneli w chmurze</span><span class="sxs-lookup"><span data-stu-id="b0cc6-224">Samples for Cloud Panel Provider authentication</span></span>

<span data-ttu-id="b0cc6-225">Aby ułatwić dostawcom panelu sterowania zrozumienie sposobu wykonywania poszczególnych wymaganych operacji, opracowaliśmy następujące przykłady.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-225">To help control panel vendors understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="b0cc6-226">Podczas wdrażania odpowiedniego rozwiązania w środowisku ważne jest, aby opracować rozwiązanie, które jest zgodnie ze standardami kodowania i zasadami zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-226">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-cpv-authentication"></a><span data-ttu-id="b0cc6-227">.NET (uwierzytelnianie CPV)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-227">.NET (CPV authentication)</span></span>

1. <span data-ttu-id="b0cc6-228">Opracowywanie i wdrażanie procesu dla partnerów Dostawca rozwiązań w chmurze w celu wyrażenia odpowiedniej zgody.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-228">Develop and deploy a process for Cloud Solution Provider partners to provide the appropriate consent.</span></span> <span data-ttu-id="b0cc6-229">Aby uzyskać więcej informacji na przykład, zobacz [Zgoda partnera](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="b0cc6-229">For more information an example, see [partner consent](#partner-consent).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b0cc6-230">Poświadczenia użytkownika od partnera Dostawca rozwiązań w chmurze nie powinny być przechowywane.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-230">User credentials from a Cloud Solution Provider partner should not be stored.</span></span> <span data-ttu-id="b0cc6-231">Token odświeżania uzyskany w procesie zgody partnera powinien być przechowywany i używany do żądania tokenów dostępu w celu interakcji z dowolnym interfejsem API firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-231">The refresh token obtained through the partner consent process should be stored and used to request access tokens for interacting with any Microsoft API.</span></span>

2. <span data-ttu-id="b0cc6-232">[Sklonuj repozytorium Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) przy użyciu Visual Studio lub następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="b0cc6-232">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. <span data-ttu-id="b0cc6-233">Otwórz `CPVApplication` projekt znaleziony w `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogu .</span><span class="sxs-lookup"><span data-stu-id="b0cc6-233">Open the `CPVApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="b0cc6-234">Zaktualizuj ustawienia aplikacji znalezione w [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-234">Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) file.</span></span>

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

5. <span data-ttu-id="b0cc6-235">Ustaw odpowiednie wartości zmiennych **PartnerId** i **CustomerId** znalezionych w [pliku Program.cs.](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-235">Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) file.</span></span>

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. <span data-ttu-id="b0cc6-236">Po uruchomieniu tego przykładowego projektu uzyskuje token odświeżania dla określonego partnera.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-236">When you run this sample project, it obtains the refresh token for the specified partner.</span></span> <span data-ttu-id="b0cc6-237">Następnie żąda tokenu dostępu w celu uzyskania Partner Center i usługi Azure AD Graph w imieniu partnera.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-237">Then, it requests an access token to access Partner Center and Azure AD Graph on behalf of the partner.</span></span> <span data-ttu-id="b0cc6-238">Następnym zadaniem, które wykonuje, jest usunięcie i utworzenie uprawnień udzielanych do dzierżawy klienta.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-238">The next task it performs is the deletion and creation of permission grants into the customer tenant.</span></span> <span data-ttu-id="b0cc6-239">Ponieważ nie ma relacji między dostawcą panelu sterowania a klientem, te uprawnienia należy dodać przy użyciu Partner Center API.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-239">Since there's no relationship between the control panel vendor and the customer, these permissions need to be added using the Partner Center API.</span></span> <span data-ttu-id="b0cc6-240">W poniższym przykładzie pokazano, jak to zrobić.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-240">The following example shows how to accomplish that.</span></span>

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

<span data-ttu-id="b0cc6-241">Po niu tych uprawnień przykład wykonuje operacje przy użyciu usługi Azure AD Graph w imieniu klienta.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-241">After these permissions have been established, the sample performs operations using Azure AD Graph on behalf of the customer.</span></span>

## <a name="java-cpv-authentication"></a><span data-ttu-id="b0cc6-242">Java (uwierzytelnianie CPV)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-242">Java (CPV authentication)</span></span>

1. <span data-ttu-id="b0cc6-243">Opracowywanie i wdrażanie procesu dla partnerów Dostawca rozwiązań w chmurze w celu wyrażenia odpowiedniej zgody.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-243">Develop and deploy a process for Cloud Solution Provider partners to provide the appropriate consent.</span></span> <span data-ttu-id="b0cc6-244">Aby uzyskać więcej informacji i przykład, zobacz [zgoda partnera](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="b0cc6-244">For more information and an example, see the [partner consent](#partner-consent).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b0cc6-245">Poświadczenia użytkownika od partnera Dostawca rozwiązań w chmurze nie powinny być przechowywane.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-245">User credentials from a Cloud Solution Provider partner should not be stored.</span></span> <span data-ttu-id="b0cc6-246">Token odświeżania uzyskany w procesie zgody partnera powinien być przechowywany i używany do żądania tokenów dostępu w celu interakcji z dowolnym interfejsem API firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-246">The refresh token obtained through the partner consent process should be stored and used to request access tokens for interacting with any Microsoft API.</span></span>

2. <span data-ttu-id="b0cc6-247">[Sklonuj repozytorium Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) przy użyciu następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="b0cc6-247">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. <span data-ttu-id="b0cc6-248">Otwórz `cpvsample` projekt znaleziony w `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogu .</span><span class="sxs-lookup"><span data-stu-id="b0cc6-248">Open the `cpvsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="b0cc6-249">Zaktualizuj ustawienia aplikacji znalezione w pliku [application.properties.](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-249">Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) file.</span></span>

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

    <span data-ttu-id="b0cc6-250">Wartością powinna `partnercenter.displayName` być nazwa wyświetlana aplikacji na platformie handlowej.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-250">The value for the `partnercenter.displayName` should be the display name of your marketplace application.</span></span>

5. <span data-ttu-id="b0cc6-251">Ustaw odpowiednie wartości zmiennych **partnerId** i **customerId** znalezionych w [pliku Program.java.](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java)</span><span class="sxs-lookup"><span data-stu-id="b0cc6-251">Set the appropriate values for the **partnerId** and **customerId** variables found in the [Program.java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) file.</span></span>

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. <span data-ttu-id="b0cc6-252">Po uruchomieniu tego przykładowego projektu uzyskuje token odświeżania dla określonego partnera.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-252">When you run this sample project, it obtains the refresh token for the specified partner.</span></span> <span data-ttu-id="b0cc6-253">Następnie żąda tokenu dostępu w celu uzyskania Partner Center w imieniu partnera.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-253">Then, it requests an access token to access Partner Center on behalf of the partner.</span></span> <span data-ttu-id="b0cc6-254">Następnym zadaniem, które wykonuje, jest usunięcie i utworzenie uprawnień udzielanych do dzierżawy klienta.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-254">The next task it performs is the deletion and creation of permission grants into the customer tenant.</span></span> <span data-ttu-id="b0cc6-255">Ponieważ nie ma relacji między dostawcą panelu sterowania a klientem, te uprawnienia należy dodać przy użyciu Partner Center API.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-255">Since there's no relationship between the control panel vendor and the customer, these permissions need to be added using the Partner Center API.</span></span> <span data-ttu-id="b0cc6-256">W poniższym przykładzie pokazano, jak udzielić uprawnień.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-256">The following example shows how to grant the permissions.</span></span>

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

<span data-ttu-id="b0cc6-257">Cokmentuj wywołania funkcji *RunAzureTask* i *RunGraphTask,* jeśli chcesz zobaczyć, jak wchodzić w interakcje z usługami Azure Resource Manager i Microsoft Graph w imieniu klienta.</span><span class="sxs-lookup"><span data-stu-id="b0cc6-257">Uncomment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with Azure Resource Manager and Microsoft Graph on behalf of the customer.</span></span>
