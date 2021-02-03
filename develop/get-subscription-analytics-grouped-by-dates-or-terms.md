---
title: Pobieranie usługi Subscription Analytics pogrupowane według dat lub warunków
description: Jak uzyskać informacje o usłudze Subscription Analytics pogrupowane według dat lub warunków.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4a9946027fa89f5a93fff5eede86e36a6be5b721
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767909"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a><span data-ttu-id="da8cb-103">Pobieranie usługi Subscription Analytics pogrupowane według dat lub warunków</span><span class="sxs-lookup"><span data-stu-id="da8cb-103">Get subscription analytics grouped by dates or terms</span></span>

<span data-ttu-id="da8cb-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="da8cb-104">**Applies To**</span></span>

- <span data-ttu-id="da8cb-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="da8cb-105">Partner Center</span></span>
- <span data-ttu-id="da8cb-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="da8cb-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="da8cb-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="da8cb-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="da8cb-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="da8cb-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="da8cb-109">Jak uzyskać informacje o usłudze Subscription Analytics dla klientów pogrupowane według dat lub warunków.</span><span class="sxs-lookup"><span data-stu-id="da8cb-109">How to get subscription analytics information for your customers grouped by dates or terms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da8cb-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="da8cb-110">Prerequisites</span></span>

- <span data-ttu-id="da8cb-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="da8cb-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="da8cb-112">Ten scenariusz obsługuje tylko uwierzytelnianie z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="da8cb-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="da8cb-113">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="da8cb-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="da8cb-114">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="da8cb-114">Request syntax</span></span>

| <span data-ttu-id="da8cb-115">Metoda</span><span class="sxs-lookup"><span data-stu-id="da8cb-115">Method</span></span> | <span data-ttu-id="da8cb-116">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="da8cb-116">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="da8cb-117">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="da8cb-117">**GET**</span></span> | <span data-ttu-id="da8cb-118">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/V1/Analytics/subscriptions? GroupBy = {groupby_queries}</span><span class="sxs-lookup"><span data-stu-id="da8cb-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?groupby={groupby_queries}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="da8cb-119">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="da8cb-119">URI parameters</span></span>

<span data-ttu-id="da8cb-120">Użyj poniższych wymaganych parametrów ścieżki, aby zidentyfikować organizację i zgrupować wyniki.</span><span class="sxs-lookup"><span data-stu-id="da8cb-120">Use the following required path parameters to identify your organization and to group the results.</span></span>

| <span data-ttu-id="da8cb-121">Nazwa</span><span class="sxs-lookup"><span data-stu-id="da8cb-121">Name</span></span> | <span data-ttu-id="da8cb-122">Typ</span><span class="sxs-lookup"><span data-stu-id="da8cb-122">Type</span></span> | <span data-ttu-id="da8cb-123">Wymagane</span><span class="sxs-lookup"><span data-stu-id="da8cb-123">Required</span></span> | <span data-ttu-id="da8cb-124">Opis</span><span class="sxs-lookup"><span data-stu-id="da8cb-124">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="da8cb-125">groupby_queries</span><span class="sxs-lookup"><span data-stu-id="da8cb-125">groupby_queries</span></span> | <span data-ttu-id="da8cb-126">pary ciągów i dateTime</span><span class="sxs-lookup"><span data-stu-id="da8cb-126">pairs of strings and dateTime</span></span> | <span data-ttu-id="da8cb-127">Tak</span><span class="sxs-lookup"><span data-stu-id="da8cb-127">Yes</span></span> | <span data-ttu-id="da8cb-128">Warunki i daty filtrowania wyniku.</span><span class="sxs-lookup"><span data-stu-id="da8cb-128">The terms and dates to filter the result.</span></span> |

### <a name="groupby-syntax"></a><span data-ttu-id="da8cb-129">Składnia GroupBy</span><span class="sxs-lookup"><span data-stu-id="da8cb-129">GroupBy syntax</span></span>

<span data-ttu-id="da8cb-130">Parametry Group by muszą składać się z serii oddzielonych przecinkami, wartości pól.</span><span class="sxs-lookup"><span data-stu-id="da8cb-130">The group by parameter must be composed as a series of comma separated, field values.</span></span>

<span data-ttu-id="da8cb-131">Niezakodowany przykład wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="da8cb-131">An unencoded example looks like this:</span></span>

```http
?groupby=termField1,dateField1,termField2
```

