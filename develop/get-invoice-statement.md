---
title: Pobieranie zestawienia faktur
description: Pobiera zestawienie faktur przy użyciu identyfikatora faktury.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 42e5201919eea5644da463dfe2584c8d55002083
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767885"
---
# <a name="get-invoice-statement"></a><span data-ttu-id="5cf27-103">Pobieranie zestawienia faktur</span><span class="sxs-lookup"><span data-stu-id="5cf27-103">Get invoice statement</span></span>

<span data-ttu-id="5cf27-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="5cf27-104">**Applies To**</span></span>

- <span data-ttu-id="5cf27-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="5cf27-105">Partner Center</span></span>
- <span data-ttu-id="5cf27-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="5cf27-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="5cf27-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="5cf27-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="5cf27-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="5cf27-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5cf27-109">Pobiera zestawienie faktur przy użyciu identyfikatora faktury.</span><span class="sxs-lookup"><span data-stu-id="5cf27-109">Retrieves an invoice statement using the invoice ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5cf27-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5cf27-110">Prerequisites</span></span>

- <span data-ttu-id="5cf27-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5cf27-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5cf27-112">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5cf27-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="5cf27-113">Prawidłowy identyfikator faktury.</span><span class="sxs-lookup"><span data-stu-id="5cf27-113">A valid Invoice ID.</span></span>

## <a name="c"></a><span data-ttu-id="5cf27-114">C\#</span><span class="sxs-lookup"><span data-stu-id="5cf27-114">C\#</span></span>

<span data-ttu-id="5cf27-115">Aby uzyskać wyciąg z faktury według identyfikatora, Użyj kolekcji **IPartner.** Invoice i Wywołaj metodę **ById ()** przy użyciu identyfikatora faktury, a następnie wywołaj metody **Documents ()** i **Statement ()** , aby uzyskać dostęp do instrukcji Invoice.</span><span class="sxs-lookup"><span data-stu-id="5cf27-115">To get an invoice statement by ID, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Documents()** and **Statement()** methods to access the invoice statement.</span></span> <span data-ttu-id="5cf27-116">Na koniec wywołaj metody **Get ()** lub **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="5cf27-116">Finally, call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Documents.Statement.Get();
```

<span data-ttu-id="5cf27-117">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="5cf27-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5cf27-118">**Project**: PartnerSDK. FeatureSample **Klasa**: GetInvoiceStatement.cs</span><span class="sxs-lookup"><span data-stu-id="5cf27-118">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceStatement.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5cf27-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="5cf27-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5cf27-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="5cf27-120">Request syntax</span></span>

| <span data-ttu-id="5cf27-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="5cf27-121">Method</span></span>  | <span data-ttu-id="5cf27-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="5cf27-122">Request URI</span></span>                                                                                       |
|---------|---------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5cf27-123">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="5cf27-123">**GET**</span></span> | <span data-ttu-id="5cf27-124">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/Documents/Statement http/1.1</span><span class="sxs-lookup"><span data-stu-id="5cf27-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/documents/statement HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="5cf27-125">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="5cf27-125">URI parameter</span></span>

<span data-ttu-id="5cf27-126">Użyj następującego parametru zapytania, aby pobrać instrukcję faktury.</span><span class="sxs-lookup"><span data-stu-id="5cf27-126">Use the following query parameter to get the invoice statement.</span></span>

| <span data-ttu-id="5cf27-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="5cf27-127">Name</span></span>       | <span data-ttu-id="5cf27-128">Typ</span><span class="sxs-lookup"><span data-stu-id="5cf27-128">Type</span></span>       | <span data-ttu-id="5cf27-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="5cf27-129">Required</span></span> | <span data-ttu-id="5cf27-130">Opis</span><span class="sxs-lookup"><span data-stu-id="5cf27-130">Description</span></span>                                                                                        |
|------------|------------|----------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5cf27-131">Identyfikator faktury</span><span class="sxs-lookup"><span data-stu-id="5cf27-131">invoice-id</span></span> | <span data-ttu-id="5cf27-132">ciąg</span><span class="sxs-lookup"><span data-stu-id="5cf27-132">string</span></span>     | <span data-ttu-id="5cf27-133">Tak</span><span class="sxs-lookup"><span data-stu-id="5cf27-133">Yes</span></span>      | <span data-ttu-id="5cf27-134">Wartość jest identyfikatorem faktury, który umożliwia odsprzedawcy filtrowanie wyników dla danej faktury.</span><span class="sxs-lookup"><span data-stu-id="5cf27-134">The value is an invoice-id that allows the reseller to filter the results for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5cf27-135">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="5cf27-135">Request headers</span></span>

<span data-ttu-id="5cf27-136">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5cf27-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5cf27-137">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="5cf27-137">Request body</span></span>

<span data-ttu-id="5cf27-138">Brak</span><span class="sxs-lookup"><span data-stu-id="5cf27-138">None</span></span>

### <a name="request-example"></a><span data-ttu-id="5cf27-139">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="5cf27-139">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="5cf27-140">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="5cf27-140">REST response</span></span>

<span data-ttu-id="5cf27-141">Jeśli to się powiedzie, metoda zwraca zasób [InvoiceStatement](invoice-resources.md#invoicestatement) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="5cf27-141">If successful, this method returns an [InvoiceStatement](invoice-resources.md#invoicestatement) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5cf27-142">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="5cf27-142">Response success and error codes</span></span>

<span data-ttu-id="5cf27-143">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="5cf27-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5cf27-144">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="5cf27-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5cf27-145">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5cf27-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5cf27-146">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="5cf27-146">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 219753
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    _content    {System.Net.Http.ByteArrayContent}    System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[219753]}    byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=Invoice_G000024132.pdf}
}
```
