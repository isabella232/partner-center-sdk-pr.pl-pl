---
title: Weryfikowanie stanu podpisywania Microsoft Partner Agreement odsprzedawcy pośredniego
description: Interfejs API AgreementStatus umożliwia sprawdzenie, czy odsprzedawca pośredni podpisał umowę Microsoft Partner Agreement.
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 517c99356a4b623b5b46bc3d33f2355cd569f97326e7d9596cff551329d10da7
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989852"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a>Weryfikowanie stanu podpisywania Microsoft Partner Agreement odsprzedawcy pośredniego

**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud for US Government

Możesz sprawdzić, czy odsprzedawca pośredni podpisał umowę Microsoft Partner Agreement przy użyciu identyfikatora Microsoft Partner Network (MPN) (PGA/PLA) lub identyfikatora dzierżawy Dostawca rozwiązań w chmurze (CSP) (identyfikator firmy Microsoft). Możesz użyć jednego z tych identyfikatorów, aby sprawdzić stan Microsoft Partner Agreement przy użyciu interfejsu API **AgreementStatus.**

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.

- Identyfikator MPN (PGA/PLA) lub identyfikator dzierżawy CSP (identyfikator Microsoft) odsprzedawcy pośredniego. *Należy użyć jednego z tych dwóch identyfikatorów.*

## <a name="c"></a>C\#

Aby uzyskać Microsoft Partner Agreement stan podpisu odsprzedawcy pośredniego:

1. Użyj **kolekcji IAggregatePartner.Compliance,** aby wywołać właściwość **AgreementSignatureStatus.**

2. Wywołaj [**metodę Get()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) [**lub GetAsync().**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync)

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id (PGA/PLA)");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- Przykład: **[aplikacja testowa konsoli](console-test-app.md)**
- Project: **PartnerCenterSDK.FeaturesSamples**
- Klasa: **GetAgreementSignatureStatus.cs**

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania |
| ------ | ----------- |
| **Pobierz** | *[{baseURL}](partner-center-rest-urls.md)*/v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId} |

#### <a name="uri-parameters"></a>Parametry URI

Aby zidentyfikować partnera, należy podać jeden z następujących dwóch parametrów zapytania. Jeśli nie poimkniesz jednego z tych dwóch parametrów zapytania, zostanie wyświetlony błąd **400 (Złe żądanie).**

| Nazwa | Typ | Wymagane | Opis |
| ---- | ---- | -------- | ----------- |
| **MpnId** | int | Nie | Identyfikator Microsoft Partner Network (PGA/PLA), który identyfikuje odsprzedawcę pośredniego. |
| **TenantId** | GUID | Nie | Identyfikator firmy Microsoft, który identyfikuje konto CSP odsprzedawcy pośredniego. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [Partner Center REST](headers.md).

### <a name="request-examples"></a>Przykłady żądań

#### <a name="request-using-mpn-id-pgapla"></a>Żądanie przy użyciu identyfikatora MPN (PGA/PLA)

Następujące przykładowe żądanie pobiera stan Microsoft Partner Agreement podpisywania odsprzedawcy pośredniego przy użyciu identyfikatora Microsoft Partner Network odsprzedawcy pośredniego.

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a>Żądanie przy użyciu identyfikatora dzierżawy CSP

Następujące przykładowe żądanie pobiera stan Microsoft Partner Agreement podpisywania odsprzedawcy pośredniego przy użyciu identyfikatora dzierżawy CSP odsprzedawcy pośredniego (Microsoft ID).

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpowiedź REST

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz Partner Center REST error (Błąd [REST).](error-codes.md)

### <a name="response-example-success"></a>Przykład odpowiedzi (powodzenie)

Następująca przykładowa odpowiedź pomyślnie zwraca, czy odsprzedawca pośredni podpisał umowę Microsoft Partner Agreement.

```http
HTTP/1.1 200 OK
Content-Length: 29
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: jn3r+1wpE06nCt/0.0
MS-ServerId: 0000005B
Date: Tue, 15 Oct 2019 12:44:34 GMT
Connection: close
{
    "isAgreementSigned": true
}
```

### <a name="response-examples-failure"></a>Przykłady odpowiedzi (błąd)

Odpowiedzi mogą być podobne do poniższych przykładów, gdy nie można zwrócić stanu Microsoft Partner Agreement odsprzedawcy pośredniego.

#### <a name="non-guid-formatted-csp-tenant-id"></a>Identyfikator dzierżawy CSP sformatowany bez identyfikatora GUID

Następująca przykładowa odpowiedź jest zwracana, gdy identyfikator dzierżawy dostawcy usług kryptograficznych przekazany do interfejsu API nie jest identyfikatorem GUID.

