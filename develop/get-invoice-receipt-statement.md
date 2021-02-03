---
title: Pobieranie potwierdzenia otrzymania faktury
description: Pobiera instrukcję paragonu faktury przy użyciu identyfikatora faktury i identyfikatora paragonu.
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 96cef11d6778de2d9bf28e466d88a39f9415727d
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767682"
---
# <a name="get-invoice-receipt-statement"></a><span data-ttu-id="b3d41-103">Pobieranie potwierdzenia otrzymania faktury</span><span class="sxs-lookup"><span data-stu-id="b3d41-103">Get invoice receipt statement</span></span>

<span data-ttu-id="b3d41-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="b3d41-104">**Applies To**</span></span>

- <span data-ttu-id="b3d41-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="b3d41-105">Partner Center</span></span>

<span data-ttu-id="b3d41-106">Pobiera instrukcję paragonu faktury przy użyciu identyfikatora faktury i identyfikatora paragonu.</span><span class="sxs-lookup"><span data-stu-id="b3d41-106">Retrieves an invoice receipt statement using invoice ID and the receipt ID.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3d41-107">Ta funkcja ma zastosowanie tylko do tajwańskich przyjęć podatkowych.</span><span class="sxs-lookup"><span data-stu-id="b3d41-107">This feature is only applicable to Taiwan tax receipts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3d41-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b3d41-108">Prerequisites</span></span>

- <span data-ttu-id="b3d41-109">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b3d41-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b3d41-110">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b3d41-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b3d41-111">Prawidłowy identyfikator faktury i odpowiedni identyfikator paragonu.</span><span class="sxs-lookup"><span data-stu-id="b3d41-111">A valid Invoice ID and a corresponding receipt ID.</span></span>

## <a name="c"></a><span data-ttu-id="b3d41-112">C\#</span><span class="sxs-lookup"><span data-stu-id="b3d41-112">C\#</span></span>

<span data-ttu-id="b3d41-113">Aby uzyskać wyciąg z faktury paragonu według identyfikatora, rozpoczynając od zestawu SDK programu partnerskiego 1.12.0, Użyj kolekcji **IPartner.** Invoice i Wywołaj metodę **ById ()** przy użyciu identyfikatora faktury, a następnie Wywołaj kolekcję **potwierdzenia** i Wywołaj **ById ()** , a następnie wywołaj metody **Documents ()** i **Statement ()** , aby uzyskać dostęp do instrukcji odbioru faktury.</span><span class="sxs-lookup"><span data-stu-id="b3d41-113">To get an invoice receipt statement by ID, starting with Partner Center SDK v1.12.0, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Receipts** collection and call **ById()** then call the **Documents()** and **Statement()** methods to access the invoice receipt statement.</span></span> <span data-ttu-id="b3d41-114">Na koniec wywołaj metody **Get ()** lub **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="b3d41-114">Finally, call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

<span data-ttu-id="b3d41-115">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b3d41-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b3d41-116">**Project**: PartnerSDK. FeatureSample **Klasa**: GetInvoiceReceiptStatement.cs</span><span class="sxs-lookup"><span data-stu-id="b3d41-116">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceReceiptStatement.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b3d41-117">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="b3d41-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b3d41-118">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="b3d41-118">Request syntax</span></span>

| <span data-ttu-id="b3d41-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="b3d41-119">Method</span></span>  | <span data-ttu-id="b3d41-120">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="b3d41-120">Request URI</span></span>                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b3d41-121">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="b3d41-121">**GET**</span></span> | <span data-ttu-id="b3d41-122">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/Receipts/{receipt-ID}/Documents/Statement http/1.1</span><span class="sxs-lookup"><span data-stu-id="b3d41-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/receipts/{receipt-id}/documents/statement HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b3d41-123">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="b3d41-123">URI parameter</span></span>

<span data-ttu-id="b3d41-124">Użyj następującego parametru zapytania, aby pobrać instrukcję paragonu faktury.</span><span class="sxs-lookup"><span data-stu-id="b3d41-124">Use the following query parameter to get the invoice receipt statement.</span></span>

| <span data-ttu-id="b3d41-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b3d41-125">Name</span></span>       | <span data-ttu-id="b3d41-126">Typ</span><span class="sxs-lookup"><span data-stu-id="b3d41-126">Type</span></span>   | <span data-ttu-id="b3d41-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b3d41-127">Required</span></span> | <span data-ttu-id="b3d41-128">Opis</span><span class="sxs-lookup"><span data-stu-id="b3d41-128">Description</span></span>                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b3d41-129">Identyfikator faktury</span><span class="sxs-lookup"><span data-stu-id="b3d41-129">invoice-id</span></span> | <span data-ttu-id="b3d41-130">ciąg</span><span class="sxs-lookup"><span data-stu-id="b3d41-130">string</span></span> | <span data-ttu-id="b3d41-131">Tak</span><span class="sxs-lookup"><span data-stu-id="b3d41-131">Yes</span></span>      | <span data-ttu-id="b3d41-132">Wartość jest identyfikatorem faktury, który umożliwia odsprzedawcy filtrowanie wyników dla danej faktury.</span><span class="sxs-lookup"><span data-stu-id="b3d41-132">The value is an invoice-id that allows the reseller to filter the results for a given invoice.</span></span> |
| <span data-ttu-id="b3d41-133">Identyfikator paragonu</span><span class="sxs-lookup"><span data-stu-id="b3d41-133">receipt-id</span></span> | <span data-ttu-id="b3d41-134">ciąg</span><span class="sxs-lookup"><span data-stu-id="b3d41-134">string</span></span> | <span data-ttu-id="b3d41-135">Tak</span><span class="sxs-lookup"><span data-stu-id="b3d41-135">Yes</span></span>      | <span data-ttu-id="b3d41-136">Wartość jest identyfikatorem paragonu, który umożliwia odsprzedawcy odfiltrowanie paragonów dla danej faktury.</span><span class="sxs-lookup"><span data-stu-id="b3d41-136">The value is a receipt-id that allows the reseller to filter the receipts for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b3d41-137">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="b3d41-137">Request headers</span></span>

<span data-ttu-id="b3d41-138">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b3d41-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b3d41-139">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="b3d41-139">Request body</span></span>

<span data-ttu-id="b3d41-140">Brak</span><span class="sxs-lookup"><span data-stu-id="b3d41-140">None</span></span>

### <a name="request-example"></a><span data-ttu-id="b3d41-141">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="b3d41-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="b3d41-142">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="b3d41-142">REST response</span></span>

<span data-ttu-id="b3d41-143">Jeśli to się powiedzie, metoda zwraca strumień PDF w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="b3d41-143">If successful, this method returns a pdf stream in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b3d41-144">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b3d41-144">Response success and error codes</span></span>

<span data-ttu-id="b3d41-145">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="b3d41-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b3d41-146">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="b3d41-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b3d41-147">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b3d41-147">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b3d41-148">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b3d41-148">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 195556
Content-Type: application/pdf
MS-CorrelationId: a1d6ab41-5a30-4643-898b-b30d65d3a0a1
MS-RequestId: cc1ba6db-ab26-404a-9196-712b6395f518
Date: Tue, 05 Feb 2019 04:08:23 GMT

{
    _content    {System.Net.Http.ByteArrayContent}    System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[195556]}    byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=E-Tax-8602768.pdf}
}
```
