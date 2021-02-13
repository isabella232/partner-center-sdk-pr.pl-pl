---
title: Testowanie i debugowanie za pomocą piaskownicy integracji
description: Dowiedz się, jak używać konta piaskownicy integracji Centrum partnerskiego (i powiązanych tokenów) do testowania i debugowania kodu, tak aby nie naliczane przypadkowo nowe opłaty.
ms.date: 09/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e5b8f6cc2eb239b7a8b8a8722b231f290e768004
ms.sourcegitcommit: a8ebfa97db9e43c6b5ff05bb37ecead6b3565721
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2021
ms.locfileid: "100335799"
---
# <a name="test-and-debug-with-your-partner-center-integration-sandbox-to-avoid-paying-unexpected-charges"></a>Przetestuj i Debuguj w piaskownicy integracji Centrum partnerskiego, aby uniknąć płacenia nieoczekiwanych opłat

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Aby przetestować kod, należy użyć konta piaskownicy integracji w centrum partnerskim (i odpowiednich tokenów), dzięki czemu nie będziesz przypadkowo ponosić nowych opłat, które firma zobowiązana do płacenia. Aby uzyskać więcej informacji o środowisku test-in-Production (TiP), zobacz [Konfigurowanie dostępu do interfejsu API w centrum partnerskim](set-up-api-access-in-partner-center.md).

## <a name="integration-sandbox-constraints"></a>Ograniczenia dotyczące integracji piaskownic

W przypadku uruchamiania zautomatyzowanych testów weryfikacyjnych kompilacji, testowania w środowisku produkcyjnym lub przeprowadzenia testów ręcznych w piaskownicy integracji można osiągnąć maksymalne limity dla piaskownicy integracji. Te limity to 75 klientów, 5 subskrypcji na klienta i 25 licencji na subskrypcję.

- Limit 25 licencji oznacza, że nie można uzyskać oferty w piaskownicy, która ma minimalne wymaganie dotyczące licencji przekraczającej 25 licencji. To ograniczenie obejmuje wersje próbne.


### <a name="azure-plan"></a>Plan platformy Azure

Domyślnie partnerzy nie mogą inicjować obsługi planów platformy Azure przy użyciu ich kont piaskownicy. Partnerzy, którzy muszą wykonać tę czynność przy użyciu konta piaskownicy, muszą mieć dostęp do programu. Aby uzyskać dostęp, skontaktuj się z menedżerem konto Microsoft lub kontaktem biznesowym. Partnerzy, którzy wcześniej zastosowali się do udostępniania subskrypcji Microsoft Azure (MS-AZR-0145P) w swoich kontach piaskownicy, nie muszą ponownie stosować się do dostępu. Zostanie udzielony dostęp do planu platformy Azure automatycznie.

W przypadku partnerów, których konta piaskownicy zostały zatwierdzone do obsługi planów platformy Azure, obowiązują następujące ograniczenia:

- Każde konto partnera piaskownicy może mieć do 10 planów platformy Azure w ramach wszystkich dzierżawców klientów (niezależnie od tego, jak plany są dystrybuowane między klientami).

- Bezpośredni partner rozliczeniowy może utworzyć do jednego planu platformy Azure dla dzierżawy klienta.

- Dostawca pośredni może utworzyć maksymalnie trzy plany platformy Azure dla dzierżawy klienta (dla różnych odsprzedawcaów pośrednich określonych jako partner-rekord).

- Każdy plan platformy Azure może mieć maksymalnie trzy subskrypcje platformy Azure.

- Każda subskrypcja platformy Azure dostawcy usług kryptograficznych w ramach konta piaskownicy jest ograniczona do czterech rdzeni maszyn wirtualnych na centrum danych. W związku z tym nie można zainicjować obsługi jednostek SKU maszyn wirtualnych, które wymagają więcej niż czterech rdzeni maszyn wirtualnych. Niektóre wyspecjalizowane jednostki SKU maszyny wirtualnej, takie jak rdzenie procesora GPU, również są wykluczone.

- Każde konto partnera piaskownicy ma limit wydatków wynoszący $2000 (USD) na cykl rozliczeniowy we wszystkich planach platformy Azure. Gdy Partner osiągnie limit wydatków, wszystkie plany platformy Azure będą tymczasowo wyłączone do następnego cyklu rozliczeniowego.

