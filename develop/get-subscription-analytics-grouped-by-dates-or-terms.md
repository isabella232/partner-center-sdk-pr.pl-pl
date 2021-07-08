---
title: Uzyskiwanie analizy subskrypcji pogrupowanych według dat lub terminów
description: Jak uzyskać informacje dotyczące analizy subskrypcji pogrupowane według dat lub terminów.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8192a9863d53ec8697a7341cd38c69200614bd4a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548723"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a><span data-ttu-id="274bf-103">Uzyskiwanie analizy subskrypcji pogrupowanych według dat lub terminów</span><span class="sxs-lookup"><span data-stu-id="274bf-103">Get subscription analytics grouped by dates or terms</span></span>

<span data-ttu-id="274bf-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="274bf-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="274bf-105">Jak uzyskać informacje analityczne dotyczące subskrypcji dla klientów pogrupowane według dat lub terminów.</span><span class="sxs-lookup"><span data-stu-id="274bf-105">How to get subscription analytics information for your customers grouped by dates or terms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="274bf-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="274bf-106">Prerequisites</span></span>

- <span data-ttu-id="274bf-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="274bf-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="274bf-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="274bf-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="274bf-109">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="274bf-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="274bf-110">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="274bf-110">Request syntax</span></span>

| <span data-ttu-id="274bf-111">Metoda</span><span class="sxs-lookup"><span data-stu-id="274bf-111">Method</span></span> | <span data-ttu-id="274bf-112">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="274bf-112">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="274bf-113">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="274bf-113">**GET**</span></span> | <span data-ttu-id="274bf-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?groupby={groupby_queries}</span><span class="sxs-lookup"><span data-stu-id="274bf-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?groupby={groupby_queries}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="274bf-115">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="274bf-115">URI parameters</span></span>

<span data-ttu-id="274bf-116">Użyj następujących wymaganych parametrów ścieżki, aby zidentyfikować organizację i pogrupować wyniki.</span><span class="sxs-lookup"><span data-stu-id="274bf-116">Use the following required path parameters to identify your organization and to group the results.</span></span>

| <span data-ttu-id="274bf-117">Nazwa</span><span class="sxs-lookup"><span data-stu-id="274bf-117">Name</span></span> | <span data-ttu-id="274bf-118">Typ</span><span class="sxs-lookup"><span data-stu-id="274bf-118">Type</span></span> | <span data-ttu-id="274bf-119">Wymagane</span><span class="sxs-lookup"><span data-stu-id="274bf-119">Required</span></span> | <span data-ttu-id="274bf-120">Opis</span><span class="sxs-lookup"><span data-stu-id="274bf-120">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="274bf-121">groupby_queries</span><span class="sxs-lookup"><span data-stu-id="274bf-121">groupby_queries</span></span> | <span data-ttu-id="274bf-122">pary ciągów i dateTime</span><span class="sxs-lookup"><span data-stu-id="274bf-122">pairs of strings and dateTime</span></span> | <span data-ttu-id="274bf-123">Tak</span><span class="sxs-lookup"><span data-stu-id="274bf-123">Yes</span></span> | <span data-ttu-id="274bf-124">Terminy i daty do filtrowania wyniku.</span><span class="sxs-lookup"><span data-stu-id="274bf-124">The terms and dates to filter the result.</span></span> |

### <a name="groupby-syntax"></a><span data-ttu-id="274bf-125">Składnia grupowania</span><span class="sxs-lookup"><span data-stu-id="274bf-125">GroupBy syntax</span></span>

<span data-ttu-id="274bf-126">Parametr grupowania musi składać się z serii wartości pól rozdzielonych przecinkami.</span><span class="sxs-lookup"><span data-stu-id="274bf-126">The group by parameter must be composed as a series of comma separated, field values.</span></span>

<span data-ttu-id="274bf-127">Niezakodowany przykład wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="274bf-127">An unencoded example looks like this:</span></span>

```http
?groupby=termField1,dateField1,termField2
```