<span data-ttu-id="da8cb-132">W poniższej tabeli przedstawiono listę obsługiwanych pól dla Grupuj według.</span><span class="sxs-lookup"><span data-stu-id="da8cb-132">The following table shows a list of the supported fields for group by.</span></span>

| <span data-ttu-id="da8cb-133">Pole</span><span class="sxs-lookup"><span data-stu-id="da8cb-133">Field</span></span> | <span data-ttu-id="da8cb-134">Typ</span><span class="sxs-lookup"><span data-stu-id="da8cb-134">Type</span></span> | <span data-ttu-id="da8cb-135">Opis</span><span class="sxs-lookup"><span data-stu-id="da8cb-135">Description</span></span> |
|-------|------|-------------|
| <span data-ttu-id="da8cb-136">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="da8cb-136">customerTenantId</span></span> | <span data-ttu-id="da8cb-137">ciąg</span><span class="sxs-lookup"><span data-stu-id="da8cb-137">string</span></span> | <span data-ttu-id="da8cb-138">Ciąg sformatowany przy użyciu identyfikatora GUID, który identyfikuje dzierżawcę klienta.</span><span class="sxs-lookup"><span data-stu-id="da8cb-138">A GUID-formatted string that identifies the customer tenant.</span></span> |
| <span data-ttu-id="da8cb-139">customerName</span><span class="sxs-lookup"><span data-stu-id="da8cb-139">customerName</span></span> | <span data-ttu-id="da8cb-140">ciąg</span><span class="sxs-lookup"><span data-stu-id="da8cb-140">string</span></span> | <span data-ttu-id="da8cb-141">Nazwa klienta.</span><span class="sxs-lookup"><span data-stu-id="da8cb-141">The name of the customer.</span></span> |
| <span data-ttu-id="da8cb-142">customerMarket</span><span class="sxs-lookup"><span data-stu-id="da8cb-142">customerMarket</span></span> | <span data-ttu-id="da8cb-143">ciąg</span><span class="sxs-lookup"><span data-stu-id="da8cb-143">string</span></span> | <span data-ttu-id="da8cb-144">Kraj/region, w którym klient wykonuje działalność.</span><span class="sxs-lookup"><span data-stu-id="da8cb-144">The country/region that the customer does business in.</span></span> |
| <span data-ttu-id="da8cb-145">identyfikator</span><span class="sxs-lookup"><span data-stu-id="da8cb-145">id</span></span> | <span data-ttu-id="da8cb-146">ciąg</span><span class="sxs-lookup"><span data-stu-id="da8cb-146">string</span></span> | <span data-ttu-id="da8cb-147">Ciąg w formacie GUID, który identyfikuje subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="da8cb-147">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="da8cb-148">status</span><span class="sxs-lookup"><span data-stu-id="da8cb-148">status</span></span> | <span data-ttu-id="da8cb-149">ciąg</span><span class="sxs-lookup"><span data-stu-id="da8cb-149">string</span></span> | <span data-ttu-id="da8cb-150">Stan subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="da8cb-150">The subscription status.</span></span> <span data-ttu-id="da8cb-151">Obsługiwane wartości to: "ACTIVE", "SUSPENDed" lub "unsupportedd".</span><span class="sxs-lookup"><span data-stu-id="da8cb-151">Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".</span></span> |
| <span data-ttu-id="da8cb-152">productName</span><span class="sxs-lookup"><span data-stu-id="da8cb-152">productName</span></span> | <span data-ttu-id="da8cb-153">ciąg</span><span class="sxs-lookup"><span data-stu-id="da8cb-153">string</span></span> | <span data-ttu-id="da8cb-154">Nazwa produktu.</span><span class="sxs-lookup"><span data-stu-id="da8cb-154">The name of the product.</span></span> |
| <span data-ttu-id="da8cb-155">SubscriptionType</span><span class="sxs-lookup"><span data-stu-id="da8cb-155">subscriptionType</span></span> | <span data-ttu-id="da8cb-156">ciąg</span><span class="sxs-lookup"><span data-stu-id="da8cb-156">string</span></span> | <span data-ttu-id="da8cb-157">Typ subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="da8cb-157">The subscription type.</span></span> <span data-ttu-id="da8cb-158">Uwaga: w tym polu jest uwzględniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="da8cb-158">Note: This field is case sensitive.</span></span> <span data-ttu-id="da8cb-159">Obsługiwane są następujące wartości: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span><span class="sxs-lookup"><span data-stu-id="da8cb-159">Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span></span> |
| <span data-ttu-id="da8cb-160">autoRenewEnabled</span><span class="sxs-lookup"><span data-stu-id="da8cb-160">autoRenewEnabled</span></span> | <span data-ttu-id="da8cb-161">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="da8cb-161">Boolean</span></span> | <span data-ttu-id="da8cb-162">Wartość wskazująca, czy subskrypcja jest odnawiana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="da8cb-162">A value indicating whether the subscription is renewed automatically.</span></span> |
| <span data-ttu-id="da8cb-163">partnerId</span><span class="sxs-lookup"><span data-stu-id="da8cb-163">partnerId</span></span>  | <span data-ttu-id="da8cb-164">ciąg</span><span class="sxs-lookup"><span data-stu-id="da8cb-164">string</span></span> | <span data-ttu-id="da8cb-165">IDENTYFIKATOR MPN.</span><span class="sxs-lookup"><span data-stu-id="da8cb-165">The MPN ID.</span></span> <span data-ttu-id="da8cb-166">Dla bezpośredniego odsprzedawcy ten parametr będzie IDENTYFIKATORem MPN partnera.</span><span class="sxs-lookup"><span data-stu-id="da8cb-166">For a direct reseller, this parameter will be the MPN ID of the partner.</span></span> <span data-ttu-id="da8cb-167">W odniesieniu do pośredniego odsprzedawcy ten parametr będzie IDENTYFIKATORem MPN pośredniego odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="da8cb-167">For an indirect reseller, this parameter will be the MPN ID of the indirect reseller.</span></span> |
| <span data-ttu-id="da8cb-168">friendlyName</span><span class="sxs-lookup"><span data-stu-id="da8cb-168">friendlyName</span></span> | <span data-ttu-id="da8cb-169">ciąg</span><span class="sxs-lookup"><span data-stu-id="da8cb-169">string</span></span> | <span data-ttu-id="da8cb-170">Nazwa subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="da8cb-170">The name of the subscription.</span></span> |
| <span data-ttu-id="da8cb-171">partnerName</span><span class="sxs-lookup"><span data-stu-id="da8cb-171">partnerName</span></span> | <span data-ttu-id="da8cb-172">ciąg</span><span class="sxs-lookup"><span data-stu-id="da8cb-172">string</span></span> | <span data-ttu-id="da8cb-173">Nazwa partnera, dla którego została zakupiona subskrypcja</span><span class="sxs-lookup"><span data-stu-id="da8cb-173">Name of the partner for whom the subscription was purchased</span></span> |
| <span data-ttu-id="da8cb-174">providerName</span><span class="sxs-lookup"><span data-stu-id="da8cb-174">providerName</span></span> | <span data-ttu-id="da8cb-175">ciąg</span><span class="sxs-lookup"><span data-stu-id="da8cb-175">string</span></span> | <span data-ttu-id="da8cb-176">Gdy transakcja subskrypcyjna dotyczy pośredniego odsprzedawcy, nazwa dostawcy jest dostawcą pośrednim, który kupił subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="da8cb-176">When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.</span></span>
| <span data-ttu-id="da8cb-177">creationDate</span><span class="sxs-lookup"><span data-stu-id="da8cb-177">creationDate</span></span> | <span data-ttu-id="da8cb-178">ciąg w formacie daty i godziny czasu UTC</span><span class="sxs-lookup"><span data-stu-id="da8cb-178">string in UTC date time format</span></span> | <span data-ttu-id="da8cb-179">Data utworzenia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="da8cb-179">The date the subscription was created.</span></span> |
| <span data-ttu-id="da8cb-180">effectiveStartDate</span><span class="sxs-lookup"><span data-stu-id="da8cb-180">effectiveStartDate</span></span> | <span data-ttu-id="da8cb-181">ciąg w formacie daty i godziny czasu UTC</span><span class="sxs-lookup"><span data-stu-id="da8cb-181">string in UTC date time format</span></span> | <span data-ttu-id="da8cb-182">Data rozpoczęcia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="da8cb-182">The date the subscription starts.</span></span> |
| <span data-ttu-id="da8cb-183">commitmentEndDate</span><span class="sxs-lookup"><span data-stu-id="da8cb-183">commitmentEndDate</span></span> | <span data-ttu-id="da8cb-184">ciąg w formacie daty i godziny czasu UTC</span><span class="sxs-lookup"><span data-stu-id="da8cb-184">string in UTC date time format</span></span> | <span data-ttu-id="da8cb-185">Data zakończenia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="da8cb-185">The date the subscription ends.</span></span> |
| <span data-ttu-id="da8cb-186">currentStateEndDate</span><span class="sxs-lookup"><span data-stu-id="da8cb-186">currentStateEndDate</span></span> | <span data-ttu-id="da8cb-187">ciąg w formacie daty i godziny czasu UTC</span><span class="sxs-lookup"><span data-stu-id="da8cb-187">string in UTC date time format</span></span> | <span data-ttu-id="da8cb-188">Data zmiany bieżącego stanu subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="da8cb-188">The date that the current status of the subscription will change.</span></span> |
| <span data-ttu-id="da8cb-189">trialToPaidConversionDate</span><span class="sxs-lookup"><span data-stu-id="da8cb-189">trialToPaidConversionDate</span></span> | <span data-ttu-id="da8cb-190">ciąg w formacie daty i godziny czasu UTC</span><span class="sxs-lookup"><span data-stu-id="da8cb-190">string in UTC date time format</span></span> | <span data-ttu-id="da8cb-191">Data konwersji subskrypcji z wersji próbnej na płatne.</span><span class="sxs-lookup"><span data-stu-id="da8cb-191">The date that the subscription converts from trial to paid.</span></span> <span data-ttu-id="da8cb-192">Wartość domyślna to null.</span><span class="sxs-lookup"><span data-stu-id="da8cb-192">The default value is null.</span></span> |
| <span data-ttu-id="da8cb-193">trialStartDate</span><span class="sxs-lookup"><span data-stu-id="da8cb-193">trialStartDate</span></span> | <span data-ttu-id="da8cb-194">ciąg w formacie daty i godziny czasu UTC</span><span class="sxs-lookup"><span data-stu-id="da8cb-194">string in UTC date time format</span></span> | <span data-ttu-id="da8cb-195">Data rozpoczęcia okresu próbnego dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="da8cb-195">The date that the trial period for the subscription started.</span></span> <span data-ttu-id="da8cb-196">Wartość domyślna to null.</span><span class="sxs-lookup"><span data-stu-id="da8cb-196">The default value is null.</span></span> |
| <span data-ttu-id="da8cb-197">lastUsageDate</span><span class="sxs-lookup"><span data-stu-id="da8cb-197">lastUsageDate</span></span> | <span data-ttu-id="da8cb-198">ciąg w formacie daty i godziny czasu UTC</span><span class="sxs-lookup"><span data-stu-id="da8cb-198">string in UTC date time format</span></span> | <span data-ttu-id="da8cb-199">Data ostatniego użycia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="da8cb-199">The date that the subscription was last used.</span></span> <span data-ttu-id="da8cb-200">Wartość domyślna to null.</span><span class="sxs-lookup"><span data-stu-id="da8cb-200">The default value is null.</span></span> |
| <span data-ttu-id="da8cb-201">deprovisionedDate</span><span class="sxs-lookup"><span data-stu-id="da8cb-201">deprovisionedDate</span></span> | <span data-ttu-id="da8cb-202">ciąg w formacie daty i godziny czasu UTC</span><span class="sxs-lookup"><span data-stu-id="da8cb-202">string in UTC date time format</span></span> | <span data-ttu-id="da8cb-203">Data anulowania aprowizacji subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="da8cb-203">The date that the subscription was deprovisioned.</span></span> <span data-ttu-id="da8cb-204">Wartość domyślna to null.</span><span class="sxs-lookup"><span data-stu-id="da8cb-204">The default value is null.</span></span> |
| <span data-ttu-id="da8cb-205">lastRenewalDate</span><span class="sxs-lookup"><span data-stu-id="da8cb-205">lastRenewalDate</span></span> | <span data-ttu-id="da8cb-206">ciąg w formacie daty i godziny czasu UTC</span><span class="sxs-lookup"><span data-stu-id="da8cb-206">string in UTC date time format</span></span> | <span data-ttu-id="da8cb-207">Data ostatniego odnowienia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="da8cb-207">The date that the subscription was last renewed.</span></span> <span data-ttu-id="da8cb-208">Wartość domyślna to null.</span><span class="sxs-lookup"><span data-stu-id="da8cb-208">The default value is null.</span></span> |

