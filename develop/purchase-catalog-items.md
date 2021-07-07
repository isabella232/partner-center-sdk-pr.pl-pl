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
# <a name="purchase-catalog-items"></a><span data-ttu-id="6cfad-103">Zakup elementów z katalogu</span><span class="sxs-lookup"><span data-stu-id="6cfad-103">Purchase catalog items</span></span>

<span data-ttu-id="6cfad-104">W poniższym scenariuszu przedstawiono ogólny proces kupowania elementów z katalogu przy użyciu interfejsu API Partner Center API.</span><span class="sxs-lookup"><span data-stu-id="6cfad-104">The following scenario demonstrates the generic process for purchasing items from the catalog by using the Partner Center API.</span></span>

## <a name="discovery"></a><span data-ttu-id="6cfad-105">Odnajdywanie</span><span class="sxs-lookup"><span data-stu-id="6cfad-105">Discovery</span></span>

<span data-ttu-id="6cfad-106">Wybierz produkty i jednostki magazynowe (SKU) i sprawdź ich dostępność przy użyciu następujących Partner Center API:</span><span class="sxs-lookup"><span data-stu-id="6cfad-106">Select products and Stock Keeping Units (SKUs) and check their availability using the following Partner Center API models:</span></span>

- <span data-ttu-id="6cfad-107">[Produkt](product-resources.md#product) — konstrukcja grupowania dla towarów lub usług, które można kupować.</span><span class="sxs-lookup"><span data-stu-id="6cfad-107">[Product](product-resources.md#product) - A grouping construct for purchasable goods or services.</span></span> <span data-ttu-id="6cfad-108">Sam produkt nie jest elementem do kupienia.</span><span class="sxs-lookup"><span data-stu-id="6cfad-108">A product by itself isn't a purchasable item.</span></span>
- <span data-ttu-id="6cfad-109">[SKU](product-resources.md#sku) — zakupna sku w ramach produktu.</span><span class="sxs-lookup"><span data-stu-id="6cfad-109">[SKU](product-resources.md#sku) - A purchasable SKU under a product.</span></span> <span data-ttu-id="6cfad-110">Reprezentują one różne kształty produktu.</span><span class="sxs-lookup"><span data-stu-id="6cfad-110">These represent the different shapes of the product.</span></span>
- <span data-ttu-id="6cfad-111">[Dostępność](product-resources.md#availability) — konfiguracja, w której można kupić sku SKU (na przykład kraj, waluta i segment branży).</span><span class="sxs-lookup"><span data-stu-id="6cfad-111">[Availability](product-resources.md#availability) - A configuration in which a SKU is available for purchase (such as country, currency, and industry segment).</span></span>

<span data-ttu-id="6cfad-112">Aby kupić element z katalogu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6cfad-112">To purchase an item from the catalog, complete the following steps:</span></span>

1. <span data-ttu-id="6cfad-113">Zidentyfikuj i pobierz produkty i sku, które chcesz zakupić.</span><span class="sxs-lookup"><span data-stu-id="6cfad-113">Identify and retrieve the Product and SKU that you want to purchase.</span></span>

   - [<span data-ttu-id="6cfad-114">Uzyskiwanie listy produktów</span><span class="sxs-lookup"><span data-stu-id="6cfad-114">Get a list of products</span></span>](get-a-list-of-products.md)
   - [<span data-ttu-id="6cfad-115">Uzyskiwanie produktu przy użyciu identyfikatora produktu</span><span class="sxs-lookup"><span data-stu-id="6cfad-115">Get a product using the product ID</span></span>](get-a-product-by-id.md)
   - [<span data-ttu-id="6cfad-116">Uzyskiwanie listy jednostki SKU dla produktu</span><span class="sxs-lookup"><span data-stu-id="6cfad-116">Get a list of SKUs for a product</span></span>](get-a-list-of-skus-for-a-product.md)
   - [<span data-ttu-id="6cfad-117">Uzyskiwanie sku przy użyciu identyfikatora SKU</span><span class="sxs-lookup"><span data-stu-id="6cfad-117">Get a SKU using the SKU ID</span></span>](get-a-sku-by-id.md)

2. <span data-ttu-id="6cfad-118">Sprawdź spis dla sku.</span><span class="sxs-lookup"><span data-stu-id="6cfad-118">Check the inventory for a SKU.</span></span> <span data-ttu-id="6cfad-119">Ten krok jest wymagany tylko w przypadku jednostki SKU, które są oznaczone wartością **InventoryCheck** we właściwości [purchasePrerequisites.](product-resources.md#sku)</span><span class="sxs-lookup"><span data-stu-id="6cfad-119">This step is only needed for SKUs that are tagged with an **InventoryCheck** value in the [purchasePrerequisites](product-resources.md#sku) property.</span></span>

   - [<span data-ttu-id="6cfad-120">Sprawdzenie spisu</span><span class="sxs-lookup"><span data-stu-id="6cfad-120">Check Inventory</span></span>](check-inventory.md)

3. <span data-ttu-id="6cfad-121">Pobierz dostępność [dla](product-resources.md#availability) usługi [SKU](product-resources.md#sku).</span><span class="sxs-lookup"><span data-stu-id="6cfad-121">Retrieve the [availability](product-resources.md#availability) for the [SKU](product-resources.md#sku).</span></span> <span data-ttu-id="6cfad-122">Podczas składania zamówienia będziesz potrzebować wartości **CatalogItemId** dostępności.</span><span class="sxs-lookup"><span data-stu-id="6cfad-122">You will need the **CatalogItemId** of the availability when placing the order.</span></span> <span data-ttu-id="6cfad-123">Aby uzyskać tę wartość, użyj jednego z następujących interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="6cfad-123">To get this value, use one of the following APIs:</span></span>

   - [<span data-ttu-id="6cfad-124">Uzyskiwanie listy dostępności dla sku</span><span class="sxs-lookup"><span data-stu-id="6cfad-124">Get a list of availabilities for a SKU</span></span>](get-a-list-of-availabilities-for-a-sku.md)
   - [<span data-ttu-id="6cfad-125">Uzyskiwanie dostępności przy użyciu identyfikatora dostępności</span><span class="sxs-lookup"><span data-stu-id="6cfad-125">Get an availability using the availability ID</span></span>](get-an-availability-by-id.md)

## <a name="order-submission"></a><span data-ttu-id="6cfad-126">Przesyłanie zamówienia</span><span class="sxs-lookup"><span data-stu-id="6cfad-126">Order submission</span></span>

<span data-ttu-id="6cfad-127">Aby przesłać zamówienie elementu katalogu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6cfad-127">To submit your catalog item order, do the following:</span></span>

1. <span data-ttu-id="6cfad-128">Utwórz koszyk [do](cart-resources.md) przechowywania kolekcji elementów katalogu, które zamierzasz kupić.</span><span class="sxs-lookup"><span data-stu-id="6cfad-128">Create a [Cart](cart-resources.md) to hold the collection of catalog items that you intend to buy.</span></span> <span data-ttu-id="6cfad-129">Podczas tworzenia koszyka elementy [](cart-resources.md#cartlineitem) wiersza koszyka są automatycznie grupowane w oparciu o elementy, które można kupić razem w tym samym [zamówieniu](order-resources.md).</span><span class="sxs-lookup"><span data-stu-id="6cfad-129">When you create a cart, the [cart line items](cart-resources.md#cartlineitem) are automatically grouped based on what can be purchased together in the same [Order](order-resources.md).</span></span>

   - [<span data-ttu-id="6cfad-130">Tworzenie koszyka</span><span class="sxs-lookup"><span data-stu-id="6cfad-130">Create a shopping cart</span></span>](create-a-cart.md)
   - [<span data-ttu-id="6cfad-131">Aktualizowanie koszyka</span><span class="sxs-lookup"><span data-stu-id="6cfad-131">Update a shopping cart</span></span>](update-a-cart.md)

2. <span data-ttu-id="6cfad-132">Wyewidencj go.</span><span class="sxs-lookup"><span data-stu-id="6cfad-132">Check out the cart.</span></span> <span data-ttu-id="6cfad-133">Wyeencjonuj koszyk powoduje utworzenie [zamówienia](order-resources.md).</span><span class="sxs-lookup"><span data-stu-id="6cfad-133">Checking out a cart results in the creation of an [Order](order-resources.md).</span></span>

   - [<span data-ttu-id="6cfad-134">Finalizacji zakupu koszyka</span><span class="sxs-lookup"><span data-stu-id="6cfad-134">Checkout the cart</span></span>](checkout-a-cart.md)

## <a name="get-order-details"></a><span data-ttu-id="6cfad-135">Uzyskiwanie szczegółów zamówienia</span><span class="sxs-lookup"><span data-stu-id="6cfad-135">Get order details</span></span>

<span data-ttu-id="6cfad-136">Szczegóły pojedynczego zamówienia można pobrać przy użyciu identyfikatora zamówienia lub listy zamówień dla klienta.</span><span class="sxs-lookup"><span data-stu-id="6cfad-136">You can retrieve the details of an individual order using the order ID, or get a list of orders for a customer.</span></span> <span data-ttu-id="6cfad-137">Istnieje opóźnienie do 15 minut między czasem, w którym zamówienie zostanie przesłane, a tym samym pojawi się na liście zamówień klienta.</span><span class="sxs-lookup"><span data-stu-id="6cfad-137">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a list of a customer's orders.</span></span>

- <span data-ttu-id="6cfad-138">Zobacz [Get an order by ID (Uzyskiwanie](get-an-order-by-id.md) zamówienia według identyfikatora), aby uzyskać szczegółowe informacje o indywidualnym zamówieniu przy użyciu identyfikatorów zamówień.</span><span class="sxs-lookup"><span data-stu-id="6cfad-138">See [Get an order by ID](get-an-order-by-id.md) to get the details of an individual order using the order IDs.</span></span>

- <span data-ttu-id="6cfad-139">Zobacz [Get all of a customer's orders](get-all-of-a-customer-s-orders.md) (Uzyskiwanie wszystkich zamówień klienta), aby uzyskać listę zamówień dla klienta przy użyciu identyfikatora klienta.</span><span class="sxs-lookup"><span data-stu-id="6cfad-139">See [Get all of a customer's orders](get-all-of-a-customer-s-orders.md) to get a list of orders for a customer using the customer ID.</span></span>

- <span data-ttu-id="6cfad-140">Zobacz Artykuł Get a list of orders [by customer and billing](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) [](product-resources.md#billingcycletype) cycle type (Uzyskiwanie listy zamówień według typu klienta i cyklu rozliczeniowego), aby uzyskać listę zamówień klienta według typu cyklu rozliczeniowego, co pozwala na oddzielną listę zamówień pozycji katalogu (opłaty godzinowe) i roczne lub miesięczne zamówienia rozliczane oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="6cfad-140">See [Get a list of orders by customer and billing cycle type](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) to get a list of orders for a customer by [billing cycle type](product-resources.md#billingcycletype) allowing you to list catalog item orders (one-time charges) and annual or monthly billed orders separately.</span></span>

## <a name="lifecycle-management"></a><span data-ttu-id="6cfad-141">Zarządzanie cyklem życia</span><span class="sxs-lookup"><span data-stu-id="6cfad-141">Lifecycle management</span></span>

<span data-ttu-id="6cfad-142">W ramach zarządzania cyklem życia elementów katalogu w programie Partner Center można [](entitlement-resources.md)pobrać informacje o uprawnieniach elementu katalogu i uzyskać szczegóły rezerwacji przy użyciu identyfikatora zamówienia rezerwacji.</span><span class="sxs-lookup"><span data-stu-id="6cfad-142">As part of managing the lifecycle of your catalog items in Partner Center, you can retrieve information about your catalog item [Entitlements](entitlement-resources.md), and get reservation details using the reservation order ID.</span></span> <span data-ttu-id="6cfad-143">Aby uzyskać przykłady, jak to zrobić, [zobacz Get entitlements (Uzyskiwanie uprawnień).](get-a-collection-of-entitlements.md)</span><span class="sxs-lookup"><span data-stu-id="6cfad-143">For examples of how to do this, see [Get entitlements](get-a-collection-of-entitlements.md).</span></span>   

## <a name="invoice-and-reconciliation"></a><span data-ttu-id="6cfad-144">Faktury i uzgadnianie</span><span class="sxs-lookup"><span data-stu-id="6cfad-144">Invoice and reconciliation</span></span>

<span data-ttu-id="6cfad-145">Poniższe scenariusze pokazują, jak programowo wyświetlać [](invoice-resources.md)faktury klienta oraz pobierać salda i podsumowania konta, które obejmują opłaty za pozycje katalogu.</span><span class="sxs-lookup"><span data-stu-id="6cfad-145">The following scenarios show you how to programmatically view your customer's [invoices](invoice-resources.md), and get your account balances and summaries that include one-time charges for catalog items.</span></span>

### <a name="balance-and-payment"></a><span data-ttu-id="6cfad-146">Saldo i płatność</span><span class="sxs-lookup"><span data-stu-id="6cfad-146">Balance and payment</span></span>

<span data-ttu-id="6cfad-147">Aby uzyskać bieżące saldo konta w domyślnym typie waluty, które jest saldem opłat cyklicznych i jednorazowych (element katalogu), zobacz Get your current account balance (Uzyskiwanie [bieżącego salda konta).](get-the-reseller-s-current-account-balance.md)</span><span class="sxs-lookup"><span data-stu-id="6cfad-147">To get current account balance in your default currency type that is a balance of both recurring and one-time (catalog item) charges, see [Get your current account balance](get-the-reseller-s-current-account-balance.md).</span></span>

### <a name="multi-currency-balance-and-payment"></a><span data-ttu-id="6cfad-148">Saldo i płatność w wielu walutach</span><span class="sxs-lookup"><span data-stu-id="6cfad-148">Multi-currency balance and payment</span></span>

<span data-ttu-id="6cfad-149">Aby uzyskać bieżące saldo konta i kolekcję podsumowań faktur zawierających podsumowanie faktury z opłatami cyklicznym i jednorazowym dla każdego typu waluty klienta, zobacz Pobieranie podsumowań [faktur](get-invoice-summaries.md).</span><span class="sxs-lookup"><span data-stu-id="6cfad-149">To get your current account balance and a collection of invoice summaries containing an invoice summary with both recurring and one-time charges for each of your customer's currency types, see [Get invoice summaries](get-invoice-summaries.md).</span></span>

### <a name="invoices"></a><span data-ttu-id="6cfad-150">Faktury</span><span class="sxs-lookup"><span data-stu-id="6cfad-150">Invoices</span></span>

<span data-ttu-id="6cfad-151">Aby uzyskać kolekcję faktur, które pokazują opłaty cykliczne i [jednorazowe, zobacz Pobieranie kolekcji faktur.](get-a-collection-of-invoices.md)</span><span class="sxs-lookup"><span data-stu-id="6cfad-151">To get a collection of invoices that show both recurring and one-time charges, see [Get a collection of invoices](get-a-collection-of-invoices.md).</span></span> 

### <a name="single-invoice"></a><span data-ttu-id="6cfad-152">Pojedyncza faktura</span><span class="sxs-lookup"><span data-stu-id="6cfad-152">Single Invoice</span></span>

<span data-ttu-id="6cfad-153">Aby pobrać określoną fakturę przy użyciu identyfikatora faktury, zobacz [Pobieranie faktury według identyfikatora](get-invoice-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="6cfad-153">To retrieve a specific invoice using the invoice ID, see [Get an invoice by ID](get-invoice-by-id.md).</span></span>  

### <a name="reconciliation"></a><span data-ttu-id="6cfad-154">Pojednania</span><span class="sxs-lookup"><span data-stu-id="6cfad-154">Reconciliation</span></span>

<span data-ttu-id="6cfad-155">Aby uzyskać kolekcję szczegółów pozycji faktury (pozycje uzgodnień) dla określonego identyfikatora faktury, zobacz [Pobieranie pozycji faktury.](get-invoiceline-items.md)</span><span class="sxs-lookup"><span data-stu-id="6cfad-155">To get a collection of invoice line item details (Reconciliation line items) for a specific invoice ID, see [Get invoice line items](get-invoiceline-items.md).</span></span>  

### <a name="download-an-invoice-as-a-pdf"></a><span data-ttu-id="6cfad-156">Pobieranie faktury w formacie PDF</span><span class="sxs-lookup"><span data-stu-id="6cfad-156">Download an invoice as a PDF</span></span>

<span data-ttu-id="6cfad-157">Aby pobrać zestawienie faktur w formacie PDF przy użyciu identyfikatora faktury, zobacz [Pobieranie zestawienia faktury.](get-invoice-statement.md)</span><span class="sxs-lookup"><span data-stu-id="6cfad-157">To retrieve an invoice statement in PDF form using an invoice ID, see [Get an invoice statement](get-invoice-statement.md).</span></span>
