---
title: Pobieranie potwierdzenia otrzymania faktury
description: Pobiera zestawienie paragonu faktury przy użyciu identyfikatora faktury i identyfikatora potwierdzenia.
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dcac4c8f0b881409dcad3560eefb82d4bb5e877a
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446133"
---
# <a name="get-invoice-receipt-statement"></a><span data-ttu-id="d6ee5-103">Pobieranie potwierdzenia otrzymania faktury</span><span class="sxs-lookup"><span data-stu-id="d6ee5-103">Get invoice receipt statement</span></span>

<span data-ttu-id="d6ee5-104">Pobiera zestawienie paragonu faktury przy użyciu identyfikatora faktury i identyfikatora potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="d6ee5-104">Retrieves an invoice receipt statement using invoice ID and the receipt ID.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6ee5-105">Ta funkcja ma zastosowanie tylko do tajwańskich paragonów podatkowych.</span><span class="sxs-lookup"><span data-stu-id="d6ee5-105">This feature is only applicable to Taiwan tax receipts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6ee5-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d6ee5-106">Prerequisites</span></span>

- <span data-ttu-id="d6ee5-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d6ee5-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d6ee5-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d6ee5-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="d6ee5-109">Prawidłowy identyfikator faktury i odpowiedni identyfikator potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="d6ee5-109">A valid Invoice ID and a corresponding receipt ID.</span></span>

## <a name="c"></a><span data-ttu-id="d6ee5-110">C\#</span><span class="sxs-lookup"><span data-stu-id="d6ee5-110">C\#</span></span>

<span data-ttu-id="d6ee5-111">Aby uzyskać zestawienie faktur według identyfikatora, począwszy od zestaw SDK Centrum partnerskiego v1.12.0, użyj kolekcji **IPartner.Invoices** i wywołaj metodę **ById()** przy użyciu identyfikatora faktury, a następnie wywołaj kolekcję **Receipts** i wywołaj metodę **ById(),** a następnie wywołaj metody **Documents()** i **Statement(),** aby uzyskać dostęp do zestawienia paragonu na fakturze.</span><span class="sxs-lookup"><span data-stu-id="d6ee5-111">To get an invoice receipt statement by ID, starting with Partner Center SDK v1.12.0, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Receipts** collection and call **ById()** then call the **Documents()** and **Statement()** methods to access the invoice receipt statement.</span></span> <span data-ttu-id="d6ee5-112">Na koniec wywołaj **metody Get()** **lub GetAsync().**</span><span class="sxs-lookup"><span data-stu-id="d6ee5-112">Finally, call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

<span data-ttu-id="d6ee5-113">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d6ee5-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d6ee5-114">**Project:** Klasa PartnerSDK.FeatureSample: GetInvoiceReceiptStatement.cs </span><span class="sxs-lookup"><span data-stu-id="d6ee5-114">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceReceiptStatement.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d6ee5-115">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="d6ee5-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d6ee5-116">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="d6ee5-116">Request syntax</span></span>

| <span data-ttu-id="d6ee5-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="d6ee5-117">Method</span></span>  | <span data-ttu-id="d6ee5-118">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="d6ee5-118">Request URI</span></span>                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d6ee5-119">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="d6ee5-119">**GET**</span></span> | <span data-ttu-id="d6ee5-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/receipts/{receipt-id}/documents/statement HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d6ee5-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/receipts/{receipt-id}/documents/statement HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d6ee5-121">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="d6ee5-121">URI parameter</span></span>

<span data-ttu-id="d6ee5-122">Użyj następującego parametru zapytania, aby uzyskać zestawienie faktur.</span><span class="sxs-lookup"><span data-stu-id="d6ee5-122">Use the following query parameter to get the invoice receipt statement.</span></span>

| <span data-ttu-id="d6ee5-123">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d6ee5-123">Name</span></span>       | <span data-ttu-id="d6ee5-124">Typ</span><span class="sxs-lookup"><span data-stu-id="d6ee5-124">Type</span></span>   | <span data-ttu-id="d6ee5-125">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6ee5-125">Required</span></span> | <span data-ttu-id="d6ee5-126">Opis</span><span class="sxs-lookup"><span data-stu-id="d6ee5-126">Description</span></span>                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d6ee5-127">identyfikator faktury</span><span class="sxs-lookup"><span data-stu-id="d6ee5-127">invoice-id</span></span> | <span data-ttu-id="d6ee5-128">ciąg</span><span class="sxs-lookup"><span data-stu-id="d6ee5-128">string</span></span> | <span data-ttu-id="d6ee5-129">Tak</span><span class="sxs-lookup"><span data-stu-id="d6ee5-129">Yes</span></span>      | <span data-ttu-id="d6ee5-130">Wartość to identyfikator faktury, który umożliwia odsprzedawcy filtrowanie wyników dla danej faktury.</span><span class="sxs-lookup"><span data-stu-id="d6ee5-130">The value is an invoice-id that allows the reseller to filter the results for a given invoice.</span></span> |
| <span data-ttu-id="d6ee5-131">identyfikator potwierdzenia</span><span class="sxs-lookup"><span data-stu-id="d6ee5-131">receipt-id</span></span> | <span data-ttu-id="d6ee5-132">ciąg</span><span class="sxs-lookup"><span data-stu-id="d6ee5-132">string</span></span> | <span data-ttu-id="d6ee5-133">Tak</span><span class="sxs-lookup"><span data-stu-id="d6ee5-133">Yes</span></span>      | <span data-ttu-id="d6ee5-134">Wartość to identyfikator paragonu, który umożliwia odsprzedawcy filtrowanie paragonów dla danej faktury.</span><span class="sxs-lookup"><span data-stu-id="d6ee5-134">The value is a receipt-id that allows the reseller to filter the receipts for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d6ee5-135">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="d6ee5-135">Request headers</span></span>

<span data-ttu-id="d6ee5-136">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d6ee5-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d6ee5-137">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="d6ee5-137">Request body</span></span>

<span data-ttu-id="d6ee5-138">Brak</span><span class="sxs-lookup"><span data-stu-id="d6ee5-138">None</span></span>

### <a name="request-example"></a><span data-ttu-id="d6ee5-139">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="d6ee5-139">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="d6ee5-140">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="d6ee5-140">REST response</span></span>

<span data-ttu-id="d6ee5-141">W przypadku powodzenia ta metoda zwraca strumień pdf w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d6ee5-141">If successful, this method returns a pdf stream in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d6ee5-142">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d6ee5-142">Response success and error codes</span></span>

<span data-ttu-id="d6ee5-143">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="d6ee5-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d6ee5-144">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="d6ee5-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d6ee5-145">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d6ee5-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d6ee5-146">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d6ee5-146">Response example</span></span>

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
