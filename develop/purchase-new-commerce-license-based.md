---
title: Kupowanie nowych usług opartych na licencjach handlowych
description: Deweloperzy mogą kupować i tworzyć nowe usługi oparte na licencjach handlowych oraz zarządzać nimi przy użyciu Partner Center API.
ms.date: 02/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: dd3aebdb0a670449d3a39f67fc2ad6c7ef8df8e5
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/03/2021
ms.locfileid: "123457315"
---
# <a name="purchasing-new-commerce-license-based-services"></a>Kupowanie nowych usług opartych na licencjach handlowych

**Dotyczy:**

* Centrum partnerskie

> [!Note] 
> Nowe zmiany w handlu są obecnie dostępne tylko dla partnerów, którzy są częścią nowego doświadczenia handlowego M365/D365 w wersji Technical Preview.

Możesz kupować i tworzyć usługi oparte na licencjach w nowym interfejsie handlowym oraz zarządzać nimi przy użyciu Partner Center API. Proces jest podobny do tego w przypadku ofert planu platformy Azure i witryny Marketplace.

## <a name="prerequisites"></a>Wymagania wstępne

* [Partner Center poświadczenia](partner-center-authentication.md) uwierzytelniania. Nowe środowisko handlowe obsługuje uwierzytelnianie zarówno przy użyciu autonomicznej aplikacji, jak i poświadczeń aplikacji i użytkownika.
* Identyfikator klienta. Jeśli nie masz identyfikatora klienta, wykonaj kroki opisane w te tematu Get a list of customers (Uzyskiwanie [listy klientów).](get-a-list-of-customers.md) Możesz też zalogować się do Partner Center, wybrać klienta z listy klientów, wybrać pozycję **Konto**, a następnie zapisać **jego identyfikator Microsoft.**
* [Potwierdzenie akceptacji przez klienta](/partner-center/confirm-customer-agreement)Umowa z Klientem Microsoft .

## <a name="get-the-catalog-item-for-new-commerce-license-based-services"></a>Pobierz element katalogu dla nowych usług opartych na licencjach handlowych

Musisz pobrać nowe pozycje katalogu usług opartych na licencjach handlowych. Pobierz elementy katalogu przy użyciu istniejących interfejsów API Partner Center wykazu zasobów z następującymi modelami zasobów:

* **[Produkt:](product-resources.md#product)** Konstrukcja grupowania dla towarów lub usług, które można kupować. Sam produkt nie jest elementem do zakupu.
* **[Jednostka SKU:](product-resources.md#sku)** jednostka magazynowa (SKU) do zakupu w ramach produktu. Jednostki SKU reprezentują różne kształty produktu.
* **[Dostępność:](product-resources.md#availability)** konfiguracja, w której można kupić sku (na przykład kraj, waluta lub segment branży).

Aby uzyskać elementy katalogu dla nowych ofert usług opartych na licencjach handlowych:

1. Wykonaj kroki opisane w [te tematu Get a list of products](get-a-list-of-products.md) (Uzyskiwanie listy produktów dla produktów) i określ element **targetView** jako **OnlineServices ( OnlineServices).** (Jeśli znasz już identyfikator produktu dla oferty, którą chcesz kupić, możesz wykonać kroki opisane w te tematu Get [a product using the product ID](get-a-product-by-id.md) instead (Uzyskiwanie produktu przy użyciu identyfikatora produktu).

2. Pobierz **sku z** produktu dla oferty, którego szukasz. Wykonaj kroki opisane w [te tematu Get a list of SKUs for a product (Uzyskiwanie listy jednostki SKU dla produktu).](get-a-list-of-skus-for-a-product.md) (Jeśli znasz już identyfikator jednostki SKU dla chętnych ofert, możesz wykonać kroki opisane w te tematu Get a SKU using the SKU ID instead (Uzyskiwanie jednostki SKU przy użyciu identyfikatora [jednostki SKU).](get-a-sku-by-id.md)

3. Pobierz dostępność **z** usługi SKU dla oferty. Różne oferty obsługują określone warunki. Niektóre jednostki SKU mają więcej niż jedną dostępność. Wykonaj kroki opisane w [te tematu Get a list of availabilities for a SKU](get-a-list-of-availabilities-for-a-sku.md)(Uzyskiwanie listy dostępności dla SKU). (Jeśli znasz już identyfikator potrzebnej dostępności, możesz wykonać kroki opisane w te tematu Uzyskiwanie dostępności przy użyciu [identyfikatora](get-an-availability-by-id.md) dostępności). *Pamiętaj, aby zanotować wartość właściwości **CatalogItemId** dostępności oferty. Ta wartość będzie potrzebna do utworzenia zamówienia*.

## <a name="create-and-submit-an-order"></a>Tworzenie i przesyłanie zamówienia

Aby przesłać zamówienie dotyczące planu platformy Azure (w tym nowych zamówień handlowych), wykonaj następujące kroki:

1. [Utwórz koszyk do](create-a-cart.md) przechowywania kolekcji elementów katalogu, które zamierzasz kupić. Po utworzeniu [koszyka](cart-resources.md#cart)elementy [wiersza](cart-resources.md#cartlineitem) koszyka są automatycznie grupowane w oparciu o elementy, które można kupić razem w tym samym [zamówieniu.](order-resources.md#order) (Możesz również [zaktualizować koszyk).](update-a-cart.md)

2. [Zapoznaj się z koszykiem](checkout-a-cart.md), co powoduje utworzenie [zamówienia](order-resources.md#order).

## <a name="get-order-details"></a>Uzyskiwanie szczegółów zamówienia

Szczegóły pojedynczego [zamówienia można pobrać przy użyciu identyfikatora zamówienia](get-an-order-by-id.md). Możesz również [pobrać listę wszystkich zamówień dla określonego klienta.](get-all-of-a-customer-s-orders.md)

>[!NOTE]
>Po przesłaniu zamówienia istnieje opóźnienie do 15 minut, zanim zamówienie pojawi się na liście zamówień tego klienta. Obecnie partnerzy z UE mogą kupować tylko nowe oferty handlowe dla: 1. Nowi klienci 2. Istniejący klienci, którzy nie mają wcześniej istniejącego planu platformy Azure, platformy handlowej, subskrypcji oprogramowania lub oprogramowania bezterminowego w walucie innej niż waluta kraju partnera.

## <a name="manage-new-commerce-subscriptions"></a>Zarządzanie nowymi subskrypcjami handlowymi

Po pomyślnym przetworzeniu zamówienia zostanie utworzony zasób Partner Center **Subskrypcji** dla planu platformy Azure. Następujące metody zarządzania zasobami subskrypcji usługi Partner Center **do** zarządzania planem platformy Azure:

* [Pobieranie subskrypcji klienta](get-all-of-a-customer-s-subscriptions.md)
* [Pobieranie listy subskrypcji według zamówienia](get-a-list-of-subscriptions-by-order.md)

Istnieją różnice i nowe możliwości specyficzne dla nowego handlu.

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
