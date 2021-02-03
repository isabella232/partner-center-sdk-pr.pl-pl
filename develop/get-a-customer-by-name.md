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
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a><span data-ttu-id="57e28-105">Pobieranie listy klientów filtrowanych według pola wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="57e28-105">Get a list of customers filtered by a search field</span></span>

<span data-ttu-id="57e28-106">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="57e28-106">**Applies To**</span></span>

- <span data-ttu-id="57e28-107">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="57e28-107">Partner Center</span></span>
- <span data-ttu-id="57e28-108">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="57e28-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="57e28-109">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="57e28-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="57e28-110">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="57e28-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="57e28-111">Pobiera kolekcję zasobów [klienta](customer-resources.md#customer) , które pasują do filtru.</span><span class="sxs-lookup"><span data-stu-id="57e28-111">Gets a collection of [Customer](customer-resources.md#customer) resources that match a filter.</span></span> <span data-ttu-id="57e28-112">Opcjonalnie można ustawić rozmiar strony.</span><span class="sxs-lookup"><span data-stu-id="57e28-112">You can optionally set a page size.</span></span> <span data-ttu-id="57e28-113">Można filtrować według nazwy firmy, domeny, odsprzedawcy pośredniego lub pośredniego dostawcy rozwiązań w chmurze (CSP).</span><span class="sxs-lookup"><span data-stu-id="57e28-113">You can filter by company name, domain, indirect reseller, or indirect cloud solution provider (CSP).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57e28-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="57e28-114">Prerequisites</span></span>

- <span data-ttu-id="57e28-115">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="57e28-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="57e28-116">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="57e28-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="57e28-117">Filtr skonstruowany przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="57e28-117">A user-constructed filter.</span></span>

## <a name="c"></a><span data-ttu-id="57e28-118">C\#</span><span class="sxs-lookup"><span data-stu-id="57e28-118">C\#</span></span>

<span data-ttu-id="57e28-119">Aby uzyskać kolekcję klientów pasujących do filtru, należy najpierw utworzyć wystąpienie obiektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) , aby utworzyć filtr.</span><span class="sxs-lookup"><span data-stu-id="57e28-119">To get a collection of customers that match a filter, first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object to create the filter.</span></span> <span data-ttu-id="57e28-120">Należy przekazać ciąg, który zawiera [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield), i wskazać typ operacji filtru jako [**FieldFilterOperation. StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation).</span><span class="sxs-lookup"><span data-stu-id="57e28-120">You'll need to pass a string that contains the [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield), and indicate the type of filter operation as [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation).</span></span> <span data-ttu-id="57e28-121">Jest to jedyna operacja filtru pola obsługiwana przez punkt końcowy klientów.</span><span class="sxs-lookup"><span data-stu-id="57e28-121">That's the only field filter operation supported by the customers end point.</span></span> <span data-ttu-id="57e28-122">Należy również podać ciąg do filtrowania.</span><span class="sxs-lookup"><span data-stu-id="57e28-122">You'll also need to provide the string to filter by.</span></span>

<span data-ttu-id="57e28-123">Następnie Utwórz wystąpienie obiektu [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) , aby przekazać go do zapytania przez wywołanie metody [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) i przekazanie jej do filtru.</span><span class="sxs-lookup"><span data-stu-id="57e28-123">Next, instantiate an [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object to pass to the query by calling the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method and passing it the filter.</span></span> <span data-ttu-id="57e28-124">BuildSimplyQuery to tylko jeden z typów zapytań obsługiwanych przez klasę [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) .</span><span class="sxs-lookup"><span data-stu-id="57e28-124">BuildSimplyQuery is just one of the query types supported by the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.</span></span>

<span data-ttu-id="57e28-125">Na koniec aby wykonać filtr i uzyskać wynik, należy najpierw użyć [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , aby uzyskać interfejs do operacji klienta partnera.</span><span class="sxs-lookup"><span data-stu-id="57e28-125">Finally, to execute the filter and get the result, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="57e28-126">Następnie Wywołaj [**zapytanie**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) lub metodę [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) .</span><span class="sxs-lookup"><span data-stu-id="57e28-126">Then call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) method.</span></span>

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

<span data-ttu-id="57e28-127">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="57e28-127">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="57e28-128">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: FilterCustomers.cs</span><span class="sxs-lookup"><span data-stu-id="57e28-128">**Project**: Partner Center SDK Samples **Class**: FilterCustomers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="57e28-129">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="57e28-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="57e28-130">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="57e28-130">Request syntax</span></span>

| <span data-ttu-id="57e28-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="57e28-131">Method</span></span>  | <span data-ttu-id="57e28-132">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="57e28-132">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="57e28-133">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="57e28-133">**GET**</span></span> | <span data-ttu-id="57e28-134">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers? size = {size} &Filter = {Filter} http/1.1</span><span class="sxs-lookup"><span data-stu-id="57e28-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}&filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="57e28-135">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="57e28-135">URI parameters</span></span>

<span data-ttu-id="57e28-136">Użyj następujących parametrów zapytania.</span><span class="sxs-lookup"><span data-stu-id="57e28-136">Use the following query parameters.</span></span>

