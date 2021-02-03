---
title: Zakup rezerwacji platformy Azure
description: Rezerwacje platformy Azure dla klienta można zakupić za pomocą interfejsu API Centrum partnerskiego za pośrednictwem istniejącej subskrypcji Microsoft Azure (MS-AZR-0145P) lub planu platformy Azure.
ms.date: 11/01/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4c09f65ae5105a74be41a7ec45824e3889217a1c
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767862"
---
# <a name="purchase-azure-reservations"></a>Zakup rezerwacji platformy Azure

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie Microsoft Cloud for US Government

Aby kupić rezerwację platformy Azure dla klienta przy użyciu interfejsu API Centrum partnerskiego, musisz mieć istniejącą subskrypcję Microsoft Azure (**MS-AZR-0145P**) lub plan platformy Azure.

> [!NOTE]
> Rezerwacje platformy Azure nie są dostępne na następujących rynkach:
>
> | Niedostępne rynki            | Dostępne rynki (kontynuuje...) | Dostępne rynki (kontynuuje...)      |
> |--------------------------------|-----------------------------------|------------------------------------------|
> | Wyspy Åland                  | Grenlandia                         | Papua Nowa Gwinea                         |
> | Samoa Amerykańskie                 | Grenada                           | Wyspy Pitcairn                         |
> | Andora                        | Gwadelupa                        | Reunion                                  |
> | Anguilla                       | Guam                              | Federacja Rosyjska                       |
> | Antarktyda                     | Guernsey                          | Saba                                     |
> | Antigua i Barbuda            | Gwinea                            | Saint Barthélemy                         |
> | Aruba                          | Gwinea Bissau                     | Saint Lucia                              |
> | Benin                          | Gujana                            | Saint-Martin                             |
> | Bhutan                         | Haiti                             | Saint Pierre i Miquelon                |
> | Bonaire                        | Wyspy Heard i McDonalda | Saint Vincent i Grenadyny         |
> | Wyspa Bouveta                  | Wyspa Man                       | Samoa                                    |
> | Brazylia                         | Jan Mayen                         | San Marino                               |
> | Brytyjskie Terytorium Oceanu Indyjskiego | Jersey                            | Wyspy Świętego Tomasza i Książęca                    |
> | Brytyjskie Wyspy Dziewicze         | Kiribati                          | Seszele                               |
> | Burkina Faso                   | Kosowo                            | Sierra Leone                             |
> | Burundi                        | Laos                              | Sint Eustatius                           |
> | Kambodża                       | Lesotho                           | Sint Maarten                             |
> | Republika Środkowoafrykańska       | Liberia                           | Wyspy Salomona                          |
> | Czad                           | Madagaskar                        | Somalia                                  |
> | Chiny                          | Malawi                            | Georgia Południowa i Sandwich Południowy |
> | Wyspa Bożego Narodzenia               | Malediwy                          | Sudan Południowy                              |
> | Wyspy Kokosowe (Keelinga)        | Mali                              | Święta Helena, Wyspa Wniebowstąpienia, Tristan da Cunha   |
> | Komory                        | Wyspy Marshalla                  | Surinam                                 |
> | Kongo                          | Martynika                        | Svalbard                                 |
> | Kongo (DRK)                    | Mauretania                        | Suazi                                |
> | Wyspy Cooka                   | Wyspa Majotta                           | Timor-Leste                              |
> | Dżibuti                       | Mikronezja                        | Togo                                     |
> | Dominika                       | Montserrat                        | Tokelau                                  |
> | Gwinea Równikowa              | Mozambik                        | Tonga                                    |
> | Erytrea                        | Myanmar                           | Wyspy Turks i Caicos                 |
> | Falklandy               | Nauru                             | Tuvalu                                   |
> | Gujana Francuska                  | Nowa Kaledonia                     | Odległe wyspy Stanów Zjednoczonych                    |
> | Polinezja Francuska               | Niger                             | Vanuatu                                  |
> | Francuskie Terytoria Południowe i Antarktyczne    | Niue                              | Watykan                             |
> | Gabon                          | Norfolk                    | Wallis i Futuna                        |
> | Gambia                         | Mariany Północne          | Jemen                                    |
> | Gibraltar                      | Palau                             | &nbsp;                                   |
>

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji dla aktywnej subskrypcji platformy Azure w ramach dostawcy CSP lub planu platformy Azure.

