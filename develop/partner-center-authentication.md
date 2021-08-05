---
title: Uwierzytelnianie w Centrum partnerskim
description: Partner Center używa usługi Azure AD do uwierzytelniania, a aby korzystać z interfejsów API Partner Center, należy poprawnie skonfigurować ustawienia uwierzytelniania.
ms.date: 11/13/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 75d60ca983cd5b8fe53134ec7481319b153e128a
ms.sourcegitcommit: 07b9a11f5c615ed1e716081392032cea2124bd98
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/04/2021
ms.locfileid: "115104197"
---
# <a name="partner-center-authentication"></a>Uwierzytelnianie w Centrum partnerskim

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Centrum partnerskie w celu uwierzytelniania używa usługi Azure Active Directory. Korzystając z interfejsu API Centrum partnerskiego, zestawu SDK lub modułu programu PowerShell, należy prawidłowo skonfigurować aplikację usługi Azure AD, a następnie zażądać tokenu dostępu. Tokeny dostępu uzyskane przy użyciu tylko aplikacji lub uwierzytelniania aplikacji i użytkowników mogą być używane z Partner Center. Istnieją jednak dwa ważne elementy, które należy rozważyć

- Użyj uwierzytelniania wieloskładnikowego podczas uzyskiwania dostępu do interfejsu API Partner Center przy użyciu uwierzytelniania aplikacji i użytkownika. Aby uzyskać więcej informacji na temat tej zmiany, zobacz [Włączanie bezpiecznego modelu aplikacji.](enable-secure-app-model.md)

- Nie wszystkie operacje interfejsu API Partner Center obsługują tylko uwierzytelnianie aplikacji. Istnieją pewne scenariusze, w których konieczne będzie użycie uwierzytelniania aplikacji i użytkowników. W *nagłówku Wymagania* [](scenarios.md)wstępne każdego artykułu znajduje się dokumentacja z pytaniem, czy obsługiwane jest tylko uwierzytelnianie aplikacji, aplikacja i uwierzytelnianie użytkowników.

## <a name="initial-setup"></a>Konfiguracja początkowa

1. Aby rozpocząć, upewnij się, że masz zarówno konto podstawowe, Partner Center, jak i piaskownicę integracji Partner Center konto. Aby uzyskać więcej informacji, zobacz Set up Partner Center accounts for API access (Konfigurowanie kont [usługi Partner Center dostępu do interfejsu API).](set-up-api-access-in-partner-center.md) Zanotuj identyfikator rejestracji aplikacji usługi Azure AAD i wpis tajny (klucz tajny klienta jest wymagany do identyfikacji tylko aplikacji) zarówno dla konta podstawowego, jak i konta piaskownicy integracji.

2. Zaloguj się do usługi Azure AD z Azure Portal. W **uprawnieniach** do innych aplikacji ustaw uprawnienia dla opcji **Windows Azure Active Directory**  na Uprawnienia delegowane **i** wybierz pozycję Uzyskaj dostęp do katalogu jako zalogowany użytkownik, a następnie pozycję Zaloguj i odczytaj **profil użytkownika.**

3. W Azure Portal dodaj **aplikację**. Wyszukaj "Microsoft Partner Center", czyli aplikację microsoft Partner Center. Ustaw uprawnienia **delegowane na dostęp** **do Partner Center API.** Jeśli korzystasz z usługi Partner Center Microsoft Cloud w Niemczech lub Partner Center dla Microsoft Cloud for US Government, ten krok jest obowiązkowy. Jeśli używasz Partner Center globalnego, ten krok jest opcjonalny. Partnerzy CSP mogą użyć funkcji zarządzania aplikacją w portalu Partner Center, aby pominąć ten krok dla Partner Center globalnego.

## <a name="app-only-authentication"></a>Uwierzytelnianie tylko aplikacji

Jeśli chcesz użyć uwierzytelniania tylko dla aplikacji w celu uzyskania dostępu do interfejsu API REST usługi Partner Center, interfejsu API .NET, interfejsu API języka Java lub modułu programu PowerShell, możesz to zrobić, korzystając z poniższych instrukcji.

## <a name="net-app-only-authentication"></a>.NET (uwierzytelnianie tylko dla aplikacji)

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

## <a name="java-app-only-authentication"></a>Java (uwierzytelnianie tylko dla aplikacji)

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

