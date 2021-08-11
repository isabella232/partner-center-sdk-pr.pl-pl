---
title: Usuwanie odsprzedawcy pośredniego w piaskownicy
description: Zawiera informacje na temat usuwania odsprzedawców pośrednich piaskownicy i włączania testowania end-to-end przy użyciu interfejsów API.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 708fedd4e34b2242aae6e6e0ac673ce77524d448dcee4a05877d37b5266e44c8
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994935"
---
# <a name="delete-indirect-reseller-in-sandbox"></a>Usuwanie odsprzedawcy pośredniego w piaskownicy

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany

W tym dokumencie przedstawiono sposób usuwania dostawców pośrednich piaskownicy i włączania testowania end-to-end przy użyciu interfejsów API.

> [!Important]
> W tym dokumencie opisano funkcje, które są dozwolone tylko w środowisku piaskownicy dla środowisk modelu pośredniego.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.

## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller"></a>Dostawca pośredni piaskownicy — usuwanie odsprzedawcy pośredniego piaskownicy 

Ta funkcja jest dostępna tylko w piaskownicy i umożliwia dostawcom pośrednim piaskownicy tworzenie odsprzedawców pośrednich piaskownicy.

1. Wymagania wstępne dotyczące usuwania odsprzedawcy pośredniego piaskownicy
    1. Wstrzymywanie subskrypcji dla każdego klienta odsprzedawcy pośredniego piaskownicy
    2. Usuwanie wszystkich klientów odsprzedawcy pośredniego
2. Dozwolony limit pięciu odsprzedawców pośrednich piaskownicy na dostawcę pośredniego piaskownicy. Po usunięciu odsprzedawcy pośredniego piaskownicy limit przydziału zostanie zresetowany.

## <a name="delete-sandbox-indirect-reseller-through-api"></a>Usuwanie odsprzedawcy pośredniego piaskownicy za pośrednictwem interfejsu API

### <a name="rest-request"></a>Żądanie REST

#### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania                                                                             |
|------------|-------------------------------------------------------------------------------------|
| **Usunąć** | [*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller/{resellerId} |

#### <a name="request-headers"></a>Nagłówki żądań

- Ten interfejs API jest idempotentny (nie da innego wyniku, jeśli wywołasz go wiele razy)
- Wymagany jest identyfikator żądania i identyfikator korelacji
- Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST)](headers.md)

### <a name="request-example"></a>Przykład żądania

Usunąć https://api.partnercenter.microsoft.com/v1/sandboxIndirectReseller/{resellerID}

```http
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

####  <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Feb 2021 00:43:02 GMT
```

#### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz inne informacje debugowania. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).

Ta metoda zwraca następujące kody błędów i powodzenia stanu:

| Kod stanu HTTP                     | Kod błędu     | Opis                                      |
|--------------------------------------|----------------|--------------------------------------------------|
| 401                                  | 6002           | Nieautoryzowany token lub konto dostawcy porad |
| 403                                  | 6003           | Usuwanie środowiska IR piaskownicy jest niedozwolone                 |
| 403                                  | 6004           | Tworzenie operacji środowiska IR piaskownicy jest niedozwolone          |
| 409                                  | 1003           | Konflikt podczas tworzenia dzierżawy                   |
