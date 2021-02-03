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
# <a name="api-throttling-guidance-for-partners-calling-partner-center-apis"></a><span data-ttu-id="b425b-103">Wskazówki dotyczące ograniczania interfejsu API dla partnerów wywołujących interfejsy API Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="b425b-103">API throttling guidance for partners calling Partner Center APIs</span></span> 

<span data-ttu-id="b425b-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="b425b-104">**Applies to**</span></span>

- <span data-ttu-id="b425b-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="b425b-105">Partner Center</span></span>

<span data-ttu-id="b425b-106">Firma Microsoft implementuje funkcję ograniczania interfejsu API, aby zapewnić bardziej spójną wydajność w ramach przedziału czasu dla partnerów wywołujących interfejsy API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="b425b-106">Microsoft is implementing API throttling to allow more consistent performance within a time span for partners calling the Partner Center APIs.</span></span> <span data-ttu-id="b425b-107">Ograniczanie przepustowości ogranicza liczbę żądań do usługi w przedziale czasu, aby zapobiec nadmiernemu użyciu zasobów.</span><span class="sxs-lookup"><span data-stu-id="b425b-107">Throttling limits the number of requests to a service in a time span to prevent overuse of resources.</span></span> <span data-ttu-id="b425b-108">Centrum partnerskie zostało zaprojektowane z myślą o obsłudze dużej liczby żądań, w przypadku przeprowadzenia przeciążenia kilku partnerów, ograniczenie przepustowości pomaga zapewnić optymalną wydajność i niezawodność dla wszystkich partnerów.</span><span class="sxs-lookup"><span data-stu-id="b425b-108">While Partner Center is designed to handle a high volume of requests, if an overwhelming number of requests occur by few partners, throttling helps maintain optimal performance and reliability for all partners.</span></span>  

<span data-ttu-id="b425b-109">Limity ograniczania są różne w zależności od scenariusza.</span><span class="sxs-lookup"><span data-stu-id="b425b-109">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="b425b-110">Na przykład jeśli wykonujesz dużą liczbę operacji zapisu, możliwość ograniczania przepustowości jest wyższa niż w przypadku wykonywania operacji odczytu.</span><span class="sxs-lookup"><span data-stu-id="b425b-110">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="what-happens-when-throttling-occurs"></a><span data-ttu-id="b425b-111">Co się stanie w przypadku wystąpienia ograniczenia przepustowości?</span><span class="sxs-lookup"><span data-stu-id="b425b-111">What happens when throttling occurs?</span></span> 

<span data-ttu-id="b425b-112">W przypadku przekroczenia progu ograniczania Centrum partnerskiego ogranicza wszelkie dalsze żądania od tego klienta przez pewien czas.</span><span class="sxs-lookup"><span data-stu-id="b425b-112">When a throttling threshold is exceeded, Partner Center limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="b425b-113">Zachowanie ograniczania zależy od typu i liczby żądań.</span><span class="sxs-lookup"><span data-stu-id="b425b-113">Throttling behavior depends on the type and number of requests.</span></span>   

### <a name="common-throttling-scenarios"></a><span data-ttu-id="b425b-114">Typowe scenariusze ograniczania przepustowości</span><span class="sxs-lookup"><span data-stu-id="b425b-114">Common throttling scenarios</span></span> 

<span data-ttu-id="b425b-115">Najczęstszymi przyczynami ograniczania liczby klientów są:</span><span class="sxs-lookup"><span data-stu-id="b425b-115">The most common causes of throttling of clients include:</span></span> 

- <span data-ttu-id="b425b-116">**Duża liczba żądań dotyczących identyfikatora dzierżawy interfejsu API na partnera**: w przypadku niektórych interfejsów API Centrum partnerskiego ograniczenie przepustowości jest określane przez identyfikator dzierżawy partnera, zbyt wiele wywołań tych interfejsów API w ramach tego samego identyfikatora dzierżawy partnera spowoduje przekroczenie progu ograniczania przepustowości.</span><span class="sxs-lookup"><span data-stu-id="b425b-116">**A large number of requests for an API per Partner Tenant ID**: for some Partner Center APIs, throttling is determined by Partner Tenant ID, too many calls to those APIs on the same Partner Tenant ID will result in exceeding the throttling threshold.</span></span>  

