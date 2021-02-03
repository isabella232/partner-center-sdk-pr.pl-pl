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
# <a name="get-invoice-receipt-statement"></a>Pobieranie potwierdzenia otrzymania faktury

**Dotyczy**

- Centrum partnerskie

Pobiera instrukcję paragonu faktury przy użyciu identyfikatora faktury i identyfikatora paragonu.

> [!IMPORTANT]
> Ta funkcja ma zastosowanie tylko do tajwańskich przyjęć podatkowych.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Prawidłowy identyfikator faktury i odpowiedni identyfikator paragonu.

## <a name="c"></a>C\#

Aby uzyskać wyciąg z faktury paragonu według identyfikatora, rozpoczynając od zestawu SDK programu partnerskiego 1.12.0, Użyj kolekcji **IPartner.** Invoice i Wywołaj metodę **ById ()** przy użyciu identyfikatora faktury, a następnie Wywołaj kolekcję **potwierdzenia** i Wywołaj **ById ()** , a następnie wywołaj metody **Documents ()** i **Statement ()** , aby uzyskać dostęp do instrukcji odbioru faktury. Na koniec wywołaj metody **Get ()** lub **GetAsync ()** .

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Project**: PartnerSDK. FeatureSample **Klasa**: GetInvoiceReceiptStatement.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/Receipts/{receipt-ID}/Documents/Statement http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby pobrać instrukcję paragonu faktury.

| Nazwa       | Typ   | Wymagane | Opis                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| Identyfikator faktury | ciąg | Tak      | Wartość jest identyfikatorem faktury, który umożliwia odsprzedawcy filtrowanie wyników dla danej faktury. |
| Identyfikator paragonu | ciąg | Tak      | Wartość jest identyfikatorem paragonu, który umożliwia odsprzedawcy odfiltrowanie paragonów dla danej faktury. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, metoda zwraca strumień PDF w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

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
