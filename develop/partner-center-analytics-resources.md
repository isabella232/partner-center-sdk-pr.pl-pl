---
title: Analiza w Centrum partnerskim
description: Partner Center Analytics w dokumentacji publicznego interfejsu API.
ms.date: 06/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 03d7d252a415524c6573c1bf62b8b9c1518a1b9f
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548094"
---
# <a name="partner-center-analytics---resources"></a>Analiza Centrum partnerskiego — zasoby

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Interfejs API analizy umożliwia programowe uzyskiwanie dostępu do danych prezentowanych w interfejsie użytkownika.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Te scenariusze obsługują uwierzytelnianie tylko przy użyciu poświadczeń użytkownika.

## <a name="csp-program-azure-usage-analytics"></a>Program CSP: Analiza użycia platformy Azure

W poniższym scenariuszu pokazano, jak za pomocą interfejsu API analizy pobrać wszystkie Partner Center analizy użycia platformy Azure.

- [Pobieranie wszystkich informacji analitycznych dotyczących użycia platformy Azure](get-all-azure-usage-analytics.md)

Ten scenariusz zwraca informacje analityczne w kolekcji zasobów [użycia platformy Azure.](#azure-usage-resource)

## <a name="azure-usage-resource"></a>Zasób użycia platformy Azure

Reprezentuje wszystkie dane analityczne dotyczące użycia platformy Azure.

| Właściwość | Typ | Opis |
|----------|------|-------------|
| CustomerTenantId | ciąg | Identyfikator dzierżawy klienta. |
| Customername | ciąg | Nazwa klienta. |
| subscriptionId | ciąg | Identyfikator subskrypcji. |
| subscriptionName | ciąg | Nazwa subskrypcji. |
| usageDate | ciąg | Data użycia. |
| resourceLocation | ciąg | Lokalizacja centrum danych, na przykład Europa Zachodnia. |
| meterCategory | ciąg | Kategoria miernika, na przykład zarządzanie danymi. |
| meterSubcategory | ciąg | Podkategoria miernika, na przykład geograficznie nadmiarowa. |
| meterUnit | ciąg | Jednostka miernika, na przykład gigabajty lub godziny. |
| reservationOrderId | ciąg | Zamówienie rezerwacji dla wystąpienia zarezerwowanego maszyny wirtualnej platformy Azure. |
| reservationId | ciąg | Wystąpienia zarezerwowane w ramach określonej kolejności wystąpień zarezerwowanych. |
| Servicetype | ciąg | Wskazuje typ maszyny wirtualnej. Na przykład Standard_E4s_v3. |
| quantity | długi | Wskazuje liczby używane w jednostce miernika. |

## <a name="csp-program-indirect-resellers-analytics"></a>Program CSP: analiza odsprzedawców pośrednich

W poniższym scenariuszu pokazano, jak używać interfejsu API analizy do pobierania wszystkich danych Partner Center analizy pośrednich odsprzedawców.

- [Pobieranie wszystkich informacji analitycznych dotyczących odsprzedawców pośrednich](get-all-indirect-resellers-analytics.md)

Ten scenariusz zwraca informacje analityczne w kolekcji zasobów [odsprzedawców pośrednich.](#indirect-resellers-resource)

## <a name="indirect-resellers-resource"></a>Zasób odsprzedawców pośrednich

Reprezentuje wszystkie dane analityczne dla pośrednich odsprzedawców.

| Właściwość | Typ | Opis |
|----------|------|-------------|
| partnerTenantId | ciąg | Identyfikator dzierżawy partnera, dla którego chcesz pobrać dane odsprzedawców pośrednich. |
| identyfikator | ciąg | Identyfikator odsprzedawcy pośredniego. |
| name | ciąg | Nazwa partnera, dla którego chcesz pobrać dane odsprzedawców pośrednich. |
| rynek | ciąg | Rynek partnera, dla którego chcesz pobrać dane odsprzedawców pośrednich. |
| firstSubscriptionCreationDate | ciąg w formacie daty i czasu UTC | Data utworzenia pierwszej subskrypcji, na podstawie której chcesz pobrać dane odsprzedawców pośrednich. |
| latestSubscriptionCreationDate | ciąg w formacie daty i czasu UTC | Data utworzenia najnowszej subskrypcji. |
| firstSubscriptionEndDate | ciąg w formacie daty i czasu UTC | Po raz pierwszy subskrypcja została zakończona. |
| latestSubscriptionEndDate | ciąg w formacie daty i czasu UTC | Najpóźniejsza data zakończenia dowolnej subskrypcji. |
| firstSubscriptionSuspendedDate | ciąg w formacie daty i czasu UTC | Po raz pierwszy wstrzymano każdą subskrypcję. |
| latestSubscriptionSuspendedDate | ciąg w formacie daty i czasu UTC | Najpóźniejsza data, kiedy jakakolwiek subskrypcja została wstrzymana. |
| firstSubscriptionDeprovisionedDate | ciąg w formacie daty i czasu UTC | Po raz pierwszy anulowano aprowizę dowolnej subskrypcji. |
| latestSubscriptionDeprovisionedDate | ciąg w formacie daty i czasu UTC | Najpóźniejsza data coprowizowana dowolnej subskrypcji. |
| subscriptionCount | double | Liczba subskrypcji dla wszystkich odsprzedawców z dodaną wartością |
| licenseCount | double | Liczba licencji dla wszystkich odsprzedawców z dodaną wartością |
| indirectResellerCount | double | Liczba odsprzedawców pośrednich |

## <a name="csp-program-subscription-analytics"></a>Program CSP: analiza subskrypcji

Poniższe scenariusze pokazują, jak używać interfejsu API analizy do pobierania wszystkich informacji analizy subskrypcji usługi Partner Center, filtrowania ich za pomocą zapytania wyszukiwania lub grupowania ich według dat lub terminów.

- [Pobieranie wszystkich informacji analitycznych dotyczących subskrypcji](get-all-subscription-analytics.md)
- [Pobieranie informacji analitycznych dotyczących subskrypcji filtrowanych wg zapytania wyszukiwania](get-subscription-analytics-by-search-query.md)
- [Pobieranie informacji analitycznych dotyczących subskrypcji pogrupowanych według dat lub warunków](get-subscription-analytics-grouped-by-dates-or-terms.md)

Wszystkie te scenariusze zwracają informacje analityczne w kolekcji [zasobów](#subscription-resource) subskrypcji.

## <a name="subscription-resource"></a>Zasób subskrypcji

Reprezentuje wszystkie dane analityczne dla subskrypcji.

|         Właściwość          |              Typ              |                                                                      Opis                                                                       |
|---------------------------|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|     customerTenantId      |             ciąg             |                                              Ciąg w formacie identyfikatora GUID, który identyfikuje dzierżawę klienta.                                              |
|       Customername        |             ciąg             |                                                               Nazwa klienta.                                                                |
|      customerMarket       |             ciąg             |                                                 Kraj/region, w którym klient działa.                                                 |
|            identyfikator             |             ciąg             |                                                              Identyfikator subskrypcji.                                                              |
|          status           |             ciąg             |                                          Stan subskrypcji: "ACTIVE", "SUSPENDED" lub "DEPROVISIONED".                                           |
|        Productname        |             ciąg             |                                                                Nazwa produktu.                                                                |
|     Subscriptiontype      |             ciąg             |       Typ subskrypcji. **Uwaga:** w tym polu jest zróżnicowa wielkość liter. Obsługiwane wartości to: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".       |
|     autoRenewEnabled      |            boolean             |                                         Wartość wskazująca, czy subskrypcja jest odnawiana automatycznie.                                          |
|         partnerId         |             ciąg             | Identyfikator Microsoft Partner Network (MPN). W przypadku odsprzedawcy bezpośredniego ten parametr będzie identyfikatorem MPN partnera. W przypadku odsprzedawcy pośredniego ten parametr będzie identyfikatorem MPN odsprzedawcy pośredniego. |
|       Friendlyname        |             ciąg             |                                                             Nazwa subskrypcji.                                                              |
|        nazwa_partnera        |             ciąg             |                                              Nazwa partnera, dla którego zakupiono subskrypcję                                               |
|       Providername        |             ciąg             |            Gdy transakcja subskrypcji jest dla odsprzedawcy pośredniego, nazwa dostawcy jest dostawcą pośrednim, który kupił subskrypcję.             |
|    effectiveStartDate     | ciąg w formacie daty i czasu UTC |                                                           Data rozpoczęcia subskrypcji.                                                            |
|     commitmentEndDate     | ciąg w formacie daty i czasu UTC |                                                            Data zakończenia subskrypcji.                                                             |
|    currentStateEndDate    | ciąg w formacie daty i czasu UTC |                                           Data zmiany bieżącego stanu subskrypcji.                                            |
| trialToPaidConversionDate | ciąg w formacie daty i czasu UTC |                                 Data konwersji subskrypcji z wersji próbnej na płatną. Wartość domyślna to null.                                 |
|      trialStartDate       | ciąg w formacie daty i czasu UTC |                                Data rozpoczęcia okresu próbnego subskrypcji. Wartość domyślna to null.                                 |
|       trialEndDate        | ciąg w formacie daty i czasu UTC |                                  Data zakończenia okresu próbnego subskrypcji. Wartość domyślna to null.                                  |
|       lastUsageDate       | ciąg w formacie daty i czasu UTC |                                        Data ostatniego użytej subskrypcji. Wartość domyślna to null.                                        |
|     deprovisionedDate     | ciąg w formacie daty i czasu UTC |                                      Data coprowizowana subskrypcji. Wartość domyślna to null.                                      |
|      lastRenewalDate      | ciąg w formacie daty i czasu UTC |                                       Data ostatniej odnowienia subskrypcji. Wartość domyślna to null.                                       |
|       licenseCount        |             liczba             |                                                             Łączna liczba licencji.                                                              |
|     subscriptionCount     |             liczba             |                        Liczba subskrypcji. Uwaga: ta wartość będzie wyświetlana tylko w odpowiedzi zapytania agregacji.                         |

## <a name="search-analytics"></a>Analiza wyszukiwania

> [!NOTE]
> Członkostwo w programie CSP nie jest wymagane do uzyskania analizy wyszukiwania.

W poniższym scenariuszu pokazano, jak za pomocą interfejsu API analizy pobrać wszystkie Partner Center analizy wyszukiwania.

- [Pobieranie wszystkich informacji analitycznych dotyczących wyszukiwania](get-all-search-analytics.md)

Ten scenariusz zwraca informacje analityczne w kolekcji [zasobów](#search-resource) wyszukiwania.

## <a name="search-resource"></a>Wyszukiwanie zasobu

Reprezentuje wszystkie dane analityczne dla wyszukiwania.

| Właściwość | Typ | Opis |
|----------|------|-------------|
| Companyname | ciąg | Nazwa firmy rozliczeniowej. |
| contactButtonClicked | Wartość logiczna | Wskazuje, czy przycisk kontaktu został klikony. |
| keywordCountry | ciąg | Kraj określony w wyszukiwaniu. |
| detailsViewed | Wartość logiczna | Wskazuje, czy szczegóły wyszukiwania były przeglądane. |
| keywordIndustryFocus | ciąg | Branża, w ramach których ma być wyszukiwana na przykład opieka zdrowotna. |
| mpnId | ciąg | Identyfikator Microsoft Partner Network (MPN). W przypadku odsprzedawcy bezpośredniego ten parametr będzie identyfikatorem MPN partnera. W przypadku odsprzedawcy pośredniego ten parametr będzie identyfikatorem MPN odsprzedawcy pośredniego. |
| partnerMarket | ciąg | Locale where the partner conducts business. |
| keywordProduct | ciąg | Produkt określony w wyszukiwaniu. |
| referralSubmitted | Wartość logiczna | Wskazuje, czy przesłano odwołanie. |
| searchDate | ciąg w formacie daty i godzin UTC | Data, kiedy wystąpiło zapytanie wyszukiwania. |
| keywordSearchText | ciąg | Tekst określony w wyszukiwaniu. |
| searchResultPageViews | długi | Liczba razy, gdy partner pojawił się w wynikach wyszukiwania. Część odpowiedzi tylko podczas agregacji.
| contactClicks | długi | Liczba kliknięcia przycisku kontaktu. Część odpowiedzi tylko podczas agregacji.
| referralCount | długi | Liczba poleceń wygenerowanych na podstawie wyszukiwania. Część odpowiedzi tylko podczas agregacji.
| profileViews | długi | Liczba wyświetlć profil partnera. Część odpowiedzi tylko podczas agregacji.

## <a name="referrals-analytics"></a>Analiza poleceń

> [!NOTE]
> Członkostwo w programie CSP nie jest wymagane do uzyskania analizy poleceń.

W poniższym scenariuszu pokazano, jak za pomocą interfejsu API analizy pobrać wszystkie Partner Center analizy poleceń.

- [Pobieranie wszystkich informacji analitycznych dotyczących poleceń](get-all-referrals-analytics.md)

Ten scenariusz zwraca informacje analityczne w kolekcji [zasobów Poleceń.](#referrals-resource)

> [!NOTE]
> Analiza skierowań nie jest dostępna dla Partner Center przez firmę 21Vianet.

## <a name="referrals-resource"></a>Zasób poleceń

Reprezentuje wszystkie dane analityczne dla polecenia.

| Właściwość | Typ | Opis |
|----------|------|-------------|
| identyfikator | ciąg | Identyfikator dzierżawy klienta.  |
| status | ciąg | Wskazuje, czy polecenie skierowało do klienta.  |
| customerMarket | ciąg | Kraj/region, w którym klient działa. |
| Customername | ciąg | Nazwa klienta. |
| customerOrgSize | ciąg | Zakres wskazujący liczbę pracowników w organizacji klienta. Na przykład "10to50employees". |
| acceptedDate | ciąg w formacie daty i godzin UTC | Data zaakceptowania polecenia. |
| acknowledgedDate | ciąg w formacie daty i godzin UTC | Data potwierdzenia odwołania. |
| archivedDate | ciąg w formacie daty i godzin UTC | Data archiwizacji polecenia. |
| declinedDate | ciąg w formacie daty i czasu UTC | Data odrzucenia odwołania. |
| expiredDate | ciąg w formacie daty i czasu UTC | Data wygaśnięcia odwołania. |
| lostDate | ciąg w formacie daty i czasu UTC | Data utraconych poleceń. |
| missedDate | ciąg w formacie daty i czasu UTC | Data pominięcia odwołania. |
| createdDate | ciąg w formacie daty i czasu UTC | Data utworzenia odwołania. |
| skippedDate | ciąg w formacie daty i czasu UTC | Data pominięcia odwołania. |
| wonDate | ciąg w formacie daty i czasu UTC | Data wygrania odwołania. |
| partnerMarket | ciąg |  Kraj/region, w którym działa partner. |
