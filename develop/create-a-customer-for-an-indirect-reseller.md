---
title: Tworzenie klienta dla odsprzedawcy pośredniego
description: Dowiedz się, w jaki sposób Dostawca pośredni może użyć interfejsów API Centrum partnerskiego, aby utworzyć klienta dla pośredniego odsprzedawcy.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 13cd1b051abb536d397dcd4000228f67fe3206b8
ms.sourcegitcommit: 204e518e794b6b076a17488ee9ca1aaaa4beaaec
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/01/2021
ms.locfileid: "106103950"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a><span data-ttu-id="aa0b4-103">Tworzenie klienta dla pośredniego odsprzedawcy przy użyciu interfejsów API usługi Partner Center</span><span class="sxs-lookup"><span data-stu-id="aa0b4-103">Create a customer for an indirect reseller using Partner Center APIs</span></span>

<span data-ttu-id="aa0b4-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="aa0b4-104">**Applies to:**</span></span>

- <span data-ttu-id="aa0b4-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="aa0b4-105">Partner Center</span></span>

<span data-ttu-id="aa0b4-106">Dostawca pośredni może utworzyć klienta dla pośredniego odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-106">An indirect provider can create a customer for an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa0b4-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="aa0b4-107">Prerequisites</span></span>

- <span data-ttu-id="aa0b4-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="aa0b4-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="aa0b4-109">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="aa0b4-110">Identyfikator dzierżawy pośredniego odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-110">The tenant identifier of the indirect reseller.</span></span>

- <span data-ttu-id="aa0b4-111">Pośredni odsprzedawca musi mieć partnerstwo z dostawcą pośrednim.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-111">The indirect reseller must have a partnership with the indirect provider.</span></span>

## <a name="c"></a><span data-ttu-id="aa0b4-112">C\#</span><span class="sxs-lookup"><span data-stu-id="aa0b4-112">C\#</span></span>

<span data-ttu-id="aa0b4-113">Aby dodać nowego klienta w odniesieniu do pośredniego odsprzedawcy:</span><span class="sxs-lookup"><span data-stu-id="aa0b4-113">To add a new customer for an indirect reseller:</span></span>