| <span data-ttu-id="57e28-137">Nazwa</span><span class="sxs-lookup"><span data-stu-id="57e28-137">Name</span></span>   | <span data-ttu-id="57e28-138">Typ</span><span class="sxs-lookup"><span data-stu-id="57e28-138">Type</span></span>   | <span data-ttu-id="57e28-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="57e28-139">Required</span></span> | <span data-ttu-id="57e28-140">Opis</span><span class="sxs-lookup"><span data-stu-id="57e28-140">Description</span></span>                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| <span data-ttu-id="57e28-141">size</span><span class="sxs-lookup"><span data-stu-id="57e28-141">size</span></span>   | <span data-ttu-id="57e28-142">int</span><span class="sxs-lookup"><span data-stu-id="57e28-142">int</span></span>    | <span data-ttu-id="57e28-143">Nie</span><span class="sxs-lookup"><span data-stu-id="57e28-143">No</span></span>       | <span data-ttu-id="57e28-144">Liczba wyników do wyświetlenia w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="57e28-144">The number of results to be displayed at one time.</span></span> <span data-ttu-id="57e28-145">Ten parametr jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="57e28-145">This parameter is optional.</span></span> |
| <span data-ttu-id="57e28-146">filter</span><span class="sxs-lookup"><span data-stu-id="57e28-146">filter</span></span> | <span data-ttu-id="57e28-147">filter</span><span class="sxs-lookup"><span data-stu-id="57e28-147">filter</span></span> | <span data-ttu-id="57e28-148">Tak</span><span class="sxs-lookup"><span data-stu-id="57e28-148">Yes</span></span>      | <span data-ttu-id="57e28-149">Filtr, który ma zostać zastosowany do klientów.</span><span class="sxs-lookup"><span data-stu-id="57e28-149">The filter to apply to customers.</span></span> <span data-ttu-id="57e28-150">Musi to być ciąg zakodowany.</span><span class="sxs-lookup"><span data-stu-id="57e28-150">This must be an encoded string.</span></span>              |

### <a name="filter-syntax"></a><span data-ttu-id="57e28-151">Składnia filtru</span><span class="sxs-lookup"><span data-stu-id="57e28-151">Filter Syntax</span></span>

<span data-ttu-id="57e28-152">Należy złożyć parametr filtru jako serię oddzielonych przecinkami par klucz-wartość.</span><span class="sxs-lookup"><span data-stu-id="57e28-152">You must compose the filter parameter as a series of comma separated, key-value pairs.</span></span> <span data-ttu-id="57e28-153">Każdy klucz i wartość muszą być osobno cytowane i oddzielone dwukropkiem.</span><span class="sxs-lookup"><span data-stu-id="57e28-153">Each key and value must be individually quoted and separated by a colon.</span></span> <span data-ttu-id="57e28-154">Cały filtr musi być zakodowany.</span><span class="sxs-lookup"><span data-stu-id="57e28-154">The entire filter must be encoded.</span></span>

<span data-ttu-id="57e28-155">Niezakodowany przykład wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="57e28-155">An unencoded example looks like this:</span></span>

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```

<span data-ttu-id="57e28-156">W poniższej tabeli opisano wymagane pary klucz-wartość:</span><span class="sxs-lookup"><span data-stu-id="57e28-156">The following table describes the required key-value pairs:</span></span>

| <span data-ttu-id="57e28-157">Klucz</span><span class="sxs-lookup"><span data-stu-id="57e28-157">Key</span></span>      | <span data-ttu-id="57e28-158">Wartość</span><span class="sxs-lookup"><span data-stu-id="57e28-158">Value</span></span>                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="57e28-159">Pole</span><span class="sxs-lookup"><span data-stu-id="57e28-159">Field</span></span>    | <span data-ttu-id="57e28-160">Pole do filtrowania.</span><span class="sxs-lookup"><span data-stu-id="57e28-160">The field to filter.</span></span> <span data-ttu-id="57e28-161">Prawidłowe wartości można znaleźć w [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield).</span><span class="sxs-lookup"><span data-stu-id="57e28-161">The valid values can be found in [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield).</span></span> |
| <span data-ttu-id="57e28-162">Wartość</span><span class="sxs-lookup"><span data-stu-id="57e28-162">Value</span></span>    | <span data-ttu-id="57e28-163">Wartość, według której ma zostać przefiltrowana.</span><span class="sxs-lookup"><span data-stu-id="57e28-163">The value to filter by.</span></span> <span data-ttu-id="57e28-164">Wielkość liter jest ignorowana.</span><span class="sxs-lookup"><span data-stu-id="57e28-164">The case of the value is ignored.</span></span>                                                                |
| <span data-ttu-id="57e28-165">Operator</span><span class="sxs-lookup"><span data-stu-id="57e28-165">Operator</span></span> | <span data-ttu-id="57e28-166">Operator, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="57e28-166">The operator to apply.</span></span> <span data-ttu-id="57e28-167">Jedyną obsługiwaną wartością tego scenariusza klienta jest "zaczyna się \_ od".</span><span class="sxs-lookup"><span data-stu-id="57e28-167">The only supported value for this customer scenario is "starts\_with".</span></span>                            |

### <a name="request-headers"></a><span data-ttu-id="57e28-168">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="57e28-168">Request headers</span></span>

<span data-ttu-id="57e28-169">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="57e28-169">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="57e28-170">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="57e28-170">Request body</span></span>

<span data-ttu-id="57e28-171">Brak.</span><span class="sxs-lookup"><span data-stu-id="57e28-171">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="57e28-172">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="57e28-172">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="57e28-173">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="57e28-173">REST response</span></span>

<span data-ttu-id="57e28-174">Jeśli to się powiedzie, ta metoda zwraca kolekcję pasujących zasobów [klienta](customer-resources.md#customer) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="57e28-174">If successful, this method returns a collection of matching [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="57e28-175">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="57e28-175">Response success and error codes</span></span>

<span data-ttu-id="57e28-176">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="57e28-176">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="57e28-177">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="57e28-177">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="57e28-178">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="57e28-178">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="57e28-179">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="57e28-179">Response example</span></span>

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
