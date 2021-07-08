---
title: Pobieranie listy klientów filtrowanych według pola wyszukiwania
description: Pobiera kolekcję zasobów klienta, które pasują do filtru. Opcjonalnie możesz ustawić rozmiar strony. Możesz filtrować według nazwy firmy, domeny, odsprzedawcy pośredniego lub pośredniego dostawcy rozwiązań w chmurze (CSP).
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 663b8509d8704f9c443796d9fbcf72fb9c5b7fb2
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874962"
---
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a>Pobieranie listy klientów filtrowanych według pola wyszukiwania

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Pobiera kolekcję [zasobów klienta,](customer-resources.md#customer) które pasują do filtru. Opcjonalnie możesz ustawić rozmiar strony. Możesz filtrować według nazwy firmy, domeny, odsprzedawcy pośredniego lub pośredniego dostawcy rozwiązań w chmurze (CSP).

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Filtr skonstruowany przez użytkownika.

## <a name="c"></a>C\#

Aby uzyskać kolekcję klientów, którzy pasują do filtru, najpierw utwórz obiekt [**SimpleFieldFilter,**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) aby utworzyć filtr. Musisz przekazać ciąg zawierający pole [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)i wskazać typ operacji filtrowania jako [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation). Jest to jedyna operacja filtrowania pól obsługiwana przez punkt końcowy klientów. Należy również podać ciąg, według których ma być filtrowany ciąg.

Następnie zaimplestruj obiekt [**iQuery,**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) aby przekazać go do zapytania, wywołując metodę [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) i przekazując do niego filtr. BuildSimplyQuery to tylko jeden z typów zapytań obsługiwanych przez [**klasę QueryFactory.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory)

Na koniec, aby wykonać filtr i uzyskać wynik, najpierw użyj funkcji [**IAggregatePartner.Customers,**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) aby uzyskać interfejs dla operacji klienta partnera. Następnie wywołaj [**metodę Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) lub [**QueryAsync.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync)

``` csharp
IAggregatePartner partnerOperations;

// Specify the partial string to filter by (to match Contoso).
string searchPrefix = "cont"

// Create a simple field filter.
var fieldFilter = new SimpleFieldFilter(
    CustomerSearchField.CompanyName.ToString(),
    FieldFilterOperation.StartsWith,
    searchPrefix);

// Create an iQuery object to pass to the Query method.
var myQuery = QueryFactory.Instance.BuildSimpleQuery(fieldFilter);

// Get the collection of matching customers.
var customers = partnerOperations.Customers.Query(myQuery);
```

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** zestaw SDK Centrum partnerskiego Samples Class : FilterCustomers.cs **(Klasa** przykładów zestaw SDK Centrum partnerskiego: FilterCustomers.cs)

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}&filter={filter} HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry URI

Użyj następujących parametrów zapytania.

| Nazwa   | Typ   | Wymagane | Opis                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| size   | int    | Nie       | Liczba wyników, które mają być wyświetlane jednocześnie. Ten parametr jest opcjonalny. |
| filter | filter | Tak      | Filtr do zastosowania do klientów. Musi to być zakodowany ciąg.              |

### <a name="filter-syntax"></a>Składnia filtru

Parametr filtru należy skomponować jako serię rozdzielonych przecinkami par klucz-wartość. Każdy klucz i wartość muszą być oddzielnie cytowane i oddzielone dwukropkiem. Cały filtr musi być zakodowany.

Niezakodowany przykład wygląda następująco:

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```

W poniższej tabeli opisano wymagane pary klucz-wartość:

| Klucz      | Wartość                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| Pole    | Pole do filtrowania. Prawidłowe wartości można znaleźć w [**customersearchfield**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield). |
| Wartość    | Wartość do filtrowania. Przypadek wartości jest ignorowany.                                                                |
| Operator | Operator do zastosowania. Jedyną obsługiwaną wartością w tym scenariuszu klienta jest "zaczyna \_ się od".                            |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22CompanyName%22%2C%22Value%22%3A%22Cont%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5ce66de5-eea9-486f-a11c-c852aa3d1502
MS-CorrelationId: a2a912ee-d595-47e2-97ae-1b0ae1efa13d
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca kolekcję [pasujących zasobów](customer-resources.md#customer) klienta w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 1839
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a2a912ee-d595-47e2-97ae-1b0ae1efa13d
MS-RequestId: dfeda56c-1af5-43fc-a9c0-346b9e85dc96
MS-CV: n0lMNyJtaUC802pO.0
MS-ServerId: 202010223
Date: Fri, 24 Feb 2017 22:08:20 GMT

{
    "totalCount": 3,
    "items": [{
            "id": "c5757d70-06f3-4f23-8367-5a9e55019f94",
            "companyProfile": {
                "tenantId": "c5757d70-06f3-4f23-8367-5a9e55019f94",
                "domain": "contoso190.onmicrosoft.com",
                "companyName": "Contoso190",
                "links": {
                    "self": {
                        "uri": "/customers/c5757d70-06f3-4f23-8367-5a9e55019f94/profiles/company",
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
                    "uri": "/customers/c5757d70-06f3-4f23-8367-5a9e55019f94",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "7b26b357-9ca3-48b8-a58e-4febe2662a5d",
            "companyProfile": {
                "tenantId": "7b26b357-9ca3-48b8-a58e-4febe2662a5d",
                "domain": "ContosoCorpCo.onmicrosoft.com",
                "companyName": "Contoso",
                "links": {
                    "self": {
                        "uri": "/customers/7b26b357-9ca3-48b8-a58e-4febe2662a5d/profiles/company",
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
                    "uri": "/customers/7b26b357-9ca3-48b8-a58e-4febe2662a5d",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
            "companyProfile": {
                "tenantId": "bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
                "domain": "contosocorpdemo.onmicrosoft.com",
                "companyName": "Contoso",
                "links": {
                    "self": {
                        "uri": "/customers/bfbd6ef0-311f-47ec-bbd7-0fcb7846661b/profiles/company",
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
                    "uri": "/customers/bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers?size=0&filter=%7B%22Field%22%3A%22Domain%22%2C%22Value%22%3A%22cont%22%2C%22Operator%22%3A%22starts_with%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