- <span data-ttu-id="b425b-117">**Duża liczba żądań dotyczących identyfikatora dzierżawy interfejsu API na partnera na identyfikator dzierżawy klienta**: dla innych interfejsów API ograniczenie przepustowości jest określane przez partnera partnerskiego identyfikator dzierżawy/identyfikator dzierżawy klienta; w takich przypadkach zbyt wiele wywołań dla tego samego identyfikatora dzierżawy klienta spowoduje ograniczenie przepustowości — podczas gdy wywołania innych klientów mogą się powieść.</span><span class="sxs-lookup"><span data-stu-id="b425b-117">**A large number of requests for an API per Partner Tenant ID per Customer Tenant ID**: for other APIs, throttling is determined by Partner Tenant ID/Customer Tenant ID combination; in those cases, making too many calls against the same customer tenant ID will result in throttling - while calls against other customers may succeed.</span></span>

## <a name="best-practices-to-avoid-throttling"></a><span data-ttu-id="b425b-118">Najlepsze rozwiązania mające na celu uniknięcie ograniczenia przepustowości</span><span class="sxs-lookup"><span data-stu-id="b425b-118">Best practices to avoid throttling</span></span> 
 
<span data-ttu-id="b425b-119">Praktyki programistyczne, takie jak ciągłe sondowanie zasobu w celu sprawdzenia dostępności aktualizacji i regularnego skanowania kolekcji zasobów, aby sprawdzać, czy nowe lub usunięte zasoby są bardziej wydajne, mogą prowadzić do ograniczania przepustowości i obniżać ogólną wydajność.</span><span class="sxs-lookup"><span data-stu-id="b425b-119">Programming practices such as continuously polling a resource to check for updates and regularly scanning resource collections to check for new or deleted resources are more likely to lead to throttling and will degrade overall performance.</span></span> <span data-ttu-id="b425b-120">Współbieżne wywołania interfejsu API mogą prowadzić do dużej liczby żądań na jednostkę czasu, co spowoduje również ograniczenie żądań.</span><span class="sxs-lookup"><span data-stu-id="b425b-120">Concurrent API calls may lead to high number of requests per unit time, which will also cause requests to be throttled.</span></span> <span data-ttu-id="b425b-121">Zamiast tego należy użyć funkcji śledzenia zmian i powiadomień o zmianach.</span><span class="sxs-lookup"><span data-stu-id="b425b-121">You should instead leverage change tracking and change notifications.</span></span> <span data-ttu-id="b425b-122">Ponadto, aby uzyskać więcej informacji, [należy skorzystać z](get-a-record-of-partner-center-activity-by-user.md) dzienników aktywności w celu wykrycia zmian.</span><span class="sxs-lookup"><span data-stu-id="b425b-122">Additionally, you should be able to leverage activity logs for detecting changes, see [Partner Center activity logs](get-a-record-of-partner-center-activity-by-user.md) for more information.</span></span>  <span data-ttu-id="b425b-123">Zdecydowanie zalecamy, aby partnerzy mogli rozważyć użycie interfejsu API dziennika aktywności w celu zwiększenia wydajności i uniknięcia ograniczenia przepustowości.</span><span class="sxs-lookup"><span data-stu-id="b425b-123">We highly recommend partners to consider using the activity log API for more efficiency and to avoid throttling.</span></span> <span data-ttu-id="b425b-124">Zobacz również przykład korzystania z dzienników aktywności poniżej.</span><span class="sxs-lookup"><span data-stu-id="b425b-124">See also the example of using activity logs, below.</span></span>

## <a name="best-practices-to-handle-throttling"></a><span data-ttu-id="b425b-125">Najlepsze rozwiązania w zakresie obsługi ograniczania przepustowości</span><span class="sxs-lookup"><span data-stu-id="b425b-125">Best practices to handle throttling</span></span>

<span data-ttu-id="b425b-126">Poniżej przedstawiono najlepsze rozwiązania dotyczące obsługi ograniczania przepustowości:</span><span class="sxs-lookup"><span data-stu-id="b425b-126">The following are best practices for handling throttling:</span></span> 

- <span data-ttu-id="b425b-127">Zmniejsz stopień równoległości.</span><span class="sxs-lookup"><span data-stu-id="b425b-127">Reduce the degree of parallelism.</span></span> 
- <span data-ttu-id="b425b-128">Zmniejsz częstotliwość wywołań.</span><span class="sxs-lookup"><span data-stu-id="b425b-128">Reduce the frequency of calls.</span></span> 
- <span data-ttu-id="b425b-129">Unikaj natychmiastowych ponownych prób, ponieważ wszystkie żądania są naliczane względem limitów użycia.</span><span class="sxs-lookup"><span data-stu-id="b425b-129">Avoid immediate retries because all requests accrue against your usage limits.</span></span> 

