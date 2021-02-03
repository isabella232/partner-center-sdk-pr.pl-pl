---
title: Tworzenie planu platformy Azure
description: Deweloperzy mogą programistycznie kupować i tworzyć plany platformy Azure oraz zarządzać nimi przy użyciu interfejsów API Centrum partnerskiego.
ms.date: 01/02/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: mowrim
ms.author: mowrim
ms.openlocfilehash: 372b94ac7217899ca560cf943bf11a7e8906872d
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768085"
---
# <a name="create-an-azure-plan"></a>Tworzenie planu platformy Azure

**Dotyczy:**

* Centrum partnerskie

Możesz kupić i utworzyć plan platformy Azure oraz zarządzać nim przy użyciu interfejsów API Centrum partnerskiego. Ten proces jest podobny do tworzenia subskrypcji Microsoft Azure (MS-AZR-0145P). Musisz [pobrać element katalogu dla planu platformy Azure](#get-the-catalog-item-for-azure-plan), a następnie [utworzyć i przesłać zamówienie](#create-and-submit-an-order).

## <a name="prerequisites"></a>Wymagania wstępne

* Poświadczenia [uwierzytelniania Centrum partnerskiego](partner-center-authentication.md) . Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.
* Identyfikator klienta. Jeśli nie masz identyfikatora klienta, wykonaj kroki opisane w sekcji [Pobieranie listy klientów](get-a-list-of-customers.md). Alternatywnie możesz zalogować się do Centrum partnerskiego, wybrać klienta z listy klientów, wybrać pozycję **konto**, a następnie zapisać **Identyfikator Microsoft**.
* [Potwierdzenie akceptacji umowy klienta firmy Microsoft przez klienta](/partner-center/confirm-customer-agreement).

## <a name="get-the-catalog-item-for-azure-plan"></a>Pobierz element katalogu dla planu platformy Azure

Aby można było utworzyć plan platformy Azure dla klienta, należy pobrać odpowiedni element katalogu. Element katalogu można pobrać przy użyciu istniejących interfejsów API katalogu Centrum partnerskiego z następującymi modelami zasobów.

* **[Produkt](product-resources.md#product)**: konstrukcja grupująca dla jednostek towarów lub usług. Sam produkt nie jest elementem jednostek.
* **[SKU](product-resources.md#sku)**: jednostka magazynowa jednostek (SKU) w ramach produktu. Jednostki SKU reprezentują różne kształty produktu.
* **[Dostępność](product-resources.md#availability)**: Konfiguracja, w której jednostka SKU jest dostępna do zakupu (na przykład kraj, waluta lub segment branżowy).

Aby uzyskać element katalogu dla planu platformy Azure, wykonaj następujące czynności:

1. Zidentyfikuj i Pobierz identyfikator *produktu* dla planu platformy Azure. Wykonaj kroki opisane w sekcji [Pobieranie listy produktów](get-a-list-of-products.md) i określanie **targetView** jako **MicrosoftAzure**. (Jeśli znasz już identyfikator *produktu* dla planu platformy Azure, możesz wykonać czynności opisane w sekcji [Uzyskiwanie produktu przy użyciu identyfikatora produktu](get-a-product-by-id.md) ).

2. Pobierz **jednostkę SKU** z produktu dla planu platformy Azure. Wykonaj kroki opisane w sekcji [Pobieranie listy jednostek SKU dla produktu](get-a-list-of-skus-for-a-product.md). Jeśli znasz już identyfikator jednostki SKU planu platformy Azure, możesz wykonać kroki opisane w sekcji [pobieranie jednostki SKU przy użyciu identyfikatora jednostki SKU](get-a-sku-by-id.md) .

3. Pobierz **dostępność** z jednostki SKU dla planu platformy Azure. Wykonaj kroki opisane w temacie [Pobieranie listy dostępność dla jednostki SKU](get-a-list-of-availabilities-for-a-sku.md). Jeśli znasz już identyfikator potrzebnej dostępności, możesz wykonać czynności opisane w sekcji [pobieranie dostępności przy użyciu identyfikatora dostępności](get-an-availability-by-id.md) . *Pamiętaj, aby zanotować wartość właściwości **CatalogItemId** dostępności planu platformy Azure. Ta wartość będzie potrzebna, aby można było utworzyć zamówienie.*

## <a name="create-and-submit-an-order"></a>Utwórz i prześlij zamówienie

Aby przesłać zamówienie do planu platformy Azure, wykonaj następujące kroki:

1. [Utwórz koszyk](create-a-cart.md) do przechowywania kolekcji elementów wykazu, które zamierzasz kupić. Podczas tworzenia [koszyka](cart-resources.md#cart) [elementy w linii koszyka](cart-resources.md#cartlineitem) są automatycznie grupowane na podstawie tego, co można zakupić razem w tej samej [kolejności](order-resources.md#order). (Możesz również [zaktualizować koszyk](update-a-cart.md)).

2. [Sprawdź koszyk](checkout-a-cart.md), w wyniku którego powstaje [Zamówienie](order-resources.md#order).

## <a name="get-order-details"></a>Pobierz szczegóły zamówienia

[Szczegółowe informacje o poszczególnych zamówieniach można pobrać przy użyciu identyfikatora zamówienia](get-an-order-by-id.md). Możesz również [pobrać listę wszystkich zamówień dla określonego klienta](get-all-of-a-customer-s-orders.md).

>[!NOTE]
>Po przesłaniu zamówienia istnieje opóźnienie do 15 minut, po upływie którego zamówienie zostanie wyświetlone na liście zamówienie tego klienta.

## <a name="manage-azure-plans"></a>Zarządzanie planami platformy Azure

Po pomyślnym przetworzeniu zamówienia zostanie utworzony zasób **subskrypcji** Centrum partnerskiego dla planu platformy Azure. Aby zarządzać planem platformy Azure, można użyć następujących metod zarządzania zasobami **subskrypcji** Centrum partnerskiego:

* [Pobieranie subskrypcji klienta](get-all-of-a-customer-s-subscriptions.md)
* [Pobieranie listy subskrypcji według zamówienia](get-a-list-of-subscriptions-by-order.md)

Po utworzeniu planu platformy Azure w centrum partnerskim zostanie również utworzona odpowiednia subskrypcja użycia platformy Azure na platformie Azure. Możesz również utworzyć dodatkowe subskrypcje użycia platformy Azure w ramach tego samego planu platformy Azure przy użyciu witryny Azure Portal i interfejsów API platformy Azure. Identyfikatory wszystkich subskrypcji użycia platformy Azure skojarzonych z planem platformy Azure można uzyskać, wykonując czynności opisane w sekcji [Uzyskiwanie listy uprawnień platformy Azure na potrzeby subskrypcji Centrum partnerskiego](get-a-list-of-azure-entitlements-for-subscription.md)

## <a name="lifecycle-management"></a>Zarządzanie cyklem życia

Istniejący plan platformy Azure można wstrzymać, wykonując czynności opisane w sekcji [wstrzymywanie subskrypcji](suspend-a-subscription.md).

*Istniejący plan platformy Azure można wstrzymać tylko wtedy, gdy nie ma już skojarzonych aktywnych zasobów użycia, w tym subskrypcji użycia platformy Azure i rezerwacji platformy Azure.*

Aby uzyskać szczegółowe informacje na temat sposobu wyłączania subskrypcji użycia platformy Azure, zobacz [Azure API on Subscription Management](/rest/api/resources/subscriptions).

Aby usunąć istniejące rezerwacje platformy Azure, musisz [anulować rezerwacje](/partner-center/azure-reservations-manage#cancel-or-exchange-a-reservation).
Po zawieszeniu planu platformy Azure Możesz go uaktywnić ponownie.

Aby uzyskać szczegółowe informacje na temat ponownego uaktywnienia planu platformy Azure, zobacz [Ponowne uaktywnianie zawieszonej subskrypcji](reactivate-a-suspended-a-subscription.md)

## <a name="transition-existing-csp-offers-to-azure-plan"></a>Przenoszenie istniejących ofert CSP do planu platformy Azure

Nie możesz utworzyć planu platformy Azure dla istniejącego klienta z subskrypcją platformy Microsoft Azure (MS-AZR-0145P). Możesz jednak [przenieść klienta z istniejących ofert dostawcy CSP Azure do usług platformy Azure w ramach planu platformy Azure](/partner-center/azure-plan-transition) w nowym środowisku handlowym w programie CSP z poziomu Centrum partnerskiego. Aby przenieść istniejącego klienta, użyj interfejsów API uaktualniania produktów i wykonaj następujące czynności:

* [Sprawdź, czy klient kwalifikuje się do przeniesienia do planu platformy Azure](get-eligibility-for-product-upgrade.md)
* [Zainicjuj uaktualnienia produktu dla klienta](create-product-upgrade-entity.md)
* [Sprawdź stan uaktualnienia produktu](get-product-upgrade-status.md)

## <a name="azure-spending"></a>Wydatki na platformie Azure

[Wydatki na platformę Azure](azure-spending.md) można śledzić, wykonując zapytania dotyczące podsumowania użycia i szczegółowych rekordów użycia przy użyciu następujących metod:

* [Pobieranie podsumowania użycia przez partnera](get-a-partner-usage-summary.md)
* [Pobieranie wszystkich rekordów dotyczących użycia przez klientów dla partnera](get-a-customer-s-usage-records.md)
* [Pobieranie podsumowania użycia przez klienta](get-a-customer-usage-summary.md)
* [Pobieranie wszystkich rekordów dotyczących użycia subskrypcji dla klienta](get-a-customer-subscription-s-usage-records.md)
* [Pobieranie podsumowania użycia subskrypcji](get-a-customer-subscription-usage-summary.md)
* [Pobieranie danych dotyczących użycia dla subskrypcji według zasobu](get-a-customer-subscription-resource-usage-records.md)
* [Pobieranie danych dotyczących użycia dla subskrypcji według miernika](get-a-customer-subscription-meter-usage-records.md)
* [Pobieranie zasobów rekordu użycia miernika](meter-usage-resources.md)
* [Pobieranie zasobów rekordu użycia zasobu](resource-usage-resources.md)

Możesz również ustawić i zarządzać budżetem użycia klienta przy użyciu następujących metod:

* [Pobieranie budżetu użycia klienta](get-a-customer-s-usage-spending-budget.md)
* [Aktualizowanie budżetu użycia klienta](update-a-customer-s-usage-spending-budget.md)

## <a name="invoice-and-reconciliation"></a>Faktura i uzgadnianie

Można zarządzać fakturami i danymi uzgadnianymi przy użyciu następujących metod:

* [Pobieranie kolekcji faktur](get-a-collection-of-invoices.md)
* [Pobieranie linków do szacunkowych faktur](get-invoice-estimate-links.md)
* [Pobierz fakturę według identyfikatora](get-invoice-by-id.md)
* [Pobieranie zestawienia faktur](get-invoice-statement.md)
* [Pobieranie podsumowania faktur](get-invoice-summaries.md)
* [Pobieranie zafakturowanych elementów wiersza dotyczących zużycia](get-invoice-billed-consumption-lineitems.md)
* [Pobieranie niezafakturowanych elementów wiersza dotyczących zużycia](get-invoice-unbilled-consumption-lineitems.md)
* [Pobierz faktury rozliczane za Rekonesans wierszy](get-invoiceline-items.md)
* [Pobieranie niezafakturowanych elementów wiersza uzgodnienia](get-invoice-unbilled-recon-lineitems.md)
