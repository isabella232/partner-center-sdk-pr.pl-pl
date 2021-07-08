---
title: Pobieranie rekordów dotyczących wykorzystania platformy Azure przez klienta
description: Za pomocą interfejsu API wykorzystania platformy Azure można pobrać rekordy wykorzystania subskrypcji platformy Azure klienta w określonym przedziale czasu.
ms.date: 04/19/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7024bc65976a9b43a62b66c529d271519181ab23
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874928"
---
# <a name="get-a-customers-utilization-records-for-azure"></a>Pobieranie rekordów dotyczących wykorzystania platformy Azure przez klienta

**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Rekordy wykorzystania subskrypcji platformy Azure klienta w określonym przedziale czasu można uzyskać przy użyciu interfejsu API użycia platformy Azure.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie zarówno za pomocą aplikacji autonomicznej, jak i poświadczeń aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji.

Ten interfejs API zwraca dzienne i godzinowe zużycie bez użycia dla dowolnego zakresu czasu. Ten interfejs *API nie jest jednak obsługiwany w przypadku planów platformy Azure.* Jeśli masz plan platformy Azure, zapoznaj się z artykułami Get [invoice unbilled consumption line items](get-invoice-unbilled-consumption-lineitems.md) (Uzyskiwanie elementów wiersza użycia bez rozliczenia faktury) i Get invoice billed consumption line items (Uzyskiwanie pozycji zużycia rozliczanych na podstawie [faktury).](get-invoice-billed-consumption-lineitems.md) W tych artykułach opisano sposób oceny zużycia na poziomie dziennym na miernik na zasób. To użycie jest równoważne z dziennymi danymi ziarna dostarczanymi przez interfejs API użycia platformy Azure. Aby pobrać rozliczane dane użycia, należy użyć identyfikatora faktury. Możesz też użyć bieżących i poprzednich okresów, aby uzyskać nienalizane oszacowania użycia. *Dane ziarna godzinowego i dowolne filtry zakresu dat nie są* obecnie obsługiwane w przypadku zasobów subskrypcji planu platformy Azure.

## <a name="azure-utilization-api"></a>Interfejs API wykorzystania platformy Azure

Ten interfejs API wykorzystania platformy Azure zapewnia dostęp do rekordów wykorzystania w okresie, który reprezentuje, kiedy wykorzystanie zostało zgłoszone w systemie rozliczeniowym. Zapewnia dostęp do tych samych danych użycia, które są używane do tworzenia i obliczania pliku uzgodnień. Nie ma jednak wiedzy na temat logiki pliku uzgodnień systemu rozliczeniowego. Nie należy oczekiwać, że wyniki podsumowania pliku uzgodnień będą zgodne z wynikiem pobranym z tego interfejsu API dokładnie dla tego samego okresu.

Na przykład system rozliczeń pobiera te same dane użycia i stosuje reguły opóźnień w celu określenia, co jest uwzględnione w pliku uzgodnień. Po zamknięciu okresu rozliczeniowego całe użycie do końca dnia zakończenia okresu rozliczeniowego jest uwzględniane w pliku uzgodnień. Wszelkie opóźnione użycie w okresie rozliczeniowym zgłoszonym w ciągu 24 godzin po zakończeniu okresu rozliczeniowego jest uwzględniane w następnym pliku uzgodnień. Aby uzyskać informacje na temat reguł opóźniań dotyczących sposobu naliczania opłat przez partnera, zobacz Get consumption data for an Azure subscription (Uzyskiwanie danych użycia [dla subskrypcji platformy Azure).](/previous-versions/azure/reference/mt219001(v=azure.100))

Ten interfejs API REST jest stronicowany. Jeśli ładunek odpowiedzi jest większy niż jedna strona, musisz użyć następnego linku, aby uzyskać następną stronę rekordów użycia.

### <a name="scenario-partner-a-has-transferred-billing-ownership-of-azure-legacy-subscription-145p-to-partner-b"></a>Scenariusz: Partner A przenieść własność rozliczeń starszej subskrypcji platformy Azure (145P) na partnera B

Jeśli partner przenosi własność rozliczeń starszej subskrypcji platformy Azure na innego partnera, gdy nowy partner wywołuje interfejs API wykorzystania dla przeniesionej subskrypcji, musi użyć identyfikatora subskrypcji handlowej (który pojawia się na jego koncie Partner Center), a nie identyfikatora uprawnień platformy Azure. Identyfikator uprawnień platformy Azure jest wyświetlany dla partnera B tylko wtedy, gdy jest administratorem w imieniu (AOBO) w imieniu klienta Azure Portal. 

