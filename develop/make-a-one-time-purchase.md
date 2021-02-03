---
title: Dokonanie jednorazowego zakupu
description: Jak przeprowadzić jednorazowe kupowanie oprogramowania i produktów rezerwacji, takich jak subskrypcje oprogramowania, bezterminowe oprogramowanie i zarezerwowane maszyny wirtualne platformy Azure, za pomocą interfejsu API Centrum partnerskiego.
ms.date: 10/09/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 17a5f5c1e845ba36a94d7ce909df30e0146ba448
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767809"
---
# <a name="make-a-one-time-purchase"></a>Dokonanie jednorazowego zakupu

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie Microsoft Cloud for US Government

Jak przeprowadzić jednorazowe kupowanie oprogramowania i produktów rezerwacji, takich jak subskrypcje oprogramowania, bezterminowe oprogramowanie i zarezerwowane maszyny wirtualne platformy Azure, za pomocą interfejsu API Centrum partnerskiego.

> [!NOTE]
> Subskrypcje oprogramowania nie są dostępne na następujących rynkach:
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
&nbsp;
> [!NOTE]
> Aby zakupić bezterminowe oprogramowanie, musisz mieć wcześniej kwalifikacje. Skontaktuj się z pomocą techniczną, aby uzyskać więcej informacji.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="making-a-one-time-purchase"></a>Jednorazowe kupowanie

Aby dokonać jednorazowego zakupu, wykonaj następujące czynności:

