---
title: Tworzenie transferu
description: Jak utworzyć przeniesienie subskrypcji dla klienta.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d459a0a96912ab27f312bc73af16af2d4fdb518c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973710"
---
# <a name="create-a-transfer"></a><span data-ttu-id="7f32d-103">Tworzenie transferu</span><span class="sxs-lookup"><span data-stu-id="7f32d-103">Create a transfer</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f32d-104">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7f32d-104">Prerequisites</span></span>

- <span data-ttu-id="7f32d-105">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="7f32d-105">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7f32d-106">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7f32d-106">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7f32d-107">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7f32d-107">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7f32d-108">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="7f32d-108">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7f32d-109">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="7f32d-109">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7f32d-110">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="7f32d-110">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7f32d-111">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="7f32d-111">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7f32d-112">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7f32d-112">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="7f32d-113">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="7f32d-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7f32d-114">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="7f32d-114">Request syntax</span></span>

| <span data-ttu-id="7f32d-115">Metoda</span><span class="sxs-lookup"><span data-stu-id="7f32d-115">Method</span></span>   | <span data-ttu-id="7f32d-116">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="7f32d-116">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7f32d-117">**Post**</span><span class="sxs-lookup"><span data-stu-id="7f32d-117">**POST**</span></span> | <span data-ttu-id="7f32d-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/transfery HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7f32d-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="7f32d-119">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="7f32d-119">URI parameter</span></span>

<span data-ttu-id="7f32d-120">Użyj następującego parametru ścieżki, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="7f32d-120">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="7f32d-121">Nazwa</span><span class="sxs-lookup"><span data-stu-id="7f32d-121">Name</span></span>            | <span data-ttu-id="7f32d-122">Typ</span><span class="sxs-lookup"><span data-stu-id="7f32d-122">Type</span></span>     | <span data-ttu-id="7f32d-123">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7f32d-123">Required</span></span> | <span data-ttu-id="7f32d-124">Opis</span><span class="sxs-lookup"><span data-stu-id="7f32d-124">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="7f32d-125">**identyfikator klienta**</span><span class="sxs-lookup"><span data-stu-id="7f32d-125">**customer-id**</span></span> | <span data-ttu-id="7f32d-126">ciąg</span><span class="sxs-lookup"><span data-stu-id="7f32d-126">string</span></span>   | <span data-ttu-id="7f32d-127">Tak</span><span class="sxs-lookup"><span data-stu-id="7f32d-127">Yes</span></span>      | <span data-ttu-id="7f32d-128">Identyfikator GUID sformatowany jako identyfikator klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="7f32d-128">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="7f32d-129">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="7f32d-129">Request headers</span></span>

<span data-ttu-id="7f32d-130">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="7f32d-130">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7f32d-131">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="7f32d-131">Request body</span></span>

