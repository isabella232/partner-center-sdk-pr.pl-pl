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
# <a name="enabling-the-secure-application-model-framework"></a>Włączanie środowiska modelu aplikacji zabezpieczonej

**Dotyczy:**

- Centrum partnerskie

Firma Microsoft wprowadza bezpieczną i skalowalną platformę do uwierzytelniania partnerów dostawcy rozwiązań w chmurze (CSP) i dostawców panelu sterowania (CPV) za pomocą Microsoft Azure architekturę uwierzytelniania wieloskładnikowego (MFA).

Nowy model umożliwia podniesienie poziomu zabezpieczeń dla wywołań integracji z interfejsem API Centrum partnerskiego. Pomoże to wszystkim stronom (w tym partnerom Microsoft, CSP i CPVs) na ochronę danych infrastruktury i klientów przed zagrożeniami bezpieczeństwa.

## <a name="scope"></a>Zakres

Ten artykuł dotyczy następujących podmiotów:

- Dostawcy oprogramowania panelu sterowania
  - Dostawca oprogramowania panelu sterowania (CPV) to niezależny dostawca oprogramowania, który opracowuje aplikacje, których partnerzy CSP mogą używać do integracji z interfejsami API Centrum partnerskiego.
  - Dostawca CPV nie jest partnerem CSP z bezpośrednim dostępem do pulpitu nawigacyjnego lub interfejsów API Centrum partnerskiego.

- Dostawcy usług kryptograficznych CSP i partnerzy bezpośredniego dostawcy usług kryptograficznych, którzy korzystają z identyfikatora aplikacji + uwierzytelnianie użytkownika i bezpośrednio integrują się z interfejsami API Centrum partnerskiego.

## <a name="security-requirements"></a>Wymagania dotyczące zabezpieczeń

Aby uzyskać szczegółowe informacje na temat wymagań dotyczących zabezpieczeń, zobacz [wymagania dotyczące zabezpieczeń partnerów](/partner-center/partner-security-requirements).

## <a name="secure-application-model"></a>Bezpieczny model aplikacji

Aplikacje Marketplace muszą personifikować uprawnienia partnerów CSP, aby wywoływać interfejsy API firmy Microsoft. Ataki na te aplikacje poufne mogą prowadzić do naruszenia bezpieczeństwa danych klientów.

Aby zapoznać się z omówieniem i szczegółami nowej struktury uwierzytelniania, Pobierz dokument [Application Framework bezpiecznego modelu aplikacji](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) . Ten dokument zawiera zasady i najlepsze rozwiązania, dzięki którym aplikacje Marketplace są trwałe i niezawodne przed naruszeniem zabezpieczeń.

## <a name="samples"></a>Samples

W poniższych dokumentach i przykładowym kodzie opisano, jak partnerzy mogą wdrożyć bezpieczną strukturę modelu aplikacji:

