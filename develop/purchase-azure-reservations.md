---
title: Zakup rezerwacji platformy Azure
description: Rezerwacje platformy Azure dla klienta można kupić przy użyciu interfejsu API Partner Center za pośrednictwem istniejącej subskrypcji platformy Microsoft Azure (MS-AZR-0145P) lub planu platformy Azure.
ms.date: 11/01/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0b9ce4a808ac12c32bd67888fc92808baeb0e575
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547771"
---
# <a name="purchase-azure-reservations"></a>Zakup rezerwacji platformy Azure

**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud for US Government

Aby kupić rezerwację platformy Azure dla klienta przy użyciu interfejsu API usługi Partner Center, musisz mieć istniejącą subskrypcję platformy Microsoft Azure **(MS-AZR-0145P)** lub plan platformy Azure.

> [!NOTE]
> Rezerwacje platformy Azure nie są dostępne na następujących rynkach:
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

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji dla aktywnej subskrypcji platformy Azure lub planu platformy Azure dla programu CSP.

## <a name="how-to-purchase-microsoft-azure-reservations"></a>Jak kupić rezerwacje Microsoft Azure rezerwacje

Po zidentyfikowaniu aktywnej subskrypcji platformy Azure dla programu CSP, do której chcesz dodać rezerwację platformy Azure, użyj następujących kroków, aby ją kupić:

