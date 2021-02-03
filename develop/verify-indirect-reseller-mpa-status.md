---
title: Weryfikowanie statusu podpisywania umowy partnerskiej firmy Microsoft pośredniego odsprzedawcy
description: Możesz użyć interfejsu API AgreementStatus, aby sprawdzić, czy pośredni odsprzedawca podpisał umowę partnera firmy Microsoft.
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 436f690991a2920465a5a13c73eb4c194956ae94
ms.sourcegitcommit: ca932ba511bf7464a634195d71891f989036ab74
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/29/2020
ms.locfileid: "97768497"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a><span data-ttu-id="fa772-103">Weryfikowanie statusu podpisywania umowy partnerskiej firmy Microsoft pośredniego odsprzedawcy</span><span class="sxs-lookup"><span data-stu-id="fa772-103">Verify an indirect reseller's Microsoft Partner Agreement signing status</span></span>

<span data-ttu-id="fa772-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="fa772-104">**Applies to:**</span></span>

- <span data-ttu-id="fa772-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="fa772-105">Partner Center</span></span>
- <span data-ttu-id="fa772-106">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="fa772-106">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="fa772-107">Możesz sprawdzić, czy pośredni odsprzedawca podpisał umowę partnera firmy Microsoft przy użyciu identyfikatora dzierżawy usługi Microsoft Partner Network (MPN) (PGA/PLA) lub dostawcy rozwiązań w chmurze (CSP).</span><span class="sxs-lookup"><span data-stu-id="fa772-107">You can verify whether an indirect reseller has signed the Microsoft Partner Agreement using their Microsoft Partner Network (MPN) ID (PGA/PLA) or Cloud Solution Provider (CSP) tenant ID (Microsoft ID).</span></span> <span data-ttu-id="fa772-108">Możesz użyć jednego z tych identyfikatorów, aby sprawdzić stan podpisywania umowy Microsoft Partner Agreement przy użyciu interfejsu API **AgreementStatus** .</span><span class="sxs-lookup"><span data-stu-id="fa772-108">You can use one of these identifiers to check the Microsoft Partner Agreement signing status using the **AgreementStatus** API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa772-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fa772-109">Prerequisites</span></span>

- <span data-ttu-id="fa772-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fa772-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fa772-111">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fa772-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="fa772-112">IDENTYFIKATOR MPN (PGA/PLA) lub identyfikator dzierżawy dostawcy usług kryptograficznych (Microsoft ID) pośredniego odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="fa772-112">The MPN ID (PGA/PLA) or the CSP tenant ID (Microsoft ID) of the indirect reseller.</span></span> <span data-ttu-id="fa772-113">*Musisz użyć jednego z tych dwóch identyfikatorów.*</span><span class="sxs-lookup"><span data-stu-id="fa772-113">*You must use one of these two identifiers.*</span></span>

## <a name="c"></a><span data-ttu-id="fa772-114">C\#</span><span class="sxs-lookup"><span data-stu-id="fa772-114">C\#</span></span>

<span data-ttu-id="fa772-115">Aby uzyskać status podpisu umowy partnerskiej firmy Microsoft dla pośredniego odsprzedawcy:</span><span class="sxs-lookup"><span data-stu-id="fa772-115">To get the Microsoft Partner Agreement signature status of an indirect reseller:</span></span>

1. <span data-ttu-id="fa772-116">Użyj kolekcji **IAggregatePartner. zgodność** , aby wywołać Właściwość **AgreementSignatureStatus** .</span><span class="sxs-lookup"><span data-stu-id="fa772-116">Use your **IAggregatePartner.Compliance** collection to call the **AgreementSignatureStatus** property.</span></span>

