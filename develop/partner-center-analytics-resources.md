---
title: Analiza w Centrum partnerskim
description: Dokumentacja publicznego interfejsu API analizy Centrum partnerskiego.
ms.date: 06/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4b14ee929f3020079f409be8817e077673d3219f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767773"
---
# <a name="partner-center-analytics---resources"></a>Analiza Centrum partnerskiego — zasoby

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Interfejs API analizy pozwala programistycznie uzyskiwać dostęp do danych, które są prezentowane w środowisku użytkownika.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Te scenariusze obsługują uwierzytelnianie tylko przy użyciu poświadczeń użytkownika.

## <a name="csp-program-azure-usage-analytics"></a>Program CSP: Analiza użycia platformy Azure

W poniższym scenariuszu pokazano, jak za pomocą interfejsu API analizy pobrać wszystkie informacje dotyczące analizy użycia platformy Azure.

- [Pobieranie wszystkich informacji analitycznych dotyczących użycia platformy Azure](get-all-azure-usage-analytics.md)

Ten scenariusz zwraca informacje o analizie w kolekcji zasobów [użycia platformy Azure](#azure-usage-resource) .

## <a name="azure-usage-resource"></a>Zasób użycia platformy Azure

Reprezentuje wszystkie dane analityczne dotyczące użycia platformy Azure.

| Właściwość | Typ | Opis |
|----------|------|-------------|
| CustomerTenantId | ciąg | Identyfikator dzierżawy klienta. |
| customerName | ciąg | Nazwa klienta. |
| subscriptionId | ciąg | Identyfikator subskrypcji. |
| subscriptionName | ciąg | Nazwa subskrypcji. |
| usageDate | ciąg | Data użycia. |
| resourceLocation | ciąg | Na przykład lokalizacja centrum danych, Europa Zachodnia. |
| meterCategory | ciąg | Kategoria licznika, zarządzanie danymi, na przykład. |
| meterSubcategory | ciąg | Podkategoria miernika, na przykład Geograficznie nadmiarowy. |
| meterUnit | ciąg | Jednostka miernika, taka jak gigabajty lub godziny. |
| reservationOrderId | ciąg | Kolejność rezerwacji dla wystąpienia zarezerwowanego maszyny wirtualnej platformy Azure. |
| reservationId | ciąg | Wystąpienia zarezerwowane w określonej kolejności. |
| Service | ciąg | Wskazuje typ maszyny wirtualnej. Na przykład Standard_E4s_v3. |
| quantity | długi | Wskazuje numery używane w jednostce miernika. |

## <a name="csp-program-indirect-resellers-analytics"></a>Program CSP: Analiza pośrednich odsprzedawcy

W poniższym scenariuszu pokazano, jak za pomocą interfejsu API analizy pobrać wszystkie pośredniego odsprzedawcy informacji analitycznych Centrum partnerskiego.

- [Pobieranie wszystkich informacji analitycznych dotyczących odsprzedawców pośrednich](get-all-indirect-resellers-analytics.md)

Ten scenariusz zwraca informacje o analizie w kolekcji [pośrednich zasobów odsprzedawcy](#indirect-resellers-resource) .

## <a name="indirect-resellers-resource"></a>Zasób pośrednich odsprzedawcy

Reprezentuje wszystkie dane analityczne dla pośrednich odsprzedawcaów.

| Właściwość | Typ | Opis |
|----------|------|-------------|
| partnerTenantId | ciąg | Identyfikator dzierżawy partnera, dla którego chcesz pobrać pośrednie dane odsprzedawcy. |
| identyfikator | ciąg | Pośredni identyfikator odsprzedawcy. |
| name | ciąg | Nazwa partnera, dla którego mają zostać pobrane pośrednie dane odsprzedawcy. |
| rynek | ciąg | Rynek partnera, dla którego chcesz pobrać pośrednie dane odsprzedawcy. |
| firstSubscriptionCreationDate | ciąg w formacie daty i godziny czasu UTC | Data utworzenia pierwszej subskrypcji, na podstawie której chcesz pobrać pośrednie dane odsprzedawcy. |
| latestSubscriptionCreationDate | ciąg w formacie daty i godziny czasu UTC | Data utworzenia najnowszej subskrypcji. |
| firstSubscriptionEndDate | ciąg w formacie daty i godziny czasu UTC | Po raz pierwszy subskrypcja została zakończona. |
| latestSubscriptionEndDate | ciąg w formacie daty i godziny czasu UTC | Najnowsza Data zakończenia subskrypcji. |
| firstSubscriptionSuspendedDate | ciąg w formacie daty i godziny czasu UTC | Po raz pierwszy subskrypcja została zawieszona. |
| latestSubscriptionSuspendedDate | ciąg w formacie daty i godziny czasu UTC | Najnowsza Data wstrzymania subskrypcji. |
| firstSubscriptionDeprovisionedDate | ciąg w formacie daty i godziny czasu UTC | Po raz pierwszy subskrypcja została anulowana. |
| latestSubscriptionDeprovisionedDate | ciąg w formacie daty i godziny czasu UTC | Najnowsza data anulowania aprowizacji subskrypcji. |
| subscriptionCount | double | Liczba subskrypcji dla wszystkich dodanych odsprzedawcy |
| licenseCount | double | Liczba licencji dla wszystkich dodanych odsprzedawcy |
| indirectResellerCount | double | Liczba pośrednich odsprzedawcy |

## <a name="csp-program-subscription-analytics"></a>Program CSP: Analiza subskrypcji

W poniższych scenariuszach pokazano, jak za pomocą interfejsu API analizy pobrać wszystkie informacje o analizie subskrypcji Centrum partnerskiego, filtrować je za pomocą zapytania wyszukiwania lub grupować według dat lub warunków.

- [Pobieranie wszystkich informacji analitycznych dotyczących subskrypcji](get-all-subscription-analytics.md)
- [Pobieranie informacji analitycznych dotyczących subskrypcji filtrowanych wg zapytania wyszukiwania](get-subscription-analytics-by-search-query.md)
- [Pobieranie informacji analitycznych dotyczących subskrypcji pogrupowanych według dat lub warunków](get-subscription-analytics-grouped-by-dates-or-terms.md)

Wszystkie te scenariusze zwracają informacje o analizie w kolekcji zasobów [subskrypcji](#subscription-resource) .

## <a name="subscription-resource"></a>Zasób subskrypcji

Reprezentuje wszystkie dane analityczne dla subskrypcji.

|         Właściwość          |              Typ              |                                                                      Opis                                                                       |
|---------------------------|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|     customerTenantId      |             ciąg             |                                              Ciąg sformatowany przy użyciu identyfikatora GUID, który identyfikuje dzierżawcę klienta.                                              |
|       customerName        |             ciąg             |                                                               Nazwa klienta.                                                                |
|      customerMarket       |             ciąg             |                                                 Kraj/region, w którym klient wykonuje działalność.                                                 |
|            identyfikator             |             ciąg             |                                                              Identyfikator subskrypcji.                                                              |
|          status           |             ciąg             |                                          Stan subskrypcji: "aktywny", "zawieszony" lub "cofnięto INICJOWANIE obsługi".                                           |
|        productName        |             ciąg             |                                                                Nazwa produktu.                                                                |
|     SubscriptionType      |             ciąg             |       Typ subskrypcji. **Uwaga**: w tym polu jest uwzględniana wielkość liter. Obsługiwane są następujące wartości: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".       |
|     autoRenewEnabled      |            boolean             |                                         Wartość wskazująca, czy subskrypcja jest odnawiana automatycznie.                                          |
|         partnerId         |             ciąg             | IDENTYFIKATOR MPN. Dla bezpośredniego odsprzedawcy ten parametr będzie IDENTYFIKATORem MPN partnera. W odniesieniu do pośredniego odsprzedawcy ten parametr będzie IDENTYFIKATORem MPN pośredniego odsprzedawcy. |
|       friendlyName        |             ciąg             |                                                             Nazwa subskrypcji.                                                              |
|        partnerName        |             ciąg             |                                              Nazwa partnera, dla którego została zakupiona subskrypcja                                               |
|       providerName        |             ciąg             |            Gdy transakcja subskrypcyjna dotyczy pośredniego odsprzedawcy, nazwa dostawcy jest dostawcą pośrednim, który kupił subskrypcję.             |
|    effectiveStartDate     | ciąg w formacie daty i godziny czasu UTC |                                                           Data rozpoczęcia subskrypcji.                                                            |
|     commitmentEndDate     | ciąg w formacie daty i godziny czasu UTC |                                                            Data zakończenia subskrypcji.                                                             |
|    currentStateEndDate    | ciąg w formacie daty i godziny czasu UTC |                                           Data zmiany bieżącego stanu subskrypcji.                                            |
| trialToPaidConversionDate | ciąg w formacie daty i godziny czasu UTC |                                 Data konwersji subskrypcji z wersji próbnej na płatne. Wartość domyślna to null.                                 |
|      trialStartDate       | ciąg w formacie daty i godziny czasu UTC |                                Data rozpoczęcia okresu próbnego dla subskrypcji. Wartość domyślna to null.                                 |
|       trialEndDate        | ciąg w formacie daty i godziny czasu UTC |                                  Data zakończenia okresu próbnego dla subskrypcji. Wartość domyślna to null.                                  |
|       lastUsageDate       | ciąg w formacie daty i godziny czasu UTC |                                        Data ostatniego użycia subskrypcji. Wartość domyślna to null.                                        |
|     deprovisionedDate     | ciąg w formacie daty i godziny czasu UTC |                                      Data anulowania aprowizacji subskrypcji. Wartość domyślna to null.                                      |
|      lastRenewalDate      | ciąg w formacie daty i godziny czasu UTC |                                       Data ostatniego odnowienia subskrypcji wartość domyślna to null.                                       |
|       licenseCount        |             liczba             |                                                             Łączna liczba licencji.                                                              |
|     subscriptionCount     |             liczba             |                        Liczba subskrypcji. Uwaga: Ta wartość zostanie wyświetlona tylko w odpowiedzi zapytania agregacji.                         |

## <a name="search-analytics"></a>Analiza wyszukiwania

> [!NOTE]
> Członkostwo programu CSP nie jest wymagane do pobrania usługi Search Analytics.

W poniższym scenariuszu pokazano, jak za pomocą interfejsu API analizy pobrać wszystkie informacje o analizie wyszukiwania Centrum partnerskiego.

- [Pobieranie wszystkich informacji analitycznych dotyczących wyszukiwania](get-all-search-analytics.md)

Ten scenariusz zwraca informacje o analizie w kolekcji zasobów [wyszukiwania](#search-resource) .

## <a name="search-resource"></a>Wyszukaj zasób

Reprezentuje wszystkie dane analityczne dla wyszukiwania.

| Właściwość | Typ | Opis |
|----------|------|-------------|
| companyName | ciąg | Nazwa firmy rozliczenia. |
| contactButtonClicked | Wartość logiczna | Wskazuje, czy przycisk kontakt został kliknięty. |
| keywordCountry | ciąg | Kraj określony w wyszukiwaniu. |
| w widoku | Wartość logiczna | Wskazuje, czy Wyświetlono szczegóły wyszukiwania. |
| keywordIndustryFocus | ciąg | Branża do przeszukiwania, na przykład opieki zdrowotnej. |
| mpnId | ciąg | Identyfikator Microsoft Partner Network (MPN). Dla bezpośredniego odsprzedawcy ten parametr będzie IDENTYFIKATORem MPN partnera. W odniesieniu do pośredniego odsprzedawcy ten parametr będzie IDENTYFIKATORem MPN pośredniego odsprzedawcy. |
| partnerMarket | ciąg | Ustawienia regionalne, w których Partner prowadzi działalność. |
| keywordProduct | ciąg | Produkt określony w wyszukiwaniu. |
| referralSubmitted | Wartość logiczna | Wskazuje, czy odwołanie zostało przesłane. |
| searchDate | ciąg w formacie daty i godziny czasu UTC | Data, kiedy wystąpiło zapytanie wyszukiwania. |
| keywordSearchText | ciąg | Tekst określony w wyszukiwaniu. |
| searchResultPageViews | długi | Liczba przypadków, w których Partner pozostały w wyniku wyszukiwania. Część odpowiedzi tylko w ramach agregacji.
| contactClicks | długi | Liczba klikniętych przycisków kontaktowych. Część odpowiedzi tylko w ramach agregacji.
| referralCount | długi | Liczba odwołań wygenerowanych na podstawie wyszukiwania. Część odpowiedzi tylko w ramach agregacji.
| profileViews | długi | Liczba przypadków wyświetlania profilu partnera. Część odpowiedzi tylko w ramach agregacji.

## <a name="referrals-analytics"></a>Analiza odwołań

> [!NOTE]
> Członkostwo programu CSP nie jest wymagane w celu pobrania analizy odwołań.

W poniższym scenariuszu pokazano, jak za pomocą interfejsu API analizy pobrać wszystkie informacje analityczne dotyczące usługi Partner Center.

- [Pobieranie wszystkich informacji analitycznych dotyczących poleceń](get-all-referrals-analytics.md)

Ten scenariusz zwraca informacje o analizie w kolekcji zasobów [referencyjnych](#referrals-resource) .

> [!NOTE]
> Analiza odwołań nie jest dostępna dla Centrum partnerskiego obsługiwanego przez firmę 21Vianet.

## <a name="referrals-resource"></a>Zasób odwołań

Reprezentuje wszystkie dane analityczne dla odwołania.

| Właściwość | Typ | Opis |
|----------|------|-------------|
| identyfikator | ciąg | Identyfikator dzierżawy klienta.  |
| status | ciąg | Wskazuje, czy odwołanie prowadzi do klienta.  |
| customerMarket | ciąg | Kraj/region, w którym klient wykonuje działalność. |
| customerName | ciąg | Nazwa klienta. |
| customerOrgSize | ciąg | Zakres wskazujący liczbę pracowników w organizacji klienta. Na przykład "10to50employees". |
| acceptedDate | ciąg w formacie daty i godziny czasu UTC | Data zaakceptowania odwołania. |
| acknowledgedDate | ciąg w formacie daty i godziny czasu UTC | Data potwierdzenia odwołania. |
| archivedDate | ciąg w formacie daty i godziny czasu UTC | Data zarchiwizowania odwołania. |
| declinedDate | ciąg w formacie daty i godziny czasu UTC | Data odrzucenia odwołania. |
| expiredDate | ciąg w formacie daty i godziny czasu UTC | Data wygaśnięcia odwołania. |
| lostDate | ciąg w formacie daty i godziny czasu UTC | Data utraty odwołania. |
| missedDate | ciąg w formacie daty i godziny czasu UTC | Data nieodebrania odwołania. |
| createdDate | ciąg w formacie daty i godziny czasu UTC | Data utworzenia odwołania. |
| skippedDate | ciąg w formacie daty i godziny czasu UTC | Data pominięcia odwołania. |
| wonDate | ciąg w formacie daty i godziny czasu UTC | Data wygrania odwołania. |
| partnerMarket | ciąg |  Kraj/region, w którym partner wykonuje działalność. |
