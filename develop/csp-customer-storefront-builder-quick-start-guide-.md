---
title: Konstruktor witryn sklepu internetowego klienta CSP — podręcznik Szybki start
description: Utwórz witrynę marketplace online, aby sprzedawać oferty dostawców rozwiązań w chmurze (CSP) przy użyciu narzędzia CSP Customer Storefront Builder.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 69fe30b61d7260e4c3365d2486cec5ffadd2a3fbb39bb50158a44d8716ff2d71
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995224"
---
# <a name="csp-customer-storefront-builder-quick-start-guide"></a>Konstruktor witryn sklepu internetowego klienta CSP — podręcznik Szybki start

Utwórz witrynę marketplace online, aby sprzedawać oferty dostawców rozwiązań w chmurze (CSP) przy użyciu narzędzia CSP Customer Storefront Builder.

## <a name="introduction-to-the-csp-customer-storefront-builder"></a>Wprowadzenie do programu CSP Customer Storefront Builder

Aplikacja CSP Customer Storefront Builder ułatwia partnerom tworzenie platformy handlowej online w celu sprzedaży ofert CSP swoim klientom. Większość partnerów i małych organizacji sprzedażowych chce skupić się na sprzedaży, a nie na tworzeniu platformy handlowej online. Przykładowa zestaw SDK Centrum partnerskiego wymaga umiejętności tworzenia oprogramowania w celu utworzenia i wdrożenia witryny internetowej. Dzięki aplikacji CSP Customer Storefront Builder możesz szybko i łatwo utworzyć własną witrynę internetową. Możesz również pobrać witrynę internetową jako przykładowy kod lub wdrożyć ją bezpośrednio w subskrypcji platformy Azure za pomocą witryny internetowej Gotowe do użycia w usłudze Transact.

