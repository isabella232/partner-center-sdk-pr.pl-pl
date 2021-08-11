---
title: Zarządzanie wypłatami przy użyciu interfejsu API usługi Wypłaty
description: Dowiedz się, jak używać interfejsu API Partner Center Wypłaty w celu uzyskiwania dostępu do danych wypłat
ms.date: 06/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: jasongroce
ms.author: sabaja
ms.openlocfilehash: b9bdc6da64a79f4f35466fb62662b086a8e1ab3cadc99c7ca685303752f9d166
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996332"
---
# <a name="manage-payouts-using-the-payout-service-api"></a>Zarządzanie wypłatami przy użyciu interfejsu API usługi Wypłaty

W tym artykule wyjaśniono, jak uzyskać dostęp do danych wypłat za pośrednictwem interfejsów API usługi Wypłaty zamiast interfejsu Partner Center użytkownika. Te interfejsy API zapewniają programowy sposób zapewnienia możliwości funkcji eksportowania danych [w](https://partner.microsoft.com/dashboard/payouts/reports/incentiveexport) Partner Center.

## <a name="available-apis"></a>Dostępne interfejsy API

Zobacz wszystkie dostępne interfejsy API na [stronie Wypłaty partnerów.](/rest/api/partner-center/partner-payouts)

## <a name="prerequisites"></a>Wymagania wstępne

- [Zarejestruj aplikację przy użyciu usługi AAD/tożsamości firmy Microsoft](/graph/auth-register-app-v2) w Azure Portal aplikacji i dodaj do aplikacji odpowiednich właścicieli i role.
- Zainstaluj [Visual Studio](https://visualstudio.microsoft.com/downloads/).

## <a name="register-an-application-with-the-microsoft-identity-platform"></a>Rejestrowanie aplikacji za pomocą platformy tożsamości firmy Microsoft

Usługa Platforma tożsamości Microsoft pomaga tworzyć aplikacje, do których użytkownicy i klienci mogą logować się przy użyciu tożsamości firmy Microsoft lub kont społecznościowych, [oraz](/azure/active-directory/develop/v2-overview) zapewniać autoryzowany dostęp do własnych interfejsów API lub interfejsów API firmy Microsoft, takich jak microsoft Graph.

1. Zaloguj się do [witryny Azure Portal](https://portal.azure.com/) przy użyciu służbowego lub osobistego konta Microsoft.

   Jeśli Twoje konto zapewnia dostęp do więcej niż jednej dzierżawy, wybierz swoje konto w prawym górnym rogu i ustaw sesję portalu na poprawną dzierżawę usługi Azure AD.

2. W okienku nawigacji po lewej stronie wybierz usługę Azure Active Directory, a następnie wybierz **Rejestracje aplikacji**, a następnie pozycję **Nowa rejestracja.** Zostanie **wyświetlona strona Rejestrowanie** aplikacji.

   :::image type="content" source="./images/manage-payouts/new-app-registration.png" alt-text="Zrzut ekranu przedstawiający ekran Rejestrowanie aplikacji w Azure Portal.":::

3. Wprowadź informacje dotyczące rejestracji aplikacji:

   - Nazwa: wprowadź znaczącą nazwę aplikacji, która będzie wyświetlana użytkownikom aplikacji.
   - Obsługiwane typy kont: wybierz konta, które będą obsługiwane przez aplikację.

    | **Obsługiwane typy kont**                             | **Opis**                                                                                            |
    |---------------------------------------------------------|------------------------------------------------------------------------------------------------------------|
    | Tylko konta w tym katalogu organizacyjnym          | Wybierz tę opcję, jeśli kompilujesz aplikację biznesową. Ta opcja nie jest dostępna, jeśli aplikacja nie jest rejestrowana w katalogu. Ta opcja mapuje do usługi Azure AD tylko aplikację jednodostępną.  Ta opcja jest opcją domyślną, chyba że rejestrujesz aplikację poza katalogiem. W przypadkach, gdy aplikacja jest rejestrowana poza katalogiem, wartość domyślna to aplikacja wielodostępna usługi Azure AD i konta osobiste Microsoft.             |
    | Konta w dowolnym katalogu organizacyjnym                | Wybierz tę opcję, jeśli aplikacja jest przeznaczona dla wszystkich klientów biznesowych i edukacyjnych.  Ta opcja mapuje do usługi Azure AD tylko aplikację wielodostępną. Jeśli aplikacja jest zarejestrowana w usłudze Azure AD jako jednodostępna, możesz ją zaktualizować do aplikacji wielodostępnej usługi Azure AD i z powrotem za pomocą bloku Uwierzytelnianie.                                                                                                                                                  |
    | Konta w dowolnym katalogu organizacyjnym i konta osobiste Microsoft | Wybierz tę opcję, aby przeznaczyć aplikację dla najszerszego możliwego grona klientów. Ta opcja mapuje do usługi Azure AD aplikację wielodostępną i konta osobiste Microsoft.  Jeśli aplikacja została zarejestrowana jako wielodostępne i osobiste konta Microsoft usługi Azure AD, nie można zmienić tego wyboru w interfejsie użytkownika. Zamiast tego musisz użyć edytora manifestu aplikacji, aby zmienić obsługiwane typy konta.                                                                          |

   - *(opcjonalnie)* Redirect URI (Adres URI przekierowania): wybierz typ budowania aplikacji, Internet lub klient publiczny (aplikacja mobilna & Desktop), a następnie wprowadź adres URI przekierowania (lub adres URL odpowiedzi) dla aplikacji. (Adres URL przekierowania to miejsce, w którym odpowiedź na uwierzytelnianie zostanie wysłana po uwierzytelnieniu użytkownika). 

      W przypadku aplikacji internetowej podaj podstawowy adres URL aplikacji. Na przykład ciąg `http://localhost:31544` może być adresem URL aplikacji internetowej uruchomionej na komputerze lokalnym. Użytkownicy mogą użyć tego adresu URL, aby zalogować się do aplikacji klienta internetowego.
      W przypadku publicznych aplikacji klienckich podaj identyfikator URI używany przez usługę Azure AD do zwracania odpowiedzi tokenu. Podaj wartość specyficzną dla Twojej aplikacji, np. `myapp://auth`.

4. Wybierz pozycję **Zarejestruj**. Usługa Azure AD przypisuje unikatowy identyfikator aplikacji (klienta) do aplikacji, a strona przeglądu aplikacji jest ładowana.

   :::image type="content" source="./images/manage-payouts/register-an-application.png" alt-text="<tekst alternatywny>":::

5. Jeśli chcesz dodać możliwości do aplikacji, możesz wybrać inne opcje konfiguracji, takie jak znakowanie, certyfikaty i wpisy tajne, uprawnienia interfejsu API i inne.

## <a name="platform-specific-properties"></a>Właściwości specyficzne dla platformy

W poniższej tabeli przedstawiono właściwości, które należy skonfigurować i skopiować dla różnych rodzajów aplikacji. **Przypisano** oznacza, że należy użyć wartości przypisanej przez usługę Azure AD.

| Typ aplikacji              | Platforma | Identyfikator aplikacji (klienta) | Klucz tajny klienta | Redirect URI/URL | Niejawne Flow                                                         |
|-----------------------|----------|-------------------------|---------------|------------------|-----------------------------------------------------------------------|
| Natywne/mobilne         | Natywna   | Przypisane                | Nie            | Przypisane         | Nie                                                                    |
| Aplikacja internetowa               | Internet      | Przypisane                | Tak           | Tak              | Opcjonalne rozwiązanie Open ID Połączenie pośredniczące domyślnie używa przepływu hybrydowego (Tak) |
| Aplikacja jednostronicowa (SPA) | Internet      | Przypisane                | Tak           | Tak              | Tak, spA używają funkcji Open ID Połączenie niejawnych Flow                            |
| Usługa/demon        | Internet      | Przypisane                | Tak           | Tak              | Nie                                                                    |

## <a name="create-a-service-principal"></a>Tworzenie nazwy głównej usługi

Aby uzyskać dostęp do zasobów w ramach subskrypcji, musisz przypisać rolę do aplikacji. Aby uzyskać pomoc przy wyborze roli, która oferuje odpowiednie uprawnienia dla aplikacji, zobacz [Wbudowane role platformy Azure.](/azure/role-based-access-control/built-in-roles)

> [!NOTE]
> Zakres można ustawić na poziomie subskrypcji, grupy zasobów lub zasobu. Uprawnienia są dziedziczone do niższych poziomów zakresu. Na przykład dodanie aplikacji do roli Czytelnik dla grupy zasobów oznacza, że może odczytywać grupę zasobów i wszystkie zasoby, które zawiera.

1. W Azure Portal wybierz poziom zakresu, do których chcesz przypisać aplikację. Aby na przykład przypisać rolę w zakresie subskrypcji, wyszukaj i wybierz pozycję Subskrypcje lub wybierz pozycję Subskrypcje **na** stronie głównej.

   :::image type="content" source="./images/manage-payouts/search-for-subscriptions.png" alt-text="Zrzut ekranu przedstawiający wyszukiwanie na ekranie Subskrypcje.":::

2. Wybierz subskrypcję, do których chcesz przypisać aplikację.

   :::image type="content" source="./images/manage-payouts/internal-testing-subscription.png" alt-text="Zrzut ekranu przedstawiający ekran Subskrypcje z flagą testowania wewnętrznego ustawioną na wartość true.":::

> [!NOTE]
> Jeśli nie widzisz subskrypcji, której szukasz, wybierz globalny filtr subskrypcji i upewnij się, że wybrano subskrypcję dla portalu.

3. Wybierz opcję **Kontrola dostępu (IAM)**, a następnie wybierz opcję **Dodaj przypisanie roli**.

4. Wybierz rolę, którą chcesz przypisać do aplikacji. Aby na przykład zezwolić aplikacji na wykonywanie akcji, takich jak ponowne uruchomienie, uruchamianie i zatrzymywanie wystąpień, wybierz rolę Współautor. Przeczytaj więcej na [temat dostępnych ról.](/azure/role-based-access-control/built-in-roles)

   Domyślnie aplikacje usługi Azure AD nie są wyświetlane w dostępnych opcjach. Aby znaleźć aplikację, wyszukaj nazwę i wybierz ją z wyników. Na poniższym zrzucie ekranu widać zarejestrowaną aplikację usługi `example-app` AAD.

   :::image type="content" source="./images/manage-payouts/add-role-assignment.png" alt-text="Zrzut ekranu przedstawiający interfejs użytkownika do dodawania przypisania roli dla aplikacji testowej.":::

5. Wybierz pozycję **Zapisz**. Następnie aplikacja będzie wyświetlona na liście użytkowników z rolą dla tego zakresu.

   Możesz rozpocząć używanie jednostki usługi do uruchamiania skryptów lub aplikacji. Aby zarządzać uprawnieniami jednostki usługi, zobacz stan zgody użytkownika, przejrzyj uprawnienia, zobacz informacje dotyczące logowania i nie tylko), wyświetl swoje aplikacje Enterprise w Azure Portal [.](https://portal.azure.com)

## <a name="set-up-api-permissions"></a>Konfigurowanie uprawnień interfejsu API

Ta sekcja zawiera instrukcje dotyczące sposobu skonfigurowania wymaganych uprawnień interfejsu API. Aby uzyskać więcej informacji na temat konfigurowania Partner Center interfejsu API, zobacz [interfejs API Partner uwierzytelniania.](/partner/develop/api-authentication)

**Udzielanie uprawnień do interfejsu API Graph API**

1. Otwórz [Rejestracje aplikacji](https://go.microsoft.com/fwlink/?linkid=2083908) w Azure Portal.

2. Wybierz aplikację lub [utwórz aplikację,](/azure/active-directory/develop/quickstart-register-app) jeśli jeszcze jej nie masz.

3. Na stronie Przegląd aplikacji w obszarze Zarządzanie wybierz pozycję **Uprawnienia interfejsu API,** **a następnie pozycję Dodaj uprawnienie.**

4. Wybierz **pozycję Microsoft Graph** z listy dostępnych interfejsów API.

5. Wybierz **pozycję Uprawnienia delegowane** i dodaj wymagane uprawnienia. Aby uzyskać więcej informacji, zobacz [Konfigurowanie dostępu do aplikacji.](/azure/active-directory/develop/quickstart-configure-app-access-web-apis)

   :::image type="content" source="./images/manage-payouts/graph-request-api-permissions.png" alt-text="Zrzut ekranu przedstawiający ekran uprawnień żądania w witrynie Azure Portal z wybraną Graph Microsoft.":::

**Zgoda na dostęp interfejsu API do Partner Center API za pośrednictwem aplikacji usługi AAD**

6. W przypadku aplikacji wybierz pozycję Uprawnienia interfejsu **API,** **a** następnie na ekranie Żądanie uprawnień interfejsu API wybierz pozycję Dodaj uprawnienie, a następnie interfejsy API używane przez **moją organizację.**

7. Wyszukaj interfejs API partnera firmy **Microsoft (Microsoft Centrum deweloperów) (4990cffe-04e8-4e8b-808a-1175604b879f).**

   :::image type="content" source="./images/manage-payouts/partner-api-request-permissions.png" alt-text="Zrzut ekranu przedstawiający ekran uprawnień interfejsu API z wybranym partnerem firmy Microsoft.":::

8. Ustaw uprawnienia delegowane na **wartość Partner Center**.

   :::image type="content" source="./images/manage-payouts/partner-api-request-permissions.png" alt-text="Zrzut ekranu przedstawiający uprawnienia delegowane wybrane dla Partner Center na ekranie Żądanie uprawnień interfejsu API.":::

9. Przyznaj **zgodę administratora** dla interfejsów API.

   :::image type="content" source="./images/manage-payouts/api-permissions.png" alt-text="Zrzut ekranu przedstawiający przełącznik zgody administratora na ekranie uprawnień interfejsu API.":::

   Sprawdź, czy na ekranie Stan zgody administratora jest włączona zgoda administratora.

   :::image type="content" source="./images/manage-payouts/admin-consent-verification.png" alt-text="Zrzut ekranu przedstawiający ekran stanu zgody administratora":::

10. W sekcji **Uwierzytelnianie** upewnij się, że opcja **Zezwalaj na publiczne** przepływy klienta jest ustawiona na **wartość Tak.**

    :::image type="content" source="./images/manage-payouts/allow-public-client-flows.png" alt-text="Zrzut ekranu przedstawiający ekran uwierzytelnianie z ustawieniem Zezwalaj na publiczne przepływy klienta na wartość Tak.":::

## <a name="run-the-sample-code-in-visual-studio"></a>Uruchom przykładowy kod w Visual Studio

Przykładowy kod przedstawiający sposób, w jaki interfejs API może być używany do płatności i historii transakcji, można znaleźć w centrum partnerskim — [interfejsy API](https://github.com/microsoft/Partner-Center-Payout-APIs) wypłat GitHub repo.

### <a name="sample-code-notes"></a>Uwagi dotyczące przykładowego kodu

- Konfiguracja wpisów tajnych i certyfikatów klienta, zgodnie z omówieniem w sekcji [Uwierzytelnianie:](/azure/active-directory/develop/howto-create-service-principal-portal) dwie opcje w sekcji Jak utworzyć jednostkę usługi w Azure Portal nie jest wymagana.
- Konta z uwierzytelnianiem wieloskładnikowym (MFA) nie są obecnie obsługiwane i spowodują błąd.
- Interfejs API wypłat obsługuje tylko poświadczenia użytkownika/hasła.

## <a name="next-steps"></a>Następne kroki

- [używanie portalu do tworzenia aplikacji usługi Azure AD i jednostki usługi w celu uzyskiwania dostępu do zasobów](/azure/active-directory/develop/howto-create-service-principal-portal)
- [Rejestrowanie aplikacji za pomocą platformy tożsamości firmy Microsoft](/graph/auth-register-app-v2)
- [Konfigurowanie aplikacji klienckiej w celu uzyskiwania dostępu do internetowego interfejsu API](/azure/active-directory/develop/quickstart-configure-app-access-web-apis)
