---
title: Dokonanie jednorazowego zakupu
description: Jak dokonać zakupu oprogramowania i produktów rezerwacji, takich jak subskrypcje oprogramowania, oprogramowanie bezterminowe i wystąpienia zarezerwowane maszyny wirtualnej platformy Azure, przy użyciu interfejsu API Partner Center API.
ms.date: 10/09/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: baf0b5d4aaa8957874ab019359aca2662a76194387e0cd06999b0bb329076c80
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994442"
---
# <a name="make-a-one-time-purchase"></a>Dokonanie jednorazowego zakupu

**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud for US Government

Jak dokonać zakupu oprogramowania i produktów rezerwacji, takich jak subskrypcje oprogramowania, oprogramowanie bezterminowe i wystąpienia zarezerwowane maszyny wirtualnej platformy Azure, przy użyciu interfejsu API Partner Center API.

> [!NOTE]
> Subskrypcje oprogramowania nie są dostępne na następujących rynkach:
>
> | Niedostępne rynki            | Niedostępne rynki (ciąg dalszy...) | Niedostępne rynki (ciąg dalszy...)      |
> |--------------------------------|-----------------------------------|------------------------------------------|
> | Wyspy alandzkie                  | Grenlandia                         | Papua Nowa Gwinea                         |
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
> | Brytyjskie Terytorium Oceanu Indyjskiego | Jersey                            | São Tomé i Prüncipe                    |
> | Brytyjskie Wyspy Dziewicze         | Kiribati                          | Seszele                               |
> | Burkina Faso                   | Kosowo                            | Sierra Leone                             |
> | Burundi                        | Laos                              | Sint Eustatius                           |
> | Kambodża                       | Lesotho                           | Sint Maarten                             |
> | Republika Środkowoafrykańska       | Liberia                           | Wyspy Salomona                          |
> | Czad                           | Madagaskar                        | Somalia                                  |
> | Chiny                          | Malawi                            | Georgia Południowa i Sandwich Południowy |
> | Wyspa Bożego Narodzenia               | Malediwy                          | Sudan Południowy                              |
> | Wyspy Kokosowe (Keelinga)        | Mali                              | St Stana, Ascension, Tristan da Cunha   |
> | Komory                        | Wyspy Marshalla                  | Surinam                                 |
> | Kongo                          | Martynika                        | Svalbard                                 |
> | Kongo (DRK)                    | Mauretania                        | Suazi                                |
> | Wyspy Cooka                   | Wyspa Majotta                           | Timor-Leste                              |
> | Dżibuti                       | Mikronezja                        | Togo                                     |
> | Dominika                       | Montserrat                        | Tokelau                                  |
> | Gwinea Równikowa              | Mozambik                        | Tonga                                    |
> | Erytrea                        | Myanmar                           | Wyspy Turks i Caicos                 |
> | Falklandy               | Nauru                             | Tuvalu                                   |
> | Gujana Francuska                  | Nowa Kaledonia                     | Stany Zjednoczone Odlying Islands                    |
> | Polinezja Francuska               | Niger                             | Vanuatu                                  |
> | Francuskie Terytoria Południowe i Antarktyczne    | Niue                              | Watykan                             |
> | Gabon                          | Norfolk                    | Wallis i Futuna                        |
> | Gambia                         | Mariany Północne          | Jemen                                    |
> | Gibraltar                      | Palau                             | &nbsp;                                   |
>
&nbsp;
> [!NOTE]
> Aby kupić oprogramowanie bezterminowe, użytkownik musi być wcześniej zakwalifikowany. Aby uzyskać więcej informacji, skontaktuj się z pomocą techniczną.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="making-a-one-time-purchase"></a>Dokonywanie zakupu w jednym momencie

Aby dokonać zakupu tylko raz, należy wykonać następujące czynności:

