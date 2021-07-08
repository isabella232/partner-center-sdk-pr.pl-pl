---
title: Pobieranie rejestru aktywności w Centrum partnerskim
description: Pobieranie rekordu operacji wykonywanego przez użytkownika partnera lub aplikację w czasie.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: aec933d4b681d99080619505792bde56bdd25580
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873975"
---
# <a name="get-a-record-of-partner-center-activity"></a><span data-ttu-id="3668f-103">Pobieranie rejestru aktywności w Centrum partnerskim</span><span class="sxs-lookup"><span data-stu-id="3668f-103">Get a record of Partner Center activity</span></span>

<span data-ttu-id="3668f-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3668f-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3668f-105">W tym artykule opisano sposób pobierania rekordu operacji, które były wykonywane przez użytkownika partnera lub aplikację w czasie.</span><span class="sxs-lookup"><span data-stu-id="3668f-105">This article describes how to retrieve a record of operations that was performed by a partner user or application over a period of time.</span></span>

<span data-ttu-id="3668f-106">Ten interfejs API umożliwia pobieranie rekordów inspekcji z ostatnich 30 dni od bieżącej daty lub dla zakresu dat określonego przez uwzględnienia daty rozpoczęcia i/lub daty zakończenia.</span><span class="sxs-lookup"><span data-stu-id="3668f-106">Use this API to retrieve audit records for the previous 30 days from the current date, or for a date range specified by including the start date and/or the end date.</span></span> <span data-ttu-id="3668f-107">Należy jednak pamiętać, że ze względu na wydajność dostępność danych dziennika aktywności jest ograniczona do poprzednich 90 dni.</span><span class="sxs-lookup"><span data-stu-id="3668f-107">Note, however, that for performance reasons activity log data availability is limited to the previous 90 days.</span></span> <span data-ttu-id="3668f-108">Żądania z datą rozpoczęcia większą niż 90 dni przed bieżącą datą otrzymają wyjątek złego żądania (kod błędu: 400) i odpowiedni komunikat.</span><span class="sxs-lookup"><span data-stu-id="3668f-108">Requests with a start date greater than 90 days prior to the current date will receive a bad request exception (error code: 400) and an appropriate message.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3668f-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3668f-109">Prerequisites</span></span>

- <span data-ttu-id="3668f-110">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3668f-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3668f-111">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3668f-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="3668f-112">C\#</span><span class="sxs-lookup"><span data-stu-id="3668f-112">C\#</span></span>

<span data-ttu-id="3668f-113">Aby pobrać rekord operacji Partner Center, najpierw ustal zakres dat dla rekordów, które chcesz pobrać.</span><span class="sxs-lookup"><span data-stu-id="3668f-113">To retrieve a record of Partner Center operations, first establish the date range for the records you want to retrieve.</span></span> <span data-ttu-id="3668f-114">W poniższym przykładzie kodu użyto tylko daty rozpoczęcia, ale można również uwzględnić datę zakończenia.</span><span class="sxs-lookup"><span data-stu-id="3668f-114">The following code example only uses a start date, but you can also include an end date.</span></span> <span data-ttu-id="3668f-115">Aby uzyskać więcej informacji, zobacz [**metodę**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) Query.</span><span class="sxs-lookup"><span data-stu-id="3668f-115">For more information, see the [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) method.</span></span> <span data-ttu-id="3668f-116">Następnie utwórz zmienne potrzebne dla typu filtru, który chcesz zastosować, i przypisz odpowiednie wartości.</span><span class="sxs-lookup"><span data-stu-id="3668f-116">Next, create the variables you need for the type of filter you want to apply, and assign the appropriate values.</span></span> <span data-ttu-id="3668f-117">Aby na przykład filtrować według podciągu nazwy firmy, utwórz zmienną do przechowywania podciągu.</span><span class="sxs-lookup"><span data-stu-id="3668f-117">For example, to filter by company name substring, create a variable to hold the substring.</span></span> <span data-ttu-id="3668f-118">Aby filtrować według identyfikatora klienta, utwórz zmienną do przechowywania identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="3668f-118">To filter by customer ID, create a variable to hold the ID.</span></span>

