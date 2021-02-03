---
title: Wskazówki dotyczące ograniczania przepustowości interfejsu API
description: W przypadku partnerów wywołujących interfejsy API Centrum partnerskiego można dowiedzieć się, które interfejsy API mają wpływ na ograniczanie interfejsu API firmy Microsoft i najlepsze rozwiązania mające na celu uniknięcie lub lepsze ograniczenie obsługi.
ms.date: 09/09/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: a52751a97e699050075c1aac910cc51e94514f26
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "97770235"
---
# <a name="api-throttling-guidance-for-partners-calling-partner-center-apis"></a>Wskazówki dotyczące ograniczania interfejsu API dla partnerów wywołujących interfejsy API Centrum partnerskiego 

**Dotyczy**

- Centrum partnerskie

Firma Microsoft implementuje funkcję ograniczania interfejsu API, aby zapewnić bardziej spójną wydajność w ramach przedziału czasu dla partnerów wywołujących interfejsy API Centrum partnerskiego. Ograniczanie przepustowości ogranicza liczbę żądań do usługi w przedziale czasu, aby zapobiec nadmiernemu użyciu zasobów. Centrum partnerskie zostało zaprojektowane z myślą o obsłudze dużej liczby żądań, w przypadku przeprowadzenia przeciążenia kilku partnerów, ograniczenie przepustowości pomaga zapewnić optymalną wydajność i niezawodność dla wszystkich partnerów.  

Limity ograniczania są różne w zależności od scenariusza. Na przykład jeśli wykonujesz dużą liczbę operacji zapisu, możliwość ograniczania przepustowości jest wyższa niż w przypadku wykonywania operacji odczytu.

## <a name="what-happens-when-throttling-occurs"></a>Co się stanie w przypadku wystąpienia ograniczenia przepustowości? 

W przypadku przekroczenia progu ograniczania Centrum partnerskiego ogranicza wszelkie dalsze żądania od tego klienta przez pewien czas. Zachowanie ograniczania zależy od typu i liczby żądań.   

### <a name="common-throttling-scenarios"></a>Typowe scenariusze ograniczania przepustowości 

Najczęstszymi przyczynami ograniczania liczby klientów są: 

- **Duża liczba żądań dotyczących identyfikatora dzierżawy interfejsu API na partnera**: w przypadku niektórych interfejsów API Centrum partnerskiego ograniczenie przepustowości jest określane przez identyfikator dzierżawy partnera, zbyt wiele wywołań tych interfejsów API w ramach tego samego identyfikatora dzierżawy partnera spowoduje przekroczenie progu ograniczania przepustowości.  

- **Duża liczba żądań dotyczących identyfikatora dzierżawy interfejsu API na partnera na identyfikator dzierżawy klienta**: dla innych interfejsów API ograniczenie przepustowości jest określane przez partnera partnerskiego identyfikator dzierżawy/identyfikator dzierżawy klienta; w takich przypadkach zbyt wiele wywołań dla tego samego identyfikatora dzierżawy klienta spowoduje ograniczenie przepustowości — podczas gdy wywołania innych klientów mogą się powieść.

## <a name="best-practices-to-avoid-throttling"></a>Najlepsze rozwiązania mające na celu uniknięcie ograniczenia przepustowości 
 
Praktyki programistyczne, takie jak ciągłe sondowanie zasobu w celu sprawdzenia dostępności aktualizacji i regularnego skanowania kolekcji zasobów, aby sprawdzać, czy nowe lub usunięte zasoby są bardziej wydajne, mogą prowadzić do ograniczania przepustowości i obniżać ogólną wydajność. Współbieżne wywołania interfejsu API mogą prowadzić do dużej liczby żądań na jednostkę czasu, co spowoduje również ograniczenie żądań. Zamiast tego należy użyć funkcji śledzenia zmian i powiadomień o zmianach. Ponadto, aby uzyskać więcej informacji, [należy skorzystać z](get-a-record-of-partner-center-activity-by-user.md) dzienników aktywności w celu wykrycia zmian.  Zdecydowanie zalecamy, aby partnerzy mogli rozważyć użycie interfejsu API dziennika aktywności w celu zwiększenia wydajności i uniknięcia ograniczenia przepustowości. Zobacz również przykład korzystania z dzienników aktywności poniżej.

## <a name="best-practices-to-handle-throttling"></a>Najlepsze rozwiązania w zakresie obsługi ograniczania przepustowości

Poniżej przedstawiono najlepsze rozwiązania dotyczące obsługi ograniczania przepustowości: 

- Zmniejsz stopień równoległości. 
- Zmniejsz częstotliwość wywołań. 
- Unikaj natychmiastowych ponownych prób, ponieważ wszystkie żądania są naliczane względem limitów użycia. 

Podczas wdrażania obsługi błędów użyj kodu błędu HTTP 429, aby wykryć ograniczenia przepustowości. Odpowiedź zakończona niepowodzeniem zawiera nagłówek odpowiedzi Retry-After. Tworzenie kopii zapasowych żądań przy użyciu opóźnienia ponawiania jest najszybszym sposobem na odzyskanie sprawności przed ograniczeniem. 

