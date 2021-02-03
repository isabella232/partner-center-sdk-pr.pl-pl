---
title: Pobierz bezpośredni stan podpisywania klienta dla umowy Microsoft Customer Agreement.
description: Za pomocą zasobu DirectSignedCustomerAgreementStatus można uzyskać status bezpośredniego podpisywania klienta (bezpośrednie zatwierdzenie) umowy klienta firmy Microsoft.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 3f1deb20a18bc6e7133cac91db528f2d1ad694e2
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767701"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="52413-103">Uzyskaj status bezpośredniego podpisywania klienta (bezpośrednie zatwierdzenie) umowy klienta firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="52413-103">Get the status of a customer's direct signing (direct acceptance) of Microsoft Customer Agreement</span></span>

<span data-ttu-id="52413-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="52413-104">**Applies to:**</span></span>

- <span data-ttu-id="52413-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="52413-105">Partner Center</span></span>

<span data-ttu-id="52413-106">Zasób **DirectSignedCustomerAgreementStatus** jest obecnie obsługiwany przez centrum partnerskie tylko w chmurze publicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="52413-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="52413-107">Ten zasób *nie ma zastosowania* do:</span><span class="sxs-lookup"><span data-stu-id="52413-107">This resource is *not applicable* to:</span></span>

- <span data-ttu-id="52413-108">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="52413-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="52413-109">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="52413-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="52413-110">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="52413-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="52413-111">W tym artykule wyjaśniono, jak można pobrać stan bezpośredniej akceptacji umowy klienta firmy Microsoft przez klienta.</span><span class="sxs-lookup"><span data-stu-id="52413-111">This article explains how you can retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="rest-request"></a><span data-ttu-id="52413-112">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="52413-112">REST request</span></span>

<span data-ttu-id="52413-113">Aby pobrać stan bezpośredniej akceptacji umowy klienta firmy Microsoft przez klienta, Utwórz żądanie REST w celu pobrania [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) dla klienta.</span><span class="sxs-lookup"><span data-stu-id="52413-113">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, create a REST request to retrieve the [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) for the customer.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="52413-114">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="52413-114">Request syntax</span></span>

<span data-ttu-id="52413-115">Użyj następującej składni żądania:</span><span class="sxs-lookup"><span data-stu-id="52413-115">Use the following request syntax:</span></span>

| <span data-ttu-id="52413-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="52413-116">Method</span></span> | <span data-ttu-id="52413-117">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="52413-117">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="52413-118">GET</span><span class="sxs-lookup"><span data-stu-id="52413-118">GET</span></span>    | <span data-ttu-id="52413-119">[*\{ BASEURL \}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/directSignedMicrosoftCustomerAgreementStatus http/1.1</span><span class="sxs-lookup"><span data-stu-id="52413-119">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="52413-120">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="52413-120">URI parameters</span></span>

<span data-ttu-id="52413-121">Z żądaniem można użyć następujących parametrów URI:</span><span class="sxs-lookup"><span data-stu-id="52413-121">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="52413-122">Nazwa</span><span class="sxs-lookup"><span data-stu-id="52413-122">Name</span></span>             | <span data-ttu-id="52413-123">Typ</span><span class="sxs-lookup"><span data-stu-id="52413-123">Type</span></span> | <span data-ttu-id="52413-124">Wymagane</span><span class="sxs-lookup"><span data-stu-id="52413-124">Required</span></span> | <span data-ttu-id="52413-125">Opis</span><span class="sxs-lookup"><span data-stu-id="52413-125">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="52413-126">Identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="52413-126">customer-tenant-id</span></span> | <span data-ttu-id="52413-127">GUID</span><span class="sxs-lookup"><span data-stu-id="52413-127">GUID</span></span> | <span data-ttu-id="52413-128">Tak</span><span class="sxs-lookup"><span data-stu-id="52413-128">Yes</span></span> | <span data-ttu-id="52413-129">Wartość jest **CustomerTenantId** w formacie GUID, która umożliwia określenie identyfikatora dzierżawy klienta.</span><span class="sxs-lookup"><span data-stu-id="52413-129">The value is a GUID-formatted **CustomerTenantId** that allows you to specify the tenant ID of a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="52413-130">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="52413-130">Request headers</span></span>

<span data-ttu-id="52413-131">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="52413-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="52413-132">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="52413-132">Request body</span></span>

<span data-ttu-id="52413-133">Brak.</span><span class="sxs-lookup"><span data-stu-id="52413-133">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="52413-134">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="52413-134">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="52413-135">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="52413-135">REST response</span></span>

<span data-ttu-id="52413-136">Jeśli to się powiedzie, metoda zwraca [zasób **DirectSignedCustomerAgreementStatus**](./customer-agreement-direct-sign-status-resource.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="52413-136">If successful, this method returns a [**DirectSignedCustomerAgreementStatus** resource](./customer-agreement-direct-sign-status-resource.md) in the response body.</span></span>

<span data-ttu-id="52413-137">Zasób ma właściwość **IsSigned** , która wskazuje stan bezpośredniego podpisywania klienta (zatwierdzenie bezpośrednie).</span><span class="sxs-lookup"><span data-stu-id="52413-137">The resource has an **isSigned** property that indicates the customer's direct signing (direct acceptance) status.</span></span>

- <span data-ttu-id="52413-138">Wartość **true** wskazuje, że umowa została podpisana (zaakceptowana) bezpośrednio przez klienta.</span><span class="sxs-lookup"><span data-stu-id="52413-138">A value of **true** indicates that the agreement has been signed (accepted) directly by the customer.</span></span>

- <span data-ttu-id="52413-139">Wartość **false** wskazuje, że umowa *nie* została podpisana (zaakceptowana) bezpośrednio przez klienta.</span><span class="sxs-lookup"><span data-stu-id="52413-139">A value of **false** indicates that the agreement has *not* been signed (accepted) directly by the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="52413-140">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="52413-140">Response success and error codes</span></span>

<span data-ttu-id="52413-141">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="52413-141">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="52413-142">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="52413-142">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="52413-143">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="52413-143">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="52413-144">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="52413-144">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