- [Dokument omówienia CPV](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [Dokument omówienia CSP](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [Przykłady dla platformy .NET](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [Przykłady dla języka Java](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [Instrukcje i przykłady REST](#rest)
- [Instrukcje i przykłady dotyczące programu PowerShell](#powershell)

## <a name="rest"></a>REST

Aby wykonać wywołania REST w środowisku bezpiecznego modelu aplikacji z przykładowym kodem, wykonaj następujące kroki:

1. [Tworzenie aplikacji internetowej](#create-a-web-app)

2. [Pobieranie kodu autoryzacji](#get-authorization-code)

3. [Pobierz token odświeżania](#get-refresh-token)

4. [Pobranie tokenu dostępu](#get-access-token)

5. [Wykonywanie wywołania interfejsu API Centrum partnerskiego](#make-partner-center-api-calls)

> [!TIP]
> Możesz użyć modułu programu PowerShell Centrum partnerskiego, aby uzyskać kod autoryzacji i token odświeżenia. Możesz wybrać tę opcję zamiast kroków 2 i 3. Aby uzyskać więcej informacji, zapoznaj się z [sekcją i przykładami programu PowerShell](#powershell).

### <a name="create-a-web-app"></a>Tworzenie aplikacji internetowej

Przed włączeniem wywołań REST należy utworzyć i zarejestrować aplikację sieci Web w centrum partnerskim.

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).

2. Utwórz aplikację Azure Active Directory (Azure AD).

3. Przyznaj delegowane uprawnienia aplikacji do następujących zasobów, w *zależności od wymagań aplikacji*. W razie potrzeby można dodać bardziej delegowane uprawnienia dla zasobów aplikacji.

   1. **Centrum partnerskie firmy Microsoft** (w przypadku niektórych dzierżawców jest to **SampleBECApp**)

   2. **Interfejsy API zarządzania platformy Azure** (Jeśli planujesz wywołać interfejsy API platformy Azure)

   3. **Windows Azure Active Directory**

4. Upewnij się, że adres URL strony głównej aplikacji jest ustawiony na punkt końcowy, w którym jest uruchomiona działająca aplikacja sieci Web. Ta aplikacja będzie musiała przyjąć [kod autoryzacji](#get-authorization-code) z wywołania logowania do usługi Azure AD. Na przykład w przykładowym kodzie w [poniższej sekcji](#get-authorization-code)aplikacja sieci Web działa w systemie `https://localhost:44395/` .

5. Zwróć uwagę na następujące informacje z ustawień aplikacji sieci Web w usłudze Azure AD:

   - Identyfikator aplikacji
   - Klucz tajny aplikacji

> [!NOTE]
> Zalecane jest [użycie certyfikatu jako klucza tajnego aplikacji](/azure/active-directory/develop/active-directory-certificate-credentials). Można jednak również utworzyć klucz aplikacji w Azure Portal. Przykładowy kod w [poniższej sekcji](#get-authorization-code) używa klucza aplikacji.

### <a name="get-authorization-code"></a>Uzyskiwanie kodu autoryzacji

Musisz uzyskać kod autoryzacji dla aplikacji sieci Web, aby akceptować dane z wywołania logowania usługi Azure AD:

1. Zaloguj się do usługi Azure AD pod następującym adresem URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) . Pamiętaj, aby zalogować się przy użyciu konta użytkownika, z którego będą nawiązywane wywołania interfejsu API centrum partnera (takie jak Agent administracyjny lub konto agenta sprzedaży).

2. Zamień **Identyfikator aplikacji** na identyfikator aplikacji usługi Azure AD (GUID).

3. Po wyświetleniu monitu zaloguj się przy użyciu konta użytkownika z skonfigurowanym uwierzytelnianiem MFA.

4. Po wyświetleniu monitu wprowadź dodatkowe informacje MFA (numer telefonu lub adres e-mail), aby zweryfikować dane logowania.

5. Po zalogowaniu przeglądarka przekieruje wywołanie do punktu końcowego aplikacji sieci Web przy użyciu kodu autoryzacji. Na przykład poniższy przykładowy kod przekierowuje do `https://localhost:44395/` .

#### <a name="authorization-code-call-trace"></a>Śledzenie wywołań kodu autoryzacji

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

### <a name="get-refresh-token"></a>Pobierz token odświeżania

Aby uzyskać token odświeżenia, należy użyć kodu autoryzacji:

1. Wprowadź wywołanie POST do punktu końcowego logowania usługi Azure AD `https://login.microsoftonline.com/CSPTenantID/oauth2/token` przy użyciu kodu autoryzacji. Aby zapoznać się z przykładem, zobacz następujące [przykładowe wywołanie](#sample-refresh-call).

2. Zwróć uwagę na zwracany token odświeżania.

3. Przechowuj token odświeżania w Azure Key Vault. Aby uzyskać więcej informacji, zobacz [dokumentację interfejsu API Key Vault](/rest/api/keyvault/).

> [!IMPORTANT]
> Token odświeżania musi być [przechowywany jako wpis tajny](/rest/api/keyvault/setsecret/setsecret) w usłudze Key Vault.

#### <a name="sample-refresh-call"></a>Przykładowe wywołanie odświeżania

Żądanie symbolu zastępczego:

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 966
Expect: 100-continue
```

Treść żądania:

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id&client_secret=Application-Secret&grant_type=authorization_code&code=AuthorizationCodeValue
```

Odpowiedź symbolu zastępczego:

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

Treść odpowiedzi:

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a>Uzyskaj token dostępu

Aby umożliwić wywoływanie interfejsów API Centrum partnerskiego, należy uzyskać token dostępu. Aby uzyskać token dostępu, należy użyć tokenu odświeżania, ponieważ token dostępu zwykle ma bardzo ograniczony okres istnienia (na przykład krótszy niż godzina).

Żądanie symbolu zastępczego:

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 1212
Expect: 100-continue
```

Treść żądania:

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id &client_secret= Application-Secret&grant_type=refresh_token&refresh_token=RefreshTokenVlaue&scope=openid
```

Odpowiedź symbolu zastępczego:

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

Treść odpowiedzi:

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a>Tworzenie wywołań interfejsu API Centrum partnerskiego

Musisz użyć tokenu dostępu, aby wywołać interfejsy API Centrum partnerskiego. Zobacz poniższe przykładowe wywołanie.

#### <a name="example-partner-center-api-call"></a>Przykład wywołania interfejsu API Centrum partnerskiego

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Możesz użyć [modułu programu PowerShell Centrum partnerskiego](https://www.powershellgallery.com/packages/PartnerCenter) , aby zmniejszyć wymaganą infrastrukturę do wymiany kodu autoryzacji dla tokenu dostępu. Ta metoda jest opcjonalna w przypadku tworzenia [wywołań REST Centrum partnerskiego](#rest).

Aby uzyskać więcej informacji na temat tego procesu, zobacz [Secure App model](/powershell/partnercenter/secure-app-model) programu PowerShell.

1. Zainstaluj moduły Azure AD i centrum partnerskie programu PowerShell.

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. Użyj polecenia **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** w celu przeprowadzenia procesu wyrażania zgody i przechwycenia wymaganego tokenu odświeżania.

    ```powershell
    $credential = Get-Credential

    New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > Parametr **serviceprincipal** jest używany z poleceniem **New-PartnerAccessToken** , ponieważ jest używana aplikacja usługi Azure AD z typem **sieci Web/API** . Ten typ aplikacji wymaga, aby identyfikator klienta i klucz tajny zostały uwzględnione w żądaniu tokenu dostępu. Po wywołaniu polecenia **Get-Credential** zostanie wyświetlony monit o podanie nazwy użytkownika i hasła. Wprowadź identyfikator aplikacji jako nazwę użytkownika. Wprowadź klucz tajny aplikacji jako hasło. Po wywołaniu polecenia **New-PartnerAccessToken** zostanie wyświetlony monit o ponowne wprowadzenie poświadczeń. Wprowadź poświadczenia dla konta usługi, którego używasz. To konto usługi powinno być kontem partnerskim z odpowiednimi uprawnieniami.

3. Skopiuj wartość tokenu odświeżania.

    ```powershell
    $token.RefreshToken | clip
    ```

Wartość tokenu odświeżania należy przechowywać w bezpiecznym repozytorium, takim jak Azure Key Vault. Aby uzyskać więcej informacji na temat korzystania z bezpiecznego modułu aplikacji za pomocą programu PowerShell, zobacz artykuł dotyczący usługi [uwierzytelniania wieloskładnikowego](/powershell/partnercenter/multi-factor-auth) .
