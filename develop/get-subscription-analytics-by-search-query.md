---
title: Pobierz usługę Subscription Analytics według zapytania wyszukiwania
description: Jak uzyskać informacje o analizie subskrypcji odfiltrowane według zapytania wyszukiwania.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1046ea3c7e813eedae4890eebf6356337c80ede
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767910"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a><span data-ttu-id="b8ee7-103">Pobieranie informacji analitycznych dotyczących subskrypcji filtrowanych wg zapytania wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="b8ee7-103">Get subscription analytics information filtered by a search query</span></span>

<span data-ttu-id="b8ee7-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="b8ee7-104">**Applies To**</span></span>

- <span data-ttu-id="b8ee7-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="b8ee7-105">Partner Center</span></span>
- <span data-ttu-id="b8ee7-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="b8ee7-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="b8ee7-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="b8ee7-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="b8ee7-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b8ee7-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b8ee7-109">Jak uzyskać informacje o analizie subskrypcji dla klientów odfiltrowanych według zapytania wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-109">How to get subscription analytics information for your customers filtered by a search query.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8ee7-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b8ee7-110">Prerequisites</span></span>

- <span data-ttu-id="b8ee7-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b8ee7-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b8ee7-112">Ten scenariusz obsługuje tylko uwierzytelnianie z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="b8ee7-113">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="b8ee7-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b8ee7-114">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="b8ee7-114">Request syntax</span></span>

| <span data-ttu-id="b8ee7-115">Metoda</span><span class="sxs-lookup"><span data-stu-id="b8ee7-115">Method</span></span> | <span data-ttu-id="b8ee7-116">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="b8ee7-116">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="b8ee7-117">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="b8ee7-117">**GET**</span></span> | <span data-ttu-id="b8ee7-118">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/V1/Analytics/subscriptions? Filter = {filter_string}</span><span class="sxs-lookup"><span data-stu-id="b8ee7-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?filter={filter_string}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="b8ee7-119">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="b8ee7-119">URI parameters</span></span>

<span data-ttu-id="b8ee7-120">Użyj poniższego wymaganego parametru Path, aby zidentyfikować organizację i przefiltrować wyszukiwanie.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-120">Use the following required path parameter to identify your organization and filter the search.</span></span>

| <span data-ttu-id="b8ee7-121">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b8ee7-121">Name</span></span> | <span data-ttu-id="b8ee7-122">Typ</span><span class="sxs-lookup"><span data-stu-id="b8ee7-122">Type</span></span> | <span data-ttu-id="b8ee7-123">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b8ee7-123">Required</span></span> | <span data-ttu-id="b8ee7-124">Opis</span><span class="sxs-lookup"><span data-stu-id="b8ee7-124">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="b8ee7-125">filter_string</span><span class="sxs-lookup"><span data-stu-id="b8ee7-125">filter_string</span></span> | <span data-ttu-id="b8ee7-126">ciąg</span><span class="sxs-lookup"><span data-stu-id="b8ee7-126">string</span></span> | <span data-ttu-id="b8ee7-127">Tak</span><span class="sxs-lookup"><span data-stu-id="b8ee7-127">Yes</span></span> | <span data-ttu-id="b8ee7-128">Filtr, który ma zostać zastosowany do analizy subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-128">The filter to apply to the subscription analytics.</span></span> <span data-ttu-id="b8ee7-129">Zobacz sekcję składnia filtrów i pola filtru, aby poznać składnię, pola i operatory, które mają być używane w tym parametrze.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-129">See the Filter syntax and Filter fields sections for the syntax, fields, and operators to use in this parameter.</span></span> |

### <a name="filter-syntax"></a><span data-ttu-id="b8ee7-130">Składnia filtru</span><span class="sxs-lookup"><span data-stu-id="b8ee7-130">Filter syntax</span></span>

<span data-ttu-id="b8ee7-131">Parametr Filter musi składać się z szeregu kombinacji pól, wartości i operatora.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-131">The filter parameter must be composed as a series of field, value, and operator combinations.</span></span> <span data-ttu-id="b8ee7-132">Wiele kombinacji można łączyć za pomocą **`and`** **`or`** operatora OR.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-132">Multiple combinations can be combined using **`and`** or **`or`** operators.</span></span>

<span data-ttu-id="b8ee7-133">Niezakodowany przykład wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="b8ee7-133">An unencoded example looks like this:</span></span>

