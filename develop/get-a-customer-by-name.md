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
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a><span data-ttu-id="33999-105">Pobieranie listy klientów filtrowanych według pola wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="33999-105">Get a list of customers filtered by a search field</span></span>

<span data-ttu-id="33999-106">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="33999-106">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="33999-107">Pobiera kolekcję [zasobów klienta,](customer-resources.md#customer) które pasują do filtru.</span><span class="sxs-lookup"><span data-stu-id="33999-107">Gets a collection of [Customer](customer-resources.md#customer) resources that match a filter.</span></span> <span data-ttu-id="33999-108">Opcjonalnie możesz ustawić rozmiar strony.</span><span class="sxs-lookup"><span data-stu-id="33999-108">You can optionally set a page size.</span></span> <span data-ttu-id="33999-109">Możesz filtrować według nazwy firmy, domeny, odsprzedawcy pośredniego lub pośredniego dostawcy rozwiązań w chmurze (CSP).</span><span class="sxs-lookup"><span data-stu-id="33999-109">You can filter by company name, domain, indirect reseller, or indirect cloud solution provider (CSP).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33999-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="33999-110">Prerequisites</span></span>

- <span data-ttu-id="33999-111">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="33999-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="33999-112">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="33999-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="33999-113">Filtr skonstruowany przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="33999-113">A user-constructed filter.</span></span>

## <a name="c"></a><span data-ttu-id="33999-114">C\#</span><span class="sxs-lookup"><span data-stu-id="33999-114">C\#</span></span>

<span data-ttu-id="33999-115">Aby uzyskać kolekcję klientów, którzy pasują do filtru, najpierw utwórz obiekt [**SimpleFieldFilter,**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) aby utworzyć filtr.</span><span class="sxs-lookup"><span data-stu-id="33999-115">To get a collection of customers that match a filter, first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object to create the filter.</span></span> <span data-ttu-id="33999-116">Musisz przekazać ciąg zawierający pole [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)i wskazać typ operacji filtrowania jako [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation).</span><span class="sxs-lookup"><span data-stu-id="33999-116">You'll need to pass a string that contains the [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield), and indicate the type of filter operation as [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation).</span></span> <span data-ttu-id="33999-117">Jest to jedyna operacja filtrowania pól obsługiwana przez punkt końcowy klientów.</span><span class="sxs-lookup"><span data-stu-id="33999-117">That's the only field filter operation supported by the customers end point.</span></span> <span data-ttu-id="33999-118">Należy również podać ciąg, według których ma być filtrowany ciąg.</span><span class="sxs-lookup"><span data-stu-id="33999-118">You'll also need to provide the string to filter by.</span></span>

<span data-ttu-id="33999-119">Następnie zaimplestruj obiekt [**iQuery,**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) aby przekazać go do zapytania, wywołując metodę [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) i przekazując do niego filtr.</span><span class="sxs-lookup"><span data-stu-id="33999-119">Next, instantiate an [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object to pass to the query by calling the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method and passing it the filter.</span></span> <span data-ttu-id="33999-120">BuildSimplyQuery to tylko jeden z typów zapytań obsługiwanych przez [**klasę QueryFactory.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory)</span><span class="sxs-lookup"><span data-stu-id="33999-120">BuildSimplyQuery is just one of the query types supported by the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.</span></span>

<span data-ttu-id="33999-121">Na koniec, aby wykonać filtr i uzyskać wynik, najpierw użyj funkcji [**IAggregatePartner.Customers,**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) aby uzyskać interfejs dla operacji klienta partnera.</span><span class="sxs-lookup"><span data-stu-id="33999-121">Finally, to execute the filter and get the result, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="33999-122">Następnie wywołaj [**metodę Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) lub [**QueryAsync.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync)</span><span class="sxs-lookup"><span data-stu-id="33999-122">Then call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) method.</span></span>

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

<span data-ttu-id="33999-123">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="33999-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="33999-124">**Project:** zestaw SDK Centrum partnerskiego Samples Class : FilterCustomers.cs **(Klasa** przykładów zestaw SDK Centrum partnerskiego: FilterCustomers.cs)</span><span class="sxs-lookup"><span data-stu-id="33999-124">**Project**: Partner Center SDK Samples **Class**: FilterCustomers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="33999-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="33999-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="33999-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="33999-126">Request syntax</span></span>

| <span data-ttu-id="33999-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="33999-127">Method</span></span>  | <span data-ttu-id="33999-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="33999-128">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="33999-129">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="33999-129">**GET**</span></span> | <span data-ttu-id="33999-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}&filter={filter} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="33999-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}&filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="33999-131">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="33999-131">URI parameters</span></span>

<span data-ttu-id="33999-132">Użyj następujących parametrów zapytania.</span><span class="sxs-lookup"><span data-stu-id="33999-132">Use the following query parameters.</span></span>

