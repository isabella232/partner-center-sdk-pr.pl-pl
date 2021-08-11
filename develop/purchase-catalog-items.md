---
title: Zakup elementów z katalogu
description: Jak kupować elementy katalogu przy użyciu interfejsu API Partner Center API.
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 34560ceff2721a805d50cd4bf0702f6e7cf6f473db3f38ee52ea439b7355b786
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997346"
---
# <a name="purchase-catalog-items"></a>Zakup elementów z katalogu

W poniższym scenariuszu przedstawiono ogólny proces kupowania elementów z katalogu przy użyciu interfejsu API Partner Center API.

## <a name="discovery"></a>Odnajdywanie

Wybierz produkty i jednostki magazynowe (SKU) i sprawdź ich dostępność przy użyciu następujących modeli Partner Center API:

- [Produkt](product-resources.md#product) — konstrukcja grupowania dla produktów lub usług, które można kupować. Sam produkt nie jest elementem do kupienia.
- [SKU](product-resources.md#sku) — zakupna sku w ramach produktu. Reprezentują one różne kształty produktu.
- [Dostępność](product-resources.md#availability) — konfiguracja, w której można kupić sku (na przykład kraj, waluta i segment branży).

Aby kupić element z katalogu, wykonaj następujące czynności:

1. Zidentyfikuj i pobierz produkt i sku, które chcesz kupić.

   - [Uzyskiwanie listy produktów](get-a-list-of-products.md)
   - [Uzyskiwanie produktu przy użyciu identyfikatora produktu](get-a-product-by-id.md)
   - [Uzyskiwanie listy jednostki SKU dla produktu](get-a-list-of-skus-for-a-product.md)
   - [Uzyskiwanie sku przy użyciu identyfikatora SKU](get-a-sku-by-id.md)

2. Sprawdź spis dla sku. Ten krok jest wymagany tylko w przypadku jednostki SKU, które są oznaczone wartością **InventoryCheck** we właściwości [purchasePrerequisites.](product-resources.md#sku)

   - [Sprawdzenie spisu](check-inventory.md)

3. Pobierz dostępność [dla](product-resources.md#availability) [SKU](product-resources.md#sku). Podczas składania zamówienia będziesz potrzebować wartości **CatalogItemId** dostępności. Aby uzyskać tę wartość, użyj jednego z następujących interfejsów API:

   - [Uzyskiwanie listy dostępności dla sku](get-a-list-of-availabilities-for-a-sku.md)
   - [Uzyskiwanie dostępności przy użyciu identyfikatora dostępności](get-an-availability-by-id.md)

## <a name="order-submission"></a>Przesyłanie zamówienia

Aby przesłać zamówienie elementu katalogu, wykonaj następujące czynności:

1. Utwórz [koszyk](cart-resources.md) do przechowywania kolekcji elementów katalogu, które zamierzasz kupić. Podczas tworzenia koszyka elementy [](cart-resources.md#cartlineitem) wiersza koszyka są automatycznie grupowane na podstawie elementów, które można kupić razem w tym samym [zamówieniu.](order-resources.md)

   - [Tworzenie koszyka](create-a-cart.md)
   - [Aktualizowanie koszyka](update-a-cart.md)

2. Zapoznaj się z koszykiem. Wyeencjonuj koszyk powoduje utworzenie [zamówienia](order-resources.md).

   - [Finalizacji zakupu koszyka](checkout-a-cart.md)

## <a name="get-order-details"></a>Uzyskiwanie szczegółów zamówienia

Szczegóły indywidualnego zamówienia możesz pobrać przy użyciu identyfikatora zamówienia lub uzyskać listę zamówień dla klienta. Istnieje opóźnienie do 15 minut między tym, kiedy zamówienie zostanie przesłane, a kiedy pojawi się na liście zamówień klienta.

- Zobacz [Get an order by ID (Uzyskiwanie](get-an-order-by-id.md) zamówienia według identyfikatora), aby uzyskać szczegółowe informacje o indywidualnym zamówieniu przy użyciu identyfikatorów zamówień.

- Zobacz [Get all of a customer's orders](get-all-of-a-customer-s-orders.md) to get a list of orders for a customer using the customer ID (Uzyskiwanie wszystkich zamówień klienta), aby uzyskać listę zamówień dla klienta przy użyciu identyfikatora klienta.

- Zobacz Artykuł Get a list of orders by customer and billing [](product-resources.md#billingcycletype) cycle [type](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) (Uzyskiwanie listy zamówień według klienta i typu cyklu rozliczeniowego), aby uzyskać listę zamówień dla klienta według typu cyklu rozliczeniowego, co pozwala oddzielnie wyświetlić listę zamówień pozycji katalogu (opłaty razowe) i roczne lub miesięczne rozliczane zamówienia.

## <a name="lifecycle-management"></a>Zarządzanie cyklem życia

W ramach zarządzania cyklem życia elementów katalogu w programie Partner Center można [](entitlement-resources.md)pobrać informacje o uprawnieniach elementu katalogu i uzyskać szczegóły rezerwacji przy użyciu identyfikatora zamówienia rezerwacji. Aby uzyskać przykłady, jak to zrobić, zobacz [Get entitlements (Uzyskiwanie uprawnień).](get-a-collection-of-entitlements.md)   

## <a name="invoice-and-reconciliation"></a>Faktura i uzgadnianie

Poniższe scenariusze pokazują, jak programowo wyświetlać [](invoice-resources.md)faktury klienta oraz pobierać salda i podsumowania konta, które obejmują opłaty za pozycje katalogu.

### <a name="balance-and-payment"></a>Saldo i płatność

Aby uzyskać bieżące saldo konta w domyślnym typie waluty, które jest saldem opłat cyklicznych i jednorazowych (element katalogu), zobacz Get your current account balance (Uzyskiwanie [bieżącego salda konta).](get-the-reseller-s-current-account-balance.md)

### <a name="multi-currency-balance-and-payment"></a>Saldo i płatność w wielu walutach

Aby uzyskać bieżące saldo konta i kolekcję podsumowań faktur zawierających podsumowanie faktury z opłatami cyklicznym i jednorazowym dla każdego typu waluty klienta, zobacz Pobieranie podsumowań [faktur](get-invoice-summaries.md).

### <a name="invoices"></a>Faktury

Aby uzyskać kolekcję faktur, które pokazują opłaty cykliczne i [jednorazowe,](get-a-collection-of-invoices.md)zobacz Pobieranie kolekcji faktur . 

### <a name="single-invoice"></a>Pojedyncza faktura

Aby pobrać określoną fakturę przy użyciu identyfikatora faktury, zobacz [Pobieranie faktury według identyfikatora](get-invoice-by-id.md).  

### <a name="reconciliation"></a>Pojednania

Aby uzyskać kolekcję szczegółów pozycji faktury (pozycje uzgodnień) dla określonego identyfikatora faktury, zobacz [Pobieranie pozycji faktury](get-invoiceline-items.md).  

### <a name="download-an-invoice-as-a-pdf"></a>Pobieranie faktury w formacie PDF

Aby pobrać zestawienie faktur w formacie PDF przy użyciu identyfikatora faktury, zobacz [Pobieranie zestawienia faktury.](get-invoice-statement.md)
