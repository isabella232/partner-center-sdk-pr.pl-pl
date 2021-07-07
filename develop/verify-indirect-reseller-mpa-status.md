---
title: Weryfikowanie stanu podpisywania Microsoft Partner Agreement odsprzedawcy pośredniego
description: Interfejs API AgreementStatus umożliwia sprawdzenie, czy odsprzedawca pośredni podpisał umowę Microsoft Partner Agreement.
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f83acc61624a72354c390905b1250bc021dd39aa
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529838"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a><span data-ttu-id="c7079-103">Weryfikowanie stanu podpisywania Microsoft Partner Agreement odsprzedawcy pośredniego</span><span class="sxs-lookup"><span data-stu-id="c7079-103">Verify an indirect reseller's Microsoft Partner Agreement signing status</span></span>

<span data-ttu-id="c7079-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="c7079-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c7079-105">Możesz sprawdzić, czy odsprzedawca pośredni podpisał umowę Microsoft Partner Agreement przy użyciu identyfikatora Microsoft Partner Network (MPN) (PGA/PLA) lub identyfikatora dzierżawy Dostawca rozwiązań w chmurze (CSP) (identyfikator firmy Microsoft).</span><span class="sxs-lookup"><span data-stu-id="c7079-105">You can verify whether an indirect reseller has signed the Microsoft Partner Agreement using their Microsoft Partner Network (MPN) ID (PGA/PLA) or Cloud Solution Provider (CSP) tenant ID (Microsoft ID).</span></span> <span data-ttu-id="c7079-106">Możesz użyć jednego z tych identyfikatorów, aby sprawdzić stan Microsoft Partner Agreement przy użyciu interfejsu API **AgreementStatus.**</span><span class="sxs-lookup"><span data-stu-id="c7079-106">You can use one of these identifiers to check the Microsoft Partner Agreement signing status using the **AgreementStatus** API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7079-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c7079-107">Prerequisites</span></span>

- <span data-ttu-id="c7079-108">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="c7079-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c7079-109">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c7079-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="c7079-110">Identyfikator MPN (PGA/PLA) lub identyfikator dzierżawy CSP (identyfikator Microsoft) odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="c7079-110">The MPN ID (PGA/PLA) or the CSP tenant ID (Microsoft ID) of the indirect reseller.</span></span> <span data-ttu-id="c7079-111">*Należy użyć jednego z tych dwóch identyfikatorów.*</span><span class="sxs-lookup"><span data-stu-id="c7079-111">*You must use one of these two identifiers.*</span></span>

## <a name="c"></a><span data-ttu-id="c7079-112">C\#</span><span class="sxs-lookup"><span data-stu-id="c7079-112">C\#</span></span>

<span data-ttu-id="c7079-113">Aby uzyskać Microsoft Partner Agreement stan podpisu odsprzedawcy pośredniego:</span><span class="sxs-lookup"><span data-stu-id="c7079-113">To get the Microsoft Partner Agreement signature status of an indirect reseller:</span></span>

1. <span data-ttu-id="c7079-114">Użyj **kolekcji IAggregatePartner.Compliance,** aby wywołać właściwość **AgreementSignatureStatus.**</span><span class="sxs-lookup"><span data-stu-id="c7079-114">Use your **IAggregatePartner.Compliance** collection to call the **AgreementSignatureStatus** property.</span></span>

2. <span data-ttu-id="c7079-115">Wywołaj [**metodę Get()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) [**lub GetAsync().**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync)</span><span class="sxs-lookup"><span data-stu-id="c7079-115">Call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id (PGA/PLA)");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- <span data-ttu-id="c7079-116">Przykład: **[aplikacja testowa konsoli](console-test-app.md)**</span><span class="sxs-lookup"><span data-stu-id="c7079-116">Sample: **[Console test app](console-test-app.md)**</span></span>
- <span data-ttu-id="c7079-117">Project: **PartnerCenterSDK.FeaturesSamples**</span><span class="sxs-lookup"><span data-stu-id="c7079-117">Project: **PartnerCenterSDK.FeaturesSamples**</span></span>
- <span data-ttu-id="c7079-118">Klasa: **GetAgreementSignatureStatus.cs**</span><span class="sxs-lookup"><span data-stu-id="c7079-118">Class: **GetAgreementSignatureStatus.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="c7079-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="c7079-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c7079-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="c7079-120">Request syntax</span></span>

| <span data-ttu-id="c7079-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="c7079-121">Method</span></span> | <span data-ttu-id="c7079-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="c7079-122">Request URI</span></span> |
| ------ | ----------- |
| <span data-ttu-id="c7079-123">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="c7079-123">**GET**</span></span> | <span data-ttu-id="c7079-124">*[{baseURL}](partner-center-rest-urls.md)*/v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId}</span><span class="sxs-lookup"><span data-stu-id="c7079-124">*[{baseURL}](partner-center-rest-urls.md)*/v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="c7079-125">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="c7079-125">URI parameters</span></span>

