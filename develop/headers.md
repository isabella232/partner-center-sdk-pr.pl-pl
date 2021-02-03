---
title: Nagłówki REST Centrum partnerskiego
description: Dowiedz się więcej na temat nagłówków żądań REST protokołu HTTP i nagłówków odpowiedzi REST obsługiwanych przez interfejs API REST Centrum partnerskiego.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9f506c8c610c2584912c24453288d0f3578b84e3
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/11/2020
ms.locfileid: "97768510"
---
# <a name="partner-center-rest-and-response-headers-supported-by-the-partner-center-rest-api"></a>Nagłówki REST i odpowiedzi Centrum partnerskiego obsługiwane przez interfejs API REST Centrum partnerskiego 

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Następujące nagłówki żądania HTTP i odpowiedzi są obsługiwane przez interfejs API REST Centrum partnerskiego. Nie wszystkie wywołania interfejsu API akceptują wszystkie nagłówki.

## <a name="rest-request-headers"></a>Nagłówki żądań REST

Następujące nagłówki żądania HTTP są obsługiwane przez interfejs API REST Centrum partnerskiego.

| Nagłówek                       | Opis                                                                                                                                                                                                                                                                            | Typ wartości |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Authorization:               | Wymagane. Token autoryzacji w postaci &lt; tokenu okaziciela &gt; .                                                                                                                                                                                                                    | ciąg     |
| Odebrać                      | Określa typ żądania i odpowiedzi "Application/JSON".                                                                                                                                                                                                                           | ciąg     |
| MS-identyfikator żądania:                | Unikatowy identyfikator wywołania, używany do zapewnienia działania dotyczącego identyfikatora. Jeśli wystąpiło przekroczenie limitu czasu, wywołanie ponawiania powinno zawierać tę samą wartość. Po odebraniu odpowiedzi (sukces lub błąd biznesowy) należy zresetować wartość dla następnego wywołania.                                            | GUID       |
| MS-identyfikator korelacji:            | Unikatowy identyfikator wywołania, przydatny w dziennikach i śladach sieci do rozwiązywania problemów z błędami. Wartość powinna być resetowana dla każdego wywołania. Wszystkie operacje powinny zawierać ten nagłówek. Aby uzyskać więcej informacji, zobacz informacje o IDENTYFIKATORze korelacji w [teście i debugowaniu](test-and-debug.md). | GUID       |
| MS-Contract-Version:         | Wymagane. Określa wersję żądanego interfejsu API; Ogólnie wersja interfejsu API: V1, o ile nie określono inaczej w sekcji [scenariusze](scenarios.md) .                                                                                                                                  | ciąg     |
| If-Match:                    | Używany na potrzeby kontroli współbieżności. Niektóre wywołania interfejsu API wymagają przekazania elementu ETag za pośrednictwem nagłówka If-Match. Element ETag zazwyczaj znajduje się w zasobie i w związku z tym wymaga pobrania najnowszych. Aby uzyskać więcej informacji, zobacz informacje ETag w artykule [Test and Debug](test-and-debug.md).                | ciąg     |
| MS-PartnerCenter — aplikacja | Opcjonalny. Określa nazwę aplikacji korzystającej z interfejsu API REST Centrum partnerskiego.                                                                                                                                                                                             | ciąg     |
| X — ustawienia regionalne:                    | Opcjonalny. Określa język, w którym są zwracane stawki. Wartość domyślna to "pl-US". Aby uzyskać listę obsługiwanych wartości, zobacz [obsługiwane języki i ustawienia regionalne usługi Partner Center](partner-center-supported-languages-and-locales.md).                                                                                                                                                                                                  | ciąg     |

## <a name="rest-response-headers"></a>Nagłówki odpowiedzi REST

Interfejs API REST Centrum partnerskiego może zwrócić następujące nagłówki odpowiedzi HTTP.

| Nagłówek            | Opis                                                                                                                                                                                                                                 | Typ wartości |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Odebrać           | Określa typ żądania i odpowiedzi "Application/JSON".                                                                                                                                                                                | ciąg     |
| MS-identyfikator żądania:     | Unikatowy identyfikator wywołania, używany do zapewnienia działania dotyczącego identyfikatora. Jeśli wystąpiło przekroczenie limitu czasu, wywołanie ponawiania powinno zawierać tę samą wartość. Po odebraniu odpowiedzi (sukces lub błąd biznesowy) należy zresetować wartość dla następnego wywołania. | GUID       |
| MS-identyfikator korelacji: | Unikatowy identyfikator wywołania. Ta wartość jest przydatna do rozwiązywania problemów z dziennikami i śladami sieci w celu znalezienia błędu. Wartość powinna być resetowana dla każdego wywołania. Wszystkie operacje powinny zawierać ten nagłówek.                                                       | GUID       |