### <a name="cloud-solution-provider-csp-azure-subscription-offers"></a>Oferty subskrypcji platformy Azure dla dostawcy rozwiązań w chmurze (CSP)

Oferty subskrypcji platformy Azure dostawcy CSP nie są już dostępne domyślnie dla kont piaskownicy. Należą do nich MS-AZR-0146P, MS-AZR-DE-0146P i MS-AZR-USGOV-0146P w przypadku subskrypcji platformy Azure dla dostawców CSP w chmurze publicznej firmy Microsoft, w chmurze niemieckiej i w chmurze dla instytucji rządowych. Partnerzy, którzy potrzebują dostępu do tych ofert przy użyciu konta piaskownicy, muszą mieć dostęp do programu. W celu uzyskania dostępu należy omówić z menedżerem konto Microsoft lub kontaktem biznesowym.

W przypadku partnerów, których konta piaskownicy zostały zatwierdzone dla ofert subskrypcji platformy Azure dla dostawcy CSP, obowiązują następujące ograniczenia:

- Możesz mieć maksymalnie 375 aktywnych subskrypcji (75 klientów x 5 USD na klienta). Jednak tylko 10 z nich może być subskrypcjami platformy Azure dla dostawcy CSP.

- Gdy subskrypcja platformy Azure dla dostawcy CSP osiągnie $200 na korzystanie z platformy Azure, jej zasoby są tymczasowo wyłączone do następnego cyklu rozliczeniowego. Nadal jest uważana za aktywną subskrypcję, która jest uwzględniana w ramach limitu 10 aktywnych subskrypcji platformy Azure.

- Każda subskrypcja platformy Azure dostawcy usług kryptograficznych w ramach konta piaskownicy jest ograniczona do czterech rdzeni maszyn wirtualnych na centrum danych. W związku z tym nie można zainicjować obsługi jednostek SKU maszyn wirtualnych, które wymagają więcej niż czterech rdzeni maszyn wirtualnych. Niektóre wyspecjalizowane jednostki SKU maszyny wirtualnej, takie jak rdzenie procesora GPU, również są wykluczone.

> [!Important]
> Wszystkie istniejące subskrypcje platformy Azure z dostawcami usług kryptograficznych, które zostały udostępnione przy użyciu kont piaskownicy przed 1 sierpnia 2018, nie są już obsługiwane i zostaną wydzielone przez firmę Microsoft od 16 października do 31 października 2018. Po cofnięciu aprowizacji subskrypcji nie można ich ponownie włączyć, a skojarzone dane nie będą już dostępne. Partnerzy, którzy mają cenne dane przechowywane w ramach tych subskrypcji, muszą wykonać kopię zapasową danych przed 16 października 2018.

### <a name="azure-reserved-vm-instance"></a>Wystąpienie zarezerwowane maszyny wirtualnej platformy Azure

Jeśli [kupujesz wystąpienie zarezerwowanych maszyn wirtualnych platformy Azure](purchase-azure-reservations.md) przy użyciu konta piaskownicy, będziesz mieć ograniczone do dwóch wystąpień maszyn wirtualnych na klienta. Można również wybrać tylko z następujących jednostek SKU wystąpienia maszyn wirtualnych platformy Azure:

| Tytuł produktu  | Data wprowadzenia  | Tytuł jednostki SKU                                               | Region [ArmRegionName] | Klucz wystąpienia [ArmSkuName] | Czas trwania | Identyfikator miernika zużycia       |
|----------------|-----------------|---------------------------------------------------------|------------------------|--------------|----------|----------------------------|
| Seria B       | 12/1/2017 0:00  | Zarezerwowane wystąpienie maszyny wirtualnej, Standard_B1s, Korea Południowa, 1 rok    | KoreaSouth             | `Standard_B1s` | `1Year`    | 3f913071-0dd7-4258-8ec4-6fad05bd976d |
| Seria B       | 12/1/2017 0:00  | Zarezerwowane wystąpienie maszyny wirtualnej, Standard_B1s, Wschodnie stany USA, 1 rok     | eastus                 | `Standard_B1s` | `1Year`    | f4d7a5a5-1b67-45ea-b1a0-282fbdd34b05 |
| Seria B       | 12/1/2017 0:00  | Zarezerwowane wystąpienie maszyny wirtualnej, Standard_B1s, zachodnie stany USA 2, 1 rok   | westus2                | `Standard_B1s` | `1Year`    | 222e39f5-e99f-4fa3-a323-f46402977888 |
| Seria B       | 12/1/2017 0:00  | Zarezerwowane wystąpienie maszyny wirtualnej, Standard_B1s, Północno-środkowe stany USA, 1 rok    | northcentralus | `Standard_B1s` | `1Year`    | 4e1716fc-4842-43f1-aa96-7c1b1b1395a7 |
| Seria B       | 12/1/2017 0:00  | Zarezerwowane wystąpienie maszyny wirtualnej, Standard_B1s, Kanada Wschodnia, 1 rok     | CanadaEast             | `Standard_B1s` | `1Year`    | ab8a5993-5db7-47c8-b3b1-2e1365b353fb |

