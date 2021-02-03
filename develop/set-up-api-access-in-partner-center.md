---
title: Konfigurowanie dostępu do interfejsu API w Centrum partnerskim
description: Skonfiguruj konta do tworzenia w porównaniu z zestawem SDK Centrum partnerskiego i test w piaskownicy integracji.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 873ff2ff9cecbfa92429958d3bfe2aa79fc3ad9a
ms.sourcegitcommit: d5de47c08ba661ba5de4935caa6843d7c2c91710
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/28/2020
ms.locfileid: "97768153"
---
# <a name="set-up-api-access-in-partner-center"></a>Konfigurowanie dostępu do interfejsu API w Centrum partnerskim

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie Microsoft Cloud for US Government
- Centrum partnerskie dla Microsoft Cloud Niemcy

W tym artykule opisano konta, które należy opracować względem zestawu SDK Centrum partnerskiego. W tym artykule opisano również sposób tworzenia [konta piaskownicy integracji](#integration-sandbox-account) i testowania w piaskownicy integracji.

>[!NOTE]
>Aby uzyskać dostęp do interfejsów API, dzierżawca musi być dzierżawcą dostawcy usług kryptograficznych i musi być dostawcą pośrednim lub bezpośrednim partnerem rozliczeniowym.

## <a name="account-definitions"></a>Definicje kont

Aby ułatwić integrację i testowanie integracji interfejsu API, centrum partnerskie obsługuje dwa rodzaje kont:

### <a name="primary-partner-account"></a>Główne konto partnerskie

To konto służy do tworzenia rzeczywistych zamówień dla rzeczywistych klientów. Jeśli wprowadzisz jakiekolwiek zmiany lub transakcje po zalogowaniu się na koncie podstawowym przy użyciu zestawu SDK Centrum partnerskiego lub interfejsu użytkownika pulpitu nawigacyjnego partnera, będą one traktowane jako oficjalne zamówienia dla rzeczywistych klientów. Zostaną one odzwierciedlone na fakturze, a firma jest odpowiedzialna za płatność za nie.

### <a name="integration-sandbox-account"></a>Konto piaskownicy integracji

To konto służy do testowania kodu i jego integracji z interfejsem API Centrum partnerskiego przed jego wdrożeniem. Zmiany i transakcje wprowadzone po zalogowaniu się do konta piaskownicy integracji zostaną wyświetlone na fakturze, ale nie musisz uiszczać kwoty faktury. Plik PDF faktury będzie miał oświadczenie "nie płacisz". TO JEST FAKTURA PIASKOWNICY, A ŻADNA AKCJA NIE JEST WYMAGANA.

Konto piaskownicy integracji i konto podstawowe działają niezależnie i nie udostępniają kont administratorów, kont użytkowników, klientów, zamówień, subskrypcji ani innych danych.

Piaskownica integracji obsługuje transakcje z ograniczoną liczbą klientów, zamówień, subskrypcji, licencji itd.

Zgodnie z zasadami konta piaskownicy integracji służą wyłącznie do celów testowania integracji.

Konto piaskownicy integracji nie istnieje domyślnie. Jeśli planujesz używać zestawu SDK Centrum partnerskiego, musisz utworzyć go samodzielnie.

## <a name="set-up-your-accounts"></a>Konfigurowanie kont

W tej sekcji opisano sposób konfigurowania konta partnera podstawowego i konta piaskownicy integracji dla zestawu SDK Centrum partnerskiego.

### <a name="create-an-integration-sandbox"></a>Tworzenie piaskownicy integracji

1. Zaloguj się do pulpitu nawigacyjnego partnera przy użyciu konta administratora globalnego (konta głównego partnera).

2. Z menu **Ustawienia** (ikona koła zębatego) wybierz pozycję **Ustawienia partnera**.

3. Wybierz kartę **piaskownica integracji** .

    >[!NOTE]
    >Jeśli nie widzisz opcji piaskownicy integracji, być może nie masz konta administratora globalnego. Może być również używane konto piaskownicy integracji i piaskownica integracji została już skonfigurowana.

4. Wprowadź informacje kontaktowe dla konta administratora piaskownicy integracji. Następnie wybierz pozycję **Utwórz konto**. Poczekaj kilka minut, aż zostanie wyświetlony komunikat z potwierdzeniem, że konto zostało utworzone.

5. Po wyświetleniu komunikatu potwierdzenia Wyloguj się z pulpitu nawigacyjnego partnera.

6. Zaloguj się ponownie przy użyciu nowego konta administratora piaskownicy integracji. Upewnij się, że używasz formatu **username@domain** poświadczeń oraz hasła, które zostało określone.

7. Wybierz pozycję **Skonfiguruj konto** powyżej **bieżących zadań** , aby zakończyć konfigurację konta piaskownicy.

### <a name="enable-api-access"></a>Włącz dostęp do interfejsu API

Po skonfigurowaniu konta należy włączyć dostęp do interfejsu API, aby można było używać zestawu SDK centrum partnerskiego z piaskownicą integracji. Należy włączyć dostęp do interfejsu API oddzielnie dla podstawowego konta partnera i dla konta piaskownicy integracji.

1. Zaloguj się do pulpitu nawigacyjnego partnera przy użyciu konta administratora globalnego.

2. Z menu **Ustawienia** (ikona koła zębatego) wybierz pozycję **Ustawienia partnera**.

3. Na stronie **Ustawienia konta** wybierz pozycję **Zarządzanie aplikacjami**.

4. Jeśli nie masz jeszcze istniejącej aplikacji, Dodaj nową aplikację sieci Web. Jeśli masz istniejącą aplikację sieci Web, wybierz przycisk **Dodaj klucz** .

5. Skopiuj informacje o rejestracji aplikacji, zwłaszcza w **przypadku tworzenia** aplikacji sieci Web i przechowywania ich w bezpiecznym miejscu.

6. Wyloguj się z pulpitu nawigacyjnego partnera.

7. Zaloguj się ponownie przy użyciu konta piaskownicy integracji. Powtórz kroki 2-5, aby włączyć dostęp do interfejsu API w piaskownicy integracji.

## <a name="write-and-test-code"></a>Napisz i Testuj kod

Kod i kod testowy można napisać w piaskownicy integracji. Aby [skonfigurować uwierzytelnianie Centrum partnerskiego](partner-center-authentication.md) za pomocą usługi Azure AD, potrzebne są poniższe informacje.

| Nazwa elementu | Lokalizacja elementu |
| --------- | ------------- |
| Identyfikator aplikacji/klienta | Z menu **Ustawienia** (ikona koła zębatego) wybierz pozycję **Ustawienia partnera**. Na stronie **Ustawienia konta** wybierz pozycję **Zarządzanie aplikacjami**. Identyfikator aplikacji lub identyfikator klienta jest wyświetlany jako **zarejestrowany identyfikator aplikacji aplikacji**. |
| Klucz | Jeśli aplikacja sieci Web została utworzona w sekcji [Włączanie dostępu do interfejsu API](#enable-api-access), jest to klucz zapisany w kroku 5. |
| Domena | Domena piaskownicy integracji. |

## <a name="run-tested-code"></a>Uruchom testowany kod

Aby korzystać z rozwiązania z rzeczywistymi danymi klienta, musisz zmienić poświadczenia usługi piaskownicy integracji na swoje poświadczenia głównego konta partnera.

Gdy wszystko będzie gotowe do użycia przetestowanego kodu na podstawowym koncie partnerskim, musisz uzyskać token zabezpieczający usługi Azure AD. Ten token zabezpieczający jest oparty na aplikacji Centrum partnerskiego, klucz i domenę (zamiast aplikacji piaskownicy integracji, klucza i domeny).

1. Postępuj zgodnie z instrukcjami w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md) , aby uzyskać token zabezpieczający usługi Azure AD przy użyciu poświadczeń podstawowego Centrum partnerskiego. (Wcześniej zostały wykonane następujące kroki, aby uzyskać token zabezpieczający usługi Azure AD dla piaskownicy integracji).

2. Zastąp token Security Integration w kodzie nowym tokenem zabezpieczającym dla głównego konta partnera.
