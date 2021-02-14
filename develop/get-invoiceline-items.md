---
title: Pobieranie elementów wiersza faktury
description: Możesz uzyskać informacje o kolekcji pozycji wiersza faktury (zamknięty element linii rozliczeniowej) dla określonej faktury przy użyciu interfejsów API Centrum partnerskiego.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e797f549e1344268c8167259a231122e7c669a2e
ms.sourcegitcommit: 9f8ba784171ab4f980ed0c60ef6f2323849c4a98
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/14/2021
ms.locfileid: "100499902"
---
# <a name="get-invoice-line-items"></a>Pobieranie elementów wiersza faktury

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Przy użyciu poniższych metod można pobrać szczegóły kolekcji dla elementów wiersza faktury (znanych także jako zamknięte elementy wierszy rozliczeń) dla określonej faktury.

*Ten interfejs API nie jest już aktualizowany, z wyjątkiem poprawek błędów.* Aplikacje należy zaktualizować w taki sposób, aby wywoływać interfejs API **jednorazowej** zamiast **witryny Marketplace**. Interfejs API **jednorazowej** zapewnia dodatkową funkcjonalność i będzie nadal aktualizowany.

Należy używać **jednorazowej** do wysyłania zapytań do wszystkich elementów linii zużycia komercyjnego, a nie z **witryny Marketplace**. Można też użyć linków w wywołaniu łączy.

Ten interfejs API obsługuje również typy **dostawców** subskrypcji **platformy Azure** i **pakietu Office** dla Microsoft Azure (MS-AZR-0145P) i oferty pakietu Office, dzięki czemu funkcja interfejsu API jest zgodna z poprzednimi wersjami.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator faktury. Identyfikuje fakturę, dla której mają zostać pobrane elementy wiersza.

## <a name="c"></a>C\#

Aby pobrać elementy wiersza dla określonej faktury:

1. Wywołaj metodę [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) , aby uzyskać interfejs do fakturowania operacji dla określonej faktury.

2. Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) , aby pobrać obiekt faktury. Obiekt Invoice zawiera wszystkie informacje dotyczące określonej faktury.
3. Użyj właściwości [**InvoiceDetails**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoice.invoicedetails) obiektu faktury, aby uzyskać dostęp do kolekcji obiektów [**InvoiceDetail**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail) , z których każdy zawiera [**BillingProvider**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.billingprovider) i [**InvoiceLineItemType**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.invoicelineitemtype). **BillingProvider** identyfikuje źródło informacji szczegółowych faktury (takich jak **Office**, **Azure**, **jednorazowej**), a **InvoiceLineItemType** określa typ (na przykład **BillingLineItem**).

Poniższy przykładowy kod używa pętli **foreach** do przetwarzania kolekcji **InvoiceDetails** . Dla każdego wystąpienia **InvoiceDetail** pobierana jest oddzielna Kolekcja elementów wierszy.

Aby uzyskać kolekcję elementów wierszy, które odpowiadają wystąpieniu **InvoiceDetail** :

1. Przekaż **BillingProvider** i **InvoiceLineItemType** wystąpienia do metody [**by**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) .

2. Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.getasync) , aby pobrać skojarzone elementy wiersza.
3. Utwórz moduł wyliczający, który przejdzie do kolekcji, jak pokazano w poniższym przykładzie.