Ta witryna internetowa jest w pełni własnością, obsługiwana i obsługiwana przez partnerów, a firma Microsoft nie zbiera żadnych danych ani danych telemetrycznych z witryny internetowej. Program CSP Customer Storefront Builder tworzy witrynę internetową dla partnera, która jest w pełni zgodna z normą [Payment Card Industry Data Security Standard](https://www.pcisecuritystandards.org/) (PCI DSS).

Kod CSP Customer Storefront Builder podlega licencji dostępnej w zestaw SDK Centrum partnerskiego [EULA.](/legal/partner-center/eula-partner-center-sdk)

>[!NOTE]
>Użytkownik jest odpowiedzialny za zarządzanie witryną sklepu, konserwację i wszelkie problemy, które mogą wynikać z tworzenia witryny internetowej. Przeczytaj i zapoznaj się z terminami w [zestaw SDK Centrum partnerskiego EULA.](/legal/partner-center/eula-partner-center-sdk)

Aby uzyskać dodatkowe informacje, zobacz również następujące artykuły: [Witryna sklepu](csp-customer-web-storefront.md) internetowego klienta CSP i [testowa aplikacja konsolowa](console-test-app.md).

## <a name="considerations"></a>Zagadnienia do rozważenia

Program CSP Customer Storefront Builder jest przeznaczony jako szybki sposób tworzenia witryny internetowej. Podczas planowania należy wziąć pod uwagę następujące kwestie:

- Po wdrożeniu firma Microsoft i Partner Center nie utrzymują kopii witryny internetowej partnera ani żadnych informacji dodanych do aplikacji CSP Customer Storefront Builder.

- Partner Center wdrożyć witrynę internetową CSP Customer Storefront tylko w subskrypcjach platformy Azure partnera.

- Po wdrożeniu ta witryna internetowa jest w pełni własnością partnera i jest przez nie zarządzana. Firma Microsoft nie ma dostępu do tej witryny internetowej ani żadnych danych związanych z witryną internetową. Partnerzy są odpowiedzialni za konserwację witryny internetowej i zarządzanie jej witryną. Firma Microsoft nie zapewni żadnej witryny internetowej na żywo ani innej pomocy technicznej związanej z programem CSP Customer Storefront Builder ani witryną internetową utworzoną za pomocą narzędzia CSP Customer Storefront Builder.

- Partner Center bezpośrednio uzyskać dostępu do tej witryny internetowej ani uaktualnić jej za pomocą nowych lub zmienionych funkcji zestawu SDK lub interfejsu API. Wszelkie nowe funkcje lub ulepszenia muszą być własnością, opracowywane i zarządzane przez partnerów, w tym dodawać nowe funkcje zestaw SDK Centrum partnerskiego interfejsu API.

- Ten program CSP Customer Storefront Builder umożliwia obecnie konfigurowanie płatności na konto PayPal Pro/płatności za płatności (dla Indiach). Jeśli partnerzy będą musieli zmienić procesor płatności, będą musieli zmienić kod w celu obsługi preferowanej formy płatności.

- Wszelkie informacje związane z płatnościami dodane w aplikacji CSP Customer Storefront Builder nie są przechowywane ani przechowywane w Partner Center.

- PayPal konfiguracja płatności będzie działać we wszystkich lokalizacjach geograficznych, PayPal są dostępne. PayPal dostępności i pomocy technicznej jest wyłącznie kontrolowana przez PayPal i może zostać wycofana w dowolnym momencie przez PayPal.

- Konfiguracja płatności w przypadku płatności w 2018 r. będzie obecnie działać tylko w Indiach. Dostępność i pomoc techniczna w przypadku płatności w przypadku płatności (PayU) jest kontrolowana wyłącznie przez payu i może zostać wycofana w dowolnym momencie przez tę usługę.

- Przeczytaj i zapoznaj się z terminami w [zestaw SDK Centrum partnerskiego EULA.](/legal/partner-center/eula-partner-center-sdk)

## <a name="using-the-csp-customer-storefront-builder"></a>Korzystanie z narzędzia Customer Storefront Builder dla programu CSP

Administratorzy partnerów programu CSP w Partner Center mogą wdrożyć sklep klienta CSP bezpośrednio z Partner Center. Przy minimalnym nakładzie pracy można wdrożyć nową witrynę internetową w dzierżawie partnera. Po wdrożeniu partnerzy mogą za pomocą witryny internetowej skonfigurować znakowanie, oferty i informacje dotyczące płatności, a następnie udostępnić adres URL witryny internetowej klientom.

Proces tworzenia witryny internetowej sklepu ma na celu:

1. [Wdrażanie witryny internetowej](#deploy)

2. [Konfigurowanie sklepu](#configure)

3. [Transakcje w sklepie](#transact)

### <a name="deploy"></a>Wdróż

Opcje wdrażania:

- Pobierz [przykładowy kod Partner Center storefront z](https://github.com/Microsoft/Partner-Center-Storefront) GitHub
- Integracja z platformą Azure w celu wdrożenia skonfigurowanej witryny internetowej
- Wdrażanie w istniejącej subskrypcji lub przyniesienie własnej subskrypcji

### <a name="configure"></a>Konfigurowanie

Do dostosowania sklepu nie są wymagane żadne umiejętności deweloperskie.

Zaloguj się przy użyciu Partner Center administratora, aby skonfigurować:

- **Znakowanie:** nazwa firmy, logo, kontakty i inne.

- **Oferty:** wyświetl wszystkie oferty CSP. Możesz wybrać oferty, które klienci mogą wyświetlać i kupować. Możesz również spersonalizować informacje o ofercie i dodać swoją cenę.

- **PayPal konfiguracji płatności:** dodaj PayPal informacje o koncie płatności. Jeśli nie masz konta PayPal, możesz odwiedzić [https://www.paypal.com](https://www.paypal.com) i utworzyć nowe konto. To konto będzie używane do PayPal środków na płatności dokonywane przez klientów. *Firma Microsoft nie jest odpowiedzialna za relację między partnerami i PayPal. Korzystanie z PayPal może wymagać od klientów partnera lub partnera zgody na dodatkowe warunki.*

- *(Indie*) **Konfiguracja płatności w przypadku płatności w** przypadku płatności Wu: dodaj informacje o koncie płatności w przypadku płatności w UŁ. Jeśli nie masz konta payu money, możesz odwiedzić [https://www.payumoney.com/](https://www.payumoney.com/) i utworzyć nowe konto. To konto będzie używane na potrzeby płatności w ramach płatności w ramach płatności dokonywanej przez klientów. *Firma Microsoft nie jest odpowiedzialna za relację między partnerami i płatnościami. Korzystanie z płatności zgodnie z płatnościami może wymagać od klientów partnera lub partnera zgody na dodatkowe warunki.*

### <a name="transact"></a>Transakcja

- Po wdrożeniu klienci mogą natychmiast kupować i kupować transakcje.

- Klienci mogą kupować bezpośrednio z portalu dla partnerów zintegrowanego z zestaw SDK Centrum partnerskiego.

#### <a name="customer-countries"></a>Kraje klientów

Klienci mogą należeć do tych krajów:

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
| Po           | Polska         |
| PT           | Portugalia       |
| RO           | Rumunia        |
| SK           | Słowacja       |
| SL           | Słowenia       |
| ES           | Hiszpania          |
| SE           | Szwecja         |
| CH           | Szwajcaria    |
| GB           | Zjednoczone Królestwo |
| USA           | Stany Zjednoczone  |

## <a name="partner-experience-scenarios"></a>Scenariusze obsługi partnerów

### <a name="deployment-scenario"></a>Scenariusz wdrożenia

Aby wdrożyć rozszerzoną lub dostosowaną usługę CSP Customer Storefront:

- Pobierz [przykładowy kod Partner Center storefront,](https://github.com/Microsoft/Partner-Center-Storefront) aby wprowadzić dodatkowe dostosowania.

- Użyj Microsoft Visual Studio 2015 (lub nowszego).

- Twórz dodatkowe zmiany i ulepszenia (w tym autoryzacje, certyfikaty, zmiany manifestu i inne elementy).

### <a name="configuration-scenario"></a>Scenariusz konfiguracji

- Nowo utworzona witryna internetowa jest połączona z dzierżawą partnera i ma dostęp do wszystkich kont administratorów tej dzierżawy partnera.

  - Partnerzy mogą logować się do tej nowej witryny internetowej przy użyciu Partner Center poświadczeń administratora.

- Aplikacja ze sklepu obsługuje obecnie język francuski, hiszpański, holenderski, niemiecki, japoński i angielski. (Angielski służy jako język rezerwowy).

  - Sklep konfiguruje ustawienia lokalne przy użyciu domyślnych ustawień regionalnych partnera z profilu partnera w Partner Center. Te ustawienia lokalne są używane do konfigurowania walut, formatów dat i zlokalizowanych ofert w repozytorium.

- Partnerzy mogą konfigurować znakowanie, oferty i PayPal lub płatność w przypadku Indie.

- Partnerzy mogą aktualizować nazwę firmy, logo firmy, obraz nagłówka, kontakty sprzedażowe i pomocy technicznej i nie tylko.

- Partnerzy mogą zobaczyć wszystkie dostępne oferty CSP w zależności od ich terytorium.

  - Partnerzy mogą wybrać oferty, które mają być wyświetlane wszystkim klientom.

  - Partner programu CSP może wybrać co najmniej jedną ofertę i zaktualizować nazwę, ilość, opis funkcji i cenę.
  - Cena jest ceną roczną. Klienci subskrybują subskrypcję co rok.

- Partnerzy mogą w dowolnym momencie skonfigurować wstępnie zatwierdzone transakcje dla (a) wszystkich bieżących i przyszłych klientów LUB (b) określonych klientów.

  - Wstępnie zatwierdzeni klienci nie muszą płacić za portal podczas dodawania nowych subskrypcji, kupowania dodatkowych licencji do istniejących subskrypcji ani odnawiania subskrypcji.

  - Wstępnie zatwierdzeni klienci nie będą przekierowywani do PayPal płatności (dla Indiach) w celu płatności podczas tych transakcji.

  - Wstępnie zatwierdzone transakcje klientów umożliwiają partnerowi wykonywanie rozliczeń i fakturowania w trybie offline dla wstępnie zatwierdzonych klientów.

- Partner programu CSP może wprowadzić swoje PayPal konta, takie jak PayPal identyfikator klienta i klucz tajny. Partner programu CSP może również wybrać, czy chce testować przy użyciu piaskownicy, czy konta na żywo.

  - Partnerzy mogą znaleźć te informacje w [https://developer.paypal.com/](https://developer.paypal.com/) chmurze w **moich & poświadczenia.** Te informacje można również uzyskać z bieżącej aplikacji lub przez utworzenie nowej aplikacji w PayPal.
  - Utwórz nowe konto PayPal, jeśli jeszcze go nie masz. To konto będzie używane do PayPal środków na płatności dokonane przez klientów.

    - Aby otworzyć konto PayPal biznesowego, zobacz [https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register](https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register) .

    - Aby utworzyć konto PayPal piaskownicy, zobacz [https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/](https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/) .

- (Indie) Partner programu CSP może wprowadzić swoje informacje o koncie płatności zgodnie z płatnością zgodnie z potrzebami, takie jak identyfikator klienta i hasło payu. Partnerzy mogą znaleźć więcej informacji na temat [https://developer.payumoney.com/](https://developer.payumoney.com/) .

  - Utwórz nowe konto płatności za platformę PayU, jeśli jeszcze go nie masz. Aby otworzyć konto payu money, odwiedź stronę [https://www.payumoney.com/merchant-account/#/](https://www.payumoney.com/merchant-account/#/) . To konto będzie używane na potrzeby płatności w ramach umowy PayU w celu nakłoniania do płatności wykonanych przez klientów.

## <a name="customer-experience-scenarios"></a>Scenariusze obsługi klienta

### <a name="new-customer-sign-up-scenario"></a>Scenariusz rejestracji nowego klienta

- Domyślnie witryna internetowa jest publicznie dostępna i zawiera katalog partnera na stronie głównej.

- Klienci mogą teraz należeć do dużej liczby [krajów klientów.](#customer-countries)

- Skupiono się na krajach European Free Trade Association (ASSOCIATION), Ameryka Północna, Japonii, Indiach, Australii i Nowej Zelandii.
  - Ta funkcja korzysta z obsługi autoryzacji regionalnej w zestaw SDK Centrum partnerskiego.

- Klienci mogą wybrać ofertę z katalogu do zakupu.
  - Mogą oni dodać nazwę klienta, adres i informacje związane z domeną.

- Klienci będą kierowani do procesu finalizacji zakupu PayPal płatności (w przypadku Indiach). Klienci mogą zapewniać płatność przy użyciu jednego z tych usług:
  - Istniejące konto PayPal lub payu (indie)
  - Instrument finansowych obsługiwanych w ich kraju przez PayPal lub PayU (indie). Mogą to być karty kredytowe, debetowe i konta bankowe, jeśli ma to zastosowanie.

- Dla tego klienta jest tworzona dzierżawa klienta. Po pomyślnym utworzeniu zamówienia dzierżawy klienci mają dostęp do nazwy użytkownika konta, hasła i szczegółów subskrypcji.
  - Klienci mogą zapisać nazwę użytkownika i hasło, aby być zalogowanym w celu dalszego zakupu.
  - Każda subskrypcja jest kupowana przez rok, a klienci mogą odnawiać subskrypcję w ciągu 30 dni przed datą zakończenia subskrypcji.

### <a name="view-prior-purchases-scenario"></a>Wyświetlanie scenariusza wcześniejszych zakupów

- Klient logowania przy użyciu nazwy użytkownika i hasła dzierżawy klienta przechodzi do **sekcji Moje** zamówienia.

- Klienci mogą przejść do strony **Moje zamówienia,** na której mogą wyświetlić zakupione subskrypcje i w razie potrzeby wprowadzić aktualizacje.

- Klienci mogą przejść do strony **Moje subskrypcje,** na której mogą wyświetlić wszystkie subskrypcje (oparte na licencjach, a także oparte na użyciu), w tym subskrypcje Partner Center.

### <a name="add-licenses-to-existing-subscriptions-scenario"></a>Dodawanie licencji do istniejącego scenariusza subskrypcji

- W sekcji **Moje zamówienia** klienci mogą dodać więcej licencji do istniejących subskrypcji. Klienci mogą dodawać więcej licencji w dowolnym momencie w ciągu roku subskrypcji.

- Każda dodana licencja nie zmienia daty zakończenia subskrypcji. Jednak cena subskrypcji zmienia się w zależności od daty dodania licencji i miejsca, w którym ta data jest w roku. Ceny są naliczane proporcjonalnie do opłat tylko za pozostałe dni roku.

### <a name="add-more-subscriptions-scenario"></a>Dodawanie scenariusza dodawania kolejnych subskrypcji

- Klienci mogą kupić dowolną liczbę subskrypcji w dowolnym momencie w sekcji **Dodawanie subskrypcji** w obszarze **Moje zamówienia.**

- Klient może wybrać subskrypcję, dodać ilość i zapłacić, aby ukończyć transakcję i natychmiast rozpocząć korzystanie z subskrypcji. Jeśli klient jest wstępnie zatwierdzonym klientem, subskrypcja jest dostępna do natychmiastowego użycia, a faktura zostanie wysłana do klienta w celu płatności.

### <a name="renew-subscription-scenario"></a>Scenariusz odnawiania subskrypcji

- Klient może odnowić subskrypcję w ciągu ostatnich 30 dni przed datą zakończenia subskrypcji.

- Jest ona dostępna tylko w ciągu ostatnich 30 dni.

- Jeśli subskrypcja nie została odnowiona w ciągu ostatnich 30 dni, zostanie usunięta z listy subskrypcji dla tej dzierżawy klienta.

- Nie można zaktualizować ilości podczas odnawiania.

### <a name="payments-scenario"></a>Scenariusz płatności

- Jeśli klient jest wstępnie zatwierdzony dla transakcji przez administratora, środowisko płatności nie jest prezentowane w powyższych scenariuszach. Zamiast tego partner może wysłać fakturę do płatności do wstępnie zatwierdzonego klienta.

- W przypadku wszystkich nowych zakupów możesz dodać więcej licencji, dodać subskrypcje i odnowić. Klient może zapłacić partnerowi za pośrednictwem tej witryny internetowej za pośrednictwem PayPal lub PayU (indie).

- Ta witryna internetowa jest zintegrowana z PayPal lub PayU (dla Indiach) i umożliwia partnerom akceptowanie płatności od klientów. PayPal lub płatność (w przypadku Indiach) ta kwota jest na koncie partnera. PayPal lub PayU (dla Indiach) Zarządzanie kontami bankowymi znajduje się poza tą witryną internetową i jest zarządzane odpowiednio w witrynie PayPal.com lub PayUmoney.com.

- Jest to zależne od partnerów, którzy konfigurują konfigurację płatności PayPal lubpłatności za indie na stronie PayPal.com lub PayUmoney.com. Firma Microsoft nie zapisuje tych informacji ani rzeczywistych transakcji płatności wynikających z użycia tej opcji.

### <a name="prorated-pricing-scenario"></a>Scenariusz cen proporcjonalny

- Ta witryna internetowa obsługuje ceny proporcjonalnie w przypadkach, gdy klienci dodają więcej licencji do istniejącej subskrypcji.

- Każda subskrypcja wygasa po upływie jednego roku i nie można jej zmienić po zakupie subskrypcji.

- Data zakończenia subskrypcji nie zmieni się przez dodanie dodatkowych licencji. Klienci zostaną obciążani opłatami za pozostałą liczbę dni do daty zakończenia. Jeśli na przykład w pierwszym dniu koszt subskrypcji wynosi 365 USD, a dodasz jeszcze jedną licencję w dniu 2, cena nowej licencji będzie 364 USD. Jeśli dodasz jeszcze jedną licencję 10 dni później, cena będzie 354 USD.
