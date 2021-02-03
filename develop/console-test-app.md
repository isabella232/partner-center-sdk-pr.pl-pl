---
title: Aplikacja testowa konsoli
description: Ta aplikacja testowa konsoli udostępnia przykładowy kod dla wszystkich scenariuszy obsługiwanych przez interfejsy API Centrum partnerskiego. Można go również użyć do testowania.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e82bac3ccc22d0e7cf898e5b2d2e002c622584ae
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767994"
---
# <a name="console-test-app"></a>Aplikacja testowa konsoli

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Aplikacja testowa konsoli dostępna w języku C# i Java zawiera przykładowe kody dla wszystkich scenariuszy obsługiwanych przez interfejsy API Centrum partnerskiego. Można go również użyć do testowania.

## <a name="get-the-code"></a>Uzyskiwanie kodu

Pobierz przykładowy kod dla aplikacji testowej konsoli.

## <a name="net"></a>.NET

[Pobierz przykładowy kod](https://go.microsoft.com/fwlink/p/?LinkId=746682) i zmodyfikuj go w razie potrzeby.

> [!IMPORTANT]
> Przed skompilowaniem aplikacji należy zaktualizować wartości w pliku *App.config* w celu odzwierciedlenia informacji o uwierzytelnianiu usługi Azure AD utworzonych w ramach uwierzytelniania w usłudze [Partner Center](partner-center-authentication.md). W szczególnych przypadkach należy używać ustawień konta piaskownicy integracji podczas wczesnego opracowywania lub testowania w środowisku produkcyjnym.

W obszarze **ScenarioSettings** w pliku *App.config* można ustawić parametry, które będą automatycznie przesyłane do wykonywanych scenariuszy.

Aby zmodyfikować listę uruchomionych scenariuszy, należy dodać komentarz do wierszy w **IPartnerScenario \[ \] mainScenarios** lub w poszczególnych metodach **Get scenariusze** znalezionych w pliku *program.cs* .

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[Pobierz przykładowy kod](https://go.microsoft.com/fwlink/p/?LinkId=2026887) i zmodyfikuj go w razie potrzeby.

> [!IMPORTANT]
> Przed skompilowaniem aplikacji należy zaktualizować wartości w *SamplesConfigurations.jsw* pliku, aby odzwierciedlić informacje o uwierzytelnianiu usługi Azure AD utworzone w ramach uwierzytelniania w usłudze [Partner Center](partner-center-authentication.md). W szczególnych przypadkach należy używać ustawień konta piaskownicy integracji podczas wczesnego opracowywania lub testowania w środowisku produkcyjnym.

W obszarze **ScenarioSettings** w pliku *SamplesConfiguration.js* , można ustawić parametry, które będą automatycznie przesyłane do wykonywanych scenariuszy.

Aby zmodyfikować listę scenariuszy, które są uruchamiane, Dodaj komentarz do wierszy w **IPartnerScenario \[ \] mainScenarios** lub w poszczególnych metodach **Get scenariusze** , które znajdują się w pliku *program. Java* .

## <a name="what-to-change"></a>Co należy zmienić

Użyj poniższych list, aby określić, co zmienić lub nie zmienić w przykładowym kodzie.

### <a name="partnerservicesettings"></a>PartnerServiceSettings

W przypadku **PartnerServiceSettings** nie zmieniaj:

- **PartnerServiceApiEndpoint**
- **AuthenticationAuthorityEndpoint**
- **GraphEndpoint**
- **CommonDomain**

Wszystkie te ustawienia są niezbędne, aby przykładowe wywołania interfejsu API działały prawidłowo.

### <a name="userauthentication"></a>UserAuthentication

W przypadku **UserAuthentication** wymagane jest zmianę:

- Identyfikator **aplikacji (Azure Active Directory** używany do logowania)
- **Nazwa użytkownika** (nazwa użytkownika usługi Active Directory)
- **Hasło** (hasło usługi Active Directory).

Nie zmieniaj:

- **Adres_Url_Zasobu**
- **RedirectUrl**

### <a name="appauthentication"></a>AppAuthentication

W przypadku **AppAuthentication** wymagane jest zmianę:

- Aplikacja **(identyfikator** aplikacji usługi Active Directory używany do logowania aplikacji)
- **ApplicationSecret** (klucz tajny aplikacji usługi Active Directory używany do logowania aplikacji)
- **Domena** (domena usługi Active Directory, na której jest hostowana aplikacja)

### <a name="scenariosettings"></a>ScenarioSettings

W przypadku **ScenarioSettings** nie zmieniaj:

- **CustomerDomainSuffix** (sufiks domeny używany podczas tworzenia nowego klienta)

Ustawienia opcjonalne. Jeśli pole pozostanie puste, te informacje będą musiały zostać zwrócone podczas uruchamiania scenariusza, w razie potrzeby):

- **CustomerIdToDelete** (identyfikator klienta używany do usuwania)
- **DefaultCustomerId** (identyfikator klienta do użycia w scenariuszach związanych z klientem)
- **DefaultInvoiceID** (Identyfikator faktury do użycia w scenariuszach faktur)
- **PartnerMpnId** (identyfikator MPN partnera, który ma być używany w scenariuszach partnera pośredniego)
- **DefaultServiceRequestId** (Identyfikator żądania obsługi, który ma być używany w scenariuszach żądania obsługi)
- **DefaultSupportTopicID** (identyfikator tematu pomocy technicznej, który ma być używany w scenariuszach żądania obsługi)
- **DefaultOfferID** (identyfikator oferty do użycia w scenariuszach oferty)
- **DefaultOrderID** (Identyfikator zamówienia do użycia w scenariuszach w kolejności)
- **DefaultSubscriptionID** (Identyfikator subskrypcji do użycia w scenariuszach subskrypcji)

Opcjonalne, aby zmienić. Wszystkie te ustawienia określają liczbę wpisów na stronie podczas pobierania zawartości stronicowanej:

- **CustomerPageSize**
- **InvoicePageSize**
- **ServiceRequestPageSize**
- **DefaultOfferPageSize**
- **SubscriptionPageSize**
