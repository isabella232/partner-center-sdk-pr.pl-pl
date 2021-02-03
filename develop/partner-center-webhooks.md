---
title: Elementy webhook Centrum partnerskiego
description: Elementy webhook umożliwiają partnerom rejestrację zdarzeń zmiany zasobów.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 8225623ade7e922ac23ebf0ed9215686b0601244
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768025"
---
# <a name="partner-center-webhooks"></a><span data-ttu-id="c6d5a-103">Elementy webhook Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="c6d5a-103">Partner Center webhooks</span></span>

<span data-ttu-id="c6d5a-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="c6d5a-104">**Applies To**</span></span>

- <span data-ttu-id="c6d5a-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="c6d5a-105">Partner Center</span></span>
- <span data-ttu-id="c6d5a-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="c6d5a-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="c6d5a-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="c6d5a-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="c6d5a-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="c6d5a-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c6d5a-109">Interfejsy API elementu webhook Centrum partnerskiego umożliwiają partnerom rejestrację zdarzeń zmiany zasobów.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-109">The Partner Center Webhook APIs allow partners to register for resource change events.</span></span> <span data-ttu-id="c6d5a-110">Te zdarzenia są dostarczane w formie wpisów HTTP do zarejestrowanego adresu URL partnera.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-110">These events are delivered in the form of HTTP POSTs to the partner's registered URL.</span></span> <span data-ttu-id="c6d5a-111">Aby otrzymać zdarzenie z Centrum partnerskiego, partnerzy będą hostować wywołanie zwrotne, gdzie centrum partnerskie może OPUBLIKOWAĆ zdarzenie zmiany zasobu.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-111">To receive an event from Partner Center, partners will host a callback where Partner Center can POST the resource change event.</span></span> <span data-ttu-id="c6d5a-112">Zdarzenie zostanie podpisane cyfrowo, aby partner mógł zweryfikować, że został wysłany z Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-112">The event will be digitally signed so that the partner can verify that it was sent from Partner Center.</span></span>

<span data-ttu-id="c6d5a-113">Partnerzy mogą wybierać z zdarzeń elementu webhook, takich jak poniższe przykłady, które są obsługiwane przez centrum partnerskie.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-113">Partners can select from Webhook events, like the following examples, that are supported by Partner Center.</span></span>

- <span data-ttu-id="c6d5a-114">**Zdarzenie testowe ("utworzone testowo")**</span><span class="sxs-lookup"><span data-stu-id="c6d5a-114">**Test Event ("test-created")**</span></span>

    <span data-ttu-id="c6d5a-115">To zdarzenie umożliwia samodzielne dołączanie i testowanie rejestracji przez zażądanie zdarzenia testowego, a następnie śledzenie jego postępu.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-115">This event allows you to self-onboard and test your registration by requesting a test event and then tracking its progress.</span></span> <span data-ttu-id="c6d5a-116">W trakcie próby dostarczenia zdarzenia można zobaczyć komunikaty o błędach odbierane przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-116">You can see the failure messages that are being received from Microsoft while trying to deliver the event.</span></span> <span data-ttu-id="c6d5a-117">To ograniczenie dotyczy tylko zdarzeń "test-created".</span><span class="sxs-lookup"><span data-stu-id="c6d5a-117">This restriction only applies to "test-created" events.</span></span> <span data-ttu-id="c6d5a-118">Przeczyszczane są dane starsze niż siedem dni.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-118">Data older than seven days will be purged.</span></span>

- <span data-ttu-id="c6d5a-119">**Zdarzenie zaktualizowane subskrypcji ("Zaktualizowano subskrypcję")**</span><span class="sxs-lookup"><span data-stu-id="c6d5a-119">**Subscription Updated Event ("subscription-updated")**</span></span>

    <span data-ttu-id="c6d5a-120">To zdarzenie jest zgłaszane w przypadku zmiany subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-120">This event is raised when the subscription changes.</span></span> <span data-ttu-id="c6d5a-121">Te zdarzenia zostaną wygenerowane w przypadku zmiany wewnętrznej poza wprowadzeniem zmian za pomocą interfejsu API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-121">These events will be generated when there is an internal change in addition to when changes are made through the Partner Center API.</span></span>

    >[!NOTE]
    ><span data-ttu-id="c6d5a-122">Istnieje opóźnienie do 48 godzin między zmianą subskrypcji i wyzwoleniem zdarzenia zaktualizowanej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-122">There is a delay of up to 48 hours between the time a subscription changes and when the Subscription Updated event is triggered.</span></span>

