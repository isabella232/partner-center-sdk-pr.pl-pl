---
title: Elementy webhook Centrum partnerskiego
description: Webhook umożliwia partnerom rejestrowanie zdarzeń zmiany zasobów.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 74d5981436ba29ea4f6f93a5693ec6da82777eb4
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547754"
---
# <a name="partner-center-webhooks"></a><span data-ttu-id="68013-103">Elementy webhook Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="68013-103">Partner Center webhooks</span></span>

<span data-ttu-id="68013-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="68013-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="68013-105">Interfejsy API Partner Center Webhook umożliwiają partnerom rejestrowanie zdarzeń zmiany zasobów.</span><span class="sxs-lookup"><span data-stu-id="68013-105">The Partner Center Webhook APIs allow partners to register for resource change events.</span></span> <span data-ttu-id="68013-106">Te zdarzenia są dostarczane w postaci punktów POP protokołu HTTP do zarejestrowanego adresu URL partnera.</span><span class="sxs-lookup"><span data-stu-id="68013-106">These events are delivered in the form of HTTP POSTs to the partner's registered URL.</span></span> <span data-ttu-id="68013-107">Aby odebrać zdarzenie od Partner Center, partnerzy będą hostować wywołanie zwrotne, w Partner Center można WYSŁAĆ ZDARZENIE ZMIANY ZASOBU.</span><span class="sxs-lookup"><span data-stu-id="68013-107">To receive an event from Partner Center, partners will host a callback where Partner Center can POST the resource change event.</span></span> <span data-ttu-id="68013-108">Zdarzenie zostanie podpisane cyfrowo, aby partner może sprawdzić, czy zostało ono wysłane z Partner Center.</span><span class="sxs-lookup"><span data-stu-id="68013-108">The event will be digitally signed so that the partner can verify that it was sent from Partner Center.</span></span>

<span data-ttu-id="68013-109">Partnerzy mogą wybierać zdarzenia z elementy webhook, takie jak poniższe przykłady, które są obsługiwane przez Partner Center.</span><span class="sxs-lookup"><span data-stu-id="68013-109">Partners can select from Webhook events, like the following examples, that are supported by Partner Center.</span></span>

- <span data-ttu-id="68013-110">**Zdarzenie testowe ("utworzono test")**</span><span class="sxs-lookup"><span data-stu-id="68013-110">**Test Event ("test-created")**</span></span>

    <span data-ttu-id="68013-111">To zdarzenie umożliwia samodzielne dołączanie i testowanie rejestracji, żądając zdarzenia testowego, a następnie śledząc jego postęp.</span><span class="sxs-lookup"><span data-stu-id="68013-111">This event allows you to self-onboard and test your registration by requesting a test event and then tracking its progress.</span></span> <span data-ttu-id="68013-112">Podczas próby dostarczenia zdarzenia są wyświetlane komunikaty o błędach odbierane od firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="68013-112">You can see the failure messages that are being received from Microsoft while trying to deliver the event.</span></span> <span data-ttu-id="68013-113">To ograniczenie dotyczy tylko zdarzeń utworzonych przez test.</span><span class="sxs-lookup"><span data-stu-id="68013-113">This restriction only applies to "test-created" events.</span></span> <span data-ttu-id="68013-114">Dane starsze niż siedem dni zostaną przeczyszone.</span><span class="sxs-lookup"><span data-stu-id="68013-114">Data older than seven days will be purged.</span></span>

- <span data-ttu-id="68013-115">**Zdarzenie zaktualizowane subskrypcji ("subskrypcja-zaktualizowana")**</span><span class="sxs-lookup"><span data-stu-id="68013-115">**Subscription Updated Event ("subscription-updated")**</span></span>

    <span data-ttu-id="68013-116">To zdarzenie jest wywoływane po zmianie subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="68013-116">This event is raised when the subscription changes.</span></span> <span data-ttu-id="68013-117">Te zdarzenia zostaną wygenerowane w przypadku zmiany wewnętrznej oprócz zmiany wprowadzonej za pośrednictwem interfejsu API Partner Center API.</span><span class="sxs-lookup"><span data-stu-id="68013-117">These events will be generated when there is an internal change in addition to when changes are made through the Partner Center API.</span></span>

    >[!NOTE]
    ><span data-ttu-id="68013-118">Między zmianą subskrypcji a wyzwoleniem zdarzenia Aktualizacja subskrypcji istnieje opóźnienie do 48 godzin.</span><span class="sxs-lookup"><span data-stu-id="68013-118">There is a delay of up to 48 hours between the time a subscription changes and when the Subscription Updated event is triggered.</span></span>