- <span data-ttu-id="b8ee7-134">Parametry `?filter=Field operator 'Value'`</span><span class="sxs-lookup"><span data-stu-id="b8ee7-134">String: `?filter=Field operator 'Value'`</span></span>
- <span data-ttu-id="b8ee7-135">Typu `?filter=Field operator Value`</span><span class="sxs-lookup"><span data-stu-id="b8ee7-135">Boolean: `?filter=Field operator Value`</span></span>
- <span data-ttu-id="b8ee7-136">Wyświetlana `?filter=contains(field,'value')`</span><span class="sxs-lookup"><span data-stu-id="b8ee7-136">Contains `?filter=contains(field,'value')`</span></span>

### <a name="filter-fields"></a><span data-ttu-id="b8ee7-137">Pola filtru</span><span class="sxs-lookup"><span data-stu-id="b8ee7-137">Filter fields</span></span>

<span data-ttu-id="b8ee7-138">Parametr Filter żądania zawiera jedną lub więcej instrukcji, które filtrują wiersze w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-138">The filter parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="b8ee7-139">Każda instrukcja zawiera pole i wartość, które są skojarzone z **`eq`** **`ne`** operatorami or.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-139">Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators.</span></span> <span data-ttu-id="b8ee7-140">Niektóre pola obsługują również **`contains`** operatory, **`gt`** , **`lt`** , **`ge`** i **`le`** .</span><span class="sxs-lookup"><span data-stu-id="b8ee7-140">Some fields also support the **`contains`**, **`gt`**, **`lt`**, **`ge`**, and **`le`** operators.</span></span> <span data-ttu-id="b8ee7-141">Instrukcje można łączyć przy użyciu **`and`** **`or`** operatorów or.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-141">Statements can be combined using **`and`** or **`or`** operators.</span></span>

<span data-ttu-id="b8ee7-142">Poniżej przedstawiono przykłady ciągów filtrów:</span><span class="sxs-lookup"><span data-stu-id="b8ee7-142">The following are examples of filter strings:</span></span>

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

<span data-ttu-id="b8ee7-143">W poniższej tabeli przedstawiono listę obsługiwanych pól i operatorów pomocy technicznej dla parametru Filter.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-143">The following table shows a list of the supported fields and support operators for the filter parameter.</span></span> <span data-ttu-id="b8ee7-144">Wartości ciągu muszą być ujęte w pojedyncze cudzysłowy.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-144">String values must be surrounded by single quotes.</span></span>