- <span data-ttu-id="c6d5a-123">**Zdarzenie przekroczenia progu ("usagerecords-thresholdExceeded")**</span><span class="sxs-lookup"><span data-stu-id="c6d5a-123">**Threshold Exceeded Event ("usagerecords-thresholdExceeded")**</span></span>

    <span data-ttu-id="c6d5a-124">To zdarzenie jest zgłaszane, gdy wielkość Microsoft Azure użycia dla każdego klienta przekroczy budżet wydatków użytkowania (ich próg).</span><span class="sxs-lookup"><span data-stu-id="c6d5a-124">This event is raised when the amount of Microsoft Azure usage for any customer exceeds their usage spending budget (their threshold).</span></span> <span data-ttu-id="c6d5a-125">Aby uzyskać więcej informacji, zobacz [Ustawianie budżetu wydatków platformy Azure dla klientów/partnerów-Center/Set-a-Azure-wydatków-budżet-dla klientów).</span><span class="sxs-lookup"><span data-stu-id="c6d5a-125">For more information, see  [Set an Azure spending budget for your customers/partner-center/set-an-azure-spending-budget-for-your-customers).</span></span>

- <span data-ttu-id="c6d5a-126">**Zdarzenie utworzone referencji ("utworzono odwołanie")**</span><span class="sxs-lookup"><span data-stu-id="c6d5a-126">**Referral Created Event ("referral-created")**</span></span>

    <span data-ttu-id="c6d5a-127">To zdarzenie jest zgłaszane po utworzeniu odwołania.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-127">This event is raised when the referral is created.</span></span>

- <span data-ttu-id="c6d5a-128">**Zdarzenie zaktualizowane odwołania ("odwołanie — zaktualizowane")**</span><span class="sxs-lookup"><span data-stu-id="c6d5a-128">**Referral Updated Event ("referral-updated")**</span></span>

    <span data-ttu-id="c6d5a-129">To zdarzenie jest zgłaszane, gdy odwołanie zostanie zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-129">This event is raised when the referral is updated.</span></span>

- <span data-ttu-id="c6d5a-130">**Wydarzenie gotowe do fakturowania ("faktura — gotowe")**</span><span class="sxs-lookup"><span data-stu-id="c6d5a-130">**Invoice Ready Event ("invoice-ready")**</span></span>

    <span data-ttu-id="c6d5a-131">To zdarzenie jest zgłaszane w przypadku gotowości nowej faktury.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-131">This event is raised when the new invoice is ready.</span></span>

<span data-ttu-id="c6d5a-132">Przyszłe zdarzenia elementu webhook zostaną dodane do zasobów, które zmieniają się w systemie, w którym partner nie ma kontroli, i zostaną wykonane kolejne aktualizacje w celu uzyskania tych zdarzeń w czasie rzeczywistym, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-132">Future Webhook events will be added for resources that change in the system that the partner isn't in control of, and further updates will be made to get those events as close to "real time" as possible.</span></span> <span data-ttu-id="c6d5a-133">Opinie partnerów, na których zdarzenia dodają wartość do swojej firmy, będą przydatne podczas określania, jakie nowe zdarzenia dodać.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-133">Feedback from Partners on which events add value to their business will be useful in determining what new events to add.</span></span>

