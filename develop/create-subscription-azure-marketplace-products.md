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
# <a name="create-a-subscription-for-commercial-marketplace-products"></a><span data-ttu-id="ea7c2-103">Tworzenie subskrypcji dla komercyjnych produktów Marketplace</span><span class="sxs-lookup"><span data-stu-id="ea7c2-103">Create a subscription for commercial marketplace products</span></span>

<span data-ttu-id="ea7c2-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="ea7c2-104">**Applies to:**</span></span>

* <span data-ttu-id="ea7c2-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="ea7c2-105">Partner Center</span></span>

<span data-ttu-id="ea7c2-106">Możesz utworzyć subskrypcję dla komercyjnych produktów Marketplace przy użyciu interfejsów API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-106">You can create a subscription for commercial marketplace products using Partner Center APIs.</span></span> <span data-ttu-id="ea7c2-107">Musisz [uzyskać listę ofert dla rynku](#get-a-list-of-offers-for-a-market), [utworzyć i przesłać zamówienie](#create-and-submit-an-order) na komercyjną subskrypcję portalu Marketplace, a następnie [pobrać link aktywacji](#get-activation-link).</span><span class="sxs-lookup"><span data-stu-id="ea7c2-107">You must [get a list of offers for a market](#get-a-list-of-offers-for-a-market), [create and submit an order](#create-and-submit-an-order) for a commercial marketplace subscription, then [retrieve an activation link](#get-activation-link).</span></span>

