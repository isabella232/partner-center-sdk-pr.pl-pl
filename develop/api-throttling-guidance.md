---
title: Wskazówki dotyczące ograniczania przepustowości interfejsu API
description: W przypadku partnerów wywołujących Partner Center API dowiedz się, na które interfejsy API ma wpływ ograniczanie przepustowości interfejsów API firmy Microsoft, oraz poznaj najlepsze rozwiązania, aby uniknąć ograniczania przepustowości lub lepiej je obsłużyć.
ms.date: 04/14/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: 4eead16c5bb2b01f0fba85e30ea35fbcdae9d5a6682872eecfeeb9e47f43d324
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993762"
---
# <a name="api-throttling-guidance-for-partners-calling-partner-center-apis"></a>Wskazówki dotyczące ograniczania interfejsu API dla partnerów wywołujących Partner Center API 

Firma Microsoft implementuje ograniczanie przepustowości interfejsu API, aby zapewnić bardziej spójną wydajność w czasie dla partnerów wywołujących interfejsy API Partner Center API. Ograniczanie ogranicza liczbę żądań do usługi w zakresie czasu, aby zapobiec nadużytości zasobów. Chociaż Partner Center jest przeznaczona do obsługi dużej liczby żądań, w przypadku przytłaczającej liczby żądań przez kilku partnerów ograniczanie przepływności pomaga zachować optymalną wydajność i niezawodność dla wszystkich partnerów.  

Limity ograniczania różnią się w zależności od scenariusza. Jeśli na przykład wykonujesz dużą liczbę operacji zapisu, możliwość ograniczenia przepustowości jest większa niż w przypadku wykonywania tylko operacji odczytu.

## <a name="what-happens-when-throttling-occurs"></a>Co się dzieje w przypadku wystąpienia ograniczania? 

Po przekroczeniu progu ograniczania Partner Center ogranicza wszelkie dalsze żądania od tego klienta przez określony czas. Zachowanie ograniczania zależy od typu i liczby żądań.   

### <a name="common-throttling-scenarios"></a>Typowe scenariusze ograniczania przepustowości 

Najczęstsze przyczyny ograniczania przepustowości klientów to: 

- Duża liczba żądań dla interfejsu API na identyfikator dzierżawy partnera: w przypadku niektórych interfejsów API programu Partner Center ograniczanie jest określane przez identyfikator dzierżawy partnera. Zbyt wiele wywołań tych interfejsów **API** w tym samym identyfikatorze dzierżawy partnera spowoduje przekroczenie progu ograniczenia.  

- **Duża liczba żądań interfejsu API** na identyfikator dzierżawy partnera na identyfikator dzierżawy klienta: w przypadku innych interfejsów API ograniczanie jest określane przez kombinację identyfikatora dzierżawy partnera/identyfikatora dzierżawy klienta; W takich przypadkach wykonanie zbyt wielu wywołań względem tego samego identyfikatora dzierżawy klienta spowoduje ograniczenie przepustowości, podczas gdy wywołania względem innych klientów mogą zakończyć się powodzeniem.

## <a name="best-practices-to-avoid-throttling"></a>Najlepsze rozwiązania w celu uniknięcia ograniczania przepustowości 
 
Rozwiązania programistyczne, takie jak ciągłe sondowanie zasobu w celu sprawdzenia aktualizacji i regularne skanowanie kolekcji zasobów w celu sprawdzenia nowych lub usuniętych zasobów, mogą prowadzić do ograniczenia przepustowości i obniżyć ogólną wydajność. Współbieżne wywołania interfejsu API mogą prowadzić do dużej liczby żądań na jednostkę czasu, co spowoduje również ograniczenie żądań. Zamiast tego należy używać śledzenia zmian i powiadomień o zmianach. Ponadto powinno być możliwe wykrywanie zmian za pomocą dzienników aktywności. Aby uzyskać więcej informacji, [zobacz Partner Center dzienników aktywności.](get-a-record-of-partner-center-activity-by-user.md)  Zdecydowanie zalecamy partnerom rozważenie użycia interfejsu API dziennika aktywności w celu zwiększenia wydajności i uniknięcia ograniczania. Zobacz również przykład użycia dzienników aktywności poniżej.

## <a name="best-practices-to-handle-throttling"></a>Najlepsze rozwiązania dotyczące obsługi ograniczania przepustowości

Poniżej przedstawiono najlepsze rozwiązania dotyczące obsługi ograniczania przepustowości: 

- Zmniejsz stopień równoległości. 
- Zmniejsz częstotliwość wywołań. 
- Unikaj natychmiastowych ponownych prób, ponieważ wszystkie żądania są naliczane względem limitów użycia. 

