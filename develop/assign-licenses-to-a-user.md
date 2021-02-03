---
title: Przypisywanie licencji do użytkownika
description: Dowiedz się, jak przypisywać licencje do użytkownika klienta za pośrednictwem interfejsów API Centrum partnerskiego, takich jak korzystanie z \# interfejsów API języka C lub Rest.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6eb0b953b9157e48074415bb3207e2946cfb2ab4
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768546"
---
# <a name="assign-licenses-to-a-user-via-partner-center-apis"></a>Przypisywanie licencji do użytkownika za pośrednictwem interfejsów API Centrum partnerskiego

**Dotyczy:**

- Centrum partnerskie

Przypisywanie licencji do użytkownika klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator użytkownika klienta. Ten identyfikator identyfikuje użytkownika, do którego ma zostać przypisana licencja.

- Identyfikator jednostki SKU produktu identyfikujący produkt na potrzeby licencji.

## <a name="assigning-licenses-through-code"></a>Przypisywanie licencji za poorednictwem kodu

W przypadku przypisywania licencji do użytkownika należy wybrać z kolekcji subskrybowanych jednostek SKU klienta. Następnie po zidentyfikowaniu produktów, które chcesz przypisać, należy uzyskać identyfikator jednostki SKU produktu dla każdego produktu w celu przypisania. Każde wystąpienie [**SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) zawiera właściwość [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) , z której można odwołać się do obiektu [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) i uzyskać [**Identyfikator**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).

Żądanie przypisania licencji musi zawierać licencje z pojedynczej grupy licencji. Na przykład nie można przypisać licencji z [**grupa1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) i **group2** w tym samym żądaniu. Próba przypisania licencji z więcej niż jednej grupy w pojedynczym żądaniu zakończy się niepowodzeniem z powodu odpowiedniego błędu. Aby dowiedzieć się, jakie licencje są dostępne dla grupy licencji, zobacz sekcję [Pobieranie listy dostępnych licencji według grupy licencji](get-a-list-of-available-licenses-by-license-group.md).

Poniżej przedstawiono procedurę przypisywania licencji za pomocą kodu:

1. Utwórz wystąpienie obiektu [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) . Ten obiekt służy do określania jednostki SKU produktu i planów usług do przypisania.

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. Wypełnij właściwości obiektu, jak pokazano poniżej. Ten kod zakłada, że masz już identyfikator SKU produktu i że wszystkie dostępne plany usług zostaną przypisane (oznacza to, że żaden z nich nie zostanie wykluczony).

    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. Jeśli nie masz identyfikatora SKU produktu, musisz pobrać kolekcję subskrybowanych jednostek SKU i uzyskać identyfikator SKU produktu z jednego z nich. Oto przykład, jeśli znasz nazwę jednostki SKU produktu.

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. Następnie Utwórz wystąpienie nowej listy typu [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)i Dodaj obiekt License. Do listy można przypisać więcej niż jedną licencję. Licencje zawarte na tej liście muszą należeć do tej samej grupy licencji.

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. Utwórz wystąpienie [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) i przypisz listę przypisań licencji do właściwości [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) .

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. Wywołaj metodę [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) lub [**onasync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) i przekaż obiekt aktualizacji licencji, jak pokazano poniżej, aby przypisać licencje.

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a>C\#

Aby przypisać licencję do użytkownika klienta, należy najpierw utworzyć wystąpienie obiektu [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) i wypełnić właściwości [**identyfikatora skuId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) i [**ExcludedPlans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) . Ten obiekt służy do określania jednostki SKU produktu do przypisania i planów usług, które mają zostać wykluczone. Następnie Utwórz wystąpienie nowej listy typu **LicenseAssignment** i Dodaj obiekt License do listy. Następnie Utwórz wystąpienie [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) i przypisz listę przypisań licencji do właściwości [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) .

Następnie użyj metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta i metodę [**users. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem użytkownika identyfikującym użytkownika. Następnie uzyskaj interfejs do operacji aktualizacji licencji użytkownika klienta z właściwości [**LicenseUpdates**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) .

Na koniec Wywołaj metodę [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) lub [**onasync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) i przekaż obiekt aktualizacji licencji, aby przypisać licencję.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerUserId;
// string selectedCustomerId;
// string selectedProductSkuId;

// Instantiate and populate a LicenseAssignment object.
LicenseAssignment license = new LicenseAssignment();
license.SkuId = selectedProductSkuId;
license.ExcludedPlans = null;

// Instantiate a list of licenses to assign and add the license to it.
List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
licenseList.Add(license);

// Instantiate a LicenseUpdate object and add the list of licenses to assign.
LicenseUpdate updateLicense = new LicenseUpdate();
updateLicense.LicensesToAssign = licenseList;

// Update the user licenses.
var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: CustomerUserAssignLicenses.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| **POUBOJOWEGO** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/users/{User-ID}/licenseupdates http/1.1 |

#### <a name="uri-parameters"></a>Parametry identyfikatora URI

Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i użytkownika.

| Nazwa        | Typ   | Wymagane | Opis                                       |
|-------------|--------|----------|---------------------------------------------------|
| Identyfikator klienta | ciąg | Tak      | Identyfikator GUID, który identyfikuje klienta. |
| user-id     | ciąg | Tak      | Identyfikator GUID, który identyfikuje użytkownika.     |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

W treści żądania należy uwzględnić zasób [LicenseUpdate](license-resources.md#licenseupdate) , który określa licencje do przypisania.

### <a name="request-example"></a>Przykład żądania

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/554526aa-cf5e-46fa-95df-98dbc55d8a1e/licenseupdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 183
Expect: 100-continue

{
    "LicensesToAssign": [{
            "ExcludedPlans": null,
            "SkuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "LicensesToRemove": null,
    "LicenseWarnings": null,
    "Attributes": {
        "ObjectType": "LicenseUpdate"
    }
}
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, zwracany jest kod stanu odpowiedzi HTTP 201, a treść odpowiedzi zawiera zasób [LicenseUpdate](license-resources.md#licenseupdate) z informacjami o licencji.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example-success"></a>Przykład odpowiedzi (powodzenie)

```http
HTTP/1.1 201 Created
Content-Length: 139
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CV: 5AnzcZQrvUqCq3kd.0
MS-ServerId: 030020525
Date: Thu, 20 Apr 2017 21:50:39 GMT

{
    "licensesToAssign": [{
            "skuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "licenseWarnings": [],
    "attributes": {
        "objectType": "LicenseUpdate"
    }
}
```

### <a name="response-example-license-isnt-available"></a>Przykład odpowiedzi (licencja jest niedostępna)

```http
HTTP/1.1 400 Bad Request
Content-Length: 341
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: f4f3b748-8b22-4d07-a5a1-dceb32824192
MS-CV: 5npA0K22CUmWPOzB.0
MS-ServerId: 102030524
Date: Thu, 20 Apr 2017 22:12:36 GMT

{
    "code": 60012,
    "description": "We&#39;re sorry, it looks like you've run out of licenses. Buy more licenses, and then try again.",
    "data": ["LicenseQuotaExceededException : Subscription with Account 0c39d6d5-c70d-4c55-bc02-f620844f3fd1 and SKU f8a1db68-be16-40ed-86d5-cb42ce701560 does not have any available licenses left."],
    "source": "PartnerFD"
}
```
