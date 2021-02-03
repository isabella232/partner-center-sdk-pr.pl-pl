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
# <a name="partner-center-webhooks"></a>Elementy webhook Centrum partnerskiego

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Interfejsy API elementu webhook Centrum partnerskiego umożliwiają partnerom rejestrację zdarzeń zmiany zasobów. Te zdarzenia są dostarczane w formie wpisów HTTP do zarejestrowanego adresu URL partnera. Aby otrzymać zdarzenie z Centrum partnerskiego, partnerzy będą hostować wywołanie zwrotne, gdzie centrum partnerskie może OPUBLIKOWAĆ zdarzenie zmiany zasobu. Zdarzenie zostanie podpisane cyfrowo, aby partner mógł zweryfikować, że został wysłany z Centrum partnerskiego.

Partnerzy mogą wybierać z zdarzeń elementu webhook, takich jak poniższe przykłady, które są obsługiwane przez centrum partnerskie.

- **Zdarzenie testowe ("utworzone testowo")**

    To zdarzenie umożliwia samodzielne dołączanie i testowanie rejestracji przez zażądanie zdarzenia testowego, a następnie śledzenie jego postępu. W trakcie próby dostarczenia zdarzenia można zobaczyć komunikaty o błędach odbierane przez firmę Microsoft. To ograniczenie dotyczy tylko zdarzeń "test-created". Przeczyszczane są dane starsze niż siedem dni.

- **Zdarzenie zaktualizowane subskrypcji ("Zaktualizowano subskrypcję")**

    To zdarzenie jest zgłaszane w przypadku zmiany subskrypcji. Te zdarzenia zostaną wygenerowane w przypadku zmiany wewnętrznej poza wprowadzeniem zmian za pomocą interfejsu API Centrum partnerskiego.

    >[!NOTE]
    >Istnieje opóźnienie do 48 godzin między zmianą subskrypcji i wyzwoleniem zdarzenia zaktualizowanej subskrypcji.

- **Zdarzenie przekroczenia progu ("usagerecords-thresholdExceeded")**

    To zdarzenie jest zgłaszane, gdy wielkość Microsoft Azure użycia dla każdego klienta przekroczy budżet wydatków użytkowania (ich próg). Aby uzyskać więcej informacji, zobacz [Ustawianie budżetu wydatków platformy Azure dla klientów/partnerów-Center/Set-a-Azure-wydatków-budżet-dla klientów).

- **Zdarzenie utworzone referencji ("utworzono odwołanie")**

    To zdarzenie jest zgłaszane po utworzeniu odwołania.

- **Zdarzenie zaktualizowane odwołania ("odwołanie — zaktualizowane")**

    To zdarzenie jest zgłaszane, gdy odwołanie zostanie zaktualizowane.

- **Wydarzenie gotowe do fakturowania ("faktura — gotowe")**

    To zdarzenie jest zgłaszane w przypadku gotowości nowej faktury.

Przyszłe zdarzenia elementu webhook zostaną dodane do zasobów, które zmieniają się w systemie, w którym partner nie ma kontroli, i zostaną wykonane kolejne aktualizacje w celu uzyskania tych zdarzeń w czasie rzeczywistym, jak to możliwe. Opinie partnerów, na których zdarzenia dodają wartość do swojej firmy, będą przydatne podczas określania, jakie nowe zdarzenia dodać.

Aby uzyskać pełną listę zdarzeń elementu webhook obsługiwanych przez Centrum partnerskiego, zobacz [zdarzenia elementu webhook Centrum partnerskiego](partner-center-webhook-events.md).

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

## <a name="receiving-events-from-partner-center"></a>Otrzymywanie zdarzeń z Centrum partnerskiego

Aby otrzymywać zdarzenia z Centrum partnerskiego, należy uwidocznić dostępny publicznie punkt końcowy. Ponieważ ten punkt końcowy jest narażony, należy sprawdzić, czy komunikacja pochodzi z Centrum partnerskiego. Wszystkie zdarzenia elementu webhook, które otrzymujesz, są podpisane cyfrowo przy użyciu certyfikatu, który jest łańcuchem do katalogu głównego firmy Microsoft. Zostanie także udostępnione łącze do certyfikatu użytego do podpisania zdarzenia. Umożliwi to odnowienie certyfikatu bez konieczności ponownego wdrażania lub zmiany konfiguracji usługi. Centrum partnerskie wykona 10 prób dostarczenia zdarzenia. Jeśli zdarzenie nadal nie zostanie dostarczone po 10 próbach, zostanie przeniesiona do kolejki offline i nie będą podejmowane dalsze próby.

Poniższy przykład pokazuje zdarzenie ogłoszone w centrum partnerskim.

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
>Nagłówek autoryzacji zawiera schemat "Signature". To jest zakodowana w formacie base64 sygnatura zawartości.

## <a name="how-to-authenticate-the-callback"></a>Jak uwierzytelnić wywołanie zwrotne

Aby uwierzytelnić zdarzenie wywołania zwrotnego otrzymane z Centrum partnerskiego, wykonaj następujące czynności:

1. Sprawdź, czy wymagane nagłówki są obecne (autoryzacja, x-MS-Certificate-URL, x-MS-sygnatura-algorytm).

2. Pobierz certyfikat używany do podpisywania zawartości (x-MS-Certificate-URL).

3. Sprawdź łańcuch certyfikatów.

4. Sprawdź "organizacja" certyfikatu.

5. Przeczytaj zawartość z kodowaniem UTF8 w buforze.

6. Utwórz dostawcę usług kryptograficznych RSA.