<span data-ttu-id="b425b-130">Podczas wdrażania obsługi błędów użyj kodu błędu HTTP 429, aby wykryć ograniczenia przepustowości.</span><span class="sxs-lookup"><span data-stu-id="b425b-130">When you implement error handling, use the HTTP error code 429 to detect throttling.</span></span> <span data-ttu-id="b425b-131">Odpowiedź zakończona niepowodzeniem zawiera nagłówek odpowiedzi Retry-After.</span><span class="sxs-lookup"><span data-stu-id="b425b-131">The failed response includes the Retry-After response header.</span></span> <span data-ttu-id="b425b-132">Tworzenie kopii zapasowych żądań przy użyciu opóźnienia ponawiania jest najszybszym sposobem na odzyskanie sprawności przed ograniczeniem.</span><span class="sxs-lookup"><span data-stu-id="b425b-132">Backing off requests using the Retry-after delay is the fastest way to recover from throttling.</span></span> 

<span data-ttu-id="b425b-133">Aby użyć opóźnień po ponownym uruchomieniu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b425b-133">To use the Retry-after delay, do the following:</span></span> 

1. <span data-ttu-id="b425b-134">Zaczekaj liczbę sekund określoną w nagłówku Retry-After.</span><span class="sxs-lookup"><span data-stu-id="b425b-134">Wait the number of seconds specified in the Retry-After header.</span></span> 

2. <span data-ttu-id="b425b-135">Ponów żądanie.</span><span class="sxs-lookup"><span data-stu-id="b425b-135">Retry the request.</span></span>  

3. <span data-ttu-id="b425b-136">Jeśli żądanie kończy się niepowodzeniem z kodem błędu 429, nadal jest ograniczany.</span><span class="sxs-lookup"><span data-stu-id="b425b-136">If the request fails again with a 429 error code, you are still being throttled.</span></span> <span data-ttu-id="b425b-137">Spróbuj ponownie za pomocą wykładniczej wycofywania, użyj zalecanego opóźnienia Retry-After i ponów próbę żądania, dopóki to się nie powiedzie.</span><span class="sxs-lookup"><span data-stu-id="b425b-137">Retry with Exponential backoff, use the recommended Retry-After delay and retry the request until it succeeds.</span></span>

4. <span data-ttu-id="b425b-138">Jeśli używasz zestawu SDK, otrzymasz wyjątek z kodem stanu 429, gdy żądanie jest ograniczone.</span><span class="sxs-lookup"><span data-stu-id="b425b-138">If you are using SDK you'll receive an exception with status code 429 when your request is being throttled.</span></span> <span data-ttu-id="b425b-139">Użyj właściwości RetryAfter w wyjątku i ponów próbę żądania po upływie czasu.</span><span class="sxs-lookup"><span data-stu-id="b425b-139">Use the RetryAfter property in the exception and retry the request after the time is elapsed.</span></span>


## <a name="apis-currently-impacted-by-throttling"></a><span data-ttu-id="b425b-140">Interfejsy API, na które obecnie wpływają ograniczenia</span><span class="sxs-lookup"><span data-stu-id="b425b-140">APIs currently impacted by throttling</span></span>

<span data-ttu-id="b425b-141">W długim przebiegu każdy interfejs API Centrum partnerskiego, który wywołuje punkt końcowy "api.partnercenter.microsoft.com/", zostanie ograniczony.</span><span class="sxs-lookup"><span data-stu-id="b425b-141">In the long run, every single Partner Center API that calls the endpoint “api.partnercenter.microsoft.com/” will be throttled.</span></span> <span data-ttu-id="b425b-142">Obecnie limity ograniczania są wymuszane tylko w przypadku kilku interfejsów API wymienionych poniżej.</span><span class="sxs-lookup"><span data-stu-id="b425b-142">Currently, the throttling limits are only enforced on the few APIs listed below.</span></span> <span data-ttu-id="b425b-143">Centrum partnerskie będzie zbierać dane telemetryczne dla każdego z interfejsów API i dynamicznie dostosowuje limity ograniczania.</span><span class="sxs-lookup"><span data-stu-id="b425b-143">Partner Center will be collecting the telemetry on each of the APIs and will dynamically adjust the throttling limits.</span></span> <span data-ttu-id="b425b-144">W poniższej tabeli wymieniono interfejsy API, w których obecnie wymuszane jest ograniczanie przepustowości.</span><span class="sxs-lookup"><span data-stu-id="b425b-144">The following table lists the APIs where throttling is currently enforced.</span></span>  