| <span data-ttu-id="b8ee7-145">Parametr</span><span class="sxs-lookup"><span data-stu-id="b8ee7-145">Parameter</span></span> | <span data-ttu-id="b8ee7-146">Obsługiwane operatory</span><span class="sxs-lookup"><span data-stu-id="b8ee7-146">Supported operators</span></span> | <span data-ttu-id="b8ee7-147">Opis</span><span class="sxs-lookup"><span data-stu-id="b8ee7-147">Description</span></span> |
|-----------|---------------------|-------------|
| <span data-ttu-id="b8ee7-148">autoRenewEnabled</span><span class="sxs-lookup"><span data-stu-id="b8ee7-148">autoRenewEnabled</span></span> | <span data-ttu-id="b8ee7-149">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="b8ee7-149">`eq`, `ne`</span></span> | <span data-ttu-id="b8ee7-150">Wartość wskazująca, czy subskrypcja jest odnawiana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-150">A value indicating whether the subscription is renewed automatically.</span></span> |
| <span data-ttu-id="b8ee7-151">commitmentEndDate</span><span class="sxs-lookup"><span data-stu-id="b8ee7-151">commitmentEndDate</span></span> | <span data-ttu-id="b8ee7-152">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="b8ee7-152">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="b8ee7-153">Data zakończenia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-153">The date the subscription ends.</span></span> |
| <span data-ttu-id="b8ee7-154">creationDate</span><span class="sxs-lookup"><span data-stu-id="b8ee7-154">creationDate</span></span> | <span data-ttu-id="b8ee7-155">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="b8ee7-155">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="b8ee7-156">Data utworzenia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-156">The date the subscription was created.</span></span> |
| <span data-ttu-id="b8ee7-157">currentStateEndDate</span><span class="sxs-lookup"><span data-stu-id="b8ee7-157">currentStateEndDate</span></span> | <span data-ttu-id="b8ee7-158">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="b8ee7-158">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="b8ee7-159">Data zmiany bieżącego stanu subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-159">The date that the current status of the subscription will change.</span></span> |
| <span data-ttu-id="b8ee7-160">customerMarket</span><span class="sxs-lookup"><span data-stu-id="b8ee7-160">customerMarket</span></span> | <span data-ttu-id="b8ee7-161">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="b8ee7-161">`eq`, `ne`</span></span> | <span data-ttu-id="b8ee7-162">Kraj/region, w którym klient wykonuje działalność.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-162">The country/region that the customer does business in.</span></span> |
| <span data-ttu-id="b8ee7-163">customerName</span><span class="sxs-lookup"><span data-stu-id="b8ee7-163">customerName</span></span> | `contains` | <span data-ttu-id="b8ee7-164">Nazwa klienta.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-164">The name of the customer.</span></span> |
| <span data-ttu-id="b8ee7-165">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="b8ee7-165">customerTenantId</span></span> | <span data-ttu-id="b8ee7-166">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="b8ee7-166">`eq`, `ne`</span></span> | <span data-ttu-id="b8ee7-167">Ciąg sformatowany przy użyciu identyfikatora GUID, który identyfikuje dzierżawcę klienta.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-167">A GUID-formatted string that identifies the customer tenant.</span></span> |
| <span data-ttu-id="b8ee7-168">deprovisionedDate</span><span class="sxs-lookup"><span data-stu-id="b8ee7-168">deprovisionedDate</span></span> | <span data-ttu-id="b8ee7-169">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="b8ee7-169">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="b8ee7-170">Data anulowania aprowizacji subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-170">The date that the subscription was deprovisioned.</span></span> <span data-ttu-id="b8ee7-171">Wartość domyślna to null.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-171">The default value is null.</span></span> |
| <span data-ttu-id="b8ee7-172">effectiveStartDate</span><span class="sxs-lookup"><span data-stu-id="b8ee7-172">effectiveStartDate</span></span> | <span data-ttu-id="b8ee7-173">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="b8ee7-173">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="b8ee7-174">Data rozpoczęcia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-174">The date the subscription starts.</span></span> |
| <span data-ttu-id="b8ee7-175">friendlyName</span><span class="sxs-lookup"><span data-stu-id="b8ee7-175">friendlyName</span></span> | `contains` | <span data-ttu-id="b8ee7-176">Nazwa subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-176">The name of the subscription.</span></span> |
| <span data-ttu-id="b8ee7-177">identyfikator</span><span class="sxs-lookup"><span data-stu-id="b8ee7-177">id</span></span> | <span data-ttu-id="b8ee7-178">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="b8ee7-178">`eq`, `ne`</span></span> | <span data-ttu-id="b8ee7-179">Ciąg w formacie GUID, który identyfikuje subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-179">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="b8ee7-180">lastRenewalDate</span><span class="sxs-lookup"><span data-stu-id="b8ee7-180">lastRenewalDate</span></span> | <span data-ttu-id="b8ee7-181">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="b8ee7-181">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="b8ee7-182">Data ostatniego odnowienia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-182">The date that the subscription was last renewed.</span></span> <span data-ttu-id="b8ee7-183">Wartość domyślna to null.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-183">The default value is null.</span></span> |
| <span data-ttu-id="b8ee7-184">lastUsageDate</span><span class="sxs-lookup"><span data-stu-id="b8ee7-184">lastUsageDate</span></span> | <span data-ttu-id="b8ee7-185">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="b8ee7-185">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="b8ee7-186">Data ostatniego użycia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-186">The date that the subscription was last used.</span></span> <span data-ttu-id="b8ee7-187">Wartość domyślna to null.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-187">The default value is null.</span></span> |
| <span data-ttu-id="b8ee7-188">partnerId</span><span class="sxs-lookup"><span data-stu-id="b8ee7-188">partnerId</span></span> | <span data-ttu-id="b8ee7-189">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="b8ee7-189">`eq`, `ne`</span></span> | <span data-ttu-id="b8ee7-190">IDENTYFIKATOR MPN.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-190">The MPN ID.</span></span> <span data-ttu-id="b8ee7-191">W przypadku bezpośredniego odsprzedawcy ta wartość będzie MPN IDENTYFIKATORem partnera.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-191">For a direct reseller, this value will be the MPN ID of the partner.</span></span> <span data-ttu-id="b8ee7-192">W odniesieniu do pośredniego odsprzedawcy ta wartość będzie IDENTYFIKATORem MPN pośredniego odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-192">For an indirect reseller, this value will be the MPN ID of the indirect reseller.</span></span> |
| <span data-ttu-id="b8ee7-193">partnerName</span><span class="sxs-lookup"><span data-stu-id="b8ee7-193">partnerName</span></span> | <span data-ttu-id="b8ee7-194">ciąg</span><span class="sxs-lookup"><span data-stu-id="b8ee7-194">string</span></span> | <span data-ttu-id="b8ee7-195">Nazwa partnera, dla którego została zakupiona subskrypcja</span><span class="sxs-lookup"><span data-stu-id="b8ee7-195">Name of the partner for whom the subscription was purchased</span></span> |
| <span data-ttu-id="b8ee7-196">productName</span><span class="sxs-lookup"><span data-stu-id="b8ee7-196">productName</span></span> | <span data-ttu-id="b8ee7-197">`contains`, `eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="b8ee7-197">`contains`, `eq`, `ne`</span></span> | <span data-ttu-id="b8ee7-198">Nazwa produktu.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-198">The name of the product.</span></span> |
| <span data-ttu-id="b8ee7-199">providerName</span><span class="sxs-lookup"><span data-stu-id="b8ee7-199">providerName</span></span> | <span data-ttu-id="b8ee7-200">ciąg</span><span class="sxs-lookup"><span data-stu-id="b8ee7-200">string</span></span> | <span data-ttu-id="b8ee7-201">Gdy transakcja subskrypcyjna dotyczy pośredniego odsprzedawcy, nazwa dostawcy jest dostawcą pośrednim, który kupił subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-201">When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.</span></span>|
| <span data-ttu-id="b8ee7-202">status</span><span class="sxs-lookup"><span data-stu-id="b8ee7-202">status</span></span> | <span data-ttu-id="b8ee7-203">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="b8ee7-203">`eq`, `ne`</span></span> | <span data-ttu-id="b8ee7-204">Stan subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-204">The subscription status.</span></span> <span data-ttu-id="b8ee7-205">Obsługiwane wartości to: "ACTIVE", "SUSPENDed" lub "unsupportedd".</span><span class="sxs-lookup"><span data-stu-id="b8ee7-205">Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".</span></span> |
| <span data-ttu-id="b8ee7-206">SubscriptionType</span><span class="sxs-lookup"><span data-stu-id="b8ee7-206">subscriptionType</span></span> | <span data-ttu-id="b8ee7-207">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="b8ee7-207">`eq`, `ne`</span></span> | <span data-ttu-id="b8ee7-208">Typ subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-208">The subscription type.</span></span> <span data-ttu-id="b8ee7-209">**Uwaga**: w tym polu jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-209">**Note**: This field is case-sensitive.</span></span> <span data-ttu-id="b8ee7-210">Obsługiwane są następujące wartości: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span><span class="sxs-lookup"><span data-stu-id="b8ee7-210">Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span></span> |
| <span data-ttu-id="b8ee7-211">trialStartDate</span><span class="sxs-lookup"><span data-stu-id="b8ee7-211">trialStartDate</span></span> | <span data-ttu-id="b8ee7-212">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="b8ee7-212">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="b8ee7-213">Data rozpoczęcia okresu próbnego dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-213">The date that the trial period for the subscription started.</span></span> <span data-ttu-id="b8ee7-214">Wartość domyślna to null.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-214">The default value is null.</span></span> |
| <span data-ttu-id="b8ee7-215">trialToPaidConversionDate</span><span class="sxs-lookup"><span data-stu-id="b8ee7-215">trialToPaidConversionDate</span></span> | <span data-ttu-id="b8ee7-216">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="b8ee7-216">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="b8ee7-217">Data konwersji subskrypcji z wersji próbnej na płatne.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-217">The date that the subscription converts from trial to paid.</span></span> <span data-ttu-id="b8ee7-218">Wartość domyślna to null.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-218">The default value is null.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b8ee7-219">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="b8ee7-219">Request headers</span></span>

<span data-ttu-id="b8ee7-220">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b8ee7-220">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b8ee7-221">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="b8ee7-221">Request body</span></span>

<span data-ttu-id="b8ee7-222">Brak.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-222">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b8ee7-223">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="b8ee7-223">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="b8ee7-224">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="b8ee7-224">REST response</span></span>

<span data-ttu-id="b8ee7-225">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [subskrypcji](partner-center-analytics-resources.md#subscription-resource) , które spełniają kryteria filtrowania.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-225">If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription-resource) resources that meet the filter criteria.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b8ee7-226">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b8ee7-226">Response success and error codes</span></span>

<span data-ttu-id="b8ee7-227">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-227">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b8ee7-228">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="b8ee7-228">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b8ee7-229">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b8ee7-229">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b8ee7-230">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b8ee7-230">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="b8ee7-231">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b8ee7-231">See also</span></span>

- [<span data-ttu-id="b8ee7-232">Analiza Centrum partnerskiego — zasoby</span><span class="sxs-lookup"><span data-stu-id="b8ee7-232">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