<span data-ttu-id="c7079-126">Aby zidentyfikować partnera, należy podać jeden z następujących dwóch parametrów zapytania.</span><span class="sxs-lookup"><span data-stu-id="c7079-126">You must provide one of the following two query parameters to identify the partner.</span></span> <span data-ttu-id="c7079-127">Jeśli nie po podaj jednego z tych dwóch parametrów zapytania, zostanie wyświetlony błąd **400 (Złe żądanie).**</span><span class="sxs-lookup"><span data-stu-id="c7079-127">If you don't provide one of these two query parameters, you will receive a **400 (Bad request)** error.</span></span>

| <span data-ttu-id="c7079-128">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c7079-128">Name</span></span> | <span data-ttu-id="c7079-129">Typ</span><span class="sxs-lookup"><span data-stu-id="c7079-129">Type</span></span> | <span data-ttu-id="c7079-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c7079-130">Required</span></span> | <span data-ttu-id="c7079-131">Opis</span><span class="sxs-lookup"><span data-stu-id="c7079-131">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="c7079-132">**MpnId**</span><span class="sxs-lookup"><span data-stu-id="c7079-132">**MpnId**</span></span> | <span data-ttu-id="c7079-133">int</span><span class="sxs-lookup"><span data-stu-id="c7079-133">int</span></span> | <span data-ttu-id="c7079-134">Nie</span><span class="sxs-lookup"><span data-stu-id="c7079-134">No</span></span> | <span data-ttu-id="c7079-135">Identyfikator Microsoft Partner Network (PGA/PLA), który identyfikuje odsprzedawcę pośredniego.</span><span class="sxs-lookup"><span data-stu-id="c7079-135">A Microsoft Partner Network ID (PGA/PLA) that identifies the indirect reseller.</span></span> |
| <span data-ttu-id="c7079-136">**TenantId**</span><span class="sxs-lookup"><span data-stu-id="c7079-136">**TenantId**</span></span> | <span data-ttu-id="c7079-137">GUID</span><span class="sxs-lookup"><span data-stu-id="c7079-137">GUID</span></span> | <span data-ttu-id="c7079-138">Nie</span><span class="sxs-lookup"><span data-stu-id="c7079-138">No</span></span> | <span data-ttu-id="c7079-139">Identyfikator firmy Microsoft, który identyfikuje konto CSP odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="c7079-139">A Microsoft ID that identifies the CSP account of the indirect reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c7079-140">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="c7079-140">Request headers</span></span>

