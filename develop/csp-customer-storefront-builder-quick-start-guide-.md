---
title: Konstruktor witryn sklepu internetowego klienta CSP — podręcznik Szybki start
description: Utwórz witrynę online Marketplace, aby sprzedawać oferty dostawcy rozwiązań w chmurze (CSP) za pomocą konstruktora aplikacji dostawcy usług kryptograficznych.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d64deff9b002b861c9f48d076feb5841af727e3d
ms.sourcegitcommit: 57620e249e218edc4af7c83c2ce8a3008a4adf4e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/04/2020
ms.locfileid: "97768013"
---
# <a name="csp-customer-storefront-builder-quick-start-guide"></a>Konstruktor witryn sklepu internetowego klienta CSP — podręcznik Szybki start

**Dotyczy:**

- Centrum partnerskie

Utwórz witrynę online Marketplace, aby sprzedawać oferty dostawcy rozwiązań w chmurze (CSP), korzystając z konstruktora w sklepie dla klientów programu CSP.

## <a name="introduction-to-the-csp-customer-storefront-builder"></a>Wprowadzenie do konstruktora w sklepie dla klientów programu CSP

Konstruktor sklepu w sklepie dostawcy usług kryptograficznych pomaga partnerom w łatwym tworzeniu rynku online do sprzedaży ofert dostawcy usług kryptograficznych dla klientów. Większość partnerów i małe organizacje sprzedaży chcą skupić się na sprzedawaniu, a nie na projektowaniu portalu online. Przykładowa aplikacja zestawu SDK Centrum partnerskiego wymaga umiejętności programowania oprogramowania do tworzenia i wdrażania witryny sieci Web. Korzystając z konstruktora witryny dostawcy usług kryptograficznych, można szybko i łatwo tworzyć własną witrynę sieci Web. Możesz również pobrać witrynę internetową jako przykładowy kod lub wdrożyć ją bezpośrednio w ramach subskrypcji platformy Azure za pomocą gotowej do transakcyjnej witryny sieci Web.

