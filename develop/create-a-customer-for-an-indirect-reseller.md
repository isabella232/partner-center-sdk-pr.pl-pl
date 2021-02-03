---
title: Tworzenie klienta dla odsprzedawcy pośredniego
description: Dowiedz się, w jaki sposób Dostawca pośredni może użyć interfejsów API Centrum partnerskiego, aby utworzyć klienta dla pośredniego odsprzedawcy.
ms.date: 11/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e2386f1963a5bb3ea4269bcbf4327c75987f3b91
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770179"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a><span data-ttu-id="9e87f-103">Tworzenie klienta dla pośredniego odsprzedawcy przy użyciu interfejsów API usługi Partner Center</span><span class="sxs-lookup"><span data-stu-id="9e87f-103">Create a customer for an indirect reseller using Partner Center APIs</span></span>

<span data-ttu-id="9e87f-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="9e87f-104">**Applies to:**</span></span>

- <span data-ttu-id="9e87f-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="9e87f-105">Partner Center</span></span>

<span data-ttu-id="9e87f-106">Dostawca pośredni może utworzyć klienta dla pośredniego odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="9e87f-106">An indirect provider can create a customer for an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e87f-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9e87f-107">Prerequisites</span></span>

- <span data-ttu-id="9e87f-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9e87f-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9e87f-109">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9e87f-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="9e87f-110">Identyfikator dzierżawy pośredniego odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="9e87f-110">The tenant identifier of the indirect reseller.</span></span>

- <span data-ttu-id="9e87f-111">Pośredni odsprzedawca musi mieć partnerstwo z dostawcą pośrednim.</span><span class="sxs-lookup"><span data-stu-id="9e87f-111">The indirect reseller must have a partnership with the indirect provider.</span></span>

## <a name="c"></a><span data-ttu-id="9e87f-112">C\#</span><span class="sxs-lookup"><span data-stu-id="9e87f-112">C\#</span></span>

<span data-ttu-id="9e87f-113">Aby dodać nowego klienta w odniesieniu do pośredniego odsprzedawcy:</span><span class="sxs-lookup"><span data-stu-id="9e87f-113">To add a new customer for an indirect reseller:</span></span>

