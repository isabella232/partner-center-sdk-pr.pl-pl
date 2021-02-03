---
title: Pobieranie rejestru aktywności w Centrum partnerskim
description: Jak pobrać rekord operacji wykonywanych przez użytkownika lub aplikację partnera w danym okresie czasu.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2f37eae8bb96c1c1e7008e8c566b085e25d8807d
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768229"
---
# <a name="get-a-record-of-partner-center-activity"></a><span data-ttu-id="c5c0f-103">Pobieranie rejestru aktywności w Centrum partnerskim</span><span class="sxs-lookup"><span data-stu-id="c5c0f-103">Get a record of Partner Center activity</span></span>

<span data-ttu-id="c5c0f-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="c5c0f-104">**Applies To**</span></span>

- <span data-ttu-id="c5c0f-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="c5c0f-105">Partner Center</span></span>
- <span data-ttu-id="c5c0f-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="c5c0f-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="c5c0f-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="c5c0f-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c5c0f-108">W tym artykule opisano sposób pobierania rekordu operacji wykonanych przez użytkownika lub aplikację partnera w określonym czasie.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-108">This article describes how to retrieve a record of operations that was performed by a partner user or application over a period of time.</span></span>

<span data-ttu-id="c5c0f-109">Użyj tego interfejsu API, aby pobrać rekordy inspekcji z ostatnich 30 dni od bieżącej daty lub dla zakresu dat określonego przez dołączenie daty rozpoczęcia i/lub daty zakończenia.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-109">Use this API to retrieve audit records for the previous 30 days from the current date, or for a date range specified by including the start date and/or the end date.</span></span> <span data-ttu-id="c5c0f-110">Należy jednak pamiętać, że ze względu na wydajność dostępność danych dziennika aktywności jest ograniczona do poprzednich 90 dni.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-110">Note, however, that for performance reasons activity log data availability is limited to the previous 90 days.</span></span> <span data-ttu-id="c5c0f-111">Żądania z datą rozpoczęcia większą niż 90 dni przed bieżącą datą otrzymają błędny wyjątek żądania (kod błędu: 400) i odpowiedni komunikat.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-111">Requests with a start date greater than 90 days prior to the current date will receive a bad request exception (error code: 400) and an appropriate message.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5c0f-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c5c0f-112">Prerequisites</span></span>

- <span data-ttu-id="c5c0f-113">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c5c0f-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c5c0f-114">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-114">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="c5c0f-115">C\#</span><span class="sxs-lookup"><span data-stu-id="c5c0f-115">C\#</span></span>

<span data-ttu-id="c5c0f-116">Aby pobrać rekord operacji Centrum partnerskiego, najpierw Ustal zakres dat dla rekordów, które chcesz pobrać.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-116">To retrieve a record of Partner Center operations, first establish the date range for the records you want to retrieve.</span></span> <span data-ttu-id="c5c0f-117">Poniższy przykład kodu używa tylko daty rozpoczęcia, ale można również dołączyć datę końcową.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-117">The following code example only uses a start date, but you can also include an end date.</span></span> <span data-ttu-id="c5c0f-118">Aby uzyskać więcej informacji, zobacz Metoda [**zapytania**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) .</span><span class="sxs-lookup"><span data-stu-id="c5c0f-118">For more information, see the [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) method.</span></span> <span data-ttu-id="c5c0f-119">Następnie należy utworzyć zmienne potrzebne dla typu filtru, który ma zostać zastosowany, i przypisać odpowiednie wartości.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-119">Next, create the variables you need for the type of filter you want to apply, and assign the appropriate values.</span></span> <span data-ttu-id="c5c0f-120">Na przykład aby przefiltrować według podciągu nazwy firmy, należy utworzyć zmienną do przechowywania podciągu.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-120">For example, to filter by company name substring, create a variable to hold the substring.</span></span> <span data-ttu-id="c5c0f-121">Aby odfiltrować według identyfikatora klienta, Utwórz zmienną do przechowywania identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-121">To filter by customer ID, create a variable to hold the ID.</span></span>

