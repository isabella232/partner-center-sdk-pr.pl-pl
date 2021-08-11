---
title: Nagłówki REST Centrum partnerskiego
description: Dowiedz się więcej o nagłówkach żądań REST protokołu HTTP i nagłówkach odpowiedzi REST obsługiwanych przez interfejs API REST Partner Center REST.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9c9483e761465be1a60003dcd44cef46af3e99634d99d804d43d101d6b8ef700
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993825"
---
# <a name="partner-center-rest-and-response-headers-supported-by-the-partner-center-rest-api"></a>Partner Center REST i nagłówki odpowiedzi obsługiwane przez interfejs API REST usługi Partner Center 

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Następujące nagłówki żądań i odpowiedzi HTTP są obsługiwane przez interfejs API REST Partner Center HTTP. Nie wszystkie wywołania interfejsu API akceptują wszystkie nagłówki.

## <a name="rest-request-headers"></a>Nagłówki żądań REST

Następujące nagłówki żądań HTTP są obsługiwane przez interfejs API REST Partner Center HTTP.

| Nagłówek                       | Opis                                                                                                                                                                                                                                                                            | Typ wartości |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Authorization:               | Wymagane. Token autoryzacji w postaci tokenu bearer &lt; &gt; .                                                                                                                                                                                                                    | ciąg     |
| Zaakceptować:                      | Określa typ żądania i odpowiedzi "application/json".                                                                                                                                                                                                                           | ciąg     |
| MS-RequestId:                | Unikatowy identyfikator wywołania, używany w celu zapewnienia id-identyfikatorów. Jeśli istnieje limit czasu, wywołanie ponawiania powinno zawierać tę samą wartość. Po otrzymaniu odpowiedzi (powodzenie lub niepowodzenie biznesowe) wartość powinna zostać zresetowana na potrzeby następnego wywołania.                                            | GUID       |
| MS-CorrelationId:            | Unikatowy identyfikator wywołania, przydatny w dziennikach i śladach sieci na potrzeby rozwiązywania problemów z błędami. Wartość powinna zostać zresetowana dla każdego wywołania. Wszystkie operacje powinny zawierać ten nagłówek. Aby uzyskać więcej informacji, zobacz informacje o identyfikatorze korelacji w [teście i debugowaniu](test-and-debug.md). | GUID       |
| MS-Contract-Version:         | Wymagane. Określa wersję żądanego interfejsu API; ogólnie wersja interfejsu API: wersja 1, chyba że określono inaczej w [sekcji Scenariusze.](scenarios.md)                                                                                                                                  | ciąg     |
| If-Match:                    | Służy do kontroli współbieżności. Niektóre wywołania interfejsu API wymagają przekazywania tagu ETag za pośrednictwem If-Match nagłówka. Tag ETag jest zwykle w zasobie i dlatego wymaga get-ting najnowsze. Aby uzyskać więcej informacji, zobacz informacje o tagu ETag w [teście i debugowaniu](test-and-debug.md).                | ciąg     |
| MS-PartnerCenter-Application | Opcjonalny. Określa nazwę aplikacji, która korzysta z interfejsu API REST Partner Center.                                                                                                                                                                                             | ciąg     |
| X-Locale(X-Locale):                    | Opcjonalny. Określa język, w którym są zwracane stawki. Wartość domyślna to "en-US". Aby uzyskać listę obsługiwanych wartości, zobacz [Partner Center obsługiwanych języków i danych regionalnych.](partner-center-supported-languages-and-locales.md)                                                                                                                                                                                                  | ciąg     |

## <a name="rest-response-headers"></a>Nagłówki odpowiedzi REST

Następujące nagłówki odpowiedzi HTTP mogą być zwracane przez interfejs API REST Partner Center HTTP.

| Nagłówek            | Opis                                                                                                                                                                                                                                 | Typ wartości |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Zaakceptować:           | Określa typ żądania i odpowiedzi "application/json".                                                                                                                                                                                | ciąg     |
| MS-RequestId:     | Unikatowy identyfikator wywołania, używany w celu zapewnienia id-identyfikatorów. Jeśli istnieje limit czasu, wywołanie ponawiania powinno zawierać tę samą wartość. Po otrzymaniu odpowiedzi (powodzenie lub niepowodzenie biznesowe) wartość powinna zostać zresetowana na potrzeby następnego wywołania. | GUID       |
| MS-CorrelationId: | Unikatowy identyfikator wywołania. Ta wartość jest przydatna do rozwiązywania problemów z dziennikami i śladami sieci w celu znalezienia błędu. Wartość powinna zostać zresetowana dla każdego wywołania. Wszystkie operacje powinny zawierać ten nagłówek.                                                       | GUID       |
