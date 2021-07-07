---
title: Pobierz pozycje użycia komercyjnego rozliczane na podstawie faktury
description: Możesz uzyskać kolekcję szczegółów pozycji pozycji faktury za użycie komercyjne (zamkniętego dziennego elementu wiersza użycia) dla określonej faktury przy użyciu interfejsów API Partner Center.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 285b6fbda774c9396dee8947550ed774d52bf901
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446228"
---
# <a name="get-invoice-billed-commercial-consumption-line-items"></a>Pobierz pozycje użycia komercyjnego rozliczane na podstawie faktury

Aby uzyskać kolekcję szczegółów dla pozycji faktur za użycie komercyjne (nazywanych również zamkniętymi pozycjami dziennego użycia) dla określonej faktury, można użyć następujących metod.


## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator faktury. Pozwala to zidentyfikować fakturę, dla której mają zostać pobrane pozycje.

## <a name="c"></a>C\#

Aby uzyskać komercyjne pozycje dla określonej faktury, musisz pobrać obiekt faktury:

1. Wywołaj [**metodę ById,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) aby uzyskać interfejs do operacji na fakturze dla określonej faktury.

2. Wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) aby pobrać obiekt faktury. Obiekt faktury zawiera wszystkie informacje dotyczące określonej faktury.

Dostawca **identyfikuje** źródło rozliczanych szczegółowych informacji (na przykład **jednogodzinnych**). Typ **invoiceLineItemType** określa typ (na przykład **UsageLineItem).**

Poniższy przykładowy kod używa pętli **foreach** do przetwarzania kolekcji elementów wiersza. Dla każdego typu **InvoiceLineItemType** pobierana jest oddzielna kolekcja elementów wiersza.

Aby uzyskać kolekcję elementów wiersza, które odpowiadają **wystąpieniu InvoiceDetail:**

1. Przekaż wartości **BillingProvider i** **InvoiceLineItemType** wystąpienia do metody [**By.**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by)

2. Wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) aby pobrać skojarzone elementy wiersza.
3. Utwórz moduł wyliczający, aby przejść przez kolekcję, jak pokazano w poniższym przykładzie.