``` csharp
// IAggregatePartner partnerOperations;
// int invoicePageSize;
// string invoiceId;

// Retrieve the invoice.
var invoiceOperations = partnerOperations.Invoices.ById(invoiceId);
var invoice = invoiceOperations.Get();

foreach (var invoiceDetail in invoice.InvoiceDetails)
{
    Console.WriteLine(string.Format("Getting invoice line item for product {0} and line item type {1}",
        invoiceDetail.BillingProvider,
        invoiceDetail.InvoiceLineItemType));

    // Is this an unpaged or paged request?
    bool isUnPaged = (this.invoicePageSize <= 0);

    // If the scenario is unpaged, get all the invoice line items, otherwise get the first page.
    var invoiceLineItemsCollection =
        (isUnPaged)
        ? invoiceOperations.By(invoiceDetail.BillingProvider, invoiceDetail.InvoiceLineItemType).Get()
        : invoiceOperations.By(invoiceDetail.BillingProvider, invoiceDetail.InvoiceLineItemType).Get(this.invoicePageSize, 0);

    // Create an enumerator for traversing the line items collection.
    var invoiceLineItemEnumerator =
        partnerOperations.Enumerators.InvoiceLineItems.Create(invoiceLineItemsCollection);

    while (invoiceLineItemEnumerator.HasValue)
    {
        // invoiceLineItemEnumerator.Current contains a collection
        // of line items.
        Console.WriteLine(String.Format("invoiceLineItemEnumerator.Current has {0} line items.",
            invoiceLineItemEnumerator.Current.TotalCount));
        //
        // Insert code here to work with the line items.
        //
        Console.WriteLine();
        Console.Write("Press any key to retrieve the next invoice line items page");
        Console.ReadKey();

        // Get the next list of invoice line items.
        invoiceLineItemEnumerator.Next();
    }
}
```

Podobny przykład można znaleźć w następujących tematach:

- Przykład: [aplikacja testowa konsoli](console-test-app.md)
- Projekt: **przykłady dla zestawu SDK Centrum partnerskiego**
- Klasa: **GetInvoiceLineItems.cs**

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

Prześlij żądanie przy użyciu odpowiedniej składni dla dostawcy rozliczeń w danym scenariuszu.

#### <a name="office"></a>Office

Następująca składnia ma zastosowanie, gdy dostawca rozliczeń to **pakiet Office**.

| Metoda  | Identyfikator URI żądania                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems? Provider = Office&invoicelineitemtype = billinglineitems&size = {size} &offset = {offset} http/1.1                               |

#### <a name="microsoft-azure-ms-azr-0145p-subscription"></a>Subskrypcja Microsoft Azure (MS-AZR-0145P)

Poniższe składnie są stosowane, gdy dostawca rozliczeń ma subskrypcję Microsoft Azure (MS-AZR-0145P).

| Metoda  | Identyfikator URI żądania                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems? Provider = Azure&invoicelineitemtype = billinglineitems&size = {size} &offset = {offset} http/1.1  |
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems? Provider = Azure&invoicelineitemtype = usagelineitems&size = {size} &offset = {offset} http/1.1  |

##### <a name="onetime"></a>Jednorazowej

Poniższe składnie są stosowane, gdy dostawca rozliczeń jest **jednorazowej**. Obejmuje to opłaty za rezerwacje, oprogramowanie, plany platformy Azure i komercyjne produkty korporacyjne platformy Azure.

| Metoda  | Identyfikator URI żądania                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems? Provider = jednorazowej&invoicelineitemtype = billinglineitems&size = {size} http/1.1  |
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems/onetime/billinglineitems&size = {size}? SeekOperation = Next                           |

#### <a name="previous-syntaxes"></a>Poprzednie składnie

Jeśli używasz następujących składni, pamiętaj, aby użyć odpowiedniej składni dla przypadku użycia.

*Ten interfejs API nie jest już aktualizowany, z wyjątkiem poprawek błędów.* Aplikacje należy zaktualizować w taki sposób, aby wywoływać interfejs API **jednorazowej** zamiast **witryny Marketplace**. Interfejs API **jednorazowej** zapewnia dodatkową funkcjonalność i będzie nadal aktualizowany.

Należy używać **jednorazowej** do wysyłania zapytań do wszystkich elementów linii zużycia komercyjnego, a nie z **witryny Marketplace**. Można też użyć linków w wywołaniu łączy.

