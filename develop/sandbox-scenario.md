---
title: Możliwości piaskownicy partnera obsługujące relację odsprzedawcy
description: Piaskownica partnerów ma możliwość obsługi relacji między partnerem a klientem
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: af46811b3615e1f904a9619de85b0aca7622490b
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711869"
---
# <a name="partner-sandbox-capabilities-that-support-reseller-relationship"></a><span data-ttu-id="6dcd6-103">Możliwości piaskownicy partnera obsługujące relację odsprzedawcy</span><span class="sxs-lookup"><span data-stu-id="6dcd6-103">Partner sandbox capabilities that support reseller relationship</span></span>

<span data-ttu-id="6dcd6-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="6dcd6-104">**Applies to:**</span></span>

- <span data-ttu-id="6dcd6-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="6dcd6-105">Partner Center</span></span>
- <span data-ttu-id="6dcd6-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="6dcd6-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="6dcd6-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="6dcd6-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="6dcd6-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6dcd6-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6dcd6-109">W tym artykule wyjaśniono, co jest obsługiwane w piaskownicy dla relacji odsprzedawcy między partnerem a klientem.</span><span class="sxs-lookup"><span data-stu-id="6dcd6-109">This article explains what is supported in the Sandbox for reseller relationships between the partner and the customer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6dcd6-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6dcd6-110">Prerequisites</span></span>

- <span data-ttu-id="6dcd6-111">Poświadczenia konta Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="6dcd6-111">Partner Center account credentials.</span></span> <span data-ttu-id="6dcd6-112">Scenariusz piaskownicy obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznej, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6dcd6-112">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span>
- <span data-ttu-id="6dcd6-113">Identyfikator klienta (identyfikator dzierżawy klienta).</span><span class="sxs-lookup"><span data-stu-id="6dcd6-113">A customer ID (customer-tenant-id).</span></span> <span data-ttu-id="6dcd6-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard/home)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="6dcd6-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard/home).</span></span> <span data-ttu-id="6dcd6-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="6dcd6-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6dcd6-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="6dcd6-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6dcd6-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="6dcd6-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6dcd6-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta (identyfikator dzierżawy klienta).</span><span class="sxs-lookup"><span data-stu-id="6dcd6-118">The Microsoft ID is the same as the customer ID (customer-tenant-id).</span></span>
- <span data-ttu-id="6dcd6-119">Wszystkie Azure Reserved Virtual Machine Instances i zamówienia zakupu oprogramowania muszą zostać anulowane przed usunięciem klienta z piaskownicy integracji z poradami.</span><span class="sxs-lookup"><span data-stu-id="6dcd6-119">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="scenarios-supporting-reseller-relationship"></a><span data-ttu-id="6dcd6-120">Scenariusze obsługujące relację odsprzedawcy</span><span class="sxs-lookup"><span data-stu-id="6dcd6-120">Scenarios Supporting Reseller Relationship</span></span>

1.  <span data-ttu-id="6dcd6-121">Bezpośredni partnerzy rozliczeń i dostawcy pośredniego w piaskownicy mogą tworzyć relacje z klientem piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="6dcd6-121">Sandbox Direct Bill Partners and Indirect Providers can create relationships with the Sandbox customer.</span></span> 
2.  <span data-ttu-id="6dcd6-122">Bezpośredni partnerzy rachunków w piaskownicy i dostawcy pośrednii nie mogą zapraszać klientów w piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="6dcd6-122">Sandbox Direct Bill Partners and Indirect Providers cannot invite Sandbox customers.</span></span>



### <a name="in-the-sandbox"></a><span data-ttu-id="6dcd6-123">W piaskownicy</span><span class="sxs-lookup"><span data-stu-id="6dcd6-123">In the Sandbox</span></span>

<span data-ttu-id="6dcd6-124">**Bezpośredni partnerzy Bill**:</span><span class="sxs-lookup"><span data-stu-id="6dcd6-124">**Direct bill partners**:</span></span>