- <span data-ttu-id="68013-119">**Zdarzenie przekroczenia progu ("usagerecords-thresholdExceeded")**</span><span class="sxs-lookup"><span data-stu-id="68013-119">**Threshold Exceeded Event ("usagerecords-thresholdExceeded")**</span></span>

    <span data-ttu-id="68013-120">To zdarzenie jest wywoływane, gdy Microsoft Azure użycia dla dowolnego klienta przekracza budżet wydatków na użycie (próg).</span><span class="sxs-lookup"><span data-stu-id="68013-120">This event is raised when the amount of Microsoft Azure usage for any customer exceeds their usage spending budget (their threshold).</span></span> <span data-ttu-id="68013-121">Aby uzyskać więcej informacji, zobacz [Ustawianie budżetu wydatków platformy Azure dla klientów/centrum partnerskiego/set-an-azure-spending-budget-for-your-customers).</span><span class="sxs-lookup"><span data-stu-id="68013-121">For more information, see  [Set an Azure spending budget for your customers/partner-center/set-an-azure-spending-budget-for-your-customers).</span></span>

- <span data-ttu-id="68013-122">**Zdarzenie utworzenia odwołania ("utworzono polecenie")**</span><span class="sxs-lookup"><span data-stu-id="68013-122">**Referral Created Event ("referral-created")**</span></span>

    <span data-ttu-id="68013-123">To zdarzenie jest wywoływane podczas tworzenia odwołania.</span><span class="sxs-lookup"><span data-stu-id="68013-123">This event is raised when the referral is created.</span></span>

- <span data-ttu-id="68013-124">**Zdarzenie aktualizacji poleceń ("polecenie zostało zaktualizowane")**</span><span class="sxs-lookup"><span data-stu-id="68013-124">**Referral Updated Event ("referral-updated")**</span></span>

    <span data-ttu-id="68013-125">To zdarzenie jest wywoływane po zaktualizowaniu polecenia.</span><span class="sxs-lookup"><span data-stu-id="68013-125">This event is raised when the referral is updated.</span></span>

- <span data-ttu-id="68013-126">**Zdarzenie gotowe do faktury ("gotowe do faktury")**</span><span class="sxs-lookup"><span data-stu-id="68013-126">**Invoice Ready Event ("invoice-ready")**</span></span>

    <span data-ttu-id="68013-127">To zdarzenie jest wywoływane, gdy nowa faktura jest gotowa.</span><span class="sxs-lookup"><span data-stu-id="68013-127">This event is raised when the new invoice is ready.</span></span>

<span data-ttu-id="68013-128">Przyszłe zdarzenia dotyczące webhook zostaną dodane dla zasobów, które zmieniają się w systemie, nad które partner nie ma kontroli, a następnie zostaną wprowadzone dalsze aktualizacje, aby te zdarzenia były możliwie jak najbardziej zbliżone do "czasu rzeczywistego".</span><span class="sxs-lookup"><span data-stu-id="68013-128">Future Webhook events will be added for resources that change in the system that the partner isn't in control of, and further updates will be made to get those events as close to "real time" as possible.</span></span> <span data-ttu-id="68013-129">Opinie od partnerów dotyczące zdarzeń, które mają wartość dodaną do ich działalności, będą przydatne podczas określania, jakie nowe zdarzenia dodać.</span><span class="sxs-lookup"><span data-stu-id="68013-129">Feedback from Partners on which events add value to their business will be useful in determining what new events to add.</span></span>

