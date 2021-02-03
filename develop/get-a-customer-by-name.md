---
title: Pobieranie listy klientów filtrowanych według pola wyszukiwania
description: Pobiera kolekcję zasobów klienta, które pasują do filtru. Opcjonalnie można ustawić rozmiar strony. Można filtrować według nazwy firmy, domeny, odsprzedawcy pośredniego lub pośredniego dostawcy rozwiązań w chmurze (CSP).
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: aad9524dbe2c9edbbd7c1d50da7a448f6872fcb9
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768125"
---
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a>Pobieranie listy klientów filtrowanych według pola wyszukiwania

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Pobiera kolekcję zasobów [klienta](customer-resources.md#customer) , które pasują do filtru. Opcjonalnie można ustawić rozmiar strony. Można filtrować według nazwy firmy, domeny, odsprzedawcy pośredniego lub pośredniego dostawcy rozwiązań w chmurze (CSP).

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Filtr skonstruowany przez użytkownika.

## <a name="c"></a>C\#

Aby uzyskać kolekcję klientów pasujących do filtru, należy najpierw utworzyć wystąpienie obiektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) , aby utworzyć filtr. Należy przekazać ciąg, który zawiera [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield), i wskazać typ operacji filtru jako [**FieldFilterOperation. StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation). Jest to jedyna operacja filtru pola obsługiwana przez punkt końcowy klientów. Należy również podać ciąg do filtrowania.

Następnie Utwórz wystąpienie obiektu [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) , aby przekazać go do zapytania przez wywołanie metody [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) i przekazanie jej do filtru. BuildSimplyQuery to tylko jeden z typów zapytań obsługiwanych przez klasę [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) .

Na koniec aby wykonać filtr i uzyskać wynik, należy najpierw użyć [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , aby uzyskać interfejs do operacji klienta partnera. Następnie Wywołaj [**zapytanie**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) lub metodę [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) .

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

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: FilterCustomers.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers? size = {size} &Filter = {Filter} http/1.1 |

### <a name="uri-parameters"></a>Parametry identyfikatora URI

Użyj następujących parametrów zapytania.

| Nazwa   | Typ   | Wymagane | Opis                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| size   | int    | Nie       | Liczba wyników do wyświetlenia w tym samym czasie. Ten parametr jest opcjonalny. |
| filter | filter | Tak      | Filtr, który ma zostać zastosowany do klientów. Musi to być ciąg zakodowany.              |

### <a name="filter-syntax"></a>Składnia filtru

Należy złożyć parametr filtru jako serię oddzielonych przecinkami par klucz-wartość. Każdy klucz i wartość muszą być osobno cytowane i oddzielone dwukropkiem. Cały filtr musi być zakodowany.

Niezakodowany przykład wygląda następująco:

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```

W poniższej tabeli opisano wymagane pary klucz-wartość:

| Klucz      | Wartość                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| Pole    | Pole do filtrowania. Prawidłowe wartości można znaleźć w [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield). |
| Wartość    | Wartość, według której ma zostać przefiltrowana. Wielkość liter jest ignorowana.                                                                |
| Operator | Operator, który ma zostać zastosowany. Jedyną obsługiwaną wartością tego scenariusza klienta jest "zaczyna się \_ od".                            |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

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

Jeśli to się powiedzie, ta metoda zwraca kolekcję pasujących zasobów [klienta](customer-resources.md#customer) w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

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
