---
title: Dokumentacja interfejsu API REST Centrum partnerskiego
description: Dowiedz się, w jaki sposób partnerzy CSP mogą używać interfejsów API REST Centrum partnerskiego do integrowania oprogramowania CRM i rozliczeń z systemami firmy Microsoft w celu lepszego zarządzania kontami klientów
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 3f83b2b73c3480f76646cae4fcbbcbacd31d4b3f
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/11/2020
ms.locfileid: "97768502"
---
# <a name="partner-center-rest-api-reference-to-rest-urls-rest-headers-rest-resources-and-rest-events"></a>Dokumentacja interfejsu API REST Centrum partnerskiego do adresów URL REST, nagłówków REST, zasobów REST i zdarzeń REST

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

## <a name="partner-center-rest-api"></a>Interfejs API REST Centrum partnerskiego

Interfejs API REST Centrum partnerskiego pomaga partnerom dostawcy rozwiązań w chmurze zintegrować swoje istniejące oprogramowanie CRM lub rozliczeń z systemami firmy Microsoft, które zarządzają kontami klientów, umieszczają zamówienia, zarządzają subskrypcjami i obsługują żądania pomocy technicznej.

Aby uzyskać więcej informacji o tym, co może zrobić interfejs API, w tym przykładowy kod, zobacz temat [scenariusze](scenarios.md) , w tym omówienie w tle.

Przed rozpoczęciem kodowania zapoznaj się [z tematem wprowadzenie.](get-started.md) Ten artykuł zawiera informacje na temat konfigurowania kont testowych i produkcyjnych, uzyskiwania informacji o działaniu uwierzytelniania i znajdowania przykładowego kodu.

## <a name="topics"></a>Tematy

| Temat | Opis |
| ----- | ----------- |
| [Adresy URL REST Centrum partnerskiego](partner-center-rest-urls.md) | Definiuje punkty końcowe interfejsu API REST dla różnych wersji Centrum partnerskiego. |
| [Nagłówki REST Centrum partnerskiego](headers.md) | Definiuje nagłówki żądań i odpowiedzi używane przez interfejs API REST. |
| [Zasoby REST Centrum partnerskiego](partner-center-rest-resources.md) | Definiuje konstrukcje JSON reprezentujące obiekty, które są konieczne do korzystania z interfejsu API REST. |
| [Zdarzenia REST Centrum partnerskiego](partner-center-webhook-events.md) | Definiuje zdarzenia zmiany zasobów REST, które są obsługiwane przez elementy webhook Centrum partnerskiego. |
| [Języki obsługiwane przez Centrum partnerskie i ustawienia regionalne](partner-center-supported-languages-and-locales.md) | Wyświetla listę ustawień regionalnych, języków i krajów/regionów, które są obsługiwane przez interfejsy API Centrum partnerskiego. |
| [Elementy webhook Centrum partnerskiego](partner-center-webhooks.md) | Jak odbierać zdarzenia, uwierzytelniać wywołania zwrotne i używać interfejsów API elementu webhook Centrum partnerskiego do tworzenia, przeglądania i aktualizowania rejestracji zdarzeń. |