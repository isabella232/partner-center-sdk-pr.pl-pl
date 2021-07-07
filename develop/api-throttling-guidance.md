---
title: Wskazówki dotyczące ograniczania przepustowości interfejsu API
description: W przypadku partnerów wywołujących Partner Center API dowiedz się, na które interfejsy API ma wpływ ograniczanie przepustowości interfejsów API firmy Microsoft, oraz poznaj najlepsze rozwiązania, aby uniknąć lub lepiej obsłużyć ograniczanie przepustowości.
ms.date: 04/14/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: f18518e88b9bb08d4fd248922f4ce2fefdde004f
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025653"
---
# <a name="api-throttling-guidance-for-partners-calling-partner-center-apis"></a><span data-ttu-id="62a5f-103">Wskazówki dotyczące ograniczania interfejsu API dla partnerów wywołujących Partner Center API</span><span class="sxs-lookup"><span data-stu-id="62a5f-103">API throttling guidance for partners calling Partner Center APIs</span></span> 

<span data-ttu-id="62a5f-104">Firma Microsoft implementuje ograniczanie interfejsów API, aby zapewnić bardziej spójną wydajność w okresie dla partnerów wywołujących interfejsy API Partner Center.</span><span class="sxs-lookup"><span data-stu-id="62a5f-104">Microsoft is implementing API throttling to allow more consistent performance within a time span for partners calling the Partner Center APIs.</span></span> <span data-ttu-id="62a5f-105">Ograniczanie ogranicza liczbę żądań do usługi w czasie, aby zapobiec wywłaszceniu zasobów.</span><span class="sxs-lookup"><span data-stu-id="62a5f-105">Throttling limits the number of requests to a service in a time span to prevent overuse of resources.</span></span> <span data-ttu-id="62a5f-106">Chociaż Partner Center jest przeznaczona do obsługi dużej liczby żądań, jeśli przytłaczającą liczbę żądań jest wielu partnerów, ograniczanie przepływności pomaga zachować optymalną wydajność i niezawodność dla wszystkich partnerów.</span><span class="sxs-lookup"><span data-stu-id="62a5f-106">While Partner Center is designed to handle a high volume of requests, if an overwhelming number of requests occur by few partners, throttling helps maintain optimal performance and reliability for all partners.</span></span>  

<span data-ttu-id="62a5f-107">Limity ograniczania różnią się w zależności od scenariusza.</span><span class="sxs-lookup"><span data-stu-id="62a5f-107">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="62a5f-108">Jeśli na przykład wykonujesz dużą liczbę operacji zapisu, możliwość ograniczenia jest większa niż w przypadku wykonywania tylko operacji odczytu.</span><span class="sxs-lookup"><span data-stu-id="62a5f-108">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="what-happens-when-throttling-occurs"></a><span data-ttu-id="62a5f-109">Co się stanie, gdy wystąpi ograniczanie przepustowości?</span><span class="sxs-lookup"><span data-stu-id="62a5f-109">What happens when throttling occurs?</span></span> 

<span data-ttu-id="62a5f-110">Po przekroczeniu progu ograniczania Partner Center ogranicza wszelkie dalsze żądania od tego klienta na określony czas.</span><span class="sxs-lookup"><span data-stu-id="62a5f-110">When a throttling threshold is exceeded, Partner Center limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="62a5f-111">Zachowanie ograniczania zależy od typu i liczby żądań.</span><span class="sxs-lookup"><span data-stu-id="62a5f-111">Throttling behavior depends on the type and number of requests.</span></span>   

### <a name="common-throttling-scenarios"></a><span data-ttu-id="62a5f-112">Typowe scenariusze ograniczania przepustowości</span><span class="sxs-lookup"><span data-stu-id="62a5f-112">Common throttling scenarios</span></span> 

<span data-ttu-id="62a5f-113">Najczęstsze przyczyny ograniczania przepustowości klientów to:</span><span class="sxs-lookup"><span data-stu-id="62a5f-113">The most common causes of throttling of clients include:</span></span> 