<span data-ttu-id="6dcd6-125">• Może dodawać istniejących klientów</span><span class="sxs-lookup"><span data-stu-id="6dcd6-125">•   Can add existing customers</span></span>

<span data-ttu-id="6dcd6-126">• Nie można zażądać relacji z nowymi klientami</span><span class="sxs-lookup"><span data-stu-id="6dcd6-126">•   Cannot request relationships with new customers</span></span>

<span data-ttu-id="6dcd6-127">**Dostawcy Pośrednii**:</span><span class="sxs-lookup"><span data-stu-id="6dcd6-127">**Indirect providers**:</span></span>

<span data-ttu-id="6dcd6-128">• Może dodawać istniejących klientów</span><span class="sxs-lookup"><span data-stu-id="6dcd6-128">•   Can add existing customers</span></span>

<span data-ttu-id="6dcd6-129">• Nie można zażądać relacji z nowymi klientami</span><span class="sxs-lookup"><span data-stu-id="6dcd6-129">•   Cannot request relationships with new customers</span></span>

<span data-ttu-id="6dcd6-130">• Nie może mieć relacji z odsprzedawcą pośrednią</span><span class="sxs-lookup"><span data-stu-id="6dcd6-130">•   Cannot have a relationship with an Indirect reseller</span></span>

<span data-ttu-id="6dcd6-131">**Pośredni odsprzedawca**: (wkrótce)</span><span class="sxs-lookup"><span data-stu-id="6dcd6-131">**Indirect reseller**: (coming soon)</span></span>

<span data-ttu-id="6dcd6-132">• Mogą mieć relacje z istniejącymi klientami</span><span class="sxs-lookup"><span data-stu-id="6dcd6-132">•   Can have a relationships with existing customers</span></span>

<span data-ttu-id="6dcd6-133">• Nie można zażądać nowych relacji lub dodać nowych klientów</span><span class="sxs-lookup"><span data-stu-id="6dcd6-133">•   Cannot request new relationships or add new customers</span></span>

### <a name="in-partner-center"></a><span data-ttu-id="6dcd6-134">W centrum partnerskim</span><span class="sxs-lookup"><span data-stu-id="6dcd6-134">In Partner Center</span></span>

<span data-ttu-id="6dcd6-135">**Bezpośredni partnerzy Bill**:</span><span class="sxs-lookup"><span data-stu-id="6dcd6-135">**Direct bill partners**:</span></span>

<span data-ttu-id="6dcd6-136">• Może dodawać nowych klientów</span><span class="sxs-lookup"><span data-stu-id="6dcd6-136">•   Can add new customers</span></span>

<span data-ttu-id="6dcd6-137">• Może zażądać relacji z nowymi klientami</span><span class="sxs-lookup"><span data-stu-id="6dcd6-137">•   Can request relationships with new customers</span></span>

<span data-ttu-id="6dcd6-138">**Dostawcy Pośrednii**:</span><span class="sxs-lookup"><span data-stu-id="6dcd6-138">**Indirect providers**:</span></span>

<span data-ttu-id="6dcd6-139">• Może dodawać nowych klientów</span><span class="sxs-lookup"><span data-stu-id="6dcd6-139">•   Can add new customers</span></span>

<span data-ttu-id="6dcd6-140">• Może zażądać relacji z nowymi klientami</span><span class="sxs-lookup"><span data-stu-id="6dcd6-140">•   Can request relationships with new customers</span></span>

<span data-ttu-id="6dcd6-141">• Mogą mieć relacje z pośrednimi odsprzedawcami</span><span class="sxs-lookup"><span data-stu-id="6dcd6-141">•   Can have relationships with indirect resellers</span></span>

<span data-ttu-id="6dcd6-142">**Odsprzedawcy Pośrednii**:</span><span class="sxs-lookup"><span data-stu-id="6dcd6-142">**Indirect resellers**:</span></span>

