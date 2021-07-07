---
title: Tworzenie klienta dla odsprzedawcy pośredniego
description: Dowiedz się, jak dostawca pośredni może używać Partner Center API do tworzenia klienta dla odsprzedawcy pośredniego.
ms.date: 04/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 9a6218aeb61f3775c89d34b4d57a17741e3a1e93
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973744"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a><span data-ttu-id="fc8bd-103">Tworzenie klienta dla odsprzedawcy pośredniego przy użyciu Partner Center API</span><span class="sxs-lookup"><span data-stu-id="fc8bd-103">Create a customer for an indirect reseller using Partner Center APIs</span></span>

<span data-ttu-id="fc8bd-104">Dostawca pośredni może utworzyć klienta dla odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-104">An indirect provider can create a customer for an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc8bd-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fc8bd-105">Prerequisites</span></span>

- <span data-ttu-id="fc8bd-106">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="fc8bd-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fc8bd-107">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="fc8bd-108">Identyfikator dzierżawy odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-108">The tenant identifier of the indirect reseller.</span></span>

- <span data-ttu-id="fc8bd-109">Odsprzedawca pośredni musi mieć partnerstwo z dostawcą pośrednim.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-109">The indirect reseller must have a partnership with the indirect provider.</span></span>

## <a name="c"></a><span data-ttu-id="fc8bd-110">C\#</span><span class="sxs-lookup"><span data-stu-id="fc8bd-110">C\#</span></span>

<span data-ttu-id="fc8bd-111">Aby dodać nowego klienta dla odsprzedawcy pośredniego:</span><span class="sxs-lookup"><span data-stu-id="fc8bd-111">To add a new customer for an indirect reseller:</span></span>

1. <span data-ttu-id="fc8bd-112">Za pomocą wystąpienia nowego [**obiektu Klient**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) należy utworzyć jego wystąpienia, a następnie wypełnić pola [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) i [**CompanyProfile.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)</span><span class="sxs-lookup"><span data-stu-id="fc8bd-112">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object and then instantiate and populate the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span> <span data-ttu-id="fc8bd-113">Pamiętaj, aby przypisać identyfikator odsprzedawcy pośredniego do właściwości [**AssociatedPartnerID.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid)</span><span class="sxs-lookup"><span data-stu-id="fc8bd-113">Be sure to assign the indirect reseller ID to the [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) property.</span></span>

2. <span data-ttu-id="fc8bd-114">Użyj właściwości [**IAggregatePartner.Customers,**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) aby uzyskać interfejs do operacji zbierania danych klientów.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-114">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) property to get an interface to customer collection operations.</span></span>

3. <span data-ttu-id="fc8bd-115">Wywołaj [**metodę Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) lub [**CreateAsync,**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) aby utworzyć klienta.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-115">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the customer.</span></span>

### <a name="c-example"></a><span data-ttu-id="fc8bd-116">Przykład w \# języku C</span><span class="sxs-lookup"><span data-stu-id="fc8bd-116">C\# example</span></span>

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

<span data-ttu-id="fc8bd-117">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="fc8bd-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="fc8bd-118">**Project**: zestaw SDK Centrum partnerskiego Samples **Class**: CreateCustomerforIndirectReseller.cs</span><span class="sxs-lookup"><span data-stu-id="fc8bd-118">**Project**: Partner Center SDK Samples **Class**: CreateCustomerforIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="fc8bd-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="fc8bd-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fc8bd-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="fc8bd-120">Request syntax</span></span>

| <span data-ttu-id="fc8bd-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="fc8bd-121">Method</span></span>   | <span data-ttu-id="fc8bd-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="fc8bd-122">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="fc8bd-123">**Post**</span><span class="sxs-lookup"><span data-stu-id="fc8bd-123">**POST**</span></span> | <span data-ttu-id="fc8bd-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fc8bd-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fc8bd-125">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="fc8bd-125">Request headers</span></span>

<span data-ttu-id="fc8bd-126">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="fc8bd-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fc8bd-127">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="fc8bd-127">Request body</span></span>