``` csharp
// IAggregatePartner partnerOperations;
// string invoiceId;
// string curencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById(invoiceId).By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine line items count: " + seekBasedResourceCollection.Items.Count());

    seekBasedResourceCollection.Items.ToList().ForEach(item =>
    {
        // Instance of type DailyRatedUsageLineItem
        if (item is DailyRatedUsageLineItem)
        {
            Type t = typeof(DailyRatedUsageLineItem);
            PropertyInfo[] properties = t.GetProperties();

            foreach (PropertyInfo property in properties)
            {
                // Insert code here to work with the line item properties
            }
        }
        itemNumber++;
    });

    Console.Out.WriteLine("\tPress any key to fetch next data. Press the Escape (Esc) key to quit: \n");
    keyInfo = Console.ReadKey();

    if (keyInfo.Key == ConsoleKey.Escape)
    {
        break;
    }

    fetchNext = !string.IsNullOrWhiteSpace(seekBasedResourceCollection.ContinuationToken);

    if (fetchNext)
    {
        if (seekBasedResourceCollection.Links.Next.Headers != null && seekBasedResourceCollection.Links.Next.Headers.Any())
        {
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById(invoiceId).By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

Podobny przykład można znaleźć w następujących tematach:

- Przykład: [aplikacja testowa konsoli](console-test-app.md)
- Project: **zestaw SDK Centrum partnerskiego przykłady**
- Klasa: **GetBilledConsumptionReconLineItemsPaging.cs**

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

Użyj pierwszej składni, aby zwrócić pełną listę wszystkich pozycji dla danej faktury. W przypadku dużych faktur użyj drugiej składni z określonym rozmiarem i przesunięciem 0, aby zwrócić stronicowane listy elementów wiersza. Użyj trzeciej składni, aby uzyskać następną stronę ponownego wiersza elementów przy użyciu polecenia `seekOperation = "Next"` .

| Metoda  | Identyfikator URI żądania                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1                              |
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1  |
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next                               |

#### <a name="uri-parameters"></a>Parametry URI

Podczas tworzenia żądania użyj następującego parametru URI i zapytania.

| Nazwa                   | Typ   | Wymagane | Opis                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| invoice-id             | ciąg | Tak      | Ciąg, który identyfikuje fakturę.                             |
| Dostawca               | ciąg | Tak      | Dostawca: "OneTime".                                  |
| typ-elementu-wiersza faktury | ciąg | Tak      | Typ szczegółów faktury: "UsageLineItems". |
| currencyCode           | ciąg | Tak      | Kod waluty dla rozliowanych pozycji.                    |
| period                 | ciąg | Tak      | Okres dla rozliowanych rekonesencji. przykład: current, previous.        |
| size                   | liczba | Nie       | Maksymalna liczba elementów do zwrócenia. Domyślny rozmiar to 2000       |
| seekOperation          | ciąg | Nie       | Ustaw wartość seekOperation=Dalej, aby uzyskać następną stronę elementów wiersza ponownego. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak.

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, odpowiedź będzie zawierała kolekcję szczegółów elementu wiersza.

Dla elementu wiersza **ChargeType** wartość **Zakup jest** mapowana na **nowy**. Wartość Zwrot **jest** mapowana na **anuluj**.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)

## <a name="rest-examples"></a>Przykłady rest

### <a name="request-response-example-1"></a>Przykład żądania i odpowiedzi 1

Szczegóły tego przykładowego żądania REST i odpowiedzi są następujące:

- **Dostawca:** **OneTime**
- **InvoiceLineItemType**: **UsageLineItems**
- **Okres:** **Poprzedni**

#### <a name="request-example-1"></a>Przykład żądania 1

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-1"></a>Przykład odpowiedzi 1

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 2,
    "items": [
        {
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Windows 2012 R2 (WebHost)",
            "productName": "Test Test on Windows",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Windows",
            "meterName": "Test Test on Windows - Test Test on Windows 2012 R2 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS2",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TestWINRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestWINRG/providers/Microsoft.Compute/virtualMachines/testWinTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209496384791679,
            "quantity": 23.200004,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.486031696515249,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.486031696515249,
            "pricingCurrency": "USD",
            "creditType": "Credit Not Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        },
        {
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Ubuntu 16.04 (WebHost)",
            "productName": "Test Test on Linux",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Linux",
            "meterName": "Test Test on Linux - Test Test on Ubuntu 16.04 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TESTRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/testUbuntuTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209951014286867,
            "quantity": 23.350007,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.490235765325545,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.490235765325545,
            "pricingCurrency": "USD",
            "entitlementId": "66bada28-271e-4b7a-aaf5-c0ead6312345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0.1999968000511991808131,
            "rateOfPartnerEarnedCredit": 0,
            "rateOfCredit": 1,
            "creditType": "Azure Credit Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
            "method": "GET",
            "headers": [
                {
                    "key": "MS-ContinuationToken",
                    "value": "AQAAAA=="
                }
            ]
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-2"></a>Przykład żądania i odpowiedzi 2

Szczegóły tego przykładowego żądania REST i odpowiedzi są następujące:

- **Dostawca:** **OneTime**
- **InvoiceLineItemType**: **UsageLineItems**
- **Okres:** **Poprzedni**
- **SeekOperation:** **Dalej**

#### <a name="request-example-2"></a>Przykład żądania 2

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/T000001234/lineitems?provider=onetime&invoiceLineItemType=usagelineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="response-example-2"></a>Przykład odpowiedzi 2

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 1,
    "items": [
          {
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Windows 2012 R2 (WebHost)",
            "productName": "Test Test on Windows",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Windows",
            "meterName": "Test Test on Windows - Test Test on Windows 2012 R2 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS2",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TestWINRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestWINRG/providers/Microsoft.Compute/virtualMachines/testWinTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209496384791679,
            "quantity": 23.200004,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.486031696515249,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.486031696515249,
            "pricingCurrency": "USD",
            "entitlementId": "66bada28-271e-4b7a-aaf5-c0ead6312345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0.1835431430074643112595,
            "rateOfPartnerEarnedCredit": 0.15,
            "rateOfCredit": 0.15,
            "creditType": "Partner Earned Credit Applied",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