## <a name="rest-app-only-authentication"></a>REST (uwierzytelnianie tylko aplikacji)

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

## <a name="app--user-authentication"></a>Uwierzytelnianie aplikacji i użytkownika

W przeszłości [](https://tools.ietf.org/html/rfc6749#section-4.3) do żądania tokenu dostępu do użycia z interfejsem API REST usługi Partner Center, interfejsem API platformy .NET, interfejsem API języka Java lub modułem programu PowerShell był używany przydział poświadczeń hasła właściciela zasobu. Ta metoda została użyta do zażądania tokenu dostępu od Azure Active Directory przy użyciu identyfikatora klienta i poświadczeń użytkownika. Jednak to podejście nie będzie już działać, ponieważ Partner Center uwierzytelniania wieloskładnikowego podczas korzystania z uwierzytelniania aplikacji i użytkowników. Aby spełnić to wymaganie, firma Microsoft wprowadziła bezpieczną, skalowalną platformę do uwierzytelniania partnerów programu Dostawca rozwiązań w chmurze (CSP) i dostawców panelu sterowania (CPV) przy użyciu uwierzytelniania wieloskładnikowego. Ta framework jest znana jako model aplikacji zabezpieczonych i składa się z procesu wyrażania zgody oraz żądania tokenu dostępu przy użyciu tokenu odświeżania.

### <a name="partner-consent"></a>Zgoda partnera

Proces wyrażania zgody przez partnera to interaktywny proces, w którym partner uwierzytelnia się przy użyciu uwierzytelniania wieloskładnikowego, wyraża zgodę na aplikację, a token odświeżania jest przechowywany w bezpiecznym repozytorium, takim jak Azure Key Vault. W tym procesie zaleca się użycie dedykowanego konta na potrzeby integracji.

> [!IMPORTANT]
> Dla konta usługi używanego w procesie wyrażania zgody partnera należy włączyć odpowiednie rozwiązanie uwierzytelniania wieloskładnikowego. Jeśli tak nie jest, wynikowy token odświeżania nie będzie zgodny z wymaganiami bezpieczeństwa.

### <a name="samples-for-app--user-authentication"></a>Przykłady uwierzytelniania aplikacji i użytkownika

Proces wyrażania zgody przez partnera można wykonać na wiele sposobów. Aby pomóc partnerom zrozumieć, jak wykonać każdą wymaganą operację, opracowaliśmy następujące przykłady. Podczas wdrażania odpowiedniego rozwiązania w środowisku ważne jest, aby opracować rozwiązanie, które jest zgodnie ze standardami kodowania i zasadami zabezpieczeń.

## <a name="net-appuser-authentication"></a>.NET (uwierzytelnianie aplikacji i użytkowników)

Przykładowy [projekt zgody](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) partnera pokazuje, jak korzystać z witryny internetowej opracowanej przy użyciu usługi ASP.NET do przechwytywania zgody, żądania tokenu odświeżania i bezpiecznego przechowywania ich w Azure Key Vault. Wykonaj poniższe kroki, aby utworzyć wymagane wymagania wstępne dla tego przykładu.

1. Utwórz wystąpienie klasy Azure Key Vault za pomocą Azure Portal lub następujących poleceń programu PowerShell. Przed wykonaniem polecenia należy odpowiednio zmodyfikować wartości parametrów. Nazwa magazynu musi być unikatowa.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Aby uzyskać więcej informacji na temat tworzenia konta usługi Azure Key Vault, zobacz Szybki [start:](/azure/key-vault/quick-create-portal) ustawianie i pobieranie informacji tajnych z usługi Azure Key Vault przy użyciu programu Azure Portal lub Szybki start: ustawianie i pobieranie informacji tajnych z usługi Azure Key Vault przy użyciu [programu PowerShell.](/azure/key-vault/quick-create-powershell) Następnie ustaw i pobierz klucz tajny.

2. Utwórz aplikację usługi Azure AD i klucz przy użyciu Azure Portal lub poniższych poleceń.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Pamiętaj, aby zanotować identyfikator aplikacji i wartości klucza tajnego, ponieważ będą one używane w poniższych krokach.

3. Przyznaj nowo utworzonej aplikacji usługi Azure AD uprawnienia do odczytu wpisów tajnych przy użyciu Azure Portal lub poniższych poleceń.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Utwórz aplikację usługi Azure AD skonfigurowaną pod Partner Center. Aby wykonać ten krok, wykonaj następujące czynności.

    - Przejdź do funkcji [zarządzania aplikacją](https://partner.microsoft.com/pcv/apiintegration/appmanagement) pulpitu nawigacyjnego Partner Center nawigacyjnego
    - Wybierz *pozycję Dodaj nową aplikację internetową,* aby utworzyć nową aplikację usługi Azure AD.

    Pamiętaj, aby udokumentować wartości *Identyfikator*  aplikacji, *Identyfikator konta** i Klucz, ponieważ będą one używane w poniższych krokach.

5. [Sklonuj repozytorium Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) przy użyciu Visual Studio lub następującego polecenia.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. Otwórz *projekt PartnerConsent* znaleziony w `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogu .

7. Wypełnij ustawienia aplikacji znalezione [](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config) wweb.config

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
    > Poufne informacje, takie jak wpisy tajne aplikacji, nie powinny być przechowywane w plikach konfiguracji. Zostało to zrobione w tym miejscu, ponieważ jest to przykładowa aplikacja. W przypadku aplikacji produkcyjnej zdecydowanie zalecamy korzystanie z uwierzytelniania opartego na certyfikatach. Aby uzyskać więcej informacji, zobacz [Poświadczenia certyfikatu do uwierzytelniania aplikacji.]( /azure/active-directory/develop/active-directory-certificate-credentials)

8. Po uruchomieniu tego przykładowego projektu zostanie wyświetlony monit o uwierzytelnienie. Po pomyślnym uwierzytelnieniu z usługi Azure AD jest żądany token dostępu. Informacje zwrócone z usługi Azure AD obejmują token odświeżania, który jest przechowywany w skonfigurowanym wystąpieniu Azure Key Vault.

## <a name="java-appuser-authentication"></a>Java (uwierzytelnianie aplikacji i użytkowników)

Przykładowy [projekt zgody](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) partnera pokazuje, jak używać witryny internetowej opracowanej przy użyciu programu JSP do przechwytywania zgody, żądania tokenu odświeżania i bezpiecznego magazynu w Azure Key Vault. Wykonaj następujące czynności, aby utworzyć wymagane wymagania wstępne dla tego przykładu.

1. Utwórz wystąpienie klasy Azure Key Vault za pomocą Azure Portal lub następujących poleceń programu PowerShell. Przed wykonaniem polecenia należy odpowiednio zmodyfikować wartości parametrów. Nazwa magazynu musi być unikatowa.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Aby uzyskać więcej informacji na temat tworzenia konta usługi Azure Key Vault, zobacz Szybki [start:](/azure/key-vault/quick-create-portal) ustawianie i pobieranie informacji tajnych z usługi Azure Key Vault przy użyciu programu Azure Portal lub Szybki start: ustawianie i pobieranie informacji tajnych z usługi Azure Key Vault przy użyciu [programu PowerShell.](/azure/key-vault/quick-create-powershell)

2. Utwórz aplikację usługi Azure AD i klucz przy użyciu Azure Portal lub poniższych poleceń.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Pamiętaj, aby udokumentować wartości identyfikatora aplikacji i klucza tajnego, ponieważ będą one używane w poniższych krokach.

3. Przyznaj nowo utworzonej aplikacji usługi Azure AD uprawnienia do odczytu wpisów tajnych przy użyciu Azure Portal lub poniższych poleceń.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Utwórz aplikację usługi Azure AD skonfigurowaną pod Partner Center. Wykonaj następujące czynności, aby ukończyć ten krok.

    - Przejdź do funkcji [zarządzania aplikacją](https://partner.microsoft.com/pcv/apiintegration/appmanagement) pulpitu nawigacyjnego Partner Center nawigacyjnego
    - Wybierz *pozycję Dodaj nową aplikację internetową,* aby utworzyć nową aplikację usługi Azure AD.

    Pamiętaj, aby udokumentować wartości *Identyfikator*  aplikacji, *Identyfikator konta** i Klucz, ponieważ będą one używane w poniższych krokach.

5. [Sklonuj repozytorium Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) przy użyciu następującego polecenia

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. Otwórz *projekt PartnerConsent* znaleziony w `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogu .

7. Wypełnij ustawienia aplikacji znalezione w pliku [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) aplikacji

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
    > Informacje poufne, takie jak wpisy tajne aplikacji, nie powinny być przechowywane w plikach konfiguracji. Zostało to zrobione w tym miejscu, ponieważ jest to przykładowa aplikacja. W przypadku aplikacji produkcyjnej zdecydowanie zalecamy używanie uwierzytelniania opartego na certyfikatach. Aby uzyskać więcej informacji, zobacz [Key Vault Certificate authentication (Uwierzytelnianie certyfikatu).](https://github.com/Azure-Samples/key-vault-java-certificate-authentication)

8. Po uruchomieniu tego przykładowego projektu zostanie wyświetlony monit o uwierzytelnienie. Po pomyślnym uwierzytelnieniu z usługi Azure AD jest żądany token dostępu. Informacje zwrócone z usługi Azure AD obejmują token odświeżania, który jest przechowywany w skonfigurowanym wystąpieniu Azure Key Vault.

## <a name="cloud-solution-provider-authentication"></a>Dostawca rozwiązań w chmurze uwierzytelniania

Dostawca rozwiązań w chmurze mogą używać tokenu odświeżania uzyskanego w procesie [wyrażania zgody](#partner-consent) przez partnera.

### <a name="samples-for-cloud-solution-provider-authentication"></a>Przykłady uwierzytelniania Dostawca rozwiązań w chmurze danych

Aby pomóc partnerom zrozumieć, jak wykonać każdą wymaganą operację, opracowaliśmy następujące przykłady. Podczas wdrażania odpowiedniego rozwiązania w środowisku ważne jest, aby opracować rozwiązanie, które jest zgodnie ze standardami kodowania i zasadami zabezpieczeń.

## <a name="net-csp-authentication"></a>.NET (uwierzytelnianie CSP)

1. Jeśli jeszcze tego nie zrobiono, wykonaj [proces wyrażania zgody przez partnera.](#partner-consent)

2. [Sklonuj repozytorium Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) przy użyciu Visual Studio lub następującego polecenia

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Otwórz `CSPApplication` projekt znaleziony w `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogu .

4. Zaktualizuj ustawienia aplikacji znalezione w [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) aplikacji.

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

5. Ustaw odpowiednie wartości zmiennych **PartnerId** i **CustomerId** znalezionych w [pliku Program.cs.](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs)

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. Po uruchomieniu tego przykładowego projektu uzyskuje on token odświeżania uzyskany podczas procesu wyrażania zgody przez partnera. Następnie żąda tokenu dostępu do interakcji z zestaw SDK Centrum partnerskiego w imieniu partnera. Na koniec żąda tokenu dostępu do interakcji z Graph Microsoft w imieniu określonego klienta.

## <a name="java-csp-authentication"></a>Java (uwierzytelnianie CSP)

1. Jeśli jeszcze tego nie zrobiono, wykonaj [proces wyrażania zgody przez partnera.](#partner-consent)

2. [Sklonuj repozytorium Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) przy użyciu Visual Studio lub następującego polecenia

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Otwórz `cspsample` projekt znaleziony w `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogu .

4. Zaktualizuj ustawienia aplikacji znalezione w [pliku application.properties.](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties)

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. Po uruchomieniu tego przykładowego projektu uzyskuje on token odświeżania uzyskany podczas procesu wyrażania zgody przez partnera. Następnie żąda tokenu dostępu do interakcji z zestaw SDK Centrum partnerskiego w imieniu partnera.

6. Opcjonalnie — cokłoń wywołania funkcji *RunAzureTask* i *RunGraphTask,* jeśli chcesz zobaczyć, jak wchodzić w interakcje z usługami Azure Resource Manager i Microsoft Graph w imieniu klienta.

## <a name="control-panel-provider-authentication"></a>Panel sterowania uwierzytelniania dostawcy

Dostawcy panelu sterowania muszą mieć każdego partnera, który obsługują, w procesie [wyrażania przez nich](#partner-consent) zgody. Po zakończeniu token odświeżania uzyskany w ramach tego procesu jest używany do uzyskiwania dostępu do interfejsu API REST Partner Center api .NET.

### <a name="samples-for-cloud-panel-provider-authentication"></a>Przykłady uwierzytelniania dostawcy paneli w chmurze

Aby ułatwić dostawcom panelu sterowania zrozumienie sposobu wykonywania poszczególnych wymaganych operacji, opracowaliśmy następujące przykłady. Podczas wdrażania odpowiedniego rozwiązania w środowisku ważne jest, aby opracować rozwiązanie, które jest zgodnie ze standardami kodowania i zasadami zabezpieczeń.

## <a name="net-cpv-authentication"></a>.NET (uwierzytelnianie CPV)

1. Opracowywanie i wdrażanie procesu dla partnerów Dostawca rozwiązań w chmurze w celu wyrażenia odpowiedniej zgody. Aby uzyskać więcej informacji na przykład, zobacz [Zgoda partnera](#partner-consent).

    > [!IMPORTANT]
    > Poświadczenia użytkownika od partnera Dostawca rozwiązań w chmurze nie powinny być przechowywane. Token odświeżania uzyskany w procesie zgody partnera powinien być przechowywany i używany do żądania tokenów dostępu do interakcji z dowolnym interfejsem API firmy Microsoft.

2. [Sklonuj repozytorium Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) przy użyciu Visual Studio lub następującego polecenia

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Otwórz `CPVApplication` projekt znaleziony w `Partner-Center-DotNet-Samples\secure-app-model\keyvault` katalogu .

4. Zaktualizuj ustawienia aplikacji znalezione w [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) aplikacji.

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

5. Ustaw odpowiednie wartości zmiennych **PartnerId** i **CustomerId** znalezionych w [pliku Program.cs.](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs)

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. Po uruchomieniu tego przykładowego projektu uzyskuje token odświeżania dla określonego partnera. Następnie żąda tokenu dostępu w celu uzyskania Partner Center i usługi Azure AD Graph w imieniu partnera. Następnym zadaniem, które wykonuje, jest usunięcie i utworzenie uprawnień udzielanych do dzierżawy klienta. Ponieważ nie ma relacji między dostawcą panelu sterowania a klientem, te uprawnienia należy dodać przy użyciu interfejsu API Partner Center. W poniższym przykładzie pokazano, jak to zrobić.

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

Po niu tych uprawnień przykład wykonuje operacje przy użyciu usługi Azure AD Graph w imieniu klienta.

## <a name="java-cpv-authentication"></a>Java (uwierzytelnianie CPV)

1. Opracowywanie i wdrażanie procesu dla partnerów Dostawca rozwiązań w chmurze w celu wyrażenia odpowiedniej zgody. Aby uzyskać więcej informacji i przykład, zobacz [zgoda partnera](#partner-consent).

    > [!IMPORTANT]
    > Poświadczenia użytkownika od partnera Dostawca rozwiązań w chmurze nie powinny być przechowywane. Token odświeżania uzyskany w procesie zgody partnera powinien być przechowywany i używany do żądania tokenów dostępu do interakcji z dowolnym interfejsem API firmy Microsoft.

2. [Sklonuj repozytorium Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) przy użyciu następującego polecenia

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Otwórz `cpvsample` projekt znaleziony w `Partner-Center-Java-Samples\secure-app-model\keyvault` katalogu .

4. Zaktualizuj ustawienia aplikacji znalezione w [pliku application.properties.](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties)

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

    Wartość powinna `partnercenter.displayName` być nazwą wyświetlaną aplikacji w witrynie Marketplace.

5. Ustaw odpowiednie wartości zmiennych **partnerId** i **customerId** znalezionych w [pliku Program.java.](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java)

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. Po uruchomieniu tego przykładowego projektu uzyskuje token odświeżania dla określonego partnera. Następnie żąda tokenu dostępu w celu uzyskania Partner Center w imieniu partnera. Następnym zadaniem, które wykonuje, jest usunięcie i utworzenie uprawnień udzielanych do dzierżawy klienta. Ponieważ nie ma relacji między dostawcą panelu sterowania a klientem, te uprawnienia należy dodać przy użyciu interfejsu API Partner Center. W poniższym przykładzie pokazano, jak udzielić uprawnień.

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

Cokmentuj wywołania funkcji *RunAzureTask* i *RunGraphTask,* jeśli chcesz zobaczyć, jak wchodzić w interakcje z usługami Azure Resource Manager i Microsoft Graph w imieniu klienta.