1. [Włączenie](#enablement) — (tylko wystąpienie ZASTRZEŻONEJ maszyny wirtualnej platformy Azure) Zarejestruj aktywną subskrypcję platformy Azure w celu umożliwienia zakupienia dowolnego produktu rezerwacji.

2. [Odnajdywanie](#discovery) — Znajdź i wybierz produkty i jednostki SKU, które chcesz kupić, i sprawdź ich dostępność.

3. [Zamówienie przesłania](#order-submission) — Utwórz koszyk z elementami w zamówieniu i prześlij go.

4. [Pobierz szczegóły zamówienia](#get-order-details) — Przejrzyj szczegóły zamówienia, wszystkie zamówienia dla klienta lub Wyświetl zamówienia według typu cyklu rozliczeniowego.

Po dokonaniu jednorazowego zakupu w poniższych scenariuszach pokazano, jak zarządzać cyklem życia produktów, pobierając informacje o uprawnieniach i sposobie pobierania zestawień bilansowych, faktur i podsumowań faktur.

- [Zarządzanie cyklem życia](#lifecycle-management)

- [Faktura i uzgadnianie](#invoice-and-reconciliation)

## <a name="enablement"></a>Włączanie

Po zidentyfikowaniu aktywnej subskrypcji, do której chcesz dodać wystąpienie zarezerwowanych maszyn wirtualnych platformy Azure do programu, należy zarejestrować subskrypcję, aby była włączona. Aby zarejestrować istniejący zasób [subskrypcji](subscription-resources.md) , aby był on włączony, zobacz [Rejestrowanie subskrypcji](register-a-subscription.md).

Po zarejestrowaniu subskrypcji należy upewnić się, że proces rejestracji został ukończony przez sprawdzenie stanu rejestracji. Aby wykonać ten krok, zobacz [pobieranie stanu rejestracji subskrypcji](get-subscription-registration-status.md).

## <a name="discovery"></a>Odnajdywanie

Po włączeniu subskrypcji możesz wybrać produkty i jednostki SKU oraz sprawdzić ich dostępność przy użyciu następujących modeli interfejsu API Centrum partnerskiego:

- [Product](product-resources.md#product) -konstrukcja grupująca dla jednostek towarów lub usług. Produkt nie jest elementem jednostek.

- [SKU](product-resources.md#sku) — jednostka magazynowa jednostek (SKU) w ramach produktu. Jednostki SKU reprezentują różne kształty produktu.

- [Dostępność](product-resources.md#availability) — konfiguracja, w której jednostka SKU jest dostępna do zakupu (na przykład kraj, waluta i segment branżowy).

Przed dokonaniem jednorazowego zakupu wykonaj następujące czynności:

1. Zidentyfikuj i Pobierz produkt i jednostkę SKU, które chcesz kupić. Ten krok można wykonać, wymieniając najpierw produkty i jednostki SKU, lub jeśli znasz już identyfikatory produktu i jednostki SKU, wybierając je.

   - [Pobierz listę produktów](get-a-list-of-products.md)
   - [Uzyskiwanie produktu przy użyciu identyfikatora produktu](get-a-product-by-id.md)
   - [Pobierz listę jednostek SKU dla produktu](get-a-list-of-skus-for-a-product.md)
   - [Pobierz jednostkę SKU przy użyciu identyfikatora jednostki SKU](get-a-sku-by-id.md)

2. Sprawdź spis dla jednostki SKU. Ten krok jest wymagany tylko w przypadku jednostek SKU, które są oznaczone jako wymaganie wstępne **InventoryCheck** .

   - [Sprawdzenie spisu](check-inventory.md)

3. Pobierz [dostępność](product-resources.md#availability) dla [jednostki SKU](product-resources.md#sku). Podczas umieszczania zamówienia będzie potrzebna **CatalogItemId** dostępność. Aby uzyskać tę wartość, użyj jednego z następujących interfejsów API:

   - [Pobierz listę dostępność dla jednostki SKU](get-a-list-of-availabilities-for-a-sku.md)
   - [Uzyskaj dostępność przy użyciu identyfikatora dostępności](get-an-availability-by-id.md)

## <a name="order-submission"></a>Przesyłanie zamówienia

Aby przesłać zamówienie, wykonaj następujące kroki:

1. Utwórz koszyk do przechowywania kolekcji elementów wykazu, które zamierzasz kupić. Podczas tworzenia [koszyka](cart-resources.md) [elementy w linii koszyka](cart-resources.md#cartlineitem) są automatycznie grupowane na podstawie tego, co można zakupić razem w tej samej [kolejności](order-resources.md).

   - [Tworzenie koszyka](create-a-cart.md)
   - [Aktualizowanie koszyka](update-a-cart.md)

2. Sprawdź koszyk. Wyewidencjonowanie koszyka powoduje utworzenie [zamówienia](order-resources.md).

   - [Wyewidencjonuj koszyk](checkout-a-cart.md)

## <a name="get-order-details"></a>Pobierz szczegóły zamówienia

Po utworzeniu zamówienia można pobrać szczegóły indywidualnego zamówienia przy użyciu identyfikatora zamówienia lub uzyskać listę zamówień dla klienta. Istnieje opóźnienie do 15 minut od momentu, gdy zamówienie zostanie przesłane i pojawi się na liście zamówień klienta.

- Aby uzyskać szczegółowe informacje o poszczególnych zamówieniach przy użyciu identyfikatora zamówienia. Zobacz, [Pobierz zamówienie według identyfikatora](get-an-order-by-id.md).

- Aby uzyskać listę zamówień dla klienta przy użyciu identyfikatora klienta. Zobacz, aby [uzyskać wszystkie zamówienia klienta](get-all-of-a-customer-s-orders.md).

- Aby uzyskać listę zamówień dla klienta według [typu cyklu rozliczeniowego](product-resources.md#billingcycletype) , który pozwala na wyświetlanie list zamówień (opłaty jednorazowe) i comiesięcznych lub miesięcznych zamówień rozliczanych osobno. Zobacz, aby [uzyskać listę zamówień według typu cyklu klienta i rozliczeń](get-a-list-of-orders-by-customer-and-billing-cycle-type.md).

## <a name="lifecycle-management"></a>Zarządzanie cyklem życia

W ramach zarządzania cyklem życia zakupów jednorazowych w centrum partnerskim można pobrać informacje o [uprawnieniach](entitlement-resources.md)i uzyskać szczegółowe informacje dotyczące rezerwacji przy użyciu identyfikatora zamówienia rezerwacji. Aby zapoznać się z przykładami, zobacz [Uzyskaj uprawnienia](get-a-collection-of-entitlements.md).

## <a name="invoice-and-reconciliation"></a>Faktura i uzgadnianie

W poniższych scenariuszach pokazano, jak programowo wyświetlić [faktury](invoice-resources.md)klienta i uzyskać salda konta oraz podsumowania obejmujące opłaty jednorazowe.

### <a name="balance-and-payment"></a>Saldo i płatność

Aby uzyskać bieżące saldo konta w ramach domyślnego typu waluty, który jest bilansem zarówno opłat cyklicznych, jak i jednorazowych, zobacz [pobieranie bieżącego salda konta](get-the-reseller-s-current-account-balance.md) .

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
