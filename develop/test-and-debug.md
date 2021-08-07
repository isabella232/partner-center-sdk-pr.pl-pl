---
title: Testowanie i debugowanie za pomocą piaskownicy integracji
description: Dowiedz się, jak używać konta Partner Center integracji aplikacji (i powiązanych tokenów) do testowania i debugowania kodu, aby uniknąć przypadkowego naliczenia nowych opłat.
ms.date: 09/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1a446f1d9a9d7370be2715305ccbaa71b09cfd45957cf8663afb42a23706a7be
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989274"
---
# <a name="test-and-debug-with-your-partner-center-integration-sandbox-to-avoid-paying-unexpected-charges"></a>Przetestuj i debuguj przy użyciu Partner Center integracji, aby uniknąć płacenia nieoczekiwanych opłat

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Aby przetestować kod, należy użyć konta piaskownicy integracji w programie Partner Center (i odpowiednich tokenów), aby uniknąć przypadkowego naliczenie nowych opłat, za które firma jest odpowiedzialna. Aby uzyskać więcej informacji na temat tego środowiska test-in-production (TiP), zobacz Konfigurowanie dostępu [do interfejsu API](set-up-api-access-in-partner-center.md)w Partner Center .

## <a name="integration-sandbox-constraints"></a>Ograniczenia piaskownicy integracji

Jeśli uruchamiasz zautomatyzowane testy weryfikacji kompilacji, przeprowadzasz testowanie w środowisku produkcyjnym lub przeprowadzasz testowanie ręczne w piaskownicy integracji, możesz osiągnąć maksymalne limity piaskownicy integracji. Te limity to 75 klientów, 5 subskrypcji na klienta i 25 licencji na subskrypcję.

Limit 25 licencji oznacza, że nie można uzyskać oferty w piaskownicy, która ma minimalne wymaganie licencyjne przekraczające 25 licencji. To ograniczenie obejmuje wersje próbne.

W środowiskach piaskownicy są dostępne różne pliki faktur i uzgodnień, ale nie wszystkie z nich są dostępne na starszych lub nowoczesnych platformach. Sprawdź tabelę poniżej, aby dowiedzieć się więcej.

| **Pliki**                    | **Dostępne w starszej wersji** | **Dostępne w nowoczesnym** |
| ---------------------------- | ------------------------ | ------------------------ |
| Faktura (PDF)                  | Nie                       | Tak                      |
| Plik uzgodnień faktur | Nie                       | Tak                      |
| Plik szacowania faktury       | Nie                       | Tak                      |
| Plik dziennego rozliczanych danych użycia     | Nie                       | Tak                      |
| Plik dziennego nienali danych użycia   | Nie                       | Tak                      |


### <a name="azure-plan"></a>Plan platformy Azure

Domyślnie partnerzy nie mogą aprowizować planów platformy Azure przy użyciu kont piaskownicy. Partnerzy, którzy muszą to zrobić za pomocą konta piaskownicy, muszą złożyć wniosek o dostęp. Aby złożyć wniosek o dostęp, skontaktuj się z konto Microsoft lub kontaktem biznesowym. Partnerzy, którzy wcześniej aprowizują subskrypcje usługi Microsoft Azure (MS-AZR-0145P) na swoich kontach piaskownicy, nie muszą ponownie składać wniosku o dostęp. Uzyskają oni dostęp do automatycznego aprowizować plany platformy Azure.

W przypadku partnerów, których konta piaskownicy zostały zatwierdzone do aprowizować plany platformy Azure, obowiązują następujące limity:

- Każde konto partnera piaskownicy może mieć maksymalnie 10 planów platformy Azure we wszystkich dzierżawach klientów (niezależnie od tego, jak plany są dystrybuowane wśród klientów).

- Partner rozliczany bezpośrednio może utworzyć maksymalnie jeden plan platformy Azure na dzierżawę klienta.

- Dostawca pośredni może utworzyć maksymalnie trzy plany platformy Azure dla dzierżawy klienta (dla różnych odsprzedawców pośrednich określonych jako partner-rekord).

- Każdy plan platformy Azure może mieć maksymalnie trzy subskrypcje platformy Azure.

- Każda subskrypcja platformy Azure dla programu CSP w ramach konta piaskownicy jest ograniczona do czterech rdzeni maszyn wirtualnych na centrum danych. W związku z tym nie można aprowizć jednostki SKU maszyn wirtualnych, które wymagają więcej niż czterech rdzeni maszyn wirtualnych. Niektóre wyspecjalizowane jednostki SKU maszyn wirtualnych, takie jak rdzenie procesora GPU, również są wykluczone.