<span data-ttu-id="3668f-119">W poniższym przykładzie podano przykładowy kod do filtrowania według podciągu nazwy firmy, identyfikatora klienta lub typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="3668f-119">In the following example, sample code is provided to filter by a company name substring, customer ID, or resource type.</span></span> <span data-ttu-id="3668f-120">Wybierz jedną z nich i zakłoń pozostałe.</span><span class="sxs-lookup"><span data-stu-id="3668f-120">Choose one and comment out the others.</span></span> <span data-ttu-id="3668f-121">W każdym przypadku należy najpierw utworzyć obiekt [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) przy użyciu jego domyślnego [**konstruktora**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) w celu utworzenia filtru.</span><span class="sxs-lookup"><span data-stu-id="3668f-121">In each case, you first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object using its default [**constructor**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) to create the filter.</span></span> <span data-ttu-id="3668f-122">Musisz przekazać ciąg zawierający pole do wyszukania oraz odpowiedni operator do zastosowania, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="3668f-122">You'll need to pass a string that contains the field to search, and the appropriate operator to apply, as shown.</span></span> <span data-ttu-id="3668f-123">Należy również podać ciąg do filtrowania.</span><span class="sxs-lookup"><span data-stu-id="3668f-123">You also must provide the string to filter by.</span></span>