Ta witryna sieci Web jest w pełni własnością, obsługiwana i utrzymywana przez partnerów, a firma Microsoft nie zbiera żadnych danych ani telemetrii z witryny sieci Web. Konstruktor sklepu z klientami programu CSP tworzy witrynę sieci Web dla partnera, który jest w pełni zgodny z [standardem Payment Card Industry Data Security](https://www.pcisecuritystandards.org/) (PCI DSS).

Kod konstruktora witryny dostawcy usług kryptograficznych klienta jest objęty licencją dostępną w [umowie EULA centrum partnera SDK](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK).

>[!NOTE]
>Użytkownik jest odpowiedzialny za zarządzanie witryną sieci Web, konserwację i wszelkie problemy, które mogą wynikać z tworzenia witryny sieci Web. Przeczytaj i zapoznaj się z warunkami w [umowie licencyjnej dotyczącej zestawu SDK Centrum partnerskiego](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK).

Aby uzyskać dodatkowe informacje, zobacz również następujące artykuły: [dostawca usług w sieci Web klienta CSP](csp-customer-web-storefront.md) i [aplikacja testowa konsoli](console-test-app.md).

## <a name="considerations"></a>Zagadnienia do rozważenia

Konstruktor sklepu w sklepie dostawcy usług kryptograficznych jest przeznaczony do szybkiego tworzenia witryny sieci Web. Podczas planowania należy pamiętać o następujących kwestiach:

- Po wdrożeniu firma Microsoft i centrum partnerskie nie przechowują kopii witryny sieci Web partnera ani dowolnych informacji dodanych do programu CSP Customer w sklepie w sklepie.

- W centrum partnerskim można wdrożyć tylko witrynę sieci Web w sklepie dostawcy usług kryptograficznych w ramach subskrypcji platformy Azure partnera.

- Ta witryna internetowa, po wdrożeniu, jest w pełni własnością i zarządzana przez partnera. Firma Microsoft nie ma dostępu do tej witryny sieci Web ani żadnych danych związanych z witryną sieci Web. Partnerzy są odpowiedzialni za konserwację i zarządzanie witryną sieci Web. Firma Microsoft nie będzie udostępniać żadnej aktywnej witryny sieci Web ani innej pomocy technicznej związanej z konstruktorem aplikacji dostawcy usług kryptograficznych lub dowolnej witryny sieci Web utworzonej przy użyciu konstruktora usług w sklepie dla klientów.

- Centrum partnerskie nie może bezpośrednio uzyskać dostępu do tej witryny sieci Web ani jej uaktualnić przy użyciu nowych lub zmienionych funkcji zestawu SDK lub interfejsu API Wszystkie nowe funkcje i ulepszenia muszą być własnością, opracowana i zarządzana przez partnerów, w tym dodanie nowego zestawu SDK lub funkcji interfejsu API Centrum partnerskiego.

- Ten konstruktor sklepu w sklepie dla klientów CSP umożliwia obecnie Konfigurowanie płatności na koncie PayPal Pro/PayU Money (dla Indii). Jeśli partnerzy muszą zmienić procesor płatniczy, muszą zmienić kod w celu zapewnienia obsługi preferowanej metody płatności.

- Wszelkie informacje dotyczące płatności dodane w konstruktorze sklepu w sklepie dostawcy CSP nie są przechowywane ani utrzymywane w centrum partnerskim.

- Konfiguracja płatności w systemie PayPal będzie działała w dowolnym lokalizacje geograficzne, w którym jest dostępna system PayPal. Dostępność i pomoc techniczna w systemie PayPal są wyłącznie kontrolowane przez system PayPal i mogą być w dowolnym momencie wycofane w systemie PayPal.

- Konfiguracja płatności PayU będzie działała tylko w Indiach. PayU dostępność i pomoc techniczna są kontrolowane wyłącznie przez PayU i mogą być wycofane w dowolnym momencie przez PayU.

- Przeczytaj i zapoznaj się z warunkami w [umowie licencyjnej dotyczącej zestawu SDK Centrum partnerskiego](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK).

## <a name="using-the-csp-customer-storefront-builder"></a>Korzystanie z konstruktora witryny Customer w sklepie dostawcy CSP

Administratorzy partnerów programu CSP w centrum partnerskim mogą wdrożyć sklep dostawcy usług kryptograficznych bezpośrednio w centrum partnerskim. Przy minimalnym wysiłku można wdrożyć nową witrynę sieci Web w dzierżawie partnera. Po wdrożeniu partnerzy mogą skorzystać z witryny sieci Web, aby skonfigurować znakowanie, oferty i informacje związane z płatnością, a następnie udostępnić adres URL witryny sieci Web klientom.

Proces tworzenia witryny sieci Web w witrynie sklepu:

1. [Wdrażanie witryny internetowej](#deploy)

2. [Konfigurowanie witryny sklepu](#configure)

3. [Usługa Transact w witrynie sklepu](#transact)

### <a name="deploy"></a>Wdróż

Opcje wdrożenia:

- Pobierz [przykładowy kod sklepu Centrum partnerskiego](https://github.com/Microsoft/Partner-Center-Storefront) z usługi GitHub
- Integracja z platformą Azure w celu wdrożenia skonfigurowanej witryny sieci Web
- Wdróż w istniejącej subskrypcji lub Przenieś własną subskrypcję

### <a name="configure"></a>Konfigurowanie

W celu dostosowania witryny sklepu nie są wymagane żadne umiejętności programistyczne.

Zaloguj się przy użyciu poświadczeń administratora Centrum partnerskiego, aby skonfigurować:

- **Znakowanie**: Nazwa firmy, logo, kontakty i inne.

- **Oferty**: Wyświetl wszystkie oferty dostawcy usług kryptograficznych. Możesz wybrać, które oferty mogą wyświetlać i kupować klienci. Możesz również spersonalizować informacje o ofercie i dodać swoją cenę.

- **Konfiguracja płatności PayPal**: Dodaj informacje o koncie płatności w systemie PayPal. Jeśli nie masz konta w systemie PayPal, możesz odwiedzać [https://www.paypal.com](https://www.paypal.com) i utworzyć nowe konto. To konto będzie używane w systemie PayPal do kredytowania płatności dokonywanych przez klientów. *Firma Microsoft nie ponosi odpowiedzialności za relacje między partnerami a firmą PayPal. Korzystanie z systemu PayPal może wymagać od klientów partnerskich lub partnerskich zgody na dodatkowe warunki.*

- (*Dla Indii*) **PayU**: Dodaj informacje o koncie płatności pieniężnych PayU. Jeśli nie masz konta w usłudze PayU Money, możesz odwiedzać [https://www.payumoney.com/](https://www.payumoney.com/) i utworzyć nowe konto. To konto będzie używane na potrzeby PayU do kredytowania płatności dokonywanych przez klientów. *Firma Microsoft nie ponosi odpowiedzialności za relacje między partnerami i PayU. Użycie PayU może wymagać od klientów partnerskich lub partnerskich zgody na dodatkowe warunki.*

### <a name="transact"></a>Transakcja

- Po wdrożeniu klienci mogą od razu zakupić i Transact.

- Klienci mogą kupować bezpośrednio z portalu partnerskiego zintegrowanego z zestawem SDK Centrum partnerskiego.

#### <a name="customer-countries"></a>Kraje klienta

Klienci mogą należeć do następujących krajów:

| Kod kraju | Nazwa kraju   |
|--------------|----------------|
| AU           | Australia      |
| AT           | Austria        |
| BE           | Belgia        |
| BG           | Bułgaria       |
| CA           | Kanada         |
| HR           | Chorwacja        |
| CY           | Cypr         |
| CZ           | Republika Czeska |
| DK           | Dania        |
| EE           | Estonia        |
| FI           | Finlandia        |
| PW           | Francja         |
| DE           | Niemcy        |
| GR           | Grecja         |
| HU           | Węgry        |
| IS           | Islandia        |
| IN           | Indie          |
| IE           | Irlandia        |
| IT           | Włochy          |
| JP           | Japonia          |
| LV           | Łotwa         |
| LI           | Liechtenstein  |
| LT           | Litwa      |
| LU           | Luksemburg     |
| MT           | Malta          |
| MC           | Monako         |
| NL           | Holandia    |
| NZ           | Nowa Zelandia    |
| NO           | Norwegia         |
| Nagłówek           | Polska         |
| PT           | Portugalia       |
| RO           | Rumunia        |
| SK           | Słowacja       |
| SL           | Słowenia       |
| ES           | Hiszpania          |
| SE           | Szwecja         |
| CH           | Szwajcaria    |
| GB           | Zjednoczone Królestwo |
| USA           | Stany Zjednoczone  |

## <a name="partner-experience-scenarios"></a>Scenariusze środowiska partnerskiego

### <a name="deployment-scenario"></a>Scenariusz wdrożenia

Aby wdrożyć ulepszony lub dostosowany sklep dostawcy usług kryptograficznych:

- Pobierz [przykładowy kod sklepu Centrum partnerskiego](https://github.com/Microsoft/Partner-Center-Storefront) , aby wprowadzić dodatkowe dostosowania.

- Użyj Microsoft Visual Studio 2015 (lub nowszego) do opracowania.

- Kompiluj dodatkowe zmiany i udoskonalenia (w tym autoryzacje, certyfikaty, zmiany manifestu i inne elementy).

### <a name="configuration-scenario"></a>Scenariusz konfiguracji

- Nowo utworzona witryna sieci Web jest połączona z dzierżawcą partnera i ma dostęp do wszystkich kont administratorów tej dzierżawy partnerskiej.

  - Partnerzy mogą zalogować się do tej nowej witryny sieci Web przy użyciu poświadczeń administratora Centrum partnerskiego.

- Aplikacja dla sklepu obsługuje obecnie język francuski, hiszpański, holenderski, niemiecki, japoński i angielski. (Angielski służy jako język rezerwowy).

  - Witryna sklepu konfiguruje ustawienia regionalne przy użyciu domyślnych ustawień regionalnych partnera z poziomu profilu partnera w centrum partnerskim. Te ustawienia regionalne służą do konfigurowania walut, formatów dat i zlokalizowanych ofert w repozytorium.

- Partnerzy mogą konfigurować informacje o płatnościach znakowania, oferty oraz PayPal lub PayU (na potrzeby Indii).

- Partnerzy mogą zaktualizować nazwę firmy, logo firmy, obraz nagłówka, kontakty sprzedaży i pomocy technicznej itd.

- Partnerzy mogą zobaczyć wszystkie oferty CSP dostępne na ich terytorium.

  - Partnerzy mogą wybrać, które oferty mają być widoczne dla wszystkich klientów.

  - Partner CSP może wybrać jedną lub więcej ofert i zaktualizować nazwę, ilość, opis funkcji i cenę.
  - Cena to cena roczna. Klienci subskrybują corocznie.

- Partnerzy mogą w dowolnym momencie skonfigurować wstępnie zatwierdzone transakcje dla (a) wszystkich bieżących i przyszłych klientów lub (b) określonych klientów.

  - Wstępnie zatwierdzeni klienci nie muszą kupować w portalu, gdy dodają nowe subskrypcje, kupią dodatkowe licencje do istniejących subskrypcji lub odnówą subskrypcję.

  - Wstępnie zatwierdzeni klienci nie zostaną przekierowani do systemu PayPal lub PayU (dla Indii) w celu dokonania płatności w ramach tych transakcji.

  - Wstępnie zatwierdzone transakcje klienta umożliwiają partnerowi przeprowadzenie rozliczania i fakturowania w trybie offline dla wstępnie zatwierdzonych klientów.

- Partner programu CSP może wprowadzać swoje informacje o koncie w systemie PayPal, takie jak identyfikator klienta i wpis tajny systemu PayPal. Partner CSP może również wybrać, czy chcą testować przy użyciu piaskownicy czy konta na żywo.

  - Partnerzy mogą znaleźć te informacje [https://developer.paypal.com/](https://developer.paypal.com/) w obszarze **moje aplikacje & poświadczeniami**. Możesz również uzyskać te informacje z bieżącej aplikacji lub tworząc nową aplikację w systemie PayPal.
  - Utwórz nowe konto w systemie PayPal, jeśli jeszcze go nie masz. To konto będzie używane w systemie PayPal do kredytowania płatności dokonywanych przez klientów.

    - Aby otworzyć konto biznesowe w systemie PayPal, zobacz [https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register](https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register) .

    - Aby utworzyć konto piaskownicy w systemie PayPal, zobacz [https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/](https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/) .

- (W przypadku Indii) partner CSP może wprowadzić swoje informacje o koncie pieniężnym PayU, takie jak identyfikator klienta PayU i hasło. Partnerzy mogą znaleźć więcej informacji na temat [https://developer.payumoney.com/](https://developer.payumoney.com/) .

  - Utwórz nowe konto w usłudze PayU Money, jeśli jeszcze go nie masz. Aby otworzyć konto PayU Money, odwiedź stronę [https://www.payumoney.com/merchant-account/#/](https://www.payumoney.com/merchant-account/#/) . To konto będzie używane na potrzeby PayU do kredytowania płatności dokonywanych przez klientów.

## <a name="customer-experience-scenarios"></a>Scenariusze obsługi klienta

### <a name="new-customer-sign-up-scenario"></a>Nowy scenariusz rejestracji klienta

- Domyślnie witryna sieci Web jest publicznie dostępna i pokazuje katalog partnera na stronie głównej.

- Klienci mogą teraz należeć do dużej liczby [krajów klientów](#customer-countries).

- Fokus znajduje się w regionach Europejskie Stowarzyszenie wolnego handlu (EFTA), Ameryka Północna, Japonia, Indie, Australia i Nowa Zelandia.
  - Ta funkcja używa obsługi autoryzacji regionalnej w zestawie SDK Centrum partnerskiego.

- Klienci mogą wybrać ofertę z katalogu do zakupu.
  - Mogą oni dodawać nazwy klientów, adresy i informacje dotyczące domeny.

- Klienci będą kierowani do środowiska wyewidencjonowywania w systemie PayPal lub PayU (dla Indii). Klienci mogą podawać płatność przy użyciu:
  - Istniejące konto PayPal lub PayU (dla Indii)
  - Instrumenty finansowania obsługiwane w ich krajach przez system PayPal lub PayU (dla Indii). Mogą to być karty kredytowe, karty debetowe i konta bankowe.

- Dla tego klienta zostanie utworzona dzierżawa klienta. Po pomyślnym utworzeniu zamówienia dzierżawy klienci otrzymają szczegółowe informacje o nazwie użytkownika, haśle i subskrypcji konta.
  - Klienci mogą zapisać nazwę użytkownika i hasło, aby zalogować się do dalszych zakupów.
  - Każda subskrypcja została zakupiona przez rok, a klienci mogą odnowić w ciągu 30 dni przed datą zakończenia subskrypcji.

### <a name="view-prior-purchases-scenario"></a>Wyświetl scenariusz wcześniejszych zakupów

- Klient loguje się przy użyciu nazwy użytkownika i hasła dzierżawy klienta i przechodzi do sekcji **My Orders (moje zamówienia** ).

- Klienci mogą przejść do strony **moje zamówienia** , gdzie mogą wyświetlać zakupione subskrypcje i wprowadzać aktualizacje w razie potrzeby.

- Klienci mogą przejść do strony **Moje subskrypcje** , na której mogą wyświetlać wszystkie subskrypcje (oparte na licencjach i oparte na użyciu), w tym te utrzymywane w centrum partnerskim.

### <a name="add-licenses-to-existing-subscriptions-scenario"></a>Scenariusz dodawania licencji do istniejących subskrypcji

- W sekcji **My Orders** klienci mogą dodawać więcej licencji do istniejących subskrypcji. Klienci mogą dodawać więcej licencji w dowolnym momencie w roku subskrypcji.

- Każda dodana licencja nie zmienia daty zakończenia subskrypcji. Jednak cena subskrypcji zmienia się w zależności od daty dodania licencji i miejsca, w którym ta data przypada w roku. Cena jest naliczana proporcjonalnie do liczby dni, które są naliczane proporcjonalnie do pozostałego dnia roku.

### <a name="add-more-subscriptions-scenario"></a>Scenariusz dodawania kolejnych subskrypcji

- Klienci mogą w dowolnym momencie zakupić dowolną liczbę subskrypcji w sekcji **Dodawanie subskrypcji** w obszarze **moje zamówienia**.

- Klient może wybrać subskrypcję, dodać ilość i uregulować, aby zakończyć transakcję i od razu zacząć korzystać z subskrypcji. Jeśli klient jest wstępnie zatwierdzonym klientem, subskrypcja będzie dostępna do użytku natychmiast, a faktura zostanie wysłana do klienta w celu dokonania płatności.

### <a name="renew-subscription-scenario"></a>Scenariusz odnawiania subskrypcji

- Klient może odnowić subskrypcję w ciągu ostatnich 30 dni przed datą zakończenia subskrypcji.

- Ta wartość jest dostępna tylko w ciągu ostatnich 30 dni.

- Jeśli nie zostanie odnowiony w ciągu ostatnich 30 dni, subskrypcja zostanie usunięta z listy subskrypcji dla tej dzierżawy klienta.

- Nie można zaktualizować ilości podczas odnawiania.

### <a name="payments-scenario"></a>Scenariusz płatności

- Jeśli klient jest wstępnie zatwierdzony dla transakcji przez administratora, w powyższych scenariuszach nie jest prezentowane środowisko płatnicze. Zamiast tego partner może wysłać fakturę za płatność do wstępnie zatwierdzonego klienta.

- W przypadku wszystkich nowych zakupów możesz dodać więcej licencji, dodać subskrypcje i odnowić. Klient może uiścić partnera przy użyciu tej witryny sieci Web za pośrednictwem systemu PayPal lub PayU (dla Indii).

- Ta witryna sieci Web jest zintegrowana z systemem PayPal lub PayU (dla Indii) i umożliwia partnerom akceptowanie płatności od klientów. W przypadku systemu PayPal lub PayU (dla Indii) kredyt ma tę kwotę na koncie partnera. Zarządzanie kontami w systemie PayPal lub PayU (dla Indii) jest poza tą witryną sieci Web i jest zarządzane odpowiednio na PayPal.com lub PayUmoney.com.

- Jest to zależne od partnerów konfigurujących konfigurację płatności w systemie PayPal orPayU (dla Indii) w PayPal.com lub PayUmoney.com. Firma Microsoft nie zapisuje tych informacji ani faktycznych transakcji płatniczych wynikających z użycia tej opcji.

### <a name="prorated-pricing-scenario"></a>Scenariusz cen ze proporcjonalną opłatą

- Ta witryna internetowa obsługuje ceny ze proporcjonalną opłatą w przypadku, gdy klienci dodają więcej licencji do istniejącej subskrypcji.

- Każda subskrypcja wygasa po upływie roku i nie można jej zmienić po zakupie subskrypcji.

- Data zakończenia subskrypcji nie ulegnie zmianie przez dodanie dodatkowych licencji. Klienci będą obciążani za pozostałą liczbę dni do daty zakończenia. Jeśli na przykład na dzień jest naliczana opłata za subskrypcję $365 i zostanie dodana co najmniej jedna licencja na dwa dni, Cena nowej licencji wynosi $364. W przypadku dodania kolejnej licencji 10 dni później cena będzie $354.
