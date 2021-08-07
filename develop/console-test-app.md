---
title: Aplikacja testowa konsoli
description: Ta aplikacja testowa konsoli zawiera przykładowy kod dla wszystkich scenariuszy obsługiwanych przez Partner Center API. Można go również używać do testowania.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 53a014608303e432be251de0845857547170a5464a1952bb4fde9ff7beb8ae95
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991960"
---
# <a name="console-test-app"></a>Aplikacja testowa konsoli

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Aplikacja testowa konsoli jest udostępniana w językach C# i Java. Udostępnia przykładowe kody dla wszystkich scenariuszy obsługiwanych przez interfejsy API Partner Center API. Można go również używać do testowania.

## <a name="get-the-code"></a>Uzyskiwanie kodu

Pobierz przykładowy kod dla aplikacji testowej konsoli.

## <a name="net"></a>.NET

[Pobierz przykładowy kod i](https://go.microsoft.com/fwlink/p/?LinkId=746682) zmodyfikuj go w razie potrzeby.

> [!IMPORTANT]
> Przed skompilowanie aplikacji zaktualizuj wartości w pliku *App.config,* aby odzwierciedlały informacje o uwierzytelnianiu usługi Azure AD utworzone podczas [Partner Center uwierzytelniania.](partner-center-authentication.md) W szczególności należy używać ustawień konta piaskownicy integracji na wczesnym etapie opracowywania lub do testowania w środowisku produkcyjnym.

W **obszarze ScenarioSettings** w *App.config* pliku można ustawić parametry, które będą automatycznie przekazywane do uruchamianych scenariuszy.

Aby zmodyfikować listę uruchamianych scenariuszy, wyeksmentuj wiersze w scenariuszu **IPartnerScenario \[ \] mainScenarios** lub w indywidualnej metodzie **Get Scenarios** znalezionej w *pliku Program.cs.*

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[Pobierz przykładowy kod i](https://go.microsoft.com/fwlink/p/?LinkId=2026887) zmodyfikuj go w razie potrzeby.

> [!IMPORTANT]
> Przed skompilowanie aplikacji zaktualizuj wartości w pliku *SamplesConfigurations.jsw* celu odzwierciedlenia informacji o uwierzytelnianiu usługi Azure AD utworzonych podczas [Partner Center uwierzytelniania.](partner-center-authentication.md) W szczególności należy używać ustawień konta piaskownicy integracji na wczesnym etapie opracowywania lub do testowania w środowisku produkcyjnym.

W **obszarze ScenarioSettings** SamplesConfiguration.js *pliku* można ustawić parametry, które będą automatycznie przekazywane do uruchamianych scenariuszy.

Aby zmodyfikować listę uruchamianych scenariuszy, należy oznaczać jako komentarz wiersze w scenariuszu **IPartnerScenario \[ \] mainScenarios** lub w poszczególnych metodach Get **Scenarios** znalezionych w *pliku Program.java.*

## <a name="what-to-change"></a>Co należy zmienić

Użyj poniższych list, aby określić, co należy zmienić w przykładowym kodzie.

### <a name="partnerservicesettings"></a>PartnerServiceSettings

W **przypadku ustawienia PartnerServiceSettings** nie zmieniaj:

- **PartnerServiceApiEndpoint**
- **AuthenticationAuthorityEndpoint**
- **GraphEndpoint**
- **CommonDomain**

Wszystkie te ustawienia są niezbędne do prawidłowego działania przykładowych wywołań interfejsu API.

### <a name="userauthentication"></a>UserAuthentication

W **przypadku uwierzytelniania użytkownika** wymagana jest zmiana:

- **ApplicationId** (identyfikator Azure Active Directory używany do logowania)
- **UserName** (nazwa użytkownika usługi Active Directory)
- **Hasło** (hasło usługi Active Directory).

Nie zmieniaj:

- **Adres_Url_Zasobu**
- **RedirectUrl**

### <a name="appauthentication"></a>AppAuthentication

W **przypadku uwierzytelniania appauthentication** należy zmienić:

- **ApplicationId** (identyfikator aplikacji usługi Active Directory używany do logowania do aplikacji)
- **ApplicationSecret** (klucz tajny aplikacji usługi Active Directory używany do logowania do aplikacji)
- **Domena** (domena usługi Active Directory, w której jest hostowana aplikacja)

### <a name="scenariosettings"></a>ScenarioSettings

W **przypadku ustawienia ScenarioSettings** nie zmieniaj:

- **CustomerDomainSuffix** (sufiks domeny używany podczas tworzenia nowego klienta)

Ustawienia opcjonalne. W przypadku pozostawionych pustych informacji należy wprowadzić te informacje podczas uruchamiania scenariusza w razie potrzeby):

- **CustomerIdToDelete** (identyfikator klienta użyty do usunięcia)
- **DefaultCustomerId** (identyfikator klienta do użycia w scenariuszach związanych z klientem)
- **DefaultInvoiceID** (identyfikator faktury do użycia w scenariuszach faktur)
- **PartnerMpnId** (identyfikator MPN partnera do użycia w scenariuszach partnerów pośrednich)
- **DefaultServiceRequestId** (identyfikator żądania obsługi do użycia w scenariuszach żądania obsługi)
- **DefaultSupportTopicID** (identyfikator tematu pomocy technicznej do użycia w scenariuszach żądania obsługi)
- **DefaultOfferID** (identyfikator oferty do użycia w scenariuszach oferty)
- **DefaultOrderID** (identyfikator zamówienia do użycia w scenariuszach kolejności)
- **DefaultSubscriptionID** (identyfikator subskrypcji do użycia w scenariuszach subskrypcji)

Opcjonalnie można zmienić. Wszystkie te ustawienia określają liczbę wpisów na stronie podczas pobierania zawartości stronicowej:

- **CustomerPageSize**
- **InvoicePageSize**
- **ServiceRequestPageSize**
- **DefaultOfferPageSize**
- **SubscriptionPageSize**
