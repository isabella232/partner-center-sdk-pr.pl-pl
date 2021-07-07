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
# <a name="create-a-customer-using-partner-center-apis"></a>Tworzenie klienta przy użyciu interfejsów PARTNER CENTER API

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud for US Government

W tym artykule wyjaśniono, jak utworzyć nowego klienta.

> [!IMPORTANT]
> Jeśli jesteś dostawcą pośrednim i chcesz utworzyć klienta dla odsprzedawcy pośredniego, zobacz Tworzenie klienta [dla odsprzedawcy pośredniego.](create-a-customer-for-an-indirect-reseller.md)

Jako partner dostawcy rozwiązań w chmurze (CSP, cloud solution provider) podczas tworzenia klienta możesz składać zamówienia w jego imieniu. Podczas tworzenia klienta tworzysz również:

- Obiekt Azure Active Directory (AD) dla klienta.

- Relacja między odsprzedawcą a klientem używana na potrzeby delegowanych uprawnień administratora.

- Nazwa użytkownika i hasło do logowania się jako administrator klienta.

Po utworzeniu klienta zapisz identyfikator klienta i szczegóły usługi Azure AD do użycia w przyszłości z usługą zestaw SDK Centrum partnerskiego (na przykład zarządzanie kontami).

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

> [!IMPORTANT]
> Aby utworzyć dzierżawę klienta, musisz podać prawidłowy adres fizyczny podczas procesu tworzenia. Adres można zweryfikować, korzystając z kroków opisanych w [scenariuszu Weryfikowanie](validate-an-address.md) adresu. Jeśli utworzysz klienta przy użyciu nieprawidłowego adresu w środowisku piaskownicy, nie będzie można usunąć tej dzierżawy klienta.

## <a name="c"></a>C\#

Aby dodać klienta:

1. Utworzyć wystąpienia nowego [**obiektu Klienta.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) Pamiętaj, aby wypełnić pola [**BillingProfile i**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).

2. Dodaj nowego klienta do [**kolekcji IAggregatePartner.Customers,**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) wywołując pozycję [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) lub [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).

### <a name="c-example"></a>Przykład w \# języku C

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

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** zestaw SDK Centrum partnerskiego Samples Class : CreateCustomer.cs **(Klasa** przykładów zestaw SDK Centrum partnerskiego: CreateCustomer.cs)

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Aby utworzyć nowego klienta:

1. Utwórz nowe wystąpienie obiektów **CustomerBillingProfile** i **CustomerCompanyProfile.** Pamiętaj, aby wypełnić wymagane pola.

2. Utwórz klienta, wywołując funkcję **IAggregatePartner.getCustomers().create.**

### <a name="java-example"></a>Przykład w języku Java

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

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Aby utworzyć klienta, wykonaj [**polecenie New-PartnerCustomer.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md)

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                       |
|----------|-------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1 |

### <a name="request-headers"></a>Nagłówki żądań

- Ten interfejs API jest idempotentny (nie da innego wyniku, jeśli wywołasz go wielokrotnie).

- Wymagany jest identyfikator żądania i identyfikator korelacji.

- Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano wymagane właściwości w treści żądania.

| Nazwa                              | Typ   | Opis                                 |
|-----------------------------------|--------|---------------------------------------------|
| [BillingProfile](#billing-profile) | object | Informacje o profilu rozliczeniowym klienta. |
| [CompanyProfile](#company-profile) | object | Informacje o profilu firmy klienta. |

#### <a name="billing-profile"></a>Profil rozliczeniowy

W tej tabeli opisano minimalne wymagane pola z zasobu [CustomerBillingProfile](customer-resources.md#customerbillingprofile) potrzebne do utworzenia nowego klienta.

| Nazwa             | Typ                                     | Opis                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| poczta e-mail            | ciąg                                   | Adres e-mail klienta.                                                                                                                                                                                   |
| kultura          | ciąg                                   | Preferowana kultura komunikacji i waluty, na przykład "en-US". Zobacz [Partner Center obsługiwanych języków i lokalizacji regionalnych](partner-center-supported-languages-and-locales.md) dla obsługiwanych kultur. |
| language         | ciąg                                   | Język domyślny. Obsługiwane są dwa kody języków znaków (na `en` przykład lub `fr` ).                                                                                                                                |
| nazwa \_ firmy    | ciąg                                   | Nazwa zarejestrowanej firmy/organizacji.                                                                                                                                                                       |
| adres \_ domyślny | [Adres](utility-resources.md#address) | Zarejestrowany adres firmy/organizacji klienta. Zapoznaj się z [zasobem](utility-resources.md#address) Adres, aby uzyskać informacje o wszelkich ograniczeniach długości.                                             |

#### <a name="company-profile"></a>Profil firmy

W tej tabeli opisano minimalne wymagane pola z zasobu [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) wymagane do utworzenia nowego klienta.

| Nazwa   | Typ   | Opis                                                  |
|--------|--------|--------------------------------------------------------------|
| domena | ciąg | Nazwa domeny klienta, na przykład contoso.onmicrosoft.com. |
|organizationRegistrationNumber|Ciąg|Numer rejestracji organizacji klienta (w niektórych krajach określany również jako numer NUMER TELEFONU). Wymagany tylko w przypadku firmy/organizacji klienta znajdującej się w następujących krajach: Do:: Armeni (AM), Azji (AZ), Kolumbii (HU), Kolumbii (KZ), Kyrgyzstan(KG), Przemysł (MD), Kolumbii (RU), Tajikistan(TJ), Dol (UZ), Azji (UA), Brazylii(BR), Indiach, Południowej Afryki, Zjednoczonej Afryki, Kolumbii, Kolumbii, Wietnamu, Anwii, Anwii, Stanów Zjednoczonych, Stanów Zjednoczonych i Stanów Zjednoczonych. W przypadku firmy/organizacji klienta znajdującej się w innych krajach jest to pole opcjonalne.|

### <a name="request-example"></a>Przykład żądania

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

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ten interfejs API zwraca [zasób Klient](customer-resources.md#customer) dla nowego klienta. Zapisz identyfikator klienta i szczegóły usługi Azure AD do użycia w przyszłości z zestaw SDK Centrum partnerskiego. Będą one potrzebne na przykład do zarządzania kontami.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Odpowiedzi zawierają kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)

### <a name="response-example"></a>Przykład odpowiedzi

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
