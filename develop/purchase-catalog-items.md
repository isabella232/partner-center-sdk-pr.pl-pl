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
# <a name="purchase-catalog-items"></a><span data-ttu-id="48dc6-103">Zakup elementów z katalogu</span><span class="sxs-lookup"><span data-stu-id="48dc6-103">Purchase catalog items</span></span>

<span data-ttu-id="48dc6-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="48dc6-104">**Applies To**</span></span>

- <span data-ttu-id="48dc6-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="48dc6-105">Partner Center</span></span>

<span data-ttu-id="48dc6-106">W poniższym scenariuszu przedstawiono ogólny proces kupowania elementów z katalogu przy użyciu interfejsu API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="48dc6-106">The following scenario demonstrates the generic process for purchasing items from the catalog by using the Partner Center API.</span></span>

## <a name="discovery"></a><span data-ttu-id="48dc6-107">Odnajdywanie</span><span class="sxs-lookup"><span data-stu-id="48dc6-107">Discovery</span></span>

<span data-ttu-id="48dc6-108">Wybierz produkty i jednostki SKU i sprawdź ich dostępność przy użyciu następujących modeli interfejsu API Centrum partnerskiego:</span><span class="sxs-lookup"><span data-stu-id="48dc6-108">Select products and SKUs and check their availability using the following Partner Center API models:</span></span>

