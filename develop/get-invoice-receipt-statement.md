---
title: Pobieranie potwierdzenia otrzymania faktury
description: Pobiera fakturę z potwierdzeniem przy użyciu identyfikatora faktury i identyfikatora potwierdzenia.
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ed47eadb377a94363b46cbc5508e5377cee005007698df9077d085705c7b9d08
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990736"
---
# <a name="get-invoice-receipt-statement"></a>Pobieranie potwierdzenia otrzymania faktury

Pobiera fakturę z potwierdzeniem przy użyciu identyfikatora faktury i identyfikatora potwierdzenia.

> [!IMPORTANT]
> Ta funkcja ma zastosowanie tylko do paragonów podatkowych w Chinach.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.

- Prawidłowy identyfikator faktury i odpowiedni identyfikator potwierdzenia.

## <a name="c"></a>C\#

Aby uzyskać zestawienie paragonu za pomocą identyfikatora, zaczynając od zestaw SDK Centrum partnerskiego w wersji 1.12.0, użyj kolekcji **IPartner.Invoices** i wywołaj metodę **ById()** przy użyciu identyfikatora faktury, a następnie wywołaj kolekcję **Receipts** i wywołaj metodę **ById(),** a następnie wywołaj metody **Documents()** i **Statement(),** aby uzyskać dostęp do zestawienia paragonu na fakturze. Na koniec wywołaj **metody Get()** **lub GetAsync().**

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** Klasa PartnerSDK.FeatureSample: GetInvoiceReceiptStatement.cs 

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/receipts/{receipt-id}/documents/statement HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby pobrać zestawienie paragonu faktury.

| Nazwa       | Typ   | Wymagane | Opis                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| invoice-id | ciąg | Tak      | Wartość to identyfikator faktury, który umożliwia odsprzedawcy filtrowanie wyników dla danej faktury. |
| identyfikator potwierdzenia | ciąg | Tak      | Wartość to identyfikator potwierdzenia, który umożliwia odsprzedawcy filtrowanie paragonów dla danej faktury. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

W przypadku powodzenia ta metoda zwraca strumień pdf w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

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