Aby pomyślnie wywołać interfejs API wykorzystania przeniesionej subskrypcji, nowy partner musi użyć identyfikatora subskrypcji handlowej.

## <a name="c"></a>C\#

Aby uzyskać rekordy użycia platformy Azure:

1. Pobierz identyfikator klienta i identyfikator subskrypcji.

2. Wywołaj [**metodę IAzureUtilizationCollection.Query,**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) aby zwrócić metodę [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) zawierającą rekordy wykorzystania.

3. Uzyskaj moduł wyliczający rekord wykorzystania platformy Azure w celu przechodzenia między stronami wykorzystania. Ten krok jest wymagany, ponieważ kolekcja zasobów jest stronicowana.

- **Przykład:** [aplikacja testowa konsoli](console-test-app.md)
- **Project:** zestaw SDK Centrum partnerskiego przykłady
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

Aby uzyskać rekordy wykorzystania platformy Azure, musisz najpierw uzyskać identyfikator klienta i identyfikator subskrypcji. Następnie wywołaj funkcję **IAzureUtilizationCollection.query,** aby zwrócić funkcję **ResourceCollection** zawierającą rekordy wykorzystania. Ponieważ kolekcja zasobów jest stronicowana, należy uzyskać moduł wyliczający rekord wykorzystania platformy Azure, aby przechodzić między stronami wykorzystania.

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

Aby uzyskać rekordy wykorzystania platformy Azure, musisz najpierw uzyskać identyfikator klienta i identyfikator subskrypcji. Następnie wywołaj pozycję [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md). To polecenie zwróci wszystkie rekordy dostępne w określonym przedziale czasu.

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania |
|------- | ----------- |
| **Pobierz** | *{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/utilizations/azure?start \_ time={godzina rozpoczęcia}&\_ zakończenia={czas zakończenia}&stopień szczegółowości={stopień szczegółowości}&pokaż \_ szczegóły={True} |

#### <a name="uri-parameters"></a>Parametry URI

Użyj następującej ścieżki i parametrów zapytania, aby pobrać rekordy wykorzystania.

| Nazwa | Typ | Wymagane | Opis |
| ---- | ---- | -------- | ----------- |
| identyfikator dzierżawy klienta | ciąg | Tak | Ciąg w formacie identyfikatora GUID, który identyfikuje klienta. |
| subscription-id | ciąg | Tak | Ciąg w formacie identyfikatora GUID, który identyfikuje subskrypcję. |
| start_time | ciąg w formacie przesunięcia daty i czasu UTC | Tak | Początek zakresu czasu, który reprezentuje, kiedy wykorzystanie zostało zgłoszone w systemie rozliczeniowym. |
| End_time | ciąg w formacie przesunięcia daty i czasu UTC | Tak | Koniec zakresu czasu, który reprezentuje, kiedy wykorzystanie zostało zgłoszone w systemie rozliczeniowym. |
| Ziarnistość | ciąg | Nie | Definiuje poziom szczegółowości agregacji użycia. Dostępne opcje to: `daily` (ustawienie domyślne) i `hourly` .
| show_details | boolean | Nie | Określa, czy uzyskać szczegóły użycia na poziomie wystąpienia. Wartość domyślna to `true`. |
| size | liczba | Nie | Określa liczbę agregacji zwróconych przez pojedyncze wywołanie interfejsu API. Wartość domyślna to 1000. Wartość maksymalna to 1000. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak

### <a name="request-example"></a>Przykład żądania

Poniższe przykładowe żądanie generuje wyniki podobne do tego, co plik uzgodnień będzie pokazywać w okresie 7/2–8/1. Te wyniki mogą nie być dokładnie zgodne (zobacz sekcję Interfejs [API użycia platformy Azure,](#azure-utilization-api) aby uzyskać szczegółowe informacje).

To przykładowe żądanie zwraca dane dotyczące wykorzystania zgłoszone w systemie rozliczeniowym między godziną 7/2 o godzinie 12:00 (UTC) a 8/2 o godzinie 12:00 (UTC).

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

W przypadku powodzenia ta metoda zwraca kolekcję zasobów [rekordu użycia platformy Azure](azure-utilization-record-resources.md) w treści odpowiedzi. Jeśli dane użycia platformy Azure nie są jeszcze gotowe w systemie zależnym, ta metoda zwraca kod stanu HTTP 204 z nagłówkiem Retry-After danych.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać kod stanu HTTP, [typ kodu błędu](error-codes.md)i dodatkowe parametry.

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
