---
title: Weryfikowanie statusu podpisywania umowy partnerskiej firmy Microsoft pośredniego odsprzedawcy
description: Możesz użyć interfejsu API AgreementStatus, aby sprawdzić, czy pośredni odsprzedawca podpisał umowę partnera firmy Microsoft.
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fa9480424eccc933bc9c28c3879a195fbd5f2bb1
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711906"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a>Weryfikowanie statusu podpisywania umowy partnerskiej firmy Microsoft pośredniego odsprzedawcy

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie Microsoft Cloud for US Government

Możesz sprawdzić, czy pośredni odsprzedawca podpisał umowę partnera firmy Microsoft przy użyciu identyfikatora dzierżawy usługi Microsoft Partner Network (MPN) (PGA/PLA) lub dostawcy rozwiązań w chmurze (CSP). Możesz użyć jednego z tych identyfikatorów, aby sprawdzić stan podpisywania umowy Microsoft Partner Agreement przy użyciu interfejsu API **AgreementStatus** .

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- IDENTYFIKATOR MPN (PGA/PLA) lub identyfikator dzierżawy dostawcy usług kryptograficznych (Microsoft ID) pośredniego odsprzedawcy. *Musisz użyć jednego z tych dwóch identyfikatorów.*

## <a name="c"></a>C\#

Aby uzyskać status podpisu umowy partnerskiej firmy Microsoft dla pośredniego odsprzedawcy:

1. Użyj kolekcji **IAggregatePartner. zgodność** , aby wywołać Właściwość **AgreementSignatureStatus** .

2. Wywołaj metodę [**Get ()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) lub [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) .

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id (PGA/PLA)");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- Przykład: **[aplikacja testowa konsoli](console-test-app.md)**
- Projekt: **PartnerCenterSDK. FeaturesSamples**
- Klasa: **GetAgreementSignatureStatus. cs**

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania |
| ------ | ----------- |
| **Pobierz** | *[{baseURL}](partner-center-rest-urls.md)*/V1/Compliance/{ProgramName}/agreementstatus? mpnId = {mpnId} &tenantId = {tenantId} |

#### <a name="uri-parameters"></a>Parametry identyfikatora URI

Musisz podać jeden z następujących dwóch parametrów zapytania, aby zidentyfikować partnera. Jeśli nie podano jednego z tych dwóch parametrów zapytania, zostanie wyświetlony komunikat o błędzie **400 (Nieprawidłowe żądanie)** .

| Nazwa | Typ | Wymagane | Opis |
| ---- | ---- | -------- | ----------- |
| **MpnId** | int | Nie | Identyfikator Microsoft Partner Network (PGA/PLA) identyfikujący pośredniego odsprzedawcy. |
| **TenantId** | GUID | Nie | Identyfikator Microsoft, który identyfikuje konto CSP pośredniego odsprzedawcy. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz temat [Partner Center REST](headers.md).

### <a name="request-examples"></a>Przykłady żądań

#### <a name="request-using-mpn-id-pgapla"></a>Żądanie przy użyciu identyfikatora MPN (PGA/PLA)

Poniższe przykładowe żądanie Pobiera stan podpisywania umowy partnerskiej Microsoft Partner pośredni przy użyciu identyfikatora Microsoft Partner Network pośredniego odsprzedawcy.

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

Poniższe przykładowe żądanie Pobiera stan podpisywania umowy partnerskiej Microsoft Partner pośredni przy użyciu identyfikatora dzierżawy dostawcy CSP pośredniego Odsprzedawcy (identyfikator firmy Microsoft).

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

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [błąd REST centrum partnera](error-codes.md).

### <a name="response-example-success"></a>Przykład odpowiedzi (powodzenie)

Następująca przykładowa odpowiedź pomyślnie zwraca, czy pośredni odsprzedawca zapisał umowę partnera firmy Microsoft.

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

### <a name="response-examples-failure"></a>Przykłady odpowiedzi (niepowodzenie)

W przypadku, gdy nie można zwrócić stanu podpisywania pośredniej umowy partnerskiej partnera firmy Microsoft, użytkownik może otrzymywać odpowiedzi podobne do poniższych przykładów.