## <a name="how-to-purchase-microsoft-azure-reservations"></a>Jak kupić rezerwacje Microsoft Azure

Po zidentyfikowaniu aktywnej subskrypcji programu CSP Azure, do której chcesz dodać zastrzeżenie platformy Azure, wykonaj następujące kroki, aby je zakupić:

1. [Włącz](#enablement) — Zarejestruj aktywną subskrypcję platformy Azure dostawcy usług kryptograficznych, aby umożliwić jej kupowanie rezerwacji na platformie Azure.

2. [Odnajdywanie](#discovery) — Znajdź i wybierz produkty i jednostki SKU rezerwacji platformy Azure, które chcesz kupić, i sprawdź ich dostępność.

3. [Zamówienie przesłania](#order-submission) — Utwórz koszyk z elementami w zamówieniu i prześlij go.

4. [Pobierz szczegóły zamówienia](#get-order-details) — Przejrzyj szczegóły zamówienia, wszystkie zamówienia dla klienta lub Wyświetl zamówienia według typu cyklu rozliczeniowego.

Po zakupionym rezerwacjach platformy Azure następujące scenariusze pokazują, jak zarządzać cyklem życia, pobierając informacje o uprawnieniach do rezerwacji platformy Azure oraz o sposobie pobierania zestawień bilansowych, faktur i podsumowań faktur.

- [Zarządzanie cyklem życia](#lifecycle-management)
- [Faktura i uzgadnianie](#invoice-and-reconciliation)

## <a name="enablement"></a>Włączanie

Włączenie oznacza skojarzenie istniejącej subskrypcji Microsoft Azure (**MS-AZR-0145P**) z zarezerwowanym wystąpieniem maszyny wirtualnej platformy Azure przez zarejestrowanie subskrypcji, aby była ona włączona dla rezerwacji platformy Azure. Rejestracja jest wymaganiem wstępnym zakupu Azure Reserved VM Instances.

Wymagana jest subskrypcja z powodu następujących czynności:

1. Aby sprawdzić, czy klient kwalifikuje się do wdrażania zasobów, a tym samym kupić Azure Reserved VM Instances w regionie.

2. Zapewnienie priorytetu pojemności dla wdrożeń w ramach subskrypcji. Ma to zastosowanie tylko do jednego zakresu Azure Reserved VM Instances z wybraną opcją **priorytet pojemności** .

Po zidentyfikowaniu aktywnej subskrypcji, do której chcesz dodać zastrzeżenie platformy Azure, musisz zarejestrować subskrypcję, aby była ona włączona dla rezerwacji na platformie Azure. Aby zarejestrować istniejący zasób [subskrypcji](subscription-resources.md) , aby był on dostępny do porządkowania rezerwacji platformy Azure, zobacz artykuł [Rejestrowanie subskrypcji](register-a-subscription.md).

Po zarejestrowaniu subskrypcji należy upewnić się, że proces rejestracji został ukończony przez sprawdzenie stanu rejestracji. Aby to zrobić, zobacz [pobieranie stanu rejestracji subskrypcji](get-subscription-registration-status.md).

> [!NOTE]
> Przy zakupie Microsoft Azure rezerwacji dla klienta z planem platformy Azure należy najpierw zarejestrować plan platformy Azure. Podobnie jak w przypadku subskrypcji Microsoft Azure (**MS-AZR-0145P**), plan platformy Azure jest reprezentowany przez zasób [subskrypcji](subscription-resources.md) Centrum partnerskiego. W związku z tym możesz użyć tej samej metody [rejestracji](register-a-subscription.md) w celu zarejestrowania planu platformy Azure.

## <a name="discovery"></a>Odnajdywanie

Po włączeniu subskrypcji zakupów platformy Azure Możesz wybrać produkty i jednostki SKU oraz sprawdzić ich dostępność przy użyciu następujących modeli interfejsu API Centrum partnerskiego:

- [Product](product-resources.md#product) -konstrukcja grupująca dla jednostek towarów lub usług. Produkt nie jest elementem jednostek.

- [SKU](product-resources.md#sku) — jednostka magazynowa jednostek (SKU) w ramach produktu. Reprezentują one różne kształty produktu.

- [Dostępność](product-resources.md#availability) — konfiguracja, w której jednostka SKU jest dostępna do zakupu (na przykład kraj, waluta i segment branżowy).

Przed zakupem rezerwacji platformy Azure wykonaj następujące czynności:

1. Zidentyfikuj i Pobierz produkt i jednostkę SKU, które chcesz kupić. Można to zrobić, wymieniając najpierw produkty i jednostki SKU, lub jeśli znasz już identyfikatory produktu i jednostki SKU, wybierając je.

   - [Pobieranie listy produktów (według kraju)](get-a-list-of-products.md)
   - [Uzyskiwanie produktu przy użyciu identyfikatora produktu](get-a-product-by-id.md)
   - [Pobieranie listy jednostek SKU dla produktu (według kraju)](get-a-list-of-skus-for-a-product.md)
   - [Pobierz jednostkę SKU przy użyciu identyfikatora jednostki SKU](get-a-sku-by-id.md)

2. Sprawdź spis dla jednostki SKU. Ten krok jest wymagany tylko w przypadku jednostek SKU, które są oznaczone jako wymaganie wstępne **InventoryCheck** .

   - [Sprawdzenie spisu](check-inventory.md)

3. Pobierz [dostępność](product-resources.md#availability) dla [jednostki SKU](product-resources.md#sku). Podczas umieszczania zamówienia będzie potrzebna **CatalogItemId** dostępność. Aby uzyskać tę wartość, użyj jednego z następujących interfejsów API:

   - [Pobieranie listy dostępności dla jednostki SKU (według kraju)](get-a-list-of-availabilities-for-a-sku.md)
   - [Uzyskaj dostępność przy użyciu identyfikatora dostępności](get-an-availability-by-id.md)

> [!IMPORTANT]
> Każdy Microsoft Azure produkt rezerwacji ma inną dostępność dla subskrypcji Microsoft Azure (**MS-AZR-0145P**) i planu platformy Azure. Aby [uzyskać listę produktów (według kraju)](get-a-list-of-products.md)lub [uzyskać listę jednostek SKU dla produktu (według kraju)](get-a-list-of-skus-for-a-product.md)lub uzyskać listę dostępności dla [jednostki SKU (według kraju)](get-a-list-of-availabilities-for-a-sku.md) , które mają zastosowanie tylko do planu platformy Azure, określ parametr "reservationScope = AzurePlan".

## <a name="order-submission"></a>Przesyłanie zamówienia

Aby przesłać swoją kolejność rezerwacji na platformie Azure, wykonaj następujące czynności:

1. Utwórz koszyk do przechowywania kolekcji elementów wykazu, które zamierzasz kupić. Podczas tworzenia [koszyka](cart-resources.md) [elementy w linii koszyka](cart-resources.md#cartlineitem) są automatycznie grupowane na podstawie tego, co można zakupić razem w tej samej [kolejności](order-resources.md).

   - [Tworzenie koszyka](create-a-cart.md)
   - [Aktualizowanie koszyka](update-a-cart.md)

2. Sprawdź koszyk. Wyewidencjonowanie koszyka powoduje utworzenie [zamówienia](order-resources.md).

   - [Wyewidencjonuj koszyk](checkout-a-cart.md)

## <a name="get-order-details"></a>Pobierz szczegóły zamówienia

Po utworzeniu zamówienia rezerwacji na platformie Azure Możesz pobrać szczegóły indywidualnego zamówienia przy użyciu identyfikatora zamówienia lub uzyskać listę zamówień dla klienta. Istnieje opóźnienie do 15 minut od momentu, gdy zamówienie zostanie przesłane i pojawi się na liście zamówień klienta.

- Aby uzyskać szczegółowe informacje o poszczególnych zamówieniach przy użyciu identyfikatora zamówienia. Zobacz, [Pobierz zamówienie według identyfikatora](get-an-order-by-id.md).

- Aby uzyskać listę zamówień dla klienta przy użyciu identyfikatora klienta. Zobacz, aby [uzyskać wszystkie zamówienia klienta](get-all-of-a-customer-s-orders.md).

- Aby uzyskać listę zamówień dla klienta według [typu cyklu rozliczeniowego](product-resources.md#billingcycletype) , na podstawie których można wyświetlić listę zamówień rezerwacji platformy Azure (opłaty jednorazowe) i osobno i comiesięcznie rozliczać zamówienia rocznie. Zobacz, aby [uzyskać listę zamówień według typu cyklu klienta i rozliczeń](get-a-list-of-orders-by-customer-and-billing-cycle-type.md).

## <a name="lifecycle-management"></a>Zarządzanie cyklem życia

W ramach zarządzania cyklem życia zastrzeżeń platformy Azure w centrum partnerskim można pobrać informacje o [uprawnieniach](entitlement-resources.md)do rezerwacji na platformie Azure i uzyskać szczegółowe informacje dotyczące rezerwacji przy użyciu identyfikatora zamówienia rezerwacji. Aby zapoznać się z przykładami, zobacz [Uzyskaj uprawnienia](get-a-collection-of-entitlements.md).   

## <a name="invoice-and-reconciliation"></a>Faktura i uzgadnianie

W poniższych scenariuszach pokazano, jak programowo wyświetlić [faktury](invoice-resources.md)klienta i uzyskać salda konta oraz podsumowania, które zawierają opłaty jednorazowe dla rezerwacji platformy Azure.

### <a name="balance-and-payment"></a>Saldo i płatność

Aby uzyskać bieżące saldo konta w domyślnym typie waluty, który jest bilansem opłat cyklicznych i jednorazowych (rezerwacja Azure), zobacz [pobieranie bieżącego salda konta](get-the-reseller-s-current-account-balance.md) .

### <a name="multi-currency-balance-and-payment"></a>Saldo i płatność za wiele walut

Aby skorzystać z bieżącego salda konta i kolekcji podsumowań faktur zawierających Podsumowanie faktur z uwzględnieniem zarówno cyklicznych, jak i jednorazowych opłat dla każdego z typów walutowych klienta, zobacz [Pobierz podsumowania faktur](get-invoice-summaries.md).

### <a name="invoices"></a>Faktury

Aby uzyskać kolekcję faktur, które pokazują jednocześnie opłaty cykliczne i jednorazowe, zobacz [pobieranie kolekcji faktur](get-a-collection-of-invoices.md). 

### <a name="single-invoice"></a>Pojedyncza faktura

Aby pobrać określoną fakturę przy użyciu identyfikatora faktury, zobacz [pobieranie faktury według identyfikatora](get-invoice-by-id.md).  

### <a name="reconciliation"></a>Uzgadniania

Aby uzyskać kolekcję szczegółów elementu wiersza faktury (elementy linii uzgadniania) dla określonego identyfikatora faktury, zobacz [Pobieranie elementów wiersza faktury](get-invoiceline-items.md).  

### <a name="download-an-invoice-as-a-pdf"></a>Pobierz fakturę jako plik PDF

Aby pobrać instrukcję faktury w formularzu PDF przy użyciu identyfikatora faktury, zobacz artykuł [pobieranie faktury](get-invoice-statement.md).
