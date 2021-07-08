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
# <a name="get-a-record-of-partner-center-activity"></a>Pobieranie rejestru aktywności w Centrum partnerskim

**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

W tym artykule opisano sposób pobierania rekordu operacji, które były wykonywane przez użytkownika partnera lub aplikację w czasie.

Ten interfejs API umożliwia pobieranie rekordów inspekcji z ostatnich 30 dni od bieżącej daty lub dla zakresu dat określonego przez uwzględnienia daty rozpoczęcia i/lub daty zakończenia. Należy jednak pamiętać, że ze względu na wydajność dostępność danych dziennika aktywności jest ograniczona do poprzednich 90 dni. Żądania z datą rozpoczęcia większą niż 90 dni przed bieżącą datą otrzymają wyjątek złego żądania (kod błędu: 400) i odpowiedni komunikat.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

## <a name="c"></a>C\#

Aby pobrać rekord operacji Partner Center, najpierw ustal zakres dat dla rekordów, które chcesz pobrać. W poniższym przykładzie kodu użyto tylko daty rozpoczęcia, ale można również uwzględnić datę zakończenia. Aby uzyskać więcej informacji, zobacz [**metodę**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) Query. Następnie utwórz zmienne potrzebne dla typu filtru, który chcesz zastosować, i przypisz odpowiednie wartości. Aby na przykład filtrować według podciągu nazwy firmy, utwórz zmienną do przechowywania podciągu. Aby filtrować według identyfikatora klienta, utwórz zmienną do przechowywania identyfikatora.

W poniższym przykładzie podano przykładowy kod do filtrowania według podciągu nazwy firmy, identyfikatora klienta lub typu zasobu. Wybierz jedną z nich i zakłoń pozostałe. W każdym przypadku należy najpierw utworzyć obiekt [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) przy użyciu jego domyślnego [**konstruktora**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) w celu utworzenia filtru. Musisz przekazać ciąg zawierający pole do wyszukania oraz odpowiedni operator do zastosowania, jak pokazano poniżej. Należy również podać ciąg do filtrowania.

Następnie użyj właściwości [**AuditRecords,**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) aby uzyskać interfejs do inspekcji operacji na rekordach, i wywołaj metodę [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) lub [**QueryAsync,**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) aby wykonać filtr i pobrać kolekcję rekordów [**AuditRecord**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) reprezentujących pierwszą stronę wyniku. Przekaż metodę data rozpoczęcia, opcjonalną datę końcową, która nie została użyta w tym przykładzie, oraz obiekt [**IQuery,**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) który reprezentuje zapytanie w jednostce. Obiekt IQuery jest tworzony przez przekazanie utworzonego powyżej filtru do metody [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) w [**obiekcie QueryFactory.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory)

Po utworzeniu początkowej strony elementów użyj metody [**Enumerators.AuditRecords.Create,**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) aby utworzyć moduł wyliczający, który będzie można użyć do iterowania po pozostałych stronach.

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

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** zestaw SDK Centrum partnerskiego Przykłady **folderu:** Inspekcja

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate} HTTP/1.1                                                                                                     |
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate} HTTP/1.1                                                                                   |
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CompanyName","Value":"{searchSubstring}","Operator":"substring"} HTTP/1.1 |
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CustomerId","Value":"{customerId}","Operator":"equals"} HTTP/1.1          |
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"ResourceType","Value":"{resourceType}","Operator":"equals"} HTTP/1.1      |

### <a name="uri-parameter"></a>Parametr URI

Podczas tworzenia żądania użyj następujących parametrów zapytania.

| Nazwa      | Typ   | Wymagane | Opis                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Startdate | data   | Nie       | Data rozpoczęcia w formacie yyyy-mm-dd. Jeśli żadna wartość nie zostanie podany, zestaw wyników zostanie ustawiony domyślnie na 30 dni przed datą żądania. Ten parametr jest opcjonalny, gdy jest podany filtr.                                          |
| Enddate   | data   | Nie       | Data końcowa w formacie yyyy-mm-dd. Ten parametr jest opcjonalny, gdy jest podany filtr. Gdy data zakończenia zostanie pominięta lub ustawiona na wartość null, żądanie zwróci maksymalne okno lub użyje dzisiaj jako daty zakończenia, w zależności od tego, która wartość jest mniejsza. |
| filter    | ciąg | Nie       | Filtr do zastosowania. Ten parametr musi być zakodowanym ciągiem. Ten parametr jest opcjonalny, gdy podano datę rozpoczęcia lub datę zakończenia.                                                                                              |

### <a name="filter-syntax"></a>Składnia filtru
Parametr filtru należy skomponować jako serię rozdzielonych przecinkami par klucz-wartość. Każdy klucz i wartość muszą być oddzielnie cytowane i oddzielone dwukropkiem. Cały filtr musi być zakodowany.

Niezakodowany przykład wygląda następująco:

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

W poniższej tabeli opisano wymagane pary klucz-wartość:

| Klucz                 | Wartość                             |
|:--------------------|:----------------------------------|
| Pole               | Pole do filtrowania. Obsługiwane wartości można znaleźć w tece [Request syntax (Składnia żądania).](get-a-record-of-partner-center-activity-by-user.md#rest-request)                                         |
| Wartość               | Wartość do filtrowania. Przypadek wartości jest ignorowany. Obsługiwane są następujące parametry wartości, jak pokazano w [tece Request syntax (Składnia żądania):](get-a-record-of-partner-center-activity-by-user.md#rest-request)<br/><br/>                                                                *searchSubstring* — zastąp nazwą firmy. Możesz wprowadzić podciąg, aby dopasować część nazwy firmy (na przykład `bri` będzie odpowiadać `Fabrikam, Inc` ).<br/>**Przykład:**`"Value":"bri"`<br/><br/>                                                                *customerId* — zastąp ciąg ciągiem sformatowanym przy użyciu identyfikatora GUID, który reprezentuje identyfikator klienta.<br/>**Przykład:**`"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`<br/><br/>                                                                                        *resourceType* — zastąp typem zasobu, dla którego mają być pobierane rekordy inspekcji (na przykład Subskrypcja). Dostępne typy zasobów są zdefiniowane w [typie ResourceType](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype).<br/>**Przykład:**`"Value":"Subscription"`                                 |
| Operator          | Operator do zastosowania. Obsługiwane operatory można znaleźć w tece [Request syntax (Składnia żądania).](get-a-record-of-partner-center-activity-by-user.md#rest-request)   |

### <a name="request-headers"></a>Nagłówki żądań

- Aby uzyskać więcej informacji, zobacz [Parter Center REST headers (Nagłówki REST centrum części).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

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

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca zestaw działań spełniających wymagania filtrów.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)

### <a name="response-example"></a>Przykład odpowiedzi

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