### <a name="filter-fields"></a><span data-ttu-id="da8cb-209">Pola filtru</span><span class="sxs-lookup"><span data-stu-id="da8cb-209">Filter fields</span></span>

<span data-ttu-id="da8cb-210">W poniższej tabeli wymieniono opcjonalne pola filtrów i ich opisy:</span><span class="sxs-lookup"><span data-stu-id="da8cb-210">The following table lists optional filter fields and their descriptions:</span></span>

| <span data-ttu-id="da8cb-211">Pole</span><span class="sxs-lookup"><span data-stu-id="da8cb-211">Field</span></span> | <span data-ttu-id="da8cb-212">Typ</span><span class="sxs-lookup"><span data-stu-id="da8cb-212">Type</span></span> |  <span data-ttu-id="da8cb-213">Opis</span><span class="sxs-lookup"><span data-stu-id="da8cb-213">Description</span></span> |
|-------|------|--------------|
| <span data-ttu-id="da8cb-214">top (pierwsze)</span><span class="sxs-lookup"><span data-stu-id="da8cb-214">top</span></span> | <span data-ttu-id="da8cb-215">int</span><span class="sxs-lookup"><span data-stu-id="da8cb-215">int</span></span> | <span data-ttu-id="da8cb-216">Liczba wierszy danych do zwrócenia w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="da8cb-216">The number of rows of data to return in the request.</span></span> <span data-ttu-id="da8cb-217">Jeśli wartość nie jest określona, wartość maksymalna i wartość domyślna to 10000.</span><span class="sxs-lookup"><span data-stu-id="da8cb-217">If the value isn't specified, the maximum value and the default value are 10000.</span></span> <span data-ttu-id="da8cb-218">Jeśli zapytanie zawiera więcej wierszy, treść odpowiedzi obejmuje następny link, którego można użyć do żądania następnej strony danych.</span><span class="sxs-lookup"><span data-stu-id="da8cb-218">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> |
| <span data-ttu-id="da8cb-219">Pomiń</span><span class="sxs-lookup"><span data-stu-id="da8cb-219">skip</span></span> | <span data-ttu-id="da8cb-220">int</span><span class="sxs-lookup"><span data-stu-id="da8cb-220">int</span></span> | <span data-ttu-id="da8cb-221">Liczba wierszy do pominięcia w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="da8cb-221">The number of rows to skip in the query.</span></span> <span data-ttu-id="da8cb-222">Użyj tego parametru, aby uzyskać stronę z dużymi zestawami danych.</span><span class="sxs-lookup"><span data-stu-id="da8cb-222">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="da8cb-223">Na przykład: Top = 10000 i Skip = 0 pobiera pierwsze 10000 wierszy danych, Top = 10000 i Skip = 10000 pobiera następne 10000 wierszy danych.</span><span class="sxs-lookup"><span data-stu-id="da8cb-223">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data.</span></span> |
| <span data-ttu-id="da8cb-224">filter</span><span class="sxs-lookup"><span data-stu-id="da8cb-224">filter</span></span> | <span data-ttu-id="da8cb-225">ciąg</span><span class="sxs-lookup"><span data-stu-id="da8cb-225">string</span></span> | <span data-ttu-id="da8cb-226">Jedna lub więcej instrukcji, które filtrują wiersze w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="da8cb-226">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="da8cb-227">Każda instrukcja filtru zawiera nazwę pola z treści odpowiedzi i wartość, która jest skojarzona z **`eq`** , **`ne`** lub dla niektórych pól, **`contains`** operatora.</span><span class="sxs-lookup"><span data-stu-id="da8cb-227">Each filter statement contains a field name from the response body and a value that are associated with the **`eq`**, **`ne`**, or for certain fields, the **`contains`** operator.</span></span> <span data-ttu-id="da8cb-228">Instrukcje można łączyć przy użyciu **`and`** lub **`or`** .</span><span class="sxs-lookup"><span data-stu-id="da8cb-228">Statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="da8cb-229">Wartości ciągu muszą być ujęte w pojedyncze cudzysłowy w parametrze Filter.</span><span class="sxs-lookup"><span data-stu-id="da8cb-229">String values must be surrounded by single quotes in the filter parameter.</span></span> <span data-ttu-id="da8cb-230">W poniższej sekcji znajduje się lista pól, które można filtrować i operatory, które są obsługiwane przez te pola.</span><span class="sxs-lookup"><span data-stu-id="da8cb-230">See the following section for a list of fields that can be filtered and the operators that are supported with those fields.</span></span> |
| <span data-ttu-id="da8cb-231">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="da8cb-231">aggregationLevel</span></span> | <span data-ttu-id="da8cb-232">ciąg</span><span class="sxs-lookup"><span data-stu-id="da8cb-232">string</span></span> | <span data-ttu-id="da8cb-233">Określa zakres czasu, dla którego mają zostać pobrane zagregowane dane.</span><span class="sxs-lookup"><span data-stu-id="da8cb-233">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="da8cb-234">Może to być jeden z następujących ciągów: **dzień**, **tydzień** lub **miesiąc**.</span><span class="sxs-lookup"><span data-stu-id="da8cb-234">Can be one of the following strings: **day**, **week**, or **month**.</span></span> <span data-ttu-id="da8cb-235">Jeśli wartość nie jest określona, wartością domyślną jest **dateRange**.</span><span class="sxs-lookup"><span data-stu-id="da8cb-235">If the value isn't specified, the default is **dateRange**.</span></span> <span data-ttu-id="da8cb-236">**Uwaga**: ten parametr ma zastosowanie tylko wtedy, gdy pole daty jest przesyłane jako część parametru GroupBy.</span><span class="sxs-lookup"><span data-stu-id="da8cb-236">**Note**: This parameter applies only when a date field is passed as part of the groupBy parameter.</span></span> |
| <span data-ttu-id="da8cb-237">groupBy</span><span class="sxs-lookup"><span data-stu-id="da8cb-237">groupBy</span></span> | <span data-ttu-id="da8cb-238">ciąg</span><span class="sxs-lookup"><span data-stu-id="da8cb-238">string</span></span> | <span data-ttu-id="da8cb-239">Instrukcja, która stosuje agregację danych tylko do określonych pól.</span><span class="sxs-lookup"><span data-stu-id="da8cb-239">A statement that applies data aggregation only to the specified fields.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="da8cb-240">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="da8cb-240">Request headers</span></span>

