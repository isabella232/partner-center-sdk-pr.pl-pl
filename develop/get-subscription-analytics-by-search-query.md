---
title: Uzyskiwanie analizy subskrypcji według zapytania wyszukiwania
description: Sposób filtrowania informacji analizy subskrypcji według zapytania wyszukiwania.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8df777b9a88206f8b22579f0f445c54d80f7cd64
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548740"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a><span data-ttu-id="7c8eb-103">Pobieranie informacji analitycznych dotyczących subskrypcji filtrowanych wg zapytania wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="7c8eb-103">Get subscription analytics information filtered by a search query</span></span>

<span data-ttu-id="7c8eb-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="7c8eb-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7c8eb-105">Jak uzyskać informacje analityczne dotyczące subskrypcji dla klientów przefiltrowane według zapytania wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-105">How to get subscription analytics information for your customers filtered by a search query.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c8eb-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7c8eb-106">Prerequisites</span></span>

- <span data-ttu-id="7c8eb-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="7c8eb-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7c8eb-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="7c8eb-109">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="7c8eb-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7c8eb-110">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="7c8eb-110">Request syntax</span></span>

| <span data-ttu-id="7c8eb-111">Metoda</span><span class="sxs-lookup"><span data-stu-id="7c8eb-111">Method</span></span> | <span data-ttu-id="7c8eb-112">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="7c8eb-112">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="7c8eb-113">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="7c8eb-113">**GET**</span></span> | <span data-ttu-id="7c8eb-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?filter={filter_string}</span><span class="sxs-lookup"><span data-stu-id="7c8eb-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?filter={filter_string}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="7c8eb-115">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="7c8eb-115">URI parameters</span></span>

<span data-ttu-id="7c8eb-116">Użyj następującego parametru wymaganej ścieżki, aby zidentyfikować organizację i odfiltrować wyszukiwanie.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-116">Use the following required path parameter to identify your organization and filter the search.</span></span>

| <span data-ttu-id="7c8eb-117">Nazwa</span><span class="sxs-lookup"><span data-stu-id="7c8eb-117">Name</span></span> | <span data-ttu-id="7c8eb-118">Typ</span><span class="sxs-lookup"><span data-stu-id="7c8eb-118">Type</span></span> | <span data-ttu-id="7c8eb-119">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7c8eb-119">Required</span></span> | <span data-ttu-id="7c8eb-120">Opis</span><span class="sxs-lookup"><span data-stu-id="7c8eb-120">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="7c8eb-121">filter_string</span><span class="sxs-lookup"><span data-stu-id="7c8eb-121">filter_string</span></span> | <span data-ttu-id="7c8eb-122">ciąg</span><span class="sxs-lookup"><span data-stu-id="7c8eb-122">string</span></span> | <span data-ttu-id="7c8eb-123">Tak</span><span class="sxs-lookup"><span data-stu-id="7c8eb-123">Yes</span></span> | <span data-ttu-id="7c8eb-124">Filtr do zastosowania do analizy subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-124">The filter to apply to the subscription analytics.</span></span> <span data-ttu-id="7c8eb-125">Zobacz sekcje Składnia filtru i Pola filtru, aby uzyskać informacje o składni, polach i operatorach do użycia w tym parametrze.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-125">See the Filter syntax and Filter fields sections for the syntax, fields, and operators to use in this parameter.</span></span> |

### <a name="filter-syntax"></a><span data-ttu-id="7c8eb-126">Składnia filtru</span><span class="sxs-lookup"><span data-stu-id="7c8eb-126">Filter syntax</span></span>

<span data-ttu-id="7c8eb-127">Parametr filtru musi składać się z serii kombinacji pól, wartości i operatorów.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-127">The filter parameter must be composed as a series of field, value, and operator combinations.</span></span> <span data-ttu-id="7c8eb-128">Wiele kombinacji można łączyć przy użyciu **`and`** operatorów **`or`** lub .</span><span class="sxs-lookup"><span data-stu-id="7c8eb-128">Multiple combinations can be combined using **`and`** or **`or`** operators.</span></span>

<span data-ttu-id="7c8eb-129">Niezakodowany przykład wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="7c8eb-129">An unencoded example looks like this:</span></span>

- <span data-ttu-id="7c8eb-130">Ciąg: `?filter=Field operator 'Value'`</span><span class="sxs-lookup"><span data-stu-id="7c8eb-130">String: `?filter=Field operator 'Value'`</span></span>
- <span data-ttu-id="7c8eb-131">Boolean: `?filter=Field operator Value`</span><span class="sxs-lookup"><span data-stu-id="7c8eb-131">Boolean: `?filter=Field operator Value`</span></span>
- <span data-ttu-id="7c8eb-132">Zawiera `?filter=contains(field,'value')`</span><span class="sxs-lookup"><span data-stu-id="7c8eb-132">Contains `?filter=contains(field,'value')`</span></span>