<span data-ttu-id="c5c0f-122">W poniższym przykładzie przedstawiono przykładowy kod służący do filtrowania według podciągu nazwy firmy, identyfikatora klienta lub typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-122">In the following example, sample code is provided to filter by a company name substring, customer ID, or resource type.</span></span> <span data-ttu-id="c5c0f-123">Wybierz jeden z nich i Dodaj komentarz do innych elementów.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-123">Choose one and comment out the others.</span></span> <span data-ttu-id="c5c0f-124">W każdym przypadku należy najpierw utworzyć wystąpienie obiektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) przy użyciu jego domyślnego [**konstruktora**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) do utworzenia filtru.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-124">In each case, you first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object using its default [**constructor**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) to create the filter.</span></span> <span data-ttu-id="c5c0f-125">Należy przekazać ciąg, który zawiera pole do wyszukania, i odpowiedni operator do zastosowania, jak pokazano.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-125">You'll need to pass a string that contains the field to search, and the appropriate operator to apply, as shown.</span></span> <span data-ttu-id="c5c0f-126">Należy również podać ciąg do filtrowania.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-126">You also must provide the string to filter by.</span></span>

<span data-ttu-id="c5c0f-127">Następnie użyj właściwości [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) , aby uzyskać interfejs do inspekcji operacji rejestrowania i wywołać metodę [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) lub [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) , aby wykonać filtr i pobrać kolekcję [**AuditRecord**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) reprezentującą pierwszą stronę wyniku.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-127">Next, use the [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) property to get an interface to audit record operations, and call the [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) method to execute the filter and get the collection of [**AuditRecord's**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) that represent the first page of the result.</span></span> <span data-ttu-id="c5c0f-128">Przekaż metodę, która jest datą początkową, opcjonalną datą końcową, która nie jest używana w przykładzie, i obiekt [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) , który reprezentuje zapytanie w jednostce.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-128">Pass the method the start date, an optional end date not used in the example here, and an [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object that represents a query on an entity.</span></span> <span data-ttu-id="c5c0f-129">Obiekt IQuery jest tworzony przez przekazanie wyżej utworzonego powyżej filtru do metody [](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) QueryFactory.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-129">The IQuery object is created by passing the filter created above to the [**QueryFactory's**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method.</span></span>

<span data-ttu-id="c5c0f-130">Gdy masz początkową stronę elementów, użyj metody [**Enumerators. AuditRecords. Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) , aby utworzyć moduł wyliczający, którego można użyć do iteracji przez pozostałe strony.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-130">Once you have the initial page of items, use the [**Enumerators.AuditRecords.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) method to create an enumerator that you can use to iterate through the remaining pages.</span></span>

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

<span data-ttu-id="c5c0f-131">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="c5c0f-131">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="c5c0f-132">**Projekt**: **folder** przykładów zestawu SDK Centrum partnerskiego: Inspekcja</span><span class="sxs-lookup"><span data-stu-id="c5c0f-132">**Project**: Partner Center SDK Samples **Folder**: Auditing</span></span>

## <a name="rest-request"></a><span data-ttu-id="c5c0f-133">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="c5c0f-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c5c0f-134">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="c5c0f-134">Request syntax</span></span>

| <span data-ttu-id="c5c0f-135">Metoda</span><span class="sxs-lookup"><span data-stu-id="c5c0f-135">Method</span></span>  | <span data-ttu-id="c5c0f-136">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="c5c0f-136">Request URI</span></span>                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c5c0f-137">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="c5c0f-137">**GET**</span></span> | <span data-ttu-id="c5c0f-138">[*{baseURL}*](partner-center-rest-urls.md)/V1/AuditRecords? StartDate = {STARTDATE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="c5c0f-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate} HTTP/1.1</span></span>                                                                                                     |
| <span data-ttu-id="c5c0f-139">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="c5c0f-139">**GET**</span></span> | <span data-ttu-id="c5c0f-140">[*{baseURL}*](partner-center-rest-urls.md)/V1/AuditRecords? StartDate = {startDate} &EndDate = {EndDate} http/1.1</span><span class="sxs-lookup"><span data-stu-id="c5c0f-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate} HTTP/1.1</span></span>                                                                                   |
| <span data-ttu-id="c5c0f-141">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="c5c0f-141">**GET**</span></span> | <span data-ttu-id="c5c0f-142">[*{baseURL}*](partner-center-rest-urls.md)/V1/AuditRecords? startDated = {startDate} &EndDate = {endDate} &Filter = {"Field": "NazwaFirmy", "value": "{searchSubstring}", "operator": "substring"} http/1.1</span><span class="sxs-lookup"><span data-stu-id="c5c0f-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CompanyName","Value":"{searchSubstring}","Operator":"substring"} HTTP/1.1</span></span> |
| <span data-ttu-id="c5c0f-143">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="c5c0f-143">**GET**</span></span> | <span data-ttu-id="c5c0f-144">[*{baseURL}*](partner-center-rest-urls.md)/V1/AuditRecords? startDated = {startDate} &EndDate = {endDate} &Filter = {"Field": "CustomerID", "value": "{CustomerID}", "operator": "Equals"} http/1.1</span><span class="sxs-lookup"><span data-stu-id="c5c0f-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CustomerId","Value":"{customerId}","Operator":"equals"} HTTP/1.1</span></span>          |
| <span data-ttu-id="c5c0f-145">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="c5c0f-145">**GET**</span></span> | <span data-ttu-id="c5c0f-146">[*{baseURL}*](partner-center-rest-urls.md)/V1/AuditRecords? startDated = {startDate} &EndDate = {endDate} &Filter = {"Field": "ResourceType", "value": "{ResourceType}", "operator": "Equals"} http/1.1</span><span class="sxs-lookup"><span data-stu-id="c5c0f-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"ResourceType","Value":"{resourceType}","Operator":"equals"} HTTP/1.1</span></span>      |