<span data-ttu-id="da8cb-241">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="da8cb-241">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="da8cb-242">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="da8cb-242">Request body</span></span>

<span data-ttu-id="da8cb-243">Brak.</span><span class="sxs-lookup"><span data-stu-id="da8cb-243">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="da8cb-244">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="da8cb-244">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="da8cb-245">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="da8cb-245">REST response</span></span>

<span data-ttu-id="da8cb-246">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [subskrypcji](partner-center-analytics-resources.md#subscription-resource) pogrupowanych według określonych warunków i dat.</span><span class="sxs-lookup"><span data-stu-id="da8cb-246">If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription-resource) resources grouped by the specified terms and dates.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="da8cb-247">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="da8cb-247">Response success and error codes</span></span>

<span data-ttu-id="da8cb-248">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="da8cb-248">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="da8cb-249">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="da8cb-249">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="da8cb-250">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="da8cb-250">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="da8cb-251">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="da8cb-251">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
{
  "Value": [
    {
      "subscriptionType": "Azure",
      "subscriptionCount": "63",
      "licenseCount": "0"
    },
    {
      "subscriptionType": "Dynamics",
      "subscriptionCount": "62",
      "licenseCount": "405"
    },
    {
      "subscriptionType": "EMS",
      "subscriptionCount": "39",
      "licenseCount": "193"
    },
    {
      "subscriptionType": "M365",
      "subscriptionCount": "2",
      "licenseCount": "5"
    },
    {
      "subscriptionType": "Office",
      "subscriptionCount": "906",
      "licenseCount": "7485"
    },
    {
      "subscriptionType": "UNKNOWN",
      "subscriptionCount": "104",
      "licenseCount": "439"
    },
    {
      "subscriptionType": "Windows",
      "subscriptionCount": "2",
      "licenseCount": "2"
    }
  ],
  "@nextLink": null,
  "TotalCount": 7
}
```

## <a name="see-also"></a><span data-ttu-id="da8cb-252">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="da8cb-252">See also</span></span>

[<span data-ttu-id="da8cb-253">Analiza Centrum partnerskiego — zasoby</span><span class="sxs-lookup"><span data-stu-id="da8cb-253">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