<span data-ttu-id="68013-130">Aby uzyskać pełną listę zdarzeń elementów webhook obsługiwanych przez Partner Center, zobacz [Partner Center zdarzenia elementów webhook](partner-center-webhook-events.md).</span><span class="sxs-lookup"><span data-stu-id="68013-130">For a complete list of Webhook events supported by Partner Center, see [Partner Center webhook events](partner-center-webhook-events.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68013-131">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="68013-131">Prerequisites</span></span>

- <span data-ttu-id="68013-132">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="68013-132">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="68013-133">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="68013-133">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="receiving-events-from-partner-center"></a><span data-ttu-id="68013-134">Odbieranie zdarzeń z Partner Center</span><span class="sxs-lookup"><span data-stu-id="68013-134">Receiving events from Partner Center</span></span>

<span data-ttu-id="68013-135">Aby odbierać zdarzenia z Partner Center, należy uwidocznić publicznie dostępny punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="68013-135">To receive events from Partner Center, you must expose a publicly accessible endpoint.</span></span> <span data-ttu-id="68013-136">Ponieważ ten punkt końcowy jest ujawniony, należy sprawdzić, czy komunikacja pochodzi z Partner Center.</span><span class="sxs-lookup"><span data-stu-id="68013-136">Because this endpoint is exposed, you must validate that the communication is from Partner Center.</span></span> <span data-ttu-id="68013-137">Wszystkie odbierane zdarzenia webhook są podpisane cyfrowo przy użyciu certyfikatu, który jest łańcuchem z katalogiem głównym firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="68013-137">All Webhook events that you receive are digitally signed with a certificate that chains to the Microsoft Root.</span></span> <span data-ttu-id="68013-138">Zostanie również podany link do certyfikatu użytego do podpisania zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="68013-138">A link to the certificate used to sign the event will also be provided.</span></span> <span data-ttu-id="68013-139">Pozwoli to odnowić certyfikat bez konieczności ponownego wdychowania lub ponownego konfigurowania usługi.</span><span class="sxs-lookup"><span data-stu-id="68013-139">This will allow the certificate to be renewed without you having to redeploy or reconfigure your service.</span></span> <span data-ttu-id="68013-140">Partner Center 10 prób dostarczenia zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="68013-140">Partner Center will make 10 attempts to deliver the event.</span></span> <span data-ttu-id="68013-141">Jeśli zdarzenie nadal nie zostanie dostarczone po 10 próbach, zostanie przeniesione do kolejki w trybie offline i żadne dalsze próby nie będą dokonywane podczas dostarczania.</span><span class="sxs-lookup"><span data-stu-id="68013-141">If the event is still not delivered after 10 attempts, it will be moved into an offline queue and no further attempts will be made at delivery.</span></span>

<span data-ttu-id="68013-142">W poniższym przykładzie pokazano zdarzenie opublikowane z Partner Center.</span><span class="sxs-lookup"><span data-stu-id="68013-142">The following sample shows an event posted from Partner Center.</span></span>

```http
POST /webhooks/callback
Content-Type: application/json
Authorization: Signature VOhcjRqA4f7u/4R29ohEzwRZibZdzfgG5/w4fHUnu8FHauBEVch8m2+5OgjLZRL33CIQpmqr2t0FsGF0UdmCR2OdY7rrAh/6QUW+u+jRUCV1s62M76jbVpTTGShmrANxnl8gz4LsbY260LAsDHufd6ab4oejerx1Ey9sFC+xwVTa+J4qGgeyIepeu4YCM0oB2RFS9rRB2F1s1OeAAPEhG7olp8B00Jss3PQrpLGOoAr5+fnQp8GOK8IdKF1/abUIyyvHxEjL76l7DVQN58pIJg4YC+pLs8pi6sTKvOdSVyCnjf+uYQWwmmWujSHfyU37j2Fzz16PJyWH41K8ZXJJkw==
X-MS-Certificate-Url: https://3psostorageacct.blob.core.windows.net/cert/pcnotifications-dispatch.microsoft.com.cer
X-MS-Signature-Algorithm: rsa-sha256
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 195

{
    "EventName": "test-created",
    "ResourceUri": "http://localhost:16722/v1/webhooks/registration/test",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

>[!NOTE]
><span data-ttu-id="68013-143">Nagłówek Autoryzacja ma schemat "Podpis".</span><span class="sxs-lookup"><span data-stu-id="68013-143">The Authorization header has a scheme of "Signature".</span></span> <span data-ttu-id="68013-144">Jest to podpis zawartości zakodowany w formacie base64.</span><span class="sxs-lookup"><span data-stu-id="68013-144">This is a base64 encoded signature of the content.</span></span>

## <a name="how-to-authenticate-the-callback"></a><span data-ttu-id="68013-145">Jak uwierzytelnić wywołanie zwrotne</span><span class="sxs-lookup"><span data-stu-id="68013-145">How to authenticate the callback</span></span>

<span data-ttu-id="68013-146">Aby uwierzytelnić zdarzenie wywołania zwrotnego odebrane z Partner Center, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="68013-146">To authenticate the callback event received from Partner Center, follow these steps:</span></span>

1. <span data-ttu-id="68013-147">Sprawdź, czy wymagane nagłówki są obecne (Authorization, x-ms-certificate-url, x-ms-signature-algorithm).</span><span class="sxs-lookup"><span data-stu-id="68013-147">Verify the required headers are present (Authorization, x-ms-certificate-url, x-ms-signature-algorithm).</span></span>

2. <span data-ttu-id="68013-148">Pobierz certyfikat używany do podpisywania zawartości (x-ms-certificate-url).</span><span class="sxs-lookup"><span data-stu-id="68013-148">Download the certificate used to sign the content (x-ms-certificate-url).</span></span>

3. <span data-ttu-id="68013-149">Sprawdź łańcuch certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="68013-149">Verify the Certificate Chain.</span></span>

4. <span data-ttu-id="68013-150">Sprawdź "Organizację" certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="68013-150">Verify the "Organization" of the certificate.</span></span>

5. <span data-ttu-id="68013-151">Odczytaj zawartość z kodowaniem UTF8 do buforu.</span><span class="sxs-lookup"><span data-stu-id="68013-151">Read the content with UTF8 encoding into a buffer.</span></span>

6. <span data-ttu-id="68013-152">Utwórz dostawcę usług kryptograficznych RSA.</span><span class="sxs-lookup"><span data-stu-id="68013-152">Create an RSA Crypto Provider.</span></span>

7. <span data-ttu-id="68013-153">Sprawdź, czy dane są takie, jakie zostały podpisane przy użyciu określonego algorytmu wyznaczania wartości skrótu (na przykład SHA256).</span><span class="sxs-lookup"><span data-stu-id="68013-153">Verify the data matches what was signed with the specified hash algorithm (for example SHA256).</span></span>

8. <span data-ttu-id="68013-154">Jeśli weryfikacja zakończy się pomyślnie, przetowalij komunikat.</span><span class="sxs-lookup"><span data-stu-id="68013-154">If the verification succeeds, process the message.</span></span>

> [!NOTE]
> <span data-ttu-id="68013-155">Domyślnie token podpisu będzie wysyłany w nagłówku autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="68013-155">By default, the signature token will be sent in an Authorization header.</span></span> <span data-ttu-id="68013-156">Jeśli ustawisz w rejestracji wartość true **signatureTokenToMsSignatureHeader,** token podpisu zostanie zamiast tego wysłany w nagłówku x-ms-signature.</span><span class="sxs-lookup"><span data-stu-id="68013-156">If you set **SignatureTokenToMsSignatureHeader** to true in your registration, the signature token will be sent in the x-ms-signature header instead.</span></span>

## <a name="event-model"></a><span data-ttu-id="68013-157">Model zdarzeń</span><span class="sxs-lookup"><span data-stu-id="68013-157">Event model</span></span>

<span data-ttu-id="68013-158">W poniższej tabeli opisano właściwości Partner Center zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="68013-158">The following table describes the properties of a Partner Center event.</span></span>

### <a name="properties"></a><span data-ttu-id="68013-159">Właściwości</span><span class="sxs-lookup"><span data-stu-id="68013-159">Properties</span></span>

| <span data-ttu-id="68013-160">Nazwa</span><span class="sxs-lookup"><span data-stu-id="68013-160">Name</span></span>                      | <span data-ttu-id="68013-161">Opis</span><span class="sxs-lookup"><span data-stu-id="68013-161">Description</span></span>                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| <span data-ttu-id="68013-162">**EventName**</span><span class="sxs-lookup"><span data-stu-id="68013-162">**EventName**</span></span>             | <span data-ttu-id="68013-163">Nazwa zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="68013-163">The name of the event.</span></span> <span data-ttu-id="68013-164">W postaci {resource}-{action}.</span><span class="sxs-lookup"><span data-stu-id="68013-164">In the form {resource}-{action}.</span></span> <span data-ttu-id="68013-165">Na przykład "test-created".</span><span class="sxs-lookup"><span data-stu-id="68013-165">For example, "test-created".</span></span>  |
| <span data-ttu-id="68013-166">**ResourceUri**</span><span class="sxs-lookup"><span data-stu-id="68013-166">**ResourceUri**</span></span>           | <span data-ttu-id="68013-167">URI zasobu, który uległ zmianie.</span><span class="sxs-lookup"><span data-stu-id="68013-167">The URI of the resource that changed.</span></span>                                                 |
| <span data-ttu-id="68013-168">**Resourcename**</span><span class="sxs-lookup"><span data-stu-id="68013-168">**ResourceName**</span></span>          | <span data-ttu-id="68013-169">Nazwa zasobu, który uległ zmianie.</span><span class="sxs-lookup"><span data-stu-id="68013-169">The name of the resource that changed.</span></span>                                                |
| <span data-ttu-id="68013-170">**AuditUrl**</span><span class="sxs-lookup"><span data-stu-id="68013-170">**AuditUrl**</span></span>              | <span data-ttu-id="68013-171">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="68013-171">Optional.</span></span> <span data-ttu-id="68013-172">URI rekordu inspekcji.</span><span class="sxs-lookup"><span data-stu-id="68013-172">The URI of the Audit record.</span></span>                                                |
| <span data-ttu-id="68013-173">**ResourceChangeUtcDate**</span><span class="sxs-lookup"><span data-stu-id="68013-173">**ResourceChangeUtcDate**</span></span> | <span data-ttu-id="68013-174">Data i godzina w formacie UTC, kiedy nastąpiła zmiana zasobu.</span><span class="sxs-lookup"><span data-stu-id="68013-174">The date and time, in UTC format, when the resource change occurred.</span></span>                  |

### <a name="sample"></a><span data-ttu-id="68013-175">Przykład</span><span class="sxs-lookup"><span data-stu-id="68013-175">Sample</span></span>

<span data-ttu-id="68013-176">Poniższy przykład przedstawia strukturę zdarzenia Partner Center zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="68013-176">The following sample shows the structure of a Partner Center event.</span></span>

```http
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

## <a name="webhook-apis"></a><span data-ttu-id="68013-177">Interfejsy API elementy webhook</span><span class="sxs-lookup"><span data-stu-id="68013-177">Webhook APIs</span></span>

### <a name="authentication"></a><span data-ttu-id="68013-178">Authentication</span><span class="sxs-lookup"><span data-stu-id="68013-178">Authentication</span></span>

<span data-ttu-id="68013-179">Wszystkie wywołania interfejsów API elementy webhook są uwierzytelniane przy użyciu tokenu bearer w nagłówku autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="68013-179">All calls to the Webhook APIs are authenticated using the Bearer token in the Authorization Header.</span></span> <span data-ttu-id="68013-180">Uzyskiwanie tokenu dostępu w celu uzyskania dostępu do usługi `https://api.partnercenter.microsoft.com` .</span><span class="sxs-lookup"><span data-stu-id="68013-180">Acquire an access token to access `https://api.partnercenter.microsoft.com`.</span></span> <span data-ttu-id="68013-181">Ten token jest tym samym tokenem, który jest używany do uzyskiwania dostępu do pozostałych Partner Center API.</span><span class="sxs-lookup"><span data-stu-id="68013-181">This token is the same token that is used to access the rest of the Partner Center APIs.</span></span>

### <a name="get-a-list-of-events"></a><span data-ttu-id="68013-182">Uzyskiwanie listy zdarzeń</span><span class="sxs-lookup"><span data-stu-id="68013-182">Get a list of events</span></span>

<span data-ttu-id="68013-183">Zwraca listę zdarzeń, które są obecnie obsługiwane przez interfejsy API elementów webhook.</span><span class="sxs-lookup"><span data-stu-id="68013-183">Returns a list of the events that are currently supported by the Webhook APIs.</span></span>

### <a name="resource-url"></a><span data-ttu-id="68013-184">Adres URL zasobu</span><span class="sxs-lookup"><span data-stu-id="68013-184">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/events`

### <a name="request-example"></a><span data-ttu-id="68013-185">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="68013-185">Request example</span></span>

```http
GET /webhooks/v1/registration/events
content-type: application/json
authorization: Bearer eyJ0e.......
accept: */*
host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="68013-186">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="68013-186">Response example</span></span>

```http
HTTP/1.1 200
Status: 200
Content-Length: 183
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: c0bcf3a3-46e9-48fd-8e05-f674b8fd5d66
MS-RequestId: 79419bbb-06ee-48da-8221-e09480537dfc
X-Locale: en-US

[ "subscription-updated", "test-created", "usagerecords-thresholdExceeded" ]
```

### <a name="register-to-receive-events"></a><span data-ttu-id="68013-187">Rejestrowanie w celu odbierania zdarzeń</span><span class="sxs-lookup"><span data-stu-id="68013-187">Register to receive events</span></span>

<span data-ttu-id="68013-188">Rejestruje dzierżawę w celu odbierania określonych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="68013-188">Registers a tenant to receive the specified events.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="68013-189">Adres URL zasobu</span><span class="sxs-lookup"><span data-stu-id="68013-189">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="68013-190">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="68013-190">Request example</span></span>

```http
POST /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer eyJ0e.....
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 219

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="response-example"></a><span data-ttu-id="68013-191">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="68013-191">Response example</span></span>

```http
HTTP/1.1 200
Status: 200
Content-Length: 346
Content-Type: application/json; charset=utf-8
content-encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 718f2336-8b56-4f42-93ac-54896047c59a
MS-RequestId: f04b1b5e-87b4-4d95-b087-d65fffec0bd2

{
    "SubscriberId": "e82cac64-dc67-4cd3-849b-78b6127dd57d",
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": [ "subscription-updated", "test-created" ]
}
```

### <a name="view-a-registration"></a><span data-ttu-id="68013-192">Wyświetlanie rejestracji</span><span class="sxs-lookup"><span data-stu-id="68013-192">View a registration</span></span>

<span data-ttu-id="68013-193">Zwraca rejestrację zdarzenia webhook dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="68013-193">Returns the Webhooks event registration for a tenant.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="68013-194">Adres URL zasobu</span><span class="sxs-lookup"><span data-stu-id="68013-194">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="68013-195">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="68013-195">Request example</span></span>

```http
GET /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a><span data-ttu-id="68013-196">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="68013-196">Response example</span></span>

```http
HTTP/1.1 200
Status: 200
Content-Length: 341
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: c3b88ab0-b7bc-48d6-8c55-4ae6200f490a
MS-RequestId: ca30367d-4b24-4516-af08-74bba6dc6657
X-Locale: en-US

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="update-an-event-registration"></a><span data-ttu-id="68013-197">Aktualizowanie rejestracji zdarzeń</span><span class="sxs-lookup"><span data-stu-id="68013-197">Update an event registration</span></span>

<span data-ttu-id="68013-198">Aktualizuje istniejącą rejestrację zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="68013-198">Updates an existing event registration.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="68013-199">Adres URL zasobu</span><span class="sxs-lookup"><span data-stu-id="68013-199">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="68013-200">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="68013-200">Request example</span></span>

```http
PUT /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOR...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 258

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="response-example"></a><span data-ttu-id="68013-201">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="68013-201">Response example</span></span>

```http
HTTP/1.1 200
Status: 200
Content-Length: 346
Content-Type: application/json; charset=utf-8
content-encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 718f2336-8b56-4f42-93ac-54896047c59a
MS-RequestId: f04b1b5e-87b4-4d95-b087-d65fffec0bd2

{
    "SubscriberId": "e82cac64-dc67-4cd3-849b-78b6127dd57d",
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": [ "subscription-updated", "test-created" ]
}
```

### <a name="send-a-test-event-to-validate-your-registration"></a><span data-ttu-id="68013-202">Wysyłanie zdarzenia testowego w celu zweryfikowania rejestracji</span><span class="sxs-lookup"><span data-stu-id="68013-202">Send a test event to validate your registration</span></span>

<span data-ttu-id="68013-203">Generuje zdarzenie testowe w celu zweryfikowania rejestracji webhook.</span><span class="sxs-lookup"><span data-stu-id="68013-203">Generates a test event to validate the Webhooks registration.</span></span> <span data-ttu-id="68013-204">Ten test ma na celu sprawdzenie, czy można odbierać zdarzenia z Partner Center.</span><span class="sxs-lookup"><span data-stu-id="68013-204">This test is intended to validate that you can receive events from Partner Center.</span></span> <span data-ttu-id="68013-205">Dane dla tych zdarzeń zostaną usunięte siedem dni po utworzeniu początkowego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="68013-205">Data for these events will be deleted seven days after the initial event is created.</span></span> <span data-ttu-id="68013-206">Przed wysłaniem zdarzenia weryfikacji musisz zarejestrować się na zdarzenie "test-created" przy użyciu interfejsu API rejestracji.</span><span class="sxs-lookup"><span data-stu-id="68013-206">You must be registered for the "test-created" event, using the registration API, before sending a validation event.</span></span>

>[!NOTE]
><span data-ttu-id="68013-207">W przypadku publikowania zdarzenia weryfikacji 2 żądania na minutę są ograniczane.</span><span class="sxs-lookup"><span data-stu-id="68013-207">There is a throttle limit of 2 requests per minute when posting a validation event.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="68013-208">Adres URL zasobu</span><span class="sxs-lookup"><span data-stu-id="68013-208">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents`

### <a name="request-example"></a><span data-ttu-id="68013-209">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="68013-209">Request example</span></span>

```http
POST /webhooks/v1/registration/validationEvents
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length:
```

### <a name="response-example"></a><span data-ttu-id="68013-210">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="68013-210">Response example</span></span>

```http
HTTP/1.1 200
Status: 200
Content-Length: 181
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 04af2aea-d413-42db-824e-f328001484d1
MS-RequestId: 2f498d5a-a6ab-468f-98d8-93c96da09051
X-Locale: en-US

{ "correlationId": "04af2aea-d413-42db-824e-f328001484d1" }
```

### <a name="verify-that-the-event-was-delivered"></a><span data-ttu-id="68013-211">Sprawdzanie, czy zdarzenie zostało dostarczone</span><span class="sxs-lookup"><span data-stu-id="68013-211">Verify that the event was delivered</span></span>

<span data-ttu-id="68013-212">Zwraca bieżący stan zdarzenia weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="68013-212">Returns the current state of the validation event.</span></span> <span data-ttu-id="68013-213">Ta weryfikacja może być przydatna do rozwiązywania problemów z dostarczaniem zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="68013-213">This verification can be helpful for troubleshooting event delivery issues.</span></span> <span data-ttu-id="68013-214">Odpowiedź zawiera wynik dla każdej próby dostarczenia zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="68013-214">The Response contains a result for each attempt that is made to deliver the event.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="68013-215">Adres URL zasobu</span><span class="sxs-lookup"><span data-stu-id="68013-215">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{correlationId}`

### <a name="request-example"></a><span data-ttu-id="68013-216">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="68013-216">Request example</span></span>

```http
GET /webhooks/v1/registration/validationEvents/04af2aea-d413-42db-824e-f328001484d1
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a><span data-ttu-id="68013-217">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="68013-217">Response example</span></span>

```http
HTTP/1.1 200
Status: 200
Content-Length: 469
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 497e0a23-9498-4d6c-bd6a-bc4d6d0054e7
MS-RequestId: 0843bdb2-113a-4926-a51c-284aa01d722e
X-Locale: en-US

{
    "correlationId": "04af2aea-d413-42db-824e-f328001484d1",
    "partnerId": "00234d9d-8c2d-4ff5-8c18-39f8afc6f7f3",
    "status": "completed",
    "callbackUrl": "{{YourCallbackUrl}}",
    "results": [{
        "responseCode": "OK",
        "responseMessage": "",
        "systemError": false,
        "dateTimeUtc": "2017-12-08T21:39:48.2386997"
    }]
}
```

## <a name="example-for-signature-validation"></a><span data-ttu-id="68013-218">Przykład weryfikacji podpisu</span><span class="sxs-lookup"><span data-stu-id="68013-218">Example for Signature Validation</span></span>

### <a name="sample-callback-controller-signature-aspnet"></a><span data-ttu-id="68013-219">Przykładowy podpis kontrolera wywołania zwrotnego (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="68013-219">Sample Callback Controller signature (ASP.NET)</span></span>

``` csharp
[AuthorizeSignature]
[Route("webhooks/callback")]
public IHttpActionResult Post(PartnerResourceChangeCallBack callback)
```

### <a name="signature-validation"></a><span data-ttu-id="68013-220">Walidacja podpisu</span><span class="sxs-lookup"><span data-stu-id="68013-220">Signature Validation</span></span>

<span data-ttu-id="68013-221">W poniższym przykładzie pokazano, jak dodać atrybut autoryzacji do kontrolera, który odbiera wywołania zwrotne ze zdarzeń element webhook.</span><span class="sxs-lookup"><span data-stu-id="68013-221">The following example shows how to add an Authorization Attribute to the controller that is receiving callbacks from Webhook events.</span></span>

``` csharp
namespace Webhooks.Security
{
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Security.Cryptography;
    using System.Security.Cryptography.X509Certificates;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using System.Web.Http;
    using System.Web.Http.Controllers;
    using Microsoft.Partner.Logging;

    /// <summary>
    /// Signature based Authorization
    /// </summary>
    public class AuthorizeSignatureAttribute : AuthorizeAttribute
    {
        private const string MsSignatureHeader = "x-ms-signature";
        private const string CertificateUrlHeader = "x-ms-certificate-url";
        private const string SignatureAlgorithmHeader = "x-ms-signature-algorithm";
        private const string MicrosoftCorporationIssuer = "O=Microsoft Corporation";
        private const string SignatureScheme = "Signature";

        /// <inheritdoc/>
        public override async Task OnAuthorizationAsync(HttpActionContext actionContext, CancellationToken cancellationToken)
        {
            ValidateAuthorizationHeaders(actionContext.Request);

            await VerifySignature(actionContext.Request);
        }

        private static async Task<string> GetContentAsync(HttpRequestMessage request)
        {
            // By default the stream can only be read once and we need to read it here so that we can hash the body to validate the signature from microsoft.
            // Load into a buffer, so that the stream can be accessed here and in the api when it binds the content to the expected model type.
            await request.Content.LoadIntoBufferAsync();

            var s = await request.Content.ReadAsStreamAsync();
            var reader = new StreamReader(s);
            var body = await reader.ReadToEndAsync();

            // set the stream position back to the beginning
            if (s.CanSeek)
            {
                s.Seek(0, SeekOrigin.Begin);
            }

            return body;
        }

        private static void ValidateAuthorizationHeaders(HttpRequestMessage request)
        {
            var authHeader = request.Headers.Authorization;
            if (string.IsNullOrWhiteSpace(authHeader?.Parameter) && string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, MsSignatureHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Authorization header missing."));
            }

            var signatureHeaderValue = GetHeaderValue(request.Headers, MsSignatureHeader);
            if (authHeader != null
                && !string.Equals(authHeader.Scheme, SignatureScheme, StringComparison.OrdinalIgnoreCase)
                && !string.IsNullOrWhiteSpace(signatureHeaderValue)
                && !signatureHeaderValue.StartsWith(SignatureScheme, StringComparison.OrdinalIgnoreCase))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, $"Authorization scheme needs to be '{SignatureScheme}'."));
            }

            if (string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, CertificateUrlHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.BadRequest, $"Request header {CertificateUrlHeader} missing."));
            }

            if (string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, SignatureAlgorithmHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.BadRequest, $"Request header {SignatureAlgorithmHeader} missing."));
            }
        }

        private static string GetHeaderValue(HttpHeaders headers, string key)
        {
            headers.TryGetValues(key, out var headerValues);

            return headerValues?.FirstOrDefault();
        }

        private static async Task VerifySignature(HttpRequestMessage request)
        {
            // Get signature value from either authorization header or x-ms-signature header.
            var base64Signature = request.Headers.Authorization?.Parameter ?? GetHeaderValue(request.Headers, MsSignatureHeader).Split(' ')[1];
            var signatureAlgorithm = GetHeaderValue(request.Headers, SignatureAlgorithmHeader);
            var certificateUrl = GetHeaderValue(request.Headers, CertificateUrlHeader);
            var certificate = await GetCertificate(certificateUrl);
            var content = await GetContentAsync(request);
            var alg = signatureAlgorithm.Split('-'); // for example RSA-SHA1
            var isValid = false;

            var logger = GetLoggerIfAvailable(request);

            // Validate the certificate
            VerifyCertificate(certificate, request, logger);

            if (alg.Length == 2 && alg[0].Equals("RSA", StringComparison.OrdinalIgnoreCase))
            {
                var signature = Convert.FromBase64String(base64Signature);
                var csp = (RSACryptoServiceProvider)certificate.PublicKey.Key;

                var encoding = new UTF8Encoding();
                var data = encoding.GetBytes(content);

                var hashAlgorithm = alg[1].ToUpper();

                isValid = csp.VerifyData(data, CryptoConfig.MapNameToOID(hashAlgorithm), signature);
            }

            if (!isValid)
            {
                // log that we were not able to validate the signature
                logger?.TrackTrace(
                    "Failed to validate signature for webhook callback",
                    new Dictionary<string, string> { { "base64Signature", base64Signature }, { "certificateUrl", certificateUrl }, { "signatureAlgorithm", signatureAlgorithm }, { "content", content } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Signature verification failed"));
            }
        }

        private static ILogger GetLoggerIfAvailable(HttpRequestMessage request)
        {
            return request.GetDependencyScope().GetService(typeof(ILogger)) as ILogger;
        }

        private static async Task<X509Certificate2> GetCertificate(string certificateUrl)
        {
            byte[] certBytes;
            using (var webClient = new WebClient())
            {
                certBytes = await webClient.DownloadDataTaskAsync(certificateUrl);
            }

            return new X509Certificate2(certBytes);
        }

        private static void VerifyCertificate(X509Certificate2 certificate, HttpRequestMessage request, ILogger logger)
        {
            if (!certificate.Verify())
            {
                logger?.TrackTrace("Failed to verify certificate for webhook callback.", new Dictionary<string, string> { { "Subject", certificate.Subject }, { "Issuer", certificate.Issuer } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Certificate verification failed."));
            }

            if (!certificate.Issuer.Contains(MicrosoftCorporationIssuer))
            {
                logger?.TrackTrace($"Certificate not issued by {MicrosoftCorporationIssuer}.", new Dictionary<string, string> { { "Issuer", certificate.Issuer } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, $"Certificate not issued by {MicrosoftCorporationIssuer}."));
            }
        }
    }
}
```