Podczas wdrażania obsługi błędów użyj kodu błędu HTTP 429, aby wykryć ograniczenia przepustowości. Odpowiedź, która zakończyła się niepowodzeniem, zawiera Retry-After odpowiedzi. Backing off requests using the Retry-after delay is the fastest way to recover from throttling (Cofanie żądań przy użyciu opóźnienia Ponów po jest najszybszym sposobem odzyskiwania po ograniczaniu przepustowości). 

Aby użyć opóźnienia Ponów po, wykonaj następujące czynności: 

1. Poczekaj liczbę sekund określoną w nagłówku Retry-After. 

2. Ponów próbę żądania.  

3. Jeśli żądanie ponownie zakończy się niepowodzeniem z kodem błędu 429, nadal trwa ograniczanie. Ponów próbę przy użyciu wykładniczego odroczania, użyj zalecanego Retry-After i ponów próbę żądania do momentu jego powodzenia.

4. Jeśli używasz zestawu SDK, otrzymasz wyjątek z kodem stanu 429, gdy żądanie jest ograniczane. Użyj właściwości RetryAfter w wyjątku i ponów próbę żądania po upływie czasu.


## <a name="apis-currently-impacted-by-throttling"></a>Interfejsy API, na które ma obecnie wpływ ograniczanie przepustowości

W końcu każdy interfejs API Partner Center, który wywołuje punkt końcowy "api.partnercenter.microsoft.com/", będzie ograniczany. Obecnie limity ograniczania są wymuszane tylko dla interfejsów API wymienionych poniżej. Partner Center będzie zbierać dane telemetryczne dla każdego z interfejsów API i dynamicznie dostosuje limity ograniczania. W poniższej tabeli wymieniono interfejsy API, w których ograniczanie jest obecnie wymuszane.  


