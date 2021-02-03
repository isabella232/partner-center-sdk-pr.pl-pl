---
title: Pobieranie klientów odsprzedawcy pośredniego
description: Jak uzyskać listę klientów pośredniego odsprzedawcy.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e4219f544a74bb3f34ec3aefe08cf18eed77fd42
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768333"
---
# <a name="get-customers-of-an-indirect-reseller"></a><span data-ttu-id="ce0cc-103">Pobieranie klientów odsprzedawcy pośredniego</span><span class="sxs-lookup"><span data-stu-id="ce0cc-103">Get customers of an indirect reseller</span></span>

<span data-ttu-id="ce0cc-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="ce0cc-104">**Applies To**</span></span>

- <span data-ttu-id="ce0cc-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="ce0cc-105">Partner Center</span></span>

<span data-ttu-id="ce0cc-106">Jak uzyskać listę klientów pośredniego odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="ce0cc-106">How to get a list of the customers of an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce0cc-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ce0cc-107">Prerequisites</span></span>

- <span data-ttu-id="ce0cc-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ce0cc-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ce0cc-109">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ce0cc-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="ce0cc-110">Identyfikator dzierżawy pośredniego odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="ce0cc-110">The tenant identifier of the indirect reseller.</span></span>

## <a name="c"></a><span data-ttu-id="ce0cc-111">C\#</span><span class="sxs-lookup"><span data-stu-id="ce0cc-111">C\#</span></span>

<span data-ttu-id="ce0cc-112">Aby uzyskać kolekcję klientów, którzy mają relację z określonym odsprzedawcą średnią, należy najpierw utworzyć wystąpienie obiektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) , aby utworzyć filtr.</span><span class="sxs-lookup"><span data-stu-id="ce0cc-112">To get a collection of customers that have a relationship with the specified indirect reseller, first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object to create the filter.</span></span> <span data-ttu-id="ce0cc-113">Należy przekazać element członkowski wyliczenia [**CustomerSearchField. IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) przekonwertowany do ciągu i wskazać [**FieldFilterOperation. StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) jako typ operacji filtrowania.</span><span class="sxs-lookup"><span data-stu-id="ce0cc-113">You'll need to pass the [**CustomerSearchField.IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) enumeration member converted to a string, and indicate [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) as the type of filter operation.</span></span> <span data-ttu-id="ce0cc-114">Należy również podać identyfikator dzierżawy pośredniego odsprzedawcy, według którego ma zostać przefiltrowany.</span><span class="sxs-lookup"><span data-stu-id="ce0cc-114">You'll also need to provide the tenant identifier of the indirect reseller to filter by.</span></span>

