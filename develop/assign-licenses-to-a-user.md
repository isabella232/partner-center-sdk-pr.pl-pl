---
title: Przypisywanie licencji do użytkownika
description: Dowiedz się, jak przypisywać licencje do użytkownika klienta za pośrednictwem Partner Center API, takich jak korzystanie z interfejsów \# API C lub REST.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 88ce0f185b0b043c4a7862b7f9808fb8805d40b9
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974373"
---
# <a name="assign-licenses-to-a-user-via-partner-center-apis"></a>Przypisywanie licencji do użytkownika za pośrednictwem Partner Center API

Jak przypisać licencje do użytkownika klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator użytkownika klienta. Ten identyfikator identyfikuje użytkownika, do którego ma zostać przypisana licencja.

- Identyfikator jednostki SKU produktu, który identyfikuje produkt licencji.

## <a name="assigning-licenses-through-code"></a>Przypisywanie licencji za pomocą kodu

Po przypisaniu licencji do użytkownika musisz wybrać jedną z kolekcji subskrybowanych jednostki SKU klienta. Następnie po zidentyfikowaniu produktów, które chcesz przypisać, musisz uzyskać identyfikator SKU produktu dla każdego produktu w celu wykonania przypisań. Każde [**wystąpienie klasy SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) zawiera właściwość [**ProductSku,**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) z której można odwołać się do [**obiektu ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) i uzyskać [**identyfikator**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).

Żądanie przypisania licencji musi zawierać licencje z jednej grupy licencji. Na przykład nie można przypisać licencji z grup [**Grupa1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) i **Grupa2** w tym samym żądaniu. Próba przypisania licencji z więcej niż jednej grupy w jednym żądaniu nie powiedzie się z odpowiednim błędem. Aby dowiedzieć się, jakie licencje są dostępne dla grupy licencji, zobacz [Get a list of available licenses by license group (Uzyskiwanie](get-a-list-of-available-licenses-by-license-group.md)listy dostępnych licencji według grupy licencji).

Oto kroki przypisywania licencji za pomocą kodu:

1. Utworzyć wystąpienia [**obiektu LicenseAssignment.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) Ten obiekt umożliwia określenie przypisanej przez program sku produktu i planów usług.

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. Wypełnij właściwości obiektu, jak pokazano poniżej. W tym kodzie przyjęto założenie, że masz już identyfikator SKU produktu i że wszystkie dostępne plany usług zostaną przypisane (to oznacza, że żaden nie zostanie wykluczony).

    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. Jeśli nie masz identyfikatora jednostki SKU produktu, musisz pobrać kolekcję subskrybowanych jednostki SKU i pobrać identyfikator jednostki SKU produktu z jednej z nich. Oto przykład, jeśli znasz nazwę sku produktu.

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. Następnie należy utworzyć nową listę typu [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)i dodać obiekt licencji. Możesz przypisać więcej niż jedną licencję, dodając każdą z nich indywidualnie do listy. Licencje uwzględnione na tej liście muszą pochodzić z tej samej grupy licencji.

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. Utwórz wystąpienie [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) i przypisz listę przypisań licencji do właściwości [**LicensesToAssign.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign)

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. Wywołaj [**metodę Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) lub [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) i przekaż obiekt aktualizacji licencji, jak pokazano poniżej, aby przypisać licencje.

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a>C\#

Aby przypisać licencję do użytkownika klienta, najpierw należy utworzyć wystąpienia obiektu [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) i wypełnić właściwości [**Skuid**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) i [**ExcludedPlans.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) Ten obiekt umożliwia określenie produktu SKU do przypisania i plany usługi do wykluczenia. Następnie należy utworzyć nową listę typu **LicenseAssignment** i dodać obiekt licencji do listy. Następnie utwórz wystąpienie [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) i przypisz listę przypisań licencji do właściwości [**LicensesToAssign.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign)

Następnie użyj metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta, oraz metody [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem użytkownika w celu zidentyfikowania użytkownika. Następnie pobierz interfejs do operacji aktualizacji licencji użytkownika klienta z [**właściwości LicenseUpdates.**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates)

Na koniec wywołaj [**metodę Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) lub [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) i przekaż obiekt aktualizacji licencji, aby przypisać licencję.

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

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** zestaw SDK Centrum partnerskiego Samples **Class**: CustomerUserAssignLicenses.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/users/{user-id}/licenseupdates HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry URI

Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i użytkownika.

| Nazwa        | Typ   | Wymagane | Opis                                       |
|-------------|--------|----------|---------------------------------------------------|
| identyfikator klienta | ciąg | Tak      | Identyfikator w formacie IDENTYFIKATORA GUID, który identyfikuje klienta. |
| user-id     | ciąg | Tak      | Identyfikator SFORMATOWANY IDENTYFIKATOR GUID, który identyfikuje użytkownika.     |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Uwzględnij [zasób LicenseUpdate](license-resources.md#licenseupdate) w treści żądania, który określa licencje do przypisania.

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

W przypadku powodzenia zwracany jest kod stanu odpowiedzi HTTP 201, a treść odpowiedzi zawiera zasób [LicenseUpdate](license-resources.md#licenseupdate) z informacjami o licencji.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)

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

### <a name="response-example-license-isnt-available"></a>Przykład odpowiedzi (licencja nie jest dostępna)

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