<span data-ttu-id="c6d5a-134">Aby uzyskać pełną listę zdarzeń elementu webhook obsługiwanych przez Centrum partnerskiego, zobacz [zdarzenia elementu webhook Centrum partnerskiego](partner-center-webhook-events.md).</span><span class="sxs-lookup"><span data-stu-id="c6d5a-134">For a complete list of Webhook events supported by Partner Center, see [Partner Center webhook events](partner-center-webhook-events.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6d5a-135">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c6d5a-135">Prerequisites</span></span>

- <span data-ttu-id="c6d5a-136">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c6d5a-136">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c6d5a-137">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-137">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="receiving-events-from-partner-center"></a><span data-ttu-id="c6d5a-138">Otrzymywanie zdarzeń z Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="c6d5a-138">Receiving events from Partner Center</span></span>

<span data-ttu-id="c6d5a-139">Aby otrzymywać zdarzenia z Centrum partnerskiego, należy uwidocznić dostępny publicznie punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-139">To receive events from Partner Center, you must expose a publicly accessible endpoint.</span></span> <span data-ttu-id="c6d5a-140">Ponieważ ten punkt końcowy jest narażony, należy sprawdzić, czy komunikacja pochodzi z Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-140">Because this endpoint is exposed, you must validate that the communication is from Partner Center.</span></span> <span data-ttu-id="c6d5a-141">Wszystkie zdarzenia elementu webhook, które otrzymujesz, są podpisane cyfrowo przy użyciu certyfikatu, który jest łańcuchem do katalogu głównego firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-141">All Webhook events that you receive are digitally signed with a certificate that chains to the Microsoft Root.</span></span> <span data-ttu-id="c6d5a-142">Zostanie także udostępnione łącze do certyfikatu użytego do podpisania zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-142">A link to the certificate used to sign the event will also be provided.</span></span> <span data-ttu-id="c6d5a-143">Umożliwi to odnowienie certyfikatu bez konieczności ponownego wdrażania lub zmiany konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-143">This will allow the certificate to be renewed without you having to redeploy or reconfigure your service.</span></span> <span data-ttu-id="c6d5a-144">Centrum partnerskie wykona 10 prób dostarczenia zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-144">Partner Center will make 10 attempts to deliver the event.</span></span> <span data-ttu-id="c6d5a-145">Jeśli zdarzenie nadal nie zostanie dostarczone po 10 próbach, zostanie przeniesiona do kolejki offline i nie będą podejmowane dalsze próby.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-145">If the event is still not delivered after 10 attempts, it will be moved into an offline queue and no further attempts will be made at delivery.</span></span>

<span data-ttu-id="c6d5a-146">Poniższy przykład pokazuje zdarzenie ogłoszone w centrum partnerskim.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-146">The following sample shows an event posted from Partner Center.</span></span>

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
><span data-ttu-id="c6d5a-147">Nagłówek autoryzacji zawiera schemat "Signature".</span><span class="sxs-lookup"><span data-stu-id="c6d5a-147">The Authorization header has a scheme of "Signature".</span></span> <span data-ttu-id="c6d5a-148">To jest zakodowana w formacie base64 sygnatura zawartości.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-148">This is a base64 encoded signature of the content.</span></span>

## <a name="how-to-authenticate-the-callback"></a><span data-ttu-id="c6d5a-149">Jak uwierzytelnić wywołanie zwrotne</span><span class="sxs-lookup"><span data-stu-id="c6d5a-149">How to authenticate the callback</span></span>

<span data-ttu-id="c6d5a-150">Aby uwierzytelnić zdarzenie wywołania zwrotnego otrzymane z Centrum partnerskiego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c6d5a-150">To authenticate the callback event received from Partner Center, follow these steps:</span></span>

1. <span data-ttu-id="c6d5a-151">Sprawdź, czy wymagane nagłówki są obecne (autoryzacja, x-MS-Certificate-URL, x-MS-sygnatura-algorytm).</span><span class="sxs-lookup"><span data-stu-id="c6d5a-151">Verify the required headers are present (Authorization, x-ms-certificate-url, x-ms-signature-algorithm).</span></span>

2. <span data-ttu-id="c6d5a-152">Pobierz certyfikat używany do podpisywania zawartości (x-MS-Certificate-URL).</span><span class="sxs-lookup"><span data-stu-id="c6d5a-152">Download the certificate used to sign the content (x-ms-certificate-url).</span></span>

3. <span data-ttu-id="c6d5a-153">Sprawdź łańcuch certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-153">Verify the Certificate Chain.</span></span>

4. <span data-ttu-id="c6d5a-154">Sprawdź "organizacja" certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-154">Verify the "Organization" of the certificate.</span></span>

5. <span data-ttu-id="c6d5a-155">Przeczytaj zawartość z kodowaniem UTF8 w buforze.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-155">Read the content with UTF8 encoding into a buffer.</span></span>

6. <span data-ttu-id="c6d5a-156">Utwórz dostawcę usług kryptograficznych RSA.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-156">Create an RSA Crypto Provider.</span></span>

7. <span data-ttu-id="c6d5a-157">Sprawdź, czy dane pasują do tego, co było podpisane przy użyciu określonego algorytmu wyznaczania wartości skrótu (na przykład SHA256).</span><span class="sxs-lookup"><span data-stu-id="c6d5a-157">Verify the data matches what was signed with the specified hash algorithm (for example SHA256).</span></span>

8. <span data-ttu-id="c6d5a-158">Jeśli weryfikacja zakończy się pomyślnie, przetwórz komunikat.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-158">If the verification succeeds, process the message.</span></span>

> [!NOTE]
> <span data-ttu-id="c6d5a-159">Domyślnie token podpisu zostanie wysłany w nagłówku autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-159">By default, the signature token will be sent in an Authorization header.</span></span> <span data-ttu-id="c6d5a-160">Jeśli ustawisz **SignatureTokenToMsSignatureHeader** na wartość true w rejestracji, token podpisu zostanie wysłany w nagłówku x-MS-Signature.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-160">If you set **SignatureTokenToMsSignatureHeader** to true in your registration, the signature token will be sent in the x-ms-signature header instead.</span></span>

## <a name="event-model"></a><span data-ttu-id="c6d5a-161">Model zdarzenia</span><span class="sxs-lookup"><span data-stu-id="c6d5a-161">Event model</span></span>

<span data-ttu-id="c6d5a-162">W poniższej tabeli opisano właściwości zdarzenia Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-162">The following table describes the properties of a Partner Center event.</span></span>

### <a name="properties"></a><span data-ttu-id="c6d5a-163">Właściwości</span><span class="sxs-lookup"><span data-stu-id="c6d5a-163">Properties</span></span>

| <span data-ttu-id="c6d5a-164">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c6d5a-164">Name</span></span>                      | <span data-ttu-id="c6d5a-165">Opis</span><span class="sxs-lookup"><span data-stu-id="c6d5a-165">Description</span></span>                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| <span data-ttu-id="c6d5a-166">**EventName**</span><span class="sxs-lookup"><span data-stu-id="c6d5a-166">**EventName**</span></span>             | <span data-ttu-id="c6d5a-167">Nazwa zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-167">The name of the event.</span></span> <span data-ttu-id="c6d5a-168">W formularzu {Resource} — {Action}.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-168">In the form {resource}-{action}.</span></span> <span data-ttu-id="c6d5a-169">Na przykład "utworzono test".</span><span class="sxs-lookup"><span data-stu-id="c6d5a-169">For example, "test-created".</span></span>  |
| <span data-ttu-id="c6d5a-170">**ResourceUri**</span><span class="sxs-lookup"><span data-stu-id="c6d5a-170">**ResourceUri**</span></span>           | <span data-ttu-id="c6d5a-171">Identyfikator URI zasobu, który został zmieniony.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-171">The URI of the resource that changed.</span></span>                                                 |
| <span data-ttu-id="c6d5a-172">**Source**</span><span class="sxs-lookup"><span data-stu-id="c6d5a-172">**ResourceName**</span></span>          | <span data-ttu-id="c6d5a-173">Nazwa zasobu, który został zmieniony.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-173">The name of the resource that changed.</span></span>                                                |
| <span data-ttu-id="c6d5a-174">**AuditUrl**</span><span class="sxs-lookup"><span data-stu-id="c6d5a-174">**AuditUrl**</span></span>              | <span data-ttu-id="c6d5a-175">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-175">Optional.</span></span> <span data-ttu-id="c6d5a-176">Identyfikator URI rekordu inspekcji.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-176">The URI of the Audit record.</span></span>                                                |
| <span data-ttu-id="c6d5a-177">**ResourceChangeUtcDate**</span><span class="sxs-lookup"><span data-stu-id="c6d5a-177">**ResourceChangeUtcDate**</span></span> | <span data-ttu-id="c6d5a-178">Data i godzina w formacie UTC, gdy nastąpiła zmiana zasobu.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-178">The date and time, in UTC format, when the resource change occurred.</span></span>                  |

### <a name="sample"></a><span data-ttu-id="c6d5a-179">Przykład</span><span class="sxs-lookup"><span data-stu-id="c6d5a-179">Sample</span></span>

<span data-ttu-id="c6d5a-180">Poniższy przykład pokazuje strukturę zdarzenia Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-180">The following sample shows the structure of a Partner Center event.</span></span>

```http
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

## <a name="webhook-apis"></a><span data-ttu-id="c6d5a-181">Interfejsy API elementu webhook</span><span class="sxs-lookup"><span data-stu-id="c6d5a-181">Webhook APIs</span></span>

### <a name="authentication"></a><span data-ttu-id="c6d5a-182">Authentication</span><span class="sxs-lookup"><span data-stu-id="c6d5a-182">Authentication</span></span>

<span data-ttu-id="c6d5a-183">Wszystkie wywołania interfejsów API elementu webhook są uwierzytelniane przy użyciu tokenu okaziciela w nagłówku autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-183">All calls to the Webhook APIs are authenticated using the Bearer token in the Authorization Header.</span></span> <span data-ttu-id="c6d5a-184">Uzyskaj token dostępu, aby uzyskać dostęp `https://api.partnercenter.microsoft.com` .</span><span class="sxs-lookup"><span data-stu-id="c6d5a-184">Acquire an access token to access `https://api.partnercenter.microsoft.com`.</span></span> <span data-ttu-id="c6d5a-185">Token ten jest tym samym tokenem, który jest używany do uzyskiwania dostępu do pozostałych interfejsów API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-185">This token is the same token that is used to access the rest of the Partner Center APIs.</span></span>

### <a name="get-a-list-of-events"></a><span data-ttu-id="c6d5a-186">Pobierz listę zdarzeń</span><span class="sxs-lookup"><span data-stu-id="c6d5a-186">Get a list of events</span></span>

<span data-ttu-id="c6d5a-187">Zwraca listę zdarzeń, które są obecnie obsługiwane przez interfejsy API elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-187">Returns a list of the events that are currently supported by the Webhook APIs.</span></span>

### <a name="resource-url"></a><span data-ttu-id="c6d5a-188">Adres URL zasobu</span><span class="sxs-lookup"><span data-stu-id="c6d5a-188">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/events`

### <a name="request-example"></a><span data-ttu-id="c6d5a-189">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="c6d5a-189">Request example</span></span>

```http
GET /webhooks/v1/registration/events
content-type: application/json
authorization: Bearer eyJ0e.......
accept: */*
host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="c6d5a-190">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c6d5a-190">Response example</span></span>

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

### <a name="register-to-receive-events"></a><span data-ttu-id="c6d5a-191">Zarejestruj się, aby otrzymywać zdarzenia</span><span class="sxs-lookup"><span data-stu-id="c6d5a-191">Register to receive events</span></span>

<span data-ttu-id="c6d5a-192">Rejestruje dzierżawcę do odbierania określonych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-192">Registers a tenant to receive the specified events.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="c6d5a-193">Adres URL zasobu</span><span class="sxs-lookup"><span data-stu-id="c6d5a-193">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="c6d5a-194">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="c6d5a-194">Request example</span></span>

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

### <a name="response-example"></a><span data-ttu-id="c6d5a-195">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c6d5a-195">Response example</span></span>

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

### <a name="view-a-registration"></a><span data-ttu-id="c6d5a-196">Wyświetlanie rejestracji</span><span class="sxs-lookup"><span data-stu-id="c6d5a-196">View a registration</span></span>

<span data-ttu-id="c6d5a-197">Zwraca rejestrację zdarzenia elementów webhook dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-197">Returns the Webhooks event registration for a tenant.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="c6d5a-198">Adres URL zasobu</span><span class="sxs-lookup"><span data-stu-id="c6d5a-198">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="c6d5a-199">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="c6d5a-199">Request example</span></span>

```http
GET /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a><span data-ttu-id="c6d5a-200">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c6d5a-200">Response example</span></span>

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

### <a name="update-an-event-registration"></a><span data-ttu-id="c6d5a-201">Aktualizowanie rejestracji zdarzeń</span><span class="sxs-lookup"><span data-stu-id="c6d5a-201">Update an event registration</span></span>

<span data-ttu-id="c6d5a-202">Aktualizuje istniejącą rejestrację zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-202">Updates an existing event registration.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="c6d5a-203">Adres URL zasobu</span><span class="sxs-lookup"><span data-stu-id="c6d5a-203">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="c6d5a-204">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="c6d5a-204">Request example</span></span>

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

### <a name="response-example"></a><span data-ttu-id="c6d5a-205">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c6d5a-205">Response example</span></span>

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

### <a name="send-a-test-event-to-validate-your-registration"></a><span data-ttu-id="c6d5a-206">Wyślij zdarzenie testowe, aby zweryfikować rejestrację</span><span class="sxs-lookup"><span data-stu-id="c6d5a-206">Send a test event to validate your registration</span></span>

<span data-ttu-id="c6d5a-207">Generuje zdarzenie testowe w celu zweryfikowania rejestracji elementów webhook.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-207">Generates a test event to validate the Webhooks registration.</span></span> <span data-ttu-id="c6d5a-208">Ten test ma na celu sprawdzenie, czy można odbierać zdarzenia z Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-208">This test is intended to validate that you can receive events from Partner Center.</span></span> <span data-ttu-id="c6d5a-209">Dane dla tych zdarzeń zostaną usunięte siedem dni po utworzeniu zdarzenia początkowego.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-209">Data for these events will be deleted seven days after the initial event is created.</span></span> <span data-ttu-id="c6d5a-210">Przed wysłaniem zdarzenia weryfikacji należy zarejestrować dla zdarzenia "test-created" przy użyciu interfejsu API rejestracji.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-210">You must be registered for the "test-created" event, using the registration API, before sending a validation event.</span></span>

>[!NOTE]
><span data-ttu-id="c6d5a-211">W przypadku ogłaszania zdarzenia weryfikacji występuje limit dławienia wynoszący 2 żądania na minutę.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-211">There is a throttle limit of 2 requests per minute when posting a validation event.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="c6d5a-212">Adres URL zasobu</span><span class="sxs-lookup"><span data-stu-id="c6d5a-212">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents`

### <a name="request-example"></a><span data-ttu-id="c6d5a-213">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="c6d5a-213">Request example</span></span>

```http
POST /webhooks/v1/registration/validationEvents
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length:
```

### <a name="response-example"></a><span data-ttu-id="c6d5a-214">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c6d5a-214">Response example</span></span>

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

### <a name="verify-that-the-event-was-delivered"></a><span data-ttu-id="c6d5a-215">Sprawdź, czy zdarzenie zostało dostarczone</span><span class="sxs-lookup"><span data-stu-id="c6d5a-215">Verify that the event was delivered</span></span>

<span data-ttu-id="c6d5a-216">Zwraca bieżący stan zdarzenia walidacji.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-216">Returns the current state of the validation event.</span></span> <span data-ttu-id="c6d5a-217">Ta weryfikacja może pomóc w rozwiązywaniu problemów z dostarczaniem zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-217">This verification can be helpful for troubleshooting event delivery issues.</span></span> <span data-ttu-id="c6d5a-218">Odpowiedź zawiera wynik dla każdej próby dostarczenia zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-218">The Response contains a result for each attempt that is made to deliver the event.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="c6d5a-219">Adres URL zasobu</span><span class="sxs-lookup"><span data-stu-id="c6d5a-219">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{correlationId}`

### <a name="request-example"></a><span data-ttu-id="c6d5a-220">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="c6d5a-220">Request example</span></span>

```http
GET /webhooks/v1/registration/validationEvents/04af2aea-d413-42db-824e-f328001484d1
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a><span data-ttu-id="c6d5a-221">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c6d5a-221">Response example</span></span>

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

## <a name="example-for-signature-validation"></a><span data-ttu-id="c6d5a-222">Przykład weryfikacji podpisu</span><span class="sxs-lookup"><span data-stu-id="c6d5a-222">Example for Signature Validation</span></span>

### <a name="sample-callback-controller-signature-aspnet"></a><span data-ttu-id="c6d5a-223">Przykładowy podpis kontrolera wywołania zwrotnego (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="c6d5a-223">Sample Callback Controller signature (ASP.NET)</span></span>

``` csharp
[AuthorizeSignature]
[Route("webhooks/callback")]
public IHttpActionResult Post(PartnerResourceChangeCallBack callback)
```

### <a name="signature-validation"></a><span data-ttu-id="c6d5a-224">Walidacja podpisu</span><span class="sxs-lookup"><span data-stu-id="c6d5a-224">Signature Validation</span></span>

<span data-ttu-id="c6d5a-225">Poniższy przykład pokazuje, jak dodać atrybut autoryzacji do kontrolera, który otrzymuje wywołania zwrotne z zdarzeń elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="c6d5a-225">The following example shows how to add an Authorization Attribute to the controller that is receiving callbacks from Webhook events.</span></span>

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