<span data-ttu-id="6dcd6-143">• Nie można dodać nowych klientów</span><span class="sxs-lookup"><span data-stu-id="6dcd6-143">•   Can’t add new customers</span></span>

<span data-ttu-id="6dcd6-144">• Może zażądać relacji z nowymi klientami</span><span class="sxs-lookup"><span data-stu-id="6dcd6-144">•   Can request relationships with new customers</span></span>

3. <span data-ttu-id="6dcd6-145">Bezpośredni partner rozliczeń i dostawcy pośredniego w piaskownicy mogą usunąć relację odsprzedawcy z interfejsu użytkownika i interfejsu API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="6dcd6-145">Sandbox Direct Bill Partner and Indirect Providers are able to remove reseller relationship from Partner Center UI and API.</span></span>

4. <span data-ttu-id="6dcd6-146">Relacja usuwania odsprzedawcy z piaskownicy spowoduje wywołanie usuwania AP klienta.</span><span class="sxs-lookup"><span data-stu-id="6dcd6-146">Sandbox Remove Reseller Relationship will call Delete customer AP.</span></span> <span data-ttu-id="6dcd6-147">Spowoduje to usunięcie relacji, a także usunięcie dzierżawy klienta.</span><span class="sxs-lookup"><span data-stu-id="6dcd6-147">This will remove the relationship as well as delete the customer tenant.</span></span> <span data-ttu-id="6dcd6-148">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="6dcd6-148">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span>

<span data-ttu-id="6dcd6-149">Aby uzyskać szczegółowe informacje, Skorzystaj z [relacji usuwanie odsprzedawcy](remove-a-reseller-relationship-with-a-customer.md) dla klienta.</span><span class="sxs-lookup"><span data-stu-id="6dcd6-149">Follow the [Remove Reseller Relationship](remove-a-reseller-relationship-with-a-customer.md) for the customer for details.</span></span> <span data-ttu-id="6dcd6-150">Istnieją jednak pewne różnice między możliwościami produktu i piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="6dcd6-150">However, there are some differences between the Product and Sandbox capabilities.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6dcd6-151">SKŁADNIA ŻĄDANIA</span><span class="sxs-lookup"><span data-stu-id="6dcd6-151">REQUEST SYNTAX</span></span>

|<span data-ttu-id="6dcd6-152">**Metoda**</span><span class="sxs-lookup"><span data-stu-id="6dcd6-152">**Method**</span></span>|<span data-ttu-id="6dcd6-153">**Usuwanie**</span><span class="sxs-lookup"><span data-stu-id="6dcd6-153">**Delete**</span></span>|
|-------------|------------|
|<span data-ttu-id="6dcd6-154">Usuń</span><span class="sxs-lookup"><span data-stu-id="6dcd6-154">Delete</span></span>|<span data-ttu-id="6dcd6-155">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="6dcd6-155">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span> |

<span data-ttu-id="6dcd6-156">Treść żądania nie</span><span class="sxs-lookup"><span data-stu-id="6dcd6-156">Request body None</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6dcd6-157">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6dcd6-157">Response success and error codes</span></span>

<span data-ttu-id="6dcd6-158">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="6dcd6-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6dcd6-159">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="6dcd6-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6dcd6-160">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](./error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6dcd6-160">For the full list, see [Partner Center REST error codes](./error-codes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6dcd6-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6dcd6-161">Next steps</span></span>

- [<span data-ttu-id="6dcd6-162">Aktywuj subskrypcje piaskownicy dla produktów portalu Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="6dcd6-162">Activate Sandbox subscriptions for Azure Marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

- [<span data-ttu-id="6dcd6-163">Anulowanie zamówienia z piaskownicy</span><span class="sxs-lookup"><span data-stu-id="6dcd6-163">Cancel an order from Sandbox</span></span>](cancel-an-order-from-the-integration-sandbox.md)

- [<span data-ttu-id="6dcd6-164">Testowanie i debugowanie</span><span class="sxs-lookup"><span data-stu-id="6dcd6-164">Test and debug</span></span>](test-and-debug.md)