```http
HTTP/1.1 400 Bad Request
Content-Length: 105
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: rbuZl5lbAkyq8WGK.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 08:55:23 GMT
Connection: close
{
    "code": 2000,
    "description": "Tenant Id must be a GUID.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

#### <a name="non-numeric-mpn-id"></a>Nieliczbowy identyfikator MPN

Następująca przykładowa odpowiedź jest zwracana, gdy identyfikator MPN (PGA/PLA) przekazany do interfejsu API jest nieliczbowy.

```http
HTTP/1.1 400 Bad Request
Content-Length: 103
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: cP5JiS4sv0GJxlJ9.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 08:58:45 GMT
Connection: close
{
    "code": 2000,
    "description": "MPN Id must be numeric.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

#### <a name="no-mpn-id-or-csp-tenant-id"></a>Brak identyfikatora MPN lub identyfikatora dzierżawy CSP

Następująca przykładowa odpowiedź jest zwracana, gdy do interfejsu API nie przekazano identyfikatora MPN (PGA/PLA) lub identyfikatora dzierżawy CSP. Do interfejsu API należy przekazać jeden z dwóch typów identyfikatorów.

```http
HTTP/1.1 400 Bad Request
Content-Length: 114
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: hEV736v4qk6joDMR.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 09:00:30 GMT
Connection: close
{
    "code": 2001,
    "description": "Both MPN Id and Tenant Id cannot be empty.",
    "data": [],
    "source": "ComplianceController"
}
```

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a>Przekazano zarówno identyfikator MPN, jak i identyfikator dzierżawy CSP

Następująca przykładowa odpowiedź jest zwracana, gdy do interfejsu API przekażemy zarówno identyfikator MPN ID (PGA/PLA), jak i identyfikator dzierżawy dostawcy CSP. Do *interfejsu* API należy przekazać tylko jeden z dwóch typów identyfikatorów.

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2000,
    "description": "Both MPN Id and Tenant Id should not be passed.",
    "data": [],
    "source": "ComplianceController"
}
```

#### <a name="csp-indirect-reseller-mpn-id-pgapla-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a>CSP Indirect Reseller IDENTYFIKATOR MPN (PGA/PLA) jest nieprawidłowy lub nie jest migrowany z Partner Membership Center do Partner Center

Następująca przykładowa odpowiedź jest zwracana, gdy przekazany identyfikator MPN odsprzedawcy pośredniego (PGA/PLA) jest nieprawidłowy lub nie jest migrowany z Partner Membership Center do Partner Center. [Więcej informacji](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2200,
    "description": "MPN Id 123456 is either invalid or not yet migrated to Partner Center. Please advise your reseller to migrate the reseller MPN ID to Partner Center to continue with this order.",
    "data": [
        "https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a>CSP Indirect Provider region i CSP Indirect Reseller są zgodne

Następująca przykładowa odpowiedź jest zwracana, gdy region odsprzedawcy pośredniego o identyfikatorze MPN (PGA/PLA) nie pasuje do regionu dostawcy pośredniego. [Dowiedz się więcej](/partner-center/mpa-indirect-provider-faq) o regionach CSP.

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2201,
    "description": "The CSP region of the MPN ID 1234567 doesn’t match the CSP region from where you are placing the order. Provide the MPN ID for the CSP region where you are placing the order.",
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq" 
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a>CSP Indirect Reseller istnieje w Partner Center, ale nie ma podpisanego umowy MPA

Następująca przykładowa odpowiedź jest zwracana, CSP Indirect Reseller konto w Partner Center nie ma podpisanego umowy MPA. [Więcej informacji](/partner-center/mpa-indirect-provider-faq)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2203,
    "description": "MPN Id 123456 has not signed Microsoft Partner Agreement (MPA) for the CSP region where the order is being placed. Please advise your reseller to sign MPA to continue with the order.",
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a>Żadne CSP Indirect Reseller nie jest skojarzone z danym identyfikatorem MPN

Następująca przykładowa odpowiedź jest zwracana, gdy program Partner Center może rozpoznać identyfikator MPN (PGA/PLA) przekazany w żądaniu, ale nie istnieje rejestracja CSP skojarzona z danym identyfikatorem MPN (PGA/PLA). [Więcej informacji](/partner-center/mpa-indirect-provider-faq)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2204,
    "description": "MPN Id 123456 is not associated with a CSP Indirect Reseller account in Partner Center. Please advise your reseller to enroll into the CSP program as an indirect reseller in Partner Center.",
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```

#### <a name="invalid-tenant-id"></a>Nieprawidłowy identyfikator dzierżawy

Następująca przykładowa odpowiedź jest zwracana, Partner Center nie znajdzie żadnego konta skojarzonego z identyfikatorem dzierżawy przekazanym w żądaniu.

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2205,
    "description": "Partner Center doesn't find any account associated to the Tenant ID 12345678-ACBD-1234-ABCD-123456789ABC",
    "data": [],
    "source": "PartnerFD"
}
```

#### <a name="no-mpa-found-with-the-given-tenant-id"></a>Nie znaleziono mpA o danym identyfikatorze dzierżawy

Następująca przykładowa odpowiedź jest zwracana, Partner Center nie może znaleźć żadnego podpisu MPA o danym identyfikatorze dzierżawy. [Więcej informacji](/partner-center/mpa-indirect-provider-faq)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2206,
    "description": "Parnter Center Account associated to Tenant Id 12345678-ACBD-1234-ABCD-123456789ABC hasn't signed the agreement",
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```