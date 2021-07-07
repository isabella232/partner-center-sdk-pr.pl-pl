---
title: Rejestrowanie szczegółów aplikacji w celu Partner Center dla chmury krajowej firmy Microsoft
description: Dowiedz się, jak i dlaczego deweloperzy aplikacji Partner Center dla chmury Microsoft National Cloud muszą zarejestrować szczegółowe informacje o swojej aplikacji w usłudze Azure AD za pośrednictwem Azure Portal.
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 93d46a17bc26e9586e5e773bdf934653a571367f
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973455"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud-through-the-azure-portal"></a>Rejestrowanie szczegółów aplikacji na Partner Center dla chmury microsoft national za pośrednictwem witryny Azure Portal

**Dotyczy:** Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Deweloperzy muszą zarejestrować szczegółowe informacje o swojej aplikacji w usłudze Azure AD za pośrednictwem Azure Portal. Dzięki temu tylko określone aplikacje będą mogły łączyć się z danymi partnera i klienta.

W Partner Center dla Microsoft Cloud for US Government obecnie musisz zarządzać aplikacjami za pomocą programu PowerShell. Aby uzyskać więcej informacji, zobacz [dokumentację Azure PowerShell dokumentacji.](/powershell/module/Azuread/#applications)

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Podczas tworzenia aplikacji dla usługi Microsoft Cloud (Niemcy) lub Partner Center for Partner Center for Microsoft Cloud for US Government należy pamiętać o następujących dodatkowych wymaganiach.

## <a name="web-apps"></a>Aplikacje internetowe

W przypadku aplikacji internetowych użyj poniższych procedur, aby zarejestrować identyfikator aplikacji.

### <a name="create-or-update-web-app"></a>Tworzenie lub aktualizowanie aplikacji internetowej

1. Przejdź do [strony Azure Portal — Rejestracje aplikacji,](https://go.microsoft.com/fwlink/?linkid=2083908) aby zarejestrować aplikację. Zaloguj się do witryny Azure Portal przy użyciu służbowego lub osobistego konta Microsoft.

2. Wybierz **pozycję Nowa rejestracja.** Aby uzyskać więcej informacji, zobacz [Szybki start: rejestrowanie aplikacji za pomocą Platforma tożsamości Microsoft](/azure/active-directory/develop/quickstart-register-app).

### <a name="configure-api-access-permissions-for-web-app"></a>Konfigurowanie uprawnień dostępu do interfejsu API dla aplikacji internetowej

1. Wybierz aplikację. Przejdź do **Ustawienia** aplikacji internetowej.

2. W **sekcji Dostęp do interfejsu API** wybierz pozycję Wymagane **uprawnienia**

3. Aby uzyskać Windows uprawnień usługi Azure Active Directory:

    1. Wybierz **Windows Azure Active Directory uprawnień.**

    2. W **uprawnienia aplikacji**, wybierz odczytu danych katalogu.

    3. Zapisz uprawnienia.

4. Zanotuj identyfikator aplikacji **w sekcji** Właściwości aplikacji internetowej.

### <a name="add-a-secret-key-to-your-app"></a>Dodawanie klucza tajnego do aplikacji

1. Przejdź do **sekcji Klucze** aplikacji internetowej.

2. Wprowadź opis klucza i wybierz czas trwania na 1 lub 2 lata, zgodnie z potrzebami.

3. Zapisz i skopiuj wartość klucza tajnego. **Ta wartość nie zostanie ponownie pokazana po opuszczeniu tej strony.**

Konfiguracja aplikacji internetowej powinna mieć następujące szczegóły:

- Identyfikator aplikacji
- Klucz tajny aplikacji

### <a name="register-the-web-app-in-partner-center"></a>Rejestrowanie aplikacji internetowej w Partner Center

1. Zaloguj się do witryny [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com).

2. Wybierz **pozycję Pulpit nawigacyjny,** a następnie **wybierz pozycję Ustawienia,** a następnie wybierz **pozycję Zarządzanie aplikacją.**

3. W sekcji **Aplikacja internetowa** wybierz pozycję **Zarejestruj istniejącą aplikację.**

4. Wybierz aplikację internetową utworzoną w Azure Portal.

5. Wybierz **pozycję Zarejestruj aplikację.**

## <a name="native-apps"></a>Aplikacje natywne

Aplikacje natywne nie muszą być zarejestrowane w Partner Center. Jednak te aplikacje należy skonfigurować tak, aby zapewniały dostęp do Partner Center API.

>[!NOTE]
>Przed utworzeniem aplikacji natywnej w Azure Portal zaloguj się do usługi Partner Center przy użyciu poświadczeń użytkownika administratora z dzierżawy partnera. Powoduje to utworzenie ustawień w dzierżawie w celu włączenia uprawnień aplikacji.

### <a name="create-native-app"></a>Tworzenie aplikacji natywnej

1. Przejdź do [strony Azure Portal — Rejestracje aplikacji,](https://go.microsoft.com/fwlink/?linkid=2083908) aby zarejestrować aplikację. Zaloguj się do witryny Azure Portal przy użyciu służbowego lub osobistego konta Microsoft.

2. Wybierz **pozycję Nowa rejestracja.** Aby uzyskać więcej informacji, zobacz [Szybki start: rejestrowanie aplikacji za pomocą Platforma tożsamości Microsoft](/azure/active-directory/develop/quickstart-register-app).

### <a name="configure-api-access-permissions-for-native-app"></a>Konfigurowanie uprawnień dostępu interfejsu API dla aplikacji natywnej

1. Wybierz aplikację. Przejdź do obszaru **Settings** (Ustawienia).

2. W dostępie do interfejsu API wybierz **pozycję Wymagane uprawnienia.**

3. Wybierz **Windows Azure Active Directory uprawnień.** W **uprawnienia delegowane**, wybierz te uprawnienia:

    - **Logowanie i odczyt profilu użytkownika**
    - **Odczyt danych katalogu**
    - **Dostęp do katalogu jako zalogowany użytkownik**
    - **Odczytywanie wszystkich grup**

4. Zapisz uprawnienia.

5. Wybierz **pozycję Dodaj** w opcji Wymagane **uprawnienia.**

6. Wybierz pozycję **Wybierz interfejs API**.

    1. W polu wyszukiwania wprowadź nazwę **Microsoft Partner Center** i wybierz ją z listy wyników.

    2. Wybierz pozycję **Wybierz**.

7. Wybierz pozycję **Wybierz uprawnienia**.

    1. Wybierz **pozycję Dostęp Partner Center PPE.**
    
    2. Wybierz pozycję **Wybierz**.

8. Wybierz pozycję **Gotowe**.

>[!IMPORTANT]
> Zanotuj identyfikator aplikacji we właściwościach aplikacji.

Nie musisz rejestrować aplikacji natywnych w Partner Center, ale aplikacja natywna musi być za zgodą administratora. Zanotuj identyfikator aplikacji natywnej.