<span data-ttu-id="ce0cc-115">Następnie Utwórz wystąpienie obiektu [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) , aby przekazać go do zapytania przez wywołanie metody [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) i przekazanie jej do filtru.</span><span class="sxs-lookup"><span data-stu-id="ce0cc-115">Next, instantiate an [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object to pass to the query by calling the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method and passing it the filter.</span></span> <span data-ttu-id="ce0cc-116">BuildSimplyQuery to tylko jeden z typów zapytań obsługiwanych przez klasę [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) .</span><span class="sxs-lookup"><span data-stu-id="ce0cc-116">BuildSimplyQuery is just one of the query types supported by the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.</span></span>

<span data-ttu-id="ce0cc-117">Aby wykonać filtr i uzyskać wynik, należy najpierw użyć [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , aby uzyskać interfejs do operacji klienta partnera.</span><span class="sxs-lookup"><span data-stu-id="ce0cc-117">To execute the filter and get the result, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="ce0cc-118">Następnie Wywołaj [**zapytanie**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) lub metodę [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) .</span><span class="sxs-lookup"><span data-stu-id="ce0cc-118">Then call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) method.</span></span>

<span data-ttu-id="ce0cc-119">Aby utworzyć moduł wyliczający do przechodzenia z stronicowanymi wynikami, Pobierz interfejs fabryki modułu wyliczającego kolekcji klienta z właściwości [**IAggregatePartner. Enumerators. Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) , a następnie Wywołaj polecenie [**Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create), jak pokazano w poniższym kodzie, przekazując zmienną, która zawiera kolekcję klientów.</span><span class="sxs-lookup"><span data-stu-id="ce0cc-119">To create an enumerator for traversing paged results, get the customer collection enumerator factory interface from the [**IAggregatePartner.Enumerators.Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) property, and then call [**Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create), as shown in the code below, passing the variable that holds the customer collection.</span></span>

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

<span data-ttu-id="ce0cc-120">**Przykład**:**projekt** [aplikacji testowej konsoli](console-test-app.md): **Klasa** przykładów zestawu SDK Centrum partnerskiego: GetCustomersOfIndirectReseller.cs</span><span class="sxs-lookup"><span data-stu-id="ce0cc-120">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetCustomersOfIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="ce0cc-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="ce0cc-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ce0cc-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="ce0cc-122">Request syntax</span></span>

| <span data-ttu-id="ce0cc-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="ce0cc-123">Method</span></span>  | <span data-ttu-id="ce0cc-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="ce0cc-124">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="ce0cc-125">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="ce0cc-125">**GET**</span></span> | <span data-ttu-id="ce0cc-126">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers? size = {size}? Filter = {Filter} http/1.1</span><span class="sxs-lookup"><span data-stu-id="ce0cc-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}?filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="ce0cc-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="ce0cc-127">URI parameter</span></span>

<span data-ttu-id="ce0cc-128">Użyj następujących parametrów zapytania, aby utworzyć żądanie.</span><span class="sxs-lookup"><span data-stu-id="ce0cc-128">Use the following query parameters to create the request.</span></span>

| <span data-ttu-id="ce0cc-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="ce0cc-129">Name</span></span>   | <span data-ttu-id="ce0cc-130">Typ</span><span class="sxs-lookup"><span data-stu-id="ce0cc-130">Type</span></span>   | <span data-ttu-id="ce0cc-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ce0cc-131">Required</span></span> | <span data-ttu-id="ce0cc-132">Opis</span><span class="sxs-lookup"><span data-stu-id="ce0cc-132">Description</span></span>                                                                                                                                                                                                                                                                                   |
|--------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ce0cc-133">size</span><span class="sxs-lookup"><span data-stu-id="ce0cc-133">size</span></span>   | <span data-ttu-id="ce0cc-134">int</span><span class="sxs-lookup"><span data-stu-id="ce0cc-134">int</span></span>    | <span data-ttu-id="ce0cc-135">Nie</span><span class="sxs-lookup"><span data-stu-id="ce0cc-135">No</span></span>       | <span data-ttu-id="ce0cc-136">Liczba wyników do wyświetlenia w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="ce0cc-136">The number of results to be displayed at one time.</span></span> <span data-ttu-id="ce0cc-137">Ten parametr jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="ce0cc-137">This parameter is optional.</span></span>                                                                                                                                                                                                                |
| <span data-ttu-id="ce0cc-138">filter</span><span class="sxs-lookup"><span data-stu-id="ce0cc-138">filter</span></span> | <span data-ttu-id="ce0cc-139">filter</span><span class="sxs-lookup"><span data-stu-id="ce0cc-139">filter</span></span> | <span data-ttu-id="ce0cc-140">Tak</span><span class="sxs-lookup"><span data-stu-id="ce0cc-140">Yes</span></span>      | <span data-ttu-id="ce0cc-141">Zapytanie filtrujące wyszukiwanie.</span><span class="sxs-lookup"><span data-stu-id="ce0cc-141">The query that filters the search.</span></span> <span data-ttu-id="ce0cc-142">Aby pobrać klientów dla określonego odsprzedawcy pośredniego, należy wstawić pośredni identyfikator odsprzedawcy i dołączyć i kodować następujący ciąg: {"pole": "IndirectReseller", "value": "{pośredni odsprzedawca identyfikator}", "operator": "zaczyna \_ się od"}.</span><span class="sxs-lookup"><span data-stu-id="ce0cc-142">To retrieve customers for a specified indirect reseller, you must insert the indirect reseller identifier and include and encode the following string: {"Field":"IndirectReseller","Value":"{indirect reseller identifier}","Operator":"starts\_with"}.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ce0cc-143">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="ce0cc-143">Request headers</span></span>

<span data-ttu-id="ce0cc-144">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ce0cc-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ce0cc-145">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="ce0cc-145">Request body</span></span>

<span data-ttu-id="ce0cc-146">Brak.</span><span class="sxs-lookup"><span data-stu-id="ce0cc-146">None.</span></span>

### <a name="request-example-encoded"></a><span data-ttu-id="ce0cc-147">Przykład żądania (zakodowany)</span><span class="sxs-lookup"><span data-stu-id="ce0cc-147">Request example (encoded)</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22IndirectReseller%22%2C%22Value%22%3A%22484e548c-f5f3-4528-93a9-c16c6373cb59%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="request-example-decoded"></a><span data-ttu-id="ce0cc-148">Przykład żądania (zdekodowany)</span><span class="sxs-lookup"><span data-stu-id="ce0cc-148">Request example (decoded)</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter={"Field":"IndirectReseller","Value":"484e548c-f5f3-4528-93a9-c16c6373cb59","Operator":"starts_with"} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="ce0cc-149">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="ce0cc-149">REST response</span></span>

<span data-ttu-id="ce0cc-150">Jeśli to się powiedzie, treść odpowiedzi zawiera informacje o klientach odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="ce0cc-150">If successful, the response body contains information about the reseller's customers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ce0cc-151">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ce0cc-151">Response success and error codes</span></span>

<span data-ttu-id="ce0cc-152">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="ce0cc-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ce0cc-153">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="ce0cc-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ce0cc-154">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ce0cc-154">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ce0cc-155">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ce0cc-155">Response example</span></span>

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