<span data-ttu-id="274bf-128">W poniższej tabeli przedstawiono listę obsługiwanych pól dla grupowania według.</span><span class="sxs-lookup"><span data-stu-id="274bf-128">The following table shows a list of the supported fields for group by.</span></span>

| <span data-ttu-id="274bf-129">Pole</span><span class="sxs-lookup"><span data-stu-id="274bf-129">Field</span></span> | <span data-ttu-id="274bf-130">Typ</span><span class="sxs-lookup"><span data-stu-id="274bf-130">Type</span></span> | <span data-ttu-id="274bf-131">Opis</span><span class="sxs-lookup"><span data-stu-id="274bf-131">Description</span></span> |
|-------|------|-------------|
| <span data-ttu-id="274bf-132">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="274bf-132">customerTenantId</span></span> | <span data-ttu-id="274bf-133">ciąg</span><span class="sxs-lookup"><span data-stu-id="274bf-133">string</span></span> | <span data-ttu-id="274bf-134">Ciąg w formacie identyfikatora GUID, który identyfikuje dzierżawę klienta.</span><span class="sxs-lookup"><span data-stu-id="274bf-134">A GUID-formatted string that identifies the customer tenant.</span></span> |
| <span data-ttu-id="274bf-135">Customername</span><span class="sxs-lookup"><span data-stu-id="274bf-135">customerName</span></span> | <span data-ttu-id="274bf-136">ciąg</span><span class="sxs-lookup"><span data-stu-id="274bf-136">string</span></span> | <span data-ttu-id="274bf-137">Nazwa klienta.</span><span class="sxs-lookup"><span data-stu-id="274bf-137">The name of the customer.</span></span> |
| <span data-ttu-id="274bf-138">customerMarket</span><span class="sxs-lookup"><span data-stu-id="274bf-138">customerMarket</span></span> | <span data-ttu-id="274bf-139">ciąg</span><span class="sxs-lookup"><span data-stu-id="274bf-139">string</span></span> | <span data-ttu-id="274bf-140">Kraj/region, w którym klient działa.</span><span class="sxs-lookup"><span data-stu-id="274bf-140">The country/region that the customer does business in.</span></span> |
| <span data-ttu-id="274bf-141">identyfikator</span><span class="sxs-lookup"><span data-stu-id="274bf-141">id</span></span> | <span data-ttu-id="274bf-142">ciąg</span><span class="sxs-lookup"><span data-stu-id="274bf-142">string</span></span> | <span data-ttu-id="274bf-143">Ciąg w formacie identyfikatora GUID, który identyfikuje subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="274bf-143">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="274bf-144">status</span><span class="sxs-lookup"><span data-stu-id="274bf-144">status</span></span> | <span data-ttu-id="274bf-145">ciąg</span><span class="sxs-lookup"><span data-stu-id="274bf-145">string</span></span> | <span data-ttu-id="274bf-146">Stan subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="274bf-146">The subscription status.</span></span> <span data-ttu-id="274bf-147">Obsługiwane wartości to: "ACTIVE", "SUSPENDED" lub "DEPROVISIONED".</span><span class="sxs-lookup"><span data-stu-id="274bf-147">Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".</span></span> |
| <span data-ttu-id="274bf-148">Productname</span><span class="sxs-lookup"><span data-stu-id="274bf-148">productName</span></span> | <span data-ttu-id="274bf-149">ciąg</span><span class="sxs-lookup"><span data-stu-id="274bf-149">string</span></span> | <span data-ttu-id="274bf-150">Nazwa produktu.</span><span class="sxs-lookup"><span data-stu-id="274bf-150">The name of the product.</span></span> |
| <span data-ttu-id="274bf-151">Subscriptiontype</span><span class="sxs-lookup"><span data-stu-id="274bf-151">subscriptionType</span></span> | <span data-ttu-id="274bf-152">ciąg</span><span class="sxs-lookup"><span data-stu-id="274bf-152">string</span></span> | <span data-ttu-id="274bf-153">Typ subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="274bf-153">The subscription type.</span></span> <span data-ttu-id="274bf-154">Uwaga: w tym polu jest zróżnicowa wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="274bf-154">Note: This field is case-sensitive.</span></span> <span data-ttu-id="274bf-155">Obsługiwane wartości to: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span><span class="sxs-lookup"><span data-stu-id="274bf-155">Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span></span> |
| <span data-ttu-id="274bf-156">autoRenewEnabled</span><span class="sxs-lookup"><span data-stu-id="274bf-156">autoRenewEnabled</span></span> | <span data-ttu-id="274bf-157">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="274bf-157">Boolean</span></span> | <span data-ttu-id="274bf-158">Wartość wskazująca, czy subskrypcja jest odnawiana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="274bf-158">A value indicating whether the subscription is renewed automatically.</span></span> |
| <span data-ttu-id="274bf-159">partnerId</span><span class="sxs-lookup"><span data-stu-id="274bf-159">partnerId</span></span>  | <span data-ttu-id="274bf-160">ciąg</span><span class="sxs-lookup"><span data-stu-id="274bf-160">string</span></span> | <span data-ttu-id="274bf-161">Identyfikator MPN.</span><span class="sxs-lookup"><span data-stu-id="274bf-161">The MPN ID.</span></span> <span data-ttu-id="274bf-162">W przypadku odsprzedawcy bezpośredniego ten parametr będzie identyfikatorem MPN partnera.</span><span class="sxs-lookup"><span data-stu-id="274bf-162">For a direct reseller, this parameter will be the MPN ID of the partner.</span></span> <span data-ttu-id="274bf-163">W przypadku odsprzedawcy pośredniego ten parametr będzie identyfikatorem MPN odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="274bf-163">For an indirect reseller, this parameter will be the MPN ID of the indirect reseller.</span></span> |
| <span data-ttu-id="274bf-164">Friendlyname</span><span class="sxs-lookup"><span data-stu-id="274bf-164">friendlyName</span></span> | <span data-ttu-id="274bf-165">ciąg</span><span class="sxs-lookup"><span data-stu-id="274bf-165">string</span></span> | <span data-ttu-id="274bf-166">Nazwa subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="274bf-166">The name of the subscription.</span></span> |
| <span data-ttu-id="274bf-167">nazwa_partnera</span><span class="sxs-lookup"><span data-stu-id="274bf-167">partnerName</span></span> | <span data-ttu-id="274bf-168">ciąg</span><span class="sxs-lookup"><span data-stu-id="274bf-168">string</span></span> | <span data-ttu-id="274bf-169">Nazwa partnera, dla którego zakupiono subskrypcję</span><span class="sxs-lookup"><span data-stu-id="274bf-169">Name of the partner for whom the subscription was purchased</span></span> |
| <span data-ttu-id="274bf-170">Providername</span><span class="sxs-lookup"><span data-stu-id="274bf-170">providerName</span></span> | <span data-ttu-id="274bf-171">ciąg</span><span class="sxs-lookup"><span data-stu-id="274bf-171">string</span></span> | <span data-ttu-id="274bf-172">Gdy transakcja subskrypcji jest dla odsprzedawcy pośredniego, nazwa dostawcy jest dostawcą pośrednim, który kupił subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="274bf-172">When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.</span></span>
| <span data-ttu-id="274bf-173">Creationdate</span><span class="sxs-lookup"><span data-stu-id="274bf-173">creationDate</span></span> | <span data-ttu-id="274bf-174">ciąg w formacie daty i czasu UTC</span><span class="sxs-lookup"><span data-stu-id="274bf-174">string in UTC date time format</span></span> | <span data-ttu-id="274bf-175">Data utworzenia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="274bf-175">The date the subscription was created.</span></span> |
| <span data-ttu-id="274bf-176">effectiveStartDate</span><span class="sxs-lookup"><span data-stu-id="274bf-176">effectiveStartDate</span></span> | <span data-ttu-id="274bf-177">ciąg w formacie daty i czasu UTC</span><span class="sxs-lookup"><span data-stu-id="274bf-177">string in UTC date time format</span></span> | <span data-ttu-id="274bf-178">Data rozpoczęcia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="274bf-178">The date the subscription starts.</span></span> |
| <span data-ttu-id="274bf-179">commitmentEndDate</span><span class="sxs-lookup"><span data-stu-id="274bf-179">commitmentEndDate</span></span> | <span data-ttu-id="274bf-180">ciąg w formacie daty i czasu UTC</span><span class="sxs-lookup"><span data-stu-id="274bf-180">string in UTC date time format</span></span> | <span data-ttu-id="274bf-181">Data zakończenia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="274bf-181">The date the subscription ends.</span></span> |
| <span data-ttu-id="274bf-182">currentStateEndDate</span><span class="sxs-lookup"><span data-stu-id="274bf-182">currentStateEndDate</span></span> | <span data-ttu-id="274bf-183">ciąg w formacie daty i czasu UTC</span><span class="sxs-lookup"><span data-stu-id="274bf-183">string in UTC date time format</span></span> | <span data-ttu-id="274bf-184">Data zmiany bieżącego stanu subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="274bf-184">The date that the current status of the subscription will change.</span></span> |
| <span data-ttu-id="274bf-185">trialToPaidConversionDate</span><span class="sxs-lookup"><span data-stu-id="274bf-185">trialToPaidConversionDate</span></span> | <span data-ttu-id="274bf-186">ciąg w formacie daty i czasu UTC</span><span class="sxs-lookup"><span data-stu-id="274bf-186">string in UTC date time format</span></span> | <span data-ttu-id="274bf-187">Data konwersji subskrypcji z wersji próbnej na płatną.</span><span class="sxs-lookup"><span data-stu-id="274bf-187">The date that the subscription converts from trial to paid.</span></span> <span data-ttu-id="274bf-188">Wartość domyślna to null.</span><span class="sxs-lookup"><span data-stu-id="274bf-188">The default value is null.</span></span> |
| <span data-ttu-id="274bf-189">trialStartDate</span><span class="sxs-lookup"><span data-stu-id="274bf-189">trialStartDate</span></span> | <span data-ttu-id="274bf-190">ciąg w formacie daty i czasu UTC</span><span class="sxs-lookup"><span data-stu-id="274bf-190">string in UTC date time format</span></span> | <span data-ttu-id="274bf-191">Data rozpoczęcia okresu próbnego subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="274bf-191">The date that the trial period for the subscription started.</span></span> <span data-ttu-id="274bf-192">Wartość domyślna to null.</span><span class="sxs-lookup"><span data-stu-id="274bf-192">The default value is null.</span></span> |
| <span data-ttu-id="274bf-193">lastUsageDate</span><span class="sxs-lookup"><span data-stu-id="274bf-193">lastUsageDate</span></span> | <span data-ttu-id="274bf-194">ciąg w formacie daty i czasu UTC</span><span class="sxs-lookup"><span data-stu-id="274bf-194">string in UTC date time format</span></span> | <span data-ttu-id="274bf-195">Data ostatniego użytej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="274bf-195">The date that the subscription was last used.</span></span> <span data-ttu-id="274bf-196">Wartość domyślna to null.</span><span class="sxs-lookup"><span data-stu-id="274bf-196">The default value is null.</span></span> |
| <span data-ttu-id="274bf-197">deprovisionedDate</span><span class="sxs-lookup"><span data-stu-id="274bf-197">deprovisionedDate</span></span> | <span data-ttu-id="274bf-198">ciąg w formacie daty i czasu UTC</span><span class="sxs-lookup"><span data-stu-id="274bf-198">string in UTC date time format</span></span> | <span data-ttu-id="274bf-199">Data coprowizowana subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="274bf-199">The date that the subscription was deprovisioned.</span></span> <span data-ttu-id="274bf-200">Wartość domyślna to null.</span><span class="sxs-lookup"><span data-stu-id="274bf-200">The default value is null.</span></span> |
| <span data-ttu-id="274bf-201">lastRenewalDate</span><span class="sxs-lookup"><span data-stu-id="274bf-201">lastRenewalDate</span></span> | <span data-ttu-id="274bf-202">ciąg w formacie daty i godzin UTC</span><span class="sxs-lookup"><span data-stu-id="274bf-202">string in UTC date time format</span></span> | <span data-ttu-id="274bf-203">Data ostatniego odnowienia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="274bf-203">The date that the subscription was last renewed.</span></span> <span data-ttu-id="274bf-204">Wartość domyślna to null.</span><span class="sxs-lookup"><span data-stu-id="274bf-204">The default value is null.</span></span> |