### <a name="filter-fields"></a><span data-ttu-id="7c8eb-133">Filtrowanie pól</span><span class="sxs-lookup"><span data-stu-id="7c8eb-133">Filter fields</span></span>

<span data-ttu-id="7c8eb-134">Parametr filtru żądania zawiera co najmniej jedną instrukcje, które filtruje wiersze w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-134">The filter parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="7c8eb-135">Każda instrukcja zawiera pole i wartość, które są skojarzone z operatorami **`eq`** **`ne`** lub .</span><span class="sxs-lookup"><span data-stu-id="7c8eb-135">Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators.</span></span> <span data-ttu-id="7c8eb-136">Niektóre pola obsługują również **`contains`** operatory **`gt`** , , , **`lt`** i **`ge`** **`le`** .</span><span class="sxs-lookup"><span data-stu-id="7c8eb-136">Some fields also support the **`contains`**, **`gt`**, **`lt`**, **`ge`**, and **`le`** operators.</span></span> <span data-ttu-id="7c8eb-137">Instrukcje można łączyć przy użyciu **`and`** operatorów **`or`** lub .</span><span class="sxs-lookup"><span data-stu-id="7c8eb-137">Statements can be combined using **`and`** or **`or`** operators.</span></span>

<span data-ttu-id="7c8eb-138">Poniżej przedstawiono przykłady ciągów filtrów:</span><span class="sxs-lookup"><span data-stu-id="7c8eb-138">The following are examples of filter strings:</span></span>

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

<span data-ttu-id="7c8eb-139">W poniższej tabeli przedstawiono listę obsługiwanych pól i operatorów obsługi dla parametru filtru.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-139">The following table shows a list of the supported fields and support operators for the filter parameter.</span></span> <span data-ttu-id="7c8eb-140">Wartości ciągu muszą być otoczone pojedynczymi cudzysłowami.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-140">String values must be surrounded by single quotes.</span></span>

