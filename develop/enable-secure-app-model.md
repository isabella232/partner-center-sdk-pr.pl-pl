---
title: Włączanie modelu aplikacji zabezpieczonych
description: Zabezpieczanie aplikacji Partner Center panelu sterowania.
ms.date: 01/20/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 19a1c39576a4f897df2d1205e3501839f6580831
ms.sourcegitcommit: e0077b2724d128ab20cb05696e5e5b1cde8e5214
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/07/2021
ms.locfileid: "113481671"
---
# <a name="enabling-the-secure-application-model-framework"></a>Włączanie środowiska modelu aplikacji zabezpieczonej

Firma Microsoft wprowadza bezpieczną, skalowalną platformę do uwierzytelniania partnerów dostawców rozwiązań w chmurze (CSP) i dostawców panelu sterowania (CPV) za pośrednictwem architektury Microsoft Azure Active Directory Multi-Factor Authentication (MFA).

Nowy model umożliwia podnieść poziom zabezpieczeń dla wywołań integracji Partner Center API. Pomoże to wszystkim stronom (w tym partnerom firmy Microsoft, partnerom programu CSP i cpv) chronić ich infrastrukturę i dane klientów przed zagrożeniami bezpieczeństwa.

## <a name="scope"></a>Zakres

Ten artykuł dotyczy następujących aktorów:

- Dostawcy oprogramowania panelu sterowania
  - Dostawca oprogramowania panelu sterowania (CPV) to niezależny dostawca oprogramowania, który opracowuje aplikacje, których partnerzy CSP mogą używać do integracji z interfejsami API Centrum partnerskiego.
  - Dostawca CPV nie jest partnerem CSP z bezpośrednim dostępem do pulpitu nawigacyjnego lub interfejsów API Centrum partnerskiego.

- Dostawcy pośredni dostawcy usług w chmurze i bezpośredni partnerzy dostawcy usług w chmurze, którzy używający identyfikatora aplikacji i uwierzytelniania użytkowników oraz bezpośrednio integrują się z Partner Center API.

## <a name="security-requirements"></a>Wymagania dotyczące zabezpieczeń

Aby uzyskać szczegółowe informacje na temat wymagań dotyczących zabezpieczeń, zobacz [Partner Security Requirements (Wymagania dotyczące zabezpieczeń partnerów).](/partner-center/partner-security-requirements)

## <a name="secure-application-model"></a>model aplikacji zabezpieczonych

Aplikacje z witryny Marketplace muszą personifikować uprawnienia partnera CSP w celu wywołania interfejsów API firmy Microsoft. Ataki na zabezpieczenia tych poufnych aplikacji mogą prowadzić do naruszenia bezpieczeństwa danych klientów.

Aby uzyskać omówienie i szczegóły nowej struktury uwierzytelniania, pobierz dokument [model aplikacji zabezpieczonych framework.](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) Ten dokument zawiera zasady i najlepsze rozwiązania, dzięki których aplikacje na platformie handlowej będą zrównoważone i odporne na naruszenia zabezpieczeń.

## <a name="samples"></a>Samples

W następujących dokumentach z omówieniem i przykładowym kodzie opisano, jak partnerzy mogą wdrożyć model aplikacji zabezpieczonych platformę:

