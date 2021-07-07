---
title: Tworzenie subskrypcji dla produktów komercyjnej platformy handlowej
description: Deweloperzy mogą tworzyć subskrypcje produktów z platformy handlowej i zarządzać nimi przy użyciu Partner Center API.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ae2e4b0a1ffa2e63e68864887093673e32079d9f
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973370"
---
# <a name="create-a-subscription-for-commercial-marketplace-products"></a>Tworzenie subskrypcji dla produktów komercyjnej platformy handlowej

Subskrypcję produktów z platformy handlowej można utworzyć przy użyciu Partner Center API. Musisz uzyskać [listę ofert dla](#get-a-list-of-offers-for-a-market)rynku, utworzyć i [przesłać](#create-and-submit-an-order) zamówienie dla subskrypcji platformy handlowej, a następnie pobrać [link aktywacji](#get-activation-link).

Możesz również [zarządzać cyklem życia i](#lifecycle-management) [zarządzać fakturami](#invoice-and-reconciliation) dla tych subskrypcji.

## <a name="prerequisites"></a>Wymagania wstępne

* [Partner Center poświadczenia](partner-center-authentication.md) uwierzytelniania. Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.
* Identyfikator klienta. Jeśli nie masz identyfikatora klienta, wykonaj kroki opisane w te tematu Get a list of customers (Uzyskiwanie [listy klientów).](get-a-list-of-customers.md) Możesz też zalogować się do Partner Center, wybrać klienta z listy klientów, wybrać pozycję **Konto**, a następnie zapisać **jego identyfikator Microsoft.**

## <a name="get-a-list-of-offers-for-a-market"></a>Pobieranie listy ofert dla rynku

Dostępne oferty dla rynku można sprawdzić przy użyciu następujących modeli interfejsu API Partner Center API:

* **[Produkt:](product-resources.md#product)** Konstrukcja grupowania dla towarów lub usług, które można kupować. Sam produkt nie jest elementem do zakupu.
* **[Jednostka SKU:](product-resources.md#sku)** jednostka magazynowa (SKU) do zakupu w ramach produktu. Reprezentują one różne kształty produktu.
* **[Dostępność:](product-resources.md#availability)** konfiguracja, w której można kupić sku (na przykład kraj, waluta lub segment branży).

Przed zakupem rezerwacji platformy Azure wykonaj następujące czynności:

1. Zidentyfikuj i pobierz produkt i sku, które chcesz kupić. Jeśli znasz już identyfikator produktu i identyfikator SKU, wybierz je.

    * [Uzyskiwanie listy produktów](get-a-list-of-products.md)
    * [Uzyskiwanie produktu przy użyciu identyfikatora produktu](get-a-product-by-id.md)
    * [Uzyskiwanie listy jednostki SKU dla produktu](get-a-list-of-skus-for-a-product.md)
    * [Uzyskiwanie sku przy użyciu identyfikatora SKU](get-a-sku-by-id.md)

    > [!NOTE]
    > Produkty platformy handlowej można zidentyfikować według właściwości **ProductType** **"Azure"** i właściwości **SubType** **"SaaS".**

2. Jeśli jednostki SKU są oznaczone za pomocą wymagania **wstępnego InventoryCheck,** sprawdź [spis dla jednostki SKU](check-inventory.md).

    > [!NOTE]
    > Obecnie nie ma żadnych produktów na platformie handlowej, które obsługują sprawdzanie spisu lub są oznaczone warunkiem **wstępnym InventoryCheck.**

3. Pobierz dostępność dla tej sku. Podczas składania zamówienia będziesz potrzebować wartości **CatalogItemId** dostępności, którą można pobrać za pośrednictwem następujących interfejsów API:

    * [Uzyskiwanie listy dostępności dla sku](get-a-list-of-availabilities-for-a-sku.md)
    * [Uzyskiwanie dostępności przy użyciu identyfikatora dostępności](get-an-availability-by-id.md)

## <a name="create-and-submit-an-order"></a>Tworzenie i przesyłanie zamówienia

Aby przesłać zamówienie rezerwacji platformy Azure, wykonaj następujące kroki:

1. [Utwórz koszyk do](create-a-cart.md) przechowywania kolekcji elementów katalogu, które zamierzasz kupić. Po utworzeniu [koszyka](cart-resources.md#cart)elementy [wiersza](cart-resources.md#cartlineitem) koszyka są automatycznie grupowane w oparciu o elementy, które można kupić razem w tym samym [zamówieniu.](order-resources.md#order) (Możesz również [zaktualizować koszyk).](update-a-cart.md)
2. [Zapoznaj się z koszykiem](checkout-a-cart.md), co powoduje utworzenie [zamówienia](order-resources.md#order).

### <a name="get-order-details"></a>Uzyskiwanie szczegółów zamówienia

Szczegóły pojedynczego [zamówienia można pobrać przy użyciu identyfikatora zamówienia](get-an-order-by-id.md). Możesz również [pobrać listę wszystkich zamówień dla określonego klienta.](get-all-of-a-customer-s-orders.md)

> [!NOTE]
> Po przesłaniu zamówienia istnieje opóźnienie do 15 minut, zanim zamówienie pojawi się na liście zamówień tego klienta.

## <a name="get-activation-link"></a>Uzyskiwanie linku aktywacji

Partner lub klient musi aktywować subskrypcje, aby Azure Marketplace produktów. Link aktywacji [można uzyskać według pozycji zamówienia](get-activation-link-by-order-line-item.md). Możesz również uzyskać [subskrypcję według identyfikatora](get-a-subscription-by-id.md), a następnie wyliczyć jej właściwość **Links,** aby utworzyć link aktywacji.

## <a name="lifecycle-management"></a>Zarządzanie cyklem życia

Cyklem życia subskrypcji produktów platformy handlowej można zarządzać przy użyciu następujących metod:

* [Anulowanie subskrypcji platformy handlowej](cancel-an-azure-marketplace-subscription.md)
* [Włączanie lub wyłączanie autorejezyscyjnie dla subskrypcji platformy handlowej](update-autorenew-for-an-azure-marketplace-subscription.md)

## <a name="quantity-management"></a>Zarządzanie ilością

Ilość subskrypcji platformy handlowej musi być w granicach limitów zdefiniowanych przez skojarzoną z nią [sku](product-resources.md#sku) (zobacz atrybuty **minimumQuantity** i **maximumQuantity).** Aby zaktualizować ilość subskrypcji platformy handlowej, użyj następującej metody:

* [Zmiana ilości subskrypcji](change-the-quantity-of-a-subscription.md)

## <a name="invoice-and-reconciliation"></a>Faktury i uzgadnianie

Fakturami klientów (w tym [opłatami](invoice-resources.md) za subskrypcje produktów z platformy handlowej) można zarządzać przy użyciu następujących metod:

* [Pobierz pozycje użycia komercyjnej platformy handlowej zafakturowane na podstawie faktury](get-invoice-billed-consumption-lineitems.md)
* [Pobieranie linków do szacunkowych faktur](get-invoice-estimate-links.md)
* [Pobierz pozycje użycia platformy handlowej bez rozlionych faktur](get-invoice-unbilled-consumption-lineitems.md)
* [Uzyskiwanie elementów wiersza uzgadniania bez rozliczenia na fakturze](get-invoice-unbilled-recon-lineitems.md)

## <a name="test-using-integration-sandbox-account"></a>Testowanie przy użyciu konta piaskownicy integracji

W środowisku produkcyjnym po utworzeniu subskrypcji produktów SaaS na platformie handlowej musisz pobrać spersonalizowany link aktywacji z usługi Partner Center i odwiedzić witrynę wydawcy, aby ukończyć proces konfiguracji. Rozliczanie subskrypcji rozpocznie się dopiero po zakończeniu konfiguracji.

W środowisku piaskownicy CSP nie ma integracji z isvs. Jeśli spróbujesz pobrać link aktywacji z Partner Center, zostanie zwrócony fikcyjny link. Nie można użyć tego fikcyjnego linku do ukończenia procesu instalacji w witrynie wydawcy. Aby przetestować rozliczenia dla subskrypcji produktów SaaS platformy handlowej przy użyciu konta piaskownicy integracji, użyj następującej metody, aby aktywować subskrypcję. Rozliczanie subskrypcji rozpocznie się po pomyślnej aktywacji:

* [Aktywowanie subskrypcji piaskownicy dla produktów komercyjnej platformy handlowej](activate-sandbox-subscription-azure-marketplace-products.md)