1. [Włączanie — zarejestruj](#enablement) aktywną subskrypcję platformy Azure dla programu CSP, aby umożliwić jej zakup rezerwacji platformy Azure.

2. [Odnajdywanie](#discovery) — znajdź i wybierz produkty rezerwacji platformy Azure oraz jednostki magazynowe (SKU), które chcesz kupić, i sprawdź ich dostępność.

3. [Przesyłanie zamówienia](#order-submission) — utwórz koszyk z elementami w zamówieniu i prześlij go.

4. [Uzyskiwanie szczegółów zamówienia](#get-order-details) — przejrzyj szczegóły zamówienia, wszystkie zamówienia dla klienta lub wyświetl zamówienia według typu cyklu rozliczeniowego.

Po zakupie rezerwacji platformy Azure następujące scenariusze pokazują, jak zarządzać ich cyklem życia, pobierać informacje o uprawnieniach do rezerwacji platformy Azure oraz jak pobierać zestawienia sald, faktury i podsumowania faktur.

- [Zarządzanie cyklem życia](#lifecycle-management)
- [Faktura i uzgadnianie](#invoice-and-reconciliation)

## <a name="enablement"></a>Włączanie

Włączenie oznacza skojarzenie istniejącej subskrypcji Microsoft Azure **(MS-AZR-0145P)** z wystąpieniem zarezerwowanym maszyny wirtualnej platformy Azure przez zarejestrowanie subskrypcji w celu włączenia jej dla rezerwacji platformy Azure. Rejestracja jest warunkiem wstępnym zakupu Azure Reserved VM Instances.

Subskrypcja jest wymagana do obsługi następujących zadań:

1. Aby sprawdzić, czy klient kwalifikuje się do wdrażania zasobów, a tym samym Azure Reserved VM Instances zakupu w regionie.

2. Aby zapewnić priorytet pojemności dla wdrożeń w ramach subskrypcji. Dotyczy to tylko pojedynczych zakresów Azure Reserved VM Instances z wybraną **opcją priorytetu** pojemności.

Po zidentyfikowaniu aktywnej subskrypcji, do której chcesz dodać rezerwację platformy Azure, musisz zarejestrować subskrypcję, aby była włączona dla rezerwacji platformy Azure. Aby zarejestrować istniejący [zasób subskrypcji,](subscription-resources.md) aby umożliwić zamawianie rezerwacji platformy Azure, zobacz [Rejestrowanie subskrypcji](register-a-subscription.md).

Po zarejestrowaniu subskrypcji należy potwierdzić ukończenie procesu rejestracji, sprawdzając stan rejestracji. Aby to zrobić, zobacz [Uzyskiwanie stanu rejestracji subskrypcji.](get-subscription-registration-status.md)

> [!NOTE]
> W przypadku Microsoft Azure rezerwacji dla klienta z planem platformy Azure należy najpierw zarejestrować plan platformy Azure. Podobnie jak Microsoft Azure subskrypcji platformy Azure **(MS-AZR-0145P),** plan platformy Azure jest reprezentowany przez Partner Center [subskrypcji.](subscription-resources.md) W związku z tym możesz użyć tej samej metody [rejestrowania subskrypcji,](register-a-subscription.md) aby zarejestrować plan platformy Azure.

## <a name="discovery"></a>Odnajdywanie

Po włączeniu subskrypcji w celu zakupu rezerwacji platformy Azure możesz wybrać produkty i jednostki SKU i sprawdzić ich dostępność przy użyciu następujących modeli Partner Center API:

- [Produkt](product-resources.md#product) — konstrukcja grupowania dla produktów lub usług, które można kupować. Sam produkt nie jest elementem do kupienia.

- [SKU](product-resources.md#sku) — zakupna sku w ramach produktu. Reprezentują one różne kształty produktu.

- [Dostępność](product-resources.md#availability) — konfiguracja, w której można kupić sku (na przykład kraj, waluta i segment branży).

Przed zakupem rezerwacji platformy Azure wykonaj następujące czynności:

1. Zidentyfikuj i pobierz produkt i sku, które chcesz kupić. Możesz to zrobić, najpierw, wymieniając produkty i jednostki SKU, lub jeśli znasz już identyfikatory produktu i jednostki SKU, wybierając je.

   - [Pobieranie listy produktów (według kraju)](get-a-list-of-products.md)
   - [Uzyskiwanie produktu przy użyciu identyfikatora produktu](get-a-product-by-id.md)
   - [Pobieranie listy jednostek SKU dla produktu (według kraju)](get-a-list-of-skus-for-a-product.md)
   - [Uzyskiwanie sku przy użyciu identyfikatora SKU](get-a-sku-by-id.md)

2. Sprawdź spis dla sku. Ten krok jest wymagany tylko w przypadku jednostki SKU, które są oznaczone wstępnie **wymaganym elementem InventoryCheck.**

   - [Sprawdzenie spisu](check-inventory.md)

3. Pobierz dostępność [dla](product-resources.md#availability) [SKU](product-resources.md#sku). Podczas składania zamówienia będziesz potrzebować wartości **CatalogItemId** dostępności. Aby uzyskać tę wartość, użyj jednego z następujących interfejsów API:

   - [Pobieranie listy dostępności dla jednostki SKU (według kraju)](get-a-list-of-availabilities-for-a-sku.md)
   - [Uzyskiwanie dostępności przy użyciu identyfikatora dostępności](get-an-availability-by-id.md)

> [!IMPORTANT]
> Każdy Microsoft Azure rezerwacji ma różne możliwości Microsoft Azure subskrypcji **(MS-AZR-0145P)** i planu platformy Azure. Aby uzyskać listę produktów [(według kraju)](get-a-list-of-products.md)lub uzyskać listę jednostki SKU dla produktu [(według kraju)](get-a-list-of-skus-for-a-product.md)lub uzyskać listę dostępności dla jednostki [SKU (według kraju),](get-a-list-of-availabilities-for-a-sku.md) które mają zastosowanie tylko do planu platformy Azure, określ parametr "reservationScope=AzurePlan".

## <a name="order-submission"></a>Przesyłanie zamówienia

Aby przesłać zamówienie rezerwacji platformy Azure, wykonaj następujące zadania:

1. Utwórz koszyk do przechowywania kolekcji elementów katalogu, które zamierzasz kupić. Podczas tworzenia koszyka [elementy wiersza](cart-resources.md) [koszyka](cart-resources.md#cartlineitem) są automatycznie grupowane na podstawie elementów, które można kupić razem w tym samym [zamówieniu.](order-resources.md)

   - [Tworzenie koszyka](create-a-cart.md)
   - [Aktualizowanie koszyka](update-a-cart.md)

2. Zapoznaj się z koszykiem. Wyeencjonuj koszyk powoduje utworzenie [zamówienia](order-resources.md).

   - [Finalizacji zakupu koszyka](checkout-a-cart.md)

## <a name="get-order-details"></a>Uzyskiwanie szczegółów zamówienia

Po utworzeniu zamówienia rezerwacji platformy Azure możesz pobrać szczegóły pojedynczego zamówienia przy użyciu identyfikatora zamówienia lub uzyskać listę zamówień dla klienta. Istnieje opóźnienie do 15 minut między tym, kiedy zamówienie zostanie przesłane, a kiedy pojawi się na liście zamówień klienta.

- Aby uzyskać szczegółowe informacje o indywidualnym zamówieniu przy użyciu identyfikatora zamówienia. Zobacz Get [an order by ID (Uzyskiwanie zamówienia według identyfikatora).](get-an-order-by-id.md)

- Aby uzyskać listę zamówień dla klienta przy użyciu identyfikatora klienta. Zobacz [Get all of a customer's orders](get-all-of-a-customer-s-orders.md)( Pobierz wszystkie zamówienia klienta).

- Aby uzyskać listę zamówień dla [](product-resources.md#billingcycletype) klienta według typu cyklu rozliczeniowego, możesz oddzielnie wyświetlić listę zamówień rezerwacji platformy Azure (opłaty roczne lub miesięczne). Zobacz Get a list of orders by customer and billing cycle type (Uzyskiwanie listy [zamówień według klienta i typu cyklu rozliczeniowego).](get-a-list-of-orders-by-customer-and-billing-cycle-type.md)

## <a name="lifecycle-management"></a>Zarządzanie cyklem życia

W ramach zarządzania cyklem życia rezerwacji platformy Azure w usłudze Partner Center [](entitlement-resources.md)można pobrać informacje o uprawnieniach rezerwacji platformy Azure i uzyskać szczegóły rezerwacji przy użyciu identyfikatora zamówienia rezerwacji. Aby uzyskać przykłady, jak to zrobić, zobacz [Get entitlements (Uzyskiwanie uprawnień).](get-a-collection-of-entitlements.md)   

## <a name="invoice-and-reconciliation"></a>Faktura i uzgadnianie

Poniższe scenariusze pokazują, jak programowo wyświetlać [](invoice-resources.md)faktury klienta oraz pobierać salda i podsumowania konta, które obejmują opłaty za rezerwacje platformy Azure.

### <a name="balance-and-payment"></a>Saldo i płatność

Aby uzyskać bieżące saldo konta w domyślnym typie waluty, który jest saldem zarówno cyklicznych, jak i jednorazowych opłat (rezerwacja platformy Azure), zobacz Get your current account balance (Uzyskiwanie [bieżącego salda konta)](get-the-reseller-s-current-account-balance.md)

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