<span data-ttu-id="7f32d-132">W tej tabeli opisano [właściwości TransferEntity](transfer-entity-resources.md) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="7f32d-132">This table describes the [TransferEntity](transfer-entity-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="7f32d-133">Właściwość</span><span class="sxs-lookup"><span data-stu-id="7f32d-133">Property</span></span>              | <span data-ttu-id="7f32d-134">Typ</span><span class="sxs-lookup"><span data-stu-id="7f32d-134">Type</span></span>          | <span data-ttu-id="7f32d-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7f32d-135">Required</span></span>  | <span data-ttu-id="7f32d-136">Opis</span><span class="sxs-lookup"><span data-stu-id="7f32d-136">Description</span></span>                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="7f32d-137">identyfikator</span><span class="sxs-lookup"><span data-stu-id="7f32d-137">id</span></span>                    | <span data-ttu-id="7f32d-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="7f32d-138">string</span></span>        | <span data-ttu-id="7f32d-139">Nie</span><span class="sxs-lookup"><span data-stu-id="7f32d-139">No</span></span>    | <span data-ttu-id="7f32d-140">Identyfikator transferEntity, który jest dostarczany po pomyślnym utworzeniu obiektu transferEntity.</span><span class="sxs-lookup"><span data-stu-id="7f32d-140">A transferEntity identifier that is supplied upon successful creation of the transferEntity.</span></span>                               |
| <span data-ttu-id="7f32d-141">createdTime (czas utworzenia)</span><span class="sxs-lookup"><span data-stu-id="7f32d-141">createdTime</span></span>           | <span data-ttu-id="7f32d-142">DateTime</span><span class="sxs-lookup"><span data-stu-id="7f32d-142">DateTime</span></span>      | <span data-ttu-id="7f32d-143">Nie</span><span class="sxs-lookup"><span data-stu-id="7f32d-143">No</span></span>    | <span data-ttu-id="7f32d-144">Data utworzenia przeniesieniaJedność w formacie daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="7f32d-144">The date the transferEntity was created, in date-time format.</span></span> <span data-ttu-id="7f32d-145">Stosowane po pomyślnym utworzeniu transferEntity.</span><span class="sxs-lookup"><span data-stu-id="7f32d-145">Applied upon successful creation of the transferEntity.</span></span>      |
| <span data-ttu-id="7f32d-146">lastModifiedTime</span><span class="sxs-lookup"><span data-stu-id="7f32d-146">lastModifiedTime</span></span>      | <span data-ttu-id="7f32d-147">DateTime</span><span class="sxs-lookup"><span data-stu-id="7f32d-147">DateTime</span></span>      | <span data-ttu-id="7f32d-148">Nie</span><span class="sxs-lookup"><span data-stu-id="7f32d-148">No</span></span>    | <span data-ttu-id="7f32d-149">Data ostatniej aktualizacji transakcji transferEntity w formacie daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="7f32d-149">The date the transferEntity was last updated, in date-time format.</span></span> <span data-ttu-id="7f32d-150">Stosowane po pomyślnym utworzeniu transferEntity.</span><span class="sxs-lookup"><span data-stu-id="7f32d-150">Applied upon successful creation of the transferEntity.</span></span> |
| <span data-ttu-id="7f32d-151">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="7f32d-151">lastModifiedUser</span></span>      | <span data-ttu-id="7f32d-152">ciąg</span><span class="sxs-lookup"><span data-stu-id="7f32d-152">string</span></span>        | <span data-ttu-id="7f32d-153">Nie</span><span class="sxs-lookup"><span data-stu-id="7f32d-153">No</span></span>    | <span data-ttu-id="7f32d-154">Użytkownik, który ostatnio zaktualizował transferEntity.</span><span class="sxs-lookup"><span data-stu-id="7f32d-154">The user who last updated the transferEntity.</span></span> <span data-ttu-id="7f32d-155">Stosowane po pomyślnym utworzeniu transferEntity.</span><span class="sxs-lookup"><span data-stu-id="7f32d-155">Applied upon successful creation of transferEntity.</span></span>                          |
| <span data-ttu-id="7f32d-156">Customername</span><span class="sxs-lookup"><span data-stu-id="7f32d-156">customerName</span></span>          | <span data-ttu-id="7f32d-157">ciąg</span><span class="sxs-lookup"><span data-stu-id="7f32d-157">string</span></span>        | <span data-ttu-id="7f32d-158">Nie</span><span class="sxs-lookup"><span data-stu-id="7f32d-158">No</span></span>    | <span data-ttu-id="7f32d-159">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="7f32d-159">Optional.</span></span> <span data-ttu-id="7f32d-160">Nazwa klienta, którego subskrypcje są przenoszone.</span><span class="sxs-lookup"><span data-stu-id="7f32d-160">The name of the customer whose subscriptions are being transferred.</span></span>                                              |
| <span data-ttu-id="7f32d-161">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="7f32d-161">customerTenantId</span></span>      | <span data-ttu-id="7f32d-162">ciąg</span><span class="sxs-lookup"><span data-stu-id="7f32d-162">string</span></span>        | <span data-ttu-id="7f32d-163">Nie</span><span class="sxs-lookup"><span data-stu-id="7f32d-163">No</span></span>    | <span data-ttu-id="7f32d-164">Identyfikator GUID sformatowany jako identyfikator klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="7f32d-164">A GUID formatted customer-id that identifies the customer.</span></span> <span data-ttu-id="7f32d-165">Stosowane po pomyślnym utworzeniu transferEntity.</span><span class="sxs-lookup"><span data-stu-id="7f32d-165">Applied upon successful creation of the transferEntity.</span></span>         |
| <span data-ttu-id="7f32d-166">partnertenantid</span><span class="sxs-lookup"><span data-stu-id="7f32d-166">partnertenantid</span></span>       | <span data-ttu-id="7f32d-167">ciąg</span><span class="sxs-lookup"><span data-stu-id="7f32d-167">string</span></span>        | <span data-ttu-id="7f32d-168">Nie</span><span class="sxs-lookup"><span data-stu-id="7f32d-168">No</span></span>    | <span data-ttu-id="7f32d-169">Identyfikator GUID sformatowany jako identyfikator partnera, który identyfikuje partnera.</span><span class="sxs-lookup"><span data-stu-id="7f32d-169">A GUID formatted partner-id that identifies the partner.</span></span>                                                                   |
| <span data-ttu-id="7f32d-170">sourcePartnerName (Nazwa partycji źródłowej)</span><span class="sxs-lookup"><span data-stu-id="7f32d-170">sourcePartnerName</span></span>     | <span data-ttu-id="7f32d-171">ciąg</span><span class="sxs-lookup"><span data-stu-id="7f32d-171">string</span></span>        | <span data-ttu-id="7f32d-172">Nie</span><span class="sxs-lookup"><span data-stu-id="7f32d-172">No</span></span>    | <span data-ttu-id="7f32d-173">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="7f32d-173">Optional.</span></span> <span data-ttu-id="7f32d-174">Nazwa organizacji partnera, który inicjuje przeniesienie.</span><span class="sxs-lookup"><span data-stu-id="7f32d-174">The name of the partner's organization who is initiating the transfer.</span></span>                                           |
| <span data-ttu-id="7f32d-175">sourcePartnerTenantId</span><span class="sxs-lookup"><span data-stu-id="7f32d-175">sourcePartnerTenantId</span></span> | <span data-ttu-id="7f32d-176">ciąg</span><span class="sxs-lookup"><span data-stu-id="7f32d-176">string</span></span>        | <span data-ttu-id="7f32d-177">Tak</span><span class="sxs-lookup"><span data-stu-id="7f32d-177">Yes</span></span>   | <span data-ttu-id="7f32d-178">Identyfikator GUID sformatowany jako identyfikator partnera, który identyfikuje partnera inicjujące przeniesienie.</span><span class="sxs-lookup"><span data-stu-id="7f32d-178">A GUID formatted partner-id that identifies the partner initiating the transfer.</span></span>                                           |
| <span data-ttu-id="7f32d-179">targetPartnerName (nazwa_serwera_docelowego)</span><span class="sxs-lookup"><span data-stu-id="7f32d-179">targetPartnerName</span></span>     | <span data-ttu-id="7f32d-180">ciąg</span><span class="sxs-lookup"><span data-stu-id="7f32d-180">string</span></span>        | <span data-ttu-id="7f32d-181">Nie</span><span class="sxs-lookup"><span data-stu-id="7f32d-181">No</span></span>    | <span data-ttu-id="7f32d-182">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="7f32d-182">Optional.</span></span> <span data-ttu-id="7f32d-183">Nazwa organizacji partnera, której celem jest przeniesienie.</span><span class="sxs-lookup"><span data-stu-id="7f32d-183">The name of the partner's organization to whom the transfer is targeted.</span></span>                                         |
| <span data-ttu-id="7f32d-184">targetPartnerTenantId</span><span class="sxs-lookup"><span data-stu-id="7f32d-184">targetPartnerTenantId</span></span> | <span data-ttu-id="7f32d-185">ciąg</span><span class="sxs-lookup"><span data-stu-id="7f32d-185">string</span></span>        | <span data-ttu-id="7f32d-186">Tak</span><span class="sxs-lookup"><span data-stu-id="7f32d-186">Yes</span></span>   | <span data-ttu-id="7f32d-187">Identyfikator GUID sformatowany jako partner-id, który identyfikuje partnera, do którego jest skierowany transfer.</span><span class="sxs-lookup"><span data-stu-id="7f32d-187">A GUID formatted partner-id that identifies the partner to whom the transfer is targeted.</span></span>                                  |
| <span data-ttu-id="7f32d-188">lineItems</span><span class="sxs-lookup"><span data-stu-id="7f32d-188">lineItems</span></span>             | <span data-ttu-id="7f32d-189">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="7f32d-189">Array of objects</span></span> | <span data-ttu-id="7f32d-190">Tak</span><span class="sxs-lookup"><span data-stu-id="7f32d-190">Yes</span></span>| <span data-ttu-id="7f32d-191">Tablica zasobów [TransferLineItem.](transfer-entity-resources.md#transferlineitem)</span><span class="sxs-lookup"><span data-stu-id="7f32d-191">An Array of [TransferLineItem](transfer-entity-resources.md#transferlineitem) resources.</span></span>                                   |
| <span data-ttu-id="7f32d-192">status</span><span class="sxs-lookup"><span data-stu-id="7f32d-192">status</span></span>                | <span data-ttu-id="7f32d-193">ciąg</span><span class="sxs-lookup"><span data-stu-id="7f32d-193">string</span></span>        | <span data-ttu-id="7f32d-194">Nie</span><span class="sxs-lookup"><span data-stu-id="7f32d-194">No</span></span>    | <span data-ttu-id="7f32d-195">Stan transferEntity.</span><span class="sxs-lookup"><span data-stu-id="7f32d-195">The status of the transferEntity.</span></span> <span data-ttu-id="7f32d-196">Możliwe wartości to "Aktywne" (można je usunąć/przesłać) i "Ukończono" (zostało już zakończone).</span><span class="sxs-lookup"><span data-stu-id="7f32d-196">Possible values are "Active" (can be deleted/submitted) and "Completed" (has already been completed).</span></span> <span data-ttu-id="7f32d-197">Stosowane po pomyślnym utworzeniu transferEntity.</span><span class="sxs-lookup"><span data-stu-id="7f32d-197">Applied upon successful creation of the transferEntity.</span></span>|

<span data-ttu-id="7f32d-198">W tej tabeli [opisano właściwości TransferLineItem](transfer-entity-resources.md#transferlineitem) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="7f32d-198">This table describes the [TransferLineItem](transfer-entity-resources.md#transferlineitem) properties in the request body.</span></span>

|      <span data-ttu-id="7f32d-199">Właściwość</span><span class="sxs-lookup"><span data-stu-id="7f32d-199">Property</span></span>       |            <span data-ttu-id="7f32d-200">Typ</span><span class="sxs-lookup"><span data-stu-id="7f32d-200">Type</span></span>             | <span data-ttu-id="7f32d-201">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7f32d-201">Required</span></span> | <span data-ttu-id="7f32d-202">Opis</span><span class="sxs-lookup"><span data-stu-id="7f32d-202">Description</span></span>                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7f32d-203">identyfikator</span><span class="sxs-lookup"><span data-stu-id="7f32d-203">id</span></span>                   | <span data-ttu-id="7f32d-204">ciąg</span><span class="sxs-lookup"><span data-stu-id="7f32d-204">string</span></span>                     | <span data-ttu-id="7f32d-205">Nie</span><span class="sxs-lookup"><span data-stu-id="7f32d-205">No</span></span>       | <span data-ttu-id="7f32d-206">Unikatowy identyfikator elementu wiersza przeniesienia.</span><span class="sxs-lookup"><span data-stu-id="7f32d-206">A unique identifier for a transfer line item.</span></span> <span data-ttu-id="7f32d-207">Stosowane po pomyślnym utworzeniu transferEntity.</span><span class="sxs-lookup"><span data-stu-id="7f32d-207">Applied upon successful creation of the transferEntity.</span></span>|
| <span data-ttu-id="7f32d-208">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7f32d-208">subscriptionId</span></span>       | <span data-ttu-id="7f32d-209">ciąg</span><span class="sxs-lookup"><span data-stu-id="7f32d-209">string</span></span>                     | <span data-ttu-id="7f32d-210">Tak</span><span class="sxs-lookup"><span data-stu-id="7f32d-210">Yes</span></span>      | <span data-ttu-id="7f32d-211">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7f32d-211">The subscription identifier.</span></span>                                                                         |
| <span data-ttu-id="7f32d-212">quantity</span><span class="sxs-lookup"><span data-stu-id="7f32d-212">quantity</span></span>             | <span data-ttu-id="7f32d-213">int</span><span class="sxs-lookup"><span data-stu-id="7f32d-213">int</span></span>                        | <span data-ttu-id="7f32d-214">Nie</span><span class="sxs-lookup"><span data-stu-id="7f32d-214">No</span></span>       | <span data-ttu-id="7f32d-215">Liczba licencji lub wystąpień.</span><span class="sxs-lookup"><span data-stu-id="7f32d-215">The number of licenses or instances.</span></span>                                                                 |
| <span data-ttu-id="7f32d-216">billingCycle</span><span class="sxs-lookup"><span data-stu-id="7f32d-216">billingCycle</span></span>         | <span data-ttu-id="7f32d-217">Obiekt</span><span class="sxs-lookup"><span data-stu-id="7f32d-217">Object</span></span>                     | <span data-ttu-id="7f32d-218">Nie</span><span class="sxs-lookup"><span data-stu-id="7f32d-218">No</span></span>       | <span data-ttu-id="7f32d-219">Typ cyklu rozliczeniowego ustawiony dla bieżącego okresu.</span><span class="sxs-lookup"><span data-stu-id="7f32d-219">The type of billing cycle set for the current period.</span></span>                                                |
| <span data-ttu-id="7f32d-220">Friendlyname</span><span class="sxs-lookup"><span data-stu-id="7f32d-220">friendlyName</span></span>         | <span data-ttu-id="7f32d-221">ciąg</span><span class="sxs-lookup"><span data-stu-id="7f32d-221">string</span></span>                     | <span data-ttu-id="7f32d-222">Nie</span><span class="sxs-lookup"><span data-stu-id="7f32d-222">No</span></span>       | <span data-ttu-id="7f32d-223">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="7f32d-223">Optional.</span></span> <span data-ttu-id="7f32d-224">Przyjazna nazwa elementu zdefiniowanego przez partnera w celu uujednoznania.</span><span class="sxs-lookup"><span data-stu-id="7f32d-224">The friendly name for the item defined by the partner to help disambiguate.</span></span>                |
| <span data-ttu-id="7f32d-225">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="7f32d-225">partnerIdOnRecord</span></span>    | <span data-ttu-id="7f32d-226">ciąg</span><span class="sxs-lookup"><span data-stu-id="7f32d-226">string</span></span>                     | <span data-ttu-id="7f32d-227">Nie</span><span class="sxs-lookup"><span data-stu-id="7f32d-227">No</span></span>       | <span data-ttu-id="7f32d-228">PartnerId on Record (IDENTYFIKATOR MPN) przy zakupie, który ma miejsce po zaakceptowaniu przeniesienia.</span><span class="sxs-lookup"><span data-stu-id="7f32d-228">PartnerId on Record (MPN ID) on the purchase that happens when the transfer is accepted.</span></span>              |
| <span data-ttu-id="7f32d-229">offerId</span><span class="sxs-lookup"><span data-stu-id="7f32d-229">offerId</span></span>              | <span data-ttu-id="7f32d-230">ciąg</span><span class="sxs-lookup"><span data-stu-id="7f32d-230">string</span></span>                     | <span data-ttu-id="7f32d-231">Nie</span><span class="sxs-lookup"><span data-stu-id="7f32d-231">No</span></span>       | <span data-ttu-id="7f32d-232">Identyfikator oferty.</span><span class="sxs-lookup"><span data-stu-id="7f32d-232">The offer identifier.</span></span>                                                                                |
| <span data-ttu-id="7f32d-233">addonItems</span><span class="sxs-lookup"><span data-stu-id="7f32d-233">addonItems</span></span>           | <span data-ttu-id="7f32d-234">Lista obiektów **TransferLineItem**</span><span class="sxs-lookup"><span data-stu-id="7f32d-234">List of **TransferLineItem** objects</span></span> | <span data-ttu-id="7f32d-235">Nie</span><span class="sxs-lookup"><span data-stu-id="7f32d-235">No</span></span> | <span data-ttu-id="7f32d-236">Kolekcja elementów wiersza transferEntity dla dodatków, które zostaną przeniesione wraz z subskrypcją podstawową, która jest przesyłana.</span><span class="sxs-lookup"><span data-stu-id="7f32d-236">A collection of transferEntity line items for addons that will be transferred along with the base subscription that is being transferred.</span></span> <span data-ttu-id="7f32d-237">Stosowane po pomyślnym utworzeniu transferEntity.</span><span class="sxs-lookup"><span data-stu-id="7f32d-237">Applied upon successful creation of the transferEntity.</span></span>|
| <span data-ttu-id="7f32d-238">transferError</span><span class="sxs-lookup"><span data-stu-id="7f32d-238">transferError</span></span>        | <span data-ttu-id="7f32d-239">ciąg</span><span class="sxs-lookup"><span data-stu-id="7f32d-239">string</span></span>                     | <span data-ttu-id="7f32d-240">Nie</span><span class="sxs-lookup"><span data-stu-id="7f32d-240">No</span></span>       | <span data-ttu-id="7f32d-241">Zastosowane po transferEntity jest akceptowana, jeśli wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="7f32d-241">Applied after transferEntity is accepted if there is an error.</span></span>                                        |
| <span data-ttu-id="7f32d-242">status</span><span class="sxs-lookup"><span data-stu-id="7f32d-242">status</span></span>               | <span data-ttu-id="7f32d-243">ciąg</span><span class="sxs-lookup"><span data-stu-id="7f32d-243">string</span></span>                     | <span data-ttu-id="7f32d-244">Nie</span><span class="sxs-lookup"><span data-stu-id="7f32d-244">No</span></span>       | <span data-ttu-id="7f32d-245">Stan lineitem w transferEntity.</span><span class="sxs-lookup"><span data-stu-id="7f32d-245">The status of the lineitem in the transferEntity.</span></span>                                                    |

### <a name="request-example"></a><span data-ttu-id="7f32d-246">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="7f32d-246">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="7f32d-247">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="7f32d-247">REST response</span></span>

<span data-ttu-id="7f32d-248">W przypadku powodzenia ta metoda zwraca wypełniony [zasób TransferEnity](transfer-entity-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="7f32d-248">If successful, this method returns the populated [TransferEnity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7f32d-249">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7f32d-249">Response success and error codes</span></span>

<span data-ttu-id="7f32d-250">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="7f32d-250">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7f32d-251">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="7f32d-251">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7f32d-252">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7f32d-252">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7f32d-253">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7f32d-253">Response example</span></span>

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
