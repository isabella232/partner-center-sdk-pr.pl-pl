---
title: Możliwości piaskownicy dla relacji odsprzedawcy
description: Piaskownica partnera ma możliwość obsługi relacji między partnerem a klientem
ms.date: 05/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9bef4a15685ebbdc2212988f5ac5724b946cfd54
ms.sourcegitcommit: 1aeaa12705a5945b8aab6bca254fedebd9c8bc4e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2021
ms.locfileid: "110243388"
---
# <a name="sandbox-capabilities-for-reseller-relationship"></a><span data-ttu-id="86958-103">Możliwości piaskownicy dla relacji odsprzedawcy</span><span class="sxs-lookup"><span data-stu-id="86958-103">Sandbox capabilities for Reseller relationship</span></span>

<span data-ttu-id="86958-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="86958-104">**Applies to:**</span></span>

- <span data-ttu-id="86958-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="86958-105">Partner Center</span></span>
- <span data-ttu-id="86958-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="86958-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="86958-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="86958-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="86958-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="86958-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="86958-109">W tym artykule wyjaśniono, co jest obsługiwane w piaskownicy w przypadku relacji odsprzedawcy między partnerem a klientem.</span><span class="sxs-lookup"><span data-stu-id="86958-109">This article explains what is supported in the Sandbox for reseller relationships between the partner and the customer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="86958-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="86958-110">Prerequisites</span></span>

