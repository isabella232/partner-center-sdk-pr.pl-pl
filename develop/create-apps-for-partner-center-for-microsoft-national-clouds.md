---
title: Rejestrowanie szczegółów aplikacji dla Centrum partnerskiego w chmurze krajowej firmy Microsoft
description: Dowiedz się, jak i dlaczego deweloperzy aplikacji dla Centrum partnerskiego w chmurze firmy Microsoft muszą rejestrować szczegółowe informacje o swojej aplikacji za pomocą usługi Azure AD za pomocą Azure Portal.
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 887cb71c752ac5d9c61398536711545c19cc7600
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770147"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud-through-the-azure-portal"></a>Rejestrowanie szczegółowych informacji o aplikacji dla Centrum partnerskiego w chmurze krajowej firmy Microsoft za pomocą Azure Portal

**Dotyczy:**

- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Deweloperzy muszą rejestrować szczegółowe informacje o swojej aplikacji za pomocą usługi Azure AD za pomocą Azure Portal. Pozwala to zagwarantować, że tylko określone aplikacje będą mogły łączyć się z danymi partnera i klienta.

Centrum partnerskie dla Microsoft Cloud dla instytucji rządowych USA wymaga obecnie zarządzania aplikacjami za poorednictwem programu PowerShell. Aby uzyskać więcej informacji, zobacz [dokumentację referencyjną Azure PowerShell](/powershell/module/Azuread/#applications).

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Należy pamiętać o następujących dodatkowych wymaganiach podczas tworzenia aplikacji dla Centrum partnerskiego na Microsoft Cloud Niemcy lub centrum partnerskie dla Microsoft Cloud dla instytucji rządowych USA.

## <a name="web-apps"></a>Aplikacje internetowe

W przypadku usługi Web Apps wykonaj następujące procedury, aby zarejestrować identyfikator aplikacji.

### <a name="create-or-update-web-app"></a>Utwórz lub zaktualizuj aplikację sieci Web

1. Przejdź do strony [Rejestracje aplikacji Azure Portal](https://go.microsoft.com/fwlink/?linkid=2083908) , aby zarejestrować aplikację. Zaloguj się do witryny Azure Portal przy użyciu służbowego lub osobistego konta Microsoft.

2. Wybierz pozycję **Nowa rejestracja**. Aby uzyskać więcej informacji, zobacz [Szybki Start: rejestrowanie aplikacji na platformie tożsamości firmy Microsoft](/azure/active-directory/develop/quickstart-register-app).

### <a name="configure-api-access-permissions-for-web-app"></a>Konfigurowanie uprawnień dostępu do interfejsu API dla aplikacji sieci Web

1. Wybierz aplikację. Przejdź do pozycji **Ustawienia** aplikacji sieci Web.

2. W sekcji **dostęp do interfejsu API** wybierz **wymagane uprawnienia**

3. W przypadku uprawnień usługi Windows Azure Active Directory:

    1. Wybierz **uprawnienia Azure Active Directory systemu Windows**.

    2. W obszarze **uprawnienia aplikacji** wybierz pozycję Odczytaj dane katalogu.

    3. Zapisz uprawnienia.

4. Zanotuj identyfikator aplikacji w sekcji **Właściwości** aplikacji sieci Web.

### <a name="add-a-secret-key-to-your-app"></a>Dodawanie klucza tajnego do aplikacji

1. Przejdź do sekcji **klucze** aplikacji sieci Web.

2. Wprowadź opis klucza i wybierz czas trwania w zakresie od 1 do 2 lat, zgodnie z potrzebami.

3. Zapisz i skopiuj wartość klucza tajnego. **Ta wartość nie będzie ponownie wyświetlana po opuszczeniu tej strony.**

W konfiguracji aplikacji sieci Web powinny znajdować się następujące szczegółowe informacje:

- Identyfikator aplikacji
- Klucz tajny aplikacji

### <a name="register-the-web-app-in-partner-center"></a>Rejestrowanie aplikacji sieci Web w centrum partnerskim

1. Zaloguj się do [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com) .

2. Wybierz pozycję **pulpit nawigacyjny**, a następnie wybierz pozycję **Ustawienia konta**, a następnie wybierz pozycję **Zarządzanie aplikacjami**.

3. W sekcji **aplikacja sieci Web** wybierz pozycję **zarejestruj istniejącą aplikację**.

4. Wybierz aplikację sieci Web utworzoną w Azure Portal.

5. Wybierz pozycję **zarejestruj aplikację**.

## <a name="native-apps"></a>Aplikacje natywne

Aplikacje natywne nie muszą być zarejestrowane w centrum partnerskim. Jednak te aplikacje muszą być skonfigurowane w taki sposób, aby zapewnić dostęp do interfejsów API Centrum partnerskiego.

>[!NOTE]
>Przed utworzeniem aplikacji natywnej w Azure Portal Zaloguj się do Centrum partnerskiego przy użyciu poświadczeń użytkownika administratora z dzierżawy partnerskiej. Spowoduje to utworzenie ustawień dzierżawy w celu włączenia uprawnień aplikacji.

### <a name="create-native-app"></a>Tworzenie aplikacji natywnej

1. Przejdź do strony [Rejestracje aplikacji Azure Portal](https://go.microsoft.com/fwlink/?linkid=2083908) , aby zarejestrować aplikację. Zaloguj się do witryny Azure Portal przy użyciu służbowego lub osobistego konta Microsoft.

2. Wybierz pozycję **Nowa rejestracja**. Aby uzyskać więcej informacji, zobacz [Szybki Start: rejestrowanie aplikacji na platformie tożsamości firmy Microsoft](/azure/active-directory/develop/quickstart-register-app).

### <a name="configure-api-access-permissions-for-native-app"></a>Konfigurowanie uprawnień dostępu do interfejsu API dla aplikacji natywnej

1. Wybierz aplikację. Przejdź do obszaru **Settings** (Ustawienia).

2. W obszarze dostęp do interfejsu API wybierz pozycję **wymagane uprawnienia**.

3. Wybierz **uprawnienia Azure Active Directory systemu Windows**. W obszarze **uprawnienia delegowane** wybierz następujące uprawnienia:

    - **Logowanie i odczyt profilu użytkownika**
    - **Odczyt danych katalogu**
    - **Dostęp do katalogu jako zalogowany użytkownik**
    - **Odczytuj wszystkie grupy**

4. Zapisz uprawnienia.

5. Wybierz pozycję **Dodaj** w obszarze **wymagane uprawnienia**.

6. Wybierz pozycję **Wybierz interfejs API**.

    1. W polu wyszukiwania wprowadź **Centrum partnerskie firmy Microsoft** i wybierz je z listy wyników.

    2. Wybierz pozycję **Wybierz**.

7. Wybierz pozycję **Wybierz uprawnienia**.

    1. Wybierz pozycję **Access partner centrum ŚOI**.
    
    2. Wybierz pozycję **Wybierz**.

8. Wybierz pozycję **Gotowe**.

>[!IMPORTANT]
> Zanotuj identyfikator aplikacji we właściwościach aplikacji.

Nie musisz rejestrować natywnych aplikacji w centrum partnerskim, jednak aplikacja natywna musi być zgodna z administratorem. Zanotuj identyfikator aplikacji w aplikacji natywnej.
