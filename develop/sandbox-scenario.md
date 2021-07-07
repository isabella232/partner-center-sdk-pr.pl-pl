---
title: Możliwości piaskownicy dla relacji odsprzedawcy
description: Piaskownica partnera ma możliwość obsługi relacji między partnerem a klientem
ms.date: 05/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: aa6c4fb9ef71bacfad7e0f1510fec15f6af60a05
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547397"
---
# <a name="sandbox-capabilities-for-reseller-relationship"></a><span data-ttu-id="7d627-103">Możliwości piaskownicy dla relacji odsprzedawcy</span><span class="sxs-lookup"><span data-stu-id="7d627-103">Sandbox capabilities for Reseller relationship</span></span>

<span data-ttu-id="7d627-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="7d627-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7d627-105">W tym artykule wyjaśniono, co jest obsługiwane w piaskownicy w przypadku relacji odsprzedawcy między partnerem a klientem.</span><span class="sxs-lookup"><span data-stu-id="7d627-105">This article explains what is supported in the Sandbox for reseller relationships between the partner and the customer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7d627-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7d627-106">Prerequisites</span></span>

- <span data-ttu-id="7d627-107">Partner Center poświadczenia konta.</span><span class="sxs-lookup"><span data-stu-id="7d627-107">Partner Center account credentials.</span></span> <span data-ttu-id="7d627-108">Scenariusz piaskownicy obsługuje uwierzytelnianie zarówno przy użyciu autonomicznej aplikacji, jak i poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7d627-108">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span>
- <span data-ttu-id="7d627-109">Identyfikator klienta (customer-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="7d627-109">A customer ID (customer-tenant-id).</span></span> <span data-ttu-id="7d627-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard/home).</span><span class="sxs-lookup"><span data-stu-id="7d627-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard/home).</span></span> <span data-ttu-id="7d627-111">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="7d627-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7d627-112">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="7d627-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7d627-113">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="7d627-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7d627-114">Identyfikator microsoft jest taki sam jak identyfikator klienta (customer-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="7d627-114">The Microsoft ID is the same as the customer ID (customer-tenant-id).</span></span>
- <span data-ttu-id="7d627-115">Wszystkie Azure Reserved Virtual Machine Instances i zamówienia zakupu oprogramowania muszą zostać anulowane przed usunięciem klienta z piaskownicy integracji Porada.</span><span class="sxs-lookup"><span data-stu-id="7d627-115">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="scenarios-supporting-reseller-relationship"></a><span data-ttu-id="7d627-116">Scenariusze obsługi relacji odsprzedawcy</span><span class="sxs-lookup"><span data-stu-id="7d627-116">Scenarios Supporting Reseller Relationship</span></span>

1.  <span data-ttu-id="7d627-117">Partnerzy rozliczani bezpośrednio w piaskownicy i dostawcy pośredni mogą tworzyć relacje z klientem piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="7d627-117">Sandbox Direct Bill Partners and Indirect Providers can create relationships with the Sandbox customer.</span></span> 
2.  <span data-ttu-id="7d627-118">Partnerzy rozliczani bezpośrednio i dostawcy pośredni piaskownicy nie mogą zapraszać klientów piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="7d627-118">Sandbox Direct Bill Partners and Indirect Providers cannot invite Sandbox customers.</span></span>

3. <span data-ttu-id="7d627-119">Dostawcy pośredni i partner rozliczani bezpośrednio w piaskownicy mogą usunąć relację odsprzedawcy z interfejsu Partner Center i interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="7d627-119">Sandbox Direct Bill Partner and Indirect Providers are able to remove reseller relationship from Partner Center UI and API.</span></span>

4. <span data-ttu-id="7d627-120">W przypadku relacji odsprzedawcy usunięcia piaskownicy zostanie wywołana nazwa Usuń klienta AP.</span><span class="sxs-lookup"><span data-stu-id="7d627-120">Sandbox Remove Reseller Relationship will call Delete customer AP.</span></span> <span data-ttu-id="7d627-121">Spowoduje to usunięcie relacji i dzierżawy klienta.</span><span class="sxs-lookup"><span data-stu-id="7d627-121">This will remove the relationship and delete the customer tenant.</span></span> <span data-ttu-id="7d627-122">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="7d627-122">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span>


    ### <a name="in-the-sandbox"></a><span data-ttu-id="7d627-123">W piaskownicy</span><span class="sxs-lookup"><span data-stu-id="7d627-123">In the Sandbox</span></span>

    <span data-ttu-id="7d627-124">**Partnerzy rozliczani bezpośrednio:**</span><span class="sxs-lookup"><span data-stu-id="7d627-124">**Direct bill partners**:</span></span>

    - <span data-ttu-id="7d627-125">Może dodawać istniejących klientów</span><span class="sxs-lookup"><span data-stu-id="7d627-125">Can add existing customers</span></span>

    - <span data-ttu-id="7d627-126">Nie można zażądać relacji z nowymi klientami</span><span class="sxs-lookup"><span data-stu-id="7d627-126">Cannot request relationships with new customers</span></span>

    <span data-ttu-id="7d627-127">**Dostawcy pośredni:**</span><span class="sxs-lookup"><span data-stu-id="7d627-127">**Indirect providers**:</span></span>

    - <span data-ttu-id="7d627-128">Może dodawać istniejących klientów</span><span class="sxs-lookup"><span data-stu-id="7d627-128">Can add existing customers</span></span>

    - <span data-ttu-id="7d627-129">Nie można zażądać relacji z nowymi klientami</span><span class="sxs-lookup"><span data-stu-id="7d627-129">Cannot request relationships with new customers</span></span>

    - <span data-ttu-id="7d627-130">Nie można mieć relacji z odsprzedawcą pośrednim</span><span class="sxs-lookup"><span data-stu-id="7d627-130">Cannot have a relationship with an Indirect reseller</span></span>

    <span data-ttu-id="7d627-131">**Odsprzedawca pośredni:**</span><span class="sxs-lookup"><span data-stu-id="7d627-131">**Indirect reseller**:</span></span> 

    -   <span data-ttu-id="7d627-132">Może mieć relacje z istniejącymi klientami</span><span class="sxs-lookup"><span data-stu-id="7d627-132">Can have relationships with existing customers</span></span>

    -   <span data-ttu-id="7d627-133">Nie można zażądać nowych relacji lub dodać nowych klientów</span><span class="sxs-lookup"><span data-stu-id="7d627-133">Cannot request new relationships or add new customers</span></span>

    ### <a name="in-partner-center"></a><span data-ttu-id="7d627-134">W Partner Center</span><span class="sxs-lookup"><span data-stu-id="7d627-134">In Partner Center</span></span>

    <span data-ttu-id="7d627-135">**Partnerzy rozliczani bezpośrednio:**</span><span class="sxs-lookup"><span data-stu-id="7d627-135">**Direct bill partners**:</span></span>

    -   <span data-ttu-id="7d627-136">Może dodawać nowych klientów</span><span class="sxs-lookup"><span data-stu-id="7d627-136">Can add new customers</span></span>

    -   <span data-ttu-id="7d627-137">Może żądać relacji z nowymi klientami</span><span class="sxs-lookup"><span data-stu-id="7d627-137">Can request relationships with new customers</span></span>

    <span data-ttu-id="7d627-138">**Dostawcy pośredni:**</span><span class="sxs-lookup"><span data-stu-id="7d627-138">**Indirect providers**:</span></span>

    -   <span data-ttu-id="7d627-139">Może dodawać nowych klientów</span><span class="sxs-lookup"><span data-stu-id="7d627-139">Can add new customers</span></span>

    -   <span data-ttu-id="7d627-140">Może żądać relacji z nowymi klientami</span><span class="sxs-lookup"><span data-stu-id="7d627-140">Can request relationships with new customers</span></span>

    -   <span data-ttu-id="7d627-141">Może mieć relacje z odsprzedawcami pośrednimi</span><span class="sxs-lookup"><span data-stu-id="7d627-141">Can have relationships with indirect resellers</span></span>

    <span data-ttu-id="7d627-142">**Odsprzedawcy pośredni:**</span><span class="sxs-lookup"><span data-stu-id="7d627-142">**Indirect resellers**:</span></span>

    -   <span data-ttu-id="7d627-143">Nie można dodać nowych klientów</span><span class="sxs-lookup"><span data-stu-id="7d627-143">Can’t add new customers</span></span>

    -   <span data-ttu-id="7d627-144">Może żądać relacji z nowymi klientami</span><span class="sxs-lookup"><span data-stu-id="7d627-144">Can request relationships with new customers</span></span>


<span data-ttu-id="7d627-145">Aby uzyskać [szczegółowe informacje,](remove-a-reseller-relationship-with-a-customer.md) postępuj zgodnie z działem usuwania relacji odsprzedawcy dla klienta.</span><span class="sxs-lookup"><span data-stu-id="7d627-145">Follow the [Remove Reseller Relationship](remove-a-reseller-relationship-with-a-customer.md) for the customer for details.</span></span> <span data-ttu-id="7d627-146">Istnieją jednak pewne różnice między możliwościami produktów i piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="7d627-146">However, there are some differences between the Product and Sandbox capabilities.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7d627-147">SKŁADNIA ŻĄDANIA</span><span class="sxs-lookup"><span data-stu-id="7d627-147">REQUEST SYNTAX</span></span>

|<span data-ttu-id="7d627-148">**Metoda**</span><span class="sxs-lookup"><span data-stu-id="7d627-148">**Method**</span></span>|<span data-ttu-id="7d627-149">**Usuwanie**</span><span class="sxs-lookup"><span data-stu-id="7d627-149">**Delete**</span></span>|
|-------------|------------|
|<span data-ttu-id="7d627-150">Usuń</span><span class="sxs-lookup"><span data-stu-id="7d627-150">Delete</span></span>|<span data-ttu-id="7d627-151">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="7d627-151">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span> |

<span data-ttu-id="7d627-152">Brak treści żądania</span><span class="sxs-lookup"><span data-stu-id="7d627-152">Request body None</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7d627-153">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7d627-153">Response success and error codes</span></span>

<span data-ttu-id="7d627-154">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="7d627-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7d627-155">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="7d627-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7d627-156">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](./error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="7d627-156">For the full list, see [Partner Center REST error codes](./error-codes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d627-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7d627-157">Next steps</span></span>

- [<span data-ttu-id="7d627-158">Aktywowanie subskrypcji piaskownicy dla Azure Marketplace produktów</span><span class="sxs-lookup"><span data-stu-id="7d627-158">Activate Sandbox subscriptions for Azure Marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

- [<span data-ttu-id="7d627-159">Anulowanie zamówienia z piaskownicy</span><span class="sxs-lookup"><span data-stu-id="7d627-159">Cancel an order from Sandbox</span></span>](cancel-an-order-from-the-integration-sandbox.md)

- [<span data-ttu-id="7d627-160">Testowanie i debugowanie</span><span class="sxs-lookup"><span data-stu-id="7d627-160">Test and debug</span></span>](test-and-debug.md)