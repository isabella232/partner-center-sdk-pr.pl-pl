---
title: Tworzenie klienta dla odsprzedawcy pośredniego
description: Dowiedz się, jak dostawca pośredni może używać Partner Center API do tworzenia klienta dla odsprzedawcy pośredniego.
ms.date: 04/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e54e083dda758cc712c889916676007a389ba69c8009bb3d4907df343a436004
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991739"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a>Tworzenie klienta dla odsprzedawcy pośredniego przy użyciu Partner Center API

Dostawca pośredni może utworzyć klienta dla odsprzedawcy pośredniego.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.

- Identyfikator dzierżawy odsprzedawcy pośredniego.

- Odsprzedawca pośredni musi mieć partnerstwo z dostawcą pośrednim.

## <a name="c"></a>C\#

Aby dodać nowego klienta dla odsprzedawcy pośredniego:

1. Należy utworzyć wystąpienia nowego obiektu [**Customer,**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) a następnie utworzyć jego wystąpienia i wypełnić pola [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) i [**CompanyProfile.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile) Pamiętaj, aby przypisać identyfikator odsprzedawcy pośredniego do właściwości [**AssociatedPartnerID.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid)

2. Użyj właściwości [**IAggregatePartner.Customers,**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) aby uzyskać interfejs do operacji zbierania danych klientów.

3. Wywołaj [**metodę Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) lub [**CreateAsync,**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) aby utworzyć klienta.

### <a name="c-example"></a>Przykład w \# języku C

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

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** zestaw SDK Centrum partnerskiego Samples **Class**: CreateCustomerforIndirectReseller.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                       |
|----------|-------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1 |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano wymagane właściwości w treści żądania.

| Nazwa                                          | Typ   | Wymagane | Opis                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [BillingProfile](#billing-profile)             | object | Tak      | Informacje o profilu rozliczeniowym klienta.                                                                                                                                                                                                                                                                                                           |
| [CompanyProfile](#company-profile)             | object | Tak      | Informacje o profilu firmy klienta.                                                               
| [AssociatedPartnerId](customer-resources.md#customer) | ciąg | Tak      | Identyfikator odsprzedawcy pośredniego. Odsprzedawca pośredni wskazany za pomocą identyfikatora podanego w tym miejscu musi mieć partnerstwo z dostawcą pośrednim, w przypadku gdy żądanie nie powiedzie się. Należy również zauważyć, że jeśli wartość AssociatedPartnerId nie zostanie dostarczona, klient zostanie utworzony jako bezpośredni klient dostawcy pośredniego, a nie odsprzedawcy pośredniego. |
|Domena| Ciąg| Tak|Nazwa domeny klienta, na przykład contoso.onmicrosoft.com.|
|organizationRegistrationNumber|    ciąg|Tak|     Numer rejestracji organizacji klienta (w niektórych krajach określany również jako numer NUMER IDENTYFIKACYJNY). Wymagana tylko w przypadku firmy/organizacji klienta znajdującej się w następujących krajach: Zamówienie (AM), Kolumbia (AZ), Kolumbia (HU), KZ), Kyrgyzstan(KG), Azja (MD), Korea (RU), Tajikistan(TJ), Przemysl(UZ), Indie, Brazylia, Republika Południowej Afryki,Portal, Zjednoczone Królestwo, Arabia, Przećwicz, Wietnam, Anwil, Przemysl, Południowe Niemówiące i Ankai. W przypadku firmy/organizacji klienta znajdującej się w innych krajach jest to pole opcjonalne.|



#### <a name="billing-profile"></a>Profil rozliczeniowy

W tej tabeli opisano minimalne wymagane pola z zasobu [CustomerBillingProfile](customer-resources.md#customerbillingprofile) potrzebne do utworzenia nowego klienta.

| Nazwa             | Typ                                     | Wymagane | Opis                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| poczta e-mail            | ciąg                                   | Tak      | Adres e-mail klienta.                                                                                                                                                                                   |
| kultura          | ciąg                                   | Tak      | Preferowana kultura komunikacji i waluty, taka jak "en-US". Zobacz [Partner Center obsługiwanych języków i lokalizacji regionalnych](partner-center-supported-languages-and-locales.md) dla obsługiwanych kultur. |
| language         | ciąg                                   | Tak      | Język domyślny. Obsługiwane są dwa kody języków znaków (na `en` przykład lub `fr` ).                                                                                                                                |
| nazwa \_ firmy    | ciąg                                   | Tak      | Nazwa zarejestrowanej firmy/organizacji.                                                                                                                                                                       |
| adres \_ domyślny | [Adres](utility-resources.md#address) | Tak      | Zarejestrowany adres firmy/organizacji klienta. Zapoznaj się z [zasobem](utility-resources.md#address) Adres, aby uzyskać informacje o wszelkich ograniczeniach długości.                                             |

#### <a name="company-profile"></a>Profil firmy

W tej tabeli opisano minimalne wymagane pola z zasobu [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) wymagane do utworzenia nowego klienta.

| Nazwa   | Typ   | Wymagane | Opis                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| domena | ciąg | Tak     | Nazwa domeny klienta, na przykład contoso.onmicrosoft.com. |
| organizationRegistrationNumber | ciąg | Zależy od warunku | Numer rejestracji organizacji klienta (określany również jako numer IDENTYFIKACYJNY w niektórych krajach). <br/><br/>Ukończenie tego pola jest wymagane tylko wtedy, gdy firma/organizacja klienta znajduje się w następujących krajach: <br/><br/>— W Szmionie (AM) <br/>— Wzręski (AZ)<br/>- Wniesienie (BY)<br/>— Dolce (HU)<br/>- Wz (KZ)<br/>- Kyrgyzstan (KG)<br/>— Dobowe (MD)<br/>— Rosyjski (RU)<br/>- Tadżykistan (TJ)<br/>- Dobrzy (UZ)<br/>- W rzece (UA)<br/>- Indie <br/>- Brazylia <br/>— Republika Południowej Afryki <br/>— W tym celu <br/>— Zjednoczone Emiraty Arabskie <br/>— Arabia Saudyjska <br/>- Wzgorąscy <br/>- Wdowa <br/>- Wietnam <br/>- W 2018 roku <br/>- Wzrędy <br/>— Południowy Dobszczyń <br/>- Wzrędy<br/> <br/>W przypadku firmy/organizacji klienta znajdującej się w innych krajach jest to pole opcjonalne.  |

### <a name="request-example"></a>Przykład żądania

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

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, odpowiedź zawiera [zasób Customer](customer-resources.md#customer) (Klient) dla nowego klienta.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Odpowiedzi zawierają kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)

### <a name="response-example"></a>Przykład odpowiedzi

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