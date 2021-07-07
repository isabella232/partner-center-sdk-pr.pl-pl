---
title: Tworzenie planu platformy Azure
description: Deweloperzy mogą programowo kupować i tworzyć plany platformy Azure oraz zarządzać nimi przy użyciu Partner Center API.
ms.date: 01/02/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: mowrim
ms.author: mowrim
ms.openlocfilehash: f329b6a3f9a61522a9fad1f0ead021563c393118
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973412"
---
# <a name="create-an-azure-plan"></a>Tworzenie planu platformy Azure

Plan platformy Azure można kupić, utworzyć i zarządzać nimi przy użyciu Partner Center API. Proces jest podobny do tworzenia subskrypcji Microsoft Azure (MS-AZR-0145P). Musisz uzyskać [element katalogu dla planu platformy Azure,](#get-the-catalog-item-for-azure-plan)a następnie utworzyć i [przesłać zamówienie.](#create-and-submit-an-order)

## <a name="prerequisites"></a>Wymagania wstępne

* [Partner Center poświadczenia](partner-center-authentication.md) uwierzytelniania. Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.
* Identyfikator klienta. Jeśli nie masz identyfikatora klienta, wykonaj kroki opisane w te tematu Get a list of customers (Uzyskiwanie [listy klientów).](get-a-list-of-customers.md) Możesz też zalogować się do Partner Center, wybrać klienta z listy klientów, wybrać pozycję **Konto**, a następnie zapisać **jego identyfikator Microsoft.**
* [Potwierdzenie akceptacji przez klienta](/partner-center/confirm-customer-agreement)Umowa z Klientem Microsoft .

## <a name="get-the-catalog-item-for-azure-plan"></a>Uzyskiwanie elementu katalogu dla planu platformy Azure

Aby można było utworzyć plan platformy Azure dla klienta, należy pobrać odpowiedni element katalogu. Element katalogu można pobrać przy użyciu istniejących interfejsów API wykazu Partner Center z następującymi modelami zasobów.

* **[Produkt:](product-resources.md#product)** Konstrukcja grupowania dla towarów lub usług, które można kupować. Sam produkt nie jest elementem do zakupu.
* **[Jednostka SKU:](product-resources.md#sku)** jednostka magazynowa (SKU) do zakupu w ramach produktu. Jednostki SKU reprezentują różne kształty produktu.
* **[Dostępność:](product-resources.md#availability)** konfiguracja, w której można kupić sku (na przykład kraj, waluta lub segment branży).

Aby uzyskać element katalogu dla planu platformy Azure, wykonaj następujące kroki:

1. Zidentyfikuj *i* pobierz identyfikator produktu dla planu platformy Azure. Wykonaj kroki opisane w [te tematu Get a list of products](get-a-list-of-products.md) (Uzyskiwanie listy produktów) i określ element **targetView** jako **MicrosoftAzure.** (Jeśli znasz już *identyfikator* produktu dla planu platformy Azure, możesz zamiast tego wykonać kroki opisane w te tematu Get [a product using the product ID](get-a-product-by-id.md) (Uzyskiwanie produktu przy użyciu identyfikatora produktu).

2. Pobierz **sku z** produktu dla planu platformy Azure. Wykonaj kroki opisane w [te tematu Get a list of SKUs for a product (Uzyskiwanie listy jednostki SKU dla produktu).](get-a-list-of-skus-for-a-product.md) Jeśli znasz już identyfikator jednostki SKU dla planu platformy Azure, możesz zamiast tego wykonać kroki opisane w te tematu Get a SKU using the SKU ID (Uzyskiwanie jednostki SKU przy [użyciu identyfikatora jednostki SKU).](get-a-sku-by-id.md)

3. Pobierz dostępność **z** wersji SKU dla planu platformy Azure. Wykonaj kroki opisane w [te tematu Get a list of availabilities for a SKU](get-a-list-of-availabilities-for-a-sku.md)(Uzyskiwanie listy dostępności dla SKU). Jeśli znasz już identyfikator potrzebnej dostępności, możesz zamiast tego wykonać kroki opisane w części Uzyskiwanie dostępności [przy użyciu identyfikatora](get-an-availability-by-id.md) dostępności. *Pamiętaj, aby zanotować wartość właściwości **CatalogItemId** dostępności planu platformy Azure. Ta wartość będzie potrzebna do utworzenia zamówienia.*

## <a name="create-and-submit-an-order"></a>Tworzenie i przesyłanie zamówienia

Aby przesłać zamówienie dotyczące planu platformy Azure, wykonaj następujące kroki:

1. [Utwórz koszyk do](create-a-cart.md) przechowywania kolekcji elementów katalogu, które zamierzasz kupić. Po utworzeniu [koszyka](cart-resources.md#cart)elementy [wiersza](cart-resources.md#cartlineitem) koszyka są automatycznie grupowane w oparciu o elementy, które można kupić razem w tym samym [zamówieniu.](order-resources.md#order) (Możesz również [zaktualizować koszyk).](update-a-cart.md)

2. [Zapoznaj się z koszykiem](checkout-a-cart.md), co powoduje utworzenie [zamówienia](order-resources.md#order).

## <a name="get-order-details"></a>Uzyskiwanie szczegółów zamówienia

Szczegóły pojedynczego [zamówienia można pobrać przy użyciu identyfikatora zamówienia](get-an-order-by-id.md). Możesz również [pobrać listę wszystkich zamówień dla określonego klienta.](get-all-of-a-customer-s-orders.md)

>[!NOTE]
>Po przesłaniu zamówienia istnieje opóźnienie do 15 minut, zanim zamówienie pojawi się na liście zamówień tego klienta.

## <a name="manage-azure-plans"></a>Zarządzanie planami platformy Azure

Po pomyślnym przetworzeniu zamówienia zostanie utworzony Partner Center **subskrypcji** platformy Azure. Następujące metody zarządzania zasobami subskrypcji usługi Partner Center **do** zarządzania planem platformy Azure:

* [Pobieranie subskrypcji klienta](get-all-of-a-customer-s-subscriptions.md)
* [Pobieranie listy subskrypcji według zamówienia](get-a-list-of-subscriptions-by-order.md)

Gdy plan platformy Azure jest tworzony w Partner Center, na platformie Azure tworzona jest również odpowiednia subskrypcja użycia platformy Azure. Możesz również utworzyć dodatkowe subskrypcje użycia platformy Azure w ramach tego samego planu platformy Azure przy użyciu Azure Portal i interfejsów API platformy Azure. Identyfikatory wszystkich subskrypcji użycia platformy Azure skojarzonych z planem platformy Azure można uzyskać, korzystając z procedury opisanej w tesłudze Get [a list of Azure entitlements for Partner Center subscription](get-a-list-of-azure-entitlements-for-subscription.md) (Uzyskiwanie listy uprawnień platformy Azure dla subskrypcji Partner Center Azure)

## <a name="lifecycle-management"></a>Zarządzanie cyklem życia

Możesz wstrzymać istniejący plan platformy Azure, korzystając z procedury [wstrzymywania subskrypcji](suspend-a-subscription.md).

*Istniejący plan platformy Azure można wstrzymać tylko wtedy, gdy nie ma już skojarzonych żadnych aktywnych zasobów użycia, w tym subskrypcji użycia platformy Azure i rezerwacji platformy Azure.*

Aby uzyskać szczegółowe informacje na temat wyłączania subskrypcji użycia platformy Azure, zobacz Interfejs [API platformy Azure na temat zarządzania cyklem życia subskrypcji.](/rest/api/resources/subscriptions)

Aby usunąć istniejące rezerwacje platformy Azure, musisz [anulować rezerwacje.](/partner-center/azure-reservations-manage#cancel-or-exchange-a-reservation)
Po wstrzymaniu planu platformy Azure można go ponownie uaktywnić.

Aby uzyskać szczegółowe informacje na temat ponownego aktywowania planu platformy Azure, zobacz [Ponowne aktywowanie wstrzymanej subskrypcji](reactivate-a-suspended-a-subscription.md)

## <a name="transition-existing-csp-offers-to-azure-plan"></a>Przenoszenie istniejących ofert CSP do planu platformy Azure

Nie możesz utworzyć planu platformy Azure dla istniejącego klienta z subskrypcją platformy Microsoft Azure (MS-AZR-0145P). Możesz jednak [przenieść klienta z istniejących ofert dostawcy CSP Azure do usług platformy Azure w ramach planu platformy Azure](/partner-center/azure-plan-transition) w nowym środowisku handlowym w programie CSP z poziomu Centrum partnerskiego. Aby przenieść istniejącego klienta, użyj interfejsów API uaktualniania produktów i wykonaj następujące czynności:

* [Sprawdź, czy klient kwalifikuje się do przeniesienia do planu platformy Azure](get-eligibility-for-product-upgrade.md)
* [Zainicjuj uaktualnienia produktu dla klienta](create-product-upgrade-entity.md)
* [Sprawdź stan uaktualnienia produktu](get-product-upgrade-status.md)

## <a name="azure-spending"></a>Wydatki na platformie Azure

Wydatki na [platformę Azure można śledzić,](azure-spending.md) odpytując o podsumowanie użycia i szczegółowe rekordy użycia przy użyciu następujących metod:

* [Pobieranie podsumowania użycia przez partnera](get-a-partner-usage-summary.md)
* [Pobieranie wszystkich rekordów dotyczących użycia przez klientów dla partnera](get-a-customer-s-usage-records.md)
* [Pobieranie podsumowania użycia przez klienta](get-a-customer-usage-summary.md)
* [Pobieranie wszystkich rekordów dotyczących użycia subskrypcji dla klienta](get-a-customer-subscription-s-usage-records.md)
* [Pobieranie podsumowania użycia subskrypcji](get-a-customer-subscription-usage-summary.md)
* [Pobieranie danych dotyczących użycia dla subskrypcji według zasobu](get-a-customer-subscription-resource-usage-records.md)
* [Pobieranie danych dotyczących użycia dla subskrypcji według miernika](get-a-customer-subscription-meter-usage-records.md)
* [Pobieranie zasobów rekordu użycia miernika](meter-usage-resources.md)
* [Pobieranie zasobów rekordu użycia zasobu](resource-usage-resources.md)

Budżet użycia klientów można również ustawić i zarządzać nimi przy użyciu następujących metod:

* [Pobieranie budżetu użycia klienta](get-a-customer-s-usage-spending-budget.md)
* [Aktualizowanie budżetu użycia klienta](update-a-customer-s-usage-spending-budget.md)

## <a name="invoice-and-reconciliation"></a>Faktury i uzgadnianie

Fakturami i danymi uzgodnień można zarządzać przy użyciu następujących metod:

* [Pobieranie kolekcji faktur](get-a-collection-of-invoices.md)
* [Pobieranie linków do szacunkowych faktur](get-invoice-estimate-links.md)
* [Uzyskiwanie faktury według identyfikatora](get-invoice-by-id.md)
* [Pobieranie zestawienia faktur](get-invoice-statement.md)
* [Pobieranie podsumowania faktur](get-invoice-summaries.md)
* [Pobieranie zafakturowanych elementów wiersza dotyczących zużycia](get-invoice-billed-consumption-lineitems.md)
* [Pobieranie niezafakturowanych elementów wiersza dotyczących zużycia](get-invoice-unbilled-consumption-lineitems.md)
* [Uzyskiwanie elementów ponownie rozliowanych na fakturze](get-invoiceline-items.md)
* [Pobieranie niezafakturowanych elementów wiersza uzgodnienia](get-invoice-unbilled-recon-lineitems.md)
