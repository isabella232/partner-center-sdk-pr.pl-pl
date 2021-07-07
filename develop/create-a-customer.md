---
title: Tworzenie klienta
description: Dowiedz się, Dostawca rozwiązań w chmurze (CSP) może używać interfejsów API Partner Center do tworzenia nowego klienta. W artykule opisano wymagania wstępne i co jeszcze się dzieje.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 6232ca77d057f2f5168b73d81ec551669d540246
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973727"
---
# <a name="create-a-customer-using-partner-center-apis"></a><span data-ttu-id="38b80-104">Tworzenie klienta przy użyciu interfejsów PARTNER CENTER API</span><span class="sxs-lookup"><span data-stu-id="38b80-104">Create a customer using Partner Center APIs</span></span>

<span data-ttu-id="38b80-105">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="38b80-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="38b80-106">W tym artykule wyjaśniono, jak utworzyć nowego klienta.</span><span class="sxs-lookup"><span data-stu-id="38b80-106">This article explains how to create a new customer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="38b80-107">Jeśli jesteś dostawcą pośrednim i chcesz utworzyć klienta dla odsprzedawcy pośredniego, zobacz Tworzenie klienta [dla odsprzedawcy pośredniego.](create-a-customer-for-an-indirect-reseller.md)</span><span class="sxs-lookup"><span data-stu-id="38b80-107">If you are an indirect provider and you want to create a customer for an indirect reseller, please see [Create a customer for an indirect reseller](create-a-customer-for-an-indirect-reseller.md).</span></span>

<span data-ttu-id="38b80-108">Jako partner dostawcy rozwiązań w chmurze (CSP, cloud solution provider) podczas tworzenia klienta możesz składać zamówienia w jego imieniu.</span><span class="sxs-lookup"><span data-stu-id="38b80-108">As a cloud solution provider (CSP) partner, when you create a customer you can place orders on behalf of the customer.</span></span> <span data-ttu-id="38b80-109">Podczas tworzenia klienta tworzysz również:</span><span class="sxs-lookup"><span data-stu-id="38b80-109">When you create a customer, you also create:</span></span>

- <span data-ttu-id="38b80-110">Obiekt Azure Active Directory (AD) dla klienta.</span><span class="sxs-lookup"><span data-stu-id="38b80-110">An Azure Active Directory (AD) tenant object for the customer.</span></span>

- <span data-ttu-id="38b80-111">Relacja między odsprzedawcą a klientem używana na potrzeby delegowanych uprawnień administratora.</span><span class="sxs-lookup"><span data-stu-id="38b80-111">A relationship between the reseller and customer, used for delegated admin privileges.</span></span>

- <span data-ttu-id="38b80-112">Nazwa użytkownika i hasło do logowania się jako administrator klienta.</span><span class="sxs-lookup"><span data-stu-id="38b80-112">A user name and password to sign in as an admin for the customer.</span></span>

<span data-ttu-id="38b80-113">Po utworzeniu klienta zapisz identyfikator klienta i szczegóły usługi Azure AD do użycia w przyszłości z usługą zestaw SDK Centrum partnerskiego (na przykład zarządzanie kontami).</span><span class="sxs-lookup"><span data-stu-id="38b80-113">Once the customer is created, be sure to save the customer ID and Azure AD details for future use with the Partner Center SDK (for example, account management).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38b80-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="38b80-114">Prerequisites</span></span>

- <span data-ttu-id="38b80-115">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="38b80-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="38b80-116">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38b80-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="38b80-117">Aby utworzyć dzierżawę klienta, musisz podać prawidłowy adres fizyczny podczas procesu tworzenia.</span><span class="sxs-lookup"><span data-stu-id="38b80-117">To create a customer tenant you must provide a valid physical address during the creation process.</span></span> <span data-ttu-id="38b80-118">Adres można zweryfikować, korzystając z kroków opisanych w [scenariuszu Weryfikowanie](validate-an-address.md) adresu.</span><span class="sxs-lookup"><span data-stu-id="38b80-118">An address can be validated by following the steps outlined in the [Validate an address](validate-an-address.md) scenario.</span></span> <span data-ttu-id="38b80-119">Jeśli utworzysz klienta przy użyciu nieprawidłowego adresu w środowisku piaskownicy, nie będzie można usunąć tej dzierżawy klienta.</span><span class="sxs-lookup"><span data-stu-id="38b80-119">If you create a customer using an invalid address in the sandbox environment, you will not be able to delete that customer tenant.</span></span>

## <a name="c"></a><span data-ttu-id="38b80-120">C\#</span><span class="sxs-lookup"><span data-stu-id="38b80-120">C\#</span></span>

