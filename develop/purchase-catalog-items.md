---
title: Zakup elementów z katalogu
description: Jak kupować elementy katalogu przy użyciu interfejsu API Partner Center API.
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d3e0deedff194b1c836d9266c2201a2b3a52cc1b
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445361"
---
# <a name="purchase-catalog-items"></a>Zakup elementów z katalogu

W poniższym scenariuszu przedstawiono ogólny proces kupowania elementów z katalogu przy użyciu interfejsu API Partner Center API.

## <a name="discovery"></a>Odnajdywanie

Wybierz produkty i jednostki magazynowe (SKU) i sprawdź ich dostępność przy użyciu następujących Partner Center API:

- [Produkt](product-resources.md#product) — konstrukcja grupowania dla towarów lub usług, które można kupować. Sam produkt nie jest elementem do kupienia.
- [SKU](product-resources.md#sku) — zakupna sku w ramach produktu. Reprezentują one różne kształty produktu.
- [Dostępność](product-resources.md#availability) — konfiguracja, w której można kupić sku SKU (na przykład kraj, waluta i segment branży).

Aby kupić element z katalogu, wykonaj następujące czynności:

1. Zidentyfikuj i pobierz produkty i sku, które chcesz zakupić.

   - [Uzyskiwanie listy produktów](get-a-list-of-products.md)
   - [Uzyskiwanie produktu przy użyciu identyfikatora produktu](get-a-product-by-id.md)
   - [Uzyskiwanie listy jednostki SKU dla produktu](get-a-list-of-skus-for-a-product.md)
   - [Uzyskiwanie sku przy użyciu identyfikatora SKU](get-a-sku-by-id.md)

2. Sprawdź spis dla sku. Ten krok jest wymagany tylko w przypadku jednostki SKU, które są oznaczone wartością **InventoryCheck** we właściwości [purchasePrerequisites.](product-resources.md#sku)

   - [Sprawdzenie spisu](check-inventory.md)

3. Pobierz dostępność [dla](product-resources.md#availability) usługi [SKU](product-resources.md#sku). Podczas składania zamówienia będziesz potrzebować wartości **CatalogItemId** dostępności. Aby uzyskać tę wartość, użyj jednego z następujących interfejsów API:

   - [Uzyskiwanie listy dostępności dla sku](get-a-list-of-availabilities-for-a-sku.md)
   - [Uzyskiwanie dostępności przy użyciu identyfikatora dostępności](get-an-availability-by-id.md)

## <a name="order-submission"></a>Przesyłanie zamówienia

Aby przesłać zamówienie elementu katalogu, wykonaj następujące czynności:

1. Utwórz koszyk [do](cart-resources.md) przechowywania kolekcji elementów katalogu, które zamierzasz kupić. Podczas tworzenia koszyka elementy [](cart-resources.md#cartlineitem) wiersza koszyka są automatycznie grupowane w oparciu o elementy, które można kupić razem w tym samym [zamówieniu](order-resources.md).

   - [Tworzenie koszyka](create-a-cart.md)
   - [Aktualizowanie koszyka](update-a-cart.md)

2. Wyewidencj go. Wyeencjonuj koszyk powoduje utworzenie [zamówienia](order-resources.md).

   - [Finalizacji zakupu koszyka](checkout-a-cart.md)

## <a name="get-order-details"></a>Uzyskiwanie szczegółów zamówienia

Szczegóły pojedynczego zamówienia można pobrać przy użyciu identyfikatora zamówienia lub listy zamówień dla klienta. Istnieje opóźnienie do 15 minut między czasem, w którym zamówienie zostanie przesłane, a tym samym pojawi się na liście zamówień klienta.

- Zobacz [Get an order by ID (Uzyskiwanie](get-an-order-by-id.md) zamówienia według identyfikatora), aby uzyskać szczegółowe informacje o indywidualnym zamówieniu przy użyciu identyfikatorów zamówień.

- Zobacz [Get all of a customer's orders](get-all-of-a-customer-s-orders.md) (Uzyskiwanie wszystkich zamówień klienta), aby uzyskać listę zamówień dla klienta przy użyciu identyfikatora klienta.

- Zobacz Artykuł Get a list of orders [by customer and billing](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) [](product-resources.md#billingcycletype) cycle type (Uzyskiwanie listy zamówień według typu klienta i cyklu rozliczeniowego), aby uzyskać listę zamówień klienta według typu cyklu rozliczeniowego, co pozwala na oddzielną listę zamówień pozycji katalogu (opłaty godzinowe) i roczne lub miesięczne zamówienia rozliczane oddzielnie.

## <a name="lifecycle-management"></a>Zarządzanie cyklem życia

W ramach zarządzania cyklem życia elementów katalogu w programie Partner Center można [](entitlement-resources.md)pobrać informacje o uprawnieniach elementu katalogu i uzyskać szczegóły rezerwacji przy użyciu identyfikatora zamówienia rezerwacji. Aby uzyskać przykłady, jak to zrobić, [zobacz Get entitlements (Uzyskiwanie uprawnień).](get-a-collection-of-entitlements.md)   

## <a name="invoice-and-reconciliation"></a>Faktury i uzgadnianie

Poniższe scenariusze pokazują, jak programowo wyświetlać [](invoice-resources.md)faktury klienta oraz pobierać salda i podsumowania konta, które obejmują opłaty za pozycje katalogu.

### <a name="balance-and-payment"></a>Saldo i płatność

Aby uzyskać bieżące saldo konta w domyślnym typie waluty, które jest saldem opłat cyklicznych i jednorazowych (element katalogu), zobacz Get your current account balance (Uzyskiwanie [bieżącego salda konta).](get-the-reseller-s-current-account-balance.md)

### <a name="multi-currency-balance-and-payment"></a>Saldo i płatność w wielu walutach

Aby uzyskać bieżące saldo konta i kolekcję podsumowań faktur zawierających podsumowanie faktury z opłatami cyklicznym i jednorazowym dla każdego typu waluty klienta, zobacz Pobieranie podsumowań [faktur](get-invoice-summaries.md).

### <a name="invoices"></a>Faktury

Aby uzyskać kolekcję faktur, które pokazują opłaty cykliczne i [jednorazowe, zobacz Pobieranie kolekcji faktur.](get-a-collection-of-invoices.md) 

### <a name="single-invoice"></a>Pojedyncza faktura

Aby pobrać określoną fakturę przy użyciu identyfikatora faktury, zobacz [Pobieranie faktury według identyfikatora](get-invoice-by-id.md).  

### <a name="reconciliation"></a>Pojednania

Aby uzyskać kolekcję szczegółów pozycji faktury (pozycje uzgodnień) dla określonego identyfikatora faktury, zobacz [Pobieranie pozycji faktury.](get-invoiceline-items.md)  

### <a name="download-an-invoice-as-a-pdf"></a>Pobieranie faktury w formacie PDF

Aby pobrać zestawienie faktur w formacie PDF przy użyciu identyfikatora faktury, zobacz [Pobieranie zestawienia faktury.](get-invoice-statement.md)