#### <a name="non-guid-formatted-csp-tenant-id"></a>Identyfikator dzierżawy CSP w formacie innym niż identyfikator GUID

Poniższy przykład odpowiedzi jest zwracany, gdy identyfikator dzierżawy CSP, który został przesłany do interfejsu API, nie jest identyfikatorem GUID.

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

Poniższy Przykładowa odpowiedź jest zwracana, gdy identyfikator MPN (PGA/PLA), który został przesłany do interfejsu API, nie jest wartością numeryczną.

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

#### <a name="no-mpn-id-or-csp-tenant-id"></a>Brak identyfikatora dzierżawy lub identyfikatora MPN

Poniższy przykład odpowiedzi jest zwracany, jeśli nie przeszedł identyfikator MPN (PGA/PLA) ani identyfikator dzierżawcy dostawcy CSP do interfejsu API. Należy przekazać jeden z dwóch typów identyfikatorów do interfejsu API.

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

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a>Przeszedł zarówno identyfikator MPN, jak i identyfikator dzierżawy dostawcy usług kryptograficznych

Poniższy Przykładowa odpowiedź jest zwracana w przypadku przekazywania identyfikatora MPN (PGA/PLA) i identyfikatora dzierżawy CSP do interfejsu API. Do interfejsu API należy przekazać *tylko jeden* z dwóch typów identyfikatorów.

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

#### <a name="csp-indirect-reseller-mpn-id-pgapla-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a>Pośredni odsprzedawca dostawcy usług kryptograficznych MPN identyfikator (PGA/PLA) jest nieprawidłowy lub nie został zmigrowany z Centrum członkostwa partnera do Centrum partnerskiego

Poniższy Przykładowa odpowiedź jest zwracana, gdy przekazana pośredni identyfikator MPN (PGA/PLA) jest nieprawidłowa lub nie została zmigrowana z Centrum członkostwa partnera do Centrum partnerskiego. [Więcej informacji](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

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

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a>Region pośredni dostawcy usług kryptograficznych i region niebezpośredniego odsprzedawcy dostawcy CSP nie są zgodne

Poniższy Przykładowa odpowiedź jest zwracana, gdy region pośredniego odsprzedawcy MPN (PGA/PLA) nie jest zgodny z regionem dostawcy pośredniego. [Dowiedz się więcej](/partner-center/mpa-indirect-provider-faq) o regionach dostawcy usług kryptograficznych.

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

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a>Pośredniego konta odsprzedawcy CSP istnieje w centrum partnerskim, ale nie podpisałem MPA

Poniższy przykład odpowiedzi jest zwracany, gdy konto odsprzedawcy pośredniego dostawcy CSP w centrum partnerskim nie podpisał MPA. [Więcej informacji](/partner-center/mpa-indirect-provider-faq)

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

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a>Brak pośredniego konta odsprzedawcy dostawcy CSP powiązanego z danym IDENTYFIKATORem MPN

Poniższy Przykładowa odpowiedź jest zwracana, gdy centrum partnerskie może rozpoznać identyfikator MPN (PGA/PLA) przekazany w żądaniu, ale nie istnieje Rejestracja dostawcy CSP skojarzona z danym IDENTYFIKATORem MPN (PGA/PLA). [Więcej informacji](/partner-center/mpa-indirect-provider-faq)

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

Poniższy Przykładowa odpowiedź jest zwracana, gdy centrum partnerskie nie znajdzie żadnego konta skojarzonego z IDENTYFIKATORem dzierżawy przesłanego w żądaniu.

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

#### <a name="no-mpa-found-with-the-given-tenant-id"></a>Nie znaleziono platformy MPA o podanym IDENTYFIKATORze dzierżawy

Poniższy Przykładowa odpowiedź jest zwracana, gdy centrum partnerskie nie może znaleźć żadnego z nich podpisania MPA z danym IDENTYFIKATORem dzierżawy. [Więcej informacji](/partner-center/mpa-indirect-provider-faq)

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