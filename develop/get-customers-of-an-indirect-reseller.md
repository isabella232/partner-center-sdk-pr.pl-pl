---
title: Pobieranie klientów odsprzedawcy pośredniego
description: Jak uzyskać listę klientów odsprzedawcy pośredniego.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e05248b16b803529258de806c25b117f3104ad2a
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446330"
---
# <a name="get-customers-of-an-indirect-reseller"></a><span data-ttu-id="2912e-103">Pobieranie klientów odsprzedawcy pośredniego</span><span class="sxs-lookup"><span data-stu-id="2912e-103">Get customers of an indirect reseller</span></span>

<span data-ttu-id="2912e-104">Jak uzyskać listę klientów odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="2912e-104">How to get a list of the customers of an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2912e-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2912e-105">Prerequisites</span></span>

- <span data-ttu-id="2912e-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2912e-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2912e-107">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2912e-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="2912e-108">Identyfikator dzierżawy odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="2912e-108">The tenant identifier of the indirect reseller.</span></span>

## <a name="c"></a><span data-ttu-id="2912e-109">C\#</span><span class="sxs-lookup"><span data-stu-id="2912e-109">C\#</span></span>

<span data-ttu-id="2912e-110">Aby uzyskać kolekcję klientów, którzy mają relację z określonym odsprzedawcą pośrednim, najpierw utwórz wystąpienia obiektu [**SimpleFieldFilter,**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) aby utworzyć filtr.</span><span class="sxs-lookup"><span data-stu-id="2912e-110">To get a collection of customers that have a relationship with the specified indirect reseller, first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object to create the filter.</span></span> <span data-ttu-id="2912e-111">Należy przekazać członka wyliczenia [**CustomerSearchField.IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) przekonwertowanego na ciąg i wskazać typ operacji filtrowania [**FieldFilterOperation.StartsWith.**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation)</span><span class="sxs-lookup"><span data-stu-id="2912e-111">You'll need to pass the [**CustomerSearchField.IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) enumeration member converted to a string, and indicate [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) as the type of filter operation.</span></span> <span data-ttu-id="2912e-112">Należy również podać identyfikator dzierżawy odsprzedawcy pośredniego, według których ma być filtrowany.</span><span class="sxs-lookup"><span data-stu-id="2912e-112">You'll also need to provide the tenant identifier of the indirect reseller to filter by.</span></span>

<span data-ttu-id="2912e-113">Następnie należy utworzyć wystąpienia obiektu [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) w celu przekazania do zapytania, wywołując metodę [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) i przekazując do niego filtr.</span><span class="sxs-lookup"><span data-stu-id="2912e-113">Next, instantiate an [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object to pass to the query by calling the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method and passing it the filter.</span></span> <span data-ttu-id="2912e-114">BuildSimplyQuery to tylko jeden z typów zapytań obsługiwanych przez [**klasę QueryFactory.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory)</span><span class="sxs-lookup"><span data-stu-id="2912e-114">BuildSimplyQuery is just one of the query types supported by the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.</span></span>

<span data-ttu-id="2912e-115">Aby wykonać filtr i uzyskać wynik, najpierw użyj funkcji [**IAggregatePartner.Customers,**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) aby uzyskać interfejs do operacji klienta partnera.</span><span class="sxs-lookup"><span data-stu-id="2912e-115">To execute the filter and get the result, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="2912e-116">Następnie wywołaj [**metodę Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) lub [**QueryAsync.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync)</span><span class="sxs-lookup"><span data-stu-id="2912e-116">Then call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) method.</span></span>

<span data-ttu-id="2912e-117">Aby utworzyć moduł wyliczający do przechodzenia wyników stronicowania, pobierz interfejs fabryki modułu wyliczania kolekcji klientów z właściwości [**IAggregatePartner.Enumerators.Customers,**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) a następnie wywołaj wywołanie create [**,**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create)jak pokazano w poniższym kodzie, przekazując zmienną, która przechowuje kolekcję klientów.</span><span class="sxs-lookup"><span data-stu-id="2912e-117">To create an enumerator for traversing paged results, get the customer collection enumerator factory interface from the [**IAggregatePartner.Enumerators.Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) property, and then call [**Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create), as shown in the code below, passing the variable that holds the customer collection.</span></span>

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

<span data-ttu-id="2912e-118">**Przykład:** [Aplikacja testowa konsoli](console-test-app.md)**Project**: zestaw SDK Centrum partnerskiego Samples **Class**: GetCustomersOfIndirectReseller.cs</span><span class="sxs-lookup"><span data-stu-id="2912e-118">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetCustomersOfIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2912e-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="2912e-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2912e-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="2912e-120">Request syntax</span></span>

