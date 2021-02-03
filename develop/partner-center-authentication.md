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
# <a name="partner-center-authentication"></a>Uwierzytelnianie w Centrum partnerskim

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Centrum partnerskie w celu uwierzytelniania używa usługi Azure Active Directory. Korzystając z interfejsu API Centrum partnerskiego, zestawu SDK lub modułu programu PowerShell, należy prawidłowo skonfigurować aplikację usługi Azure AD, a następnie zażądać tokenu dostępu. Tokeny dostępu uzyskane przy użyciu tylko aplikacji lub uwierzytelnianie użytkownika i aplikacji mogą być używane z centrum partnerskim. Istnieją jednak dwa ważne elementy, które należy wziąć pod uwagę

- Użyj uwierzytelniania wieloskładnikowego podczas uzyskiwania dostępu do interfejsu API Centrum partnerskiego przy użyciu aplikacji + uwierzytelnianie użytkowników. Aby uzyskać więcej informacji dotyczących tej zmiany, zobacz [Włączanie bezpiecznego modelu aplikacji](enable-secure-app-model.md).

- Nie wszystkie operacje obsługują tylko aplikacje w interfejsie API Centrum partnerskiego. Istnieją pewne scenariusze, w których będzie wymagane użycie aplikacji i uwierzytelniania użytkowników. W sekcji *wymagania wstępne* dotyczące każdego [artykułu](scenarios.md)znajdziesz dokumentację zawierającą informacje o tym, czy obsługiwane są tylko aplikacje uwierzytelnianie, aplikacja + uwierzytelnianie użytkownika, czy też oba te elementy.

## <a name="initial-setup"></a>Początkowa konfiguracja

1. Aby rozpocząć, musisz upewnić się, że masz zarówno konto głównego centrum partnerskiego, jak i konto Centrum partnerskiego usługi piaskownicy integracji. Aby uzyskać więcej informacji, zobacz [Konfigurowanie kont Centrum partnerskiego na potrzeby dostępu do interfejsu API](set-up-api-access-in-partner-center.md). Zanotuj identyfikator rejestracji i wpis tajny aplikacji usługi Azure AAD (klucz tajny klienta jest wymagany tylko do identyfikacji aplikacji) zarówno dla konta podstawowego, jak i konta piaskownicy integracji.

2. Zaloguj się do usługi Azure AD z poziomu Azure Portal. W obszarze **uprawnienia do innych aplikacji** Ustaw uprawnienia dla **systemu Windows Azure Active Directory** na **delegowane uprawnienia**, a następnie wybierz pozycję **dostęp do katalogu jako zalogowany użytkownik** i **Zaloguj się i odczytaj profil użytkownika**.

3. W Azure Portal **Dodaj aplikację**. Wyszukaj frazę "Microsoft Partner Center", która jest aplikacją Microsoft Partner Center. Ustaw **uprawnienia delegowane** na **dostęp do interfejsu API Centrum partnerskiego**. Jeśli używasz Centrum partnerskiego do Microsoft Cloud Niemiec lub Centrum partnerskiego dla Microsoft Cloud dla instytucji rządowych USA, ten krok jest obowiązkowy. Jeśli używasz wystąpienia globalnego Centrum partnerskiego, ten krok jest opcjonalny. Partnerzy programu CSP mogą użyć funkcji zarządzania aplikacjami w portalu Centrum partnerskiego, aby pominąć ten krok dla wystąpienia globalnego Centrum partnerskiego.

## <a name="app-only-authentication"></a>Uwierzytelnianie tylko aplikacji

Jeśli chcesz użyć uwierzytelniania tylko do aplikacji w celu uzyskania dostępu do interfejsu API REST Centrum partnerskiego, interfejsu API platformy .NET, interfejsu API języka Java lub modułu programu PowerShell, możesz to zrobić, wykonując poniższe instrukcje.

## <a name="net-app-only-authentication"></a>.NET (uwierzytelnianie tylko aplikacji)

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

## <a name="java-app-only-authentication"></a>Java (uwierzytelnianie tylko w aplikacji)

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

## <a name="rest-app-only-authentication"></a>REST (uwierzytelnianie tylko w aplikacji)

### <a name="rest-request"></a>Żądanie REST

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

### <a name="rest-response"></a>Odpowiedź REST

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

