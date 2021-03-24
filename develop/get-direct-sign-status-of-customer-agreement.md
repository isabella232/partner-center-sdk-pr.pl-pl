---
title: Pobierz bezpośredni stan podpisywania klienta dla umowy Microsoft Customer Agreement.
description: Za pomocą zasobu DirectSignedCustomerAgreementStatus można uzyskać status bezpośredniego podpisywania klienta (bezpośrednie zatwierdzenie) umowy klienta firmy Microsoft.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 267e3aa63a94c5045977ad566eb5061df3b59882
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030566"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="4aef5-103">Uzyskaj status bezpośredniego podpisywania klienta (bezpośrednie zatwierdzenie) umowy klienta firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="4aef5-103">Get the status of a customer's direct signing (direct acceptance) of Microsoft Customer Agreement</span></span>

<span data-ttu-id="4aef5-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="4aef5-104">**Applies to:**</span></span>

- <span data-ttu-id="4aef5-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="4aef5-105">Partner Center</span></span>

<span data-ttu-id="4aef5-106">Zasób **DirectSignedCustomerAgreementStatus** jest obecnie obsługiwany przez centrum partnerskie tylko w chmurze publicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4aef5-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="4aef5-107">Ten zasób *nie ma zastosowania* do:</span><span class="sxs-lookup"><span data-stu-id="4aef5-107">This resource is *not applicable* to:</span></span>

- <span data-ttu-id="4aef5-108">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="4aef5-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="4aef5-109">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="4aef5-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="4aef5-110">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="4aef5-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4aef5-111">W tym artykule wyjaśniono, jak można pobrać stan bezpośredniej akceptacji umowy klienta firmy Microsoft przez klienta.</span><span class="sxs-lookup"><span data-stu-id="4aef5-111">This article explains how you can retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4aef5-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4aef5-112">Prerequisites</span></span>

- <span data-ttu-id="4aef5-113">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4aef5-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4aef5-114">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4aef5-114">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="4aef5-115">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4aef5-115">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4aef5-116">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="4aef5-116">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4aef5-117">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="4aef5-117">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4aef5-118">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="4aef5-118">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4aef5-119">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="4aef5-119">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4aef5-120">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4aef5-120">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="4aef5-121">C\#</span><span class="sxs-lookup"><span data-stu-id="4aef5-121">C\#</span></span>

