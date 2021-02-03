---
title: Tworzenie klienta
description: Dowiedz się, w jaki sposób partner dostawcy rozwiązań w chmurze (CSP) może używać interfejsów API Centrum partnerskiego do tworzenia nowego klienta. Artykuł zawiera opis wymagań wstępnych i innych sytuacji.
ms.date: 11/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 3bc8081c682bdf522bcb0ca218f16cafab7b3a99
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "97770228"
---
# <a name="create-a-customer-using-partner-center-apis"></a><span data-ttu-id="cf614-104">Tworzenie klienta przy użyciu interfejsów API Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="cf614-104">Create a customer using Partner Center APIs</span></span>

<span data-ttu-id="cf614-105">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="cf614-105">**Applies to:**</span></span>

- <span data-ttu-id="cf614-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="cf614-106">Partner Center</span></span>
- <span data-ttu-id="cf614-107">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="cf614-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="cf614-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="cf614-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="cf614-109">W tym artykule wyjaśniono, jak utworzyć nowego klienta.</span><span class="sxs-lookup"><span data-stu-id="cf614-109">This article explains how to create a new customer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cf614-110">Jeśli jesteś dostawcą pośrednim i chcesz utworzyć klienta dla pośredniego odsprzedawcy, zobacz temat [Tworzenie klienta dla pośredniego odsprzedawcy](create-a-customer-for-an-indirect-reseller.md).</span><span class="sxs-lookup"><span data-stu-id="cf614-110">If you are an indirect provider and you want to create a customer for an indirect reseller, please see [Create a customer for an indirect reseller](create-a-customer-for-an-indirect-reseller.md).</span></span>

<span data-ttu-id="cf614-111">Jako partner dostawcy rozwiązań w chmurze (CSP), podczas tworzenia klienta możesz umieścić zamówienia w imieniu klienta.</span><span class="sxs-lookup"><span data-stu-id="cf614-111">As a cloud solution provider (CSP) partner, when you create a customer you can place orders on behalf of the customer.</span></span> <span data-ttu-id="cf614-112">Podczas tworzenia klienta należy również utworzyć następujące:</span><span class="sxs-lookup"><span data-stu-id="cf614-112">When you create a customer, you also create:</span></span>

- <span data-ttu-id="cf614-113">Obiekt dzierżawy Azure Active Directory (AD) dla klienta.</span><span class="sxs-lookup"><span data-stu-id="cf614-113">An Azure Active Directory (AD) tenant object for the customer.</span></span>

- <span data-ttu-id="cf614-114">Relacja między odsprzedawcą a klientem używanym do delegowania uprawnień administratora.</span><span class="sxs-lookup"><span data-stu-id="cf614-114">A relationship between the reseller and customer, used for delegated admin privileges.</span></span>

- <span data-ttu-id="cf614-115">Nazwa użytkownika i hasło, aby zalogować się jako administrator dla klienta.</span><span class="sxs-lookup"><span data-stu-id="cf614-115">A user name and password to sign in as an admin for the customer.</span></span>

<span data-ttu-id="cf614-116">Po utworzeniu klienta Pamiętaj, aby zapisać informacje o IDENTYFIKATORze klienta i usłudze Azure AD do użycia w przyszłości z zestawem SDK Centrum partnerskiego (na przykład zarządzanie kontami).</span><span class="sxs-lookup"><span data-stu-id="cf614-116">Once the customer is created, be sure to save the customer ID and Azure AD details for future use with the Partner Center SDK (for example, account management).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf614-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cf614-117">Prerequisites</span></span>

- <span data-ttu-id="cf614-118">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cf614-118">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cf614-119">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cf614-119">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cf614-120">Aby utworzyć dzierżawę klienta, należy podać prawidłowy adres fizyczny podczas procesu tworzenia.</span><span class="sxs-lookup"><span data-stu-id="cf614-120">To create a customer tenant you must provide a valid physical address during the creation process.</span></span> <span data-ttu-id="cf614-121">Adres można zweryfikować, wykonując czynności opisane w scenariuszu [Weryfikuj adres](validate-an-address.md) .</span><span class="sxs-lookup"><span data-stu-id="cf614-121">An address can be validated by following the steps outlined in the [Validate an address](validate-an-address.md) scenario.</span></span> <span data-ttu-id="cf614-122">Jeśli klient zostanie utworzony przy użyciu nieprawidłowego adresu w środowisku piaskownicy, nie będzie można usunąć tej dzierżawy klienta.</span><span class="sxs-lookup"><span data-stu-id="cf614-122">If you create a customer using an invalid address in the sandbox environment, you will not be able to delete that customer tenant.</span></span>