| <span data-ttu-id="2912e-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="2912e-121">Method</span></span>  | <span data-ttu-id="2912e-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="2912e-122">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="2912e-123">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="2912e-123">**GET**</span></span> | <span data-ttu-id="2912e-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}?filter={filter} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2912e-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}?filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="2912e-125">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="2912e-125">URI parameter</span></span>

<span data-ttu-id="2912e-126">Aby utworzyć żądanie, użyj następujących parametrów zapytania.</span><span class="sxs-lookup"><span data-stu-id="2912e-126">Use the following query parameters to create the request.</span></span>

| <span data-ttu-id="2912e-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="2912e-127">Name</span></span>   | <span data-ttu-id="2912e-128">Typ</span><span class="sxs-lookup"><span data-stu-id="2912e-128">Type</span></span>   | <span data-ttu-id="2912e-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2912e-129">Required</span></span> | <span data-ttu-id="2912e-130">Opis</span><span class="sxs-lookup"><span data-stu-id="2912e-130">Description</span></span>                                                                                                                                                                                                                                                                                   |
|--------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2912e-131">size</span><span class="sxs-lookup"><span data-stu-id="2912e-131">size</span></span>   | <span data-ttu-id="2912e-132">int</span><span class="sxs-lookup"><span data-stu-id="2912e-132">int</span></span>    | <span data-ttu-id="2912e-133">Nie</span><span class="sxs-lookup"><span data-stu-id="2912e-133">No</span></span>       | <span data-ttu-id="2912e-134">Liczba wyników, które mają być wyświetlane jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="2912e-134">The number of results to be displayed at one time.</span></span> <span data-ttu-id="2912e-135">Ten parametr jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="2912e-135">This parameter is optional.</span></span>                                                                                                                                                                                                                |
| <span data-ttu-id="2912e-136">filter</span><span class="sxs-lookup"><span data-stu-id="2912e-136">filter</span></span> | <span data-ttu-id="2912e-137">filter</span><span class="sxs-lookup"><span data-stu-id="2912e-137">filter</span></span> | <span data-ttu-id="2912e-138">Tak</span><span class="sxs-lookup"><span data-stu-id="2912e-138">Yes</span></span>      | <span data-ttu-id="2912e-139">Zapytanie filtruje wyszukiwanie.</span><span class="sxs-lookup"><span data-stu-id="2912e-139">The query that filters the search.</span></span> <span data-ttu-id="2912e-140">Aby pobrać klientów dla określonego odsprzedawcy pośredniego, należy wstawić identyfikator odsprzedawcy pośredniego oraz dołączyć i zakodować następujący ciąg: {"Pole":"IndirectReseller","Value":"{identyfikator odsprzedawcy pośredniego}","Operator":"rozpoczyna się \_ od"}.</span><span class="sxs-lookup"><span data-stu-id="2912e-140">To retrieve customers for a specified indirect reseller, you must insert the indirect reseller identifier and include and encode the following string: {"Field":"IndirectReseller","Value":"{indirect reseller identifier}","Operator":"starts\_with"}.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2912e-141">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="2912e-141">Request headers</span></span>

<span data-ttu-id="2912e-142">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2912e-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2912e-143">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="2912e-143">Request body</span></span>

<span data-ttu-id="2912e-144">Brak.</span><span class="sxs-lookup"><span data-stu-id="2912e-144">None.</span></span>

### <a name="request-example-encoded"></a><span data-ttu-id="2912e-145">Przykład żądania (zakodowany)</span><span class="sxs-lookup"><span data-stu-id="2912e-145">Request example (encoded)</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22IndirectReseller%22%2C%22Value%22%3A%22484e548c-f5f3-4528-93a9-c16c6373cb59%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="request-example-decoded"></a><span data-ttu-id="2912e-146">Przykładowe żądanie (zdekodowane)</span><span class="sxs-lookup"><span data-stu-id="2912e-146">Request example (decoded)</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter={"Field":"IndirectReseller","Value":"484e548c-f5f3-4528-93a9-c16c6373cb59","Operator":"starts_with"} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="2912e-147">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="2912e-147">REST response</span></span>

<span data-ttu-id="2912e-148">W przypadku powodzenia treść odpowiedzi zawiera informacje o klientach odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="2912e-148">If successful, the response body contains information about the reseller's customers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2912e-149">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2912e-149">Response success and error codes</span></span>

<span data-ttu-id="2912e-150">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="2912e-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2912e-151">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="2912e-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2912e-152">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2912e-152">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2912e-153">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2912e-153">Response example</span></span>

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