- [Dokument z omówieniem protokołu CPV](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [Dokument z omówieniem programu CSP](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [Przykłady dla oprogramowania .NET](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [Przykłady dla języka Java](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [Instrukcje i przykłady DOTYCZĄCE REST](#rest)
- [Instrukcje i przykłady dotyczące programu PowerShell](#powershell)

## <a name="rest"></a>REST

Aby wykonać wywołania REST za pomocą struktury model aplikacji zabezpieczonych z przykładowym kodem, wykonaj następujące kroki:

1. [Tworzenie aplikacji internetowej](#create-a-web-app)

2. [Uzyskiwanie kodu autoryzacji](#get-authorization-code)

3. [Uzyskiwanie tokenu odświeżania](#get-refresh-token)

4. [Pobranie tokenu dostępu](#get-access-token)

5. [Wykonywanie wywołania interfejsu API Centrum partnerskiego](#make-partner-center-api-calls)

> [!TIP]
> Możesz użyć modułu Partner Center PowerShell, aby uzyskać kod autoryzacji i token odświeżania. Tę opcję można wybrać w miejsce kroków 2 i 3. Aby uzyskać więcej informacji, zobacz [sekcję programu PowerShell i przykłady](#powershell).

### <a name="create-a-web-app"></a>Tworzenie aplikacji internetowej

Przed wykonaniem wywołań REST musisz utworzyć i zarejestrować aplikację internetową w Partner Center aplikacji internetowej.

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).

2. Tworzenie aplikacji Azure Active Directory (Azure AD).

3. Nadaj delegowanym aplikacjom uprawnienia do następujących zasobów, *w zależności od wymagań aplikacji.* W razie potrzeby można dodać więcej delegowanych uprawnień dla zasobów aplikacji.

   1. **Microsoft Partner Center** (niektóre dzierżawy pokazują to jako **SampleBECApp**)

   2. **Interfejsy API usługi Azure Management** (jeśli planujesz wywołać interfejsy API platformy Azure)

   3. **Windows Azure Active Directory**

4. Upewnij się, że adres URL strony głównej aplikacji jest ustawiony na punkt końcowy, w którym działa żywa aplikacja internetowa. Ta aplikacja będzie musiała zaakceptować kod [autoryzacji z](#get-authorization-code) wywołania logowania usługi Azure AD. Na przykład w przykładowym kodzie w [poniższej sekcji](#get-authorization-code)aplikacja internetowa działa pod następującym kodem: `https://localhost:44395/` .

5. Zwróć uwagę na następujące informacje z ustawień aplikacji internetowej w usłudze Azure AD:

   - Identyfikator aplikacji
   - Klucz tajny aplikacji

> [!NOTE]
> Zaleca się używanie [certyfikatu jako tajnego certyfikatu aplikacji.](/azure/active-directory/develop/active-directory-certificate-credentials) Można jednak również utworzyć klucz aplikacji w Azure Portal. Przykładowy kod w [poniższej sekcji](#get-authorization-code) używa klucza aplikacji.

### <a name="get-authorization-code"></a>Uzyskiwanie kodu autoryzacji

Musisz uzyskać kod autoryzacji aplikacji internetowej do zaakceptowania z wywołania logowania usługi Azure AD:

1. Zaloguj się do usługi Azure AD pod następującym adresem URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) . Pamiętaj, aby zalogować się przy użyciu konta użytkownika, z którego będą Partner Center interfejsu API (na przykład agenta administracyjnego lub konta agenta sprzedaży).

2. Zastąp **identyfikator Application-Id** identyfikatorem aplikacji usługi Azure AD (IDENTYFIKATOR GUID).

3. Po wyświetleniu monitu zaloguj się przy użyciu konta użytkownika ze skonfigurowanym uwierzytelniania wieloskładnikowego.

4. Po wyświetleniu monitu wprowadź dodatkowe informacje dotyczące usługi MFA (numer telefonu lub adres e-mail), aby zweryfikować logowanie.

5. Po zalogowaniu przeglądarka przekieruje wywołanie do punktu końcowego aplikacji internetowej przy użyciu kodu autoryzacji. Na przykład poniższy przykładowy kod przekierowuje `https://localhost:44395/` do .

#### <a name="authorization-code-call-trace"></a>Śledzenie wywołania kodu autoryzacji

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

### <a name="get-refresh-token"></a>Uzyskiwanie tokenu odświeżania

Następnie należy użyć kodu autoryzacji, aby uzyskać token odświeżania:

1. Wywołanie POST do punktu końcowego logowania usługi Azure AD `https://login.microsoftonline.com/CSPTenantID/oauth2/token` przy użyciu kodu autoryzacji. Aby uzyskać przykład, zobacz następujące [przykładowe wywołanie .](#sample-refresh-call)

2. Zanotuj zwrócony token odświeżania.

3. Token odświeżania należy przechowywać w Azure Key Vault. Aby uzyskać więcej informacji, zobacz [dokumentację Key Vault API.](/rest/api/keyvault/)

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

### <a name="get-access-token"></a>Uzyskiwanie tokenu dostępu

Aby można było wykonać wywołania do interfejsów API usługi Partner Center, należy uzyskać token dostępu. Aby uzyskać token dostępu, należy użyć tokenu odświeżania, ponieważ tokeny dostępu zazwyczaj mają bardzo ograniczony okres istnienia (na przykład mniej niż godzinę).

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

### <a name="make-partner-center-api-calls"></a>Wywołania Partner Center API

Należy użyć tokenu dostępu, aby wywołać interfejsy PARTNER CENTER API. Zobacz następujące przykładowe wywołanie.

#### <a name="example-partner-center-api-call"></a>Przykład wywołania Partner Center API

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Możesz użyć modułu [Partner Center PowerShell,](https://www.powershellgallery.com/packages/PartnerCenter) aby zmniejszyć wymaganą infrastrukturę do wymiany kodu autoryzacji na token dostępu. Ta metoda jest opcjonalna do tworzenia [Partner Center REST](#rest).

Aby uzyskać więcej informacji na temat tego procesu, [zobacz dokumentację dotyczącą bezpiecznego model aplikacji](/powershell/partnercenter/secure-app-model) PowerShell.

1. Zainstaluj usługę Azure AD i Partner Center modułów programu PowerShell.

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. Użyj polecenia **[New-PartnerAccessToken,](/powershell/module/partnercenter/new-partneraccesstoken)** aby wykonać proces wyrażania zgody i przechwycić wymagany token odświeżania.

    ```powershell
    $credential = Get-Credential

    $token = New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > Parametr **ServicePrincipal** jest używany z poleceniem **New-PartnerAccessToken,** ponieważ jest używana aplikacja usługi Azure AD o typie **Internet/interfejs API.** Ten typ aplikacji wymaga, aby identyfikator klienta i wpis tajny były uwzględniane w żądaniu tokenu dostępu. Po **wywołaniu polecenia Get-Credential** zostanie wyświetlony monit o wprowadzenie nazwy użytkownika i hasła. Wprowadź identyfikator aplikacji jako nazwę użytkownika. Wprowadź klucz tajny aplikacji jako hasło. Po **wywołaniu polecenia New-PartnerAccessToken** zostanie ponownie wyświetlony monit o wprowadzenie poświadczeń. Wprowadź poświadczenia dla używanego konta usługi. To konto usługi powinno być kontem partnera z odpowiednimi uprawnieniami.

3. Skopiuj wartość tokenu odświeżania.

    ```powershell
    $token.RefreshToken | clip
    ```

Wartość tokenu odświeżania należy przechowywać w bezpiecznym repozytorium, takim jak Azure Key Vault. Aby uzyskać więcej informacji na temat wykorzystania modułu bezpiecznej aplikacji przy użyciu programu PowerShell, zobacz artykuł [Uwierzytelnianie wieloskładnikowe.](/powershell/partnercenter/multi-factor-auth)
