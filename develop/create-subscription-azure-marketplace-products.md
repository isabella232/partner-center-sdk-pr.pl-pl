---
title: Tworzenie subskrypcji dla komercyjnych produktów Marketplace
description: Deweloperzy mogą tworzyć i zarządzać subskrypcją komercyjnych produktów Marketplace przy użyciu interfejsów API Centrum partnerskiego.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df2a3707e00ba36a11c404b102304c08d105244e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767749"
---
# <a name="create-a-subscription-for-commercial-marketplace-products"></a>Tworzenie subskrypcji dla komercyjnych produktów Marketplace

**Dotyczy:**

* Centrum partnerskie

Możesz utworzyć subskrypcję dla komercyjnych produktów Marketplace przy użyciu interfejsów API Centrum partnerskiego. Musisz [uzyskać listę ofert dla rynku](#get-a-list-of-offers-for-a-market), [utworzyć i przesłać zamówienie](#create-and-submit-an-order) na komercyjną subskrypcję portalu Marketplace, a następnie [pobrać link aktywacji](#get-activation-link).

Możesz również [wykonywać Zarządzanie cyklem życia](#lifecycle-management) i [zarządzać fakturami](#invoice-and-reconciliation) dla tych subskrypcji.

## <a name="prerequisites"></a>Wymagania wstępne

* Poświadczenia [uwierzytelniania Centrum partnerskiego](partner-center-authentication.md) . Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.
* Identyfikator klienta. Jeśli nie masz identyfikatora klienta, wykonaj kroki opisane w sekcji [Pobieranie listy klientów](get-a-list-of-customers.md). Alternatywnie możesz zalogować się do Centrum partnerskiego, wybrać klienta z listy klientów, wybrać pozycję **konto**, a następnie zapisać **Identyfikator Microsoft**.

## <a name="get-a-list-of-offers-for-a-market"></a>Pobieranie listy ofert dla rynku

Dostępne oferty można sprawdzić na rynku przy użyciu następujących modeli interfejsu API Centrum partnerskiego:

* **[Produkt](product-resources.md#product)**: konstrukcja grupująca dla jednostek towarów lub usług. Sam produkt nie jest elementem jednostek.
* **[SKU](product-resources.md#sku)**: jednostka magazynowa jednostek (SKU) w ramach produktu. Reprezentują one różne kształty produktu.
* **[Dostępność](product-resources.md#availability)**: Konfiguracja, w której jednostka SKU jest dostępna do zakupu (na przykład kraj, waluta lub segment branżowy).

Przed zakupem rezerwacji platformy Azure wykonaj następujące czynności:

1. Zidentyfikuj i Pobierz produkt i jednostkę SKU, które chcesz kupić. Jeśli znasz już identyfikator produktu i identyfikator jednostki SKU, zaznacz je.

    * [Pobierz listę produktów](get-a-list-of-products.md)
    * [Uzyskiwanie produktu przy użyciu identyfikatora produktu](get-a-product-by-id.md)
    * [Pobierz listę jednostek SKU dla produktu](get-a-list-of-skus-for-a-product.md)
    * [Pobierz jednostkę SKU przy użyciu identyfikatora jednostki SKU](get-a-sku-by-id.md)

    > [!NOTE]
    > Możesz identyfikować komercyjne produkty Marketplace według ich właściwości **ProductType** **"Azure"** i ich właściwości **podtyp** **"SaaS"**.

2. Jeśli jednostki SKU są znakowane z wymaganiem wstępnym **InventoryCheck** , [Sprawdź spis dla jednostki SKU](check-inventory.md).

    > [!NOTE]
    > W tej chwili nie ma żadnych komercyjnych produktów Marketplace, które obsługują sprawdzanie spisu lub są oznaczone jako wymaganie wstępne **InventoryCheck** .

3. Pobierz dostępność dla jednostki SKU. **CatalogItemId** dostępność będzie potrzebna podczas umieszczania zamówienia, który można pobrać za pomocą następujących interfejsów API:

    * [Pobierz listę dostępność dla jednostki SKU](get-a-list-of-availabilities-for-a-sku.md)
    * [Uzyskaj dostępność przy użyciu identyfikatora dostępności](get-an-availability-by-id.md)

## <a name="create-and-submit-an-order"></a>Utwórz i prześlij zamówienie

Aby przesłać swoją kolejność rezerwacji na platformie Azure, wykonaj następujące kroki:

1. [Utwórz koszyk](create-a-cart.md) do przechowywania kolekcji elementów wykazu, które zamierzasz kupić. Podczas tworzenia [koszyka](cart-resources.md#cart) [elementy w linii koszyka](cart-resources.md#cartlineitem) są automatycznie grupowane na podstawie tego, co można zakupić razem w tej samej [kolejności](order-resources.md#order). (Możesz również [zaktualizować koszyk](update-a-cart.md)).
2. [Sprawdź koszyk](checkout-a-cart.md), w wyniku którego powstaje [Zamówienie](order-resources.md#order).

### <a name="get-order-details"></a>Pobierz szczegóły zamówienia

[Szczegółowe informacje o poszczególnych zamówieniach można pobrać przy użyciu identyfikatora zamówienia](get-an-order-by-id.md). Możesz również [pobrać listę wszystkich zamówień dla określonego klienta](get-all-of-a-customer-s-orders.md).

> [!NOTE]
> Po przesłaniu zamówienia istnieje opóźnienie do 15 minut, po upływie którego zamówienie zostanie wyświetlone na liście zamówienie tego klienta.

## <a name="get-activation-link"></a>Uzyskaj link aktywacji

Partner lub klient muszą aktywować subskrypcje produktów w witrynie Azure Marketplace. Możesz [uzyskać link aktywacji, wybierając pozycję wiersz zamówienia](get-activation-link-by-order-line-item.md). Możesz również [uzyskać subskrypcję według identyfikatora](get-a-subscription-by-id.md), a następnie wyliczyć jej właściwość **Links** , aby utworzyć łącze aktywacji.

## <a name="lifecycle-management"></a>Zarządzanie cyklem życia

Możesz zarządzać cyklem życia subskrypcji dla komercyjnych produktów Marketplace przy użyciu następujących metod:

* [Anulowanie subskrypcji platformy handlowej](cancel-an-azure-marketplace-subscription.md)
* [Włączanie lub wyłączanie autoodnawiania dla komercyjnej subskrypcji portalu Marketplace](update-autorenew-for-an-azure-marketplace-subscription.md)

## <a name="quantity-management"></a>Zarządzanie ilościami

Ilość komercyjnej subskrypcji portalu Marketplace musi przypadać w ramach limitów zdefiniowanych przez skojarzoną [jednostkę SKU](product-resources.md#sku) (zobacz atrybuty **minimumQuantity** i **maximumQuantity** ). Aby zaktualizować ilość komercyjnej subskrypcji portalu Marketplace, użyj następującej metody:

* [Zmiana ilości subskrypcji](change-the-quantity-of-a-subscription.md)

## <a name="invoice-and-reconciliation"></a>Faktura i uzgadnianie

Można zarządzać [fakturami](invoice-resources.md) klienta (w tym opłatami za subskrypcje do komercyjnych produktów Marketplace) przy użyciu następujących metod:

* [Pobierz fakturę z rozliczanej komercyjnie towarami za użycie w portalu Marketplace](get-invoice-billed-consumption-lineitems.md)
* [Pobieranie linków do szacunkowych faktur](get-invoice-estimate-links.md)
* [Pobierz faktury dla rozliczanej komercyjnego zużycia w portalu Marketplace](get-invoice-unbilled-consumption-lineitems.md)
* [Pobierz faktury rozliczane pozycje wiersza uzgadniania](get-invoice-unbilled-recon-lineitems.md)

## <a name="test-using-integration-sandbox-account"></a>Testowanie przy użyciu konta piaskownicy integracji

W środowisku produkcyjnym po utworzeniu subskrypcji dla komercyjnych produktów SaaS Marketplace musisz pobrać spersonalizowany link aktywacji z Centrum partnerskiego i odwiedzić witrynę wydawcy, aby ukończyć proces instalacji. Rozliczanie subskrypcji rozpocznie się dopiero po zakończeniu instalacji.

W środowisku piaskownicy CSP nie ma integracji z niezależnymi dostawcami oprogramowania. Jeśli spróbujesz pobrać link aktywacji z Centrum partnerskiego, zostanie zwrócony fikcyjny link. Nie można użyć tego fikcyjnego linku, aby zakończyć proces instalacji w lokacji wydawcy. Aby skorzystać z konta piaskownicy Integration do testowania rozliczeń dla subskrypcji dla komercyjnych produktów SaaS Marketplace, użyj następującej metody, aby aktywować subskrypcję. Rozliczanie subskrypcji rozpocznie się po pomyślnej aktywacji:

* [Aktywuj subskrypcję piaskownicy dla komercyjnych produktów Marketplace](activate-sandbox-subscription-azure-marketplace-products.md)