<span data-ttu-id="4aef5-122">Aby pobrać stan bezpośredniego akceptacji umowy klienta firmy Microsoft przez klienta, wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta.</span><span class="sxs-lookup"><span data-stu-id="4aef5-122">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="4aef5-123">Następnie użyj właściwości [**Agreements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) , aby pobrać Interfejs [**ICustomerAgreementCollection**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) .</span><span class="sxs-lookup"><span data-stu-id="4aef5-123">Then use the [**Agreements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) property to retrieve a [**ICustomerAgreementCollection**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) interface.</span></span> <span data-ttu-id="4aef5-124">Na koniec Wywołaj `GetDirectSignedCustomerAgreementStatus()` lub, `GetDirectSignedCustomerAgreementStatusAsync()` Aby pobrać stan.</span><span class="sxs-lookup"><span data-stu-id="4aef5-124">Finally, call `GetDirectSignedCustomerAgreementStatus()` or `GetDirectSignedCustomerAgreementStatusAsync()` to retrieve the status.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerDirectSigningStatus = partnerOperations.Customers.ById(selectedCustomerId).Agreements.GetDirectSignedCustomerAgreementStatus();
```

<span data-ttu-id="4aef5-125">**Przykład**: [Przykładowa aplikacja konsolowa](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="4aef5-125">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="4aef5-126">**Projekt**: SdkSamples **Class**: GetDirectSignedCustomerAgreementStatus. cs</span><span class="sxs-lookup"><span data-stu-id="4aef5-126">**Project**: SdkSamples **Class**: GetDirectSignedCustomerAgreementStatus.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="4aef5-127">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="4aef5-127">REST request</span></span>

<span data-ttu-id="4aef5-128">Aby pobrać stan bezpośredniej akceptacji umowy klienta firmy Microsoft przez klienta, Utwórz żądanie REST w celu pobrania [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) dla klienta.</span><span class="sxs-lookup"><span data-stu-id="4aef5-128">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, create a REST request to retrieve the [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) for the customer.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4aef5-129">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="4aef5-129">Request syntax</span></span>

<span data-ttu-id="4aef5-130">Użyj następującej składni żądania:</span><span class="sxs-lookup"><span data-stu-id="4aef5-130">Use the following request syntax:</span></span>

| <span data-ttu-id="4aef5-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="4aef5-131">Method</span></span> | <span data-ttu-id="4aef5-132">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="4aef5-132">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4aef5-133">GET</span><span class="sxs-lookup"><span data-stu-id="4aef5-133">GET</span></span>    | <span data-ttu-id="4aef5-134">[*\{ BASEURL \}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/directSignedMicrosoftCustomerAgreementStatus http/1.1</span><span class="sxs-lookup"><span data-stu-id="4aef5-134">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="4aef5-135">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="4aef5-135">URI parameters</span></span>

<span data-ttu-id="4aef5-136">Z żądaniem można użyć następujących parametrów URI:</span><span class="sxs-lookup"><span data-stu-id="4aef5-136">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="4aef5-137">Nazwa</span><span class="sxs-lookup"><span data-stu-id="4aef5-137">Name</span></span>             | <span data-ttu-id="4aef5-138">Typ</span><span class="sxs-lookup"><span data-stu-id="4aef5-138">Type</span></span> | <span data-ttu-id="4aef5-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4aef5-139">Required</span></span> | <span data-ttu-id="4aef5-140">Opis</span><span class="sxs-lookup"><span data-stu-id="4aef5-140">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="4aef5-141">Identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="4aef5-141">customer-tenant-id</span></span> | <span data-ttu-id="4aef5-142">GUID</span><span class="sxs-lookup"><span data-stu-id="4aef5-142">GUID</span></span> | <span data-ttu-id="4aef5-143">Tak</span><span class="sxs-lookup"><span data-stu-id="4aef5-143">Yes</span></span> | <span data-ttu-id="4aef5-144">Wartość jest **CustomerTenantId** w formacie GUID, która umożliwia określenie identyfikatora dzierżawy klienta.</span><span class="sxs-lookup"><span data-stu-id="4aef5-144">The value is a GUID-formatted **CustomerTenantId** that allows you to specify the tenant ID of a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4aef5-145">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="4aef5-145">Request headers</span></span>

<span data-ttu-id="4aef5-146">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4aef5-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4aef5-147">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="4aef5-147">Request body</span></span>

<span data-ttu-id="4aef5-148">Brak.</span><span class="sxs-lookup"><span data-stu-id="4aef5-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4aef5-149">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="4aef5-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="4aef5-150">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="4aef5-150">REST response</span></span>

<span data-ttu-id="4aef5-151">Jeśli to się powiedzie, metoda zwraca [zasób **DirectSignedCustomerAgreementStatus**](./customer-agreement-direct-sign-status-resource.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="4aef5-151">If successful, this method returns a [**DirectSignedCustomerAgreementStatus** resource](./customer-agreement-direct-sign-status-resource.md) in the response body.</span></span>

<span data-ttu-id="4aef5-152">Zasób ma właściwość **IsSigned** , która wskazuje stan bezpośredniego podpisywania klienta (zatwierdzenie bezpośrednie).</span><span class="sxs-lookup"><span data-stu-id="4aef5-152">The resource has an **isSigned** property that indicates the customer's direct signing (direct acceptance) status.</span></span>

- <span data-ttu-id="4aef5-153">Wartość **true** wskazuje, że umowa została podpisana (zaakceptowana) bezpośrednio przez klienta.</span><span class="sxs-lookup"><span data-stu-id="4aef5-153">A value of **true** indicates that the agreement has been signed (accepted) directly by the customer.</span></span>

- <span data-ttu-id="4aef5-154">Wartość **false** wskazuje, że umowa *nie* została podpisana (zaakceptowana) bezpośrednio przez klienta.</span><span class="sxs-lookup"><span data-stu-id="4aef5-154">A value of **false** indicates that the agreement has *not* been signed (accepted) directly by the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4aef5-155">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4aef5-155">Response success and error codes</span></span>

<span data-ttu-id="4aef5-156">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="4aef5-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="4aef5-157">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="4aef5-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4aef5-158">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4aef5-158">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4aef5-159">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4aef5-159">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