## <a name="c"></a><span data-ttu-id="cf614-123">C\#</span><span class="sxs-lookup"><span data-stu-id="cf614-123">C\#</span></span>

<span data-ttu-id="cf614-124">Aby dodać klienta:</span><span class="sxs-lookup"><span data-stu-id="cf614-124">To add a customer:</span></span>

1. <span data-ttu-id="cf614-125">Tworzenie wystąpienia nowego obiektu [**klienta**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) .</span><span class="sxs-lookup"><span data-stu-id="cf614-125">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object.</span></span> <span data-ttu-id="cf614-126">Upewnij się, że [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) i [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span><span class="sxs-lookup"><span data-stu-id="cf614-126">Be sure to fill in the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span>

2. <span data-ttu-id="cf614-127">Dodaj nowego klienta do kolekcji [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , wywołując metodę [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) lub [**Async**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).</span><span class="sxs-lookup"><span data-stu-id="cf614-127">Add the new customer to your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection by calling [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).</span></span>

### <a name="c-example"></a><span data-ttu-id="cf614-128">\#Przykład C</span><span class="sxs-lookup"><span data-stu-id="cf614-128">C\# example</span></span>

```csharp
// IAggregatePartner partnerOperations;

var partnerOperations = this.Context.UserPartnerOperations;

var customerToCreate = new Customer()
{
    CompanyProfile = new CustomerCompanyProfile()
    {
        Domain = string.Format(CultureInfo.InvariantCulture,
            "SampleApplication{0}.{1}",
            new Random().Next(),
            this.Context.Configuration.Scenario.CustomerDomainSuffix),
        //// OrganizationRegistrationNumber = "123456" // Please add if in specific country that requires
    },
    BillingProfile = new CustomerBillingProfile()
    {
        Culture = "EN-US",
        Email = "someone@example.com",
        Language = "En",
        CompanyName = "Some Company" + new Random().Next(),
        DefaultAddress = new Address()
        {
            FirstName = "Tania",
            MiddleName = "MiddleName",
            LastName = "Carr",
            AddressLine1 = "One Microsoft Way",
            City = "Redmond",
            State = "WA",
            Country = "US",
            PostalCode = "98052",
            PhoneNumber = ""
        }
    }
};

var newCustomer = partnerOperations.Customers.Create(customerToCreate);
```

<span data-ttu-id="cf614-129">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="cf614-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="cf614-130">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: CreateCustomer.cs</span><span class="sxs-lookup"><span data-stu-id="cf614-130">**Project**: Partner Center SDK Samples **Class**: CreateCustomer.cs</span></span>

## <a name="java"></a><span data-ttu-id="cf614-131">Java</span><span class="sxs-lookup"><span data-stu-id="cf614-131">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="cf614-132">Aby utworzyć nowego klienta:</span><span class="sxs-lookup"><span data-stu-id="cf614-132">To create a new customer:</span></span>

1. <span data-ttu-id="cf614-133">Utwórz nowe wystąpienie **CustomerBillingProfile** i obiektów **CustomerCompanyProfile** .</span><span class="sxs-lookup"><span data-stu-id="cf614-133">Create a new instance of the **CustomerBillingProfile** and the **CustomerCompanyProfile** objects.</span></span> <span data-ttu-id="cf614-134">Pamiętaj, aby wypełnić wymagane pola.</span><span class="sxs-lookup"><span data-stu-id="cf614-134">Be sure to populate the required fields.</span></span>

2. <span data-ttu-id="cf614-135">Utwórz klienta, wywołując funkcję **IAggregatePartner. GetCustomers (). Create** .</span><span class="sxs-lookup"><span data-stu-id="cf614-135">Create the customer by calling the **IAggregatePartner.getCustomers().create** function.</span></span>

### <a name="java-example"></a><span data-ttu-id="cf614-136">Przykład Java</span><span class="sxs-lookup"><span data-stu-id="cf614-136">Java example</span></span>

```java
// IAggregatePartner partnerOperations;

Address address = new Address();

address.setFirstName( "Gena" );
address.setLastName( "Soto" );
address.setAddressLine1( "One Microsoft Way" );
address.setCity( "Redmond" );
address.setState( "WA" );
address.setCountry( "US" );
address.setPostalCode( "98052" );
address.setPhoneNumber( "4255550101" );

CustomerBillingProfile billingProfile = new CustomerBillingProfile();

billingProfile.setCulture( "en-US" );
billingProfile.setEmail( "gena@wingtiptoys.com" );
billingProfile.setLanguage( "en" );
billingProfile.setCompanyName( "Wingtip Toys" + new Random().nextInt() );
billingProfile.setDefaultAddress( address );

CustomerCompanyProfile companyProfile = new CustomerCompanyProfile();

companyProfile.setDomain( "WingtipToys" + Math.abs( new Random().nextInt() ) + ".onmicrosoft.com" );

Customer customerToCreate = new Customer();

customerToCreate.setBillingProfile( billingProfile );
customerToCreate.setCompanyProfile( companyProfile );

Customer newCustomer = partnerOperations.getCustomers().create( customerToCreate );
```

## <a name="powershell"></a><span data-ttu-id="cf614-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf614-137">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="cf614-138">Aby utworzyć klienta, uruchom polecenie [**New-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) .</span><span class="sxs-lookup"><span data-stu-id="cf614-138">To create a customer execute the [**New-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) command.</span></span>

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <a name="rest-request"></a><span data-ttu-id="cf614-139">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="cf614-139">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cf614-140">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="cf614-140">Request syntax</span></span>

| <span data-ttu-id="cf614-141">Metoda</span><span class="sxs-lookup"><span data-stu-id="cf614-141">Method</span></span>   | <span data-ttu-id="cf614-142">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="cf614-142">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="cf614-143">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="cf614-143">**POST**</span></span> | <span data-ttu-id="cf614-144">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers http/1.1</span><span class="sxs-lookup"><span data-stu-id="cf614-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="cf614-145">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="cf614-145">Request headers</span></span>

- <span data-ttu-id="cf614-146">Ten interfejs API to idempotentne (w przypadku wywołania go wielokrotnie) nie zostanie wyznaczony inny wynik.</span><span class="sxs-lookup"><span data-stu-id="cf614-146">This API is idempotent (it will not yield a different result if you call it multiple times).</span></span>

- <span data-ttu-id="cf614-147">Identyfikator żądania i identyfikator korelacji są wymagane.</span><span class="sxs-lookup"><span data-stu-id="cf614-147">A request ID and correlation ID are required.</span></span>

- <span data-ttu-id="cf614-148">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="cf614-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cf614-149">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="cf614-149">Request body</span></span>

<span data-ttu-id="cf614-150">W tej tabeli opisano wymagane właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="cf614-150">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="cf614-151">Nazwa</span><span class="sxs-lookup"><span data-stu-id="cf614-151">Name</span></span>                              | <span data-ttu-id="cf614-152">Typ</span><span class="sxs-lookup"><span data-stu-id="cf614-152">Type</span></span>   | <span data-ttu-id="cf614-153">Opis</span><span class="sxs-lookup"><span data-stu-id="cf614-153">Description</span></span>                                 |
|-----------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="cf614-154">BillingProfile</span><span class="sxs-lookup"><span data-stu-id="cf614-154">BillingProfile</span></span>](#billing-profile) | <span data-ttu-id="cf614-155">object</span><span class="sxs-lookup"><span data-stu-id="cf614-155">object</span></span> | <span data-ttu-id="cf614-156">Informacje o profilu rozliczania klienta.</span><span class="sxs-lookup"><span data-stu-id="cf614-156">The customer's billing profile information.</span></span> |
| [<span data-ttu-id="cf614-157">CompanyProfile</span><span class="sxs-lookup"><span data-stu-id="cf614-157">CompanyProfile</span></span>](#company-profile) | <span data-ttu-id="cf614-158">object</span><span class="sxs-lookup"><span data-stu-id="cf614-158">object</span></span> | <span data-ttu-id="cf614-159">Informacje o profilu firmy klienta.</span><span class="sxs-lookup"><span data-stu-id="cf614-159">The customer's company profile information.</span></span> |

#### <a name="billing-profile"></a><span data-ttu-id="cf614-160">Profil rozliczeniowy</span><span class="sxs-lookup"><span data-stu-id="cf614-160">Billing profile</span></span>

<span data-ttu-id="cf614-161">Ta tabela zawiera opis minimalnych wymaganych pól z zasobów [CustomerBillingProfile](customer-resources.md#customerbillingprofile) wymaganych do utworzenia nowego klienta.</span><span class="sxs-lookup"><span data-stu-id="cf614-161">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="cf614-162">Nazwa</span><span class="sxs-lookup"><span data-stu-id="cf614-162">Name</span></span>             | <span data-ttu-id="cf614-163">Typ</span><span class="sxs-lookup"><span data-stu-id="cf614-163">Type</span></span>                                     | <span data-ttu-id="cf614-164">Opis</span><span class="sxs-lookup"><span data-stu-id="cf614-164">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cf614-165">poczta e-mail</span><span class="sxs-lookup"><span data-stu-id="cf614-165">email</span></span>            | <span data-ttu-id="cf614-166">ciąg</span><span class="sxs-lookup"><span data-stu-id="cf614-166">string</span></span>                                   | <span data-ttu-id="cf614-167">Adres e-mail klienta.</span><span class="sxs-lookup"><span data-stu-id="cf614-167">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="cf614-168">kultura</span><span class="sxs-lookup"><span data-stu-id="cf614-168">culture</span></span>          | <span data-ttu-id="cf614-169">ciąg</span><span class="sxs-lookup"><span data-stu-id="cf614-169">string</span></span>                                   | <span data-ttu-id="cf614-170">Ich preferowana kultura do komunikacji i waluty, na przykład "en-US".</span><span class="sxs-lookup"><span data-stu-id="cf614-170">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="cf614-171">Zobacz obsługiwane [Języki w centrum partnerskim i ustawienia regionalne](partner-center-supported-languages-and-locales.md) dla obsługiwanych kultur.</span><span class="sxs-lookup"><span data-stu-id="cf614-171">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="cf614-172">language</span><span class="sxs-lookup"><span data-stu-id="cf614-172">language</span></span>         | <span data-ttu-id="cf614-173">ciąg</span><span class="sxs-lookup"><span data-stu-id="cf614-173">string</span></span>                                   | <span data-ttu-id="cf614-174">Język domyślny.</span><span class="sxs-lookup"><span data-stu-id="cf614-174">The default language.</span></span> <span data-ttu-id="cf614-175">Obsługiwane są dwa znaki kodów języka (na przykład `en` lub `fr` ).</span><span class="sxs-lookup"><span data-stu-id="cf614-175">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="cf614-176">\_Nazwa firmy</span><span class="sxs-lookup"><span data-stu-id="cf614-176">company\_name</span></span>    | <span data-ttu-id="cf614-177">ciąg</span><span class="sxs-lookup"><span data-stu-id="cf614-177">string</span></span>                                   | <span data-ttu-id="cf614-178">Nazwa zarejestrowanej firmy/organizacji.</span><span class="sxs-lookup"><span data-stu-id="cf614-178">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="cf614-179">domyślny \_ adres</span><span class="sxs-lookup"><span data-stu-id="cf614-179">default\_address</span></span> | [<span data-ttu-id="cf614-180">Adres</span><span class="sxs-lookup"><span data-stu-id="cf614-180">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="cf614-181">Zarejestrowany adres firmy/organizacji klienta.</span><span class="sxs-lookup"><span data-stu-id="cf614-181">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="cf614-182">Zobacz zasób [adresu](utility-resources.md#address) , aby uzyskać informacje o ograniczeniach długości.</span><span class="sxs-lookup"><span data-stu-id="cf614-182">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="cf614-183">Profil firmy</span><span class="sxs-lookup"><span data-stu-id="cf614-183">Company profile</span></span>

<span data-ttu-id="cf614-184">Ta tabela zawiera opis minimalnych wymaganych pól z zasobów [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) wymaganych do utworzenia nowego klienta.</span><span class="sxs-lookup"><span data-stu-id="cf614-184">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="cf614-185">Nazwa</span><span class="sxs-lookup"><span data-stu-id="cf614-185">Name</span></span>   | <span data-ttu-id="cf614-186">Typ</span><span class="sxs-lookup"><span data-stu-id="cf614-186">Type</span></span>   | <span data-ttu-id="cf614-187">Opis</span><span class="sxs-lookup"><span data-stu-id="cf614-187">Description</span></span>                                                  |
|--------|--------|--------------------------------------------------------------|
| <span data-ttu-id="cf614-188">domena</span><span class="sxs-lookup"><span data-stu-id="cf614-188">domain</span></span> | <span data-ttu-id="cf614-189">ciąg</span><span class="sxs-lookup"><span data-stu-id="cf614-189">string</span></span> | <span data-ttu-id="cf614-190">Nazwa domeny klienta, na przykład contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="cf614-190">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
|<span data-ttu-id="cf614-191">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="cf614-191">organizationRegistrationNumber</span></span>|<span data-ttu-id="cf614-192">Ciąg</span><span class="sxs-lookup"><span data-stu-id="cf614-192">String</span></span>|<span data-ttu-id="cf614-193">Numer identyfikacyjny organizacji klienta (określany również jako numer INN w niektórych krajach).</span><span class="sxs-lookup"><span data-stu-id="cf614-193">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="cf614-194">Wymagane tylko dla firmy lub organizacji klienta w następujących krajach.</span><span class="sxs-lookup"><span data-stu-id="cf614-194">Only required for customer’s company/organization located in the following countries.</span></span> <span data-ttu-id="cf614-195">Armenia (AM), Azerbejdżan (AZ), Białoruś (przez), Węgry (HU), Kazachstan (KZ), Kirgistan (KG), Mołdawia (MD), Rosja (RU), Tadżykistan (TJ), Uzbekistan (UZ), Ukraina (UA).</span><span class="sxs-lookup"><span data-stu-id="cf614-195">Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA).</span></span> <span data-ttu-id="cf614-196">W przypadku firmy/organizacji klienta znajdującej się w innych krajach nie należy określać tego elementu.</span><span class="sxs-lookup"><span data-stu-id="cf614-196">For customer’s company/organization located in other countries this should not be specified.</span></span>|


### <a name="request-example"></a><span data-ttu-id="cf614-197">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="cf614-197">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 789
Expect: 100-continue
Connection: Keep-Alive

{
    "CompanyProfile": {
        "Domain": "xyz.ccsctp.net",
    },
    "BillingProfile": {
        "Culture": "EN-US",
        "Email": "test@outlook.com",
        "Language": "en",
        "CompanyName": "test company",
        "DefaultAddress": {
            "FirstName": "Test",
            "LastName": "Test",
            "AddressLine1": "One Microsoft Way",
            "City": "Redmond",
            "State": "WA",
            "PostalCode": "98052",
            "Country": "US",
        }
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="cf614-198">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="cf614-198">REST response</span></span>

<span data-ttu-id="cf614-199">Jeśli to się powiedzie, ten interfejs API zwraca zasób [klienta](customer-resources.md#customer) dla nowego klienta.</span><span class="sxs-lookup"><span data-stu-id="cf614-199">If successful, this API returns a [Customer](customer-resources.md#customer) resource for the new customer.</span></span> <span data-ttu-id="cf614-200">Zapisz identyfikator klienta i szczegóły usługi Azure AD do użytku w przyszłości z zestawem SDK Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="cf614-200">Save the customer ID and Azure AD details for future use with the Partner Center SDK.</span></span> <span data-ttu-id="cf614-201">Będą one potrzebne do korzystania z zarządzania kontami, na przykład.</span><span class="sxs-lookup"><span data-stu-id="cf614-201">You will need them for use with account management, for example.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cf614-202">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cf614-202">Response success and error codes</span></span>

<span data-ttu-id="cf614-203">Odpowiedzi są uzyskiwane przy użyciu kodu stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="cf614-203">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cf614-204">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="cf614-204">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cf614-205">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cf614-205">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="cf614-206">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cf614-206">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CV: ObwhuhD2tUKJoM+Z.0
MS-ServerId: 202010223
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "id": "dfd8cc0a-c592-468c-8461-869a38d24738",
    "commerceId": "0a4ce58a-6f96-4273-8035-d9c7d31b9ba4",
    "companyProfile": {
        "tenantId": "dfd8cc0a-c592-468c-8461-869a38d24738",
        "domain": "xyz.ccsctp.net",
        "attributes": {
            "objectType": "CustomerCompanyProfile"
        }
    },
    "billingProfile": {
        "id": "d17c0275-da92-5c33-9032-782ef1d0b69b",
        "email": "test@outlook.com",
        "culture": "en-US",
        "language": "en",
        "companyName": "test company",
        "defaultAddress": {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "One Microsoft Way",
            "postalCode": "98052",
            "firstName": "Test",
            "lastName": "Test",
            "phoneNumber": ""
        },
        "attributes": {
            "etag": "5920358838484612121",
            "objectType": "CustomerBillingProfile"
        }
    },
    "relationshipToPartner": "none",
    "userCredentials": {
        "userName": "admin",
        "password": "=;;n.=s9Z"
    },
    "attributes": {
        "objectType": "Customer"
    }
}
```