### <a name="uri-parameter"></a><span data-ttu-id="c5c0f-147">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="c5c0f-147">URI parameter</span></span>

<span data-ttu-id="c5c0f-148">Podczas tworzenia żądania Użyj następujących parametrów zapytania.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-148">Use the following query parameters when creating the request.</span></span>

| <span data-ttu-id="c5c0f-149">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c5c0f-149">Name</span></span>      | <span data-ttu-id="c5c0f-150">Typ</span><span class="sxs-lookup"><span data-stu-id="c5c0f-150">Type</span></span>   | <span data-ttu-id="c5c0f-151">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c5c0f-151">Required</span></span> | <span data-ttu-id="c5c0f-152">Opis</span><span class="sxs-lookup"><span data-stu-id="c5c0f-152">Description</span></span>                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c5c0f-153">startDate</span><span class="sxs-lookup"><span data-stu-id="c5c0f-153">startDate</span></span> | <span data-ttu-id="c5c0f-154">date</span><span class="sxs-lookup"><span data-stu-id="c5c0f-154">date</span></span>   | <span data-ttu-id="c5c0f-155">Nie</span><span class="sxs-lookup"><span data-stu-id="c5c0f-155">No</span></span>       | <span data-ttu-id="c5c0f-156">Data rozpoczęcia w formacie RRRR-MM-DD.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-156">The start date in yyyy-mm-dd format.</span></span> <span data-ttu-id="c5c0f-157">Jeśli żaden nie jest podany, zestaw wyników będzie domyślnie miał 30 dni przed datą żądania.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-157">If none is provided, the result set will default to 30 days prior to the request date.</span></span> <span data-ttu-id="c5c0f-158">Ten parametr jest opcjonalny w przypadku podania filtru.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-158">This parameter is optional when a filter is supplied.</span></span>                                          |
| <span data-ttu-id="c5c0f-159">endDate</span><span class="sxs-lookup"><span data-stu-id="c5c0f-159">endDate</span></span>   | <span data-ttu-id="c5c0f-160">date</span><span class="sxs-lookup"><span data-stu-id="c5c0f-160">date</span></span>   | <span data-ttu-id="c5c0f-161">Nie</span><span class="sxs-lookup"><span data-stu-id="c5c0f-161">No</span></span>       | <span data-ttu-id="c5c0f-162">Data zakończenia w formacie RRRR-MM-DD.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-162">The end date in yyyy-mm-dd format.</span></span> <span data-ttu-id="c5c0f-163">Ten parametr jest opcjonalny w przypadku podania filtru.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-163">This parameter is optional when a filter is supplied.</span></span> <span data-ttu-id="c5c0f-164">Gdy data zakończenia jest pomijana lub ma wartość null, żądanie zwróci wartość maksymalnego okna lub używa dzisiaj jako daty zakończenia, w zależności od tego, która wartość jest mniejsza.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-164">When the end date is omitted or set to null, the request returns the max window or uses today as the end date, whichever is less.</span></span> |
| <span data-ttu-id="c5c0f-165">filter</span><span class="sxs-lookup"><span data-stu-id="c5c0f-165">filter</span></span>    | <span data-ttu-id="c5c0f-166">ciąg</span><span class="sxs-lookup"><span data-stu-id="c5c0f-166">string</span></span> | <span data-ttu-id="c5c0f-167">Nie</span><span class="sxs-lookup"><span data-stu-id="c5c0f-167">No</span></span>       | <span data-ttu-id="c5c0f-168">Filtr, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-168">The filter to apply.</span></span> <span data-ttu-id="c5c0f-169">Ten parametr musi być zakodowanym ciągiem.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-169">This parameter must be an encoded string.</span></span> <span data-ttu-id="c5c0f-170">Ten parametr jest opcjonalny, gdy podano datę początkową lub datę końcową.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-170">This parameter is optional when the start date or end date are supplied.</span></span>                                                                                              |