### <a name="subscriptions-for-commercial-marketplace-products"></a>Subskrypcje dla komercyjnych produktów Marketplace

W środowisku produkcyjnym po [utworzeniu subskrypcji dla komercyjnych produktów SaaS Marketplace](create-subscription-azure-marketplace-products.md)musisz pobrać spersonalizowany link aktywacji z Centrum partnerskiego i odwiedzić witrynę wydawcy, aby ukończyć proces instalacji. Rozliczanie subskrypcji rozpocznie się dopiero po zakończeniu instalacji.

W środowisku piaskownicy CSP nie ma integracji z niezależnymi dostawcami oprogramowania. Jeśli spróbujesz pobrać link aktywacji z Centrum partnerskiego, zostanie zwrócony fikcyjny link. Nie można użyć tego fikcyjnego linku, aby zakończyć proces instalacji w lokacji wydawcy. Aby skorzystać z konta piaskownicy Integration do testowania rozliczeń dla subskrypcji komercyjnych produktów SaaS Marketplace, zobacz sekcję [Aktywuj subskrypcję piaskownicy dla komercyjnych produktów Marketplace](activate-sandbox-subscription-azure-marketplace-products.md) . Rozliczanie subskrypcji rozpocznie się po pomyślnej aktywacji.

Aby oczyścić na końcu przebiegu testowego, tak aby była dostępna następująca liczba testów, zobacz następujące artykuły:

- [Usuwanie konta klienta z piaskownicy integracji](delete-a-customer-account-from-the-integration-sandbox.md)

- [Zmniejsz liczbę subskrypcji](change-the-quantity-of-a-subscription.md)

- [Wstrzymaj subskrypcję](suspend-a-subscription.md) , aby można było ją usunąć.

## <a name="best-practices-for-rest-development"></a>Najlepsze rozwiązania w zakresie programowania REST

- Użyj narzędzia do śledzenia sieci, aby zobaczyć żądanie, odpowiedź i wystąpiły błędy w kodzie stanu HTTP w odpowiedzi. Aby uzyskać więcej informacji na temat obsługi błędów, zobacz [kody błędów REST centrum partnera](error-codes.md).

- Użyj nowego identyfikatora korelacji dla każdego wywołania w interfejsie API REST Centrum partnerskiego. To rozwiązanie zapewnia lepsze rejestrowanie i pomaga w debugowaniu. Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

## <a name="troubleshooting-tips-for-common-rest-problems"></a>Porady dotyczące rozwiązywania typowych problemów z technologią REST

- Przejrzyj wszystkie właściwości nagłówka, w tym adres URL i wersję interfejsu API.

- Upewnij się, że właściwości są zawarte w razie potrzeby i prawidłowo sformatowane.

- Nieprawidłowe formatowanie tablicy jest typowym błędem.

- Elementy **ETag** są tymczasowe i jako wyniki nie powinny być przechowywane. Gdy wywołanie funkcji wymaga elementów **ETag**, należy użyć najnowszych wartości **ETag** , ponownie pobierając zasób. Wartości **ETag** powinny być zawarte w podwójnych cudzysłowach, takich jak ciąg:

   ```rest
   If-Match : "eyJpZCI6IjUwMWE4NjBjLTE2OTgtNDQyYi04MDhjLTRiNjEyY2NmMzVmMiIsInZlcnNpb24iOjF9"
   ```
