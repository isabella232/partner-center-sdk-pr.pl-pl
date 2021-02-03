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
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a>Tworzenie klienta dla pośredniego odsprzedawcy przy użyciu interfejsów API usługi Partner Center

**Dotyczy:**

- Centrum partnerskie

Dostawca pośredni może utworzyć klienta dla pośredniego odsprzedawcy.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator dzierżawy pośredniego odsprzedawcy.

- Pośredni odsprzedawca musi mieć partnerstwo z dostawcą pośrednim.

## <a name="c"></a>C\#

Aby dodać nowego klienta w odniesieniu do pośredniego odsprzedawcy:

1. Utwórz wystąpienie nowego obiektu [**klienta**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) , a następnie Utwórz wystąpienie i wypełnij [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) i [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile). Należy pamiętać, aby przypisać pośredni identyfikator odsprzedawcy do właściwości [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) .

2. Użyj właściwości [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , aby uzyskać interfejs do operacji zbierania danych przez klienta.

3. Wywołaj metodę [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) lub [**onasync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) , aby utworzyć klienta.

### <a name="c-example"></a>\#Przykład C

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

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: CreateCustomerforIndirectReseller.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                       |
|----------|-------------------------------------------------------------------|
| **POUBOJOWEGO** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers http/1.1 |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano wymagane właściwości w treści żądania.

| Nazwa                                          | Typ   | Wymagane | Opis                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [BillingProfile](#billing-profile)             | object | Tak      | Informacje o profilu rozliczania klienta.                                                                                                                                                                                                                                                                                                           |
| [CompanyProfile](#company-profile)             | object | Tak      | Informacje o profilu firmy klienta.                                                               
| [AssociatedPartnerId](customer-resources.md#customer) | ciąg | Tak      | Identyfikator pośredniego odsprzedawcy. Pośredni odsprzedawca określony przez podany tutaj identyfikator musi mieć powiązanie z dostawcą pośrednim lub żądanie zakończy się niepowodzeniem. Należy również pamiętać, że jeśli wartość AssociatedPartnerId nie zostanie podana, klient zostanie utworzony jako bezpośredni klient dostawcy pośredniego, a nie pośredni odsprzedawca. |
|Domena| Ciąg| Tak|Nazwa domeny klienta, na przykład contoso.onmicrosoft.com.|
|organizationRegistrationNumber|    ciąg|Tak|     Numer identyfikacyjny organizacji klienta (określany również jako numer INN w niektórych krajach). Wymagane tylko dla firmy lub organizacji klienta w następujących krajach. Armenia (AM), Azerbejdżan (AZ), Białoruś (przez), Węgry (HU), Kazachstan (KZ), Kirgistan (KG), Mołdawia (MD), Rosja (RU), Tadżykistan (TJ), Uzbekistan (UZ), Ukraina (UA). W przypadku firmy/organizacji klienta znajdującej się w innych krajach nie należy określać tego elementu.|



#### <a name="billing-profile"></a>Profil rozliczeniowy

Ta tabela zawiera opis minimalnych wymaganych pól z zasobów [CustomerBillingProfile](customer-resources.md#customerbillingprofile) wymaganych do utworzenia nowego klienta.

| Nazwa             | Typ                                     | Wymagane | Opis                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| poczta e-mail            | ciąg                                   | Tak      | Adres e-mail klienta.                                                                                                                                                                                   |
| kultura          | ciąg                                   | Tak      | Ich preferowana kultura do komunikacji i waluty, na przykład "en-US". Zobacz obsługiwane [Języki w centrum partnerskim i ustawienia regionalne](partner-center-supported-languages-and-locales.md) dla obsługiwanych kultur. |
| language         | ciąg                                   | Tak      | Język domyślny. Obsługiwane są dwa znaki kodów języka (na przykład `en` lub `fr` ).                                                                                                                                |
| \_Nazwa firmy    | ciąg                                   | Tak      | Nazwa zarejestrowanej firmy/organizacji.                                                                                                                                                                       |
| domyślny \_ adres | [Adres](utility-resources.md#address) | Tak      | Zarejestrowany adres firmy/organizacji klienta. Zobacz zasób [adresu](utility-resources.md#address) , aby uzyskać informacje o ograniczeniach długości.                                             |

#### <a name="company-profile"></a>Profil firmy

Ta tabela zawiera opis minimalnych wymaganych pól z zasobów [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) wymaganych do utworzenia nowego klienta.

| Nazwa   | Typ   | Wymagane | Opis                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| domena | ciąg | Tak     | Nazwa domeny klienta, na przykład contoso.onmicrosoft.com. |
| organizationRegistrationNumber | ciąg | Zależy od warunku | Numer rejestracji organizacji klienta (określany również jako numer INN w niektórych krajach). <br/><br/>Wypełnienie tego pola jest wymagane tylko wtedy, gdy firma lub organizacja klienta znajduje się w następujących krajach: <br/><br/>-Armenia (AM) <br/>-Azerbejdżan (AZ)<br/>-Białoruś (przez)<br/>-Węgry (HU)<br/>-Kazachstan (KZ)<br/>-Kirgistan (KG)<br/>— Mołdawia (MD)<br/>— Rosja (RU)<br/>-Tadżykistan (TJ)<br/>-Uzbekistan (UZ)<br/>-Ukraina (UA)<br/><br/>To pole nie jest wymagane, jeśli firma/organizacja klienta znajduje się w innych krajach poza tymi przedstawionymi tutaj.  |

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

Jeśli to się powiedzie, odpowiedź zawiera zasób [klienta](customer-resources.md#customer) dla nowego klienta.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Odpowiedzi są uzyskiwane przy użyciu kodu stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

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