| Metoda | Identyfikator URI żądania | Opis przypadku użycia składni |
| ------ | ----------- | -------------------------------- |
| GET | [*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems/{Billing-Provider}/{Invoice-line-Item-Type} http/1.1                              | Możesz użyć tej składni, aby zwrócić pełną listę każdego elementu wiersza dla danej faktury. |
| GET | [*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems/{Billing-Provider}/{Invoice-line-Item-Type}? size = {size} &offset = {offset} http/1.1  | W przypadku dużych faktur można użyć tej składni z określonym rozmiarem i przesunięciu na 0, aby zwrócić stronicowaną listę elementów wiersza. |
| GET | [*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems/onetime/{Invoice-line-Item-Type}? SeekOperation = Next                               | Możesz użyć tej składni dla faktury z wartością dostawcy rozliczeń **jednorazowej** i ustawić **SeekOperation** , aby **dalej** uzyskać następną stronę elementów wiersza faktury. |

##### <a name="uri-parameters"></a>Parametry identyfikatora URI

Podczas tworzenia żądania Użyj następujących parametrów URI i zapytania.

| Nazwa                   | Typ   | Wymagane | Opis                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| Identyfikator faktury             | ciąg | Tak      | Ciąg, który identyfikuje fakturę.                             |
| rozliczenia — dostawca       | ciąg | Tak      | Dostawca rozliczeń: "Office", "Azure", "jednorazowej". W starszej wersji istnieją osobne modele danych dla transakcji pakietu Office & platformy Azure. Jednak nowoczesny ma jeden model danych dla wszystkich transakcji przefiltrowanych przez wartość "jednorazowej".            |
| Typ faktury-wiersz-element | ciąg | Tak      | Typ faktury szczegóły: "BillingLineItems", "UsageLineItems". |
| size                   | liczba | Nie       | Maksymalna liczba elementów do zwrócenia. Domyślny maksymalny rozmiar = 2000    |
| przesunięcie                 | liczba | Nie       | Indeks (liczony od zera) elementu pierwszego wiersza do zwrócenia.            |
| seekOperation          | ciąg | Nie       | Jeśli **dostawca rozliczeń** jest równy **jednorazowej**, ustaw wartość **seekOperation** równą **Next** , aby uzyskać następną stronę elementów wiersza faktury. |
| hasPartnerEarnedCredit | bool | Nie | Wartość wskazująca, czy zwrócić elementy wiersza z zastosowaniem środków uzyskanych przez partnera. Uwaga: ten parametr zostanie zastosowany tylko wtedy, gdy typ dostawcy rozliczeń to jednorazowej, a InvoiceLineItemType to UsageLineItems. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, odpowiedź zawiera kolekcję szczegółów elementu wiersza.

*Dla pozycji **line ItemType** wartość **Purchase** jest mapowana na **nową**. **Zwrot** wartości jest mapowany na **Anuluj**.*

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="rest-request-response-examples"></a>Przykłady żądania REST — odpowiedzi

### <a name="request-response-example-1"></a>Przykład żądania — odpowiedź 1

W tym przykładzie szczegóły są następujące:

- **BillingProvider**: **Office**
- **InvoiceLineItemType**: **BillingLineItems**

#### <a name="request-example-1"></a>Przykład żądania 1

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/1234000000/lineitems?provider=Office&nvoicelineitemtype=BillingLineItems&size=2&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-1"></a>Przykład odpowiedzi 1

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

{
    "totalCount": 2,
    "items": [{
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "74221236-D09C-4870-AC1D-33E155E9AEBE",
            "customerName": "TSTAGIN1CUST190",
            "mpnId": 4391507,
            "tier2MpnId": -1,
            "orderId": "567735045559164136",
            "subscriptionId": "4KIKawEAAAAAAAEA",
            "syndicationPartnerSubscriptionNumber": "1F58ACD7-FE51-4705-9567-D009C9ADA150",
            "offerId": "AAA5B3F0-0EE2-431B-A42F-3F18F3C6D540",
            "durableOfferId": "2F707C7C-2433-49A5-A437-9CA7CF40D3EB",
            "offerName": "EXCHANGE ONLINE (PLAN 2)",
            "domainName": "TStagin1Cust190.onmicrosoft.com",
            "billingCycleType": "MONTHLY",
            "subscriptionName": "EXCHANGE ONLINE (PLAN 2)",
            "subscriptionDescription": "EXCHANGE ONLINE (PLAN 2)",
            "subscriptionStartDate": "2017-05-12T00:00:00",
            "subscriptionEndDate": "2018-06-10T00:00:00",
            "chargeStartDate": "2017-05-12T00:00:00",
            "chargeEndDate": "2017-06-09T00:00:00",
            "chargeType": "New",
            "unitPrice": 0.0,
            "quantity": 3,
            "amount": 0.0,
            "totalOtherDiscount": 0.0,
            "subtotal": 0.0,
            "tax": 0.0,
            "totalForCustomer": 0.0,
            "currency": "USD",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "office",
            "attributes": {
                "objectType": "LicenseBasedLineItem"
            }
        }, {
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "74221236-D09C-4870-AC1D-33E155E9AEBE",
            "customerName": "TSTAGIN1CUST190",
            "mpnId": 4391507,
            "tier2MpnId": -1,
            "orderId": "567735045564795186",
            "subscriptionId": "Ik4YawEAAAAAAAEA",
            "syndicationPartnerSubscriptionNumber": "D8A8F773-9D3E-4244-8797-3182075F09FA",
            "offerId": "618B53FE-9B99-428B-9745-F706AEAF3979",
            "durableOfferId": "69C67983-CF78-4102-83F6-3E5FD246864F",
            "offerName": "SHAREPOINT ONLINE (PLAN 2)",
            "domainName": "TStagin1Cust190.onmicrosoft.com",
            "billingCycleType": "MONTHLY",
            "subscriptionName": "SHAREPOINT ONLINE (PLAN 2)",
            "subscriptionDescription": "SHAREPOINT ONLINE (PLAN 2)",
            "subscriptionStartDate": "2017-05-13T00:00:00",
            "subscriptionEndDate": "2018-06-10T00:00:00",
            "chargeStartDate": "2017-05-13T00:00:00",
            "chargeEndDate": "2017-06-09T00:00:00",
            "chargeType": "New",
            "unitPrice": 0.0,
            "quantity": 1,
            "amount": 0.0,
            "totalOtherDiscount": 0.0,
            "subtotal": 0.0,
            "tax": 0.0,
            "totalForCustomer": 0.0,
            "currency": "USD",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "office",
            "attributes": {
                "objectType": "LicenseBasedLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/1234000000/lineitems?provider=Office&nvoicelineitemtype=BillingLineItems&size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/1234000000/lineitems?provider=Office&nvoicelineitemtype=BillingLineItems&size=2&offset=",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-2"></a>Przykład żądania — odpowiedź 2

W poniższym przykładzie szczegóły są następujące:

- **BillingProvider**: **Azure**
- **InvoiceLineItemType**: **BillingLineItems**

#### <a name="request-example-2"></a>Przykład żądania 2

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=BillingLineItems&size=2&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-2"></a>Przykład odpowiedzi 2

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

{
    "totalCount": 2,
    "items": [
        {
            "detailLineItemId": 1,
            "sku": "7UD-00001",
            "includedQuantity": 0,
            "overageQuantity": 745,
            "listPrice": 0.085,
            "currency": "USD",
            "pretaxCharges": 63.33,
            "taxAmount": 6.34,
            "postTaxTotal": 69.67,
            "pretaxEffectiveRate": 0.08500671,
            "postTaxEffectiveRate": 0.09351677,
            "chargeType": "Assess usage fee for current cycle",
            "invoiceLineItemType": "billing_line_items",
            "partnerId": "1F5CCB06-8E36-4A74-A74C-FCAA9E000000",
            "partnerName": "TEST_TEST_Big foot consulting",
            "partnerBillableAccountId": "1010578050",
            "customerId": "65726577-c208-40fd-9735-8c85ac000000",
            "domainName": "600test.onmicrosoft.com",
            "customerCompanyName": "601 tests",
            "mpnId": 4390934,
            "tier2MpnId": -1,
            "invoiceNumber": "1234000000",
            "subscriptionId": "87f4b92f-a490-485e-ad34-5b70cb000000",
            "subscriptionName": "Microsoft Azure",
            "subscriptionDescription": "Microsoft Azure",
            "billingCycleType": "Monthly",
            "orderId": "568297985427000000",
            "serviceName": "Azure App Service",
            "serviceType": "Standard Plan",
            "resourceGuid": "505db374-df8a-44df-9d8c-13c14b61dee1",
            "resourceName": "S1",
            "region": "",
            "consumedQuantity": 745,
            "chargeStartDate": "2019-08-02T00:00:00",
            "chargeEndDate": "2019-09-01T00:00:00",
            "unit": "1 Hour",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "UsageBasedLineItem"
            }
        },
        {
            "detailLineItemId": 1,
            "sku": "7UD-00001",
            "includedQuantity": 0,
            "overageQuantity": 0.000882,
            "listPrice": 0.0383,
            "currency": "USD",
            "pretaxCharges": 0,
            "taxAmount": 0,
            "postTaxTotal": 0,
            "pretaxEffectiveRate": 0,
            "postTaxEffectiveRate": 0,
            "chargeType": "Assess usage fee for current cycle",
            "invoiceLineItemType": "billing_line_items",
            "partnerId": "1F5CCB06-8E36-4A74-A74C-FCAA9E87E26A",
            "partnerName": "TEST_TEST_Big foot consulting",
            "partnerBillableAccountId": "1010578050",
            "customerId": "65726577-c208-40fd-9735-8c85ac9cac68",
            "domainName": "600test.onmicrosoft.com",
            "customerCompanyName": "601 tests",
            "mpnId": 4390934,
            "tier2MpnId": -1,
            "invoiceNumber": "1234000000",
            "subscriptionId": "87f4b92f-a490-485e-ad34-5b70cb000000",
            "subscriptionName": "Microsoft Azure",
            "subscriptionDescription": "Microsoft Azure",
            "billingCycleType": "Monthly",
            "orderId": "568297985427000000",
            "serviceName": "Storage",
            "serviceType": "Standard Page Blob",
            "resourceGuid": "d23a5753-ff85-4ddf-af28-8cc5cf2d3882",
            "resourceName": "LRS Data Stored",
            "region": "",
            "consumedQuantity": 0.000882,
            "chargeStartDate": "2019-08-02T00:00:00",
            "chargeEndDate": "2019-09-01T00:00:00",
            "unit": "1 GB/Month",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "UsageBasedLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=BillingLineItems&size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=BillingLineItems&size=2&offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-3"></a>Przykład żądania — odpowiedź 3

W poniższym przykładzie szczegóły są następujące:

- **BillingProvider**: **Azure**
- **InvoiceLineItemType**: **UsageLineItems**

#### <a name="request-example-3"></a>Przykład żądania 3

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=UsageLineItems&size=2&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-3"></a>Przykład odpowiedzi 3

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

{
    "totalCount": 2,
    "items": [
        {
            "customerBillableAccount": "1439508127",
            "usageDate": "2019-08-05T00:00:00",
            "invoiceLineItemType": "usage_line_items",
            "partnerId": "1F5CCB06-8E36-4A74-A74C-FCAA9E000000",
            "partnerName": "TEST_TEST_BIG FOOT CONSULTING",
            "partnerBillableAccountId": "1010578050",
            "customerId": "9E9B71BA-3442-458B-B519-E1CCF72FBB54",
            "domainName": "test600.onmicrosoft.com",
            "customerCompanyName": "600 TEST",
            "mpnId": 4390934,
            "tier2MpnId": -1,
            "invoiceNumber": "1234000000",
            "subscriptionId": "F9BA6DA0-6DAC-4F88-B623-313C9B9C117A",
            "subscriptionName": "MICROSOFT AZURE",
            "subscriptionDescription": "MICROSOFT AZURE",
            "billingCycleType": "MONTHLY",
            "orderId": "568297985577171353",
            "serviceName": "STORAGE",
            "serviceType": "STANDARD PAGE BLOB",
            "resourceGuid": "9CC63CF8-6593-410A-B0E7-26A4EF71E8B3",
            "resourceName": "DISK DELETE OPERATIONS",
            "region": "",
            "consumedQuantity": 2.9616,
            "chargeStartDate": "2019-08-05T00:00:00",
            "chargeEndDate": "2019-09-04T00:00:00",
            "unit": "10K",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "DailyUsageLineItem"
            }
        },
        {
            "customerBillableAccount": "1307536861",
            "usageDate": "2019-08-10T00:00:00",
            "invoiceLineItemType": "usage_line_items",
            "partnerId": "1F5CCB06-8E36-4A74-A74C-FCAA9E000000",
            "partnerName": "TEST_TEST_BIG FOOT CONSULTING",
            "partnerBillableAccountId": "1010578050",
            "customerId": "EB53B7BD-267E-440E-B3C0-8F0B40000000",
            "domainName": "brandontest.onmicrosoft.com",
            "customerCompanyName": "BRANDON'S TEST",
            "mpnId": 4390934,
            "tier2MpnId": -1,
            "invoiceNumber": "1234000000",
            "subscriptionId": "62D22561-AB15-41E5-AD59-99025C000000",
            "subscriptionName": "MICROSOFT AZURE",
            "subscriptionDescription": "MICROSOFT AZURE",
            "billingCycleType": "MONTHLY",
            "orderId": "568297985605838583",
            "serviceName": "VIRTUAL MACHINES",
            "serviceType": "D/DS SERIES WINDOWS",
            "resourceGuid": "62C64B6C-4033-4E20-AB33-9E81271AC12A",
            "resourceName": "D1/DS1",
            "region": "US WEST",
            "consumedQuantity": 24,
            "chargeStartDate": "2019-08-05T00:00:00",
            "chargeEndDate": "2019-09-04T00:00:00",
            "unit": "1 HOUR",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "DailyUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=UsageLineItems&size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=UsageLineItems&size=2&offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-4"></a>Przykład żądania-odpowiedź 4

W poniższym przykładzie szczegóły są następujące:

- **BillingProvider**: **jednorazowej**
- **InvoiceLineItemType**: **BillingLineItems**

#### <a name="request-example-4"></a>Przykład żądania 4

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/G000024135/lineitems/OneTime/BillingLineItems?size=2&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-4"></a>Przykład odpowiedzi 4

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

 {
    "continuationToken": "d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7",
    "totalCount": 2,
    "items": [
        {
            "partnerId": "6480d686-cfb4-424d-a945-6b9b9f000000",
            "customerId": "org:9060d13d-c5ed-482e-b059-a15a38000000",
            "customerName": "recipientCustomerName",
            "customerDomainName": "recipientCustomerDomain",
            "invoiceNumber": "1234000000",
            "quoteId": "abcd12345678",
            "mpnId": "4870137",
            "resellerMpnId": 0,
            "orderId": "QDOx5ZN3YR9uYhm4M1MGQJ_0nievUOrx1",
            "orderDate": "2018-02-08T22:31:42.9397946Z",
            "productId": "productid",
            "skuId": "skuid",
            "availabilityId": "availabilityid",
            "productName": "TEST PRODUCT",
            "skuName": "TEST SKU TITLE",
            "chargeType": "New",
            "unitPrice": 431.8,
            "effectiveUnitPrice": 496.07,
            "unitType": "Seats",
            "quantity": 1,
            "subtotal": 431.8,
            "taxTotal": 38.87,
            "totalForCustomer": 470.67,
            "currency": "USD",
            "providerName": "Test Networks Inc",
            "providerId": "12343810",
            "subscriptionDescription": "",
            "subscriptionId": "281e26fe-9ce7-415b-911c-f39232000000",
            "subscriptionStartDate": "2019-01-03T19:53:55.1292512+00:00",
            "subscriptionEndDate": "2019-02-02T19:53:55.1292512+00:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "1234278124b8",
            "priceAdjustmentDescription": "[\"100.0% Tier 1 Discount\"]",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-09-30T23:59:59Z",
            "billableQuantity": 0.0159369774,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "billingFrequency": "Monthly",
            "reservationOrderId": "883d475b-0000-2222-0000-8818752f1234",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        },
        {
            "partnerId": "6480d686-cfb4-424d-a945-6b9b9f4badc2",
            "customerId": "org:9060d13d-c5ed-482e-b059-a15a38cbb28e",
            "customerName": "recipientCustomerName",
            "customerDomainName": "recipientCustomerDomain",
            "invoiceNumber": "1234000000",
            "quoteId": "abcd12345678",
            "mpnId": "4870137",
            "resellerMpnId": 0,
            "orderId": "QDOx5ZN3YR9uYhm4M1MGQJ_0nievUOrx1",
            "orderDate": "2018-02-08T22:31:42.9397946Z",
            "productId": "productid",
            "skuId": "skuid",
            "availabilityId": "availabilityid",
            "productName": "TEST PRODUCT",
            "skuName": "TEST SKU TITLE",
            "chargeType": "New",
            "unitPrice": 26.35,
            "effectiveUnitPrice": 496.07,
            "unitType": "1 Hour",
            "quantity": 1,
            "subtotal": 26.35,
            "taxTotal": 2.37,
            "totalForCustomer": 28.72,
            "currency": "USD",
            "providerName": "Test Networks Inc",
            "providerId": "12343810",
            "subscriptionDescription": "",
            "subscriptionId": "281e26fe-9ce7-415b-911c-f39232ea904a",
            "subscriptionStartDate": "2019-01-03T19:53:55.1292512+00:00",
            "subscriptionEndDate": "2019-02-02T19:53:55.1292512+00:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "1234578124b8",
            "priceAdjustmentDescription": "[\"100.0% Tier 1 Discount\"]",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-09-30T23:59:59Z",
            "billableQuantity": 0.0130687981,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "reservationOrderId": "",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/G000024135/lineitems?provider=OneTime&nvoicelineitemtype=BillingLineItems&size=2",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/G000024135/lineitems?provider=OneTime&nvoicelineitemtype=BillingLineItems&size=2?seekOperation=Next",
            "method": "GET",
            "headers": [
                {
                    "key": "MS-ContinuationToken",
                    "value": "d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7"
                }
            ]
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-5"></a>Przykład żądania — odpowiedź 5

W poniższym przykładzie jest stronicowanie przy użyciu tokenu kontynuacji. Szczegóły są następujące:

- **BillingProvider**: **jednorazowej**
- **InvoiceLineItemType**: **BillingLineItems**
- **SeekOperation**: **dalej**

#### <a name="request-example-5"></a>Przykład żądania 5

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/G000024135/lineitems/OneTime/BillingLineItems?seekOperation=Next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-5"></a>Przykład odpowiedzi 5

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

{
    "totalCount": 1,
    "items": [
        {
            "partnerId": "6480d686-cfb4-424d-a945-6b9b9f000000",
            "customerId": "org:9060d13d-c5ed-482e-b059-a15a38000000",
            "customerName": "recipientCustomerName",
            "customerDomainName": "recipientCustomerDomain",
            "invoiceNumber": "1234000000",
            "quoteId": "abcd12345678",
            "mpnId": "4870137",
            "resellerMpnId": 0,
            "orderId": "NeqT31Kziwf8gkCXM9YQToWTqU-9Jbm81",
            "orderDate": "2018-02-08T22:31:47.1751688Z",
            "productId": "DZH318Z0BQ3P",
            "skuId": "001F",
            "availabilityId": "DZH318Z0DR0H",
            "productName": "Reserved VM Instance, Standard_D1, AP East, 3 years",
            "skuName": "D Series",
            "chargeType": "New",
            "unitPrice": 1447,
            "effectiveUnitPrice": 496.07,
            "unitType": "Seats",
            "quantity": 1,
            "subtotal": 1447,
            "taxTotal": 130.24,
            "totalForCustomer": 1577.24,
            "currency": "USD",
            "providerName": "Test Networks Inc",
            "providerId": "12343810",
            "subscriptionDescription": "",
            "subscriptionId": "281e26fe-9ce7-415b-911c-f39232000000",
            "subscriptionStartDate": "2019-01-03T19:53:55.1292512+00:00",
            "subscriptionEndDate": "2019-02-02T19:53:55.1292512+00:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "1234568124b8",
            "priceAdjustmentDescription": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-09-30T23:59:59Z",
            "billableQuantity": 0.0130687981,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "reservationOrderId": "",
            "billingFrequency": "Monthly",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/G000024135/lineitems?provider=OneTime&nvoicelineitemtype=BillingLineItems&size=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