<span data-ttu-id="ea7c2-108">Możesz również [wykonywać Zarządzanie cyklem życia](#lifecycle-management) i [zarządzać fakturami](#invoice-and-reconciliation) dla tych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-108">You can also [perform lifecycle management](#lifecycle-management) and [manage invoices](#invoice-and-reconciliation) for these subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea7c2-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ea7c2-109">Prerequisites</span></span>

* <span data-ttu-id="ea7c2-110">Poświadczenia [uwierzytelniania Centrum partnerskiego](partner-center-authentication.md) .</span><span class="sxs-lookup"><span data-stu-id="ea7c2-110">[Partner Center authentication](partner-center-authentication.md) credentials.</span></span> <span data-ttu-id="ea7c2-111">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>
* <span data-ttu-id="ea7c2-112">Identyfikator klienta.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-112">The customer identifier.</span></span> <span data-ttu-id="ea7c2-113">Jeśli nie masz identyfikatora klienta, wykonaj kroki opisane w sekcji [Pobieranie listy klientów](get-a-list-of-customers.md).</span><span class="sxs-lookup"><span data-stu-id="ea7c2-113">If you don't have a customer's identifier, follow the steps in [Get a list of customers](get-a-list-of-customers.md).</span></span> <span data-ttu-id="ea7c2-114">Alternatywnie możesz zalogować się do Centrum partnerskiego, wybrać klienta z listy klientów, wybrać pozycję **konto**, a następnie zapisać **Identyfikator Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-114">Alternatively, sign in to Partner Center, choose the customer from the list of customers, select **Account**, then save their **Microsoft ID**.</span></span>

## <a name="get-a-list-of-offers-for-a-market"></a><span data-ttu-id="ea7c2-115">Pobieranie listy ofert dla rynku</span><span class="sxs-lookup"><span data-stu-id="ea7c2-115">Get a list of offers for a market</span></span>

<span data-ttu-id="ea7c2-116">Dostępne oferty można sprawdzić na rynku przy użyciu następujących modeli interfejsu API Centrum partnerskiego:</span><span class="sxs-lookup"><span data-stu-id="ea7c2-116">You can check the available offers for a market using the following Partner Center API models:</span></span>

* <span data-ttu-id="ea7c2-117">**[Produkt](product-resources.md#product)**: konstrukcja grupująca dla jednostek towarów lub usług.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-117">**[Product](product-resources.md#product)**: A grouping construct for purchasable goods or services.</span></span> <span data-ttu-id="ea7c2-118">Sam produkt nie jest elementem jednostek.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-118">A product itself isn't a purchasable item.</span></span>
* <span data-ttu-id="ea7c2-119">**[SKU](product-resources.md#sku)**: jednostka magazynowa jednostek (SKU) w ramach produktu.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-119">**[SKU](product-resources.md#sku)**: A purchasable Stock Keeping Unit (SKU) under a product.</span></span> <span data-ttu-id="ea7c2-120">Reprezentują one różne kształty produktu.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-120">These represent the different shapes of the product.</span></span>
* <span data-ttu-id="ea7c2-121">**[Dostępność](product-resources.md#availability)**: Konfiguracja, w której jednostka SKU jest dostępna do zakupu (na przykład kraj, waluta lub segment branżowy).</span><span class="sxs-lookup"><span data-stu-id="ea7c2-121">**[Availability](product-resources.md#availability)**: A configuration in which a SKU is available for purchase (such as country, currency, or industry segment).</span></span>

<span data-ttu-id="ea7c2-122">Przed zakupem rezerwacji platformy Azure wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ea7c2-122">Before you purchase an Azure reservation, complete the following steps:</span></span>

1. <span data-ttu-id="ea7c2-123">Zidentyfikuj i Pobierz produkt i jednostkę SKU, które chcesz kupić.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-123">Identify and retrieve the product and SKU that you want to purchase.</span></span> <span data-ttu-id="ea7c2-124">Jeśli znasz już identyfikator produktu i identyfikator jednostki SKU, zaznacz je.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-124">If you already know the Product ID and SKU ID, select them.</span></span>

    * [<span data-ttu-id="ea7c2-125">Pobierz listę produktów</span><span class="sxs-lookup"><span data-stu-id="ea7c2-125">Get a list of products</span></span>](get-a-list-of-products.md)
    * [<span data-ttu-id="ea7c2-126">Uzyskiwanie produktu przy użyciu identyfikatora produktu</span><span class="sxs-lookup"><span data-stu-id="ea7c2-126">Get a product using the product ID</span></span>](get-a-product-by-id.md)
    * [<span data-ttu-id="ea7c2-127">Pobierz listę jednostek SKU dla produktu</span><span class="sxs-lookup"><span data-stu-id="ea7c2-127">Get a list of SKUs for a product</span></span>](get-a-list-of-skus-for-a-product.md)
    * [<span data-ttu-id="ea7c2-128">Pobierz jednostkę SKU przy użyciu identyfikatora jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="ea7c2-128">Get a SKU using the SKU ID</span></span>](get-a-sku-by-id.md)

    > [!NOTE]
    > <span data-ttu-id="ea7c2-129">Możesz identyfikować komercyjne produkty Marketplace według ich właściwości **ProductType** **"Azure"** i ich właściwości **podtyp** **"SaaS"**.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-129">You can identify commercial marketplace products by their **ProductType** property of **"Azure"** and their **SubType** property of **"SaaS"**.</span></span>

2. <span data-ttu-id="ea7c2-130">Jeśli jednostki SKU są znakowane z wymaganiem wstępnym **InventoryCheck** , [Sprawdź spis dla jednostki SKU](check-inventory.md).</span><span class="sxs-lookup"><span data-stu-id="ea7c2-130">If the SKUs are tagged with an **InventoryCheck** prerequisite, [check the inventory for a SKU](check-inventory.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="ea7c2-131">W tej chwili nie ma żadnych komercyjnych produktów Marketplace, które obsługują sprawdzanie spisu lub są oznaczone jako wymaganie wstępne **InventoryCheck** .</span><span class="sxs-lookup"><span data-stu-id="ea7c2-131">At this time, there are no commercial marketplace products that support inventory check or are tagged with an **InventoryCheck** prerequisite.</span></span>

3. <span data-ttu-id="ea7c2-132">Pobierz dostępność dla jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-132">Retrieve the availability for the SKU.</span></span> <span data-ttu-id="ea7c2-133">**CatalogItemId** dostępność będzie potrzebna podczas umieszczania zamówienia, który można pobrać za pomocą następujących interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="ea7c2-133">You will need the **CatalogItemId** of the availability when placing the order, which you can retrieve through the following APIs:</span></span>

    * [<span data-ttu-id="ea7c2-134">Pobierz listę dostępność dla jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="ea7c2-134">Get a list of availabilities for a SKU</span></span>](get-a-list-of-availabilities-for-a-sku.md)
    * [<span data-ttu-id="ea7c2-135">Uzyskaj dostępność przy użyciu identyfikatora dostępności</span><span class="sxs-lookup"><span data-stu-id="ea7c2-135">Get an availability using the availability ID</span></span>](get-an-availability-by-id.md)

## <a name="create-and-submit-an-order"></a><span data-ttu-id="ea7c2-136">Utwórz i prześlij zamówienie</span><span class="sxs-lookup"><span data-stu-id="ea7c2-136">Create and submit an order</span></span>

<span data-ttu-id="ea7c2-137">Aby przesłać swoją kolejność rezerwacji na platformie Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ea7c2-137">To submit your Azure reservation order, follow these steps:</span></span>

1. <span data-ttu-id="ea7c2-138">[Utwórz koszyk](create-a-cart.md) do przechowywania kolekcji elementów wykazu, które zamierzasz kupić.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-138">[Create a cart](create-a-cart.md) to hold the collection of catalog items that you intend to buy.</span></span> <span data-ttu-id="ea7c2-139">Podczas tworzenia [koszyka](cart-resources.md#cart) [elementy w linii koszyka](cart-resources.md#cartlineitem) są automatycznie grupowane na podstawie tego, co można zakupić razem w tej samej [kolejności](order-resources.md#order).</span><span class="sxs-lookup"><span data-stu-id="ea7c2-139">When you create a [cart](cart-resources.md#cart), the [cart line items](cart-resources.md#cartlineitem) are automatically grouped based on what can be purchased together in the same [order](order-resources.md#order).</span></span> <span data-ttu-id="ea7c2-140">(Możesz również [zaktualizować koszyk](update-a-cart.md)).</span><span class="sxs-lookup"><span data-stu-id="ea7c2-140">(You can also [update a cart](update-a-cart.md).)</span></span>
2. <span data-ttu-id="ea7c2-141">[Sprawdź koszyk](checkout-a-cart.md), w wyniku którego powstaje [Zamówienie](order-resources.md#order).</span><span class="sxs-lookup"><span data-stu-id="ea7c2-141">[Check out the cart](checkout-a-cart.md), which results in the creation of an [order](order-resources.md#order).</span></span>

### <a name="get-order-details"></a><span data-ttu-id="ea7c2-142">Pobierz szczegóły zamówienia</span><span class="sxs-lookup"><span data-stu-id="ea7c2-142">Get order details</span></span>

<span data-ttu-id="ea7c2-143">[Szczegółowe informacje o poszczególnych zamówieniach można pobrać przy użyciu identyfikatora zamówienia](get-an-order-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="ea7c2-143">You can [retrieve the details of an individual order using the order ID](get-an-order-by-id.md).</span></span> <span data-ttu-id="ea7c2-144">Możesz również [pobrać listę wszystkich zamówień dla określonego klienta](get-all-of-a-customer-s-orders.md).</span><span class="sxs-lookup"><span data-stu-id="ea7c2-144">You can also [retrieve a list of all orders for a specific customer](get-all-of-a-customer-s-orders.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ea7c2-145">Po przesłaniu zamówienia istnieje opóźnienie do 15 minut, po upływie którego zamówienie zostanie wyświetlone na liście zamówienie tego klienta.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-145">After an order is submitted, there is a delay of up to 15 minutes before the order appears in that customer's order list.</span></span>

## <a name="get-activation-link"></a><span data-ttu-id="ea7c2-146">Uzyskaj link aktywacji</span><span class="sxs-lookup"><span data-stu-id="ea7c2-146">Get activation link</span></span>

<span data-ttu-id="ea7c2-147">Partner lub klient muszą aktywować subskrypcje produktów w witrynie Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-147">The partner or customer must activate subscriptions to Azure Marketplace products.</span></span> <span data-ttu-id="ea7c2-148">Możesz [uzyskać link aktywacji, wybierając pozycję wiersz zamówienia](get-activation-link-by-order-line-item.md).</span><span class="sxs-lookup"><span data-stu-id="ea7c2-148">You can [get an activation link by order line item](get-activation-link-by-order-line-item.md).</span></span> <span data-ttu-id="ea7c2-149">Możesz również [uzyskać subskrypcję według identyfikatora](get-a-subscription-by-id.md), a następnie wyliczyć jej właściwość **Links** , aby utworzyć łącze aktywacji.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-149">You can also [get a subscription by ID](get-a-subscription-by-id.md), then enumerate its **Links** property to create an activation link.</span></span>

## <a name="lifecycle-management"></a><span data-ttu-id="ea7c2-150">Zarządzanie cyklem życia</span><span class="sxs-lookup"><span data-stu-id="ea7c2-150">Lifecycle management</span></span>

<span data-ttu-id="ea7c2-151">Możesz zarządzać cyklem życia subskrypcji dla komercyjnych produktów Marketplace przy użyciu następujących metod:</span><span class="sxs-lookup"><span data-stu-id="ea7c2-151">You can manage the lifecycle of your subscriptions to commercial marketplace products using the following methods:</span></span>

* [<span data-ttu-id="ea7c2-152">Anulowanie subskrypcji platformy handlowej</span><span class="sxs-lookup"><span data-stu-id="ea7c2-152">Cancel a commercial marketplace subscription</span></span>](cancel-an-azure-marketplace-subscription.md)
* [<span data-ttu-id="ea7c2-153">Włączanie lub wyłączanie autoodnawiania dla komercyjnej subskrypcji portalu Marketplace</span><span class="sxs-lookup"><span data-stu-id="ea7c2-153">Enable or disable autorenew for a commercial marketplace subscription</span></span>](update-autorenew-for-an-azure-marketplace-subscription.md)

## <a name="quantity-management"></a><span data-ttu-id="ea7c2-154">Zarządzanie ilościami</span><span class="sxs-lookup"><span data-stu-id="ea7c2-154">Quantity management</span></span>

<span data-ttu-id="ea7c2-155">Ilość komercyjnej subskrypcji portalu Marketplace musi przypadać w ramach limitów zdefiniowanych przez skojarzoną [jednostkę SKU](product-resources.md#sku) (zobacz atrybuty **minimumQuantity** i **maximumQuantity** ).</span><span class="sxs-lookup"><span data-stu-id="ea7c2-155">The quantity of a commercial marketplace subscription must be within the limits defined by its associated [SKU](product-resources.md#sku) (see the **minimumQuantity** and **maximumQuantity** attributes).</span></span> <span data-ttu-id="ea7c2-156">Aby zaktualizować ilość komercyjnej subskrypcji portalu Marketplace, użyj następującej metody:</span><span class="sxs-lookup"><span data-stu-id="ea7c2-156">To update the quantity of a commercial marketplace subscription, use the following method:</span></span>

* [<span data-ttu-id="ea7c2-157">Zmiana ilości subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ea7c2-157">Change the quantity of a subscription</span></span>](change-the-quantity-of-a-subscription.md)

## <a name="invoice-and-reconciliation"></a><span data-ttu-id="ea7c2-158">Faktura i uzgadnianie</span><span class="sxs-lookup"><span data-stu-id="ea7c2-158">Invoice and reconciliation</span></span>

<span data-ttu-id="ea7c2-159">Można zarządzać [fakturami](invoice-resources.md) klienta (w tym opłatami za subskrypcje do komercyjnych produktów Marketplace) przy użyciu następujących metod:</span><span class="sxs-lookup"><span data-stu-id="ea7c2-159">You can manage customer [invoices](invoice-resources.md) (including charges for subscriptions to commercial marketplace products) using the following methods:</span></span>

* [<span data-ttu-id="ea7c2-160">Pobierz fakturę z rozliczanej komercyjnie towarami za użycie w portalu Marketplace</span><span class="sxs-lookup"><span data-stu-id="ea7c2-160">Get invoice billed commercial marketplace consumption line items</span></span>](get-invoice-billed-consumption-lineitems.md)
* [<span data-ttu-id="ea7c2-161">Pobieranie linków do szacunkowych faktur</span><span class="sxs-lookup"><span data-stu-id="ea7c2-161">Get invoice estimate links</span></span>](get-invoice-estimate-links.md)
* [<span data-ttu-id="ea7c2-162">Pobierz faktury dla rozliczanej komercyjnego zużycia w portalu Marketplace</span><span class="sxs-lookup"><span data-stu-id="ea7c2-162">Get invoice unbilled commercial marketplace consumption line items</span></span>](get-invoice-unbilled-consumption-lineitems.md)
* [<span data-ttu-id="ea7c2-163">Pobierz faktury rozliczane pozycje wiersza uzgadniania</span><span class="sxs-lookup"><span data-stu-id="ea7c2-163">Get invoice unbilled reconciliation line items</span></span>](get-invoice-unbilled-recon-lineitems.md)

## <a name="test-using-integration-sandbox-account"></a><span data-ttu-id="ea7c2-164">Testowanie przy użyciu konta piaskownicy integracji</span><span class="sxs-lookup"><span data-stu-id="ea7c2-164">Test using integration sandbox account</span></span>

<span data-ttu-id="ea7c2-165">W środowisku produkcyjnym po utworzeniu subskrypcji dla komercyjnych produktów SaaS Marketplace musisz pobrać spersonalizowany link aktywacji z Centrum partnerskiego i odwiedzić witrynę wydawcy, aby ukończyć proces instalacji.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-165">In production, after you have created a subscription to commercial marketplace SaaS products, you need to retrieve a personalized activation link from Partner Center and visit the publisher's site to complete the setup process.</span></span> <span data-ttu-id="ea7c2-166">Rozliczanie subskrypcji rozpocznie się dopiero po zakończeniu instalacji.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-166">Subscription billing will begin only after setup is complete.</span></span>

<span data-ttu-id="ea7c2-167">W środowisku piaskownicy CSP nie ma integracji z niezależnymi dostawcami oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-167">In the CSP sandbox environment, there is no integration with ISVs.</span></span> <span data-ttu-id="ea7c2-168">Jeśli spróbujesz pobrać link aktywacji z Centrum partnerskiego, zostanie zwrócony fikcyjny link.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-168">If you try to retrieve an activation link from Partner Center, a dummy link will be returned.</span></span> <span data-ttu-id="ea7c2-169">Nie można użyć tego fikcyjnego linku, aby zakończyć proces instalacji w lokacji wydawcy.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-169">You cannot use this dummy link to complete the setup process at the publisher's site.</span></span> <span data-ttu-id="ea7c2-170">Aby skorzystać z konta piaskownicy Integration do testowania rozliczeń dla subskrypcji dla komercyjnych produktów SaaS Marketplace, użyj następującej metody, aby aktywować subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-170">To use the integration sandbox account to test billing for subscriptions to commercial marketplace SaaS products, use the following method to activate the subscription instead.</span></span> <span data-ttu-id="ea7c2-171">Rozliczanie subskrypcji rozpocznie się po pomyślnej aktywacji:</span><span class="sxs-lookup"><span data-stu-id="ea7c2-171">Subscription billing will begin after successful activation:</span></span>

* [<span data-ttu-id="ea7c2-172">Aktywuj subskrypcję piaskownicy dla komercyjnych produktów Marketplace</span><span class="sxs-lookup"><span data-stu-id="ea7c2-172">Activate a sandbox subscription for commercial marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

