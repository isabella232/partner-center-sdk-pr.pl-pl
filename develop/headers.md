---
title: Nagłówki REST Centrum partnerskiego
description: Dowiedz się więcej na temat nagłówków żądań REST protokołu HTTP i nagłówków odpowiedzi REST obsługiwanych przez Partner Center API REST.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3f09ab5808a9751f02e451da2027f6b35877390b
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548468"
---
# <a name="partner-center-rest-and-response-headers-supported-by-the-partner-center-rest-api"></a>Partner Center REST i nagłówki odpowiedzi obsługiwane przez interfejs API REST Partner Center api 

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Następujące nagłówki żądań i odpowiedzi HTTP są obsługiwane przez interfejs API REST Partner Center HTTP. Nie wszystkie wywołania interfejsu API akceptują wszystkie nagłówki.

## <a name="rest-request-headers"></a>Nagłówki żądań REST

Następujące nagłówki żądań HTTP są obsługiwane przez interfejs API REST Partner Center HTTP.

| Nagłówek                       | Opis                                                                                                                                                                                                                                                                            | Typ wartości |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Authorization:               | Wymagane. Token autoryzacji w postaci tokenu bearer &lt; &gt; .                                                                                                                                                                                                                    | ciąg     |
| Zaakceptować:                      | Określa typ żądania i odpowiedzi "application/json".                                                                                                                                                                                                                           | ciąg     |
| MS-RequestId:                | Unikatowy identyfikator wywołania, używany w celu zapewnienia id-identyfikator. Jeśli istnieje limit czasu, wywołanie ponawiania powinno zawierać tę samą wartość. Po otrzymaniu odpowiedzi (powodzenie lub niepowodzenie biznesowe) wartość powinna zostać zresetowana na potrzeby następnego wywołania.                                            | GUID       |
| MS-CorrelationId:            | Unikatowy identyfikator wywołania, przydatny w dziennikach i śladach sieci na potrzeby rozwiązywania problemów z błędami. Wartość powinna zostać zresetowana dla każdego wywołania. Wszystkie operacje powinny zawierać ten nagłówek. Aby uzyskać więcej informacji, zobacz informacje o identyfikatorze korelacji w [teście i debugowaniu](test-and-debug.md). | GUID       |
| MS-Contract-Version:         | Wymagane. Określa wersję żądanego interfejsu API; ogólnie wersja interfejsu API: wersja 1, chyba że określono inaczej w [sekcji Scenariusze.](scenarios.md)                                                                                                                                  | ciąg     |
| If-Match:                    | Służy do kontroli współbieżności. Niektóre wywołania interfejsu API wymagają przekazywania tagu ETag za pośrednictwem If-Match nagłówka. Tag ETag zwykle znajduje się w zasobie i dlatego wymaga get-ting najnowszej wersji. Aby uzyskać więcej informacji, zobacz informacje dotyczące tagów ETag w [teście i debugowaniu](test-and-debug.md).                | ciąg     |
| MS-PartnerCenter-Application | Opcjonalny. Określa nazwę aplikacji korzystającej z interfejsu API PARTNER CENTER REST.                                                                                                                                                                                             | ciąg     |
| X-Locale:                    | Opcjonalny. Określa język, w którym są zwracane stawki. Wartość domyślna to "en-US". Aby uzyskać listę obsługiwanych wartości, zobacz [Partner Center obsługiwanych języków i danych regionalnych.](partner-center-supported-languages-and-locales.md)                                                                                                                                                                                                  | ciąg     |

## <a name="rest-response-headers"></a>Nagłówki odpowiedzi REST

Następujące nagłówki odpowiedzi HTTP mogą być zwracane przez interfejs API PARTNER CENTER REST.

| Nagłówek            | Opis                                                                                                                                                                                                                                 | Typ wartości |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Zaakceptować:           | Określa typ żądania i odpowiedzi "application/json".                                                                                                                                                                                | ciąg     |
| MS-RequestId:     | Unikatowy identyfikator wywołania, używany w celu zapewnienia id-identyfikator. Jeśli istnieje limit czasu, wywołanie ponawiania powinno zawierać tę samą wartość. Po otrzymaniu odpowiedzi (powodzenie lub niepowodzenie biznesowe) wartość powinna zostać zresetowana na potrzeby następnego wywołania. | GUID       |
| MS-CorrelationId: | Unikatowy identyfikator wywołania. Ta wartość jest przydatna do rozwiązywania problemów z dziennikami i śladami sieci w celu znalezienia błędu. Wartość powinna zostać zresetowana dla każdego wywołania. Wszystkie operacje powinny zawierać ten nagłówek.                                                       | GUID       |