| <span data-ttu-id="33999-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="33999-133">Name</span></span>   | <span data-ttu-id="33999-134">Typ</span><span class="sxs-lookup"><span data-stu-id="33999-134">Type</span></span>   | <span data-ttu-id="33999-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="33999-135">Required</span></span> | <span data-ttu-id="33999-136">Opis</span><span class="sxs-lookup"><span data-stu-id="33999-136">Description</span></span>                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| <span data-ttu-id="33999-137">size</span><span class="sxs-lookup"><span data-stu-id="33999-137">size</span></span>   | <span data-ttu-id="33999-138">int</span><span class="sxs-lookup"><span data-stu-id="33999-138">int</span></span>    | <span data-ttu-id="33999-139">Nie</span><span class="sxs-lookup"><span data-stu-id="33999-139">No</span></span>       | <span data-ttu-id="33999-140">Liczba wyników, które mają być wyświetlane jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="33999-140">The number of results to be displayed at one time.</span></span> <span data-ttu-id="33999-141">Ten parametr jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="33999-141">This parameter is optional.</span></span> |
| <span data-ttu-id="33999-142">filter</span><span class="sxs-lookup"><span data-stu-id="33999-142">filter</span></span> | <span data-ttu-id="33999-143">filter</span><span class="sxs-lookup"><span data-stu-id="33999-143">filter</span></span> | <span data-ttu-id="33999-144">Tak</span><span class="sxs-lookup"><span data-stu-id="33999-144">Yes</span></span>      | <span data-ttu-id="33999-145">Filtr do zastosowania do klientów.</span><span class="sxs-lookup"><span data-stu-id="33999-145">The filter to apply to customers.</span></span> <span data-ttu-id="33999-146">Musi to być zakodowany ciąg.</span><span class="sxs-lookup"><span data-stu-id="33999-146">This must be an encoded string.</span></span>              |

### <a name="filter-syntax"></a><span data-ttu-id="33999-147">Składnia filtru</span><span class="sxs-lookup"><span data-stu-id="33999-147">Filter Syntax</span></span>

<span data-ttu-id="33999-148">Parametr filtru należy skomponować jako serię rozdzielonych przecinkami par klucz-wartość.</span><span class="sxs-lookup"><span data-stu-id="33999-148">You must compose the filter parameter as a series of comma separated, key-value pairs.</span></span> <span data-ttu-id="33999-149">Każdy klucz i wartość muszą być oddzielnie cytowane i oddzielone dwukropkiem.</span><span class="sxs-lookup"><span data-stu-id="33999-149">Each key and value must be individually quoted and separated by a colon.</span></span> <span data-ttu-id="33999-150">Cały filtr musi być zakodowany.</span><span class="sxs-lookup"><span data-stu-id="33999-150">The entire filter must be encoded.</span></span>

<span data-ttu-id="33999-151">Niezakodowany przykład wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="33999-151">An unencoded example looks like this:</span></span>

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```

<span data-ttu-id="33999-152">W poniższej tabeli opisano wymagane pary klucz-wartość:</span><span class="sxs-lookup"><span data-stu-id="33999-152">The following table describes the required key-value pairs:</span></span>

| <span data-ttu-id="33999-153">Klucz</span><span class="sxs-lookup"><span data-stu-id="33999-153">Key</span></span>      | <span data-ttu-id="33999-154">Wartość</span><span class="sxs-lookup"><span data-stu-id="33999-154">Value</span></span>                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="33999-155">Pole</span><span class="sxs-lookup"><span data-stu-id="33999-155">Field</span></span>    | <span data-ttu-id="33999-156">Pole do filtrowania.</span><span class="sxs-lookup"><span data-stu-id="33999-156">The field to filter.</span></span> <span data-ttu-id="33999-157">Prawidłowe wartości można znaleźć w [**customersearchfield**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield).</span><span class="sxs-lookup"><span data-stu-id="33999-157">The valid values can be found in [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield).</span></span> |
| <span data-ttu-id="33999-158">Wartość</span><span class="sxs-lookup"><span data-stu-id="33999-158">Value</span></span>    | <span data-ttu-id="33999-159">Wartość do filtrowania.</span><span class="sxs-lookup"><span data-stu-id="33999-159">The value to filter by.</span></span> <span data-ttu-id="33999-160">Przypadek wartości jest ignorowany.</span><span class="sxs-lookup"><span data-stu-id="33999-160">The case of the value is ignored.</span></span>                                                                |
| <span data-ttu-id="33999-161">Operator</span><span class="sxs-lookup"><span data-stu-id="33999-161">Operator</span></span> | <span data-ttu-id="33999-162">Operator do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="33999-162">The operator to apply.</span></span> <span data-ttu-id="33999-163">Jedyną obsługiwaną wartością w tym scenariuszu klienta jest "zaczyna \_ się od".</span><span class="sxs-lookup"><span data-stu-id="33999-163">The only supported value for this customer scenario is "starts\_with".</span></span>                            |

### <a name="request-headers"></a><span data-ttu-id="33999-164">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="33999-164">Request headers</span></span>

<span data-ttu-id="33999-165">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="33999-165">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="33999-166">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="33999-166">Request body</span></span>

<span data-ttu-id="33999-167">Brak.</span><span class="sxs-lookup"><span data-stu-id="33999-167">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="33999-168">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="33999-168">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="33999-169">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="33999-169">REST response</span></span>

<span data-ttu-id="33999-170">W przypadku powodzenia ta metoda zwraca kolekcję [pasujących zasobów](customer-resources.md#customer) klienta w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="33999-170">If successful, this method returns a collection of matching [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="33999-171">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="33999-171">Response success and error codes</span></span>

<span data-ttu-id="33999-172">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="33999-172">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="33999-173">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="33999-173">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="33999-174">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="33999-174">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="33999-175">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="33999-175">Response example</span></span>

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