### <a name="filter-fields"></a><span data-ttu-id="274bf-205">Filtrowanie pól</span><span class="sxs-lookup"><span data-stu-id="274bf-205">Filter fields</span></span>

<span data-ttu-id="274bf-206">W poniższej tabeli wymieniono opcjonalne pola filtru i ich opisy:</span><span class="sxs-lookup"><span data-stu-id="274bf-206">The following table lists optional filter fields and their descriptions:</span></span>

| <span data-ttu-id="274bf-207">Pole</span><span class="sxs-lookup"><span data-stu-id="274bf-207">Field</span></span> | <span data-ttu-id="274bf-208">Typ</span><span class="sxs-lookup"><span data-stu-id="274bf-208">Type</span></span> |  <span data-ttu-id="274bf-209">Opis</span><span class="sxs-lookup"><span data-stu-id="274bf-209">Description</span></span> |
|-------|------|--------------|
| <span data-ttu-id="274bf-210">top (pierwsze)</span><span class="sxs-lookup"><span data-stu-id="274bf-210">top</span></span> | <span data-ttu-id="274bf-211">int</span><span class="sxs-lookup"><span data-stu-id="274bf-211">int</span></span> | <span data-ttu-id="274bf-212">Liczba wierszy danych do zwrócenia w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="274bf-212">The number of rows of data to return in the request.</span></span> <span data-ttu-id="274bf-213">Jeśli wartość nie zostanie określona, wartość maksymalna i wartość domyślna to 10000.</span><span class="sxs-lookup"><span data-stu-id="274bf-213">If the value isn't specified, the maximum value and the default value are 10000.</span></span> <span data-ttu-id="274bf-214">Jeśli w zapytaniu znajduje się więcej wierszy, treść odpowiedzi zawiera następny link, za pomocą których można zażądać następnej strony danych.</span><span class="sxs-lookup"><span data-stu-id="274bf-214">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> |
| <span data-ttu-id="274bf-215">Pomiń</span><span class="sxs-lookup"><span data-stu-id="274bf-215">skip</span></span> | <span data-ttu-id="274bf-216">int</span><span class="sxs-lookup"><span data-stu-id="274bf-216">int</span></span> | <span data-ttu-id="274bf-217">Liczba wierszy do pominięcia w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="274bf-217">The number of rows to skip in the query.</span></span> <span data-ttu-id="274bf-218">Ten parametr umożliwia stronicować duże zestawy danych.</span><span class="sxs-lookup"><span data-stu-id="274bf-218">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="274bf-219">Na przykład wartości top=10000 i skip=0 pobierają pierwsze 10000 wierszy danych, top=10000, a skip=10000 pobiera następne 10000 wierszy danych.</span><span class="sxs-lookup"><span data-stu-id="274bf-219">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data.</span></span> |
| <span data-ttu-id="274bf-220">filter</span><span class="sxs-lookup"><span data-stu-id="274bf-220">filter</span></span> | <span data-ttu-id="274bf-221">ciąg</span><span class="sxs-lookup"><span data-stu-id="274bf-221">string</span></span> | <span data-ttu-id="274bf-222">Co najmniej jedna instrukcja, która filtruje wiersze w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="274bf-222">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="274bf-223">Każda instrukcja filtru zawiera nazwę pola z treści odpowiedzi i wartość skojarzoną z operatorem **`eq`** , lub dla niektórych **`ne`** **`contains`** pól.</span><span class="sxs-lookup"><span data-stu-id="274bf-223">Each filter statement contains a field name from the response body and a value that are associated with the **`eq`**, **`ne`**, or for certain fields, the **`contains`** operator.</span></span> <span data-ttu-id="274bf-224">Instrukcje można łączyć przy użyciu **`and`** instrukcji lub **`or`** .</span><span class="sxs-lookup"><span data-stu-id="274bf-224">Statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="274bf-225">Wartości ciągu muszą być otoczone pojedynczymi cudzysłowami w parametrze filtru.</span><span class="sxs-lookup"><span data-stu-id="274bf-225">String values must be surrounded by single quotes in the filter parameter.</span></span> <span data-ttu-id="274bf-226">W poniższej sekcji znajduje się lista pól, które można filtrować, oraz operatorów obsługiwanych przez te pola.</span><span class="sxs-lookup"><span data-stu-id="274bf-226">See the following section for a list of fields that can be filtered and the operators that are supported with those fields.</span></span> |
| <span data-ttu-id="274bf-227">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="274bf-227">aggregationLevel</span></span> | <span data-ttu-id="274bf-228">ciąg</span><span class="sxs-lookup"><span data-stu-id="274bf-228">string</span></span> | <span data-ttu-id="274bf-229">Określa zakres czasu, dla którego mają zostać pobrane zagregowane dane.</span><span class="sxs-lookup"><span data-stu-id="274bf-229">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="274bf-230">Może być jednym z następujących ciągów: **dzień,** **tydzień** lub **miesiąc**.</span><span class="sxs-lookup"><span data-stu-id="274bf-230">Can be one of the following strings: **day**, **week**, or **month**.</span></span> <span data-ttu-id="274bf-231">Jeśli wartość nie zostanie określona, wartość domyślna to **dateRange**.</span><span class="sxs-lookup"><span data-stu-id="274bf-231">If the value isn't specified, the default is **dateRange**.</span></span> <span data-ttu-id="274bf-232">**Uwaga:** ten parametr ma zastosowanie tylko wtedy, gdy pole daty jest przekazywane jako część parametru groupBy.</span><span class="sxs-lookup"><span data-stu-id="274bf-232">**Note**: This parameter applies only when a date field is passed as part of the groupBy parameter.</span></span> |
| <span data-ttu-id="274bf-233">Groupby</span><span class="sxs-lookup"><span data-stu-id="274bf-233">groupBy</span></span> | <span data-ttu-id="274bf-234">ciąg</span><span class="sxs-lookup"><span data-stu-id="274bf-234">string</span></span> | <span data-ttu-id="274bf-235">Instrukcja, która stosuje agregację danych tylko do określonych pól.</span><span class="sxs-lookup"><span data-stu-id="274bf-235">A statement that applies data aggregation only to the specified fields.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="274bf-236">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="274bf-236">Request headers</span></span>

<span data-ttu-id="274bf-237">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="274bf-237">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="274bf-238">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="274bf-238">Request body</span></span>

<span data-ttu-id="274bf-239">Brak.</span><span class="sxs-lookup"><span data-stu-id="274bf-239">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="274bf-240">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="274bf-240">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="274bf-241">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="274bf-241">REST response</span></span>

<span data-ttu-id="274bf-242">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [subskrypcji](partner-center-analytics-resources.md#subscription-resource) pogrupowanych według określonych warunków i dat.</span><span class="sxs-lookup"><span data-stu-id="274bf-242">If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription-resource) resources grouped by the specified terms and dates.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="274bf-243">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="274bf-243">Response success and error codes</span></span>

<span data-ttu-id="274bf-244">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="274bf-244">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="274bf-245">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="274bf-245">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="274bf-246">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="274bf-246">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="274bf-247">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="274bf-247">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="274bf-248">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="274bf-248">See also</span></span>

[<span data-ttu-id="274bf-249">Analiza Centrum partnerskiego — zasoby</span><span class="sxs-lookup"><span data-stu-id="274bf-249">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