| <span data-ttu-id="7c8eb-141">Parametr</span><span class="sxs-lookup"><span data-stu-id="7c8eb-141">Parameter</span></span> | <span data-ttu-id="7c8eb-142">Obsługiwane operatory</span><span class="sxs-lookup"><span data-stu-id="7c8eb-142">Supported operators</span></span> | <span data-ttu-id="7c8eb-143">Opis</span><span class="sxs-lookup"><span data-stu-id="7c8eb-143">Description</span></span> |
|-----------|---------------------|-------------|
| <span data-ttu-id="7c8eb-144">autoRenewEnabled</span><span class="sxs-lookup"><span data-stu-id="7c8eb-144">autoRenewEnabled</span></span> | <span data-ttu-id="7c8eb-145">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="7c8eb-145">`eq`, `ne`</span></span> | <span data-ttu-id="7c8eb-146">Wartość wskazująca, czy subskrypcja jest odnawiana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-146">A value indicating whether the subscription is renewed automatically.</span></span> |
| <span data-ttu-id="7c8eb-147">commitmentEndDate</span><span class="sxs-lookup"><span data-stu-id="7c8eb-147">commitmentEndDate</span></span> | <span data-ttu-id="7c8eb-148">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="7c8eb-148">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="7c8eb-149">Data zakończenia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-149">The date the subscription ends.</span></span> |
| <span data-ttu-id="7c8eb-150">Creationdate</span><span class="sxs-lookup"><span data-stu-id="7c8eb-150">creationDate</span></span> | <span data-ttu-id="7c8eb-151">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="7c8eb-151">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="7c8eb-152">Data utworzenia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-152">The date the subscription was created.</span></span> |
| <span data-ttu-id="7c8eb-153">currentStateEndDate</span><span class="sxs-lookup"><span data-stu-id="7c8eb-153">currentStateEndDate</span></span> | <span data-ttu-id="7c8eb-154">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="7c8eb-154">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="7c8eb-155">Data zmiany bieżącego stanu subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-155">The date that the current status of the subscription will change.</span></span> |
| <span data-ttu-id="7c8eb-156">customerMarket</span><span class="sxs-lookup"><span data-stu-id="7c8eb-156">customerMarket</span></span> | <span data-ttu-id="7c8eb-157">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="7c8eb-157">`eq`, `ne`</span></span> | <span data-ttu-id="7c8eb-158">Kraj/region, w którym klient działa.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-158">The country/region that the customer does business in.</span></span> |
| <span data-ttu-id="7c8eb-159">Customername</span><span class="sxs-lookup"><span data-stu-id="7c8eb-159">customerName</span></span> | `contains` | <span data-ttu-id="7c8eb-160">Nazwa klienta.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-160">The name of the customer.</span></span> |
| <span data-ttu-id="7c8eb-161">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="7c8eb-161">customerTenantId</span></span> | <span data-ttu-id="7c8eb-162">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="7c8eb-162">`eq`, `ne`</span></span> | <span data-ttu-id="7c8eb-163">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje dzierżawę klienta.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-163">A GUID-formatted string that identifies the customer tenant.</span></span> |
| <span data-ttu-id="7c8eb-164">deprovisionedDate</span><span class="sxs-lookup"><span data-stu-id="7c8eb-164">deprovisionedDate</span></span> | <span data-ttu-id="7c8eb-165">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="7c8eb-165">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="7c8eb-166">Data coprowizowana subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-166">The date that the subscription was deprovisioned.</span></span> <span data-ttu-id="7c8eb-167">Wartość domyślna to null.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-167">The default value is null.</span></span> |
| <span data-ttu-id="7c8eb-168">effectiveStartDate</span><span class="sxs-lookup"><span data-stu-id="7c8eb-168">effectiveStartDate</span></span> | <span data-ttu-id="7c8eb-169">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="7c8eb-169">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="7c8eb-170">Data rozpoczęcia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-170">The date the subscription starts.</span></span> |
| <span data-ttu-id="7c8eb-171">Friendlyname</span><span class="sxs-lookup"><span data-stu-id="7c8eb-171">friendlyName</span></span> | `contains` | <span data-ttu-id="7c8eb-172">Nazwa subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-172">The name of the subscription.</span></span> |
| <span data-ttu-id="7c8eb-173">identyfikator</span><span class="sxs-lookup"><span data-stu-id="7c8eb-173">id</span></span> | <span data-ttu-id="7c8eb-174">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="7c8eb-174">`eq`, `ne`</span></span> | <span data-ttu-id="7c8eb-175">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-175">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="7c8eb-176">lastRenewalDate</span><span class="sxs-lookup"><span data-stu-id="7c8eb-176">lastRenewalDate</span></span> | <span data-ttu-id="7c8eb-177">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="7c8eb-177">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="7c8eb-178">Data ostatniego odnowienia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-178">The date that the subscription was last renewed.</span></span> <span data-ttu-id="7c8eb-179">Wartość domyślna to null.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-179">The default value is null.</span></span> |
| <span data-ttu-id="7c8eb-180">lastUsageDate</span><span class="sxs-lookup"><span data-stu-id="7c8eb-180">lastUsageDate</span></span> | <span data-ttu-id="7c8eb-181">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="7c8eb-181">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="7c8eb-182">Data ostatniego użytej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-182">The date that the subscription was last used.</span></span> <span data-ttu-id="7c8eb-183">Wartość domyślna to null.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-183">The default value is null.</span></span> |
| <span data-ttu-id="7c8eb-184">partnerId</span><span class="sxs-lookup"><span data-stu-id="7c8eb-184">partnerId</span></span> | <span data-ttu-id="7c8eb-185">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="7c8eb-185">`eq`, `ne`</span></span> | <span data-ttu-id="7c8eb-186">Identyfikator MPN.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-186">The MPN ID.</span></span> <span data-ttu-id="7c8eb-187">W przypadku odsprzedawcy bezpośredniego ta wartość będzie identyfikatorem MPN partnera.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-187">For a direct reseller, this value will be the MPN ID of the partner.</span></span> <span data-ttu-id="7c8eb-188">W przypadku odsprzedawcy pośredniego ta wartość będzie identyfikatorem MPN odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-188">For an indirect reseller, this value will be the MPN ID of the indirect reseller.</span></span> |
| <span data-ttu-id="7c8eb-189">partnerName</span><span class="sxs-lookup"><span data-stu-id="7c8eb-189">partnerName</span></span> | <span data-ttu-id="7c8eb-190">ciąg</span><span class="sxs-lookup"><span data-stu-id="7c8eb-190">string</span></span> | <span data-ttu-id="7c8eb-191">Nazwa partnera, dla którego zakupiono subskrypcję</span><span class="sxs-lookup"><span data-stu-id="7c8eb-191">Name of the partner for whom the subscription was purchased</span></span> |
| <span data-ttu-id="7c8eb-192">Productname</span><span class="sxs-lookup"><span data-stu-id="7c8eb-192">productName</span></span> | <span data-ttu-id="7c8eb-193">`contains`, `eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="7c8eb-193">`contains`, `eq`, `ne`</span></span> | <span data-ttu-id="7c8eb-194">Nazwa produktu.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-194">The name of the product.</span></span> |
| <span data-ttu-id="7c8eb-195">Providername</span><span class="sxs-lookup"><span data-stu-id="7c8eb-195">providerName</span></span> | <span data-ttu-id="7c8eb-196">ciąg</span><span class="sxs-lookup"><span data-stu-id="7c8eb-196">string</span></span> | <span data-ttu-id="7c8eb-197">Gdy transakcja subskrypcji jest dla odsprzedawcy pośredniego, nazwa dostawcy jest dostawcą pośrednim, który kupił subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-197">When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.</span></span>|
| <span data-ttu-id="7c8eb-198">status</span><span class="sxs-lookup"><span data-stu-id="7c8eb-198">status</span></span> | <span data-ttu-id="7c8eb-199">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="7c8eb-199">`eq`, `ne`</span></span> | <span data-ttu-id="7c8eb-200">Stan subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-200">The subscription status.</span></span> <span data-ttu-id="7c8eb-201">Obsługiwane wartości to: "ACTIVE", "SUSPENDED" lub "DEPROVISIONED".</span><span class="sxs-lookup"><span data-stu-id="7c8eb-201">Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".</span></span> |
| <span data-ttu-id="7c8eb-202">Subscriptiontype</span><span class="sxs-lookup"><span data-stu-id="7c8eb-202">subscriptionType</span></span> | <span data-ttu-id="7c8eb-203">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="7c8eb-203">`eq`, `ne`</span></span> | <span data-ttu-id="7c8eb-204">Typ subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-204">The subscription type.</span></span> <span data-ttu-id="7c8eb-205">**Uwaga:** w tym polu jest zróżnicowa wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-205">**Note**: This field is case-sensitive.</span></span> <span data-ttu-id="7c8eb-206">Obsługiwane wartości to: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span><span class="sxs-lookup"><span data-stu-id="7c8eb-206">Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span></span> |
| <span data-ttu-id="7c8eb-207">trialStartDate</span><span class="sxs-lookup"><span data-stu-id="7c8eb-207">trialStartDate</span></span> | <span data-ttu-id="7c8eb-208">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="7c8eb-208">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="7c8eb-209">Data rozpoczęcia okresu próbnego subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-209">The date that the trial period for the subscription started.</span></span> <span data-ttu-id="7c8eb-210">Wartość domyślna to null.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-210">The default value is null.</span></span> |
| <span data-ttu-id="7c8eb-211">trialToPaidConversionDate</span><span class="sxs-lookup"><span data-stu-id="7c8eb-211">trialToPaidConversionDate</span></span> | <span data-ttu-id="7c8eb-212">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="7c8eb-212">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="7c8eb-213">Data konwersji subskrypcji z wersji próbnej na płatną.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-213">The date that the subscription converts from trial to paid.</span></span> <span data-ttu-id="7c8eb-214">Wartość domyślna to null.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-214">The default value is null.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7c8eb-215">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="7c8eb-215">Request headers</span></span>

<span data-ttu-id="7c8eb-216">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="7c8eb-216">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7c8eb-217">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="7c8eb-217">Request body</span></span>

<span data-ttu-id="7c8eb-218">Brak.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-218">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7c8eb-219">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="7c8eb-219">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="7c8eb-220">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="7c8eb-220">REST response</span></span>

<span data-ttu-id="7c8eb-221">W przypadku powodzenia treść odpowiedzi zawiera kolekcję zasobów [subskrypcji](partner-center-analytics-resources.md#subscription-resource) spełniających kryteria filtrowania.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-221">If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription-resource) resources that meet the filter criteria.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7c8eb-222">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7c8eb-222">Response success and error codes</span></span>

<span data-ttu-id="7c8eb-223">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-223">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7c8eb-224">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="7c8eb-224">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7c8eb-225">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7c8eb-225">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7c8eb-226">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7c8eb-226">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123

{
    "customerTenantId": "735920EB-A564-4C72-9FE5-52632562712C",
    "customerName": "SURFACE TEST2",
    "customerMarket": "US",
    "id": "B76412DA-D382-4688-A6A4-711A207C1C2E",
    "status": "ACTIVE",
    "productName": "UNKNOWN",
    "subscriptionType": "Azure",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "MICROSOFT AZURE",
    "creationDate": "2017-06-02T23:11:58.747",
    "effectiveStartDate": "2017-06-02T00:00:00",
    "commitmentEndDate": null,
    "currentStateEndDate": null,
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": null,
    "licenseCount": 0
}
```

## <a name="see-also"></a><span data-ttu-id="7c8eb-227">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="7c8eb-227">See also</span></span>

- [<span data-ttu-id="7c8eb-228">Analiza Centrum partnerskiego — zasoby</span><span class="sxs-lookup"><span data-stu-id="7c8eb-228">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