<span data-ttu-id="38b80-121">Aby dodać klienta:</span><span class="sxs-lookup"><span data-stu-id="38b80-121">To add a customer:</span></span>

1. <span data-ttu-id="38b80-122">Utworzyć wystąpienia nowego [**obiektu Klienta.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer)</span><span class="sxs-lookup"><span data-stu-id="38b80-122">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object.</span></span> <span data-ttu-id="38b80-123">Pamiętaj, aby wypełnić pola [**BillingProfile i**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span><span class="sxs-lookup"><span data-stu-id="38b80-123">Be sure to fill in the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span>

2. <span data-ttu-id="38b80-124">Dodaj nowego klienta do [**kolekcji IAggregatePartner.Customers,**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) wywołując pozycję [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) lub [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).</span><span class="sxs-lookup"><span data-stu-id="38b80-124">Add the new customer to your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection by calling [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).</span></span>

### <a name="c-example"></a><span data-ttu-id="38b80-125">Przykład w \# języku C</span><span class="sxs-lookup"><span data-stu-id="38b80-125">C\# example</span></span>

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

<span data-ttu-id="38b80-126">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="38b80-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="38b80-127">**Project:** zestaw SDK Centrum partnerskiego Samples Class : CreateCustomer.cs **(Klasa** przykładów zestaw SDK Centrum partnerskiego: CreateCustomer.cs)</span><span class="sxs-lookup"><span data-stu-id="38b80-127">**Project**: Partner Center SDK Samples **Class**: CreateCustomer.cs</span></span>

## <a name="java"></a><span data-ttu-id="38b80-128">Java</span><span class="sxs-lookup"><span data-stu-id="38b80-128">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="38b80-129">Aby utworzyć nowego klienta:</span><span class="sxs-lookup"><span data-stu-id="38b80-129">To create a new customer:</span></span>

1. <span data-ttu-id="38b80-130">Utwórz nowe wystąpienie obiektów **CustomerBillingProfile** i **CustomerCompanyProfile.**</span><span class="sxs-lookup"><span data-stu-id="38b80-130">Create a new instance of the **CustomerBillingProfile** and the **CustomerCompanyProfile** objects.</span></span> <span data-ttu-id="38b80-131">Pamiętaj, aby wypełnić wymagane pola.</span><span class="sxs-lookup"><span data-stu-id="38b80-131">Be sure to populate the required fields.</span></span>

2. <span data-ttu-id="38b80-132">Utwórz klienta, wywołując funkcję **IAggregatePartner.getCustomers().create.**</span><span class="sxs-lookup"><span data-stu-id="38b80-132">Create the customer by calling the **IAggregatePartner.getCustomers().create** function.</span></span>

### <a name="java-example"></a><span data-ttu-id="38b80-133">Przykład w języku Java</span><span class="sxs-lookup"><span data-stu-id="38b80-133">Java example</span></span>

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

## <a name="powershell"></a><span data-ttu-id="38b80-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="38b80-134">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="38b80-135">Aby utworzyć klienta, wykonaj [**polecenie New-PartnerCustomer.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md)</span><span class="sxs-lookup"><span data-stu-id="38b80-135">To create a customer, execute the [**New-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) command.</span></span>

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <a name="rest-request"></a><span data-ttu-id="38b80-136">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="38b80-136">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="38b80-137">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="38b80-137">Request syntax</span></span>

| <span data-ttu-id="38b80-138">Metoda</span><span class="sxs-lookup"><span data-stu-id="38b80-138">Method</span></span>   | <span data-ttu-id="38b80-139">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="38b80-139">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="38b80-140">**Post**</span><span class="sxs-lookup"><span data-stu-id="38b80-140">**POST**</span></span> | <span data-ttu-id="38b80-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="38b80-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="38b80-142">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="38b80-142">Request headers</span></span>

- <span data-ttu-id="38b80-143">Ten interfejs API jest idempotentny (nie da innego wyniku, jeśli wywołasz go wielokrotnie).</span><span class="sxs-lookup"><span data-stu-id="38b80-143">This API is idempotent (it will not yield a different result if you call it multiple times).</span></span>

- <span data-ttu-id="38b80-144">Wymagany jest identyfikator żądania i identyfikator korelacji.</span><span class="sxs-lookup"><span data-stu-id="38b80-144">A request ID and correlation ID are required.</span></span>

- <span data-ttu-id="38b80-145">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="38b80-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="38b80-146">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="38b80-146">Request body</span></span>

<span data-ttu-id="38b80-147">W tej tabeli opisano wymagane właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="38b80-147">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="38b80-148">Nazwa</span><span class="sxs-lookup"><span data-stu-id="38b80-148">Name</span></span>                              | <span data-ttu-id="38b80-149">Typ</span><span class="sxs-lookup"><span data-stu-id="38b80-149">Type</span></span>   | <span data-ttu-id="38b80-150">Opis</span><span class="sxs-lookup"><span data-stu-id="38b80-150">Description</span></span>                                 |
|-----------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="38b80-151">BillingProfile</span><span class="sxs-lookup"><span data-stu-id="38b80-151">BillingProfile</span></span>](#billing-profile) | <span data-ttu-id="38b80-152">object</span><span class="sxs-lookup"><span data-stu-id="38b80-152">object</span></span> | <span data-ttu-id="38b80-153">Informacje o profilu rozliczeniowym klienta.</span><span class="sxs-lookup"><span data-stu-id="38b80-153">The customer's billing profile information.</span></span> |
| [<span data-ttu-id="38b80-154">CompanyProfile</span><span class="sxs-lookup"><span data-stu-id="38b80-154">CompanyProfile</span></span>](#company-profile) | <span data-ttu-id="38b80-155">object</span><span class="sxs-lookup"><span data-stu-id="38b80-155">object</span></span> | <span data-ttu-id="38b80-156">Informacje o profilu firmy klienta.</span><span class="sxs-lookup"><span data-stu-id="38b80-156">The customer's company profile information.</span></span> |

#### <a name="billing-profile"></a><span data-ttu-id="38b80-157">Profil rozliczeniowy</span><span class="sxs-lookup"><span data-stu-id="38b80-157">Billing profile</span></span>

<span data-ttu-id="38b80-158">W tej tabeli opisano minimalne wymagane pola z zasobu [CustomerBillingProfile](customer-resources.md#customerbillingprofile) potrzebne do utworzenia nowego klienta.</span><span class="sxs-lookup"><span data-stu-id="38b80-158">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="38b80-159">Nazwa</span><span class="sxs-lookup"><span data-stu-id="38b80-159">Name</span></span>             | <span data-ttu-id="38b80-160">Typ</span><span class="sxs-lookup"><span data-stu-id="38b80-160">Type</span></span>                                     | <span data-ttu-id="38b80-161">Opis</span><span class="sxs-lookup"><span data-stu-id="38b80-161">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="38b80-162">poczta e-mail</span><span class="sxs-lookup"><span data-stu-id="38b80-162">email</span></span>            | <span data-ttu-id="38b80-163">ciąg</span><span class="sxs-lookup"><span data-stu-id="38b80-163">string</span></span>                                   | <span data-ttu-id="38b80-164">Adres e-mail klienta.</span><span class="sxs-lookup"><span data-stu-id="38b80-164">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="38b80-165">kultura</span><span class="sxs-lookup"><span data-stu-id="38b80-165">culture</span></span>          | <span data-ttu-id="38b80-166">ciąg</span><span class="sxs-lookup"><span data-stu-id="38b80-166">string</span></span>                                   | <span data-ttu-id="38b80-167">Preferowana kultura komunikacji i waluty, na przykład "en-US".</span><span class="sxs-lookup"><span data-stu-id="38b80-167">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="38b80-168">Zobacz [Partner Center obsługiwanych języków i lokalizacji regionalnych](partner-center-supported-languages-and-locales.md) dla obsługiwanych kultur.</span><span class="sxs-lookup"><span data-stu-id="38b80-168">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="38b80-169">language</span><span class="sxs-lookup"><span data-stu-id="38b80-169">language</span></span>         | <span data-ttu-id="38b80-170">ciąg</span><span class="sxs-lookup"><span data-stu-id="38b80-170">string</span></span>                                   | <span data-ttu-id="38b80-171">Język domyślny.</span><span class="sxs-lookup"><span data-stu-id="38b80-171">The default language.</span></span> <span data-ttu-id="38b80-172">Obsługiwane są dwa kody języków znaków (na `en` przykład lub `fr` ).</span><span class="sxs-lookup"><span data-stu-id="38b80-172">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="38b80-173">nazwa \_ firmy</span><span class="sxs-lookup"><span data-stu-id="38b80-173">company\_name</span></span>    | <span data-ttu-id="38b80-174">ciąg</span><span class="sxs-lookup"><span data-stu-id="38b80-174">string</span></span>                                   | <span data-ttu-id="38b80-175">Nazwa zarejestrowanej firmy/organizacji.</span><span class="sxs-lookup"><span data-stu-id="38b80-175">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="38b80-176">adres \_ domyślny</span><span class="sxs-lookup"><span data-stu-id="38b80-176">default\_address</span></span> | [<span data-ttu-id="38b80-177">Adres</span><span class="sxs-lookup"><span data-stu-id="38b80-177">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="38b80-178">Zarejestrowany adres firmy/organizacji klienta.</span><span class="sxs-lookup"><span data-stu-id="38b80-178">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="38b80-179">Zapoznaj się z [zasobem](utility-resources.md#address) Adres, aby uzyskać informacje o wszelkich ograniczeniach długości.</span><span class="sxs-lookup"><span data-stu-id="38b80-179">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="38b80-180">Profil firmy</span><span class="sxs-lookup"><span data-stu-id="38b80-180">Company profile</span></span>

<span data-ttu-id="38b80-181">W tej tabeli opisano minimalne wymagane pola z zasobu [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) wymagane do utworzenia nowego klienta.</span><span class="sxs-lookup"><span data-stu-id="38b80-181">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="38b80-182">Nazwa</span><span class="sxs-lookup"><span data-stu-id="38b80-182">Name</span></span>   | <span data-ttu-id="38b80-183">Typ</span><span class="sxs-lookup"><span data-stu-id="38b80-183">Type</span></span>   | <span data-ttu-id="38b80-184">Opis</span><span class="sxs-lookup"><span data-stu-id="38b80-184">Description</span></span>                                                  |
|--------|--------|--------------------------------------------------------------|
| <span data-ttu-id="38b80-185">domena</span><span class="sxs-lookup"><span data-stu-id="38b80-185">domain</span></span> | <span data-ttu-id="38b80-186">ciąg</span><span class="sxs-lookup"><span data-stu-id="38b80-186">string</span></span> | <span data-ttu-id="38b80-187">Nazwa domeny klienta, na przykład contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="38b80-187">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
|<span data-ttu-id="38b80-188">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="38b80-188">organizationRegistrationNumber</span></span>|<span data-ttu-id="38b80-189">Ciąg</span><span class="sxs-lookup"><span data-stu-id="38b80-189">String</span></span>|<span data-ttu-id="38b80-190">Numer rejestracji organizacji klienta (w niektórych krajach określany również jako numer NUMER TELEFONU).</span><span class="sxs-lookup"><span data-stu-id="38b80-190">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="38b80-191">Wymagany tylko w przypadku firmy/organizacji klienta znajdującej się w następujących krajach: Do:: Armeni (AM), Azji (AZ), Kolumbii (HU), Kolumbii (KZ), Kyrgyzstan(KG), Przemysł (MD), Kolumbii (RU), Tajikistan(TJ), Dol (UZ), Azji (UA), Brazylii(BR), Indiach, Południowej Afryki, Zjednoczonej Afryki, Kolumbii, Kolumbii, Wietnamu, Anwii, Anwii, Stanów Zjednoczonych, Stanów Zjednoczonych i Stanów Zjednoczonych.</span><span class="sxs-lookup"><span data-stu-id="38b80-191">Only required for customer’s company/organization located in the following countries: Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA), Brazil(BR), India, South Africa, Poland, United Arab Emirates, Saudi Arabia, Turkey, Thailand, Vietnam, Myanmar, Iraq, South Sudan, and Venezuela.</span></span> <span data-ttu-id="38b80-192">W przypadku firmy/organizacji klienta znajdującej się w innych krajach jest to pole opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="38b80-192">For customer’s company/organization located in other countries, this is an optional field.</span></span>|

### <a name="request-example"></a><span data-ttu-id="38b80-193">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="38b80-193">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="38b80-194">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="38b80-194">REST response</span></span>

<span data-ttu-id="38b80-195">W przypadku powodzenia ten interfejs API zwraca [zasób Klient](customer-resources.md#customer) dla nowego klienta.</span><span class="sxs-lookup"><span data-stu-id="38b80-195">If successful, this API returns a [Customer](customer-resources.md#customer) resource for the new customer.</span></span> <span data-ttu-id="38b80-196">Zapisz identyfikator klienta i szczegóły usługi Azure AD do użycia w przyszłości z zestaw SDK Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="38b80-196">Save the customer ID and Azure AD details for future use with the Partner Center SDK.</span></span> <span data-ttu-id="38b80-197">Będą one potrzebne na przykład do zarządzania kontami.</span><span class="sxs-lookup"><span data-stu-id="38b80-197">You will need them for use with account management, for example.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="38b80-198">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="38b80-198">Response success and error codes</span></span>

<span data-ttu-id="38b80-199">Odpowiedzi zawierają kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="38b80-199">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="38b80-200">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="38b80-200">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="38b80-201">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="38b80-201">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="38b80-202">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="38b80-202">Response example</span></span>

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
