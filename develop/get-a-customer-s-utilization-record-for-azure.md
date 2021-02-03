---
title: Pobieranie rekordów dotyczących wykorzystania platformy Azure przez klienta
description: Korzystając z interfejsu API wykorzystania platformy Azure, można uzyskać rekordy wykorzystania subskrypcji platformy Azure klienta przez określony czas.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bcdeb51b04039fd05b923150c85119385c0537e0
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768102"
---
# <a name="get-a-customers-utilization-records-for-azure"></a>Pobieranie rekordów dotyczących wykorzystania platformy Azure przez klienta

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Możesz uzyskać rekordy wykorzystania subskrypcji platformy Azure klienta przez określony czas przy użyciu interfejsu API użycia platformy Azure.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji.

Ten interfejs API zwraca codziennie i co godzinę użycie nieklasyfikowane dla dowolnego przedziału czasu. Jednak *ten interfejs API nie jest obsługiwany w przypadku planów platformy Azure*. Jeśli masz plan platformy Azure, zapoznaj się z artykułem [Pobierz fakturę za rozliczane opłaty za wiersze](get-invoice-unbilled-consumption-lineitems.md) i [Pobierz faktury za użycie](get-invoice-billed-consumption-lineitems.md) . W tych artykułach opisano, jak uzyskać zużycie znamionowe na poziomie dziennym dla każdego z zasobów. To użycie stawki jest równoznaczne z codziennymi danymi ziarna, które są udostępniane przez interfejs API użycia platformy Azure. Aby pobrać dane użycia, należy użyć identyfikatora faktury. Można też użyć bieżących i poprzednich okresów, aby uzyskać szacowane oszacowania użycia. *Dane o godzinowych ziarnach i dowolnych filtrach zakresów dat nie są obecnie obsługiwane w przypadku zasobów subskrypcji planu platformy Azure*.

## <a name="azure-utilization-api"></a>Interfejs API użycia platformy Azure

Ten interfejs API wykorzystania platformy Azure zapewnia dostęp do rekordów użycia w okresie, który reprezentuje, kiedy wykorzystanie zostało zgłoszone w systemie rozliczeniowym. Zapewnia dostęp do tych samych danych użycia, które są używane do tworzenia i obliczania pliku uzgadniania. Nie ma jednak informacji o logice pliku uzgodnienia systemu rozliczeń. Nie należy oczekiwać, że wyniki podsumowania plików są zgodne z wynikami pobranymi z tego interfejsu API dokładnie dla tego samego okresu.

Na przykład system rozliczeń pobiera te same dane dotyczące użycia i stosuje reguły opóźnienia, aby określić, co jest uwzględnione w pliku uzgadniania. Gdy okres rozliczeniowy zostanie zamknięty, wszystkie użycie do końca dnia, w którym kończy się okres rozliczeniowy, zostanie uwzględniony w pliku uzgodnienia. Każde późniejsze użycie w okresie rozliczeniowym, które jest zgłaszane w ciągu 24 godzin po zakończeniu okresu rozliczeniowego, jest uwzględniane w następnym pliku uzgodnienia. Aby uzyskać reguły dotyczące opóźnień związanych z naliczaniem partnera, zobacz [pobieranie danych dotyczących zużycia dla subskrypcji platformy Azure](/previous-versions/azure/reference/mt219001(v=azure.100)).

Ten interfejs API REST jest stronicowany. Jeśli ładunek odpowiedzi jest większy niż jedna strona, należy wykonać kolejne łącze, aby uzyskać następną stronę rekordów użycia.

## <a name="c"></a>C\#

Aby uzyskać rekordy użycia platformy Azure:

1. Pobierz identyfikator klienta i Identyfikator subskrypcji.

2. Wywołaj metodę [**IAzureUtilizationCollection. Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) , aby zwrócić element [**resourcecollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) , który zawiera rekordy użycia.

3. Uzyskaj moduł wyliczający rekordu wykorzystania platformy Azure, aby przechodzenie przez strony użycia. Ten krok jest wymagany, ponieważ jest stronicowana kolekcja zasobów.

- **Przykład**: [aplikacja testowa konsoli](console-test-app.md)
- **Projekt**: przykłady dla zestawu SDK Centrum partnerskiego
- **Klasa**: GetAzureSubscriptionUtilization.cs

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

IPartner partner = PartnerService.Instance.CreatePartnerOperations(credentials);