- <span data-ttu-id="62a5f-114">**Duża liczba** żądań interfejsu API na identyfikator dzierżawy partnera: w przypadku niektórych interfejsów API programu Partner Center ograniczanie jest określane przez identyfikator dzierżawy partnera. Zbyt wiele wywołań tych interfejsów API w tym samym identyfikatorze dzierżawy partnera spowoduje przekroczenie progu ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="62a5f-114">**A large number of requests for an API per Partner Tenant ID**: for some Partner Center APIs, throttling is determined by Partner Tenant ID, too many calls to those APIs on the same Partner Tenant ID will result in exceeding the throttling threshold.</span></span>  

- <span data-ttu-id="62a5f-115">**Duża liczba żądań interfejsu API** na identyfikator dzierżawy partnera na identyfikator dzierżawy klienta: w przypadku innych interfejsów API ograniczanie jest określane przez kombinację identyfikatora dzierżawy partnera/identyfikatora dzierżawy klienta. W takich przypadkach wykonanie zbyt wielu wywołań dla tego samego identyfikatora dzierżawy klienta spowoduje ograniczenie przepustowości , podczas gdy wywołania względem innych klientów mogą zakończyć się powodzeniem.</span><span class="sxs-lookup"><span data-stu-id="62a5f-115">**A large number of requests for an API per Partner Tenant ID per Customer Tenant ID**: for other APIs, throttling is determined by Partner Tenant ID/Customer Tenant ID combination; in those cases, making too many calls against the same customer tenant ID will result in throttling - while calls against other customers may succeed.</span></span>

## <a name="best-practices-to-avoid-throttling"></a><span data-ttu-id="62a5f-116">Najlepsze rozwiązania w celu uniknięcia ograniczania przepustowości</span><span class="sxs-lookup"><span data-stu-id="62a5f-116">Best practices to avoid throttling</span></span> 
 
<span data-ttu-id="62a5f-117">Praktyki programowania, takie jak ciągłe sondowanie zasobu w celu sprawdzenia, czy są dostępne aktualizacje, oraz regularne skanowanie kolekcji zasobów w celu sprawdzenia nowych lub usuniętych zasobów, mogą prowadzić do ograniczenia wydajności i obniżyć ogólną wydajność.</span><span class="sxs-lookup"><span data-stu-id="62a5f-117">Programming practices such as continuously polling a resource to check for updates and regularly scanning resource collections to check for new or deleted resources are more likely to lead to throttling and will degrade overall performance.</span></span> <span data-ttu-id="62a5f-118">Współbieżne wywołania interfejsu API mogą prowadzić do dużej liczby żądań na jednostkę czasu, co spowoduje również ograniczenie żądań.</span><span class="sxs-lookup"><span data-stu-id="62a5f-118">Concurrent API calls may lead to high number of requests per unit time, which will also cause requests to be throttled.</span></span> <span data-ttu-id="62a5f-119">Zamiast tego należy używać śledzenia zmian i powiadomień o zmianach.</span><span class="sxs-lookup"><span data-stu-id="62a5f-119">You should instead use change tracking and change notifications.</span></span> <span data-ttu-id="62a5f-120">Ponadto powinno być możliwe wykrywanie zmian za pomocą dzienników aktywności.</span><span class="sxs-lookup"><span data-stu-id="62a5f-120">Additionally, you should be able to use activity logs for detecting changes.</span></span> <span data-ttu-id="62a5f-121">Aby uzyskać więcej informacji, [zobacz Partner Center aktywności.](get-a-record-of-partner-center-activity-by-user.md)</span><span class="sxs-lookup"><span data-stu-id="62a5f-121">For more information, see [Partner Center activity logs](get-a-record-of-partner-center-activity-by-user.md).</span></span>  <span data-ttu-id="62a5f-122">Zdecydowanie zalecamy partnerom rozważenie użycia interfejsu API dziennika aktywności w celu zwiększenia wydajności i uniknięcia ograniczania.</span><span class="sxs-lookup"><span data-stu-id="62a5f-122">We highly recommend partners to consider using the activity log API for more efficiency and to avoid throttling.</span></span> <span data-ttu-id="62a5f-123">Zobacz również przykład użycia dzienników aktywności poniżej.</span><span class="sxs-lookup"><span data-stu-id="62a5f-123">See also the example of using activity logs, below.</span></span>