- <span data-ttu-id="86958-111">Partner Center poświadczeń konta.</span><span class="sxs-lookup"><span data-stu-id="86958-111">Partner Center account credentials.</span></span> <span data-ttu-id="86958-112">Scenariusz piaskownicy obsługuje uwierzytelnianie zarówno przy użyciu autonomicznej aplikacji, jak i poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="86958-112">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span>
- <span data-ttu-id="86958-113">Identyfikator klienta (customer-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="86958-113">A customer ID (customer-tenant-id).</span></span> <span data-ttu-id="86958-114">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard/home).</span><span class="sxs-lookup"><span data-stu-id="86958-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard/home).</span></span> <span data-ttu-id="86958-115">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="86958-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="86958-116">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="86958-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="86958-117">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="86958-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="86958-118">Identyfikator microsoft jest taki sam jak identyfikator klienta (customer-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="86958-118">The Microsoft ID is the same as the customer ID (customer-tenant-id).</span></span>
- <span data-ttu-id="86958-119">Wszystkie Azure Reserved Virtual Machine Instances i zamówienia zakupu oprogramowania muszą zostać anulowane przed usunięciem klienta z piaskownicy integracji porad.</span><span class="sxs-lookup"><span data-stu-id="86958-119">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="scenarios-supporting-reseller-relationship"></a><span data-ttu-id="86958-120">Scenariusze obsługi relacji odsprzedawcy</span><span class="sxs-lookup"><span data-stu-id="86958-120">Scenarios Supporting Reseller Relationship</span></span>

1.  <span data-ttu-id="86958-121">Partnerzy rozliczani bezpośrednio w piaskownicy i dostawcy pośredni mogą tworzyć relacje z klientem piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="86958-121">Sandbox Direct Bill Partners and Indirect Providers can create relationships with the Sandbox customer.</span></span> 
2.  <span data-ttu-id="86958-122">Partnerzy rozliczani bezpośrednio w piaskownicy i dostawcy pośredni nie mogą zapraszać klientów piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="86958-122">Sandbox Direct Bill Partners and Indirect Providers cannot invite Sandbox customers.</span></span>

3. <span data-ttu-id="86958-123">Dostawcy pośredni i partner rozliczani bezpośrednio w piaskownicy mogą usunąć relację odsprzedawcy z Partner Center interfejsu użytkownika i interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="86958-123">Sandbox Direct Bill Partner and Indirect Providers are able to remove reseller relationship from Partner Center UI and API.</span></span>

4. <span data-ttu-id="86958-124">W przypadku relacji odsprzedawcy usunięcia piaskownicy zostanie wywołana nazwa Usuń klienta AP.</span><span class="sxs-lookup"><span data-stu-id="86958-124">Sandbox Remove Reseller Relationship will call Delete customer AP.</span></span> <span data-ttu-id="86958-125">Spowoduje to usunięcie relacji oraz dzierżawy klienta.</span><span class="sxs-lookup"><span data-stu-id="86958-125">This will remove the relationship as well as delete the customer tenant.</span></span> <span data-ttu-id="86958-126">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="86958-126">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span>


    ### <a name="in-the-sandbox"></a><span data-ttu-id="86958-127">W piaskownicy</span><span class="sxs-lookup"><span data-stu-id="86958-127">In the Sandbox</span></span>

    <span data-ttu-id="86958-128">**Partnerzy rozliczani bezpośrednio:**</span><span class="sxs-lookup"><span data-stu-id="86958-128">**Direct bill partners**:</span></span>

    - <span data-ttu-id="86958-129">Może dodawać istniejących klientów</span><span class="sxs-lookup"><span data-stu-id="86958-129">Can add existing customers</span></span>

    - <span data-ttu-id="86958-130">Nie można zażądać relacji z nowymi klientami</span><span class="sxs-lookup"><span data-stu-id="86958-130">Cannot request relationships with new customers</span></span>

    <span data-ttu-id="86958-131">**Dostawcy pośredni:**</span><span class="sxs-lookup"><span data-stu-id="86958-131">**Indirect providers**:</span></span>

    - <span data-ttu-id="86958-132">Może dodawać istniejących klientów</span><span class="sxs-lookup"><span data-stu-id="86958-132">Can add existing customers</span></span>

    - <span data-ttu-id="86958-133">Nie można zażądać relacji z nowymi klientami</span><span class="sxs-lookup"><span data-stu-id="86958-133">Cannot request relationships with new customers</span></span>

    - <span data-ttu-id="86958-134">Nie można mieć relacji z odsprzedawcą pośrednim</span><span class="sxs-lookup"><span data-stu-id="86958-134">Cannot have a relationship with an Indirect reseller</span></span>

    <span data-ttu-id="86958-135">**Odsprzedawca pośredni:**</span><span class="sxs-lookup"><span data-stu-id="86958-135">**Indirect reseller**:</span></span> 

    -   <span data-ttu-id="86958-136">Może mieć relacje z istniejącymi klientami</span><span class="sxs-lookup"><span data-stu-id="86958-136">Can have a relationships with existing customers</span></span>

    -   <span data-ttu-id="86958-137">Nie można zażądać nowych relacji lub dodać nowych klientów</span><span class="sxs-lookup"><span data-stu-id="86958-137">Cannot request new relationships or add new customers</span></span>

    ### <a name="in-partner-center"></a><span data-ttu-id="86958-138">W Partner Center</span><span class="sxs-lookup"><span data-stu-id="86958-138">In Partner Center</span></span>

    <span data-ttu-id="86958-139">**Partnerzy rozliczani bezpośrednio:**</span><span class="sxs-lookup"><span data-stu-id="86958-139">**Direct bill partners**:</span></span>

    -   <span data-ttu-id="86958-140">Może dodawać nowych klientów</span><span class="sxs-lookup"><span data-stu-id="86958-140">Can add new customers</span></span>

    -   <span data-ttu-id="86958-141">Może żądać relacji z nowymi klientami</span><span class="sxs-lookup"><span data-stu-id="86958-141">Can request relationships with new customers</span></span>

    <span data-ttu-id="86958-142">**Dostawcy pośredni:**</span><span class="sxs-lookup"><span data-stu-id="86958-142">**Indirect providers**:</span></span>

    -   <span data-ttu-id="86958-143">Może dodawać nowych klientów</span><span class="sxs-lookup"><span data-stu-id="86958-143">Can add new customers</span></span>

    -   <span data-ttu-id="86958-144">Może żądać relacji z nowymi klientami</span><span class="sxs-lookup"><span data-stu-id="86958-144">Can request relationships with new customers</span></span>

    -   <span data-ttu-id="86958-145">Może mieć relacje z odsprzedawcami pośrednimi</span><span class="sxs-lookup"><span data-stu-id="86958-145">Can have relationships with indirect resellers</span></span>

    <span data-ttu-id="86958-146">**Odsprzedawcy pośredni:**</span><span class="sxs-lookup"><span data-stu-id="86958-146">**Indirect resellers**:</span></span>

    -   <span data-ttu-id="86958-147">Nie można dodać nowych klientów</span><span class="sxs-lookup"><span data-stu-id="86958-147">Can’t add new customers</span></span>

    -   <span data-ttu-id="86958-148">Może żądać relacji z nowymi klientami</span><span class="sxs-lookup"><span data-stu-id="86958-148">Can request relationships with new customers</span></span>


<span data-ttu-id="86958-149">Postępuj zgodnie [z działem usuwania relacji](remove-a-reseller-relationship-with-a-customer.md) odsprzedawcy dla klienta, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="86958-149">Follow the [Remove Reseller Relationship](remove-a-reseller-relationship-with-a-customer.md) for the customer for details.</span></span> <span data-ttu-id="86958-150">Istnieją jednak pewne różnice między możliwościami produktów i piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="86958-150">However, there are some differences between the Product and Sandbox capabilities.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="86958-151">SKŁADNIA ŻĄDANIA</span><span class="sxs-lookup"><span data-stu-id="86958-151">REQUEST SYNTAX</span></span>

|<span data-ttu-id="86958-152">**Metoda**</span><span class="sxs-lookup"><span data-stu-id="86958-152">**Method**</span></span>|<span data-ttu-id="86958-153">**Usuwanie**</span><span class="sxs-lookup"><span data-stu-id="86958-153">**Delete**</span></span>|
|-------------|------------|
|<span data-ttu-id="86958-154">Usuń</span><span class="sxs-lookup"><span data-stu-id="86958-154">Delete</span></span>|<span data-ttu-id="86958-155">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="86958-155">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span> |

<span data-ttu-id="86958-156">Brak treści żądania</span><span class="sxs-lookup"><span data-stu-id="86958-156">Request body None</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="86958-157">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="86958-157">Response success and error codes</span></span>

<span data-ttu-id="86958-158">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="86958-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="86958-159">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="86958-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="86958-160">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](./error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="86958-160">For the full list, see [Partner Center REST error codes](./error-codes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="86958-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="86958-161">Next steps</span></span>

- [<span data-ttu-id="86958-162">Aktywowanie subskrypcji piaskownicy dla Azure Marketplace produktów</span><span class="sxs-lookup"><span data-stu-id="86958-162">Activate Sandbox subscriptions for Azure Marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

- [<span data-ttu-id="86958-163">Anulowanie zamówienia z piaskownicy</span><span class="sxs-lookup"><span data-stu-id="86958-163">Cancel an order from Sandbox</span></span>](cancel-an-order-from-the-integration-sandbox.md)

- [<span data-ttu-id="86958-164">Testowanie i debugowanie</span><span class="sxs-lookup"><span data-stu-id="86958-164">Test and debug</span></span>](test-and-debug.md)