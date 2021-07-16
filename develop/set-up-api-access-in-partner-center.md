---
title: Konfigurowanie dostępu do interfejsu API w Centrum partnerskim
description: Skonfiguruj konta do testowania na zestaw SDK Centrum partnerskiego i testowania w piaskownicy integracji.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: db7d9bba34abadc907910c68c4a5583ed1f530f4
ms.sourcegitcommit: de1e68545d37d7fa1862788f7fa8c84a9c4f2795
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/16/2021
ms.locfileid: "114282103"
---
# <a name="set-up-api-access-in-partner-center"></a>Konfigurowanie dostępu do interfejsu API w Centrum partnerskim

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center dla Microsoft Cloud for US Government | Partner Center for Microsoft Cloud Germany

W tym artykule opisano konta, które należy opracować w zestaw SDK Centrum partnerskiego. W tym artykule wyjaśniono również, jak utworzyć konto piaskownicy [integracji i](#integration-sandbox-account) przetestować je w piaskownicy integracji.

>[!NOTE]
>Aby uzyskać dostęp do interfejsów API, dzierżawa musi być dzierżawą dostawcy usług w chmurze i musisz być dostawcą pośrednim lub partnerem z rozliczeniami bezpośrednimi.

## <a name="account-definitions"></a>Definicje kont

Aby ułatwić integrację i testowanie integracji interfejsu API, Partner Center obsługuje dwa rodzaje kont:

### <a name="primary-partner-account"></a>Konto podstawowego partnera

To konto umożliwia tworzenie rzeczywistych zamówień dla rzeczywistych klientów. Jeśli po zalogowaniu się na konto podstawowe zostaną wprowadzone jakiekolwiek zmiany lub transakcje przy użyciu interfejsu użytkownika pulpitu nawigacyjnego partnera lub usługi zestaw SDK Centrum partnerskiego, będą one traktowane jako oficjalne zamówienia dla rzeczywistych klientów. Zostaną one odzwierciedlone na fakturze, a Twoja firma jest odpowiedzialna za ich opłacenie.

### <a name="integration-sandbox-account"></a>Konto piaskownicy integracji

To konto jest do testowania kodu i jego integracji z interfejsami API Partner Center przed szerokim wdrożeniem. Zmiany i transakcje wprowadzone po zalogowaniu się do konta piaskownicy integracji pojawią się na fakturze, jednak nie trzeba płacić kwoty faktury. Faktura w formacie PDF będzie mieć zastrzeżenia "NIE PŁAĆ. JEST TO FAKTURA PIASKOWNICY I NIE JEST WYMAGANA ŻADNA AKCJA".

Konto piaskownicy integracji i konto podstawowe działają niezależnie i nie współdzielą kont administratorów, kont użytkowników, klientów, zamówień, subskrypcji ani innych danych.

Piaskownica integracji obsługuje transakcje z ograniczoną liczbą klientów, zamówień, subskrypcji, licencji itp.

Według zasad konta piaskownicy integracji są tylko do celów testowania integracji.

Konto piaskownicy integracji nie istnieje domyślnie. Musisz utworzyć go samodzielnie, jeśli zamierzasz używać zestaw SDK Centrum partnerskiego.

## <a name="set-up-your-accounts"></a>Konfigurowanie kont

W tej sekcji opisano sposób skonfigurowania podstawowego konta partnera i konta piaskownicy integracji dla zestaw SDK Centrum partnerskiego.

### <a name="create-an-integration-sandbox"></a>Tworzenie piaskownicy integracji

1. Zaloguj się do pulpitu nawigacyjnego partnera przy użyciu konta administratora globalnego (podstawowego konta partnera).

2. W menu **Ustawienia** (ikona koła zębatego) wybierz **pozycję Ustawienia konta.**

3. Wybierz **kartę Piaskownica integracji.**

    >[!NOTE]
    >Jeśli nie widzisz opcji Piaskownica integracji, możesz nie mieć konta administratora globalnego. Być może korzystasz również z konta piaskownicy integracji, a piaskownica integracji została już ustawiona.

4. Wprowadź informacje kontaktowe dla konta administratora piaskownicy integracji. Następnie wybierz pozycję **Utwórz konto.** Poczekaj kilka minut na komunikat potwierdzający, że konto zostało utworzone.

5. Po wyświetleniu komunikatu z potwierdzeniem wyloguj się z pulpitu nawigacyjnego partnera.

6. Zaloguj się ponownie przy użyciu nowego konta administratora piaskownicy integracji. Upewnij się, że używasz **username@domain** formatu swoich poświadczeń wraz z określonym hasłem.

7. Wybierz **pozycję Skonfiguruj konto powyżej** **bieżącego zadania,** aby ukończyć konfigurowanie konta piaskownicy.

### <a name="enable-api-access"></a>Włączanie dostępu do interfejsu API

Po skonfigurowaniu konta należy włączyć dostęp do interfejsu API, aby można było używać zestawu SDK centrum partnerskiego z piaskownicą integracji. Należy włączyć dostęp do interfejsu API oddzielnie dla podstawowego konta partnera i dla konta piaskownicy integracji.

1. Zaloguj się do pulpitu nawigacyjnego partnera przy użyciu konta administratora globalnego.

2. W menu **Ustawienia** (ikona koła zębatego) wybierz **pozycję Ustawienia konta.**

3. Na stronie **Ustawienia konta** wybierz pozycję **Zarządzanie aplikacją.**

4. Jeśli nie masz jeszcze istniejącej aplikacji, dodaj nową aplikację internetową. Jeśli masz istniejącą aplikację internetową, wybierz **przycisk Dodaj** klucz.

5. Skopiuj informacje o rejestracji  aplikacji, zwłaszcza klucz, jeśli tworzysz aplikację internetową, i przechowuj ją w bezpiecznym miejscu.

6. Wyloguj się z pulpitu nawigacyjnego partnera.

7. Zaloguj się ponownie przy użyciu konta piaskownicy integracji. Powtórz kroki 2–5, aby włączyć dostęp do interfejsu API w piaskownicy integracji.

## <a name="write-and-test-code"></a>Pisanie i testowanie kodu

Kod i kod testowy można napisać w piaskownicy integracji. Poniższe informacje są potrzebne do skonfigurowania uwierzytelniania Partner Center [usłudze](partner-center-authentication.md) Azure AD.

| Nazwa elementu | Lokalizacja elementu |
| --------- | ------------- |
| Identyfikator aplikacji/identyfikator klienta | W menu **Ustawienia** (ikona koła zębatego) wybierz **pozycję Ustawienia konta.** Na stronie **Ustawienia konta** wybierz pozycję **Zarządzanie aplikacją.** Identyfikator aplikacji/identyfikator klienta jest wymieniony jako **identyfikator zarejestrowanej aplikacji.** |
| Klucz | Jeśli aplikacja internetowa została utworzona w sekcji Włączanie dostępu [do interfejsu API](#enable-api-access), jest to klucz zapisany w kroku 5. |
| Domena | Domena piaskownicy integracji. |

## <a name="run-tested-code"></a>Uruchamianie przetestowanych kodów

Aby korzystać z rozwiązania z rzeczywistymi danymi klienta, należy zmienić poświadczenia piaskownicy integracji na poświadczenia podstawowego konta partnera.

Gdy wszystko będzie gotowe do użycia przetestowanych kodów na podstawowym koncie partnera, musisz uzyskać token zabezpieczający usługi Azure AD. Ten token zabezpieczający jest oparty na Partner Center, kluczu i domenie (zamiast aplikacji, klucza i domeny piaskownicy integracji).

1. Postępuj zgodnie z instrukcjami [Partner Center uwierzytelniania,](partner-center-authentication.md) aby uzyskać token zabezpieczający usługi Azure AD przy użyciu poświadczeń Partner Center podstawowego. (Wcześniej zostały one opisane w celu uzyskania tokenu zabezpieczającego usługi Azure AD dla piaskownicy integracji).

2. Zastąp token zabezpieczeń integracji w kodzie nowym tokenem zabezpieczającym dla podstawowego konta partnera.