1. [Włączanie —](#enablement) (tylko wystąpienie zarezerwowane maszyny wirtualnej platformy Azure) Zarejestruj aktywną subskrypcję platformy Azure CSP, aby umożliwić jej zakup dowolnego produktu rezerwacji.

2. [Odnajdywanie](#discovery) — znajdź i wybierz produkty oraz jednostki SKU, które chcesz kupić, i sprawdź ich dostępność.

3. [Przesyłanie zamówienia](#order-submission) — utwórz koszyk z elementami w zamówieniu i prześlij go.

4. [Uzyskiwanie szczegółów zamówienia](#get-order-details) — przejrzyj szczegóły zamówienia, wszystkie zamówienia dla klienta lub wyświetl zamówienia według typu cyklu rozliczeniowego.

Po dokonanej płatności za pomocą jednego zakupu następujące scenariusze pokazują, jak zarządzać cyklem życia produktów, pobierać informacje o uprawnieniach oraz jak pobierać zestawienia sald, faktury i podsumowania faktur.

- [Zarządzanie cyklem życia](#lifecycle-management)

- [Faktura i uzgadnianie](#invoice-and-reconciliation)

## <a name="enablement"></a>Włączanie

Po zidentyfikowaniu aktywnej subskrypcji, do której chcesz dodać wystąpienie zarezerwowane maszyny wirtualnej platformy Azure, musisz zarejestrować subskrypcję, aby została włączona. Aby zarejestrować istniejący [zasób subskrypcji,](subscription-resources.md) aby go włączyć, zobacz [Rejestrowanie subskrypcji](register-a-subscription.md).

Po zarejestrowaniu subskrypcji należy potwierdzić ukończenie procesu rejestracji, sprawdzając stan rejestracji. Aby wykonać ten krok, zobacz Get subscription registration status (Uzyskiwanie [stanu rejestracji subskrypcji).](get-subscription-registration-status.md)

## <a name="discovery"></a>Odnajdywanie

Po włączeniu subskrypcji możesz wybrać produkty i jednostki SKU i sprawdzić ich dostępność przy użyciu następujących modeli Partner Center API:

- [Produkt](product-resources.md#product) — konstrukcja grupowania dla produktów lub usług, które można kupować. Sam produkt nie jest elementem do kupienia.

- [Jednostka SKU](product-resources.md#sku) — jednostka magazynowa (SKU) do zakupu w ramach produktu. Jednostki SKU reprezentują różne kształty produktu.

- [Dostępność](product-resources.md#availability) — konfiguracja, w której można kupić sku (na przykład kraj, waluta i segment branży).

Przed dokonaniem zakupu w jednym momencie wykonaj następujące czynności:

1. Zidentyfikuj i pobierz produkt i sku, które chcesz kupić. W tym kroku możesz najpierw utworzyć listę produktów i jednostki SKU lub, jeśli znasz już identyfikatory produktu i jednostki SKU, wybierając je.

   - [Uzyskiwanie listy produktów](get-a-list-of-products.md)
   - [Uzyskiwanie produktu przy użyciu identyfikatora produktu](get-a-product-by-id.md)
   - [Uzyskiwanie listy jednostki SKU dla produktu](get-a-list-of-skus-for-a-product.md)
   - [Uzyskiwanie sku przy użyciu identyfikatora SKU](get-a-sku-by-id.md)

2. Sprawdź spis dla sku. Ten krok jest wymagany tylko w przypadku jednostki SKU, które są oznaczone wstępnie **wymaganym elementem InventoryCheck.**

   - [Sprawdzenie spisu](check-inventory.md)

3. Pobierz dostępność [dla](product-resources.md#availability) [SKU](product-resources.md#sku). Podczas składania zamówienia będziesz potrzebować wartości **CatalogItemId** dostępności. Aby uzyskać tę wartość, użyj jednego z następujących interfejsów API:

   - [Uzyskiwanie listy dostępności dla sku](get-a-list-of-availabilities-for-a-sku.md)
   - [Uzyskiwanie dostępności przy użyciu identyfikatora dostępności](get-an-availability-by-id.md)

## <a name="order-submission"></a>Przesyłanie zamówienia

Aby przesłać zamówienie, wykonaj następujące kroki:

1. Utwórz koszyk do przechowywania kolekcji elementów katalogu, które zamierzasz kupić. Podczas tworzenia koszyka [elementy wiersza](cart-resources.md) [koszyka](cart-resources.md#cartlineitem) są automatycznie grupowane na podstawie elementów, które można kupić razem w tym samym [zamówieniu.](order-resources.md)

   - [Tworzenie koszyka](create-a-cart.md)
   - [Aktualizowanie koszyka](update-a-cart.md)

2. Zapoznaj się z koszykiem. Wyeencjonuj koszyk powoduje utworzenie [zamówienia](order-resources.md).

   - [Finalizacji zakupu koszyka](checkout-a-cart.md)

## <a name="get-order-details"></a>Uzyskiwanie szczegółów zamówienia

Po utworzeniu zamówienia możesz pobrać szczegóły pojedynczego zamówienia przy użyciu identyfikatora zamówienia lub uzyskać listę zamówień dla klienta. Istnieje opóźnienie do 15 minut między tym, kiedy zamówienie zostanie przesłane, a kiedy pojawi się na liście zamówień klienta.

- Aby uzyskać szczegółowe informacje o indywidualnym zamówieniu przy użyciu identyfikatora zamówienia. Zobacz Get [an order by ID (Uzyskiwanie zamówienia według identyfikatora).](get-an-order-by-id.md)

- Aby uzyskać listę zamówień dla klienta przy użyciu identyfikatora klienta. Zobacz [Get all of a customer's orders](get-all-of-a-customer-s-orders.md)( Pobierz wszystkie zamówienia klienta).

- Aby uzyskać listę zamówień dla [](product-resources.md#billingcycletype) klienta według typu cyklu rozliczeniowego, możesz oddzielnie wyświetlić listę zamówień (opłaty roczne lub miesięczne). Zobacz Get a list of orders by customer and billing cycle type (Uzyskiwanie listy [zamówień według klienta i typu cyklu rozliczeniowego).](get-a-list-of-orders-by-customer-and-billing-cycle-type.md)

## <a name="lifecycle-management"></a>Zarządzanie cyklem życia

W ramach zarządzania cyklem życia zakupów w ramach usługi Partner Center można pobrać [](entitlement-resources.md)informacje o uprawnieniach i uzyskać szczegóły rezerwacji przy użyciu identyfikatora zamówienia rezerwacji. Aby uzyskać przykłady, jak to zrobić, zobacz [Get entitlements (Uzyskiwanie uprawnień).](get-a-collection-of-entitlements.md)

## <a name="invoice-and-reconciliation"></a>Faktura i uzgadnianie

Poniższe scenariusze pokazują, jak programowo wyświetlać [](invoice-resources.md)faktury klienta oraz pobierać salda i podsumowania konta, które obejmują opłaty razowe.

### <a name="balance-and-payment"></a>Saldo i płatność

Aby uzyskać bieżące saldo konta w domyślnym typie waluty, który jest saldem opłat cyklicznych i jednorazowych, zobacz Get your current account balance (Uzyskiwanie [bieżącego salda konta).](get-the-reseller-s-current-account-balance.md)

### <a name="multi-currency-balance-and-payment"></a>Saldo i płatność w wielu walutach

Aby uzyskać bieżące saldo konta i kolekcję podsumowań faktur zawierających podsumowanie faktury z opłatami cyklicznym i jednorazowym dla każdego typu waluty klienta, zobacz Pobieranie podsumowań [faktur](get-invoice-summaries.md).

### <a name="invoices"></a>Faktury

Aby uzyskać kolekcję faktur, które pokazują opłaty cykliczne i jednorazowy, zobacz [Pobieranie kolekcji faktur](get-a-collection-of-invoices.md).

### <a name="single-invoice"></a>Pojedyncza faktura

Aby pobrać określoną fakturę przy użyciu identyfikatora faktury, zobacz [Pobieranie faktury według identyfikatora](get-invoice-by-id.md).

### <a name="reconciliation"></a>Pojednania

Aby uzyskać kolekcję szczegółów pozycji faktury (pozycje uzgodnień) dla określonego identyfikatora faktury, zobacz [Pobieranie pozycji faktury](get-invoiceline-items.md).

### <a name="download-an-invoice-as-a-pdf"></a>Pobieranie faktury w formacie PDF

Aby pobrać zestawienie faktur w formacie PDF przy użyciu identyfikatora faktury, zobacz [Pobieranie zestawienia faktury.](get-invoice-statement.md)