## <a name="best-practices-to-handle-throttling"></a><span data-ttu-id="62a5f-124">Najlepsze rozwiązania dotyczące obsługi ograniczania przepustowości</span><span class="sxs-lookup"><span data-stu-id="62a5f-124">Best practices to handle throttling</span></span>

<span data-ttu-id="62a5f-125">Poniżej przedstawiono najlepsze rozwiązania dotyczące obsługi ograniczania przepustowości:</span><span class="sxs-lookup"><span data-stu-id="62a5f-125">The following are best practices for handling throttling:</span></span> 

- <span data-ttu-id="62a5f-126">Zmniejsz stopień równoległości.</span><span class="sxs-lookup"><span data-stu-id="62a5f-126">Reduce the degree of parallelism.</span></span> 
- <span data-ttu-id="62a5f-127">Zmniejsz częstotliwość wywołań.</span><span class="sxs-lookup"><span data-stu-id="62a5f-127">Reduce the frequency of calls.</span></span> 
- <span data-ttu-id="62a5f-128">Unikaj natychmiastowych ponownych prób, ponieważ wszystkie żądania są naliczane względem limitów użycia.</span><span class="sxs-lookup"><span data-stu-id="62a5f-128">Avoid immediate retries because all requests accrue against your usage limits.</span></span> 

<span data-ttu-id="62a5f-129">Podczas wdrażania obsługi błędów użyj kodu błędu HTTP 429, aby wykryć ograniczenia przepustowości.</span><span class="sxs-lookup"><span data-stu-id="62a5f-129">When you implement error handling, use the HTTP error code 429 to detect throttling.</span></span> <span data-ttu-id="62a5f-130">Odpowiedź, która zakończyła się niepowodzeniem, zawiera Retry-After odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="62a5f-130">The failed response includes the Retry-After response header.</span></span> <span data-ttu-id="62a5f-131">Backing off requests using the Retry-after delay (Ponawianie żądań po opóźnieniu) to najszybszy sposób odzyskania danych po ograniczaniu przepustowości.</span><span class="sxs-lookup"><span data-stu-id="62a5f-131">Backing off requests using the Retry-after delay is the fastest way to recover from throttling.</span></span> 

<span data-ttu-id="62a5f-132">Aby użyć opóźnienia Ponów po, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="62a5f-132">To use the Retry-after delay, do the following:</span></span> 

1. <span data-ttu-id="62a5f-133">Poczekaj liczbę sekund określoną w nagłówku Retry-After ciągu.</span><span class="sxs-lookup"><span data-stu-id="62a5f-133">Wait the number of seconds specified in the Retry-After header.</span></span> 

2. <span data-ttu-id="62a5f-134">Ponów próbę żądania.</span><span class="sxs-lookup"><span data-stu-id="62a5f-134">Retry the request.</span></span>  

3. <span data-ttu-id="62a5f-135">Jeśli żądanie ponownie zakończy się niepowodzeniem z kodem błędu 429, nadal trwa ograniczanie.</span><span class="sxs-lookup"><span data-stu-id="62a5f-135">If the request fails again with a 429 error code, you are still being throttled.</span></span> <span data-ttu-id="62a5f-136">Ponów próbę przy użyciu wykładniczego odroczania, użyj zalecanego Retry-After i ponów próbę żądania, aż zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="62a5f-136">Retry with Exponential backoff, use the recommended Retry-After delay and retry the request until it succeeds.</span></span>

4. <span data-ttu-id="62a5f-137">Jeśli używasz zestawu SDK, otrzymasz wyjątek z kodem stanu 429, gdy żądanie jest ograniczane.</span><span class="sxs-lookup"><span data-stu-id="62a5f-137">If you are using the SDK, you'll receive an exception with status code 429 when your request is being throttled.</span></span> <span data-ttu-id="62a5f-138">Użyj właściwości RetryAfter w wyjątku i ponów próbę żądania po upływie czasu.</span><span class="sxs-lookup"><span data-stu-id="62a5f-138">Use the RetryAfter property in the exception and retry the request after the time is elapsed.</span></span>