1. <span data-ttu-id="aa0b4-114">Utwórz wystąpienie nowego obiektu [**klienta**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) , a następnie Utwórz wystąpienie i wypełnij [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) i [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span><span class="sxs-lookup"><span data-stu-id="aa0b4-114">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object and then instantiate and populate the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span> <span data-ttu-id="aa0b4-115">Należy pamiętać, aby przypisać pośredni identyfikator odsprzedawcy do właściwości [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) .</span><span class="sxs-lookup"><span data-stu-id="aa0b4-115">Be sure to assign the indirect reseller ID to the [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) property.</span></span>

2. <span data-ttu-id="aa0b4-116">Użyj właściwości [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , aby uzyskać interfejs do operacji zbierania danych przez klienta.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-116">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) property to get an interface to customer collection operations.</span></span>

3. <span data-ttu-id="aa0b4-117">Wywołaj metodę [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) lub [**onasync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) , aby utworzyć klienta.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-117">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the customer.</span></span>

### <a name="c-example"></a><span data-ttu-id="aa0b4-118">\#Przykład C</span><span class="sxs-lookup"><span data-stu-id="aa0b4-118">C\# example</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var indirectResellerId;
var customerToCreate = new Customer()
{
    CompanyProfile = new CustomerCompanyProfile()
    {
        Domain = string.Format(CultureInfo.InvariantCulture,
            "WingtipToys{0}.{1}",
            new Random().Next(),
            this.Context.Configuration.Scenario.CustomerDomainSuffix)
    },
    BillingProfile = new CustomerBillingProfile()
    {
        Culture = "EN-US",
        Email = "Gena@wingtiptoys.com",
        Language = "En",
        CompanyName = "Wingtip Toys" + new Random().Next(),
        DefaultAddress = new Address()
        {
            FirstName = "Gena",
            LastName = "Soto",
            AddressLine1 = "One Microsoft Way",
            City = "Redmond",
            State = "WA",
            Country = "US",
            PostalCode = "98052",
            PhoneNumber = "4255550101"
        }
    },
    AssociatedPartnerId = indirectResellerId
};

var newCustomer = partnerOperations.Customers.Create(customerToCreate);
```

<span data-ttu-id="aa0b4-119">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="aa0b4-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="aa0b4-120">**Projekt**: **Klasa** przykładów zestawu SDK Centrum partnerskiego: CreateCustomerforIndirectReseller. cs</span><span class="sxs-lookup"><span data-stu-id="aa0b4-120">**Project**: Partner Center SDK Samples **Class**: CreateCustomerforIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="aa0b4-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="aa0b4-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="aa0b4-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="aa0b4-122">Request syntax</span></span>

| <span data-ttu-id="aa0b4-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="aa0b4-123">Method</span></span>   | <span data-ttu-id="aa0b4-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="aa0b4-124">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="aa0b4-125">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="aa0b4-125">**POST**</span></span> | <span data-ttu-id="aa0b4-126">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers http/1.1</span><span class="sxs-lookup"><span data-stu-id="aa0b4-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="aa0b4-127">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="aa0b4-127">Request headers</span></span>

<span data-ttu-id="aa0b4-128">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="aa0b4-128">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="aa0b4-129">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="aa0b4-129">Request body</span></span>

<span data-ttu-id="aa0b4-130">W tej tabeli opisano wymagane właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-130">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="aa0b4-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="aa0b4-131">Name</span></span>                                          | <span data-ttu-id="aa0b4-132">Typ</span><span class="sxs-lookup"><span data-stu-id="aa0b4-132">Type</span></span>   | <span data-ttu-id="aa0b4-133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="aa0b4-133">Required</span></span> | <span data-ttu-id="aa0b4-134">Opis</span><span class="sxs-lookup"><span data-stu-id="aa0b4-134">Description</span></span>                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="aa0b4-135">BillingProfile</span><span class="sxs-lookup"><span data-stu-id="aa0b4-135">BillingProfile</span></span>](#billing-profile)             | <span data-ttu-id="aa0b4-136">object</span><span class="sxs-lookup"><span data-stu-id="aa0b4-136">object</span></span> | <span data-ttu-id="aa0b4-137">Tak</span><span class="sxs-lookup"><span data-stu-id="aa0b4-137">Yes</span></span>      | <span data-ttu-id="aa0b4-138">Informacje o profilu rozliczania klienta.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-138">The customer's billing profile information.</span></span>                                                                                                                                                                                                                                                                                                           |
| [<span data-ttu-id="aa0b4-139">CompanyProfile</span><span class="sxs-lookup"><span data-stu-id="aa0b4-139">CompanyProfile</span></span>](#company-profile)             | <span data-ttu-id="aa0b4-140">object</span><span class="sxs-lookup"><span data-stu-id="aa0b4-140">object</span></span> | <span data-ttu-id="aa0b4-141">Tak</span><span class="sxs-lookup"><span data-stu-id="aa0b4-141">Yes</span></span>      | <span data-ttu-id="aa0b4-142">Informacje o profilu firmy klienta.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-142">The customer's company profile information.</span></span>                                                               
| [<span data-ttu-id="aa0b4-143">AssociatedPartnerId</span><span class="sxs-lookup"><span data-stu-id="aa0b4-143">AssociatedPartnerId</span></span>](customer-resources.md#customer) | <span data-ttu-id="aa0b4-144">ciąg</span><span class="sxs-lookup"><span data-stu-id="aa0b4-144">string</span></span> | <span data-ttu-id="aa0b4-145">Tak</span><span class="sxs-lookup"><span data-stu-id="aa0b4-145">Yes</span></span>      | <span data-ttu-id="aa0b4-146">Identyfikator pośredniego odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-146">The indirect reseller ID.</span></span> <span data-ttu-id="aa0b4-147">Pośredni odsprzedawca określony przez podany tutaj identyfikator musi mieć powiązanie z dostawcą pośrednim lub żądanie zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-147">The indirect reseller as indicated by the ID supplied here must have a partnership with the indirect provider or the request will fail.</span></span> <span data-ttu-id="aa0b4-148">Należy również pamiętać, że jeśli wartość AssociatedPartnerId nie zostanie podana, klient zostanie utworzony jako bezpośredni klient dostawcy pośredniego, a nie pośredni odsprzedawca.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-148">Also note that if the AssociatedPartnerId value isn't supplied, the customer is created as a direct customer of the indirect provider rather than the indirect reseller.</span></span> |
|<span data-ttu-id="aa0b4-149">Domena</span><span class="sxs-lookup"><span data-stu-id="aa0b4-149">Domain</span></span>| <span data-ttu-id="aa0b4-150">Ciąg</span><span class="sxs-lookup"><span data-stu-id="aa0b4-150">String</span></span>| <span data-ttu-id="aa0b4-151">Tak</span><span class="sxs-lookup"><span data-stu-id="aa0b4-151">Yes</span></span>|<span data-ttu-id="aa0b4-152">Nazwa domeny klienta, na przykład contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-152">The customer's domain name, such as contoso.onmicrosoft.com.</span></span>|
|<span data-ttu-id="aa0b4-153">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="aa0b4-153">organizationRegistrationNumber</span></span>|    <span data-ttu-id="aa0b4-154">ciąg</span><span class="sxs-lookup"><span data-stu-id="aa0b4-154">string</span></span>|<span data-ttu-id="aa0b4-155">Tak</span><span class="sxs-lookup"><span data-stu-id="aa0b4-155">Yes</span></span>|     <span data-ttu-id="aa0b4-156">Numer identyfikacyjny organizacji klienta (określany również jako numer INN w niektórych krajach).</span><span class="sxs-lookup"><span data-stu-id="aa0b4-156">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="aa0b4-157">Wymagane tylko w przypadku firmowego/organizacji klienta znajdującego się w następujących krajach: Armenia (AM), Azerbejdżan (AZ), Białoruś (w przypadku), Węgry (HU), Kazachstan (KZ), Kirgistan (KG), Mołdawia (MD), Rosja (RU), Tadżykistan (TJ), Uzbekistan (UZ), Ukraina (UA), Indie, Brazylia, Afryka Południowa, Polskę, Zjednoczone Emiraty Arabskie, Arabia Saudyjska, Turcja, Tajlandia, Wietnam, Myanmar, Irak, Sudan Południowy i Wenezuela.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-157">Only required for customer’s company/organization located in the following countries: Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA), India, Brazil, South Africa, Poland, United Arab Emirates, Saudi Arabia, Turkey, Thailand, Vietnam, Myanmar, Iraq, South Sudan and Venezuela.</span></span> <span data-ttu-id="aa0b4-158">W przypadku firmy/organizacji klienta znajdującej się w innych krajach jest to pole opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-158">For customer’s company/organization located in other countries this is an optional field.</span></span>|



#### <a name="billing-profile"></a><span data-ttu-id="aa0b4-159">Profil rozliczeniowy</span><span class="sxs-lookup"><span data-stu-id="aa0b4-159">Billing profile</span></span>

<span data-ttu-id="aa0b4-160">Ta tabela zawiera opis minimalnych wymaganych pól z zasobów [CustomerBillingProfile](customer-resources.md#customerbillingprofile) wymaganych do utworzenia nowego klienta.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-160">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="aa0b4-161">Nazwa</span><span class="sxs-lookup"><span data-stu-id="aa0b4-161">Name</span></span>             | <span data-ttu-id="aa0b4-162">Typ</span><span class="sxs-lookup"><span data-stu-id="aa0b4-162">Type</span></span>                                     | <span data-ttu-id="aa0b4-163">Wymagane</span><span class="sxs-lookup"><span data-stu-id="aa0b4-163">Required</span></span> | <span data-ttu-id="aa0b4-164">Opis</span><span class="sxs-lookup"><span data-stu-id="aa0b4-164">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="aa0b4-165">poczta e-mail</span><span class="sxs-lookup"><span data-stu-id="aa0b4-165">email</span></span>            | <span data-ttu-id="aa0b4-166">ciąg</span><span class="sxs-lookup"><span data-stu-id="aa0b4-166">string</span></span>                                   | <span data-ttu-id="aa0b4-167">Tak</span><span class="sxs-lookup"><span data-stu-id="aa0b4-167">Yes</span></span>      | <span data-ttu-id="aa0b4-168">Adres e-mail klienta.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-168">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="aa0b4-169">kultura</span><span class="sxs-lookup"><span data-stu-id="aa0b4-169">culture</span></span>          | <span data-ttu-id="aa0b4-170">ciąg</span><span class="sxs-lookup"><span data-stu-id="aa0b4-170">string</span></span>                                   | <span data-ttu-id="aa0b4-171">Tak</span><span class="sxs-lookup"><span data-stu-id="aa0b4-171">Yes</span></span>      | <span data-ttu-id="aa0b4-172">Ich preferowana kultura do komunikacji i waluty, na przykład "en-US".</span><span class="sxs-lookup"><span data-stu-id="aa0b4-172">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="aa0b4-173">Zobacz obsługiwane [Języki w centrum partnerskim i ustawienia regionalne](partner-center-supported-languages-and-locales.md) dla obsługiwanych kultur.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-173">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="aa0b4-174">language</span><span class="sxs-lookup"><span data-stu-id="aa0b4-174">language</span></span>         | <span data-ttu-id="aa0b4-175">ciąg</span><span class="sxs-lookup"><span data-stu-id="aa0b4-175">string</span></span>                                   | <span data-ttu-id="aa0b4-176">Tak</span><span class="sxs-lookup"><span data-stu-id="aa0b4-176">Yes</span></span>      | <span data-ttu-id="aa0b4-177">Język domyślny.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-177">The default language.</span></span> <span data-ttu-id="aa0b4-178">Obsługiwane są dwa znaki kodów języka (na przykład `en` lub `fr` ).</span><span class="sxs-lookup"><span data-stu-id="aa0b4-178">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="aa0b4-179">\_Nazwa firmy</span><span class="sxs-lookup"><span data-stu-id="aa0b4-179">company\_name</span></span>    | <span data-ttu-id="aa0b4-180">ciąg</span><span class="sxs-lookup"><span data-stu-id="aa0b4-180">string</span></span>                                   | <span data-ttu-id="aa0b4-181">Tak</span><span class="sxs-lookup"><span data-stu-id="aa0b4-181">Yes</span></span>      | <span data-ttu-id="aa0b4-182">Nazwa zarejestrowanej firmy/organizacji.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-182">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="aa0b4-183">domyślny \_ adres</span><span class="sxs-lookup"><span data-stu-id="aa0b4-183">default\_address</span></span> | [<span data-ttu-id="aa0b4-184">Adres</span><span class="sxs-lookup"><span data-stu-id="aa0b4-184">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="aa0b4-185">Tak</span><span class="sxs-lookup"><span data-stu-id="aa0b4-185">Yes</span></span>      | <span data-ttu-id="aa0b4-186">Zarejestrowany adres firmy/organizacji klienta.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-186">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="aa0b4-187">Zobacz zasób [adresu](utility-resources.md#address) , aby uzyskać informacje o ograniczeniach długości.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-187">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="aa0b4-188">Profil firmy</span><span class="sxs-lookup"><span data-stu-id="aa0b4-188">Company profile</span></span>

<span data-ttu-id="aa0b4-189">Ta tabela zawiera opis minimalnych wymaganych pól z zasobów [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) wymaganych do utworzenia nowego klienta.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-189">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="aa0b4-190">Nazwa</span><span class="sxs-lookup"><span data-stu-id="aa0b4-190">Name</span></span>   | <span data-ttu-id="aa0b4-191">Typ</span><span class="sxs-lookup"><span data-stu-id="aa0b4-191">Type</span></span>   | <span data-ttu-id="aa0b4-192">Wymagane</span><span class="sxs-lookup"><span data-stu-id="aa0b4-192">Required</span></span> | <span data-ttu-id="aa0b4-193">Opis</span><span class="sxs-lookup"><span data-stu-id="aa0b4-193">Description</span></span>                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="aa0b4-194">domena</span><span class="sxs-lookup"><span data-stu-id="aa0b4-194">domain</span></span> | <span data-ttu-id="aa0b4-195">ciąg</span><span class="sxs-lookup"><span data-stu-id="aa0b4-195">string</span></span> | <span data-ttu-id="aa0b4-196">Tak</span><span class="sxs-lookup"><span data-stu-id="aa0b4-196">Yes</span></span>     | <span data-ttu-id="aa0b4-197">Nazwa domeny klienta, na przykład contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-197">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
| <span data-ttu-id="aa0b4-198">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="aa0b4-198">organizationRegistrationNumber</span></span> | <span data-ttu-id="aa0b4-199">ciąg</span><span class="sxs-lookup"><span data-stu-id="aa0b4-199">string</span></span> | <span data-ttu-id="aa0b4-200">Zależy od warunku</span><span class="sxs-lookup"><span data-stu-id="aa0b4-200">Depends on condition</span></span> | <span data-ttu-id="aa0b4-201">Numer rejestracji organizacji klienta (określany również jako numer INN w niektórych krajach).</span><span class="sxs-lookup"><span data-stu-id="aa0b4-201">The customer’s organization registration number (also referred to as the INN number in certain countries).</span></span> <br/><br/><span data-ttu-id="aa0b4-202">Wypełnienie tego pola jest wymagane tylko wtedy, gdy firma lub organizacja klienta znajduje się w następujących krajach:</span><span class="sxs-lookup"><span data-stu-id="aa0b4-202">Completing this field is required only if a customer’s company/organization is located in the following countries:</span></span> <br/><br/><span data-ttu-id="aa0b4-203">-Armenia (AM)</span><span class="sxs-lookup"><span data-stu-id="aa0b4-203">- Armenia (AM)</span></span> <br/><span data-ttu-id="aa0b4-204">-Azerbejdżan (AZ)</span><span class="sxs-lookup"><span data-stu-id="aa0b4-204">- Azerbaijan (AZ)</span></span><br/><span data-ttu-id="aa0b4-205">-Białoruś (przez)</span><span class="sxs-lookup"><span data-stu-id="aa0b4-205">- Belarus (BY)</span></span><br/><span data-ttu-id="aa0b4-206">-Węgry (HU)</span><span class="sxs-lookup"><span data-stu-id="aa0b4-206">- Hungary (HU)</span></span><br/><span data-ttu-id="aa0b4-207">-Kazachstan (KZ)</span><span class="sxs-lookup"><span data-stu-id="aa0b4-207">- Kazakhstan (KZ)</span></span><br/><span data-ttu-id="aa0b4-208">-Kirgistan (KG)</span><span class="sxs-lookup"><span data-stu-id="aa0b4-208">- Kyrgyzstan (KG)</span></span><br/><span data-ttu-id="aa0b4-209">— Mołdawia (MD)</span><span class="sxs-lookup"><span data-stu-id="aa0b4-209">- Moldova (MD)</span></span><br/><span data-ttu-id="aa0b4-210">— Rosja (RU)</span><span class="sxs-lookup"><span data-stu-id="aa0b4-210">- Russia (RU)</span></span><br/><span data-ttu-id="aa0b4-211">-Tadżykistan (TJ)</span><span class="sxs-lookup"><span data-stu-id="aa0b4-211">- Tajikistan (TJ)</span></span><br/><span data-ttu-id="aa0b4-212">-Uzbekistan (UZ)</span><span class="sxs-lookup"><span data-stu-id="aa0b4-212">- Uzbekistan (UZ)</span></span><br/><span data-ttu-id="aa0b4-213">-Ukraina (UA)</span><span class="sxs-lookup"><span data-stu-id="aa0b4-213">- Ukraine (UA)</span></span><br/><br/><span data-ttu-id="aa0b4-214">To pole nie jest wymagane, jeśli firma/organizacja klienta znajduje się w innych krajach poza tymi przedstawionymi tutaj.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-214">This field is not required if the customer’s company/organization is located in other countries beyond those shown here.</span></span>  |

### <a name="request-example"></a><span data-ttu-id="aa0b4-215">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="aa0b4-215">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: d628adbe-b7ee-412e-ac55-58f22b4ba2f4
MS-CorrelationId: 0dd197a8-992c-44ca-aeae-21cd83494dce
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 823
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": null,
    "CommerceId": null,
    "CompanyProfile": {
        "TenantId": null,
        "Domain": "WingtipToys678152504.onmicrosoft.com",
        "CompanyName": null,
        "Attributes": {
            "ObjectType": "CustomerCompanyProfile"
        }
    },
    "BillingProfile": {
        "Id": null,
        "FirstName": null,
        "LastName": null,
        "Email": "Gena@wingtiptoys.com",
        "Culture": "EN-US",
        "Language": "En",
        "CompanyName": "Wingtip Toys678152504",
        "DefaultAddress": {
            "Country": "US",
            "Region": null,
            "City": "Redmond",
            "State": "WA",
            "AddressLine1": "One Microsoft Way",
            "AddressLine2": null,
            "PostalCode": "98052",
            "FirstName": "Gena",
            "LastName": "Soto",
            "PhoneNumber": "4255550101"
        },
        "Attributes": {
            "ObjectType": "CustomerBillingProfile"
        }
    },
    "RelationshipToPartner": "none",
    "AllowDelegatedAccess": null,
    "UserCredentials": null,
    "CustomDomains": null,
    "AssociatedPartnerId": "484e548c-f5f3-4528-93a9-c16c6373cb59",
    "Attributes": {
        "ObjectType": "Customer"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="aa0b4-216">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="aa0b4-216">REST response</span></span>

<span data-ttu-id="aa0b4-217">Jeśli to się powiedzie, odpowiedź zawiera zasób [klienta](customer-resources.md#customer) dla nowego klienta.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-217">If successful, the response contains a [Customer](customer-resources.md#customer) resource for the new customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="aa0b4-218">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="aa0b4-218">Response success and error codes</span></span>

<span data-ttu-id="aa0b4-219">Odpowiedzi są uzyskiwane przy użyciu kodu stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-219">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="aa0b4-220">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="aa0b4-220">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="aa0b4-221">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="aa0b4-221">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="aa0b4-222">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="aa0b4-222">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 1085
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0dd197a8-992c-44ca-aeae-21cd83494dce
MS-RequestId: d628adbe-b7ee-412e-ac55-58f22b4ba2f4
MS-CV: Yy/YaA0gYEmfQyR/.0
MS-ServerId: 030020525
Date: Tue, 06 Jun 2017 23:11:40 GMT

{
    "id": "626099fe-17af-4756-9fd0-6a73b7127859",
    "commerceId": "626099fe-17af-4756-9fd0-6a73b7127859",
    "companyProfile": {
        "tenantId": "626099fe-17af-4756-9fd0-6a73b7127859",
        "domain": "WingtipToys678152504.onmicrosoft.com",
        "companyName": "Wingtip Toys678152504",
        "links": {
            "self": {
                "uri": "/customers/626099fe-17af-4756-9fd0-6a73b7127859/profiles/company",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "CustomerCompanyProfile"
        }
    },
    "billingProfile": {
        "id": "7079246e-7b62-56ef-7cbd-a819514b54b5",
        "email": "Gena@wingtiptoys.com",
        "culture": "en-US",
        "language": "En",
        "companyName": "Wingtip Toys678152504",
        "defaultAddress": {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "One Microsoft Way",
            "postalCode": "98052",
            "firstName": "Gena",
            "lastName": "Soto",
            "phoneNumber": "4255550101"
        },
        "attributes": {
            "etag": "-8799889149591823008",
            "objectType": "CustomerBillingProfile"
        }
    },
    "relationshipToPartner": "reseller",
    "allowDelegatedAccess": true,
    "userCredentials": {
        "userName": "admin",
        "password": "0Krha*Io"
    },
    "associatedPartnerId": "484e548c-f5f3-4528-93a9-c16c6373cb59",
    "attributes": {
        "objectType": "Customer"
    }
}
```