### <a name="filter-syntax"></a><span data-ttu-id="c5c0f-171">Składnia filtru</span><span class="sxs-lookup"><span data-stu-id="c5c0f-171">Filter syntax</span></span>
<span data-ttu-id="c5c0f-172">Należy złożyć parametr filtru jako serię oddzielonych przecinkami par klucz-wartość.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-172">You must compose the filter parameter as a series of comma separated, key-value pairs.</span></span> <span data-ttu-id="c5c0f-173">Każdy klucz i wartość muszą być osobno cytowane i oddzielone dwukropkiem.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-173">Each key and value must be individually quoted and separated by a colon.</span></span> <span data-ttu-id="c5c0f-174">Cały filtr musi być zakodowany.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-174">The entire filter must be encoded.</span></span>

<span data-ttu-id="c5c0f-175">Niezakodowany przykład wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="c5c0f-175">An unencoded example looks like this:</span></span>

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

<span data-ttu-id="c5c0f-176">W poniższej tabeli opisano wymagane pary klucz-wartość:</span><span class="sxs-lookup"><span data-stu-id="c5c0f-176">The following table describes the required key-value pairs:</span></span>

| <span data-ttu-id="c5c0f-177">Klucz</span><span class="sxs-lookup"><span data-stu-id="c5c0f-177">Key</span></span>                 | <span data-ttu-id="c5c0f-178">Wartość</span><span class="sxs-lookup"><span data-stu-id="c5c0f-178">Value</span></span>                             |
|:--------------------|:----------------------------------|
| <span data-ttu-id="c5c0f-179">Pole</span><span class="sxs-lookup"><span data-stu-id="c5c0f-179">Field</span></span>               | <span data-ttu-id="c5c0f-180">Pole do filtrowania.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-180">The field to filter.</span></span> <span data-ttu-id="c5c0f-181">Obsługiwane wartości można znaleźć w [składni żądania](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span><span class="sxs-lookup"><span data-stu-id="c5c0f-181">The supported values can be found in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span></span>                                         |
| <span data-ttu-id="c5c0f-182">Wartość</span><span class="sxs-lookup"><span data-stu-id="c5c0f-182">Value</span></span>               | <span data-ttu-id="c5c0f-183">Wartość, według której ma zostać przefiltrowana.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-183">The value to filter by.</span></span> <span data-ttu-id="c5c0f-184">Wielkość liter jest ignorowana.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-184">The case of the value is ignored.</span></span> <span data-ttu-id="c5c0f-185">Następujące parametry wartości są obsługiwane, jak pokazano w [składni żądania](get-a-record-of-partner-center-activity-by-user.md#rest-request):</span><span class="sxs-lookup"><span data-stu-id="c5c0f-185">The following value parameters are supported as shown in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request):</span></span><br/><br/>                                                                <span data-ttu-id="c5c0f-186">*searchSubstring* — Zamień na nazwę firmy.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-186">*searchSubstring* - Replace with the name of the company.</span></span> <span data-ttu-id="c5c0f-187">Aby dopasować część nazwy firmy (na przykład, będzie ona pasować), można wprowadzić podciąg `bri` `Fabrikam, Inc` .</span><span class="sxs-lookup"><span data-stu-id="c5c0f-187">You can enter a substring to match part of the company name (for example, `bri` will match `Fabrikam, Inc`).</span></span><br/><span data-ttu-id="c5c0f-188">**Przykład:** `"Value":"bri"`</span><span class="sxs-lookup"><span data-stu-id="c5c0f-188">**Example:** `"Value":"bri"`</span></span><br/><br/>                                                                <span data-ttu-id="c5c0f-189">*customerId* -Zamień na ciąg z SFORMATOWANYm identyfikatorem GUID, który reprezentuje identyfikator klienta.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-189">*customerId* - Replace with a GUID formatted string that represents the customer identifier.</span></span><br/><span data-ttu-id="c5c0f-190">**Przykład:** `"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`</span><span class="sxs-lookup"><span data-stu-id="c5c0f-190">**Example:** `"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`</span></span><br/><br/>                                                                                        <span data-ttu-id="c5c0f-191">*ResourceType* — Zamień na typ zasobu, dla którego mają zostać pobrane rekordy inspekcji (na przykład subskrypcja).</span><span class="sxs-lookup"><span data-stu-id="c5c0f-191">*resourceType* - Replace with the type of resource for which to retrieve audit records (for example, Subscription).</span></span> <span data-ttu-id="c5c0f-192">Dostępne typy zasobów są zdefiniowane w elemencie [ResourceType](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype).</span><span class="sxs-lookup"><span data-stu-id="c5c0f-192">The available resource types are defined in [ResourceType](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype).</span></span><br/><span data-ttu-id="c5c0f-193">**Przykład:** `"Value":"Subscription"`</span><span class="sxs-lookup"><span data-stu-id="c5c0f-193">**Example:** `"Value":"Subscription"`</span></span>                                 |
| <span data-ttu-id="c5c0f-194">Operator</span><span class="sxs-lookup"><span data-stu-id="c5c0f-194">Operator</span></span>          | <span data-ttu-id="c5c0f-195">Operator, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-195">The operator to apply.</span></span> <span data-ttu-id="c5c0f-196">Obsługiwane operatory można znaleźć w [składni żądania](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span><span class="sxs-lookup"><span data-stu-id="c5c0f-196">The supported operators can be found in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="c5c0f-197">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="c5c0f-197">Request headers</span></span>

- <span data-ttu-id="c5c0f-198">Aby uzyskać więcej informacji, zobacz [nagłówki REST programu Part Center](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="c5c0f-198">See [Parter Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="c5c0f-199">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="c5c0f-199">Request body</span></span>

<span data-ttu-id="c5c0f-200">Brak.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-200">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c5c0f-201">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="c5c0f-201">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="c5c0f-202">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="c5c0f-202">REST response</span></span>

<span data-ttu-id="c5c0f-203">Jeśli to się powiedzie, ta metoda zwraca zestaw działań, które spełniają filtry.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-203">If successful, this method returns a set of activities that meet the filters.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c5c0f-204">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c5c0f-204">Response success and error codes</span></span>

<span data-ttu-id="c5c0f-205">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-205">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c5c0f-206">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="c5c0f-206">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c5c0f-207">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c5c0f-207">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c5c0f-208">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c5c0f-208">Response example</span></span>

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