// Retrieve the utilization records for the last year in pages of 100 records.
var utilizationRecords = partner.Customers[customerId].Subscriptions[subscriptionId].Utilization.Azure.Query(
    DateTimeOffset.Now.AddYears(-1),
    DateTimeOffset.Now,
    size: 100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages.
var utilizationRecordEnumerator = partner.Enumerators.Utilization.Azure.Create(utilizationRecords);

while (utilizationRecordEnumerator.HasValue)
{
    //
    // Insert code here to work with this page.
    //

    // Get the next page.
    utilizationRecordEnumerator.Next();
}
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Aby uzyskać rekordy użycia platformy Azure, musisz najpierw mieć identyfikator klienta i Identyfikator subskrypcji. Następnie należy wywołać funkcję **IAzureUtilizationCollection. Query** w celu zwrócenia elementu **resourcecollection** , który zawiera rekordy użycia. Ponieważ kolekcja zasobów jest stronicowana, należy uzyskać moduł wyliczający rekordy wykorzystania platformy Azure, aby przechodzenie przez strony użycia.

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;

ResourceCollection<AzureUtilizationRecord> utilizationRecords = partnerOperations.getCustomers()
  .byId(customerId).getSubscriptions().byId(subscriptionId)
  .getUtilization().getAzure().query(
      new DateTime().minusYears(1),
      new DateTime(),
      AzureUtilizationGranularity.Daily,
      true,
      100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages
IResourceCollectionEnumerator<ResourceCollection<AzureUtilizationRecord>> utilizationRecordEnumerator =
    partnerOperations.getEnumerators().getUtilization().getAzure().create(utilizationRecords);

while (utilizationRecordEnumerator.hasValue())
{
    //
    // Insert code here to work with this page.
    //

    // get the next page
    utilizationRecordEnumerator.next();
}
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Aby uzyskać rekordy użycia platformy Azure, musisz najpierw mieć identyfikator klienta i Identyfikator subskrypcji. Następnie Wywołaj polecenie [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md). To polecenie zwróci wszystkie rekordy dostępne w określonym przedziale czasu.

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania |
|------- | ----------- |
| **Pobierz** | *{baseURL}*/V1/Customers/{Customer-tenant-ID}/subscriptions/{Subscription-ID}/utilizations/Azure? \_ czas rozpoczęcia = {Start-Time} &\_ czas zakończenia = {czas zakończenia} &stopnia szczegółowości = {stopień szczegółowości} &pokazać \_ szczegóły = {true} |

#### <a name="uri-parameters"></a>Parametry identyfikatora URI

Użyj następującej ścieżki i parametrów zapytania, aby pobrać rekordy użycia.

| Nazwa | Typ | Wymagane | Opis |
| ---- | ---- | -------- | ----------- |
| Identyfikator dzierżawy klienta | ciąg | Tak | Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta. |
| Identyfikator subskrypcji | ciąg | Tak | Ciąg w formacie GUID, który identyfikuje subskrypcję. |
| start_time | ciąg w formacie UTC Data-godzina przesunięcia | Tak | Początek zakresu czasu, który reprezentuje, kiedy wykorzystanie zostało zgłoszone w systemie rozliczeń. |
| end_time | ciąg w formacie UTC Data-godzina przesunięcia | Tak | Koniec zakresu czasu, który reprezentuje, kiedy wykorzystanie zostało zgłoszone w systemie rozliczeń. |
| stopnia szczegółowości | ciąg | Nie | Definiuje stopień szczegółowości agregacji użycia. Dostępne opcje to: `daily` (ustawienie domyślne) i `hourly` .
| show_details | boolean | Nie | Określa, czy mają zostać pobrane szczegóły użycia na poziomie wystąpienia. Wartość domyślna to `true`. |
| size | liczba | Nie | Określa liczbę agregacji zwracanych przez pojedyncze wywołanie interfejsu API. Wartość domyślna to 1000. Wartość maksymalna to 1000. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak

### <a name="request-example"></a>Przykład żądania

Poniższe przykładowe żądanie generuje wyniki podobne do tego, jaki plik uzgadniania będzie wyświetlany przez okres 7/2-8/1. Te wyniki mogą nie być dokładnie zgodne (szczegółowe informacje znajdują się w sekcji [interfejsu API wykorzystania platformy Azure](#azure-utilization-api) ).

To przykładowe żądanie zwraca dane użycia zgłoszone w systemie rozliczeniowym między 7/2 o 12 AM (UTC) i 8/2 o godzinie 00:00 (UTC).

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów [rekordu użycia platformy Azure](azure-utilization-record-resources.md) w treści odpowiedzi. Jeśli dane użycia platformy Azure nie są jeszcze gotowe w systemie zależnym, Metoda ta zwraca kod stanu HTTP 204 z nagłówkiem Retry-After.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać kod stanu HTTP, [typ kodu błędu](error-codes.md)i dodatkowe parametry.

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 2630
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: PjuGoYrw806o6A3Y.0
MS-ServerId: 030020525
Date: Fri, 04 Aug 2017 23:48:28 GMT

{
  "totalCount": 2,
  "items": [
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        }
      },
      "attributes": {
        "objectType": "AzureUtilizationRecord"
      }
    },
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        },
        "attributes": {
          "objectType": "AzureUtilizationRecord"
        }
      },

      "links": {
        "self": {
          "uri": "customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-06-10T00:00:00Z&end_time=2017-07-09T00:00:00Z&granularity=Daily&show_details=True&size=1000",
          "method": "GET",
          "headers": []
        }
      },
      "attributes": {
        "objectType": "Collection"
      }
    }
  ]
}
```
