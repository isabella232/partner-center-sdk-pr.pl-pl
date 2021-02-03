---
title: Tworzenie transferu
description: Jak utworzyć transfer subskrypcji dla klienta.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d5e70cc5b7ce4fcfa715f581a2151f0b8d1922b0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767761"
---
# <a name="create-a-transfer"></a><span data-ttu-id="a93d9-103">Tworzenie transferu</span><span class="sxs-lookup"><span data-stu-id="a93d9-103">Create a transfer</span></span>

<span data-ttu-id="a93d9-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="a93d9-104">**Applies to:**</span></span>

- <span data-ttu-id="a93d9-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="a93d9-105">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a93d9-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a93d9-106">Prerequisites</span></span>

- <span data-ttu-id="a93d9-107">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a93d9-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a93d9-108">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a93d9-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a93d9-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a93d9-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a93d9-110">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="a93d9-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a93d9-111">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="a93d9-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a93d9-112">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="a93d9-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a93d9-113">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="a93d9-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a93d9-114">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a93d9-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="a93d9-115">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="a93d9-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a93d9-116">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="a93d9-116">Request syntax</span></span>

| <span data-ttu-id="a93d9-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="a93d9-117">Method</span></span>   | <span data-ttu-id="a93d9-118">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="a93d9-118">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a93d9-119">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="a93d9-119">**POST**</span></span> | <span data-ttu-id="a93d9-120">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/Transfers http/1.1</span><span class="sxs-lookup"><span data-stu-id="a93d9-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="a93d9-121">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="a93d9-121">URI parameter</span></span>

<span data-ttu-id="a93d9-122">Użyj następującego parametru ścieżki, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="a93d9-122">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="a93d9-123">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a93d9-123">Name</span></span>            | <span data-ttu-id="a93d9-124">Typ</span><span class="sxs-lookup"><span data-stu-id="a93d9-124">Type</span></span>     | <span data-ttu-id="a93d9-125">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a93d9-125">Required</span></span> | <span data-ttu-id="a93d9-126">Opis</span><span class="sxs-lookup"><span data-stu-id="a93d9-126">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="a93d9-127">**Identyfikator klienta**</span><span class="sxs-lookup"><span data-stu-id="a93d9-127">**customer-id**</span></span> | <span data-ttu-id="a93d9-128">ciąg</span><span class="sxs-lookup"><span data-stu-id="a93d9-128">string</span></span>   | <span data-ttu-id="a93d9-129">Tak</span><span class="sxs-lookup"><span data-stu-id="a93d9-129">Yes</span></span>      | <span data-ttu-id="a93d9-130">Identyfikator GUID sformatowany przez klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="a93d9-130">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="a93d9-131">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="a93d9-131">Request headers</span></span>

<span data-ttu-id="a93d9-132">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a93d9-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a93d9-133">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a93d9-133">Request body</span></span>