<span data-ttu-id="fc8bd-128">W tej tabeli opisano wymagane właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-128">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="fc8bd-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fc8bd-129">Name</span></span>                                          | <span data-ttu-id="fc8bd-130">Typ</span><span class="sxs-lookup"><span data-stu-id="fc8bd-130">Type</span></span>   | <span data-ttu-id="fc8bd-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fc8bd-131">Required</span></span> | <span data-ttu-id="fc8bd-132">Opis</span><span class="sxs-lookup"><span data-stu-id="fc8bd-132">Description</span></span>                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="fc8bd-133">BillingProfile</span><span class="sxs-lookup"><span data-stu-id="fc8bd-133">BillingProfile</span></span>](#billing-profile)             | <span data-ttu-id="fc8bd-134">object</span><span class="sxs-lookup"><span data-stu-id="fc8bd-134">object</span></span> | <span data-ttu-id="fc8bd-135">Tak</span><span class="sxs-lookup"><span data-stu-id="fc8bd-135">Yes</span></span>      | <span data-ttu-id="fc8bd-136">Informacje o profilu rozliczeniowym klienta.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-136">The customer's billing profile information.</span></span>                                                                                                                                                                                                                                                                                                           |
| [<span data-ttu-id="fc8bd-137">CompanyProfile</span><span class="sxs-lookup"><span data-stu-id="fc8bd-137">CompanyProfile</span></span>](#company-profile)             | <span data-ttu-id="fc8bd-138">object</span><span class="sxs-lookup"><span data-stu-id="fc8bd-138">object</span></span> | <span data-ttu-id="fc8bd-139">Tak</span><span class="sxs-lookup"><span data-stu-id="fc8bd-139">Yes</span></span>      | <span data-ttu-id="fc8bd-140">Informacje o profilu firmy klienta.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-140">The customer's company profile information.</span></span>                                                               
| [<span data-ttu-id="fc8bd-141">AssociatedPartnerId</span><span class="sxs-lookup"><span data-stu-id="fc8bd-141">AssociatedPartnerId</span></span>](customer-resources.md#customer) | <span data-ttu-id="fc8bd-142">ciąg</span><span class="sxs-lookup"><span data-stu-id="fc8bd-142">string</span></span> | <span data-ttu-id="fc8bd-143">Tak</span><span class="sxs-lookup"><span data-stu-id="fc8bd-143">Yes</span></span>      | <span data-ttu-id="fc8bd-144">Identyfikator odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-144">The indirect reseller ID.</span></span> <span data-ttu-id="fc8bd-145">Odsprzedawca pośredni wskazany za pomocą identyfikatora podanego w tym miejscu musi mieć partnerstwo z dostawcą pośrednim, w przypadku gdy żądanie nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-145">The indirect reseller as indicated by the ID supplied here must have a partnership with the indirect provider or the request will fail.</span></span> <span data-ttu-id="fc8bd-146">Należy również zauważyć, że jeśli wartość AssociatedPartnerId nie zostanie dostarczona, klient jest tworzony jako bezpośredni klient dostawcy pośredniego, a nie odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-146">Also note that if the AssociatedPartnerId value isn't supplied, the customer is created as a direct customer of the indirect provider rather than the indirect reseller.</span></span> |
|<span data-ttu-id="fc8bd-147">Domena</span><span class="sxs-lookup"><span data-stu-id="fc8bd-147">Domain</span></span>| <span data-ttu-id="fc8bd-148">Ciąg</span><span class="sxs-lookup"><span data-stu-id="fc8bd-148">String</span></span>| <span data-ttu-id="fc8bd-149">Tak</span><span class="sxs-lookup"><span data-stu-id="fc8bd-149">Yes</span></span>|<span data-ttu-id="fc8bd-150">Nazwa domeny klienta, na przykład contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-150">The customer's domain name, such as contoso.onmicrosoft.com.</span></span>|
|<span data-ttu-id="fc8bd-151">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="fc8bd-151">organizationRegistrationNumber</span></span>|    <span data-ttu-id="fc8bd-152">ciąg</span><span class="sxs-lookup"><span data-stu-id="fc8bd-152">string</span></span>|<span data-ttu-id="fc8bd-153">Tak</span><span class="sxs-lookup"><span data-stu-id="fc8bd-153">Yes</span></span>|     <span data-ttu-id="fc8bd-154">Numer rejestracji organizacji klienta (w niektórych krajach określany również jako numer NUMER TELEFONU).</span><span class="sxs-lookup"><span data-stu-id="fc8bd-154">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="fc8bd-155">Wymagana tylko w przypadku firmy/organizacji klienta znajdującej się w następujących krajach: Zamówienie (AM), Kolumbia (AZ), Kolumbia (HU), KZ), Kyrgyzstan(KG), Azja (MD), Korea (RU), Tajikistan(TJ), Przemysl(UZ), Indie, Brazylia, Republika Południowej Afryki,Portal, Zjednoczone Królestwo, Arabia, Przećwicz, Wietnam, Anwil, Przemysl, Południowe Niemówiące i Ankai.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-155">Only required for customer’s company/organization located in the following countries: Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA), India, Brazil, South Africa, Poland, United Arab Emirates, Saudi Arabia, Turkey, Thailand, Vietnam, Myanmar, Iraq, South Sudan, and Venezuela.</span></span> <span data-ttu-id="fc8bd-156">W przypadku firmy/organizacji klienta znajdującej się w innych krajach jest to pole opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-156">For customer’s company/organization located in other countries this is an optional field.</span></span>|



#### <a name="billing-profile"></a><span data-ttu-id="fc8bd-157">Profil rozliczeniowy</span><span class="sxs-lookup"><span data-stu-id="fc8bd-157">Billing profile</span></span>

<span data-ttu-id="fc8bd-158">W tej tabeli opisano minimalne wymagane pola z zasobu [CustomerBillingProfile](customer-resources.md#customerbillingprofile) potrzebne do utworzenia nowego klienta.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-158">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="fc8bd-159">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fc8bd-159">Name</span></span>             | <span data-ttu-id="fc8bd-160">Typ</span><span class="sxs-lookup"><span data-stu-id="fc8bd-160">Type</span></span>                                     | <span data-ttu-id="fc8bd-161">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fc8bd-161">Required</span></span> | <span data-ttu-id="fc8bd-162">Opis</span><span class="sxs-lookup"><span data-stu-id="fc8bd-162">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fc8bd-163">poczta e-mail</span><span class="sxs-lookup"><span data-stu-id="fc8bd-163">email</span></span>            | <span data-ttu-id="fc8bd-164">ciąg</span><span class="sxs-lookup"><span data-stu-id="fc8bd-164">string</span></span>                                   | <span data-ttu-id="fc8bd-165">Tak</span><span class="sxs-lookup"><span data-stu-id="fc8bd-165">Yes</span></span>      | <span data-ttu-id="fc8bd-166">Adres e-mail klienta.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-166">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="fc8bd-167">kultura</span><span class="sxs-lookup"><span data-stu-id="fc8bd-167">culture</span></span>          | <span data-ttu-id="fc8bd-168">ciąg</span><span class="sxs-lookup"><span data-stu-id="fc8bd-168">string</span></span>                                   | <span data-ttu-id="fc8bd-169">Tak</span><span class="sxs-lookup"><span data-stu-id="fc8bd-169">Yes</span></span>      | <span data-ttu-id="fc8bd-170">Preferowana kultura komunikacji i waluty, na przykład "en-US".</span><span class="sxs-lookup"><span data-stu-id="fc8bd-170">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="fc8bd-171">Zobacz [Partner Center obsługiwanych języków i lokalizacji regionalnych](partner-center-supported-languages-and-locales.md) dla obsługiwanych kultur.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-171">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="fc8bd-172">language</span><span class="sxs-lookup"><span data-stu-id="fc8bd-172">language</span></span>         | <span data-ttu-id="fc8bd-173">ciąg</span><span class="sxs-lookup"><span data-stu-id="fc8bd-173">string</span></span>                                   | <span data-ttu-id="fc8bd-174">Tak</span><span class="sxs-lookup"><span data-stu-id="fc8bd-174">Yes</span></span>      | <span data-ttu-id="fc8bd-175">Język domyślny.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-175">The default language.</span></span> <span data-ttu-id="fc8bd-176">Obsługiwane są dwa kody języków znaków (na `en` przykład lub `fr` ).</span><span class="sxs-lookup"><span data-stu-id="fc8bd-176">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="fc8bd-177">nazwa \_ firmy</span><span class="sxs-lookup"><span data-stu-id="fc8bd-177">company\_name</span></span>    | <span data-ttu-id="fc8bd-178">ciąg</span><span class="sxs-lookup"><span data-stu-id="fc8bd-178">string</span></span>                                   | <span data-ttu-id="fc8bd-179">Tak</span><span class="sxs-lookup"><span data-stu-id="fc8bd-179">Yes</span></span>      | <span data-ttu-id="fc8bd-180">Nazwa zarejestrowanej firmy/organizacji.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-180">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="fc8bd-181">adres \_ domyślny</span><span class="sxs-lookup"><span data-stu-id="fc8bd-181">default\_address</span></span> | [<span data-ttu-id="fc8bd-182">Adres</span><span class="sxs-lookup"><span data-stu-id="fc8bd-182">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="fc8bd-183">Tak</span><span class="sxs-lookup"><span data-stu-id="fc8bd-183">Yes</span></span>      | <span data-ttu-id="fc8bd-184">Zarejestrowany adres firmy/organizacji klienta.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-184">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="fc8bd-185">Zapoznaj się z [zasobem](utility-resources.md#address) Adres, aby uzyskać informacje o wszelkich ograniczeniach długości.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-185">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="fc8bd-186">Profil firmy</span><span class="sxs-lookup"><span data-stu-id="fc8bd-186">Company profile</span></span>

<span data-ttu-id="fc8bd-187">W tej tabeli opisano minimalne wymagane pola z zasobu [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) wymagane do utworzenia nowego klienta.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-187">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="fc8bd-188">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fc8bd-188">Name</span></span>   | <span data-ttu-id="fc8bd-189">Typ</span><span class="sxs-lookup"><span data-stu-id="fc8bd-189">Type</span></span>   | <span data-ttu-id="fc8bd-190">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fc8bd-190">Required</span></span> | <span data-ttu-id="fc8bd-191">Opis</span><span class="sxs-lookup"><span data-stu-id="fc8bd-191">Description</span></span>                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="fc8bd-192">domena</span><span class="sxs-lookup"><span data-stu-id="fc8bd-192">domain</span></span> | <span data-ttu-id="fc8bd-193">ciąg</span><span class="sxs-lookup"><span data-stu-id="fc8bd-193">string</span></span> | <span data-ttu-id="fc8bd-194">Tak</span><span class="sxs-lookup"><span data-stu-id="fc8bd-194">Yes</span></span>     | <span data-ttu-id="fc8bd-195">Nazwa domeny klienta, na przykład contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-195">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
| <span data-ttu-id="fc8bd-196">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="fc8bd-196">organizationRegistrationNumber</span></span> | <span data-ttu-id="fc8bd-197">ciąg</span><span class="sxs-lookup"><span data-stu-id="fc8bd-197">string</span></span> | <span data-ttu-id="fc8bd-198">Zależy od warunku</span><span class="sxs-lookup"><span data-stu-id="fc8bd-198">Depends on condition</span></span> | <span data-ttu-id="fc8bd-199">Numer rejestracji organizacji klienta (określany również jako numer IDENTYFIKACYJNY w niektórych krajach).</span><span class="sxs-lookup"><span data-stu-id="fc8bd-199">The customer’s organization registration number (also referred to as the INN number in certain countries).</span></span> <br/><br/><span data-ttu-id="fc8bd-200">Ukończenie tego pola jest wymagane tylko wtedy, gdy firma/organizacja klienta znajduje się w następujących krajach:</span><span class="sxs-lookup"><span data-stu-id="fc8bd-200">Completing this field is required only if a customer’s company/organization is located in the following countries:</span></span> <br/><br/><span data-ttu-id="fc8bd-201">— Zamów (AM)</span><span class="sxs-lookup"><span data-stu-id="fc8bd-201">- Armenia (AM)</span></span> <br/><span data-ttu-id="fc8bd-202">— Zakłotek (AZ)</span><span class="sxs-lookup"><span data-stu-id="fc8bd-202">- Azerbaijan (AZ)</span></span><br/><span data-ttu-id="fc8bd-203">- Wniesienie (BY)</span><span class="sxs-lookup"><span data-stu-id="fc8bd-203">- Belarus (BY)</span></span><br/><span data-ttu-id="fc8bd-204">- Wschowa (HU)</span><span class="sxs-lookup"><span data-stu-id="fc8bd-204">- Hungary (HU)</span></span><br/><span data-ttu-id="fc8bd-205">- Wz (KZ)</span><span class="sxs-lookup"><span data-stu-id="fc8bd-205">- Kazakhstan (KZ)</span></span><br/><span data-ttu-id="fc8bd-206">— Kyrgyzstan (KG)</span><span class="sxs-lookup"><span data-stu-id="fc8bd-206">- Kyrgyzstan (KG)</span></span><br/><span data-ttu-id="fc8bd-207">— Zamów (MD)</span><span class="sxs-lookup"><span data-stu-id="fc8bd-207">- Moldova (MD)</span></span><br/><span data-ttu-id="fc8bd-208">- Rosyjski (RU)</span><span class="sxs-lookup"><span data-stu-id="fc8bd-208">- Russia (RU)</span></span><br/><span data-ttu-id="fc8bd-209">- Tadżykistan (TJ)</span><span class="sxs-lookup"><span data-stu-id="fc8bd-209">- Tajikistan (TJ)</span></span><br/><span data-ttu-id="fc8bd-210">- Zdjęcie (UZ)</span><span class="sxs-lookup"><span data-stu-id="fc8bd-210">- Uzbekistan (UZ)</span></span><br/><span data-ttu-id="fc8bd-211">- Waze (UA)</span><span class="sxs-lookup"><span data-stu-id="fc8bd-211">- Ukraine (UA)</span></span><br/><span data-ttu-id="fc8bd-212">— Indie</span><span class="sxs-lookup"><span data-stu-id="fc8bd-212">- India</span></span> <br/><span data-ttu-id="fc8bd-213">- Brazylia</span><span class="sxs-lookup"><span data-stu-id="fc8bd-213">- Brazil</span></span> <br/><span data-ttu-id="fc8bd-214">— Republika Południowej Afryki</span><span class="sxs-lookup"><span data-stu-id="fc8bd-214">- South Africa</span></span> <br/><span data-ttu-id="fc8bd-215">— Zięć</span><span class="sxs-lookup"><span data-stu-id="fc8bd-215">- Poland</span></span> <br/><span data-ttu-id="fc8bd-216">— Zjednoczone Królestwo</span><span class="sxs-lookup"><span data-stu-id="fc8bd-216">- United Arab Emirates</span></span> <br/><span data-ttu-id="fc8bd-217">— Arabia Saudyjska</span><span class="sxs-lookup"><span data-stu-id="fc8bd-217">- Saudi Arabia</span></span> <br/><span data-ttu-id="fc8bd-218">- W tym celu</span><span class="sxs-lookup"><span data-stu-id="fc8bd-218">- Turkey</span></span> <br/><span data-ttu-id="fc8bd-219">- Zięć</span><span class="sxs-lookup"><span data-stu-id="fc8bd-219">- Thailand</span></span> <br/><span data-ttu-id="fc8bd-220">- Wietnam</span><span class="sxs-lookup"><span data-stu-id="fc8bd-220">- Vietnam</span></span> <br/><span data-ttu-id="fc8bd-221">- Zięć</span><span class="sxs-lookup"><span data-stu-id="fc8bd-221">- Myanmar</span></span> <br/><span data-ttu-id="fc8bd-222">- Wzgorę</span><span class="sxs-lookup"><span data-stu-id="fc8bd-222">- Iraq</span></span> <br/><span data-ttu-id="fc8bd-223">- Południowy Dobszczyń</span><span class="sxs-lookup"><span data-stu-id="fc8bd-223">- South Sudan</span></span> <br/><span data-ttu-id="fc8bd-224">- Wzgorę</span><span class="sxs-lookup"><span data-stu-id="fc8bd-224">- Venezuela</span></span><br/> <br/><span data-ttu-id="fc8bd-225">W przypadku firmy/organizacji klienta znajdującej się w innych krajach jest to pole opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-225">For customer’s company/organization located in other countries, this is an optional field.</span></span>  |

### <a name="request-example"></a><span data-ttu-id="fc8bd-226">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="fc8bd-226">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="fc8bd-227">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="fc8bd-227">REST response</span></span>

<span data-ttu-id="fc8bd-228">W przypadku powodzenia odpowiedź zawiera [zasób Klient](customer-resources.md#customer) dla nowego klienta.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-228">If successful, the response contains a [Customer](customer-resources.md#customer) resource for the new customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fc8bd-229">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fc8bd-229">Response success and error codes</span></span>

<span data-ttu-id="fc8bd-230">Odpowiedzi zawierają kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-230">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fc8bd-231">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="fc8bd-231">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fc8bd-232">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="fc8bd-232">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fc8bd-233">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fc8bd-233">Response example</span></span>

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