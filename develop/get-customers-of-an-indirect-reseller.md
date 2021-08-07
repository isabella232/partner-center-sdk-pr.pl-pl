---
title: Pobieranie klientów odsprzedawcy pośredniego
description: Jak uzyskać listę klientów odsprzedawcy pośredniego.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e0b3a45c8cf63334ac53e673fbe88734d3692dfca00c5fe8458695cc28c34f64
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990515"
---
# <a name="get-customers-of-an-indirect-reseller"></a>Pobieranie klientów odsprzedawcy pośredniego

Jak uzyskać listę klientów odsprzedawcy pośredniego.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.

- Identyfikator dzierżawy odsprzedawcy pośredniego.

## <a name="c"></a>C\#

Aby uzyskać kolekcję klientów, którzy mają relację z określonym odsprzedawcą pośrednim, najpierw utwórz wystąpienia obiektu [**SimpleFieldFilter,**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) aby utworzyć filtr. Należy przekazać członka wyliczenia [**CustomerSearchField.IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) przekonwertowanego na ciąg i wskazać typ operacji filtrowania [**FieldFilterOperation.StartsWith.**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) Należy również podać identyfikator dzierżawy odsprzedawcy pośredniego, według których ma być filtrowany.

Następnie należy utworzyć wystąpienia obiektu [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) w celu przekazania do zapytania, wywołując metodę [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) i przekazując do niego filtr. BuildSimplyQuery to tylko jeden z typów zapytań obsługiwanych przez [**klasę QueryFactory.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory)

Aby wykonać filtr i uzyskać wynik, najpierw użyj funkcji [**IAggregatePartner.Customers,**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) aby uzyskać interfejs do operacji klienta partnera. Następnie wywołaj [**metodę Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) lub [**QueryAsync.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync)

Aby utworzyć moduł wyliczający do przechodzenia wyników stronicowania, pobierz interfejs fabryki modułu wyliczania kolekcji klientów z właściwości [**IAggregatePartner.Enumerators.Customers,**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) a następnie wywołaj wywołanie create [**,**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create)jak pokazano w poniższym kodzie, przekazując zmienną, która przechowuje kolekcję klientów.

``` csharp
IAggregatePartner partnerOperations;
string indirectResellerId;

// Create a filter.
var filter = new SimpleFieldFilter(
    CustomerSearchField.IndirectReseller.ToString(),
    FieldFilterOperation.StartsWith,
    indirectResellerId);

// Create an iQuery object to pass to the Query method.
var myQuery = QueryFactory.Instance.BuildSimpleQuery(filter);

// Get the collection of matching customers.
var customersPage = partnerOperations.Customers.Query(myQuery);

// Create a customer enumerator for traversing the customer pages.
var customersEnumerator = partnerOperations.Enumerators.Customers.Create(customersPage);
int pageNumber = 1;

while (customersEnumerator.HasValue)
{
    // Work with the current page.
     foreach (var c in customersEnumerator.Current.Items)
    {
        // Display customer tenant identifier and company name.
        Console.WriteLine(string.Format("{0} - {1}.",c.Id,c.CompanyProfile.CompanyName));
    }
    // Get the next page of customers.
    customersEnumerator.Next();
}
```

**Przykład:** [Aplikacja testowa konsoli](console-test-app.md)**Project**: zestaw SDK Centrum partnerskiego Samples **Class**: GetCustomersOfIndirectReseller.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}?filter={filter} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Aby utworzyć żądanie, użyj następujących parametrów zapytania.

| Nazwa   | Typ   | Wymagane | Opis                                                                                                                                                                                                                                                                                   |
|--------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| size   | int    | Nie       | Liczba wyników, które mają być wyświetlane jednocześnie. Ten parametr jest opcjonalny.                                                                                                                                                                                                                |
| filter | filter | Tak      | Zapytanie filtruje wyszukiwanie. Aby pobrać klientów dla określonego odsprzedawcy pośredniego, należy wstawić identyfikator odsprzedawcy pośredniego oraz dołączyć i zakodować następujący ciąg: {"Pole":"IndirectReseller","Value":"{identyfikator odsprzedawcy pośredniego}","Operator":"rozpoczyna się \_ od"}. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example-encoded"></a>Przykład żądania (zakodowany)

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22IndirectReseller%22%2C%22Value%22%3A%22484e548c-f5f3-4528-93a9-c16c6373cb59%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="request-example-decoded"></a>Przykładowe żądanie (zdekodowane)

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter={"Field":"IndirectReseller","Value":"484e548c-f5f3-4528-93a9-c16c6373cb59","Operator":"starts_with"} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia treść odpowiedzi zawiera informacje o klientach odsprzedawcy.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 2273
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: XI2/vIHmIEGVlGL9.0
MS-ServerId: 101112012
Date: Tue, 11 Apr 2017 23:31:28 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
            "companyProfile": {
                "tenantId": "53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
                "domain": "FourthCoffee137.onmicrosoft.com",
                "companyName": "FourthCoffee137",
                "links": {
                    "self": {
                        "uri": "/customers/53eb21cb-6b2d-4ee5-9e92-27dfc927e93c/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "3dfe847b-cad9-4fc1-86d3-cf16c2790087",
            "companyProfile": {
                "tenantId": "3dfe847b-cad9-4fc1-86d3-cf16c2790087",
                "domain": "WingtipToys1254789149.onmicrosoft.com",
                "companyName": "Wingtip Toys1254789149",
                "links": {
                    "self": {
                        "uri": "/customers/3dfe847b-cad9-4fc1-86d3-cf16c2790087/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/3dfe847b-cad9-4fc1-86d3-cf16c2790087",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        },
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
