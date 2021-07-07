---
title: Tworzenie odsprzedawcy pośredniego w piaskownicy
description: Zawiera informacje dla dostawców pośrednich piaskownicy na temat włączania testowania end-to-end przy użyciu interfejsów API.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 93e26792b66e447a0047bd550f4302c7fca4e87b
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973438"
---
# <a name="create-indirect-reseller-in-sandbox"></a><span data-ttu-id="4d730-103">Tworzenie odsprzedawcy pośredniego w piaskownicy</span><span class="sxs-lookup"><span data-stu-id="4d730-103">Create Indirect Reseller in Sandbox</span></span>

<span data-ttu-id="4d730-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="4d730-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="4d730-105">W tym dokumencie przedstawiono sposób tworzenia dostawców pośrednich piaskownicy i włączania testowania end-to-end przy użyciu interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="4d730-105">This document shows how to create Sandbox Indirect Providers and enable end-to-end testing using APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d730-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4d730-106">Prerequisites</span></span>

- <span data-ttu-id="4d730-107">Poświadczenia zgodnie z opisem w te [Partner Center Authentication (Uwierzytelnianie).](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4d730-107">Credentials as described in [Partner Center Authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4d730-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4d730-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="csp-indirect-provider"></a><span data-ttu-id="4d730-109">CSP Indirect Provider</span><span class="sxs-lookup"><span data-stu-id="4d730-109">CSP Indirect Provider</span></span>

| <span data-ttu-id="4d730-110">Możliwości produkcyjne</span><span class="sxs-lookup"><span data-stu-id="4d730-110">Production capabilities</span></span>             | <span data-ttu-id="4d730-111">Możliwości piaskownicy</span><span class="sxs-lookup"><span data-stu-id="4d730-111">Sandbox capabilities</span></span>                            |
|-------------------------------------|-------------------------------------------------|
| <span data-ttu-id="4d730-112">Sprzedaż odsprzedawcy pośredniego klientowi końcowego</span><span class="sxs-lookup"><span data-stu-id="4d730-112">Sells through the indirect reseller to the end customer</span></span> | <span data-ttu-id="4d730-113">Obsługiwane</span><span class="sxs-lookup"><span data-stu-id="4d730-113">Supported</span></span> |
| <span data-ttu-id="4d730-114">Właścicielem całej sprzedaży, rozliczeń, aprowiwizowania i zarządzania/pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="4d730-114">Owns all sales, billing, provisioning, and management/support</span></span> | <span data-ttu-id="4d730-115">Obsługiwane</span><span class="sxs-lookup"><span data-stu-id="4d730-115">Supported</span></span> |
| <span data-ttu-id="4d730-116">Żądanie partnerstwa z odsprzedawcami</span><span class="sxs-lookup"><span data-stu-id="4d730-116">Request a partnership with the resellers</span></span> | <span data-ttu-id="4d730-117">Obsługiwane</span><span class="sxs-lookup"><span data-stu-id="4d730-117">Supported</span></span> |
| <span data-ttu-id="4d730-118">Wyświetlanie klientów według odsprzedawcy</span><span class="sxs-lookup"><span data-stu-id="4d730-118">View customers by Reseller</span></span> | <span data-ttu-id="4d730-119">Obsługiwane</span><span class="sxs-lookup"><span data-stu-id="4d730-119">Supported</span></span> |
| <span data-ttu-id="4d730-120">Dodawanie nowych klientów według odsprzedawców</span><span class="sxs-lookup"><span data-stu-id="4d730-120">Add new customers by resellers</span></span> | <span data-ttu-id="4d730-121">Obsługiwane</span><span class="sxs-lookup"><span data-stu-id="4d730-121">Supported</span></span> |
| <span data-ttu-id="4d730-122">Zapraszanie klientów</span><span class="sxs-lookup"><span data-stu-id="4d730-122">Invite customers</span></span> | <span data-ttu-id="4d730-123">Żądanie relacji z klientem nie jest obsługiwane w piaskownicy</span><span class="sxs-lookup"><span data-stu-id="4d730-123">Customer relationship request not supported in Sandbox</span></span> |
| <span data-ttu-id="4d730-124">Dostawca pośredni piaskownicy może wybrać środowisko IR piaskownicy (identyfikator MPN) jako dostawcę tożsamości podczas umieszczania transakcji</span><span class="sxs-lookup"><span data-stu-id="4d730-124">Sandbox Indirect Provider can select Sandbox IR (MPN ID) as the POR while placing the transaction</span></span> | <span data-ttu-id="4d730-125">Obsługiwane</span><span class="sxs-lookup"><span data-stu-id="4d730-125">Supported</span></span> |
| <span data-ttu-id="4d730-126">Nie jest obsługiwane w środowisku produkcyjnym</span><span class="sxs-lookup"><span data-stu-id="4d730-126">Not supported in production</span></span> | <span data-ttu-id="4d730-127">Dostawca pośredni piaskownicy może utworzyć odsprzedawcę pośredniego piaskownicy</span><span class="sxs-lookup"><span data-stu-id="4d730-127">Sandbox Indirect Provider can create Sandbox Indirect Reseller</span></span> |
| <span data-ttu-id="4d730-128">Należy wprowadzić identyfikator MPN piaskownicy. Identyfikator MPN produktu nie będzie działać</span><span class="sxs-lookup"><span data-stu-id="4d730-128">Sandbox MPN ID should be entered, the product MPN ID will not work</span></span> | <span data-ttu-id="4d730-129">Nie jest obsługiwane w środowisku produkcyjnym</span><span class="sxs-lookup"><span data-stu-id="4d730-129">Not supported in production</span></span> |
| <span data-ttu-id="4d730-130">Nie jest obsługiwane w środowisku produkcyjnym</span><span class="sxs-lookup"><span data-stu-id="4d730-130">Not supported in production</span></span> | <span data-ttu-id="4d730-131">Dostawca pośredni piaskownicy może usunąć odsprzedawcę pośredniego piaskownicy</span><span class="sxs-lookup"><span data-stu-id="4d730-131">Sandbox Indirect Provider can delete Sandbox Indirect Reseller</span></span> |

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller"></a><span data-ttu-id="4d730-132">Dostawca pośredni piaskownicy — tworzenie odsprzedawcy pośredniego piaskownicy</span><span class="sxs-lookup"><span data-stu-id="4d730-132">Sandbox Indirect Provider – Create Sandbox Indirect Reseller</span></span>

<span data-ttu-id="4d730-133">Ta funkcja jest dostępna tylko w piaskownicy i umożliwia dostawcom pośrednim piaskownicy tworzenie odsprzedawców pośrednich piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="4d730-133">This feature is only available in the Sandbox and gives Sandbox Indirect Providers an ability to create Sandbox Indirect Resellers.</span></span>

1. <span data-ttu-id="4d730-134">Limit pięciu pośrednich odsprzedawców piaskownicy dozwolonych na dostawcę pośredniego piaskownicy</span><span class="sxs-lookup"><span data-stu-id="4d730-134">Limit of five Sandbox Indirect Resellers allowed per Sandbox Indirect Provider</span></span>
2. <span data-ttu-id="4d730-135">Dostawcy pośredni piaskownicy mogą tworzyć klientów u `associatedPartnerId` odsprzedawcy pośredniego piaskownicy</span><span class="sxs-lookup"><span data-stu-id="4d730-135">Sandbox Indirect Providers can create customers with `associatedPartnerId` of Sandbox Indirect Reseller</span></span>
3. <span data-ttu-id="4d730-136">Wprowadź identyfikator [MPN](/partner-center/mpn-create-a-partner-center-account) określonego regionu podczas tworzenia odsprzedawcy pośredniego piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="4d730-136">Enter the [MPN](/partner-center/mpn-create-a-partner-center-account) ID of a specific region while creating a Sandbox Indirect Reseller.</span></span> <span data-ttu-id="4d730-137">Wielu pośrednich odsprzedawców piaskownicy można utworzyć przy użyciu tego samego identyfikatora MPN piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="4d730-137">Multiple Sandbox Indirect Resellers can be created with the same Sandbox MPN ID.</span></span>
4. <span data-ttu-id="4d730-138">Tylko 75 klientów jest dozwolonych na dostawcę pośredniego piaskownicy</span><span class="sxs-lookup"><span data-stu-id="4d730-138">Only 75 customers are allowed per Sandbox Indirect Provider</span></span>

## <a name="sandbox-indirect-resellers--view-customers"></a><span data-ttu-id="4d730-139">Odsprzedawcy pośredni piaskownicy — wyświetlanie klientów</span><span class="sxs-lookup"><span data-stu-id="4d730-139">Sandbox Indirect Resellers – View customers</span></span>

1. <span data-ttu-id="4d730-140">Odsprzedawcy pośredni piaskownicy mogą wyświetlać listę klientów piaskownicy według dostawców pośrednich piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="4d730-140">Sandbox Indirect Resellers can view the list of sandbox customers by Sandbox Indirect providers.</span></span>
2. <span data-ttu-id="4d730-141">Odsprzedawcy pośredni piaskownicy mogą zarządzać kontem klienta przy użyciu delegowanych uprawnień administratora.</span><span class="sxs-lookup"><span data-stu-id="4d730-141">Sandbox Indirect Resellers can manage the customer account by using delegated administrator permissions.</span></span>

## <a name="create-sandbox-indirect-reseller-through-api"></a><span data-ttu-id="4d730-142">Tworzenie odsprzedawcy pośredniego piaskownicy za pomocą interfejsu API</span><span class="sxs-lookup"><span data-stu-id="4d730-142">Create Sandbox Indirect Reseller through API</span></span>

### <a name="rest-request"></a><span data-ttu-id="4d730-143">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="4d730-143">REST request</span></span>

#### <a name="request-syntax"></a><span data-ttu-id="4d730-144">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="4d730-144">Request syntax</span></span>

| <span data-ttu-id="4d730-145">**Metoda**</span><span class="sxs-lookup"><span data-stu-id="4d730-145">**Method**</span></span> | <span data-ttu-id="4d730-146">**Identyfikator URI żądania**</span><span class="sxs-lookup"><span data-stu-id="4d730-146">**Request URI**</span></span>                                                        |
|------------|------------------------------------------------------------------------|
| <span data-ttu-id="4d730-147">**Post**</span><span class="sxs-lookup"><span data-stu-id="4d730-147">**POST**</span></span>   | <span data-ttu-id="4d730-148">[*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller</span><span class="sxs-lookup"><span data-stu-id="4d730-148">[*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller</span></span> |

#### <a name="request-headers"></a><span data-ttu-id="4d730-149">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="4d730-149">Request headers</span></span>

- <span data-ttu-id="4d730-150">Ten interfejs API jest idempotentny (nie da innego wyniku, jeśli wywołasz go wielokrotnie).</span><span class="sxs-lookup"><span data-stu-id="4d730-150">This API is idempotent (it will not yield a different result if you call it multiple times).</span></span>
- <span data-ttu-id="4d730-151">Wymagany jest identyfikator żądania i identyfikator korelacji.</span><span class="sxs-lookup"><span data-stu-id="4d730-151">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="4d730-152">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="4d730-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

#### <a name="request-body"></a><span data-ttu-id="4d730-153">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="4d730-153">Request body</span></span>

<span data-ttu-id="4d730-154">W tej tabeli opisano wymagane właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="4d730-154">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="4d730-155">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4d730-155">Property</span></span>             | <span data-ttu-id="4d730-156">Typ</span><span class="sxs-lookup"><span data-stu-id="4d730-156">Type</span></span>           | <span data-ttu-id="4d730-157">Opis</span><span class="sxs-lookup"><span data-stu-id="4d730-157">Description</span></span>                                      |
|----------------------|----------------|--------------------------------------------------|
| <span data-ttu-id="4d730-158">mpnId</span><span class="sxs-lookup"><span data-stu-id="4d730-158">mpnId</span></span>                | <span data-ttu-id="4d730-159">ciąg</span><span class="sxs-lookup"><span data-stu-id="4d730-159">string</span></span>         | <span data-ttu-id="4d730-160">Identyfikator MPN dla ir w określonym regionie</span><span class="sxs-lookup"><span data-stu-id="4d730-160">The MPN ID for the IR in specific region</span></span>         |
| <span data-ttu-id="4d730-161">Dzierżawy</span><span class="sxs-lookup"><span data-stu-id="4d730-161">tenant</span></span>               | <span data-ttu-id="4d730-162">Ciąg &lt; słownika, ciąg&gt;</span><span class="sxs-lookup"><span data-stu-id="4d730-162">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="4d730-163">Zbieranie podstawowych informacji definiującej konto do utworzenia</span><span class="sxs-lookup"><span data-stu-id="4d730-163">Collection of basic information that defines an account to be created</span></span> |
| <span data-ttu-id="4d730-164">legalBusinessProfile</span><span class="sxs-lookup"><span data-stu-id="4d730-164">legalBusinessProfile</span></span> | <span data-ttu-id="4d730-165">Ciąg &lt; słownika, ciąg&gt;</span><span class="sxs-lookup"><span data-stu-id="4d730-165">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="4d730-166">Zbieranie informacji, które reprezentują prawne jednostki biznesowe, takie jak kontakt, adres i nazwa</span><span class="sxs-lookup"><span data-stu-id="4d730-166">Collection of information that represents the legal business entity such as contact, address, and name</span></span> |
| <span data-ttu-id="4d730-167">organizationProfileLanguage</span><span class="sxs-lookup"><span data-stu-id="4d730-167">organizationProfileLanguage</span></span> | <span data-ttu-id="4d730-168">Ciąg &lt; słownika, ciąg&gt;</span><span class="sxs-lookup"><span data-stu-id="4d730-168">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="4d730-169">Identyfikator języka organizacji</span><span class="sxs-lookup"><span data-stu-id="4d730-169">The organization language identifier</span></span> |

<span data-ttu-id="4d730-170">W tej tabeli opisano wymagane właściwości **atrybutu dzierżawy.**</span><span class="sxs-lookup"><span data-stu-id="4d730-170">This table describes the required properties in the **tenant** attribute.</span></span>

| <span data-ttu-id="4d730-171">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4d730-171">Property</span></span>           | <span data-ttu-id="4d730-172">Typ</span><span class="sxs-lookup"><span data-stu-id="4d730-172">Type</span></span>           | <span data-ttu-id="4d730-173">Opis</span><span class="sxs-lookup"><span data-stu-id="4d730-173">Description</span></span>                         |
|--------------------|----------------|-------------------------------------|
| <span data-ttu-id="4d730-174">domainPrefix</span><span class="sxs-lookup"><span data-stu-id="4d730-174">domainPrefix</span></span>       | <span data-ttu-id="4d730-175">Ciąg; Unikatowy</span><span class="sxs-lookup"><span data-stu-id="4d730-175">String; unique</span></span> | <span data-ttu-id="4d730-176">Domena dla konta dzierżawy</span><span class="sxs-lookup"><span data-stu-id="4d730-176">Domain for the tenant account</span></span>       |
| <span data-ttu-id="4d730-177">name</span><span class="sxs-lookup"><span data-stu-id="4d730-177">name</span></span>               | <span data-ttu-id="4d730-178">ciąg</span><span class="sxs-lookup"><span data-stu-id="4d730-178">string</span></span>         | <span data-ttu-id="4d730-179">Przyjazna nazwa dzierżawy</span><span class="sxs-lookup"><span data-stu-id="4d730-179">Friendly name of the tenant</span></span>         |
| <span data-ttu-id="4d730-180">displayName</span><span class="sxs-lookup"><span data-stu-id="4d730-180">displayName</span></span>        | <span data-ttu-id="4d730-181">ciąg</span><span class="sxs-lookup"><span data-stu-id="4d730-181">string</span></span>         | <span data-ttu-id="4d730-182">Nazwa wyświetlana konta</span><span class="sxs-lookup"><span data-stu-id="4d730-182">Display name for the account</span></span>        |
| <span data-ttu-id="4d730-183">adminUserName</span><span class="sxs-lookup"><span data-stu-id="4d730-183">adminUserName</span></span>      | <span data-ttu-id="4d730-184">ciąg</span><span class="sxs-lookup"><span data-stu-id="4d730-184">string</span></span>         | <span data-ttu-id="4d730-185">Nazwa użytkownika konta do logowania</span><span class="sxs-lookup"><span data-stu-id="4d730-185">User name for the account for login</span></span> |
| <span data-ttu-id="4d730-186">adminfirstname (nazwa administratora)</span><span class="sxs-lookup"><span data-stu-id="4d730-186">adminfirstname</span></span>     | <span data-ttu-id="4d730-187">ciąg</span><span class="sxs-lookup"><span data-stu-id="4d730-187">string</span></span>         | <span data-ttu-id="4d730-188">Imię administratora</span><span class="sxs-lookup"><span data-stu-id="4d730-188">First Name for the admin user</span></span>       |
| <span data-ttu-id="4d730-189">adminlastname (nazwa administratora)</span><span class="sxs-lookup"><span data-stu-id="4d730-189">adminlastname</span></span>      | <span data-ttu-id="4d730-190">ciąg</span><span class="sxs-lookup"><span data-stu-id="4d730-190">string</span></span>         | <span data-ttu-id="4d730-191">Nazwisko administratora</span><span class="sxs-lookup"><span data-stu-id="4d730-191">Last Name for the admin user</span></span>        |
| <span data-ttu-id="4d730-192">adminAlernateEmail</span><span class="sxs-lookup"><span data-stu-id="4d730-192">adminAlernateEmail</span></span> | <span data-ttu-id="4d730-193">ciąg</span><span class="sxs-lookup"><span data-stu-id="4d730-193">string</span></span>         | <span data-ttu-id="4d730-194">wiadomość e-mail dla administratora</span><span class="sxs-lookup"><span data-stu-id="4d730-194">email for the admin user</span></span>            |
| <span data-ttu-id="4d730-195">country</span><span class="sxs-lookup"><span data-stu-id="4d730-195">country</span></span>            | <span data-ttu-id="4d730-196">ciąg</span><span class="sxs-lookup"><span data-stu-id="4d730-196">string</span></span>         | <span data-ttu-id="4d730-197">Kraj konta</span><span class="sxs-lookup"><span data-stu-id="4d730-197">Country of the account</span></span>              |
| <span data-ttu-id="4d730-198">kultura</span><span class="sxs-lookup"><span data-stu-id="4d730-198">culture</span></span>            | <span data-ttu-id="4d730-199">ciąg</span><span class="sxs-lookup"><span data-stu-id="4d730-199">string</span></span>         | <span data-ttu-id="4d730-200">Preferencja języka dla konta</span><span class="sxs-lookup"><span data-stu-id="4d730-200">Language preference for account</span></span>     |

<span data-ttu-id="4d730-201">W tej tabeli opisano wymagane właściwości **atrybutu legalBusinessProfile.**</span><span class="sxs-lookup"><span data-stu-id="4d730-201">This table describes the required properties in the **legalBusinessProfile** attribute.</span></span>

| <span data-ttu-id="4d730-202">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4d730-202">Property</span></span>       | <span data-ttu-id="4d730-203">Typ</span><span class="sxs-lookup"><span data-stu-id="4d730-203">Type</span></span>                             | <span data-ttu-id="4d730-204">Opis</span><span class="sxs-lookup"><span data-stu-id="4d730-204">Description</span></span>                          |
|----------------|----------------------------------|--------------------------------------|
| <span data-ttu-id="4d730-205">Companyname</span><span class="sxs-lookup"><span data-stu-id="4d730-205">companyName</span></span>    | <span data-ttu-id="4d730-206">ciąg</span><span class="sxs-lookup"><span data-stu-id="4d730-206">string</span></span>                           | <span data-ttu-id="4d730-207">Nazwa firmy dla jednostki prawnej</span><span class="sxs-lookup"><span data-stu-id="4d730-207">Company name for legal entity</span></span>        |
| <span data-ttu-id="4d730-208">adres</span><span class="sxs-lookup"><span data-stu-id="4d730-208">address</span></span>        | <span data-ttu-id="4d730-209">Ciąg &lt; słownika, ciąg&gt;</span><span class="sxs-lookup"><span data-stu-id="4d730-209">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="4d730-210">Adres lokalizacji jednostki prawnej</span><span class="sxs-lookup"><span data-stu-id="4d730-210">Address of the legal entity location</span></span> |
| <span data-ttu-id="4d730-211">primaryContact</span><span class="sxs-lookup"><span data-stu-id="4d730-211">primaryContact</span></span> | <span data-ttu-id="4d730-212">Ciąg &lt; słownika, ciąg&gt;</span><span class="sxs-lookup"><span data-stu-id="4d730-212">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="4d730-213">Dane kontaktowe firmy</span><span class="sxs-lookup"><span data-stu-id="4d730-213">Contact details of the company</span></span>       |
| <span data-ttu-id="4d730-214">kultura</span><span class="sxs-lookup"><span data-stu-id="4d730-214">culture</span></span>        | <span data-ttu-id="4d730-215">ciąg</span><span class="sxs-lookup"><span data-stu-id="4d730-215">string</span></span>                           | <span data-ttu-id="4d730-216">Język preferowany przez firmę</span><span class="sxs-lookup"><span data-stu-id="4d730-216">Language preferred by the company</span></span>    |

### <a name="request-example"></a><span data-ttu-id="4d730-217">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="4d730-217">Request Example</span></span>

```http
{
    "mpnId": "6363276",
    "tenant": {
        "domainPrefix": "TipIRIntTest705",
        "name": "TipIRIntTest705",
        "displayName": "TipIRIntTest705",
        "adminUserName": "admin",
        "adminFirstName": "TipIRIntTest705",
        "adminLastName": "TipIRIntTest705",
        "adminAlternateEmail": "TipIRIntTest705@test.com",
        "country": "US",
        "culture": "en-us"
    },
    "legalBusinessProfile": {
        "companyName": "TipIRIntTest705",
        "address": {
            "country": "FR",
            "city": "Issy-les-Moulineaux",
            "state": "",
            "addressLine1": "39-41 quai du Président Roosevelt",
            "addressLine2": "",
            "postalCode": "92130"
        },
        "primaryContact": {
            "firstName": "Sandbox",
            "lastName": "Scenario",
            "email": "Sandbox.Scenario@test.com",
            "phoneNumber": "1234567890"
        },
        "culture": "en-US"
    },
    "organizationProfileLanguage": "en"
}
```

### <a name="rest-response"></a><span data-ttu-id="4d730-218">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="4d730-218">REST response</span></span>

<span data-ttu-id="4d730-219">W przypadku powodzenia ta metoda zwraca wypełniony zasób środowiska IR piaskownicy w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="4d730-219">If successful, this method returns the populated Sandbox IR resource in the response body.</span></span>

```http
{

    "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
    "mpnId": "6363276",
    "tenant": {
        "id": "6f94b119-793c-44c7-862b-c327c9057eab",
        "adminUserAccount": "admin@TipIRIntTest705.onmicrosoft.com",
        "password": "\*\*\*\*\*\*”
    },
    "agreementSignature": {
        "id": "30ac23e7-e200-42cf-a5bc-dd9148cdc632",
        "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
        "agreementId": "1e18c5b2-e42a-4b84-82c8-d0155aa94c6e",
        "agreementType": "ValueAddedReseller",
        "dateSigned": "2021-02-23T18:10:14.8461137Z",
        "signedByFirstName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserPrincipalName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserObjectId": "e6e0c29d-acda-4ef2-b370-d37a4e06fb98",
        "signedByUserTenantId": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "attributes": {
            "objectType": "AgreementSignatureResponse"
        }
    },
    "partnerRelationship": {
        "id": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "name": "PLAMUATT2NetNew",
        "relationshipType": "is\_indirect\_reseller\_of",
        "state": "Active",
        "mpnId": "6363276",
        "attributes": {
            "objectType": "PartnerRelationshipResponse"
        }
    }
}
```