- <span data-ttu-id="48dc6-109">[Product](product-resources.md#product) -konstrukcja grupująca dla jednostek towarów lub usług.</span><span class="sxs-lookup"><span data-stu-id="48dc6-109">[Product](product-resources.md#product) - A grouping construct for purchasable goods or services.</span></span> <span data-ttu-id="48dc6-110">Produkt nie jest elementem jednostek.</span><span class="sxs-lookup"><span data-stu-id="48dc6-110">A product by itself isn't a purchasable item.</span></span>
- <span data-ttu-id="48dc6-111">[SKU](product-resources.md#sku) — jednostka magazynowa jednostek (SKU) w ramach produktu.</span><span class="sxs-lookup"><span data-stu-id="48dc6-111">[SKU](product-resources.md#sku) - A purchasable Stock Keeping Unit (SKU) under a product.</span></span> <span data-ttu-id="48dc6-112">Reprezentują one różne kształty produktu.</span><span class="sxs-lookup"><span data-stu-id="48dc6-112">These represent the different shapes of the product.</span></span>
- <span data-ttu-id="48dc6-113">[Dostępność](product-resources.md#availability) — konfiguracja, w której jednostka SKU jest dostępna do zakupu (na przykład kraj, waluta i segment branżowy).</span><span class="sxs-lookup"><span data-stu-id="48dc6-113">[Availability](product-resources.md#availability) - A configuration in which a SKU is available for purchase (such as country, currency and industry segment).</span></span>

<span data-ttu-id="48dc6-114">Aby kupić element z wykazu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="48dc6-114">To purchase an item from the catalog, complete the following steps:</span></span>

1. <span data-ttu-id="48dc6-115">Zidentyfikuj i Pobierz produkt i jednostkę SKU, które chcesz kupić.</span><span class="sxs-lookup"><span data-stu-id="48dc6-115">Identify and retrieve the Product and SKU that you want to purchase.</span></span>

   - [<span data-ttu-id="48dc6-116">Pobierz listę produktów</span><span class="sxs-lookup"><span data-stu-id="48dc6-116">Get a list of products</span></span>](get-a-list-of-products.md)
   - [<span data-ttu-id="48dc6-117">Uzyskiwanie produktu przy użyciu identyfikatora produktu</span><span class="sxs-lookup"><span data-stu-id="48dc6-117">Get a product using the product ID</span></span>](get-a-product-by-id.md)
   - [<span data-ttu-id="48dc6-118">Pobierz listę jednostek SKU dla produktu</span><span class="sxs-lookup"><span data-stu-id="48dc6-118">Get a list of SKUs for a product</span></span>](get-a-list-of-skus-for-a-product.md)
   - [<span data-ttu-id="48dc6-119">Pobierz jednostkę SKU przy użyciu identyfikatora jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="48dc6-119">Get a SKU using the SKU ID</span></span>](get-a-sku-by-id.md)

2. <span data-ttu-id="48dc6-120">Sprawdź spis dla jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="48dc6-120">Check the inventory for a SKU.</span></span> <span data-ttu-id="48dc6-121">Ten krok jest wymagany tylko w przypadku jednostek SKU, które są oznaczone wartością **InventoryCheck** we właściwości [purchasePrerequisites](product-resources.md#sku) .</span><span class="sxs-lookup"><span data-stu-id="48dc6-121">This step is only needed for SKUs that are tagged with an **InventoryCheck** value in the [purchasePrerequisites](product-resources.md#sku) property.</span></span>

   - [<span data-ttu-id="48dc6-122">Sprawdzenie spisu</span><span class="sxs-lookup"><span data-stu-id="48dc6-122">Check Inventory</span></span>](check-inventory.md)

3. <span data-ttu-id="48dc6-123">Pobierz [dostępność](product-resources.md#availability) dla [jednostki SKU](product-resources.md#sku).</span><span class="sxs-lookup"><span data-stu-id="48dc6-123">Retrieve the [availability](product-resources.md#availability) for the [SKU](product-resources.md#sku).</span></span> <span data-ttu-id="48dc6-124">Podczas umieszczania zamówienia będzie potrzebna **CatalogItemId** dostępność.</span><span class="sxs-lookup"><span data-stu-id="48dc6-124">You will need the **CatalogItemId** of the availability when placing the order.</span></span> <span data-ttu-id="48dc6-125">Aby uzyskać tę wartość, użyj jednego z następujących interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="48dc6-125">To get this value, use one of the following APIs:</span></span>

   - [<span data-ttu-id="48dc6-126">Pobierz listę dostępność dla jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="48dc6-126">Get a list of availabilities for a SKU</span></span>](get-a-list-of-availabilities-for-a-sku.md)
   - [<span data-ttu-id="48dc6-127">Uzyskaj dostępność przy użyciu identyfikatora dostępności</span><span class="sxs-lookup"><span data-stu-id="48dc6-127">Get an availability using the availability ID</span></span>](get-an-availability-by-id.md)

## <a name="order-submission"></a><span data-ttu-id="48dc6-128">Przesyłanie zamówienia</span><span class="sxs-lookup"><span data-stu-id="48dc6-128">Order submission</span></span>

<span data-ttu-id="48dc6-129">Aby przesłać zamówienie elementu katalogu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="48dc6-129">To submit your catalog item order, do the following:</span></span>

1. <span data-ttu-id="48dc6-130">Utwórz [koszyk](cart-resources.md) do przechowywania kolekcji elementów wykazu, które zamierzasz kupić.</span><span class="sxs-lookup"><span data-stu-id="48dc6-130">Create a [Cart](cart-resources.md) to hold the collection of catalog items that you intend to buy.</span></span> <span data-ttu-id="48dc6-131">Podczas tworzenia koszyka [elementy w linii koszyka](cart-resources.md#cartlineitem) są automatycznie grupowane na podstawie tego, co można zakupić razem w tej samej [kolejności](order-resources.md).</span><span class="sxs-lookup"><span data-stu-id="48dc6-131">When you create a cart, the [cart line items](cart-resources.md#cartlineitem) are automatically grouped based on what can be purchased together in the same [Order](order-resources.md).</span></span>

   - [<span data-ttu-id="48dc6-132">Tworzenie koszyka</span><span class="sxs-lookup"><span data-stu-id="48dc6-132">Create a shopping cart</span></span>](create-a-cart.md)
   - [<span data-ttu-id="48dc6-133">Aktualizowanie koszyka</span><span class="sxs-lookup"><span data-stu-id="48dc6-133">Update a shopping cart</span></span>](update-a-cart.md)

2. <span data-ttu-id="48dc6-134">Sprawdź koszyk.</span><span class="sxs-lookup"><span data-stu-id="48dc6-134">Check out the cart.</span></span> <span data-ttu-id="48dc6-135">Wyewidencjonowanie koszyka powoduje utworzenie [zamówienia](order-resources.md).</span><span class="sxs-lookup"><span data-stu-id="48dc6-135">Checking out a cart results in the creation of an [Order](order-resources.md).</span></span>

   - [<span data-ttu-id="48dc6-136">Wyewidencjonuj koszyk</span><span class="sxs-lookup"><span data-stu-id="48dc6-136">Checkout the cart</span></span>](checkout-a-cart.md)

## <a name="get-order-details"></a><span data-ttu-id="48dc6-137">Pobierz szczegóły zamówienia</span><span class="sxs-lookup"><span data-stu-id="48dc6-137">Get order details</span></span>

<span data-ttu-id="48dc6-138">Możesz pobrać szczegóły pojedynczego zamówienia przy użyciu identyfikatora zamówienia lub uzyskać listę zamówień dla klienta.</span><span class="sxs-lookup"><span data-stu-id="48dc6-138">You can retrieve the details of an individual order using the order ID, or get a list of orders for a customer.</span></span> <span data-ttu-id="48dc6-139">Istnieje opóźnienie do 15 minut od momentu, gdy zamówienie zostanie przesłane i pojawi się na liście zamówień klienta.</span><span class="sxs-lookup"><span data-stu-id="48dc6-139">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a list of a customer's orders.</span></span>

- <span data-ttu-id="48dc6-140">Zobacz [Pobierz zamówienie według identyfikatora](get-an-order-by-id.md) , aby uzyskać szczegółowe informacje o poszczególnych zamówieniach, korzystając z identyfikatorów zamówień.</span><span class="sxs-lookup"><span data-stu-id="48dc6-140">See [Get an order by ID](get-an-order-by-id.md) to get the details of an individual order using the order IDs.</span></span>

- <span data-ttu-id="48dc6-141">Zobacz [Pobierz wszystkie zamówienia klienta](get-all-of-a-customer-s-orders.md) , aby uzyskać listę zamówień dla klienta przy użyciu identyfikatora klienta.</span><span class="sxs-lookup"><span data-stu-id="48dc6-141">See [Get all of a customer's orders](get-all-of-a-customer-s-orders.md) to get a list of orders for a customer using the customer ID.</span></span>

- <span data-ttu-id="48dc6-142">Aby uzyskać listę zamówień dla klienta według [typu cyklu rozliczeniowego](product-resources.md#billingcycletype) , należy zapoznać się z listą zakupów [według numerów klientów i rozliczeń](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) , co pozwala na wyświetlanie listy zamówień dotyczących elementów katalogu (opłat jednorazowych) oraz zamówień rocznych i miesięcznych.</span><span class="sxs-lookup"><span data-stu-id="48dc6-142">See [Get a list of orders by customer and billing cycle type](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) to get a list of orders for a customer by [billing cycle type](product-resources.md#billingcycletype) allowing you to list catalog item orders (one-time charges) and annual or monthly billed orders separately.</span></span>

## <a name="lifecycle-management"></a><span data-ttu-id="48dc6-143">Zarządzanie cyklem życia</span><span class="sxs-lookup"><span data-stu-id="48dc6-143">Lifecycle management</span></span>

<span data-ttu-id="48dc6-144">W ramach zarządzania cyklem życia elementów katalogu w centrum partnerskim można pobrać informacje o [uprawnieniach](entitlement-resources.md)elementów katalogu i uzyskać szczegółowe informacje dotyczące rezerwacji przy użyciu identyfikatora zamówienia rezerwacji.</span><span class="sxs-lookup"><span data-stu-id="48dc6-144">As part of managing the lifecycle of your catalog items in Partner Center, you can retrieve information about your catalog item [Entitlements](entitlement-resources.md), and get reservation details using the reservation order ID.</span></span> <span data-ttu-id="48dc6-145">Aby zapoznać się z przykładami, zobacz [Uzyskaj uprawnienia](get-a-collection-of-entitlements.md).</span><span class="sxs-lookup"><span data-stu-id="48dc6-145">For examples of how to do this, see [Get entitlements](get-a-collection-of-entitlements.md).</span></span>   

## <a name="invoice-and-reconciliation"></a><span data-ttu-id="48dc6-146">Faktura i uzgadnianie</span><span class="sxs-lookup"><span data-stu-id="48dc6-146">Invoice and reconciliation</span></span>

<span data-ttu-id="48dc6-147">W poniższych scenariuszach pokazano, jak programowo wyświetlić [faktury](invoice-resources.md)klienta i uzyskać salda konta oraz podsumowania, które zawierają opłaty jednorazowe dla elementów katalogu.</span><span class="sxs-lookup"><span data-stu-id="48dc6-147">The following scenarios show you how to programmatically view your customer's [invoices](invoice-resources.md), and get your account balances and summaries that include one-time charges for catalog items.</span></span>

### <a name="balance-and-payment"></a><span data-ttu-id="48dc6-148">Saldo i płatność</span><span class="sxs-lookup"><span data-stu-id="48dc6-148">Balance and payment</span></span>

<span data-ttu-id="48dc6-149">Aby uzyskać bieżące saldo konta w domyślnym typie waluty, który jest bilansem opłat cyklicznych i jednorazowych (element katalogu), zobacz [pobieranie bieżącego salda konta](get-the-reseller-s-current-account-balance.md).</span><span class="sxs-lookup"><span data-stu-id="48dc6-149">To get current account balance in your default currency type that is a balance of both recurring and one-time (catalog item) charges, see [Get your current account balance](get-the-reseller-s-current-account-balance.md).</span></span>

### <a name="multi-currency-balance-and-payment"></a><span data-ttu-id="48dc6-150">Saldo i płatność za wiele walut</span><span class="sxs-lookup"><span data-stu-id="48dc6-150">Multi-currency balance and payment</span></span>

<span data-ttu-id="48dc6-151">Aby skorzystać z bieżącego salda konta i kolekcji podsumowań faktur zawierających Podsumowanie faktur z uwzględnieniem zarówno cyklicznych, jak i jednorazowych opłat dla każdego z typów walutowych klienta, zobacz [Pobierz podsumowania faktur](get-invoice-summaries.md).</span><span class="sxs-lookup"><span data-stu-id="48dc6-151">To get your current account balance and a collection of invoice summaries containing an invoice summary with both recurring and one-time charges for each of your customer's currency types, see [Get invoice summaries](get-invoice-summaries.md).</span></span>

### <a name="invoices"></a><span data-ttu-id="48dc6-152">Faktury</span><span class="sxs-lookup"><span data-stu-id="48dc6-152">Invoices</span></span>

<span data-ttu-id="48dc6-153">Aby uzyskać kolekcję faktur, które pokazują jednocześnie opłaty cykliczne i jednorazowe, zobacz [pobieranie kolekcji faktur](get-a-collection-of-invoices.md).</span><span class="sxs-lookup"><span data-stu-id="48dc6-153">To get a collection of invoices that show both recurring and one-time charges, see [Get a collection of invoices](get-a-collection-of-invoices.md).</span></span> 

### <a name="single-invoice"></a><span data-ttu-id="48dc6-154">Pojedyncza faktura</span><span class="sxs-lookup"><span data-stu-id="48dc6-154">Single Invoice</span></span>

<span data-ttu-id="48dc6-155">Aby pobrać określoną fakturę przy użyciu identyfikatora faktury, zobacz [pobieranie faktury według identyfikatora](get-invoice-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="48dc6-155">To retrieve a specific invoice using the invoice ID, see [Get an invoice by ID](get-invoice-by-id.md).</span></span>  

### <a name="reconciliation"></a><span data-ttu-id="48dc6-156">Uzgadniania</span><span class="sxs-lookup"><span data-stu-id="48dc6-156">Reconciliation</span></span>

<span data-ttu-id="48dc6-157">Aby uzyskać kolekcję szczegółów elementu wiersza faktury (elementy linii uzgadniania) dla określonego identyfikatora faktury, zobacz [Pobieranie elementów wiersza faktury](get-invoiceline-items.md).</span><span class="sxs-lookup"><span data-stu-id="48dc6-157">To get a collection of invoice line item details (Reconciliation line items) for a specific invoice ID, see [Get invoice line items](get-invoiceline-items.md).</span></span>  

### <a name="download-an-invoice-as-a-pdf"></a><span data-ttu-id="48dc6-158">Pobierz fakturę jako plik PDF</span><span class="sxs-lookup"><span data-stu-id="48dc6-158">Download an invoice as a PDF</span></span>

<span data-ttu-id="48dc6-159">Aby pobrać instrukcję faktury w formularzu PDF przy użyciu identyfikatora faktury, zobacz artykuł [pobieranie faktury](get-invoice-statement.md).</span><span class="sxs-lookup"><span data-stu-id="48dc6-159">To retrieve an invoice statement in PDF form using an invoice ID, see [Get an invoice statement](get-invoice-statement.md).</span></span>