7. Sprawdź, czy dane pasują do tego, co było podpisane przy użyciu określonego algorytmu wyznaczania wartości skrótu (na przykład SHA256).

8. Jeśli weryfikacja zakończy się pomyślnie, przetwórz komunikat.

> [!NOTE]
> Domyślnie token podpisu zostanie wysłany w nagłówku autoryzacji. Jeśli ustawisz **SignatureTokenToMsSignatureHeader** na wartość true w rejestracji, token podpisu zostanie wysłany w nagłówku x-MS-Signature.

## <a name="event-model"></a>Model zdarzenia

W poniższej tabeli opisano właściwości zdarzenia Centrum partnerskiego.

### <a name="properties"></a>Właściwości

| Nazwa                      | Opis                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| **EventName**             | Nazwa zdarzenia. W formularzu {Resource} — {Action}. Na przykład "utworzono test".  |
| **ResourceUri**           | Identyfikator URI zasobu, który został zmieniony.                                                 |
| **Source**          | Nazwa zasobu, który został zmieniony.                                                |
| **AuditUrl**              | Opcjonalny. Identyfikator URI rekordu inspekcji.                                                |
| **ResourceChangeUtcDate** | Data i godzina w formacie UTC, gdy nastąpiła zmiana zasobu.                  |

### <a name="sample"></a>Przykład

Poniższy przykład pokazuje strukturę zdarzenia Centrum partnerskiego.

```http
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

## <a name="webhook-apis"></a>Interfejsy API elementu webhook

### <a name="authentication"></a>Authentication

Wszystkie wywołania interfejsów API elementu webhook są uwierzytelniane przy użyciu tokenu okaziciela w nagłówku autoryzacji. Uzyskaj token dostępu, aby uzyskać dostęp `https://api.partnercenter.microsoft.com` . Token ten jest tym samym tokenem, który jest używany do uzyskiwania dostępu do pozostałych interfejsów API Centrum partnerskiego.

### <a name="get-a-list-of-events"></a>Pobierz listę zdarzeń

Zwraca listę zdarzeń, które są obecnie obsługiwane przez interfejsy API elementu webhook.

### <a name="resource-url"></a>Adres URL zasobu

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/events`

### <a name="request-example"></a>Przykład żądania

```http
GET /webhooks/v1/registration/events
content-type: application/json
authorization: Bearer eyJ0e.......
accept: */*
host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a>Przykład odpowiedzi

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

### <a name="register-to-receive-events"></a>Zarejestruj się, aby otrzymywać zdarzenia

Rejestruje dzierżawcę do odbierania określonych zdarzeń.

#### <a name="resource-url"></a>Adres URL zasobu

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a>Przykład żądania

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

### <a name="response-example"></a>Przykład odpowiedzi

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

### <a name="view-a-registration"></a>Wyświetlanie rejestracji

Zwraca rejestrację zdarzenia elementów webhook dla dzierżawy.

#### <a name="resource-url"></a>Adres URL zasobu

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a>Przykład żądania

```http
GET /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a>Przykład odpowiedzi

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

### <a name="update-an-event-registration"></a>Aktualizowanie rejestracji zdarzeń

Aktualizuje istniejącą rejestrację zdarzenia.

#### <a name="resource-url"></a>Adres URL zasobu

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a>Przykład żądania

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

### <a name="response-example"></a>Przykład odpowiedzi

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

### <a name="send-a-test-event-to-validate-your-registration"></a>Wyślij zdarzenie testowe, aby zweryfikować rejestrację

Generuje zdarzenie testowe w celu zweryfikowania rejestracji elementów webhook. Ten test ma na celu sprawdzenie, czy można odbierać zdarzenia z Centrum partnerskiego. Dane dla tych zdarzeń zostaną usunięte siedem dni po utworzeniu zdarzenia początkowego. Przed wysłaniem zdarzenia weryfikacji należy zarejestrować dla zdarzenia "test-created" przy użyciu interfejsu API rejestracji.

>[!NOTE]
>W przypadku ogłaszania zdarzenia weryfikacji występuje limit dławienia wynoszący 2 żądania na minutę.

#### <a name="resource-url"></a>Adres URL zasobu

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents`

### <a name="request-example"></a>Przykład żądania

```http
POST /webhooks/v1/registration/validationEvents
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length:
```

### <a name="response-example"></a>Przykład odpowiedzi

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

### <a name="verify-that-the-event-was-delivered"></a>Sprawdź, czy zdarzenie zostało dostarczone

Zwraca bieżący stan zdarzenia walidacji. Ta weryfikacja może pomóc w rozwiązywaniu problemów z dostarczaniem zdarzeń. Odpowiedź zawiera wynik dla każdej próby dostarczenia zdarzenia.

#### <a name="resource-url"></a>Adres URL zasobu

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{correlationId}`

### <a name="request-example"></a>Przykład żądania

```http
GET /webhooks/v1/registration/validationEvents/04af2aea-d413-42db-824e-f328001484d1
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a>Przykład odpowiedzi

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

## <a name="example-for-signature-validation"></a>Przykład weryfikacji podpisu

### <a name="sample-callback-controller-signature-aspnet"></a>Przykładowy podpis kontrolera wywołania zwrotnego (ASP.NET)

``` csharp
[AuthorizeSignature]
[Route("webhooks/callback")]
public IHttpActionResult Post(PartnerResourceChangeCallBack callback)
```

### <a name="signature-validation"></a>Walidacja podpisu

Poniższy przykład pokazuje, jak dodać atrybut autoryzacji do kontrolera, który otrzymuje wywołania zwrotne z zdarzeń elementu webhook.

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
