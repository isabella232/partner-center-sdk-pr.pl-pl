---
title: Uzyskiwanie stanu bezpośredniego podpisywania klienta dla Umowa z Klientem Microsoft.
description: Możesz użyć zasobu DirectSignedCustomerAgreementStatus, aby uzyskać stan bezpośredniego podpisywania klienta (akceptacja bezpośrednia) Umowa z Klientem Microsoft.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: a17775614b4eb328514b2b32b4cac1e513019cff
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549182"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="9e968-103">Uzyskiwanie stanu bezpośredniego podpisywania klienta (akceptacja bezpośrednia) Umowa z Klientem Microsoft</span><span class="sxs-lookup"><span data-stu-id="9e968-103">Get the status of a customer's direct signing (direct acceptance) of Microsoft Customer Agreement</span></span>

<span data-ttu-id="9e968-104">**Dotyczy:** Partner Center</span><span class="sxs-lookup"><span data-stu-id="9e968-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="9e968-105">**Nie dotyczy:** Partner Center obsługiwane przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9e968-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9e968-106">Zasób **DirectSignedCustomerAgreementStatus** jest obecnie obsługiwany Partner Center tylko w chmurze publicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9e968-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="9e968-107">W tym artykule wyjaśniono, jak można pobrać stan bezpośredniej akceptacji klienta dla Umowa z Klientem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9e968-107">This article explains how you can retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e968-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9e968-108">Prerequisites</span></span>

- <span data-ttu-id="9e968-109">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9e968-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9e968-110">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9e968-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="9e968-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9e968-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9e968-112">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="9e968-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9e968-113">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="9e968-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9e968-114">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="9e968-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9e968-115">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="9e968-115">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9e968-116">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9e968-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="9e968-117">C\#</span><span class="sxs-lookup"><span data-stu-id="9e968-117">C\#</span></span>