<span data-ttu-id="c7079-141">Aby uzyskać więcej informacji, zobacz [Partner Center REST](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c7079-141">For more information, see [Partner Center REST](headers.md).</span></span>

### <a name="request-examples"></a><span data-ttu-id="c7079-142">Przykłady żądań</span><span class="sxs-lookup"><span data-stu-id="c7079-142">Request examples</span></span>

#### <a name="request-using-mpn-id-pgapla"></a><span data-ttu-id="c7079-143">Żądanie przy użyciu identyfikatora MPN (PGA/PLA)</span><span class="sxs-lookup"><span data-stu-id="c7079-143">Request using MPN ID (PGA/PLA)</span></span>

<span data-ttu-id="c7079-144">Następujące przykładowe żądanie pobiera stan Microsoft Partner Agreement podpisywania odsprzedawcy pośredniego przy użyciu identyfikatora Microsoft Partner Network odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="c7079-144">The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's Microsoft Partner Network ID.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a><span data-ttu-id="c7079-145">Żądanie przy użyciu identyfikatora dzierżawy CSP</span><span class="sxs-lookup"><span data-stu-id="c7079-145">Request using CSP tenant ID</span></span>

<span data-ttu-id="c7079-146">Następujące przykładowe żądanie pobiera stan podpisywania Microsoft Partner Agreement odsprzedawcy pośredniego przy użyciu identyfikatora dzierżawy CSP odsprzedawcy pośredniego (Microsoft ID).</span><span class="sxs-lookup"><span data-stu-id="c7079-146">The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's CSP tenant ID (Microsoft ID).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="c7079-147">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="c7079-147">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c7079-148">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c7079-148">Response success and error codes</span></span>

<span data-ttu-id="c7079-149">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="c7079-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c7079-150">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="c7079-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c7079-151">Aby uzyskać pełną listę, zobacz [Partner Center REST .](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="c7079-151">For the full list, see [Partner Center REST error](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="c7079-152">Przykład odpowiedzi (powodzenie)</span><span class="sxs-lookup"><span data-stu-id="c7079-152">Response example (success)</span></span>

<span data-ttu-id="c7079-153">Następująca przykładowa odpowiedź pomyślnie zwraca, czy odsprzedawca pośredni podpisał umowę Microsoft Partner Agreement.</span><span class="sxs-lookup"><span data-stu-id="c7079-153">The following example response successfully returns whether the indirect reseller has signed the Microsoft Partner Agreement.</span></span>

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

### <a name="response-examples-failure"></a><span data-ttu-id="c7079-154">Przykłady odpowiedzi (błąd)</span><span class="sxs-lookup"><span data-stu-id="c7079-154">Response examples (failure)</span></span>

<span data-ttu-id="c7079-155">Odpowiedzi mogą być podobne do poniższych przykładów, gdy nie można zwrócić stanu Microsoft Partner Agreement odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="c7079-155">You may receive responses similar to the following examples when the signing status of the indirect reseller's Microsoft Partner Agreement can't be returned.</span></span>

#### <a name="non-guid-formatted-csp-tenant-id"></a><span data-ttu-id="c7079-156">Identyfikator dzierżawy CSP sformatowany bez identyfikatora GUID</span><span class="sxs-lookup"><span data-stu-id="c7079-156">Non-GUID formatted CSP tenant ID</span></span>

<span data-ttu-id="c7079-157">Następująca przykładowa odpowiedź jest zwracana, gdy identyfikator dzierżawy dostawcy usług kryptograficznych przekazany do interfejsu API nie jest identyfikatorem GUID.</span><span class="sxs-lookup"><span data-stu-id="c7079-157">The following example response is returned when the CSP tenant ID that you passed to the API isn't a GUID.</span></span>

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

#### <a name="non-numeric-mpn-id"></a><span data-ttu-id="c7079-158">Nieliczbowy identyfikator MPN</span><span class="sxs-lookup"><span data-stu-id="c7079-158">Non-numeric MPN ID</span></span>

<span data-ttu-id="c7079-159">Następująca przykładowa odpowiedź jest zwracana, gdy identyfikator MPN (PGA/PLA) przekazany do interfejsu API jest nieliczbowy.</span><span class="sxs-lookup"><span data-stu-id="c7079-159">The following example response is returned when the MPN ID (PGA/PLA) that you passed to the API is non-numeric.</span></span>

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

#### <a name="no-mpn-id-or-csp-tenant-id"></a><span data-ttu-id="c7079-160">Brak identyfikatora MPN lub identyfikatora dzierżawy CSP</span><span class="sxs-lookup"><span data-stu-id="c7079-160">No MPN ID or CSP tenant ID</span></span>

<span data-ttu-id="c7079-161">Następująca przykładowa odpowiedź jest zwracana, gdy do interfejsu API nie przekazano identyfikatora MPN (PGA/PLA) lub identyfikatora dzierżawy dostawcy CSP.</span><span class="sxs-lookup"><span data-stu-id="c7079-161">The following example response is returned when you haven't passed an MPN ID (PGA/PLA) or CSP tenant ID to the API.</span></span> <span data-ttu-id="c7079-162">Do interfejsu API należy przekazać jeden z dwóch typów identyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="c7079-162">You must pass one of the two ID types to the API.</span></span>

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

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a><span data-ttu-id="c7079-163">Przekazano zarówno identyfikator MPN, jak i identyfikator dzierżawy CSP</span><span class="sxs-lookup"><span data-stu-id="c7079-163">Both MPN ID and CSP tenant ID passed</span></span>

<span data-ttu-id="c7079-164">Następująca przykładowa odpowiedź jest zwracana, gdy do interfejsu API przekażemy zarówno identyfikator MPN ID (PGA/PLA), jak i identyfikator dzierżawy dostawcy CSP.</span><span class="sxs-lookup"><span data-stu-id="c7079-164">The following example response is returned when you pass both the MPN ID (PGA/PLA) and CSP tenant ID to the API.</span></span> <span data-ttu-id="c7079-165">Do *interfejsu* API należy przekazać tylko jeden z dwóch typów identyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="c7079-165">You must pass *only one* of the two identifier types to the API.</span></span>

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

#### <a name="csp-indirect-reseller-mpn-id-pgapla-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a><span data-ttu-id="c7079-166">CSP Indirect Reseller IDENTYFIKATOR MPN (PGA/PLA) jest nieprawidłowy lub nie jest migrowany z Partner Membership Center do Partner Center</span><span class="sxs-lookup"><span data-stu-id="c7079-166">CSP Indirect Reseller MPN ID (PGA/PLA) is either invalid or not migrated from Partner Membership Center to Partner Center</span></span>

<span data-ttu-id="c7079-167">Następująca przykładowa odpowiedź jest zwracana, gdy przekazany identyfikator MPN odsprzedawcy pośredniego (PGA/PLA) jest nieprawidłowy lub nie jest migrowany z Partner Membership Center do Partner Center.</span><span class="sxs-lookup"><span data-stu-id="c7079-167">The following example response is returned when Indirect reseller MPN ID (PGA/PLA) passed is either invalid or it is not migrated from Partner Membership Center to Partner Center.</span></span> [<span data-ttu-id="c7079-168">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="c7079-168">Learn More</span></span>](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

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

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a><span data-ttu-id="c7079-169">CSP Indirect Provider region i CSP Indirect Reseller są zgodne</span><span class="sxs-lookup"><span data-stu-id="c7079-169">CSP Indirect Provider region and CSP Indirect Reseller region does not match</span></span>

<span data-ttu-id="c7079-170">Następująca przykładowa odpowiedź jest zwracana, gdy region odsprzedawcy pośredniego o identyfikatorze MPN (PGA/PLA) nie pasuje do regionu dostawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="c7079-170">The following example response is returned when region of Indirect reseller MPN ID (PGA/PLA) doesn't match with region of the Indirect Provider.</span></span> <span data-ttu-id="c7079-171">[Dowiedz się więcej](/partner-center/mpa-indirect-provider-faq) o regionach CSP.</span><span class="sxs-lookup"><span data-stu-id="c7079-171">[Learn more](/partner-center/mpa-indirect-provider-faq) about CSP Regions.</span></span>

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

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a><span data-ttu-id="c7079-172">CSP Indirect Reseller istnieje w Partner Center, ale nie ma podpisanego umowy MPA</span><span class="sxs-lookup"><span data-stu-id="c7079-172">CSP Indirect Reseller account exists in Partner Center but hasn't signed the MPA</span></span>

<span data-ttu-id="c7079-173">Następująca przykładowa odpowiedź jest zwracana, CSP Indirect Reseller konto w Partner Center nie ma podpisanego umowy MPA.</span><span class="sxs-lookup"><span data-stu-id="c7079-173">The following example response is returned when CSP Indirect Reseller account in Partner Center hasn't signed the MPA.</span></span> [<span data-ttu-id="c7079-174">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="c7079-174">Learn More</span></span>](/partner-center/mpa-indirect-provider-faq)

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

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a><span data-ttu-id="c7079-175">Żadne CSP Indirect Reseller nie jest skojarzone z danym identyfikatorem MPN</span><span class="sxs-lookup"><span data-stu-id="c7079-175">No CSP Indirect Reseller account is associated with the given MPN ID</span></span>

<span data-ttu-id="c7079-176">Następująca przykładowa odpowiedź jest zwracana, gdy program Partner Center może rozpoznać identyfikator MPN (PGA/PLA) przekazany w żądaniu, ale nie istnieje rejestracja CSP skojarzona z danym identyfikatorem MPN (PGA/PLA).</span><span class="sxs-lookup"><span data-stu-id="c7079-176">The following example response is returned when Partner Center can recognize the MPN ID (PGA/PLA) passed in the request but there is no CSP enrollment associated to the given MPN ID (PGA/PLA).</span></span> [<span data-ttu-id="c7079-177">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="c7079-177">Learn More</span></span>](/partner-center/mpa-indirect-provider-faq)

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

#### <a name="invalid-tenant-id"></a><span data-ttu-id="c7079-178">Nieprawidłowy identyfikator dzierżawy</span><span class="sxs-lookup"><span data-stu-id="c7079-178">Invalid Tenant ID</span></span>

<span data-ttu-id="c7079-179">Następująca przykładowa odpowiedź jest zwracana, Partner Center nie znajdzie żadnego konta skojarzonego z identyfikatorem dzierżawy przekazanym w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="c7079-179">The following example response is returned when Partner Center doesn't find any account associated to the Tenant ID passed in the request.</span></span>

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

#### <a name="no-mpa-found-with-the-given-tenant-id"></a><span data-ttu-id="c7079-180">Nie znaleziono mpA o danym identyfikatorze dzierżawy</span><span class="sxs-lookup"><span data-stu-id="c7079-180">No MPA found with the given Tenant ID</span></span>

<span data-ttu-id="c7079-181">Następująca przykładowa odpowiedź jest zwracana, Partner Center nie może znaleźć żadnego podpisu MPA o danym identyfikatorze dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="c7079-181">The following example response is returned when Partner Center can't find any MPA signature with the given Tenant ID.</span></span> [<span data-ttu-id="c7079-182">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="c7079-182">Learn More</span></span>](/partner-center/mpa-indirect-provider-faq)

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