<span data-ttu-id="a93d9-134">W tej tabeli opisano właściwości [TransferEntity](transfer-entity-resources.md) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="a93d9-134">This table describes the [TransferEntity](transfer-entity-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="a93d9-135">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a93d9-135">Property</span></span>              | <span data-ttu-id="a93d9-136">Typ</span><span class="sxs-lookup"><span data-stu-id="a93d9-136">Type</span></span>          | <span data-ttu-id="a93d9-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a93d9-137">Required</span></span>  | <span data-ttu-id="a93d9-138">Opis</span><span class="sxs-lookup"><span data-stu-id="a93d9-138">Description</span></span>                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="a93d9-139">identyfikator</span><span class="sxs-lookup"><span data-stu-id="a93d9-139">id</span></span>                    | <span data-ttu-id="a93d9-140">ciąg</span><span class="sxs-lookup"><span data-stu-id="a93d9-140">string</span></span>        | <span data-ttu-id="a93d9-141">Nie</span><span class="sxs-lookup"><span data-stu-id="a93d9-141">No</span></span>    | <span data-ttu-id="a93d9-142">Identyfikator transferEntity, który jest dostarczany po pomyślnym utworzeniu transferEntity.</span><span class="sxs-lookup"><span data-stu-id="a93d9-142">A transferEntity identifier that is supplied upon successful creation of the transferEntity.</span></span>                               |
| <span data-ttu-id="a93d9-143">createdTime</span><span class="sxs-lookup"><span data-stu-id="a93d9-143">createdTime</span></span>           | <span data-ttu-id="a93d9-144">DateTime</span><span class="sxs-lookup"><span data-stu-id="a93d9-144">DateTime</span></span>      | <span data-ttu-id="a93d9-145">Nie</span><span class="sxs-lookup"><span data-stu-id="a93d9-145">No</span></span>    | <span data-ttu-id="a93d9-146">Data, w której utworzono transferEntity, w formacie daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="a93d9-146">The date the transferEntity was created, in date-time format.</span></span> <span data-ttu-id="a93d9-147">Stosowane po pomyślnym utworzeniu transferEntity.</span><span class="sxs-lookup"><span data-stu-id="a93d9-147">Applied upon successful creation of the transferEntity.</span></span>      |
| <span data-ttu-id="a93d9-148">lastModifiedTime</span><span class="sxs-lookup"><span data-stu-id="a93d9-148">lastModifiedTime</span></span>      | <span data-ttu-id="a93d9-149">DateTime</span><span class="sxs-lookup"><span data-stu-id="a93d9-149">DateTime</span></span>      | <span data-ttu-id="a93d9-150">Nie</span><span class="sxs-lookup"><span data-stu-id="a93d9-150">No</span></span>    | <span data-ttu-id="a93d9-151">Data ostatniej aktualizacji transferEntity w formacie daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="a93d9-151">The date the transferEntity was last updated, in date-time format.</span></span> <span data-ttu-id="a93d9-152">Stosowane po pomyślnym utworzeniu transferEntity.</span><span class="sxs-lookup"><span data-stu-id="a93d9-152">Applied upon successful creation of the transferEntity.</span></span> |
| <span data-ttu-id="a93d9-153">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="a93d9-153">lastModifiedUser</span></span>      | <span data-ttu-id="a93d9-154">ciąg</span><span class="sxs-lookup"><span data-stu-id="a93d9-154">string</span></span>        | <span data-ttu-id="a93d9-155">Nie</span><span class="sxs-lookup"><span data-stu-id="a93d9-155">No</span></span>    | <span data-ttu-id="a93d9-156">Użytkownik, który ostatnio zaktualizował transferEntity.</span><span class="sxs-lookup"><span data-stu-id="a93d9-156">The user who last updated the transferEntity.</span></span> <span data-ttu-id="a93d9-157">Stosowane po pomyślnym utworzeniu transferEntity.</span><span class="sxs-lookup"><span data-stu-id="a93d9-157">Applied upon successful creation of transferEntity.</span></span>                          |
| <span data-ttu-id="a93d9-158">customerName</span><span class="sxs-lookup"><span data-stu-id="a93d9-158">customerName</span></span>          | <span data-ttu-id="a93d9-159">ciąg</span><span class="sxs-lookup"><span data-stu-id="a93d9-159">string</span></span>        | <span data-ttu-id="a93d9-160">Nie</span><span class="sxs-lookup"><span data-stu-id="a93d9-160">No</span></span>    | <span data-ttu-id="a93d9-161">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="a93d9-161">Optional.</span></span> <span data-ttu-id="a93d9-162">Nazwa klienta, którego subskrypcje są transferowane.</span><span class="sxs-lookup"><span data-stu-id="a93d9-162">The name of the customer whose subscriptions are being transferred.</span></span>                                              |
| <span data-ttu-id="a93d9-163">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="a93d9-163">customerTenantId</span></span>      | <span data-ttu-id="a93d9-164">ciąg</span><span class="sxs-lookup"><span data-stu-id="a93d9-164">string</span></span>        | <span data-ttu-id="a93d9-165">Nie</span><span class="sxs-lookup"><span data-stu-id="a93d9-165">No</span></span>    | <span data-ttu-id="a93d9-166">Identyfikator GUID sformatowany przez klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="a93d9-166">A GUID formatted customer-id that identifies the customer.</span></span> <span data-ttu-id="a93d9-167">Stosowane po pomyślnym utworzeniu transferEntity.</span><span class="sxs-lookup"><span data-stu-id="a93d9-167">Applied upon successful creation of the transferEntity.</span></span>         |
| <span data-ttu-id="a93d9-168">partnertenantid</span><span class="sxs-lookup"><span data-stu-id="a93d9-168">partnertenantid</span></span>       | <span data-ttu-id="a93d9-169">ciąg</span><span class="sxs-lookup"><span data-stu-id="a93d9-169">string</span></span>        | <span data-ttu-id="a93d9-170">Nie</span><span class="sxs-lookup"><span data-stu-id="a93d9-170">No</span></span>    | <span data-ttu-id="a93d9-171">Identyfikator GUID w formacie identyfikatora partnera, który identyfikuje partnera.</span><span class="sxs-lookup"><span data-stu-id="a93d9-171">A GUID formatted partner-id that identifies the partner.</span></span>                                                                   |
| <span data-ttu-id="a93d9-172">sourcePartnerName</span><span class="sxs-lookup"><span data-stu-id="a93d9-172">sourcePartnerName</span></span>     | <span data-ttu-id="a93d9-173">ciąg</span><span class="sxs-lookup"><span data-stu-id="a93d9-173">string</span></span>        | <span data-ttu-id="a93d9-174">Nie</span><span class="sxs-lookup"><span data-stu-id="a93d9-174">No</span></span>    | <span data-ttu-id="a93d9-175">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="a93d9-175">Optional.</span></span> <span data-ttu-id="a93d9-176">Nazwa organizacji partnera, która inicjuje transfer.</span><span class="sxs-lookup"><span data-stu-id="a93d9-176">The name of the partner's organization who is initiating the transfer.</span></span>                                           |
| <span data-ttu-id="a93d9-177">sourcePartnerTenantId</span><span class="sxs-lookup"><span data-stu-id="a93d9-177">sourcePartnerTenantId</span></span> | <span data-ttu-id="a93d9-178">ciąg</span><span class="sxs-lookup"><span data-stu-id="a93d9-178">string</span></span>        | <span data-ttu-id="a93d9-179">Tak</span><span class="sxs-lookup"><span data-stu-id="a93d9-179">Yes</span></span>   | <span data-ttu-id="a93d9-180">Identyfikator GUID w formacie identyfikatora partnera, który identyfikuje partnera inicjującego transfer.</span><span class="sxs-lookup"><span data-stu-id="a93d9-180">A GUID formatted partner-id that identifies the partner initiating the transfer.</span></span>                                           |
| <span data-ttu-id="a93d9-181">targetPartnerName</span><span class="sxs-lookup"><span data-stu-id="a93d9-181">targetPartnerName</span></span>     | <span data-ttu-id="a93d9-182">ciąg</span><span class="sxs-lookup"><span data-stu-id="a93d9-182">string</span></span>        | <span data-ttu-id="a93d9-183">Nie</span><span class="sxs-lookup"><span data-stu-id="a93d9-183">No</span></span>    | <span data-ttu-id="a93d9-184">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="a93d9-184">Optional.</span></span> <span data-ttu-id="a93d9-185">Nazwa organizacji partnera, do której przeznaczony jest transfer.</span><span class="sxs-lookup"><span data-stu-id="a93d9-185">The name of the partner's organization to whom the transfer is targeted.</span></span>                                         |
| <span data-ttu-id="a93d9-186">targetPartnerTenantId</span><span class="sxs-lookup"><span data-stu-id="a93d9-186">targetPartnerTenantId</span></span> | <span data-ttu-id="a93d9-187">ciąg</span><span class="sxs-lookup"><span data-stu-id="a93d9-187">string</span></span>        | <span data-ttu-id="a93d9-188">Tak</span><span class="sxs-lookup"><span data-stu-id="a93d9-188">Yes</span></span>   | <span data-ttu-id="a93d9-189">Identyfikator partnera w formacie GUID, który identyfikuje partnera, do którego jest przeznaczony transfer.</span><span class="sxs-lookup"><span data-stu-id="a93d9-189">A GUID formatted partner-id that identifies the partner to whom the transfer is targeted.</span></span>                                  |
| <span data-ttu-id="a93d9-190">lineItems</span><span class="sxs-lookup"><span data-stu-id="a93d9-190">lineItems</span></span>             | <span data-ttu-id="a93d9-191">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="a93d9-191">Array of objects</span></span> | <span data-ttu-id="a93d9-192">Tak</span><span class="sxs-lookup"><span data-stu-id="a93d9-192">Yes</span></span>| <span data-ttu-id="a93d9-193">Tablica zasobów [TransferLineItem](transfer-entity-resources.md#transferlineitem) .</span><span class="sxs-lookup"><span data-stu-id="a93d9-193">An Array of [TransferLineItem](transfer-entity-resources.md#transferlineitem) resources.</span></span>                                   |
| <span data-ttu-id="a93d9-194">status</span><span class="sxs-lookup"><span data-stu-id="a93d9-194">status</span></span>                | <span data-ttu-id="a93d9-195">ciąg</span><span class="sxs-lookup"><span data-stu-id="a93d9-195">string</span></span>        | <span data-ttu-id="a93d9-196">Nie</span><span class="sxs-lookup"><span data-stu-id="a93d9-196">No</span></span>    | <span data-ttu-id="a93d9-197">Stan transferEntity.</span><span class="sxs-lookup"><span data-stu-id="a93d9-197">The status of the transferEntity.</span></span> <span data-ttu-id="a93d9-198">Możliwe wartości to "Active" (można je usunąć/przesłać) i "ukończone" (zostały już ukończone).</span><span class="sxs-lookup"><span data-stu-id="a93d9-198">Possible values are "Active" (can be deleted/submitted) and "Completed" (has already been completed).</span></span> <span data-ttu-id="a93d9-199">Stosowane po pomyślnym utworzeniu transferEntity.</span><span class="sxs-lookup"><span data-stu-id="a93d9-199">Applied upon successful creation of the transferEntity.</span></span>|

<span data-ttu-id="a93d9-200">W tej tabeli opisano właściwości [TransferLineItem](transfer-entity-resources.md#transferlineitem) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="a93d9-200">This table describes the [TransferLineItem](transfer-entity-resources.md#transferlineitem) properties in the request body.</span></span>

|      <span data-ttu-id="a93d9-201">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a93d9-201">Property</span></span>       |            <span data-ttu-id="a93d9-202">Typ</span><span class="sxs-lookup"><span data-stu-id="a93d9-202">Type</span></span>             | <span data-ttu-id="a93d9-203">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a93d9-203">Required</span></span> | <span data-ttu-id="a93d9-204">Opis</span><span class="sxs-lookup"><span data-stu-id="a93d9-204">Description</span></span>                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a93d9-205">identyfikator</span><span class="sxs-lookup"><span data-stu-id="a93d9-205">id</span></span>                   | <span data-ttu-id="a93d9-206">ciąg</span><span class="sxs-lookup"><span data-stu-id="a93d9-206">string</span></span>                     | <span data-ttu-id="a93d9-207">Nie</span><span class="sxs-lookup"><span data-stu-id="a93d9-207">No</span></span>       | <span data-ttu-id="a93d9-208">Unikatowy identyfikator elementu wiersza przeniesienia.</span><span class="sxs-lookup"><span data-stu-id="a93d9-208">A unique identifier for a transfer line item.</span></span> <span data-ttu-id="a93d9-209">Stosowane po pomyślnym utworzeniu transferEntity.</span><span class="sxs-lookup"><span data-stu-id="a93d9-209">Applied upon successful creation of the transferEntity.</span></span>|
| <span data-ttu-id="a93d9-210">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="a93d9-210">subscriptionId</span></span>       | <span data-ttu-id="a93d9-211">ciąg</span><span class="sxs-lookup"><span data-stu-id="a93d9-211">string</span></span>                     | <span data-ttu-id="a93d9-212">Tak</span><span class="sxs-lookup"><span data-stu-id="a93d9-212">Yes</span></span>      | <span data-ttu-id="a93d9-213">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a93d9-213">The subscription identifier.</span></span>                                                                         |
| <span data-ttu-id="a93d9-214">quantity</span><span class="sxs-lookup"><span data-stu-id="a93d9-214">quantity</span></span>             | <span data-ttu-id="a93d9-215">int</span><span class="sxs-lookup"><span data-stu-id="a93d9-215">int</span></span>                        | <span data-ttu-id="a93d9-216">Nie</span><span class="sxs-lookup"><span data-stu-id="a93d9-216">No</span></span>       | <span data-ttu-id="a93d9-217">Liczba licencji lub wystąpień.</span><span class="sxs-lookup"><span data-stu-id="a93d9-217">The number of licenses or instances.</span></span>                                                                 |
| <span data-ttu-id="a93d9-218">billingCycle</span><span class="sxs-lookup"><span data-stu-id="a93d9-218">billingCycle</span></span>         | <span data-ttu-id="a93d9-219">Obiekt</span><span class="sxs-lookup"><span data-stu-id="a93d9-219">Object</span></span>                     | <span data-ttu-id="a93d9-220">Nie</span><span class="sxs-lookup"><span data-stu-id="a93d9-220">No</span></span>       | <span data-ttu-id="a93d9-221">Typ cyklu rozliczeniowego ustawiony dla bieżącego okresu.</span><span class="sxs-lookup"><span data-stu-id="a93d9-221">The type of billing cycle set for the current period.</span></span>                                                |
| <span data-ttu-id="a93d9-222">friendlyName</span><span class="sxs-lookup"><span data-stu-id="a93d9-222">friendlyName</span></span>         | <span data-ttu-id="a93d9-223">ciąg</span><span class="sxs-lookup"><span data-stu-id="a93d9-223">string</span></span>                     | <span data-ttu-id="a93d9-224">Nie</span><span class="sxs-lookup"><span data-stu-id="a93d9-224">No</span></span>       | <span data-ttu-id="a93d9-225">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="a93d9-225">Optional.</span></span> <span data-ttu-id="a93d9-226">Przyjazna nazwa dla elementu zdefiniowanego przez partnera, która pomaga w odróżnieniu od siebie.</span><span class="sxs-lookup"><span data-stu-id="a93d9-226">The friendly name for the item defined by the partner to help disambiguate.</span></span>                |
| <span data-ttu-id="a93d9-227">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="a93d9-227">partnerIdOnRecord</span></span>    | <span data-ttu-id="a93d9-228">ciąg</span><span class="sxs-lookup"><span data-stu-id="a93d9-228">string</span></span>                     | <span data-ttu-id="a93d9-229">Nie</span><span class="sxs-lookup"><span data-stu-id="a93d9-229">No</span></span>       | <span data-ttu-id="a93d9-230">PartnerId on Record (MPNID) zakupu, który ma miejsce, gdy transfer zostanie zaakceptowany.</span><span class="sxs-lookup"><span data-stu-id="a93d9-230">PartnerId on Record (MPNID) on the purchase that happens when the transfer is accepted.</span></span>              |
| <span data-ttu-id="a93d9-231">offerId</span><span class="sxs-lookup"><span data-stu-id="a93d9-231">offerId</span></span>              | <span data-ttu-id="a93d9-232">ciąg</span><span class="sxs-lookup"><span data-stu-id="a93d9-232">string</span></span>                     | <span data-ttu-id="a93d9-233">Nie</span><span class="sxs-lookup"><span data-stu-id="a93d9-233">No</span></span>       | <span data-ttu-id="a93d9-234">Identyfikator oferty.</span><span class="sxs-lookup"><span data-stu-id="a93d9-234">The offer identifier.</span></span>                                                                                |
| <span data-ttu-id="a93d9-235">addonItems</span><span class="sxs-lookup"><span data-stu-id="a93d9-235">addonItems</span></span>           | <span data-ttu-id="a93d9-236">Lista obiektów **TransferLineItem**</span><span class="sxs-lookup"><span data-stu-id="a93d9-236">List of **TransferLineItem** objects</span></span> | <span data-ttu-id="a93d9-237">Nie</span><span class="sxs-lookup"><span data-stu-id="a93d9-237">No</span></span> | <span data-ttu-id="a93d9-238">Kolekcja elementów transferEntity line dla dodatków, które będą transferowane wraz z subskrypcją podstawową, która jest transferowana.</span><span class="sxs-lookup"><span data-stu-id="a93d9-238">A collection of transferEntity line items for addons that will be transferred along with the base subscription that is being transferred.</span></span> <span data-ttu-id="a93d9-239">Stosowane po pomyślnym utworzeniu transferEntity.</span><span class="sxs-lookup"><span data-stu-id="a93d9-239">Applied upon successful creation of the transferEntity.</span></span>|
| <span data-ttu-id="a93d9-240">transferError</span><span class="sxs-lookup"><span data-stu-id="a93d9-240">transferError</span></span>        | <span data-ttu-id="a93d9-241">ciąg</span><span class="sxs-lookup"><span data-stu-id="a93d9-241">string</span></span>                     | <span data-ttu-id="a93d9-242">Nie</span><span class="sxs-lookup"><span data-stu-id="a93d9-242">No</span></span>       | <span data-ttu-id="a93d9-243">Stosowane po zaakceptowaniu transferEntity w przypadku błędu.</span><span class="sxs-lookup"><span data-stu-id="a93d9-243">Applied after transferEntity is accepted in case of an error.</span></span>                                        |
| <span data-ttu-id="a93d9-244">status</span><span class="sxs-lookup"><span data-stu-id="a93d9-244">status</span></span>               | <span data-ttu-id="a93d9-245">ciąg</span><span class="sxs-lookup"><span data-stu-id="a93d9-245">string</span></span>                     | <span data-ttu-id="a93d9-246">Nie</span><span class="sxs-lookup"><span data-stu-id="a93d9-246">No</span></span>       | <span data-ttu-id="a93d9-247">Stan LineItem w transferEntity.</span><span class="sxs-lookup"><span data-stu-id="a93d9-247">The status of the lineitem in the transferEntity.</span></span>                                                    |

### <a name="request-example"></a><span data-ttu-id="a93d9-248">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="a93d9-248">Request example</span></span>

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Expect: 100-continue

{
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lineItems": [
        {
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "partnerIdOnRecord": "517285"
        },
        {
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "partnerIdOnRecord": "517285"
        }
    ]
}
```

## <a name="rest-response"></a><span data-ttu-id="a93d9-249">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="a93d9-249">REST response</span></span>

<span data-ttu-id="a93d9-250">Jeśli to się powiedzie, ta metoda zwraca wypełniony zasób [TransferEnity](transfer-entity-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="a93d9-250">If successful, this method returns the populated [TransferEnity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a93d9-251">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a93d9-251">Response success and error codes</span></span>

<span data-ttu-id="a93d9-252">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="a93d9-252">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a93d9-253">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="a93d9-253">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a93d9-254">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a93d9-254">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a93d9-255">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a93d9-255">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 138
Content-Type: application/json; charset=utf-8
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US,en-US
{
    "id": "67c5b05b-09b5-47ba-9047-5056fe2afa4f",
    "status": "Active",
    "createdTime": "2020-03-24T20:44:14.9602781Z",
    "lastModifiedTime": "2020-03-24T20:44:15Z",
    "customerTenantId": "823c6c3f-9259-4d51-bae2-5dd06743177f",
    "partnertenantid": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lastModifiedUser": "d0648481-b615-45c9-8cd1-ff87940dbdc4",
    "lineItems": [
        {
            "id": 0,
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "offerId": "50E9A47A-7B4D-4970-9D90-CAE927F53753",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 for Sales Enterprise Attach to Qualifying Dynamics 365 Base Offer",
            "quantity": 1,
            "addonItems": [
                {
                    "id": 0,
                    "subscriptionId": "D738C6C9-DDBD-46E9-B316-65F9D9B3ECB4",
                    "offerId": "2BCF9FE8-8B65-4FCF-9240-419203FB8CF4",
                    "billingCycle": "annual",
                    "friendlyName": "Dynamics 365 - Additional Production Instance (Qualified Offer)",
                    "quantity": 4
                }
            ]
        },
        {
            "id": 0,
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "offerId": "455DDD41-32ED-4E2D-B3A2-BBCB22CAA467",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 Customer Engagement Plan Patch",
            "quantity": 8,
            "addonItems": []
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "TransferEntity"
    }
}
```
