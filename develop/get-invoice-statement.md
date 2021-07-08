---
title: Pobieranie zestawienia faktur
description: Pobiera zestawienie faktur przy użyciu identyfikatora faktury.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: f0324916eb2efd9244530a53b1d7bb4abc0c8e6e
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549131"
---
# <a name="get-invoice-statement"></a><span data-ttu-id="91602-103">Pobieranie zestawienia faktur</span><span class="sxs-lookup"><span data-stu-id="91602-103">Get invoice statement</span></span>

<span data-ttu-id="91602-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="91602-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91602-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="91602-105">Prerequisites</span></span>

- <span data-ttu-id="91602-106">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="91602-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="91602-107">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="91602-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="91602-108">Prawidłowy identyfikator faktury.</span><span class="sxs-lookup"><span data-stu-id="91602-108">A valid Invoice ID.</span></span>

## <a name="c"></a><span data-ttu-id="91602-109">C\#</span><span class="sxs-lookup"><span data-stu-id="91602-109">C\#</span></span>

<span data-ttu-id="91602-110">Aby uzyskać zestawienie faktur według identyfikatora, użyj kolekcji **IPartner.Invoices** i wywołaj metodę **ById()** przy użyciu identyfikatora faktury, a następnie wywołaj metody **Documents()** i **Statement(),** aby uzyskać dostęp do zestawienia faktur.</span><span class="sxs-lookup"><span data-stu-id="91602-110">To get an invoice statement by ID, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Documents()** and **Statement()** methods to access the invoice statement.</span></span> <span data-ttu-id="91602-111">Na koniec wywołaj **metody Get()** **lub GetAsync().**</span><span class="sxs-lookup"><span data-stu-id="91602-111">Finally, call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Documents.Statement.Get();
```

<span data-ttu-id="91602-112">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="91602-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="91602-113">**Project:** Klasa PartnerSDK.FeatureSample: GetInvoiceStatement.cs </span><span class="sxs-lookup"><span data-stu-id="91602-113">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceStatement.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="91602-114">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="91602-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="91602-115">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="91602-115">Request syntax</span></span>

| <span data-ttu-id="91602-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="91602-116">Method</span></span>  | <span data-ttu-id="91602-117">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="91602-117">Request URI</span></span>                                                                                       |
|---------|---------------------------------------------------------------------------------------------------|
| <span data-ttu-id="91602-118">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="91602-118">**GET**</span></span> | <span data-ttu-id="91602-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/documents/statement HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="91602-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/documents/statement HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="91602-120">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="91602-120">URI parameter</span></span>

<span data-ttu-id="91602-121">Użyj następującego parametru zapytania, aby pobrać zestawienie faktur.</span><span class="sxs-lookup"><span data-stu-id="91602-121">Use the following query parameter to get the invoice statement.</span></span>

| <span data-ttu-id="91602-122">Nazwa</span><span class="sxs-lookup"><span data-stu-id="91602-122">Name</span></span>       | <span data-ttu-id="91602-123">Typ</span><span class="sxs-lookup"><span data-stu-id="91602-123">Type</span></span>       | <span data-ttu-id="91602-124">Wymagane</span><span class="sxs-lookup"><span data-stu-id="91602-124">Required</span></span> | <span data-ttu-id="91602-125">Opis</span><span class="sxs-lookup"><span data-stu-id="91602-125">Description</span></span>                                                                                        |
|------------|------------|----------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="91602-126">invoice-id</span><span class="sxs-lookup"><span data-stu-id="91602-126">invoice-id</span></span> | <span data-ttu-id="91602-127">ciąg</span><span class="sxs-lookup"><span data-stu-id="91602-127">string</span></span>     | <span data-ttu-id="91602-128">Tak</span><span class="sxs-lookup"><span data-stu-id="91602-128">Yes</span></span>      | <span data-ttu-id="91602-129">Wartość to identyfikator faktury, który umożliwia odsprzedawcy filtrowanie wyników dla danej faktury.</span><span class="sxs-lookup"><span data-stu-id="91602-129">The value is an invoice-id that allows the reseller to filter the results for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="91602-130">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="91602-130">Request headers</span></span>

<span data-ttu-id="91602-131">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="91602-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="91602-132">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="91602-132">Request body</span></span>

<span data-ttu-id="91602-133">Brak</span><span class="sxs-lookup"><span data-stu-id="91602-133">None</span></span>

### <a name="request-example"></a><span data-ttu-id="91602-134">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="91602-134">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="91602-135">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="91602-135">REST response</span></span>

<span data-ttu-id="91602-136">W przypadku powodzenia ta metoda zwraca [zasób InvoiceStatement](invoice-resources.md#invoicestatement) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="91602-136">If successful, this method returns an [InvoiceStatement](invoice-resources.md#invoicestatement) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="91602-137">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="91602-137">Response success and error codes</span></span>

<span data-ttu-id="91602-138">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="91602-138">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="91602-139">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="91602-139">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="91602-140">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="91602-140">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="91602-141">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="91602-141">Response example</span></span>

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