2. <span data-ttu-id="fa772-117">Wywołaj metodę [**Get ()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) lub [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) .</span><span class="sxs-lookup"><span data-stu-id="fa772-117">Call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id (PGA/PLA)");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- <span data-ttu-id="fa772-118">Przykład: **[aplikacja testowa konsoli](console-test-app.md)**</span><span class="sxs-lookup"><span data-stu-id="fa772-118">Sample: **[Console test app](console-test-app.md)**</span></span>
- <span data-ttu-id="fa772-119">Projekt: **PartnerCenterSDK. FeaturesSamples**</span><span class="sxs-lookup"><span data-stu-id="fa772-119">Project: **PartnerCenterSDK.FeaturesSamples**</span></span>
- <span data-ttu-id="fa772-120">Klasa: **GetAgreementSignatureStatus.cs**</span><span class="sxs-lookup"><span data-stu-id="fa772-120">Class: **GetAgreementSignatureStatus.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="fa772-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="fa772-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fa772-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="fa772-122">Request syntax</span></span>

| <span data-ttu-id="fa772-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="fa772-123">Method</span></span> | <span data-ttu-id="fa772-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="fa772-124">Request URI</span></span> |
| ------ | ----------- |
| <span data-ttu-id="fa772-125">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="fa772-125">**GET**</span></span> | <span data-ttu-id="fa772-126">*[{baseURL}](partner-center-rest-urls.md)*/V1/Compliance/{ProgramName}/agreementstatus? mpnId = {mpnId} &tenantId = {tenantId}</span><span class="sxs-lookup"><span data-stu-id="fa772-126">*[{baseURL}](partner-center-rest-urls.md)*/v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="fa772-127">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="fa772-127">URI parameters</span></span>

<span data-ttu-id="fa772-128">Musisz podać jeden z następujących dwóch parametrów zapytania, aby zidentyfikować partnera.</span><span class="sxs-lookup"><span data-stu-id="fa772-128">You must provide one of the following two query parameters to identify the partner.</span></span> <span data-ttu-id="fa772-129">Jeśli nie podano jednego z tych dwóch parametrów zapytania, zostanie wyświetlony komunikat o błędzie **400 (Nieprawidłowe żądanie)** .</span><span class="sxs-lookup"><span data-stu-id="fa772-129">If you don't provide one of these two query parameters, you will receive a **400 (Bad request)** error.</span></span>

| <span data-ttu-id="fa772-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fa772-130">Name</span></span> | <span data-ttu-id="fa772-131">Typ</span><span class="sxs-lookup"><span data-stu-id="fa772-131">Type</span></span> | <span data-ttu-id="fa772-132">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fa772-132">Required</span></span> | <span data-ttu-id="fa772-133">Opis</span><span class="sxs-lookup"><span data-stu-id="fa772-133">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="fa772-134">**MpnId**</span><span class="sxs-lookup"><span data-stu-id="fa772-134">**MpnId**</span></span> | <span data-ttu-id="fa772-135">int</span><span class="sxs-lookup"><span data-stu-id="fa772-135">int</span></span> | <span data-ttu-id="fa772-136">Nie</span><span class="sxs-lookup"><span data-stu-id="fa772-136">No</span></span> | <span data-ttu-id="fa772-137">Identyfikator Microsoft Partner Network (PGA/PLA) identyfikujący pośredniego odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="fa772-137">A Microsoft Partner Network ID (PGA/PLA) that identifies the indirect reseller.</span></span> |
| <span data-ttu-id="fa772-138">**TenantId**</span><span class="sxs-lookup"><span data-stu-id="fa772-138">**TenantId**</span></span> | <span data-ttu-id="fa772-139">GUID</span><span class="sxs-lookup"><span data-stu-id="fa772-139">GUID</span></span> | <span data-ttu-id="fa772-140">Nie</span><span class="sxs-lookup"><span data-stu-id="fa772-140">No</span></span> | <span data-ttu-id="fa772-141">Identyfikator Microsoft, który identyfikuje konto CSP pośredniego odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="fa772-141">A Microsoft ID that identifies the CSP account of the indirect reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fa772-142">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="fa772-142">Request headers</span></span>