<span data-ttu-id="9e968-118">Aby pobrać stan bezpośredniej akceptacji klienta dla klienta Umowa z Klientem Microsoft, wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta.</span><span class="sxs-lookup"><span data-stu-id="9e968-118">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="9e968-119">Następnie użyj właściwości [**Agreements,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) aby pobrać [**interfejs ICustomerAgreementCollection.**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection)</span><span class="sxs-lookup"><span data-stu-id="9e968-119">Then use the [**Agreements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) property to retrieve a [**ICustomerAgreementCollection**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) interface.</span></span> <span data-ttu-id="9e968-120">Na koniec `GetDirectSignedCustomerAgreementStatus()` wywołaj lub `GetDirectSignedCustomerAgreementStatusAsync()` , aby pobrać stan.</span><span class="sxs-lookup"><span data-stu-id="9e968-120">Finally, call `GetDirectSignedCustomerAgreementStatus()` or `GetDirectSignedCustomerAgreementStatusAsync()` to retrieve the status.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerDirectSigningStatus = partnerOperations.Customers.ById(selectedCustomerId).Agreements.GetDirectSignedCustomerAgreementStatus();
```

<span data-ttu-id="9e968-121">**Przykład:** [Przykładowa aplikacja konsoli](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="9e968-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="9e968-122">**Project:** SdkSamples, **klasa**: GetDirectSignedCustomerAgreementStatus.cs</span><span class="sxs-lookup"><span data-stu-id="9e968-122">**Project**: SdkSamples **Class**: GetDirectSignedCustomerAgreementStatus.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9e968-123">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="9e968-123">REST request</span></span>

<span data-ttu-id="9e968-124">Aby pobrać stan bezpośredniej akceptacji klienta dla klienta Umowa z Klientem Microsoft, utwórz żądanie REST w celu pobrania dla klienta stanu [DirectSignedCustomerAgreementStatus.](./customer-agreement-direct-sign-status-resource.md)</span><span class="sxs-lookup"><span data-stu-id="9e968-124">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, create a REST request to retrieve the [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) for the customer.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9e968-125">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="9e968-125">Request syntax</span></span>

<span data-ttu-id="9e968-126">Użyj następującej składni żądania:</span><span class="sxs-lookup"><span data-stu-id="9e968-126">Use the following request syntax:</span></span>

| <span data-ttu-id="9e968-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="9e968-127">Method</span></span> | <span data-ttu-id="9e968-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="9e968-128">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9e968-129">GET</span><span class="sxs-lookup"><span data-stu-id="9e968-129">GET</span></span>    | <span data-ttu-id="9e968-130">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9e968-130">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="9e968-131">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="9e968-131">URI parameters</span></span>

<span data-ttu-id="9e968-132">W żądaniu można użyć następujących parametrów URI:</span><span class="sxs-lookup"><span data-stu-id="9e968-132">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="9e968-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9e968-133">Name</span></span>             | <span data-ttu-id="9e968-134">Typ</span><span class="sxs-lookup"><span data-stu-id="9e968-134">Type</span></span> | <span data-ttu-id="9e968-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9e968-135">Required</span></span> | <span data-ttu-id="9e968-136">Opis</span><span class="sxs-lookup"><span data-stu-id="9e968-136">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="9e968-137">identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="9e968-137">customer-tenant-id</span></span> | <span data-ttu-id="9e968-138">GUID</span><span class="sxs-lookup"><span data-stu-id="9e968-138">GUID</span></span> | <span data-ttu-id="9e968-139">Tak</span><span class="sxs-lookup"><span data-stu-id="9e968-139">Yes</span></span> | <span data-ttu-id="9e968-140">Wartość jest identyfikatorem **CustomerTenantId** w formacie identyfikatora GUID, który umożliwia określenie identyfikatora dzierżawy klienta.</span><span class="sxs-lookup"><span data-stu-id="9e968-140">The value is a GUID-formatted **CustomerTenantId** that allows you to specify the tenant ID of a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9e968-141">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="9e968-141">Request headers</span></span>

<span data-ttu-id="9e968-142">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="9e968-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9e968-143">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="9e968-143">Request body</span></span>

<span data-ttu-id="9e968-144">Brak.</span><span class="sxs-lookup"><span data-stu-id="9e968-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9e968-145">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="9e968-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="9e968-146">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="9e968-146">REST response</span></span>

<span data-ttu-id="9e968-147">W przypadku powodzenia ta metoda zwraca [ **zasób DirectSignedCustomerAgreementStatus**](./customer-agreement-direct-sign-status-resource.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="9e968-147">If successful, this method returns a [**DirectSignedCustomerAgreementStatus** resource](./customer-agreement-direct-sign-status-resource.md) in the response body.</span></span>

<span data-ttu-id="9e968-148">Zasób ma właściwość **isSigned,** która wskazuje stan bezpośredniego podpisywania (akceptacji bezpośredniej) klienta.</span><span class="sxs-lookup"><span data-stu-id="9e968-148">The resource has an **isSigned** property that indicates the customer's direct signing (direct acceptance) status.</span></span>

- <span data-ttu-id="9e968-149">Wartość true **oznacza,** że umowa została podpisana (zaakceptowana) bezpośrednio przez klienta.</span><span class="sxs-lookup"><span data-stu-id="9e968-149">A value of **true** indicates that the agreement has been signed (accepted) directly by the customer.</span></span>

- <span data-ttu-id="9e968-150">Wartość false **oznacza,** że umowa *nie* została podpisana (zaakceptowana) bezpośrednio przez klienta.</span><span class="sxs-lookup"><span data-stu-id="9e968-150">A value of **false** indicates that the agreement has *not* been signed (accepted) directly by the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9e968-151">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9e968-151">Response success and error codes</span></span>

<span data-ttu-id="9e968-152">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="9e968-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="9e968-153">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="9e968-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9e968-154">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="9e968-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9e968-155">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9e968-155">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