<span data-ttu-id="3668f-124">Następnie użyj właściwości [**AuditRecords,**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) aby uzyskać interfejs do inspekcji operacji na rekordach, i wywołaj metodę [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) lub [**QueryAsync,**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) aby wykonać filtr i pobrać kolekcję rekordów [**AuditRecord**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) reprezentujących pierwszą stronę wyniku.</span><span class="sxs-lookup"><span data-stu-id="3668f-124">Next, use the [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) property to get an interface to audit record operations, and call the [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) method to execute the filter and get the collection of [**AuditRecord's**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) that represent the first page of the result.</span></span> <span data-ttu-id="3668f-125">Przekaż metodę data rozpoczęcia, opcjonalną datę końcową, która nie została użyta w tym przykładzie, oraz obiekt [**IQuery,**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) który reprezentuje zapytanie w jednostce.</span><span class="sxs-lookup"><span data-stu-id="3668f-125">Pass the method the start date, an optional end date not used in the example here, and an [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object that represents a query on an entity.</span></span> <span data-ttu-id="3668f-126">Obiekt IQuery jest tworzony przez przekazanie utworzonego powyżej filtru do metody [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) w [**obiekcie QueryFactory.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory)</span><span class="sxs-lookup"><span data-stu-id="3668f-126">The IQuery object is created by passing the filter created above to the [**QueryFactory's**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method.</span></span>

<span data-ttu-id="3668f-127">Po utworzeniu początkowej strony elementów użyj metody [**Enumerators.AuditRecords.Create,**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) aby utworzyć moduł wyliczający, który będzie można użyć do iterowania po pozostałych stronach.</span><span class="sxs-lookup"><span data-stu-id="3668f-127">Once you have the initial page of items, use the [**Enumerators.AuditRecords.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) method to create an enumerator that you can use to iterate through the remaining pages.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var startDate = new DateTime(DateTime.Now.Year, DateTime.Now.Month, 01);

// First perform the query, then get the enumerator. Choose one of the following and comment out the other two.

// To retrieve audit records by company name substring (for example "bri" matches "Fabrikam, Inc.").
var searchSubstring="bri";
var filter = new SimpleFieldFilter(AuditRecordSearchField.CompanyName.ToString(), FieldFilterOperation.Substring, searchSubstring);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

// To retrieve audit records by customer ID.
var customerId="0c39d6d5-c70d-4c55-bc02-f620844f3fd1";
var filter = new SimpleFieldFilter(AuditRecordSearchField.CustomerId.ToString(), FieldFilterOperation.Equals, customerId);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

// To retrieve audit records by resource type.
int resourceTypeInt = 3; // Subscription Resource.
string searchField = Enum.GetName(typeof(ResourceType), resourceTypeInt);
var filter = new SimpleFieldFilter(AuditRecordSearchField.ResourceType.ToString(), FieldFilterOperation.Equals, searchField);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

var auditRecordEnumerator = partnerOperations.Enumerators.AuditRecords.Create(auditRecordsPage);

int pageNumber = 1;
while (auditRecordEnumerator.HasValue)
{
    // Work with the current page.
    foreach (var c in auditRecordEnumerator.Current.Items)
    {
        // Display some info, such as operation type, operation date, and operation status.
        Console.WriteLine(string.Format("{0} {1} {2}.", c.OperationType, c.OperationDate, c.OperationStatus));
    }

    // Get the next page of audit records.
    auditRecordEnumerator.Next();
}
```

<span data-ttu-id="3668f-128">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="3668f-128">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="3668f-129">**Project:** zestaw SDK Centrum partnerskiego Przykłady **folderu:** Inspekcja</span><span class="sxs-lookup"><span data-stu-id="3668f-129">**Project**: Partner Center SDK Samples **Folder**: Auditing</span></span>

## <a name="rest-request"></a><span data-ttu-id="3668f-130">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="3668f-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3668f-131">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="3668f-131">Request syntax</span></span>

| <span data-ttu-id="3668f-132">Metoda</span><span class="sxs-lookup"><span data-stu-id="3668f-132">Method</span></span>  | <span data-ttu-id="3668f-133">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="3668f-133">Request URI</span></span>                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3668f-134">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="3668f-134">**GET**</span></span> | <span data-ttu-id="3668f-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3668f-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate} HTTP/1.1</span></span>                                                                                                     |
| <span data-ttu-id="3668f-136">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="3668f-136">**GET**</span></span> | <span data-ttu-id="3668f-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3668f-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate} HTTP/1.1</span></span>                                                                                   |
| <span data-ttu-id="3668f-138">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="3668f-138">**GET**</span></span> | <span data-ttu-id="3668f-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CompanyName","Value":"{searchSubstring}","Operator":"substring"} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3668f-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CompanyName","Value":"{searchSubstring}","Operator":"substring"} HTTP/1.1</span></span> |
| <span data-ttu-id="3668f-140">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="3668f-140">**GET**</span></span> | <span data-ttu-id="3668f-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CustomerId","Value":"{customerId}","Operator":"equals"} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3668f-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CustomerId","Value":"{customerId}","Operator":"equals"} HTTP/1.1</span></span>          |
| <span data-ttu-id="3668f-142">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="3668f-142">**GET**</span></span> | <span data-ttu-id="3668f-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"ResourceType","Value":"{resourceType}","Operator":"equals"} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3668f-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"ResourceType","Value":"{resourceType}","Operator":"equals"} HTTP/1.1</span></span>      |

### <a name="uri-parameter"></a><span data-ttu-id="3668f-144">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="3668f-144">URI parameter</span></span>

<span data-ttu-id="3668f-145">Podczas tworzenia żądania użyj następujących parametrów zapytania.</span><span class="sxs-lookup"><span data-stu-id="3668f-145">Use the following query parameters when creating the request.</span></span>

| <span data-ttu-id="3668f-146">Nazwa</span><span class="sxs-lookup"><span data-stu-id="3668f-146">Name</span></span>      | <span data-ttu-id="3668f-147">Typ</span><span class="sxs-lookup"><span data-stu-id="3668f-147">Type</span></span>   | <span data-ttu-id="3668f-148">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3668f-148">Required</span></span> | <span data-ttu-id="3668f-149">Opis</span><span class="sxs-lookup"><span data-stu-id="3668f-149">Description</span></span>                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3668f-150">Startdate</span><span class="sxs-lookup"><span data-stu-id="3668f-150">startDate</span></span> | <span data-ttu-id="3668f-151">data</span><span class="sxs-lookup"><span data-stu-id="3668f-151">date</span></span>   | <span data-ttu-id="3668f-152">Nie</span><span class="sxs-lookup"><span data-stu-id="3668f-152">No</span></span>       | <span data-ttu-id="3668f-153">Data rozpoczęcia w formacie yyyy-mm-dd.</span><span class="sxs-lookup"><span data-stu-id="3668f-153">The start date in yyyy-mm-dd format.</span></span> <span data-ttu-id="3668f-154">Jeśli żadna wartość nie zostanie podany, zestaw wyników zostanie ustawiony domyślnie na 30 dni przed datą żądania.</span><span class="sxs-lookup"><span data-stu-id="3668f-154">If none is provided, the result set will default to 30 days prior to the request date.</span></span> <span data-ttu-id="3668f-155">Ten parametr jest opcjonalny, gdy jest podany filtr.</span><span class="sxs-lookup"><span data-stu-id="3668f-155">This parameter is optional when a filter is supplied.</span></span>                                          |
| <span data-ttu-id="3668f-156">Enddate</span><span class="sxs-lookup"><span data-stu-id="3668f-156">endDate</span></span>   | <span data-ttu-id="3668f-157">data</span><span class="sxs-lookup"><span data-stu-id="3668f-157">date</span></span>   | <span data-ttu-id="3668f-158">Nie</span><span class="sxs-lookup"><span data-stu-id="3668f-158">No</span></span>       | <span data-ttu-id="3668f-159">Data końcowa w formacie yyyy-mm-dd.</span><span class="sxs-lookup"><span data-stu-id="3668f-159">The end date in yyyy-mm-dd format.</span></span> <span data-ttu-id="3668f-160">Ten parametr jest opcjonalny, gdy jest podany filtr.</span><span class="sxs-lookup"><span data-stu-id="3668f-160">This parameter is optional when a filter is supplied.</span></span> <span data-ttu-id="3668f-161">Gdy data zakończenia zostanie pominięta lub ustawiona na wartość null, żądanie zwróci maksymalne okno lub użyje dzisiaj jako daty zakończenia, w zależności od tego, która wartość jest mniejsza.</span><span class="sxs-lookup"><span data-stu-id="3668f-161">When the end date is omitted or set to null, the request returns the max window or uses today as the end date, whichever is less.</span></span> |
| <span data-ttu-id="3668f-162">filter</span><span class="sxs-lookup"><span data-stu-id="3668f-162">filter</span></span>    | <span data-ttu-id="3668f-163">ciąg</span><span class="sxs-lookup"><span data-stu-id="3668f-163">string</span></span> | <span data-ttu-id="3668f-164">Nie</span><span class="sxs-lookup"><span data-stu-id="3668f-164">No</span></span>       | <span data-ttu-id="3668f-165">Filtr do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="3668f-165">The filter to apply.</span></span> <span data-ttu-id="3668f-166">Ten parametr musi być zakodowanym ciągiem.</span><span class="sxs-lookup"><span data-stu-id="3668f-166">This parameter must be an encoded string.</span></span> <span data-ttu-id="3668f-167">Ten parametr jest opcjonalny, gdy podano datę rozpoczęcia lub datę zakończenia.</span><span class="sxs-lookup"><span data-stu-id="3668f-167">This parameter is optional when the start date or end date are supplied.</span></span>                                                                                              |

### <a name="filter-syntax"></a><span data-ttu-id="3668f-168">Składnia filtru</span><span class="sxs-lookup"><span data-stu-id="3668f-168">Filter syntax</span></span>
<span data-ttu-id="3668f-169">Parametr filtru należy skomponować jako serię rozdzielonych przecinkami par klucz-wartość.</span><span class="sxs-lookup"><span data-stu-id="3668f-169">You must compose the filter parameter as a series of comma separated, key-value pairs.</span></span> <span data-ttu-id="3668f-170">Każdy klucz i wartość muszą być oddzielnie cytowane i oddzielone dwukropkiem.</span><span class="sxs-lookup"><span data-stu-id="3668f-170">Each key and value must be individually quoted and separated by a colon.</span></span> <span data-ttu-id="3668f-171">Cały filtr musi być zakodowany.</span><span class="sxs-lookup"><span data-stu-id="3668f-171">The entire filter must be encoded.</span></span>

<span data-ttu-id="3668f-172">Niezakodowany przykład wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="3668f-172">An unencoded example looks like this:</span></span>

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

<span data-ttu-id="3668f-173">W poniższej tabeli opisano wymagane pary klucz-wartość:</span><span class="sxs-lookup"><span data-stu-id="3668f-173">The following table describes the required key-value pairs:</span></span>

| <span data-ttu-id="3668f-174">Klucz</span><span class="sxs-lookup"><span data-stu-id="3668f-174">Key</span></span>                 | <span data-ttu-id="3668f-175">Wartość</span><span class="sxs-lookup"><span data-stu-id="3668f-175">Value</span></span>                             |
|:--------------------|:----------------------------------|
| <span data-ttu-id="3668f-176">Pole</span><span class="sxs-lookup"><span data-stu-id="3668f-176">Field</span></span>               | <span data-ttu-id="3668f-177">Pole do filtrowania.</span><span class="sxs-lookup"><span data-stu-id="3668f-177">The field to filter.</span></span> <span data-ttu-id="3668f-178">Obsługiwane wartości można znaleźć w tece [Request syntax (Składnia żądania).](get-a-record-of-partner-center-activity-by-user.md#rest-request)</span><span class="sxs-lookup"><span data-stu-id="3668f-178">The supported values can be found in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span></span>                                         |
| <span data-ttu-id="3668f-179">Wartość</span><span class="sxs-lookup"><span data-stu-id="3668f-179">Value</span></span>               | <span data-ttu-id="3668f-180">Wartość do filtrowania.</span><span class="sxs-lookup"><span data-stu-id="3668f-180">The value to filter by.</span></span> <span data-ttu-id="3668f-181">Przypadek wartości jest ignorowany.</span><span class="sxs-lookup"><span data-stu-id="3668f-181">The case of the value is ignored.</span></span> <span data-ttu-id="3668f-182">Obsługiwane są następujące parametry wartości, jak pokazano w [tece Request syntax (Składnia żądania):](get-a-record-of-partner-center-activity-by-user.md#rest-request)</span><span class="sxs-lookup"><span data-stu-id="3668f-182">The following value parameters are supported as shown in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request):</span></span><br/><br/>                                                                <span data-ttu-id="3668f-183">*searchSubstring* — zastąp nazwą firmy.</span><span class="sxs-lookup"><span data-stu-id="3668f-183">*searchSubstring* - Replace with the name of the company.</span></span> <span data-ttu-id="3668f-184">Możesz wprowadzić podciąg, aby dopasować część nazwy firmy (na przykład `bri` będzie odpowiadać `Fabrikam, Inc` ).</span><span class="sxs-lookup"><span data-stu-id="3668f-184">You can enter a substring to match part of the company name (for example, `bri` will match `Fabrikam, Inc`).</span></span><br/><span data-ttu-id="3668f-185">**Przykład:**`"Value":"bri"`</span><span class="sxs-lookup"><span data-stu-id="3668f-185">**Example:** `"Value":"bri"`</span></span><br/><br/>                                                                <span data-ttu-id="3668f-186">*customerId* — zastąp ciąg ciągiem sformatowanym przy użyciu identyfikatora GUID, który reprezentuje identyfikator klienta.</span><span class="sxs-lookup"><span data-stu-id="3668f-186">*customerId* - Replace with a GUID formatted string that represents the customer identifier.</span></span><br/><span data-ttu-id="3668f-187">**Przykład:**`"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`</span><span class="sxs-lookup"><span data-stu-id="3668f-187">**Example:** `"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`</span></span><br/><br/>                                                                                        <span data-ttu-id="3668f-188">*resourceType* — zastąp typem zasobu, dla którego mają być pobierane rekordy inspekcji (na przykład Subskrypcja).</span><span class="sxs-lookup"><span data-stu-id="3668f-188">*resourceType* - Replace with the type of resource for which to retrieve audit records (for example, Subscription).</span></span> <span data-ttu-id="3668f-189">Dostępne typy zasobów są zdefiniowane w [typie ResourceType](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype).</span><span class="sxs-lookup"><span data-stu-id="3668f-189">The available resource types are defined in [ResourceType](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype).</span></span><br/><span data-ttu-id="3668f-190">**Przykład:**`"Value":"Subscription"`</span><span class="sxs-lookup"><span data-stu-id="3668f-190">**Example:** `"Value":"Subscription"`</span></span>                                 |
| <span data-ttu-id="3668f-191">Operator</span><span class="sxs-lookup"><span data-stu-id="3668f-191">Operator</span></span>          | <span data-ttu-id="3668f-192">Operator do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="3668f-192">The operator to apply.</span></span> <span data-ttu-id="3668f-193">Obsługiwane operatory można znaleźć w tece [Request syntax (Składnia żądania).](get-a-record-of-partner-center-activity-by-user.md#rest-request)</span><span class="sxs-lookup"><span data-stu-id="3668f-193">The supported operators can be found in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="3668f-194">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="3668f-194">Request headers</span></span>

- <span data-ttu-id="3668f-195">Aby uzyskać więcej informacji, zobacz [Parter Center REST headers (Nagłówki REST centrum części).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3668f-195">For more information, see [Parter Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3668f-196">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="3668f-196">Request body</span></span>

<span data-ttu-id="3668f-197">Brak.</span><span class="sxs-lookup"><span data-stu-id="3668f-197">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3668f-198">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="3668f-198">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=6/1/2017%2012:00:00%20AM&filter=%7B%22Field%22:%22CustomerId%22,%22Value%22:%220c39d6d5-c70d-4c55-bc02-f620844f3fd1%22,%22Operator%22:%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893
MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="3668f-199">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="3668f-199">REST response</span></span>

<span data-ttu-id="3668f-200">W przypadku powodzenia ta metoda zwraca zestaw działań spełniających wymagania filtrów.</span><span class="sxs-lookup"><span data-stu-id="3668f-200">If successful, this method returns a set of activities that meet the filters.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3668f-201">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3668f-201">Response success and error codes</span></span>

<span data-ttu-id="3668f-202">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="3668f-202">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3668f-203">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="3668f-203">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3668f-204">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="3668f-204">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3668f-205">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3668f-205">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2859
Content-Type: application/json; charset=utf-8
MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14
MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893
MS-CV: 4xDKynq/zE2im0wj.0
MS-ServerId: 030011719
Date: Tue, 27 Jun 2017 22:19:46 GMT

{
    "totalCount": 2,
    "items": [{
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "0c39d6d5-c70d-4c55-bc02-f620844f3fd1",
            "customerName": "Relecloud",
            "userPrincipalName": "admin@domain.onmicrosoft.com",
            "resourceType": "order",
            "resourceNewValue": "{\"Id\":\"d51a052e-043c-4a2a-aa37-2bb938cef6c1\",\"ReferenceCustomerId\":\"0c39d6d5-c70d-4c55-bc02-f620844f3fd1\",\"BillingCycle\":\"none\",\"LineItems\":[{\"LineItemNumber\":0,\"OfferId\":\"C0BD2E08-11AC-4836-BDC7-3712E744922F\",\"SubscriptionId\":\"488745B5-2086-4912-802C-6ABB9F7C3638\",\"ParentSubscriptionId\":null,\"FriendlyName\":\"Office 365 Business Premium Trial\",\"Quantity\":25,\"PartnerIdOnRecord\":null,\"Links\":{\"Subscription\":{\"Uri\":\"/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638\",\"Method\":\"GET\",\"Headers\":[]}}}],\"CreationDate\":\"2017-06-15T15:56:04.077-07:00\",\"Links\":{\"Self\":{\"Uri\":\"/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/orders/d51a052e-043c-4a2a-aa37-2bb938cef6c1\",\"Method\":\"GET\",\"Headers\":[]}},\"Attributes\":{\"Etag\":\"eyJpZCI6ImQ1MWEwNTJlLTA0M2MtNGEyYS1hYTM3LTJiYjkzOGNlZjZjMSIsInZlcnNpb24iOjF9\",\"ObjectType\":\"Order\"}}",
            "operationType": "create_order",
            "operationDate": "2017-06-15T22:56:05.0589308Z",
            "operationStatus": "succeeded",
            "customizedData": [{
                    "key": "OrderId",
                    "value": "d51a052e-043c-4a2a-aa37-2bb938cef6c1"
                }, {
                    "key": "BillingCycle",
                    "value": "None"
                }, {
                    "key": "OfferId-0",
                    "value": "C0BD2E08-11AC-4836-BDC7-3712E744922F"
                }, {
                    "key": "SubscriptionId-0",
                    "value": "488745B5-2086-4912-802C-6ABB9F7C3638"
                }, {
                    "key": "SubscriptionName-0",
                    "value": "Office 365 Business Premium Trial"
                }, {
                    "key": "Quantity-0",
                    "value": "25"
                }, {
                    "key": "PartnerOnRecord-0",
                    "value": null
                }
            ],
            "attributes": {
                "objectType": "AuditRecord"
            }
        }, {
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "0c39d6d5-c70d-4c55-bc02-f620844f3fd1",
            "customerName": "Relecloud",
            "userPrincipalName": "admin@domain.onmicrosoft.com",
            "applicationId": "Partner Center Native App",
            "resourceType": "license",
            "resourceNewValue": "{\"LicensesToAssign\":[{\"ExcludedPlans\":null,\"SkuId\":\"efccb6f7-5641-4e0e-bd10-b4976e1bf68e\"}],\"LicensesToRemove\":null,\"LicenseWarnings\":[],\"Attributes\":{\"ObjectType\":\"LicenseUpdate\"}}",
            "operationType": "update_customer_user_licenses",
            "operationDate": "2017-06-01T20:09:07.0450483Z",
            "operationStatus": "succeeded",
            "customizedData": [{
                    "key": "CustomerUserId",
                    "value": "482e2152-4b49-48ec-b715-823365ce3d4c"
                }, {
                    "key": "AddedLicenseSkuId",
                    "value": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e"
                }
            ],
            "attributes": {
                "objectType": "AuditRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/auditrecords?startDate=2017-06-01&size=500&filter=%7B%22Field%22%3A%22CustomerId%22%2C%22Value%22%3A%220c39d6d5-c70d-4c55-bc02-f620844f3fd1%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```