|<span data-ttu-id="b425b-145">**Operacja**</span><span class="sxs-lookup"><span data-stu-id="b425b-145">**Operation**</span></span>| <span data-ttu-id="b425b-146">**Dokumentacja Centrum partnerskiego**</span><span class="sxs-lookup"><span data-stu-id="b425b-146">**Partner Center documentation**</span></span>|       
|------------------------|----------------------------|
|<span data-ttu-id="b425b-147">{baseURL}/V1/Customers/{customer_id}/Orders</span><span class="sxs-lookup"><span data-stu-id="b425b-147">{baseURL}/v1/customers/{customer_id}/orders</span></span>|[<span data-ttu-id="b425b-148">Tworzenie zamówienia</span><span class="sxs-lookup"><span data-stu-id="b425b-148">create an order</span></span>](create-an-order.md)|
|<span data-ttu-id="b425b-149">{baseURL}/V1/Customers/{Customer-tenant-ID}/subscriptions/{ID-for-Subscription}/Upgrades</span><span class="sxs-lookup"><span data-stu-id="b425b-149">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades</span></span>|[<span data-ttu-id="b425b-150">przejście do subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b425b-150">transition a subscription</span></span>](transition-a-subscription.md)|
|<span data-ttu-id="b425b-151">{baseURL}/V1/Customers/{Customer-tenant-ID}/Orders/{Order-ID}</span><span class="sxs-lookup"><span data-stu-id="b425b-151">{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}</span></span>|[<span data-ttu-id="b425b-152">Kupowanie dodatku do subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b425b-152">purchase an addon to a subscription</span></span>](purchase-an-add-on-to-a-subscription.md)|
|<span data-ttu-id="b425b-153">{baseURL}/V1/Customers/{Customer-ID}/Carts/{Cart-ID}</span><span class="sxs-lookup"><span data-stu-id="b425b-153">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span></span>|[<span data-ttu-id="b425b-154">Tworzenie koszyka</span><span class="sxs-lookup"><span data-stu-id="b425b-154">create a cart</span></span>](create-a-cart.md)|
|<span data-ttu-id="b425b-155">{baseURL}/V1/Customers/{Customer-ID}/Carts/{Cart-ID}/Checkout</span><span class="sxs-lookup"><span data-stu-id="b425b-155">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout</span></span>|[<span data-ttu-id="b425b-156">Wyewidencjonowywanie koszyka</span><span class="sxs-lookup"><span data-stu-id="b425b-156">checkout a cart</span></span>](checkout-a-cart.md)|
|<span data-ttu-id="b425b-157">{baseURL}/V1/Customers/{Customer-ID}/Carts/{Cart-ID}</span><span class="sxs-lookup"><span data-stu-id="b425b-157">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span></span>|[<span data-ttu-id="b425b-158">Aktualizowanie koszyka</span><span class="sxs-lookup"><span data-stu-id="b425b-158">update a cart</span></span>](update-a-cart.md)|
|<span data-ttu-id="b425b-159">{baseURL}/V1/Customers/{Customer-ID}/subscriptions/{Subscription-ID}/registrations</span><span class="sxs-lookup"><span data-stu-id="b425b-159">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations</span></span>|[<span data-ttu-id="b425b-160">Rejestrowanie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b425b-160">register a subscription</span></span>](register-a-subscription.md)|
|<span data-ttu-id="b425b-161">{baseURL}/V1/productupgrades</span><span class="sxs-lookup"><span data-stu-id="b425b-161">{baseURL}/v1/productupgrades</span></span>|[<span data-ttu-id="b425b-162">Utwórz jednostkę uaktualnienia produktu</span><span class="sxs-lookup"><span data-stu-id="b425b-162">create product upgrade entity</span></span>](create-product-upgrade-entity.md)|
|<span data-ttu-id="b425b-163">{baseURL}/V1/Customers/{Customer-ID}/subscriptions/{Subscription-ID}/Conversions</span><span class="sxs-lookup"><span data-stu-id="b425b-163">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span></span> |[<span data-ttu-id="b425b-164">Konwertuj subskrypcję wersji próbnej na płatną</span><span class="sxs-lookup"><span data-stu-id="b425b-164">convert a trial subscription to paid</span></span>](convert-a-trial-subscription-to-paid.md)|
|<span data-ttu-id="b425b-165">{baseURL}/V1/Customers/{Customer-tenant-ID}</span><span class="sxs-lookup"><span data-stu-id="b425b-165">{baseURL}/v1/customers/{customer-tenant-id}</span></span>|[<span data-ttu-id="b425b-166">Uzyskaj klienta według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="b425b-166">get a customer by id</span></span>](get-a-customer-by-id.md)|
|<span data-ttu-id="b425b-167">{baseURL}/v1/productUpgrades/eligibility</span><span class="sxs-lookup"><span data-stu-id="b425b-167">{baseURL}/v1/productUpgrades/eligibility</span></span>|[<span data-ttu-id="b425b-168">Uzyskaj uprawnienia do uaktualniania produktu</span><span class="sxs-lookup"><span data-stu-id="b425b-168">get eligibility for product upgrade</span></span>](get-eligibility-for-product-upgrade.md)|
|<span data-ttu-id="b425b-169">{baseURL}/V1/Customers/{Customer-tenant-ID}/subscriptions/{ID-for-Subscription}</span><span class="sxs-lookup"><span data-stu-id="b425b-169">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}</span></span> |[<span data-ttu-id="b425b-170">Zarządzaj subskrypcją</span><span class="sxs-lookup"><span data-stu-id="b425b-170">manage subscription</span></span>](manage-orders.md#manage-a-subscription)|


### <a name="error-code-response"></a><span data-ttu-id="b425b-171">Odpowiedź kodu błędu:</span><span class="sxs-lookup"><span data-stu-id="b425b-171">Error code response:</span></span>
```http
HTTP/1.1 429 Too Many Requests 

Content-Length: 84 

Content-Type: application/json 

Retry-After: 57 

Date: Tue, 21 Jul 2020 04:10:58 GMT 

{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 57 seconds." } 
```

## <a name="example-of-activity-log"></a><span data-ttu-id="b425b-172">Przykład dziennika aktywności</span><span class="sxs-lookup"><span data-stu-id="b425b-172">Example of activity log</span></span>

<span data-ttu-id="b425b-173">Aby uzyskać najlepsze rozwiązania w zakresie analizowania codziennych zmian, zalecamy wykonanie zapytania o rekord inspekcji w określonym dniu.</span><span class="sxs-lookup"><span data-stu-id="b425b-173">For best practice in analyzing daily changes, we recommend that you query audit record for a specific day.</span></span> 

<span data-ttu-id="b425b-174">W odpowiedzi otrzymasz wynik ze zmianami w określonym typie operacji.</span><span class="sxs-lookup"><span data-stu-id="b425b-174">In the response, you will get a result with changes to specific operation type.</span></span><span data-ttu-id="b425b-175">Można filtrować na podstawie pożądanej operacji.</span><span class="sxs-lookup"><span data-stu-id="b425b-175">  You can filter based on the operation you care about.</span></span> <span data-ttu-id="b425b-176">Na przykład jeśli interesuje Cię nowo utworzony klient, możesz przyjrzeć się operacji OperationType = "add_customer".</span><span class="sxs-lookup"><span data-stu-id="b425b-176"> For example, if you are interested in a newly created customer, you can look at operationType = “add_customer”.</span></span>  

<span data-ttu-id="b425b-177">Listę elementów OperationType/zasobów można znaleźć w poniższych dokumentach interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="b425b-177">List of operationtype/resources can be found in below API docs.</span></span>  

- [<span data-ttu-id="b425b-178">Inspekcja zasobów</span><span class="sxs-lookup"><span data-stu-id="b425b-178">Auditing resources</span></span>](auditing-resources.md)  

- [<span data-ttu-id="b425b-179">Pobierz rekord działania Centrum partnerskiego według użytkownika</span><span class="sxs-lookup"><span data-stu-id="b425b-179">Get a record of a Partner Center activity by user</span></span>](get-a-record-of-partner-center-activity-by-user.md)  



### <a name="response-example"></a><span data-ttu-id="b425b-180">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b425b-180">Response example</span></span>

<span data-ttu-id="b425b-181">**Żądanie**:</span><span class="sxs-lookup"><span data-stu-id="b425b-181">**Request**:</span></span>  
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

<span data-ttu-id="b425b-182">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="b425b-182">**Response**:</span></span>    
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
 