- Każde konto partnera piaskownicy ma limit wydatków w wysokości 2000 USD na cykl rozliczeniowy we wszystkich planach platformy Azure. Gdy partner osiągnie limit wydatków, wszystkie plany platformy Azure zostaną tymczasowo wyłączone do następnego cyklu rozliczeniowego.

### <a name="cloud-solution-provider-csp-azure-subscription-offers"></a>Dostawca rozwiązań w chmurze subskrypcji platformy Azure (CSP)

Oferty subskrypcji platformy Azure dla programu CSP nie są już domyślnie dostępne dla kont piaskownicy. Należą do nich ms-AZR-0146P, MS-AZR-DE-0146P i MS-AZR-USGOV-0146P dla subskrypcji platformy Azure dostawcy usług w chmurze publicznej firmy Microsoft, w chmurze niemieckiej i chmurze dla instytucji rządowych. Partnerzy, którzy potrzebują dostępu do tych ofert za pomocą konta piaskownicy, muszą złożyć wniosek o dostęp. Aby zgłosić wniosek o dostęp, skontaktuj się z konto Microsoft lub kontaktem biznesowym.

W przypadku partnerów, których konta piaskownicy zostały zatwierdzone dla ofert subskrypcji CSP platformy Azure, obowiązują następujące limity:

- Możesz mieć maksymalnie 375 aktywnych subskrypcji (75 klientów x 5 subskrypcji na klienta). Jednak tylko 10 z nich może być subskrypcjami CSP platformy Azure.

- Gdy subskrypcja platformy Azure dla programu CSP osiągnie 200 USD użycia platformy Azure, jej zasoby zostaną tymczasowo wyłączone do następnego cyklu rozliczeniowego. Nadal jest uważana za aktywną subskrypcję i jest wliczane do limitu 10 aktywnych subskrypcji platformy Azure.

- Każda subskrypcja platformy Azure dla programu CSP w ramach konta piaskownicy jest ograniczona do czterech rdzeni maszyn wirtualnych na centrum danych. W związku z tym nie można aprowizć jednostki SKU maszyn wirtualnych, które wymagają więcej niż czterech rdzeni maszyn wirtualnych. Niektóre wyspecjalizowane jednostki SKU maszyn wirtualnych, takie jak rdzenie procesora GPU, również są wykluczone.

> [!Important]
> Wszystkie istniejące subskrypcje CSP platformy Azure aprowowane przy użyciu kont piaskownicy przed 1 sierpnia 2018 r. nie są już obsługiwane i firma Microsoft nie będzie już aprowizowana od 16 października do 31 października 2018 r. Po anulowaniu aprowizowanych subskrypcji nie można ich ponownie włączyć i skojarzone dane nie będą już dostępne. Partnerzy, którzy mają cenne dane przechowywane w ramach tych subskrypcji, muszą wykonać kopię zapasową danych przed 16 października 2018 r.

### <a name="azure-reserved-vm-instance"></a>Wystąpienie zarezerwowane maszyny wirtualnej platformy Azure

Jeśli kupujesz [wystąpienie zarezerwowane maszyny wirtualnej](purchase-azure-reservations.md) platformy Azure za pomocą konta piaskownicy, możesz ograniczyć do dwóch wystąpień maszyn wirtualnych na klienta. Można również wybrać tylko następujące jednostki SKU produktu wystąpienia zarezerwowanego maszyny wirtualnej platformy Azure:

| Tytuł produktu  | Data wejścia w życie  | Tytuł SKU                                               | Region [ArmRegionName] | Klucz wystąpienia [ArmSkuName] | Czas trwania | Identyfikator miernika zużycia       |
|----------------|-----------------|---------------------------------------------------------|------------------------|--------------|----------|----------------------------|
| Seria B       | 12/1/2017 0:00  | Wystąpienie zarezerwowane maszyny wirtualnej, Standard_B1s, Korea Południowa, 1 rok    | Korea Północna             | `Standard_B1s` | `1Year`    | 3f913071-0dd7-4258-8ec4-6fad05bd976d |
| Seria B       | 12/1/2017 0:00  | Wystąpienie zarezerwowane maszyny wirtualnej, Standard_B1s, Wschodnie usa, 1 rok     | eastus                 | `Standard_B1s` | `1Year`    | f4d7a5a5-1b67-45ea-b1a0-282fbdd34b05 |
| Seria B       | 12/1/2017 0:00  | Wystąpienie zarezerwowane maszyny wirtualnej, Standard_B1s, Zachodnie stany USA 2, 1 rok   | westus2                | `Standard_B1s` | `1Year`    | 222e39f5-e99f-4fa3-a323-f46402977888 |
| Seria B       | 12/1/2017 0:00  | Wystąpienie zarezerwowane maszyny wirtualnej, Standard_B1s, Północno-środkowe usa, 1 rok    | northcentralus | `Standard_B1s` | `1Year`    | 4e1716fc-4842-43f1-aa96-7c1b1b1395a7 |
| Seria B       | 12/1/2017 0:00  | Wystąpienie zarezerwowane maszyny wirtualnej, Standard_B1s, Wschód urzędu certyfikacji, 1 rok     | CanadaEast             | `Standard_B1s` | `1Year`    | ab8a5993-5db7-47c8-b3b1-2e1365b353fb |

### <a name="subscriptions-for-commercial-marketplace-products"></a>Subskrypcje produktów komercyjnej platformy handlowej

W środowisku produkcyjnym po utworzeniu subskrypcji produktów [SaaS](create-subscription-azure-marketplace-products.md)na platformie handlowej musisz pobrać spersonalizowany link aktywacji z usługi Partner Center i odwiedzić witrynę wydawcy, aby ukończyć proces konfiguracji. Rozliczanie subskrypcji rozpocznie się dopiero po zakończeniu konfiguracji.

W środowisku piaskownicy CSP nie ma integracji z isvs. Jeśli spróbujesz pobrać link aktywacji z Partner Center, zostanie zwrócony fikcyjny link. Nie można użyć tego fikcyjnego linku do ukończenia procesu instalacji w witrynie wydawcy. Aby przetestować rozliczenia subskrypcji produktów SaaS na platformie handlowej przy użyciu konta piaskownicy integracji, zobacz Aktywowanie subskrypcji piaskownicy dla produktów [platformy handlowej.](activate-sandbox-subscription-azure-marketplace-products.md) Rozliczanie subskrypcji rozpocznie się po pomyślnej aktywacji.

Aby wyczyścić pod koniec testu, aby było miejsce na następną rundę testowania, zobacz następujące artykuły:

- [Usuwanie konta klienta z piaskownicy integracji](delete-a-customer-account-from-the-integration-sandbox.md)

- [Zmniejszanie ilości subskrypcji](change-the-quantity-of-a-subscription.md)

- [Wstrzymaj subskrypcję,](suspend-a-subscription.md) aby można było ją usunąć.

## <a name="best-practices-for-rest-development"></a>Najlepsze rozwiązania dotyczące opracowywania rozwiązań REST

- Użyj narzędzia śledzenia sieci, aby wyświetlić żądanie, odpowiedź oraz czy w kodzie stanu HTTP w odpowiedzi wystąpiły jakieś błędy. Aby uzyskać więcej informacji na temat obsługi błędów, [zobacz Partner Center kodów błędów REST](error-codes.md).

- Użyj nowego identyfikatora korelacji dla każdego wywołania interfejsu API PARTNER CENTER REST. To rozwiązanie zapewnia lepsze rejestrowanie i pomaga podczas debugowania. Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

## <a name="troubleshooting-tips-for-common-rest-problems"></a>Porady dotyczące rozwiązywania typowych problemów z technologią REST

- Przejrzyj wszystkie właściwości nagłówka, w tym adres URL i wersję interfejsu API.

- Upewnij się, że właściwości są dołączone w razie potrzeby i poprawnie sformatowane.

- Nieprawidłowe formatowanie tablicy jest powszechnym błędem.

- **ETags** są tymczasowe i w związku z tym nie powinny być przechowywane. Gdy wywołanie funkcji wymaga **tagów ETag,** użyj najnowszej **wartości ETag,** ponownie pobieranie zasobu. **Wartości ETag powinny** być zawarte w podwójnych cudzysłowach, takich jak ciąg:

   ```rest
   If-Match : "eyJpZCI6IjUwMWE4NjBjLTE2OTgtNDQyYi04MDhjLTRiNjEyY2NmMzVmMiIsInZlcnNpb24iOjF9"
   ```