## <a name="apis-currently-impacted-by-throttling"></a><span data-ttu-id="62a5f-139">Interfejsy API, na które ma obecnie wpływ ograniczanie przepustowości</span><span class="sxs-lookup"><span data-stu-id="62a5f-139">APIs currently impacted by throttling</span></span>

<span data-ttu-id="62a5f-140">W końcu każdy pojedynczy interfejs API Partner Center, który wywołuje punkt końcowy "api.partnercenter.microsoft.com/", będzie ograniczany.</span><span class="sxs-lookup"><span data-stu-id="62a5f-140">In the end, every single Partner Center API that calls the endpoint “api.partnercenter.microsoft.com/” will be throttled.</span></span> <span data-ttu-id="62a5f-141">Obecnie limity ograniczania są wymuszane tylko dla interfejsów API wymienionych poniżej.</span><span class="sxs-lookup"><span data-stu-id="62a5f-141">Currently, the throttling limits are only enforced on the APIs listed below.</span></span> <span data-ttu-id="62a5f-142">Partner Center będzie zbierać dane telemetryczne dla każdego z interfejsów API i dynamicznie dostosuje limity ograniczania przepustowości.</span><span class="sxs-lookup"><span data-stu-id="62a5f-142">Partner Center will be collecting the telemetry on each of the APIs and will dynamically adjust the throttling limits.</span></span> <span data-ttu-id="62a5f-143">W poniższej tabeli wymieniono interfejsy API, w których ograniczanie jest obecnie wymuszane.</span><span class="sxs-lookup"><span data-stu-id="62a5f-143">The following table lists the APIs where throttling is currently enforced.</span></span>  