Aby użyć opóźnień po ponownym uruchomieniu, wykonaj następujące czynności: 

1. Zaczekaj liczbę sekund określoną w nagłówku Retry-After. 

2. Ponów żądanie.  

3. Jeśli żądanie kończy się niepowodzeniem z kodem błędu 429, nadal jest ograniczany. Spróbuj ponownie za pomocą wykładniczej wycofywania, użyj zalecanego opóźnienia Retry-After i ponów próbę żądania, dopóki to się nie powiedzie.

4. Jeśli używasz zestawu SDK, otrzymasz wyjątek z kodem stanu 429, gdy żądanie jest ograniczone. Użyj właściwości RetryAfter w wyjątku i ponów próbę żądania po upływie czasu.


## <a name="apis-currently-impacted-by-throttling"></a>Interfejsy API, na które obecnie wpływają ograniczenia

W długim przebiegu każdy interfejs API Centrum partnerskiego, który wywołuje punkt końcowy "api.partnercenter.microsoft.com/", zostanie ograniczony. Obecnie limity ograniczania są wymuszane tylko w przypadku kilku interfejsów API wymienionych poniżej. Centrum partnerskie będzie zbierać dane telemetryczne dla każdego z interfejsów API i dynamicznie dostosowuje limity ograniczania. W poniższej tabeli wymieniono interfejsy API, w których obecnie wymuszane jest ograniczanie przepustowości.  


|**Operacja**| **Dokumentacja Centrum partnerskiego**|       
|------------------------|----------------------------|
|{baseURL}/V1/Customers/{customer_id}/Orders|[Tworzenie zamówienia](create-an-order.md)|
|{baseURL}/V1/Customers/{Customer-tenant-ID}/subscriptions/{ID-for-Subscription}/Upgrades|[przejście do subskrypcji](transition-a-subscription.md)|
|{baseURL}/V1/Customers/{Customer-tenant-ID}/Orders/{Order-ID}|[Kupowanie dodatku do subskrypcji](purchase-an-add-on-to-a-subscription.md)|
|{baseURL}/V1/Customers/{Customer-ID}/Carts/{Cart-ID}|[Tworzenie koszyka](create-a-cart.md)|
|{baseURL}/V1/Customers/{Customer-ID}/Carts/{Cart-ID}/Checkout|[Wyewidencjonowywanie koszyka](checkout-a-cart.md)|
|{baseURL}/V1/Customers/{Customer-ID}/Carts/{Cart-ID}|[Aktualizowanie koszyka](update-a-cart.md)|
|{baseURL}/V1/Customers/{Customer-ID}/subscriptions/{Subscription-ID}/registrations|[Rejestrowanie subskrypcji](register-a-subscription.md)|
|{baseURL}/V1/productupgrades|[Utwórz jednostkę uaktualnienia produktu](create-product-upgrade-entity.md)|
|{baseURL}/V1/Customers/{Customer-ID}/subscriptions/{Subscription-ID}/Conversions |[Konwertuj subskrypcję wersji próbnej na płatną](convert-a-trial-subscription-to-paid.md)|
|{baseURL}/V1/Customers/{Customer-tenant-ID}|[Uzyskaj klienta według identyfikatora](get-a-customer-by-id.md)|
|{baseURL}/v1/productUpgrades/eligibility|[Uzyskaj uprawnienia do uaktualniania produktu](get-eligibility-for-product-upgrade.md)|
|{baseURL}/V1/Customers/{Customer-tenant-ID}/subscriptions/{ID-for-Subscription} |[Zarządzaj subskrypcją](manage-orders.md#manage-a-subscription)|


### <a name="error-code-response"></a>Odpowiedź kodu błędu:
```http
HTTP/1.1 429 Too Many Requests 

Content-Length: 84 

Content-Type: application/json 

Retry-After: 57 

Date: Tue, 21 Jul 2020 04:10:58 GMT 

{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 57 seconds." } 
```

## <a name="example-of-activity-log"></a>Przykład dziennika aktywności

Aby uzyskać najlepsze rozwiązania w zakresie analizowania codziennych zmian, zalecamy wykonanie zapytania o rekord inspekcji w określonym dniu. 

W odpowiedzi otrzymasz wynik ze zmianami w określonym typie operacji.Można filtrować na podstawie pożądanej operacji. Na przykład jeśli interesuje Cię nowo utworzony klient, możesz przyjrzeć się operacji OperationType = "add_customer".  

Listę elementów OperationType/zasobów można znaleźć w poniższych dokumentach interfejsu API.  

- [Inspekcja zasobów](auditing-resources.md)  

- [Pobierz rekord działania Centrum partnerskiego według użytkownika](get-a-record-of-partner-center-activity-by-user.md)  



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

**Odpowiedź**:    
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
 