|**Operacja**| **Dokumentacja Centrum partnerskiego**|
|------------------------|----------------------------|
|{baseURL}/v1/customers/{customer_id}/orders|[tworzenie zamówienia](create-an-order.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades|[przejście subskrypcji](transition-a-subscription.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}|[zakup dodatku do subskrypcji](purchase-an-add-on-to-a-subscription.md)|
|{baseURL}/v1/customers/{customer-id}/carts/{cart-id}|[tworzenie koszyka](create-a-cart.md)|
|{baseURL}/v1/customers/{identyfikator-klienta}/carts/{identyfikator-koszyka}/finalizacji zakupu|[finalizacji zakupu koszyka](checkout-a-cart.md)|
|{baseURL}/v1/customers/{customer-id}/carts/{cart-id}|[aktualizowanie koszyka](update-a-cart.md)|
|{baseURL}/v1/customers/{identyfikator-klienta}/subscriptions/{subscription-id}/registrations|[rejestrowanie subskrypcji](register-a-subscription.md)|
|{baseURL}/v1/productupgrades|[tworzenie jednostki uaktualnienia produktu](create-product-upgrade-entity.md)|
|{baseURL}/v1/customers/{identyfikator-klienta}/subscriptions/{subscription-id}/conversions |[konwertowanie subskrypcji wersji próbnej na płatną](convert-a-trial-subscription-to-paid.md)|
|{baseURL}/v1/customers/{customer-tenant-id}|[uzyskiwanie klienta według identyfikatora](get-a-customer-by-id.md)|
|{baseURL}/v1/productUpgrades/eligibility|[uzyskiwanie uprawnień do uaktualnienia produktu](get-eligibility-for-product-upgrade.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} |[zarządzanie subskrypcją](manage-orders.md#manage-a-subscription)|
|{baseURL}/v1/customers/{customer_id}/subscriptions |[get-all-of-a-customer-s-subscriptions](get-all-of-a-customer-s-subscriptions.md)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}|[Pobieranie subskrypcji według identyfikatora](get-a-subscription-by-id.md)|
|{baseURL}/v1/customers/{customer_id}/orders|[Pobierz wszystkie zamówienia klientów](get-all-of-a-customer-s-orders.md)|
|{baseURL}/v1/customers/{customer_id}/orders/{order_id}|[Pobieranie zamówienia według identyfikatora](get-an-order-by-id.md)|
|{baseURL}/v1/customers/{customer_id}/orders/{order_id}/provisioningstatus|[Pobieranie stanu aprowizacji subskrypcji](get-subscription-provisioning-status.md)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}|[Zarządzanie zamówieniami i zarządzanie subskrypcją](manage-orders.md#manage-a-subscription)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/addons|[Pobieranie listy dodatków dla subskrypcji](get-a-list-of-add-ons-for-a-subscription.md)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/azureEntitlements|[Uzyskiwanie listy uprawnień platformy Azure dla subskrypcji](get-a-list-of-azure-entitlements-for-subscription.md)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/registrationstatus|[Pobieranie stanu rejestracji subskrypcji](get-subscription-registration-status.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/transfers|[Uzyskiwanie wszystkich transferów klientów](get-all-of-a-customer-s-transfers.md)|
|{baseURL}/v1/productUpgrades/{upgrade-id}/status|[Pobieranie stanu uaktualniania produktu](get-product-upgrade-status.md)|
|{baseURL}/v1/customers/{identyfikator-klienta}/subscriptions/{subscription-id}/conversions|[Pobieranie listy ofert konwersji wersji próbnej](get-a-list-of-trial-conversion-offers.md)|


### <a name="error-code-response"></a>Odpowiedź z kodem błędu:
```http
HTTP/1.1 429 Too Many Requests 

Content-Length: 84 

Content-Type: application/json 

Retry-After: 57 

Date: Tue, 21 Jul 2020 04:10:58 GMT 

{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 57 seconds." } 
```

## <a name="example-of-activity-log"></a>Przykład dziennika aktywności

Aby uzyskać najlepsze rozwiązanie dotyczące analizowania dziennych zmian, zalecamy wykonywanie zapytań o rekord inspekcji dla określonego dnia. 

W odpowiedzi otrzymasz wynik ze zmianami określonego typu operacji.Możesz filtrować na podstawie operacji, która Cię zależy. Jeśli na przykład interesuje Cię nowo utworzony klient, możesz przyjrzeć się typowi operationType = "add_customer".  

Listę typów operacji/zasobów można znaleźć w poniższych dokumentacjach interfejsu API.  

- [Inspekcja zasobów](auditing-resources.md)  

- [Uzyskiwanie rekordu działania Partner Center przez użytkownika](get-a-record-of-partner-center-activity-by-user.md)  



### <a name="response-example"></a>Przykład odpowiedzi

**Żądanie**:  
```http
Http Get call:  https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50 

Authorization: Bearer <token> 

Accept: application/json 

MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893 

MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14 

X-Locale: en-US 

Host: api.partnercenter.microsoft.com 

Connection: Keep-Alive 
```

**Odpowiedź:**    
```http
{ 

    "totalCount": 17, 

    "items": [ 

        { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_e905b566-4779-4e57-944c-7b1b5312705b_updatecustomeruserlicenses_637346859797753934", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "e905b566-4779-4e57-944c-7b1b5312705b", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "FulfillmentService", 

            "resourceType": "license", 

            "operationType": "update_customer_user_licenses", 

            "operationDate": "2020-09-02T23:26:19.7753934Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "CustomerUserId", 

                    "value": "933808c7-b165-496c-a24e-1a4b7846fab4" 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

        { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_ia80zlkxp6ewoqpp35pbqjlhqv9iigvz1_createorder_637346662909268372", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "86bddccf-9a53-40c6-907c-08067a3f8da7", 

            "customerName": "CustomMetersStagingTest", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "4990cffe-04e8-4e8b-808a-1175604b879f", 

            "resourceType": "order", 

            "resourceNewValue": "{\"Id\":\"Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"AlternateId\":\"64144d300bde\",\"ReferenceCustomerId\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"BillingCycle\":\"monthly\",\"CurrencyCode\":\"USD\",\"CurrencySymbol\":\"$\",\"LineItems\":[{\"LineItemNumber\":0,\"ProvisioningContext\":null,\"OfferId\":\"DZH318Z0C964:0001:DZH318Z0BZDG\",\"SubscriptionId\":\"f428d44a-d08b-348b-579e-ce92a6362c7b\",\"ParentSubscriptionId\":null,\"TermDuration\":\"P1M\",\"TransactionType\":\"New\",\"FriendlyName\":\"SaaS custom meter offer - Bronze\",\"Quantity\":1,\"Pricing\":null,\"PartnerIdOnRecord\":null,\"RenewsTo\":null,\"Links\":{\"Product\":{\"Uri\":\"/products/DZH318Z0C964?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"Sku\":{\"Uri\":\"/products/DZH318Z0C964/skus/0001?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"Availability\":{\"Uri\":\"/products/DZH318Z0C964/skus/0001/availabilities/DZH318Z0BZDG?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"ActivationLinks\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/lineitems/0/activationlinks\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]}}}],\"CreationDate\":\"2020-09-02T17:58:01.7755853Z\",\"Status\":\"pending\",\"TransactionType\":\"UserPurchase\",\"Links\":{\"Self\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"ProvisioningStatus\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/provisioningstatus\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"PatchOperation\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"Method\":\"PATCH\",\"Body\":null,\"Headers\":[]}},\"Client\":{\"marketplaceCountry\":\"US\",\"deviceFamily\":\"UniversalStore-PartnerCenter\",\"name\":\"Partner Center Web\"},\"Attributes\":{\"ObjectType\":\"Order\"}}", 

            "operationType": "create_order", 

            "originalCorrelationId": "96514ebe-c1b2-4865-cb46-2c2d20a2e911", 

            "operationDate": "2020-09-02T17:58:10.9268372Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "OrderId", 

                    "value": "Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1" 

                }, 

                { 

                    "key": "AlternateId", 

                    "value": "64144d300bde" 

                }, 

                { 

                    "key": "BillingCycle", 

                    "value": "Monthly" 

                }, 

                { 

                    "key": "OfferId-0", 

                    "value": "DZH318Z0C964:0001:DZH318Z0BZDG" 

                }, 

                { 

                    "key": "SubscriptionId-0", 

                    "value": "f428d44a-d08b-348b-579e-ce92a6362c7b" 

                }, 

                { 

                    "key": "SubscriptionName-0", 

                    "value": "SaaS custom meter offer - Bronze" 

                }, 

                { 

                   "key": "Quantity-0", 

                    "value": "1" 

                }, 

                { 

                    "key": "PartnerOnRecord-0", 

                    "value": null 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

                           { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_86bddccf-9a53-40c6-907c-08067a3f8da7_addcustomer_637346648528069005", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "86bddccf-9a53-40c6-907c-08067a3f8da7", 

            "customerName": "CustomMetersStagingTest", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "4990cffe-04e8-4e8b-808a-1175604b879f", 

            "resourceType": "customer", 

            "resourceNewValue": "{\"Id\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"CommerceId\":\"9dd78b4f-f98a-44b4-a2fa-2b82ac58d24c\",\"CompanyProfile\":{\"TenantId\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"Domain\":\"CustomMetersStagingTest.onmicrosoft.com\",\"CompanyName\":\"CustomMetersStagingTest\",\"Address\":null,\"Email\":null,\"OrganizationRegistrationNumber\":null,\"Links\":{\"Self\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/profiles/company\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]}},\"Attributes\":{\"ObjectType\":\"CustomerCompanyProfile\"}},\"BillingProfile\":{\"Id\":\"4beafd7b-cdab-5bdc-52ed-02e16edf2e7a\",\"FirstName\":\"CustomMetersStagingTest\",\"LastName\":\"CustomMetersStagingTest\",\"Email\":\"CustomMetersStagingTest@CustomMetersStagingTest.com\",\"Culture\":\"en-US\",\"Language\":\"en\",\"CompanyName\":\"CustomMetersStagingTest\",\"DefaultAddress\":{\"Id\":null,\"Country\":\"US\",\"Region\":null,\"City\":\"Seattle\",\"State\":\"WA\",\"District\":null,\"AddressLine1\":\"CustomMetersStagingTest\",\"AddressLine2\":null,\"AddressLine3\":null,\"PostalCode\":\"98122\",\"FirstName\":\"CustomMetersStagingTest\",\"LastName\":\"CustomMetersStagingTest\",\"EmailAddress\":null,\"PhoneNumber\":null,\"MiddleName\":null},\"Attributes\":{\"Etag\":\"-2279334701316321663\",\"ObjectType\":\"CustomerBillingProfile\"}},\"RelationshipToPartner\":\"reseller\",\"AllowDelegatedAccess\":true,\"UserCredentials\":{\"userName\":\"admin\",\"password\":\"\"},\"AssociatedPartnerId\":null,\"CustomDomains\":null,\"Attributes\":{\"ObjectType\":\"Customer\"}}", 

            "operationType": "add_customer", 

            "originalCorrelationId": "7550d9ea-e64a-416f-e49b-3670c516cf69", 

            "operationDate": "2020-09-02T17:34:12.8069005Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "PrimaryDomainName", 

                    "value": "CustomMetersStagingTest.onmicrosoft.com" 

                }, 

                { 

                    "key": "Relationship", 

                    "value": "Reseller" 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

                            

        ... 

    ], 

    "links": { 

        "self": { 

            "uri": "/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50", 

            "method": "GET", 

            "headers": [] 

        } 

    }, 

    "attributes": { 

        "objectType": "Collection" 

    } 

} 
```
 