## <a name="app--user-authentication"></a>Aplikacja + uwierzytelnianie użytkownika

Historycznie [Przydziel poświadczenia hasła właściciela zasobu](https://tools.ietf.org/html/rfc6749#section-4.3) , aby zażądać tokenu dostępu do użycia w module interfejsu API REST Centrum partnerskiego, interfejsu API platformy .NET, interfejsu API języka Java lub modułu PowerShell. Ta metoda została użyta do żądania tokenu dostępu z Azure Active Directory przy użyciu identyfikatora klienta i poświadczeń użytkownika. Jednak takie podejście przestanie działać, ponieważ centrum partnerskie wymaga uwierzytelniania wieloskładnikowego w przypadku korzystania z aplikacji i uwierzytelniania użytkowników. Aby zapewnić zgodność z tym wymaganiem, firma Microsoft wprowadziła bezpieczną, skalowalną platformę do uwierzytelniania partnerów dostawcy rozwiązań w chmurze (CSP) i dostawców panelu sterowania (CPV) przy użyciu uwierzytelniania wieloskładnikowego. Ta struktura jest znana jako bezpieczny model aplikacji i składa się z procesu wyrażania zgody oraz żądania tokenu dostępu przy użyciu tokenu odświeżania.

### <a name="partner-consent"></a>Zgoda partnera

Proces zgody partnera to interaktywny proces, w którym partner uwierzytelnia się przy użyciu uwierzytelniania wieloskładnikowego, jest wysyłany do aplikacji, a token odświeżania jest przechowywany w bezpiecznym repozytorium, takim jak Azure Key Vault. Zalecamy, aby dla tego procesu używać dedykowanego konta do celów związanych z integracją.

> [!IMPORTANT]
> Należy włączyć odpowiednie rozwiązanie do uwierzytelniania wieloskładnikowego dla konta usługi używanego w procesie zgody partnera. Jeśli nie, wynikowy token odświeżania nie będzie zgodny z wymaganiami dotyczącymi zabezpieczeń.

### <a name="samples-for-app--user-authentication"></a>Przykłady dla aplikacji i uwierzytelniania użytkowników

Proces zgody partnera można wykonać na wiele sposobów. Aby pomóc partnerom zrozumieć, jak wykonać każdą wymaganą operację, opracowano następujące przykłady. W przypadku zaimplementowania odpowiedniego rozwiązania w środowisku należy opracować rozwiązanie, które jest zgodne ze standardami kodowania i zasadami zabezpieczeń.

## <a name="net-appuser-authentication"></a>.NET (aplikacja + uwierzytelnianie użytkownika)

Przykładowy projekt [zgody partnera](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) pokazuje, jak używać witryny sieci Web opracowanej przy użyciu ASP.NET do przechwytywania zgody, żądania tokenu odświeżania i bezpiecznego przechowywania w Azure Key Vault. Wykonaj następujące kroki, aby utworzyć wymagane wymagania wstępne dla tego przykładu.

1. Utwórz wystąpienie Azure Key Vault przy użyciu Azure Portal lub następujących poleceń programu PowerShell. Przed wykonaniem polecenia należy koniecznie zmodyfikować wartości parametrów. Nazwa magazynu musi być unikatowa.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Aby uzyskać więcej informacji na temat tworzenia Azure Key Vault, zobacz [Szybki Start: Ustawianie i pobieranie klucza tajnego z Azure Key Vault przy użyciu Azure Portal](/azure/key-vault/quick-create-portal) lub [szybkiego startu: Ustaw i Pobierz klucz tajny z Azure Key Vault przy użyciu programu PowerShell](/azure/key-vault/quick-create-powershell). Następnie ustaw i Pobierz wpis tajny.

2. Utwórz aplikację usługi Azure AD i klucz przy użyciu Azure Portal lub następujących poleceń.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Pamiętaj, aby zanotować identyfikator aplikacji i wartości klucza tajnego, ponieważ zostaną one użyte w poniższych krokach.

3. Przyznaj nowo utworzone aplikacje usługi Azure AD za pomocą Azure Portal lub następujących poleceń.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Utwórz aplikację usługi Azure AD, która jest skonfigurowana dla Centrum partnerskiego. Wykonaj poniższe czynności, aby wykonać ten krok.

    - Przejdź do funkcji [zarządzania aplikacjami](https://partner.microsoft.com/pcv/apiintegration/appmanagement) na pulpicie nawigacyjnym Centrum partnerskiego
    - Kliknij pozycję *Dodaj nową aplikację sieci Web* , aby utworzyć nową aplikację usługi Azure AD.

    Upewnij się, że zostały udokumentowane *identyfikatory aplikacji*, * identyfikator konta * * i wartości *klucza* , ponieważ zostaną one użyte w poniższych krokach.

5. Sklonuj repozytorium [partnerskie — przykłady](https://github.com/Microsoft/Partner-Center-DotNet-Samples) dla tego programu przy użyciu programu Visual Studio lub poniższego polecenia.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. Otwórz projekt *PartnerConsent* znaleziony w `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogu.

7. Wypełnij ustawienia aplikacji Znalezione w [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)

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
    > Informacje poufne, takie jak wpisy tajne aplikacji, nie powinny być przechowywane w plikach konfiguracji. Zostało to zrobione w tym miejscu, ponieważ jest to przykładowa aplikacja. W przypadku aplikacji produkcyjnej zdecydowanie zalecamy użycie uwierzytelniania opartego na certyfikatach. Aby uzyskać więcej informacji, zobacz [poświadczenia certyfikatu na potrzeby uwierzytelniania aplikacji]( /azure/active-directory/develop/active-directory-certificate-credentials).

8. Po uruchomieniu tego przykładowego projektu zostanie wyświetlony monit o uwierzytelnienie. Po pomyślnym uwierzytelnieniu token dostępu jest zaproszony z usługi Azure AD. Informacje zwracane z usługi Azure AD obejmują token odświeżania, który jest przechowywany w skonfigurowanym wystąpieniu Azure Key Vault.

## <a name="java-appuser-authentication"></a>Java (uwierzytelnianie aplikacji i użytkowników)

Przykładowy projekt [zgody partnera](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) pokazuje, jak używać witryny sieci Web opracowanej przy użyciu JSP do przechwytywania zgody, żądania tokenu odświeżania i bezpiecznego magazynu w Azure Key Vault. Wykonaj poniższe czynności, aby utworzyć wymagane wymagania wstępne dla tego przykładu.

1. Utwórz wystąpienie Azure Key Vault przy użyciu Azure Portal lub następujących poleceń programu PowerShell. Przed wykonaniem polecenia należy koniecznie zmodyfikować wartości parametrów. Nazwa magazynu musi być unikatowa.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Aby uzyskać więcej informacji na temat tworzenia Azure Key Vault, zobacz [Szybki Start: Ustawianie i pobieranie klucza tajnego z Azure Key Vault przy użyciu Azure Portal](/azure/key-vault/quick-create-portal) lub [szybkiego startu: Ustaw i Pobierz klucz tajny z Azure Key Vault przy użyciu programu PowerShell](/azure/key-vault/quick-create-powershell).

2. Utwórz aplikację usługi Azure AD i klucz przy użyciu Azure Portal lub następujących poleceń.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Upewnij się, że zostały udokumentowane identyfikatory aplikacji i wartości tajne, ponieważ zostaną one użyte w poniższych krokach.

3. Przyznaj nowo utworzoną aplikację usługi Azure AD uprawnienia Odczyt wpisów tajnych przy użyciu Azure Portal lub następujących poleceń.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Utwórz aplikację usługi Azure AD, która jest skonfigurowana dla Centrum partnerskiego. Aby ukończyć ten krok, wykonaj następujące czynności.

    - Przejdź do funkcji [zarządzania aplikacjami](https://partner.microsoft.com/pcv/apiintegration/appmanagement) na pulpicie nawigacyjnym Centrum partnerskiego
    - Kliknij pozycję *Dodaj nową aplikację sieci Web* , aby utworzyć nową aplikację usługi Azure AD.

    Upewnij się, że zostały udokumentowane *identyfikatory aplikacji*, * identyfikator konta * * i wartości *klucza* , ponieważ zostaną one użyte w poniższych krokach.

5. Sklonuj repozytorium [partnerskie-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) przy użyciu następującego polecenia

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. Otwórz projekt *PartnerConsent* znaleziony w `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogu.

7. Wypełnij ustawienia aplikacji Znalezione w pliku [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml)

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
    > Informacje poufne, takie jak wpisy tajne aplikacji, nie powinny być przechowywane w plikach konfiguracji. Zostało to zrobione w tym miejscu, ponieważ jest to przykładowa aplikacja. Zdecydowanie zalecamy używanie uwierzytelniania opartego na certyfikatach w aplikacji produkcyjnej. Aby uzyskać więcej informacji, zobacz [Key Vault uwierzytelnianie certyfikatu](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).

8. Po uruchomieniu tego przykładowego projektu zostanie wyświetlony monit o uwierzytelnienie. Po pomyślnym uwierzytelnieniu token dostępu jest zaproszony z usługi Azure AD. Informacje zwracane z usługi Azure AD obejmują token odświeżania, który jest przechowywany w skonfigurowanym wystąpieniu Azure Key Vault.

## <a name="cloud-solution-provider-authentication"></a>Uwierzytelnianie dostawcy rozwiązań w chmurze

Partnerzy dostawcy rozwiązań w chmurze mogą używać tokenu odświeżania uzyskanego w ramach procesu [zgody partnera](#partner-consent) .

### <a name="samples-for-cloud-solution-provider-authentication"></a>Przykłady uwierzytelniania dostawcy rozwiązań w chmurze

Aby pomóc partnerom zrozumieć, jak wykonać każdą wymaganą operację, opracowano następujące przykłady. W przypadku zaimplementowania odpowiedniego rozwiązania w środowisku należy opracować rozwiązanie, które jest zgodne ze standardami kodowania i zasadami zabezpieczeń.

## <a name="net-csp-authentication"></a>.NET (uwierzytelnianie CSP)

1. Jeśli jeszcze tego nie zrobiono, wykonaj [proces zgody partnera](#partner-consent).

2. Klonowanie repozytorium z [przykładem partnera](https://github.com/Microsoft/Partner-Center-DotNet-Samples) z użyciem programu Visual Studio lub następującego polecenia

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Otwórz `CSPApplication` projekt znaleziony w `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogu.

4. Aktualizacja ustawień aplikacji znalezionych w pliku [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) .

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

5. Ustaw odpowiednie wartości zmiennych **PartnerId** i **CustomerID** znalezionych w pliku [program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) .

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. Po uruchomieniu tego przykładowego projektu uzyskuje token odświeżania uzyskany podczas procesu wyrażania zgody partnera. Następnie żąda tokenu dostępu do współdziałania z zestawem SDK Centrum partnerskiego w imieniu partnera. Na koniec żąda tokenu dostępu do współpracy z Microsoft Graph w imieniu określonego klienta.

## <a name="java-csp-authentication"></a>Java (uwierzytelnianie CSP)

1. Jeśli jeszcze tego nie zrobiono, wykonaj [proces zgody partnera](#partner-consent).

2. Sklonuj repozytorium [partner-Sample-Java-przykłady](https://github.com/Microsoft/Partner-Center-Java-Samples) przy użyciu programu Visual Studio lub następującego polecenia

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Otwórz `cspsample` projekt znaleziony w `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogu.

4. Zaktualizuj ustawienia aplikacji Znalezione w pliku [Application. Properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) .

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. Po uruchomieniu tego przykładowego projektu uzyskuje token odświeżania uzyskany podczas procesu wyrażania zgody partnera. Następnie żąda tokenu dostępu do współdziałania z zestawem SDK Centrum partnerskiego w imieniu partnera.

6. Opcjonalne — Usuń komentarz z wywołań funkcji *RunAzureTask* i *RunGraphTask* , jeśli chcesz zobaczyć, jak korzystać z Azure Resource Manager i Microsoft Graph w imieniu klienta.

## <a name="control-panel-provider-authentication"></a>Uwierzytelnianie dostawcy panelu sterowania

Dostawcy panelu sterowania muszą mieć wszystkich partnerów, którzy obsługują proces [wyrażania zgody partnera](#partner-consent) . Po ukończeniu token odświeżania uzyskany za pomocą tego procesu jest używany w celu uzyskania dostępu do interfejsu API REST Centrum partnerskiego i interfejsu API platformy .NET.

### <a name="samples-for-cloud-panel-provider-authentication"></a>Przykłady uwierzytelniania dostawcy w panelu Cloud

Aby ułatwić dostawcom panelu sterowania zrozumienie, jak wykonać każdą wymaganą operację, opracowano następujące przykłady. W przypadku zaimplementowania odpowiedniego rozwiązania w środowisku należy opracować rozwiązanie, które jest zgodne ze standardami kodowania i zasadami zabezpieczeń.

## <a name="net-cpv-authentication"></a>.NET (uwierzytelnianie CPV)

1. Utwórz i Wdróż proces dla partnerów dostawcy rozwiązań w chmurze, aby zapewnić odpowiednią zgodę. Aby uzyskać więcej informacji, zobacz temat [zgody partnera](#partner-consent).

    > [!IMPORTANT]
    > Nie należy przechowywać poświadczeń użytkownika od partnera dostawcy rozwiązań w chmurze. Token odświeżania uzyskany przez proces wyrażania zgody partnera powinien być przechowywany i używany do żądania tokenów dostępu w celu współpracy z dowolnym interfejsem API firmy Microsoft.

2. Klonowanie repozytorium z [przykładem partnera](https://github.com/Microsoft/Partner-Center-DotNet-Samples) z użyciem programu Visual Studio lub następującego polecenia

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Otwórz `CPVApplication` projekt znaleziony w `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogu.

4. Aktualizacja ustawień aplikacji znalezionych w pliku [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) .

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

5. Ustaw odpowiednie wartości zmiennych **PartnerId** i **CustomerID** znalezionych w pliku [program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) .

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. Po uruchomieniu tego przykładowego projektu zostanie uzyskany token odświeżania dla określonego partnera. Następnie żąda tokenu dostępu, aby uzyskać dostęp do Centrum partnerskiego i grafu usługi Azure AD w imieniu partnera. Następne zadanie, które wykonuje, to usunięcie i utworzenie dotacji do dzierżawy klienta. Ponieważ nie istnieje żadna relacja między dostawcą panelu sterowania a klientem, te uprawnienia należy dodać przy użyciu interfejsu API Centrum partnerskiego. Poniższy przykład pokazuje, jak to zrobić.

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

Po nawiązaniu tych uprawnień przykład wykonuje operacje przy użyciu programu Azure AD Graph w imieniu klienta.

## <a name="java-cpv-authentication"></a>Java (uwierzytelnianie CPV)

1. Utwórz i Wdróż proces dla partnerów dostawcy rozwiązań w chmurze, aby zapewnić odpowiednią zgodę. Aby uzyskać więcej informacji i zapoznać się z przykładem, zapoznaj się z tematem [zgody partnera](#partner-consent).

    > [!IMPORTANT]
    > Nie należy przechowywać poświadczeń użytkownika od partnera dostawcy rozwiązań w chmurze. Token odświeżania uzyskany przez proces wyrażania zgody partnera powinien być przechowywany i używany do żądania tokenów dostępu w celu współpracy z dowolnym interfejsem API firmy Microsoft.

2. Sklonuj repozytorium [partnerskie-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) przy użyciu następującego polecenia

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Otwórz `cpvsample` projekt znaleziony w `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogu.

4. Zaktualizuj ustawienia aplikacji Znalezione w pliku [Application. Properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) .

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

    Wartość `partnercenter.displayName` powinna być nazwą wyświetlaną aplikacji Marketplace.

5. Ustaw odpowiednie wartości zmiennych **partnerId** i **customerId** znalezionych w pliku [program. Java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) .

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. Po uruchomieniu tego przykładowego projektu zostanie uzyskany token odświeżania dla określonego partnera. Następnie żąda tokenu dostępu, aby uzyskać dostęp do Centrum partnerskiego w imieniu partnera. Następne zadanie, które wykonuje, to usunięcie i utworzenie dotacji do dzierżawy klienta. Ponieważ nie istnieje żadna relacja między dostawcą panelu sterowania a klientem, te uprawnienia należy dodać przy użyciu interfejsu API Centrum partnerskiego. Poniższy przykład pokazuje, jak przyznać uprawnienia.

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

Usuń komentarz z wywołań funkcji *RunAzureTask* i *RunGraphTask* , jeśli chcesz zobaczyć, jak korzystać z Azure Resource Manager i Microsoft Graph w imieniu klienta.
