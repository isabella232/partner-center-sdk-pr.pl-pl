---
title: Aplikacja testowa konsoli
description: Ta aplikacja testowa konsoli zawiera przykładowy kod dla wszystkich scenariuszy obsługiwanych przez Partner Center API. Można go również używać do testowania.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b35167104deeede50107d59fca6112c10dc7b4bf
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974033"
---
# <a name="console-test-app"></a>Aplikacja testowa konsoli

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Aplikacja testowa konsoli jest dostarczana w językach C# i Java. Udostępnia przykładowe kody dla wszystkich scenariuszy obsługiwanych przez interfejsy API Partner Center Api. Można go również używać do testowania.

## <a name="get-the-code"></a>Uzyskiwanie kodu

Pobierz przykładowy kod aplikacji testowej konsoli.

## <a name="net"></a>.NET

[Pobierz przykładowy kod i](https://go.microsoft.com/fwlink/p/?LinkId=746682) zmodyfikuj go w razie potrzeby.

> [!IMPORTANT]
> Przed skompilowanie aplikacji zaktualizuj wartości w pliku *App.config,* aby odzwierciedlić informacje uwierzytelniania usługi Azure AD utworzone w ramach [Partner Center uwierzytelniania.](partner-center-authentication.md) W szczególności należy używać ustawień konta piaskownicy integracji na wczesnym etapie opracowywania lub do testowania w środowisku produkcyjnym.

W **obszarze ScenarioSettings** w *App.config* można ustawić parametry, które będą automatycznie przekazywane do uruchamianych scenariuszy.

Aby zmodyfikować listę uruchamianych scenariuszy, przekrzywij wiersze w scenariuszu **IPartnerScenario \[ \] mainScenarios** lub w indywidualnej metodzie **Get Scenarios** znalezionej w *pliku Program.cs.*

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[Pobierz przykładowy kod i](https://go.microsoft.com/fwlink/p/?LinkId=2026887) zmodyfikuj go w razie potrzeby.

> [!IMPORTANT]
> Przed skompilowanie aplikacji zaktualizuj wartości w pliku *SamplesConfigurations.jsw* celu odzwierciedlenia informacji uwierzytelniania usługi Azure AD utworzonych podczas [Partner Center uwierzytelniania.](partner-center-authentication.md) W szczególności należy używać ustawień konta piaskownicy integracji na wczesnym etapie opracowywania lub do testowania w środowisku produkcyjnym.

W **obszarze ScenarioSettings** SamplesConfiguration.js *pliku* można ustawić parametry, które będą automatycznie przekazywane do uruchamianych scenariuszy.

Aby zmodyfikować listę uruchamianych scenariuszy, przekrzywij wiersze w scenariuszu **IPartnerScenario \[ \] mainScenarios** lub w indywidualnej metodzie **Get Scenarios** znalezionej w *pliku Program.java.*

## <a name="what-to-change"></a>Co należy zmienić

Użyj poniższych list, aby określić, co należy zmienić w przykładowym kodzie.

### <a name="partnerservicesettings"></a>PartnerServiceSettings

W **przypadku usługi PartnerServiceSettings** nie zmieniaj:

- **PartnerServiceApiEndpoint**
- **AuthenticationAuthorityEndpoint**
- **GraphEndpoint**
- **CommonDomain**

Wszystkie te ustawienia są niezbędne do poprawnego działania przykładowych wywołań interfejsu API.

### <a name="userauthentication"></a>UserAuthentication

W **przypadku uwierzytelniania UserAuthentication** należy zmienić:

- **ApplicationId** (identyfikator Azure Active Directory używany do logowania)
- **UserName** (nazwa użytkownika usługi Active Directory)
- **Hasło** (hasło usługi Active Directory).

Nie zmieniaj:

- **Adres_Url_Zasobu**
- **RedirectUrl**

### <a name="appauthentication"></a>AppAuthentication

W **przypadku uwierzytelniania AppAuthentication** należy zmienić:

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