1. <span data-ttu-id="9e87f-114">Utwórz wystąpienie nowego obiektu [**klienta**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) , a następnie Utwórz wystąpienie i wypełnij [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) i [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span><span class="sxs-lookup"><span data-stu-id="9e87f-114">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object and then instantiate and populate the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span> <span data-ttu-id="9e87f-115">Należy pamiętać, aby przypisać pośredni identyfikator odsprzedawcy do właściwości [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) .</span><span class="sxs-lookup"><span data-stu-id="9e87f-115">Be sure to assign the indirect reseller ID to the [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) property.</span></span>

2. <span data-ttu-id="9e87f-116">Użyj właściwości [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , aby uzyskać interfejs do operacji zbierania danych przez klienta.</span><span class="sxs-lookup"><span data-stu-id="9e87f-116">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) property to get an interface to customer collection operations.</span></span>

3. <span data-ttu-id="9e87f-117">Wywołaj metodę [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) lub [**onasync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) , aby utworzyć klienta.</span><span class="sxs-lookup"><span data-stu-id="9e87f-117">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the customer.</span></span>

### <a name="c-example"></a><span data-ttu-id="9e87f-118">\#Przykład C</span><span class="sxs-lookup"><span data-stu-id="9e87f-118">C\# example</span></span>

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

<span data-ttu-id="9e87f-119">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9e87f-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9e87f-120">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: CreateCustomerforIndirectReseller.cs</span><span class="sxs-lookup"><span data-stu-id="9e87f-120">**Project**: Partner Center SDK Samples **Class**: CreateCustomerforIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9e87f-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="9e87f-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9e87f-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="9e87f-122">Request syntax</span></span>

| <span data-ttu-id="9e87f-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="9e87f-123">Method</span></span>   | <span data-ttu-id="9e87f-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="9e87f-124">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="9e87f-125">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="9e87f-125">**POST**</span></span> | <span data-ttu-id="9e87f-126">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers http/1.1</span><span class="sxs-lookup"><span data-stu-id="9e87f-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9e87f-127">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="9e87f-127">Request headers</span></span>

<span data-ttu-id="9e87f-128">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9e87f-128">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9e87f-129">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="9e87f-129">Request body</span></span>

<span data-ttu-id="9e87f-130">W tej tabeli opisano wymagane właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="9e87f-130">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="9e87f-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9e87f-131">Name</span></span>                                          | <span data-ttu-id="9e87f-132">Typ</span><span class="sxs-lookup"><span data-stu-id="9e87f-132">Type</span></span>   | <span data-ttu-id="9e87f-133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9e87f-133">Required</span></span> | <span data-ttu-id="9e87f-134">Opis</span><span class="sxs-lookup"><span data-stu-id="9e87f-134">Description</span></span>                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="9e87f-135">BillingProfile</span><span class="sxs-lookup"><span data-stu-id="9e87f-135">BillingProfile</span></span>](#billing-profile)             | <span data-ttu-id="9e87f-136">object</span><span class="sxs-lookup"><span data-stu-id="9e87f-136">object</span></span> | <span data-ttu-id="9e87f-137">Tak</span><span class="sxs-lookup"><span data-stu-id="9e87f-137">Yes</span></span>      | <span data-ttu-id="9e87f-138">Informacje o profilu rozliczania klienta.</span><span class="sxs-lookup"><span data-stu-id="9e87f-138">The customer's billing profile information.</span></span>                                                                                                                                                                                                                                                                                                           |
| [<span data-ttu-id="9e87f-139">CompanyProfile</span><span class="sxs-lookup"><span data-stu-id="9e87f-139">CompanyProfile</span></span>](#company-profile)             | <span data-ttu-id="9e87f-140">object</span><span class="sxs-lookup"><span data-stu-id="9e87f-140">object</span></span> | <span data-ttu-id="9e87f-141">Tak</span><span class="sxs-lookup"><span data-stu-id="9e87f-141">Yes</span></span>      | <span data-ttu-id="9e87f-142">Informacje o profilu firmy klienta.</span><span class="sxs-lookup"><span data-stu-id="9e87f-142">The customer's company profile information.</span></span>                                                               
| [<span data-ttu-id="9e87f-143">AssociatedPartnerId</span><span class="sxs-lookup"><span data-stu-id="9e87f-143">AssociatedPartnerId</span></span>](customer-resources.md#customer) | <span data-ttu-id="9e87f-144">ciąg</span><span class="sxs-lookup"><span data-stu-id="9e87f-144">string</span></span> | <span data-ttu-id="9e87f-145">Tak</span><span class="sxs-lookup"><span data-stu-id="9e87f-145">Yes</span></span>      | <span data-ttu-id="9e87f-146">Identyfikator pośredniego odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="9e87f-146">The indirect reseller ID.</span></span> <span data-ttu-id="9e87f-147">Pośredni odsprzedawca określony przez podany tutaj identyfikator musi mieć powiązanie z dostawcą pośrednim lub żądanie zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="9e87f-147">The indirect reseller as indicated by the ID supplied here must have a partnership with the indirect provider or the request will fail.</span></span> <span data-ttu-id="9e87f-148">Należy również pamiętać, że jeśli wartość AssociatedPartnerId nie zostanie podana, klient zostanie utworzony jako bezpośredni klient dostawcy pośredniego, a nie pośredni odsprzedawca.</span><span class="sxs-lookup"><span data-stu-id="9e87f-148">Also note that if the AssociatedPartnerId value isn't supplied, the customer is created as a direct customer of the indirect provider rather than the indirect reseller.</span></span> |
|<span data-ttu-id="9e87f-149">Domena</span><span class="sxs-lookup"><span data-stu-id="9e87f-149">Domain</span></span>| <span data-ttu-id="9e87f-150">Ciąg</span><span class="sxs-lookup"><span data-stu-id="9e87f-150">String</span></span>| <span data-ttu-id="9e87f-151">Tak</span><span class="sxs-lookup"><span data-stu-id="9e87f-151">Yes</span></span>|<span data-ttu-id="9e87f-152">Nazwa domeny klienta, na przykład contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="9e87f-152">The customer's domain name, such as contoso.onmicrosoft.com.</span></span>|
|<span data-ttu-id="9e87f-153">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="9e87f-153">organizationRegistrationNumber</span></span>|    <span data-ttu-id="9e87f-154">ciąg</span><span class="sxs-lookup"><span data-stu-id="9e87f-154">string</span></span>|<span data-ttu-id="9e87f-155">Tak</span><span class="sxs-lookup"><span data-stu-id="9e87f-155">Yes</span></span>|     <span data-ttu-id="9e87f-156">Numer identyfikacyjny organizacji klienta (określany również jako numer INN w niektórych krajach).</span><span class="sxs-lookup"><span data-stu-id="9e87f-156">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="9e87f-157">Wymagane tylko dla firmy lub organizacji klienta w następujących krajach.</span><span class="sxs-lookup"><span data-stu-id="9e87f-157">Only required for customer’s company/organization located in the following countries.</span></span> <span data-ttu-id="9e87f-158">Armenia (AM), Azerbejdżan (AZ), Białoruś (przez), Węgry (HU), Kazachstan (KZ), Kirgistan (KG), Mołdawia (MD), Rosja (RU), Tadżykistan (TJ), Uzbekistan (UZ), Ukraina (UA).</span><span class="sxs-lookup"><span data-stu-id="9e87f-158">Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA).</span></span> <span data-ttu-id="9e87f-159">W przypadku firmy/organizacji klienta znajdującej się w innych krajach nie należy określać tego elementu.</span><span class="sxs-lookup"><span data-stu-id="9e87f-159">For customer’s company/organization located in other countries this should not be specified.</span></span>|



#### <a name="billing-profile"></a><span data-ttu-id="9e87f-160">Profil rozliczeniowy</span><span class="sxs-lookup"><span data-stu-id="9e87f-160">Billing profile</span></span>

<span data-ttu-id="9e87f-161">Ta tabela zawiera opis minimalnych wymaganych pól z zasobów [CustomerBillingProfile](customer-resources.md#customerbillingprofile) wymaganych do utworzenia nowego klienta.</span><span class="sxs-lookup"><span data-stu-id="9e87f-161">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="9e87f-162">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9e87f-162">Name</span></span>             | <span data-ttu-id="9e87f-163">Typ</span><span class="sxs-lookup"><span data-stu-id="9e87f-163">Type</span></span>                                     | <span data-ttu-id="9e87f-164">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9e87f-164">Required</span></span> | <span data-ttu-id="9e87f-165">Opis</span><span class="sxs-lookup"><span data-stu-id="9e87f-165">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9e87f-166">poczta e-mail</span><span class="sxs-lookup"><span data-stu-id="9e87f-166">email</span></span>            | <span data-ttu-id="9e87f-167">ciąg</span><span class="sxs-lookup"><span data-stu-id="9e87f-167">string</span></span>                                   | <span data-ttu-id="9e87f-168">Tak</span><span class="sxs-lookup"><span data-stu-id="9e87f-168">Yes</span></span>      | <span data-ttu-id="9e87f-169">Adres e-mail klienta.</span><span class="sxs-lookup"><span data-stu-id="9e87f-169">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="9e87f-170">kultura</span><span class="sxs-lookup"><span data-stu-id="9e87f-170">culture</span></span>          | <span data-ttu-id="9e87f-171">ciąg</span><span class="sxs-lookup"><span data-stu-id="9e87f-171">string</span></span>                                   | <span data-ttu-id="9e87f-172">Tak</span><span class="sxs-lookup"><span data-stu-id="9e87f-172">Yes</span></span>      | <span data-ttu-id="9e87f-173">Ich preferowana kultura do komunikacji i waluty, na przykład "en-US".</span><span class="sxs-lookup"><span data-stu-id="9e87f-173">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="9e87f-174">Zobacz obsługiwane [Języki w centrum partnerskim i ustawienia regionalne](partner-center-supported-languages-and-locales.md) dla obsługiwanych kultur.</span><span class="sxs-lookup"><span data-stu-id="9e87f-174">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="9e87f-175">language</span><span class="sxs-lookup"><span data-stu-id="9e87f-175">language</span></span>         | <span data-ttu-id="9e87f-176">ciąg</span><span class="sxs-lookup"><span data-stu-id="9e87f-176">string</span></span>                                   | <span data-ttu-id="9e87f-177">Tak</span><span class="sxs-lookup"><span data-stu-id="9e87f-177">Yes</span></span>      | <span data-ttu-id="9e87f-178">Język domyślny.</span><span class="sxs-lookup"><span data-stu-id="9e87f-178">The default language.</span></span> <span data-ttu-id="9e87f-179">Obsługiwane są dwa znaki kodów języka (na przykład `en` lub `fr` ).</span><span class="sxs-lookup"><span data-stu-id="9e87f-179">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="9e87f-180">\_Nazwa firmy</span><span class="sxs-lookup"><span data-stu-id="9e87f-180">company\_name</span></span>    | <span data-ttu-id="9e87f-181">ciąg</span><span class="sxs-lookup"><span data-stu-id="9e87f-181">string</span></span>                                   | <span data-ttu-id="9e87f-182">Tak</span><span class="sxs-lookup"><span data-stu-id="9e87f-182">Yes</span></span>      | <span data-ttu-id="9e87f-183">Nazwa zarejestrowanej firmy/organizacji.</span><span class="sxs-lookup"><span data-stu-id="9e87f-183">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="9e87f-184">domyślny \_ adres</span><span class="sxs-lookup"><span data-stu-id="9e87f-184">default\_address</span></span> | [<span data-ttu-id="9e87f-185">Adres</span><span class="sxs-lookup"><span data-stu-id="9e87f-185">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="9e87f-186">Tak</span><span class="sxs-lookup"><span data-stu-id="9e87f-186">Yes</span></span>      | <span data-ttu-id="9e87f-187">Zarejestrowany adres firmy/organizacji klienta.</span><span class="sxs-lookup"><span data-stu-id="9e87f-187">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="9e87f-188">Zobacz zasób [adresu](utility-resources.md#address) , aby uzyskać informacje o ograniczeniach długości.</span><span class="sxs-lookup"><span data-stu-id="9e87f-188">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="9e87f-189">Profil firmy</span><span class="sxs-lookup"><span data-stu-id="9e87f-189">Company profile</span></span>

<span data-ttu-id="9e87f-190">Ta tabela zawiera opis minimalnych wymaganych pól z zasobów [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) wymaganych do utworzenia nowego klienta.</span><span class="sxs-lookup"><span data-stu-id="9e87f-190">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="9e87f-191">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9e87f-191">Name</span></span>   | <span data-ttu-id="9e87f-192">Typ</span><span class="sxs-lookup"><span data-stu-id="9e87f-192">Type</span></span>   | <span data-ttu-id="9e87f-193">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9e87f-193">Required</span></span> | <span data-ttu-id="9e87f-194">Opis</span><span class="sxs-lookup"><span data-stu-id="9e87f-194">Description</span></span>                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="9e87f-195">domena</span><span class="sxs-lookup"><span data-stu-id="9e87f-195">domain</span></span> | <span data-ttu-id="9e87f-196">ciąg</span><span class="sxs-lookup"><span data-stu-id="9e87f-196">string</span></span> | <span data-ttu-id="9e87f-197">Tak</span><span class="sxs-lookup"><span data-stu-id="9e87f-197">Yes</span></span>     | <span data-ttu-id="9e87f-198">Nazwa domeny klienta, na przykład contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="9e87f-198">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
| <span data-ttu-id="9e87f-199">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="9e87f-199">organizationRegistrationNumber</span></span> | <span data-ttu-id="9e87f-200">ciąg</span><span class="sxs-lookup"><span data-stu-id="9e87f-200">string</span></span> | <span data-ttu-id="9e87f-201">Zależy od warunku</span><span class="sxs-lookup"><span data-stu-id="9e87f-201">Depends on condition</span></span> | <span data-ttu-id="9e87f-202">Numer rejestracji organizacji klienta (określany również jako numer INN w niektórych krajach).</span><span class="sxs-lookup"><span data-stu-id="9e87f-202">The customer’s organization registration number (also referred to as the INN number in certain countries).</span></span> <br/><br/><span data-ttu-id="9e87f-203">Wypełnienie tego pola jest wymagane tylko wtedy, gdy firma lub organizacja klienta znajduje się w następujących krajach:</span><span class="sxs-lookup"><span data-stu-id="9e87f-203">Completing this field is required only if a customer’s company/organization is located in the following countries:</span></span> <br/><br/><span data-ttu-id="9e87f-204">-Armenia (AM)</span><span class="sxs-lookup"><span data-stu-id="9e87f-204">- Armenia (AM)</span></span> <br/><span data-ttu-id="9e87f-205">-Azerbejdżan (AZ)</span><span class="sxs-lookup"><span data-stu-id="9e87f-205">- Azerbaijan (AZ)</span></span><br/><span data-ttu-id="9e87f-206">-Białoruś (przez)</span><span class="sxs-lookup"><span data-stu-id="9e87f-206">- Belarus (BY)</span></span><br/><span data-ttu-id="9e87f-207">-Węgry (HU)</span><span class="sxs-lookup"><span data-stu-id="9e87f-207">- Hungary (HU)</span></span><br/><span data-ttu-id="9e87f-208">-Kazachstan (KZ)</span><span class="sxs-lookup"><span data-stu-id="9e87f-208">- Kazakhstan (KZ)</span></span><br/><span data-ttu-id="9e87f-209">-Kirgistan (KG)</span><span class="sxs-lookup"><span data-stu-id="9e87f-209">- Kyrgyzstan (KG)</span></span><br/><span data-ttu-id="9e87f-210">— Mołdawia (MD)</span><span class="sxs-lookup"><span data-stu-id="9e87f-210">- Moldova (MD)</span></span><br/><span data-ttu-id="9e87f-211">— Rosja (RU)</span><span class="sxs-lookup"><span data-stu-id="9e87f-211">- Russia (RU)</span></span><br/><span data-ttu-id="9e87f-212">-Tadżykistan (TJ)</span><span class="sxs-lookup"><span data-stu-id="9e87f-212">- Tajikistan (TJ)</span></span><br/><span data-ttu-id="9e87f-213">-Uzbekistan (UZ)</span><span class="sxs-lookup"><span data-stu-id="9e87f-213">- Uzbekistan (UZ)</span></span><br/><span data-ttu-id="9e87f-214">-Ukraina (UA)</span><span class="sxs-lookup"><span data-stu-id="9e87f-214">- Ukraine (UA)</span></span><br/><br/><span data-ttu-id="9e87f-215">To pole nie jest wymagane, jeśli firma/organizacja klienta znajduje się w innych krajach poza tymi przedstawionymi tutaj.</span><span class="sxs-lookup"><span data-stu-id="9e87f-215">This field is not required if the customer’s company/organization is located in other countries beyond those shown here.</span></span>  |

### <a name="request-example"></a><span data-ttu-id="9e87f-216">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="9e87f-216">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="9e87f-217">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="9e87f-217">REST response</span></span>

<span data-ttu-id="9e87f-218">Jeśli to się powiedzie, odpowiedź zawiera zasób [klienta](customer-resources.md#customer) dla nowego klienta.</span><span class="sxs-lookup"><span data-stu-id="9e87f-218">If successful, the response contains a [Customer](customer-resources.md#customer) resource for the new customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9e87f-219">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9e87f-219">Response success and error codes</span></span>

<span data-ttu-id="9e87f-220">Odpowiedzi są uzyskiwane przy użyciu kodu stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="9e87f-220">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9e87f-221">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="9e87f-221">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9e87f-222">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9e87f-222">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9e87f-223">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9e87f-223">Response example</span></span>

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