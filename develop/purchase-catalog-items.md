---
title: Zakup elementów z katalogu
description: Jak kupić elementy katalogu przy użyciu interfejsu API Centrum partnerskiego.
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f2b3a34cdb6b29cb7eaaf5d977e4588f538fff09
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767797"
---
# <a name="purchase-catalog-items"></a>Zakup elementów z katalogu

**Dotyczy**

- Centrum partnerskie

W poniższym scenariuszu przedstawiono ogólny proces kupowania elementów z katalogu przy użyciu interfejsu API Centrum partnerskiego.

## <a name="discovery"></a>Odnajdywanie

Wybierz produkty i jednostki SKU i sprawdź ich dostępność przy użyciu następujących modeli interfejsu API Centrum partnerskiego:

- [Product](product-resources.md#product) -konstrukcja grupująca dla jednostek towarów lub usług. Produkt nie jest elementem jednostek.
- [SKU](product-resources.md#sku) — jednostka magazynowa jednostek (SKU) w ramach produktu. Reprezentują one różne kształty produktu.
- [Dostępność](product-resources.md#availability) — konfiguracja, w której jednostka SKU jest dostępna do zakupu (na przykład kraj, waluta i segment branżowy).

Aby kupić element z wykazu, wykonaj następujące czynności:

1. Zidentyfikuj i Pobierz produkt i jednostkę SKU, które chcesz kupić.

   - [Pobierz listę produktów](get-a-list-of-products.md)
   - [Uzyskiwanie produktu przy użyciu identyfikatora produktu](get-a-product-by-id.md)
   - [Pobierz listę jednostek SKU dla produktu](get-a-list-of-skus-for-a-product.md)
   - [Pobierz jednostkę SKU przy użyciu identyfikatora jednostki SKU](get-a-sku-by-id.md)

2. Sprawdź spis dla jednostki SKU. Ten krok jest wymagany tylko w przypadku jednostek SKU, które są oznaczone wartością **InventoryCheck** we właściwości [purchasePrerequisites](product-resources.md#sku) .

   - [Sprawdzenie spisu](check-inventory.md)

3. Pobierz [dostępność](product-resources.md#availability) dla [jednostki SKU](product-resources.md#sku). Podczas umieszczania zamówienia będzie potrzebna **CatalogItemId** dostępność. Aby uzyskać tę wartość, użyj jednego z następujących interfejsów API:

   - [Pobierz listę dostępność dla jednostki SKU](get-a-list-of-availabilities-for-a-sku.md)
   - [Uzyskaj dostępność przy użyciu identyfikatora dostępności](get-an-availability-by-id.md)

## <a name="order-submission"></a>Przesyłanie zamówienia

Aby przesłać zamówienie elementu katalogu, wykonaj następujące czynności:

1. Utwórz [koszyk](cart-resources.md) do przechowywania kolekcji elementów wykazu, które zamierzasz kupić. Podczas tworzenia koszyka [elementy w linii koszyka](cart-resources.md#cartlineitem) są automatycznie grupowane na podstawie tego, co można zakupić razem w tej samej [kolejności](order-resources.md).

   - [Tworzenie koszyka](create-a-cart.md)
   - [Aktualizowanie koszyka](update-a-cart.md)

2. Sprawdź koszyk. Wyewidencjonowanie koszyka powoduje utworzenie [zamówienia](order-resources.md).

   - [Wyewidencjonuj koszyk](checkout-a-cart.md)

## <a name="get-order-details"></a>Pobierz szczegóły zamówienia

Możesz pobrać szczegóły pojedynczego zamówienia przy użyciu identyfikatora zamówienia lub uzyskać listę zamówień dla klienta. Istnieje opóźnienie do 15 minut od momentu, gdy zamówienie zostanie przesłane i pojawi się na liście zamówień klienta.

- Zobacz [Pobierz zamówienie według identyfikatora](get-an-order-by-id.md) , aby uzyskać szczegółowe informacje o poszczególnych zamówieniach, korzystając z identyfikatorów zamówień.

- Zobacz [Pobierz wszystkie zamówienia klienta](get-all-of-a-customer-s-orders.md) , aby uzyskać listę zamówień dla klienta przy użyciu identyfikatora klienta.

- Aby uzyskać listę zamówień dla klienta według [typu cyklu rozliczeniowego](product-resources.md#billingcycletype) , należy zapoznać się z listą zakupów [według numerów klientów i rozliczeń](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) , co pozwala na wyświetlanie listy zamówień dotyczących elementów katalogu (opłat jednorazowych) oraz zamówień rocznych i miesięcznych.

## <a name="lifecycle-management"></a>Zarządzanie cyklem życia

W ramach zarządzania cyklem życia elementów katalogu w centrum partnerskim można pobrać informacje o [uprawnieniach](entitlement-resources.md)elementów katalogu i uzyskać szczegółowe informacje dotyczące rezerwacji przy użyciu identyfikatora zamówienia rezerwacji. Aby zapoznać się z przykładami, zobacz [Uzyskaj uprawnienia](get-a-collection-of-entitlements.md).   

## <a name="invoice-and-reconciliation"></a>Faktura i uzgadnianie

W poniższych scenariuszach pokazano, jak programowo wyświetlić [faktury](invoice-resources.md)klienta i uzyskać salda konta oraz podsumowania, które zawierają opłaty jednorazowe dla elementów katalogu.

### <a name="balance-and-payment"></a>Saldo i płatność

Aby uzyskać bieżące saldo konta w domyślnym typie waluty, który jest bilansem opłat cyklicznych i jednorazowych (element katalogu), zobacz [pobieranie bieżącego salda konta](get-the-reseller-s-current-account-balance.md).

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