<span data-ttu-id="fa772-143">Aby uzyskać więcej informacji, zobacz temat [Partner Center REST](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fa772-143">For more information, see [Partner Center REST](headers.md).</span></span>

### <a name="request-examples"></a><span data-ttu-id="fa772-144">Przykłady żądań</span><span class="sxs-lookup"><span data-stu-id="fa772-144">Request examples</span></span>

#### <a name="request-using-mpn-id-pgapla"></a><span data-ttu-id="fa772-145">Żądanie przy użyciu identyfikatora MPN (PGA/PLA)</span><span class="sxs-lookup"><span data-stu-id="fa772-145">Request using MPN ID (PGA/PLA)</span></span>

<span data-ttu-id="fa772-146">Poniższe przykładowe żądanie Pobiera stan podpisywania umowy partnerskiej Microsoft Partner pośredni przy użyciu identyfikatora Microsoft Partner Network pośredniego odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="fa772-146">The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's Microsoft Partner Network ID.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a><span data-ttu-id="fa772-147">Żądanie przy użyciu identyfikatora dzierżawy CSP</span><span class="sxs-lookup"><span data-stu-id="fa772-147">Request using CSP tenant ID</span></span>

<span data-ttu-id="fa772-148">Poniższe przykładowe żądanie Pobiera stan podpisywania umowy partnerskiej Microsoft Partner pośredni przy użyciu identyfikatora dzierżawy dostawcy CSP pośredniego Odsprzedawcy (identyfikator firmy Microsoft).</span><span class="sxs-lookup"><span data-stu-id="fa772-148">The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's CSP tenant ID (Microsoft ID).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="fa772-149">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="fa772-149">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fa772-150">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fa772-150">Response success and error codes</span></span>

<span data-ttu-id="fa772-151">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="fa772-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fa772-152">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="fa772-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fa772-153">Aby uzyskać pełną listę, zobacz [błąd REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fa772-153">For the full list, see [Partner Center REST error](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="fa772-154">Przykład odpowiedzi (powodzenie)</span><span class="sxs-lookup"><span data-stu-id="fa772-154">Response example (success)</span></span>

<span data-ttu-id="fa772-155">Następująca przykładowa odpowiedź pomyślnie zwraca, czy pośredni odsprzedawca zapisał umowę partnera firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fa772-155">The following example response successfully returns whether the indirect reseller has signed the Microsoft Partner Agreement.</span></span>

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

### <a name="response-examples-failure"></a><span data-ttu-id="fa772-156">Przykłady odpowiedzi (niepowodzenie)</span><span class="sxs-lookup"><span data-stu-id="fa772-156">Response examples (failure)</span></span>

<span data-ttu-id="fa772-157">W przypadku, gdy nie można zwrócić stanu podpisywania pośredniej umowy partnerskiej partnera firmy Microsoft, użytkownik może otrzymywać odpowiedzi podobne do poniższych przykładów.</span><span class="sxs-lookup"><span data-stu-id="fa772-157">You may receive responses similar to the following examples when the signing status of the indirect reseller's Microsoft Partner Agreement can't be returned.</span></span>

#### <a name="non-guid-formatted-csp-tenant-id"></a><span data-ttu-id="fa772-158">Identyfikator dzierżawy CSP w formacie innym niż identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="fa772-158">Non-GUID formatted CSP tenant ID</span></span>

<span data-ttu-id="fa772-159">Poniższy przykład odpowiedzi jest zwracany, gdy identyfikator dzierżawy CSP, który został przesłany do interfejsu API, nie jest identyfikatorem GUID.</span><span class="sxs-lookup"><span data-stu-id="fa772-159">The following example response is returned when the CSP tenant ID that you passed to the API isn't a GUID.</span></span>

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

#### <a name="non-numeric-mpn-id"></a><span data-ttu-id="fa772-160">Nieliczbowy identyfikator MPN</span><span class="sxs-lookup"><span data-stu-id="fa772-160">Non-numeric MPN ID</span></span>

<span data-ttu-id="fa772-161">Poniższy Przykładowa odpowiedź jest zwracana, gdy identyfikator MPN (PGA/PLA), który został przesłany do interfejsu API, nie jest wartością numeryczną.</span><span class="sxs-lookup"><span data-stu-id="fa772-161">The following example response is returned when the MPN ID (PGA/PLA) that you passed to the API is non-numeric.</span></span>

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

#### <a name="no-mpn-id-or-csp-tenant-id"></a><span data-ttu-id="fa772-162">Brak identyfikatora dzierżawy lub identyfikatora MPN</span><span class="sxs-lookup"><span data-stu-id="fa772-162">No MPN ID or CSP tenant ID</span></span>

<span data-ttu-id="fa772-163">Poniższy przykład odpowiedzi jest zwracany, jeśli nie przeszedł identyfikator MPN (PGA/PLA) ani identyfikator dzierżawcy dostawcy CSP do interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="fa772-163">The following example response is returned when you haven't passed an MPN ID (PGA/PLA) or CSP tenant ID to the API.</span></span> <span data-ttu-id="fa772-164">Należy przekazać jeden z dwóch typów identyfikatorów do interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="fa772-164">You must pass one of the two ID types to the API.</span></span>

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

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a><span data-ttu-id="fa772-165">Przeszedł zarówno identyfikator MPN, jak i identyfikator dzierżawy dostawcy usług kryptograficznych</span><span class="sxs-lookup"><span data-stu-id="fa772-165">Both MPN ID and CSP tenant ID passed</span></span>

<span data-ttu-id="fa772-166">Poniższy Przykładowa odpowiedź jest zwracana w przypadku przekazywania identyfikatora MPN (PGA/PLA) i identyfikatora dzierżawy CSP do interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="fa772-166">The following example response is returned when you pass both the MPN ID (PGA/PLA) and CSP tenant ID to the API.</span></span> <span data-ttu-id="fa772-167">Do interfejsu API należy przekazać *tylko jeden* z dwóch typów identyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="fa772-167">You must pass *only one* of the two identifier types to the API.</span></span>

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

#### <a name="csp-indirect-reseller-mpn-id-pgapla-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a><span data-ttu-id="fa772-168">Pośredni odsprzedawca dostawcy usług kryptograficznych MPN identyfikator (PGA/PLA) jest nieprawidłowy lub nie został zmigrowany z Centrum członkostwa partnera do Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="fa772-168">CSP Indirect Reseller MPN Id (PGA/PLA) is either invalid or not migrated from Partner Membership Center to Partner Center</span></span>

<span data-ttu-id="fa772-169">Poniższy Przykładowa odpowiedź jest zwracana, gdy przekazana pośredni identyfikator MPN (PGA/PLA) jest nieprawidłowa lub nie została zmigrowana z Centrum członkostwa partnera do Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="fa772-169">The following example response is returned when Indirect reseller MPN ID (PGA/PLA) passed is either invalid or it is not migrated from Partner Membership Center to Partner Center.</span></span> [<span data-ttu-id="fa772-170">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="fa772-170">Learn More</span></span>](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

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
        "https://partner.microsoft.com/en-us/resources/detail/migrate-pmc-pc-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a><span data-ttu-id="fa772-171">Region pośredni dostawcy usług kryptograficznych i region niebezpośredniego odsprzedawcy dostawcy CSP nie są zgodne</span><span class="sxs-lookup"><span data-stu-id="fa772-171">CSP Indirect Provider region and CSP Indirect Reseller region does not match</span></span>

<span data-ttu-id="fa772-172">Poniższy Przykładowa odpowiedź jest zwracana, gdy region pośredniego odsprzedawcy MPN (PGA/PLA) nie jest zgodny z regionem dostawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="fa772-172">The following example response is returned when region of Indirect reseller MPN ID (PGA/PLA) doesn't match with region of the Indirect Provider.</span></span> <span data-ttu-id="fa772-173">[Dowiedz się więcej](/partner-center/regional-authorization-overview) o regionach dostawcy usług kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="fa772-173">[Learn more](/partner-center/regional-authorization-overview) about CSP Regions.</span></span>

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
        "https://docs.microsoft.com/en-us/partner-center/regional-authorization-overview" 
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a><span data-ttu-id="fa772-174">Pośredniego konta odsprzedawcy CSP istnieje w centrum partnerskim, ale nie podpisałem MPA</span><span class="sxs-lookup"><span data-stu-id="fa772-174">CSP Indirect Reseller account exists in Partner Center but hasn't signed the MPA</span></span>

<span data-ttu-id="fa772-175">Poniższy przykład odpowiedzi jest zwracany, gdy konto odsprzedawcy pośredniego dostawcy CSP w centrum partnerskim nie podpisał MPA.</span><span class="sxs-lookup"><span data-stu-id="fa772-175">The following example response is returned when CSP Indirect Reseller account in Partner Center hasn't signed the MPA.</span></span> [<span data-ttu-id="fa772-176">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="fa772-176">Learn More</span></span>](https://partner.microsoft.com/resources/detail/verify-mpa-acceptance-status-pptx)

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
        "https://partner.microsoft.com/en-gb/resources/detail/verify-mpa-acceptance-status-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a><span data-ttu-id="fa772-177">Brak pośredniego konta odsprzedawcy dostawcy CSP powiązanego z danym IDENTYFIKATORem MPN</span><span class="sxs-lookup"><span data-stu-id="fa772-177">No CSP Indirect Reseller account is associated with the given MPN ID</span></span>

<span data-ttu-id="fa772-178">Poniższy Przykładowa odpowiedź jest zwracana, gdy centrum partnerskie może rozpoznać identyfikator MPN (PGA/PLA) przekazany w żądaniu, ale nie istnieje Rejestracja dostawcy CSP skojarzona z danym IDENTYFIKATORem MPN (PGA/PLA).</span><span class="sxs-lookup"><span data-stu-id="fa772-178">The following example response is returned when Partner Center can recognize the MPN ID (PGA/PLA) passed in the request but there is no CSP enrollment associated to the given MPN ID (PGA/PLA).</span></span> [<span data-ttu-id="fa772-179">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="fa772-179">Learn More</span></span>](https://partner.microsoft.com/resources/detail/onboard-pc-csp-mpn-mpa-guide-pptx)

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
        "https://partner.microsoft.com/en-us/resources/detail/onboard-pc-csp-mpn-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="invalid-tenant-id"></a><span data-ttu-id="fa772-180">Nieprawidłowy identyfikator dzierżawy</span><span class="sxs-lookup"><span data-stu-id="fa772-180">Invalid Tenant ID</span></span>

<span data-ttu-id="fa772-181">Poniższy Przykładowa odpowiedź jest zwracana, gdy centrum partnerskie nie znajdzie żadnego konta skojarzonego z IDENTYFIKATORem dzierżawy przesłanego w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="fa772-181">The following example response is returned when Partner Center doesn't find any account associated to the Tenant ID passed in the request.</span></span>

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

#### <a name="no-mpa-found-with-the-given-tenant-id"></a><span data-ttu-id="fa772-182">Nie znaleziono platformy MPA o podanym IDENTYFIKATORze dzierżawy</span><span class="sxs-lookup"><span data-stu-id="fa772-182">No MPA found with the given Tenant ID</span></span>

<span data-ttu-id="fa772-183">Poniższy Przykładowa odpowiedź jest zwracana, gdy centrum partnerskie nie może znaleźć żadnego z nich podpisania MPA z danym IDENTYFIKATORem dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="fa772-183">The following example response is returned when Partner Center can't find any MPA signature with the given Tenant ID.</span></span>

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
    "data": [],
    "source": "PartnerFD"
}
```