|<span data-ttu-id="62a5f-144">**Operacja**</span><span class="sxs-lookup"><span data-stu-id="62a5f-144">**Operation**</span></span>| <span data-ttu-id="62a5f-145">**Dokumentacja Centrum partnerskiego**</span><span class="sxs-lookup"><span data-stu-id="62a5f-145">**Partner Center documentation**</span></span>|
|------------------------|----------------------------|
|<span data-ttu-id="62a5f-146">{baseURL}/v1/customers/{customer_id}/orders</span><span class="sxs-lookup"><span data-stu-id="62a5f-146">{baseURL}/v1/customers/{customer_id}/orders</span></span>|[<span data-ttu-id="62a5f-147">tworzenie zamówienia</span><span class="sxs-lookup"><span data-stu-id="62a5f-147">create an order</span></span>](create-an-order.md)|
|<span data-ttu-id="62a5f-148">{baseURL}/v1/customers/{identyfikator-dzierżawy-klienta}/subscriptions/{id-for-subscription}/upgrades</span><span class="sxs-lookup"><span data-stu-id="62a5f-148">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades</span></span>|[<span data-ttu-id="62a5f-149">przejście subskrypcji</span><span class="sxs-lookup"><span data-stu-id="62a5f-149">transition a subscription</span></span>](transition-a-subscription.md)|
|<span data-ttu-id="62a5f-150">{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}</span><span class="sxs-lookup"><span data-stu-id="62a5f-150">{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}</span></span>|[<span data-ttu-id="62a5f-151">zakup dodatku do subskrypcji</span><span class="sxs-lookup"><span data-stu-id="62a5f-151">purchase an addon to a subscription</span></span>](purchase-an-add-on-to-a-subscription.md)|
|<span data-ttu-id="62a5f-152">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span><span class="sxs-lookup"><span data-stu-id="62a5f-152">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span></span>|[<span data-ttu-id="62a5f-153">tworzenie koszyka</span><span class="sxs-lookup"><span data-stu-id="62a5f-153">create a cart</span></span>](create-a-cart.md)|
|<span data-ttu-id="62a5f-154">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout</span><span class="sxs-lookup"><span data-stu-id="62a5f-154">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout</span></span>|[<span data-ttu-id="62a5f-155">finalizacji zakupu koszyka</span><span class="sxs-lookup"><span data-stu-id="62a5f-155">checkout a cart</span></span>](checkout-a-cart.md)|
|<span data-ttu-id="62a5f-156">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span><span class="sxs-lookup"><span data-stu-id="62a5f-156">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span></span>|[<span data-ttu-id="62a5f-157">aktualizowanie koszyka</span><span class="sxs-lookup"><span data-stu-id="62a5f-157">update a cart</span></span>](update-a-cart.md)|
|<span data-ttu-id="62a5f-158">{baseURL}/v1/customers/{identyfikator-klienta}/subscriptions/{subscription-id}/registrations</span><span class="sxs-lookup"><span data-stu-id="62a5f-158">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations</span></span>|[<span data-ttu-id="62a5f-159">rejestrowanie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="62a5f-159">register a subscription</span></span>](register-a-subscription.md)|
|<span data-ttu-id="62a5f-160">{baseURL}/v1/productupgrades</span><span class="sxs-lookup"><span data-stu-id="62a5f-160">{baseURL}/v1/productupgrades</span></span>|[<span data-ttu-id="62a5f-161">tworzenie jednostki uaktualnienia produktu</span><span class="sxs-lookup"><span data-stu-id="62a5f-161">create product upgrade entity</span></span>](create-product-upgrade-entity.md)|
|<span data-ttu-id="62a5f-162">{baseURL}/v1/customers/{identyfikator-klienta}/subscriptions/{subscription-id}/conversions</span><span class="sxs-lookup"><span data-stu-id="62a5f-162">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span></span> |[<span data-ttu-id="62a5f-163">konwertowanie subskrypcji wersji próbnej na płatną</span><span class="sxs-lookup"><span data-stu-id="62a5f-163">convert a trial subscription to paid</span></span>](convert-a-trial-subscription-to-paid.md)|
|<span data-ttu-id="62a5f-164">{baseURL}/v1/customers/{customer-tenant-id}</span><span class="sxs-lookup"><span data-stu-id="62a5f-164">{baseURL}/v1/customers/{customer-tenant-id}</span></span>|[<span data-ttu-id="62a5f-165">uzyskiwanie klienta według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="62a5f-165">get a customer by ID</span></span>](get-a-customer-by-id.md)|
|<span data-ttu-id="62a5f-166">{baseURL}/v1/productUpgrades/eligibility</span><span class="sxs-lookup"><span data-stu-id="62a5f-166">{baseURL}/v1/productUpgrades/eligibility</span></span>|[<span data-ttu-id="62a5f-167">uzyskiwanie uprawnień do uaktualnienia produktu</span><span class="sxs-lookup"><span data-stu-id="62a5f-167">get eligibility for product upgrade</span></span>](get-eligibility-for-product-upgrade.md)|
|<span data-ttu-id="62a5f-168">{baseURL}/v1/customers/{identyfikator-dzierżawy-klienta}/subscriptions/{id-for-subscription}</span><span class="sxs-lookup"><span data-stu-id="62a5f-168">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}</span></span> |[<span data-ttu-id="62a5f-169">zarządzanie subskrypcją</span><span class="sxs-lookup"><span data-stu-id="62a5f-169">manage subscription</span></span>](manage-orders.md#manage-a-subscription)|
|<span data-ttu-id="62a5f-170">{baseURL}/v1/customers/{customer_id}/subscriptions</span><span class="sxs-lookup"><span data-stu-id="62a5f-170">{baseURL}/v1/customers/{customer_id}/subscriptions</span></span> |[<span data-ttu-id="62a5f-171">get-all-of-a-customer-s-subscriptions</span><span class="sxs-lookup"><span data-stu-id="62a5f-171">get-all-of-a-customer-s-subscriptions</span></span>](get-all-of-a-customer-s-subscriptions.md)|
|<span data-ttu-id="62a5f-172">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span><span class="sxs-lookup"><span data-stu-id="62a5f-172">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span></span>|[<span data-ttu-id="62a5f-173">Pobieranie subskrypcji według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="62a5f-173">Get a subscription by ID</span></span>](get-a-subscription-by-id.md)|
|<span data-ttu-id="62a5f-174">{baseURL}/v1/customers/{customer_id}/orders</span><span class="sxs-lookup"><span data-stu-id="62a5f-174">{baseURL}/v1/customers/{customer_id}/orders</span></span>|[<span data-ttu-id="62a5f-175">Pobierz wszystkie zamówienia klientów</span><span class="sxs-lookup"><span data-stu-id="62a5f-175">Get all customer orders</span></span>](get-all-of-a-customer-s-orders.md)|
|<span data-ttu-id="62a5f-176">{baseURL}/v1/customers/{customer_id}/orders/{order_id}</span><span class="sxs-lookup"><span data-stu-id="62a5f-176">{baseURL}/v1/customers/{customer_id}/orders/{order_id}</span></span>|[<span data-ttu-id="62a5f-177">Pobieranie zamówienia według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="62a5f-177">Get an order by ID</span></span>](get-an-order-by-id.md)|
|<span data-ttu-id="62a5f-178">{baseURL}/v1/customers/{customer_id}/orders/{order_id}/provisioningstatus</span><span class="sxs-lookup"><span data-stu-id="62a5f-178">{baseURL}/v1/customers/{customer_id}/orders/{order_id}/provisioningstatus</span></span>|[<span data-ttu-id="62a5f-179">Pobieranie stanu aprowizacji subskrypcji</span><span class="sxs-lookup"><span data-stu-id="62a5f-179">Get subscription provisioning status</span></span>](get-subscription-provisioning-status.md)|
|<span data-ttu-id="62a5f-180">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span><span class="sxs-lookup"><span data-stu-id="62a5f-180">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span></span>|[<span data-ttu-id="62a5f-181">Zarządzanie zamówieniami i zarządzanie subskrypcją</span><span class="sxs-lookup"><span data-stu-id="62a5f-181">Manage orders and manage a subscription</span></span>](manage-orders.md#manage-a-subscription)|
|<span data-ttu-id="62a5f-182">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/addons</span><span class="sxs-lookup"><span data-stu-id="62a5f-182">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/addons</span></span>|[<span data-ttu-id="62a5f-183">Pobieranie listy dodatków dla subskrypcji</span><span class="sxs-lookup"><span data-stu-id="62a5f-183">Get a list of add-ons for a subscription</span></span>](get-a-list-of-add-ons-for-a-subscription.md)|
|<span data-ttu-id="62a5f-184">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/azureEntitlements</span><span class="sxs-lookup"><span data-stu-id="62a5f-184">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/azureEntitlements</span></span>|[<span data-ttu-id="62a5f-185">Uzyskiwanie listy uprawnień platformy Azure dla subskrypcji</span><span class="sxs-lookup"><span data-stu-id="62a5f-185">Get a list of Azure entitlements for a subscription</span></span>](get-a-list-of-azure-entitlements-for-subscription.md)|
|<span data-ttu-id="62a5f-186">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/registrationstatus</span><span class="sxs-lookup"><span data-stu-id="62a5f-186">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/registrationstatus</span></span>|[<span data-ttu-id="62a5f-187">Pobieranie stanu rejestracji subskrypcji</span><span class="sxs-lookup"><span data-stu-id="62a5f-187">Get subscription registration status</span></span>](get-subscription-registration-status.md)|
|<span data-ttu-id="62a5f-188">{baseURL}/v1/customers/{identyfikator-dzierżawy-klienta}/transfers</span><span class="sxs-lookup"><span data-stu-id="62a5f-188">{baseURL}/v1/customers/{customer-tenant-id}/transfers</span></span>|[<span data-ttu-id="62a5f-189">Pobierz wszystkie przelewy klienta</span><span class="sxs-lookup"><span data-stu-id="62a5f-189">Get all of a customer's transfers</span></span>](get-all-of-a-customer-s-transfers.md)|
|<span data-ttu-id="62a5f-190">{baseURL}/v1/productUpgrades/{upgrade-id}/status</span><span class="sxs-lookup"><span data-stu-id="62a5f-190">{baseURL}/v1/productUpgrades/{upgrade-id}/status</span></span>|[<span data-ttu-id="62a5f-191">Pobieranie stanu uaktualniania produktu</span><span class="sxs-lookup"><span data-stu-id="62a5f-191">Get product upgrade status</span></span>](get-product-upgrade-status.md)|
|<span data-ttu-id="62a5f-192">{baseURL}/v1/customers/{identyfikator-klienta}/subscriptions/{subscription-id}/conversions</span><span class="sxs-lookup"><span data-stu-id="62a5f-192">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span></span>|[<span data-ttu-id="62a5f-193">Pobieranie listy ofert konwersji wersji próbnej</span><span class="sxs-lookup"><span data-stu-id="62a5f-193">Get a list of trial conversion offers</span></span>](get-a-list-of-trial-conversion-offers.md)|


### <a name="error-code-response"></a><span data-ttu-id="62a5f-194">Odpowiedź z kodem błędu:</span><span class="sxs-lookup"><span data-stu-id="62a5f-194">Error code response:</span></span>
```http
HTTP/1.1 429 Too Many Requests 

Content-Length: 84 

Content-Type: application/json 

Retry-After: 57 

Date: Tue, 21 Jul 2020 04:10:58 GMT 

{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 57 seconds." } 
```

## <a name="example-of-activity-log"></a><span data-ttu-id="62a5f-195">Przykład dziennika aktywności</span><span class="sxs-lookup"><span data-stu-id="62a5f-195">Example of activity log</span></span>

<span data-ttu-id="62a5f-196">Aby uzyskać najlepsze rozwiązanie dotyczące analizowania dziennych zmian, zalecamy wykonywanie zapytań o rekord inspekcji dla określonego dnia.</span><span class="sxs-lookup"><span data-stu-id="62a5f-196">For best practice in analyzing daily changes, we recommend that you query audit record for a specific day.</span></span> 

<span data-ttu-id="62a5f-197">W odpowiedzi otrzymasz wynik ze zmianami określonego typu operacji.</span><span class="sxs-lookup"><span data-stu-id="62a5f-197">In the response, you will get a result with changes to specific operation type.</span></span><span data-ttu-id="62a5f-198">Możesz filtrować na podstawie operacji, która Cię zależy.</span><span class="sxs-lookup"><span data-stu-id="62a5f-198">  You can filter based on the operation you care about.</span></span> <span data-ttu-id="62a5f-199">Jeśli na przykład interesuje Cię nowo utworzony klient, możesz przyjrzeć się typowi operationType = "add_customer".</span><span class="sxs-lookup"><span data-stu-id="62a5f-199"> For example, if you are interested in a newly created customer, you can look at operationType = “add_customer”.</span></span>  

<span data-ttu-id="62a5f-200">Listę typów operacji/zasobów można znaleźć w poniższych dokumentacjach interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="62a5f-200">List of operationtype/resources can be found in below API docs.</span></span>  

- [<span data-ttu-id="62a5f-201">Inspekcja zasobów</span><span class="sxs-lookup"><span data-stu-id="62a5f-201">Auditing resources</span></span>](auditing-resources.md)  

- [<span data-ttu-id="62a5f-202">Uzyskiwanie rekordu działania Partner Center przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="62a5f-202">Get a record of a Partner Center activity by user</span></span>](get-a-record-of-partner-center-activity-by-user.md)  



### <a name="response-example"></a><span data-ttu-id="62a5f-203">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="62a5f-203">Response example</span></span>

<span data-ttu-id="62a5f-204">**Żądanie**:</span><span class="sxs-lookup"><span data-stu-id="62a5f-204">**Request**:</span></span>  
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

<span data-ttu-id="62a5f-205">**Odpowiedź:**</span><span class="sxs-lookup"><span data-stu-id="62a5f-205">**Response**:</span></span>    
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
 

