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
# <a name="partner-center-rest-api-reference-to-rest-urls-rest-headers-rest-resources-and-rest-events"></a><span data-ttu-id="c51c5-103">Dokumentacja interfejsu API REST Centrum partnerskiego do adresów URL REST, nagłówków REST, zasobów REST i zdarzeń REST</span><span class="sxs-lookup"><span data-stu-id="c51c5-103">Partner Center REST API reference to REST URLs, REST headers, REST resources, and REST events</span></span>

<span data-ttu-id="c51c5-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="c51c5-104">**Applies to:**</span></span>

- <span data-ttu-id="c51c5-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="c51c5-105">Partner Center</span></span>
- <span data-ttu-id="c51c5-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="c51c5-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="c51c5-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="c51c5-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="c51c5-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="c51c5-108">Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="partner-center-rest-api"></a><span data-ttu-id="c51c5-109">Interfejs API REST Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="c51c5-109">Partner Center REST API</span></span>

<span data-ttu-id="c51c5-110">Interfejs API REST Centrum partnerskiego pomaga partnerom dostawcy rozwiązań w chmurze zintegrować swoje istniejące oprogramowanie CRM lub rozliczeń z systemami firmy Microsoft, które zarządzają kontami klientów, umieszczają zamówienia, zarządzają subskrypcjami i obsługują żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="c51c5-110">The Partner Center REST API helps Cloud Solution Provider (CSP) partners integrate their existing CRM or billing software with the Microsoft systems that manage customer accounts, place orders, manage subscriptions, and handle support requests.</span></span>

<span data-ttu-id="c51c5-111">Aby uzyskać więcej informacji o tym, co może zrobić interfejs API, w tym przykładowy kod, zobacz temat [scenariusze](scenarios.md) , w tym omówienie w tle.</span><span class="sxs-lookup"><span data-stu-id="c51c5-111">For more information about what the API can do, including sample code, see the [Scenarios](scenarios.md) topic, including the background overview.</span></span>

<span data-ttu-id="c51c5-112">Przed rozpoczęciem kodowania zapoznaj się [z tematem wprowadzenie.](get-started.md)</span><span class="sxs-lookup"><span data-stu-id="c51c5-112">Before you begin coding, read the [Get started](get-started.md) topic.</span></span> <span data-ttu-id="c51c5-113">Ten artykuł zawiera informacje na temat konfigurowania kont testowych i produkcyjnych, uzyskiwania informacji o działaniu uwierzytelniania i znajdowania przykładowego kodu.</span><span class="sxs-lookup"><span data-stu-id="c51c5-113">This article contains information about setting up your test and production accounts, getting authentication working, and finding the sample code.</span></span>

## <a name="topics"></a><span data-ttu-id="c51c5-114">Tematy</span><span class="sxs-lookup"><span data-stu-id="c51c5-114">Topics</span></span>

| <span data-ttu-id="c51c5-115">Temat</span><span class="sxs-lookup"><span data-stu-id="c51c5-115">Topic</span></span> | <span data-ttu-id="c51c5-116">Opis</span><span class="sxs-lookup"><span data-stu-id="c51c5-116">Description</span></span> |
| ----- | ----------- |
| [<span data-ttu-id="c51c5-117">Adresy URL REST Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="c51c5-117">Partner Center REST URLs</span></span>](partner-center-rest-urls.md) | <span data-ttu-id="c51c5-118">Definiuje punkty końcowe interfejsu API REST dla różnych wersji Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="c51c5-118">Defines the REST API endpoints for different versions of Partner Center.</span></span> |
| [<span data-ttu-id="c51c5-119">Nagłówki REST Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="c51c5-119">Partner Center REST headers</span></span>](headers.md) | <span data-ttu-id="c51c5-120">Definiuje nagłówki żądań i odpowiedzi używane przez interfejs API REST.</span><span class="sxs-lookup"><span data-stu-id="c51c5-120">Defines the request and response headers used by the REST API.</span></span> |
| [<span data-ttu-id="c51c5-121">Zasoby REST Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="c51c5-121">Partner Center REST resources</span></span>](partner-center-rest-resources.md) | <span data-ttu-id="c51c5-122">Definiuje konstrukcje JSON reprezentujące obiekty, które są konieczne do korzystania z interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="c51c5-122">Defines the JSON constructs that represent the objects needed to use the REST API.</span></span> |
| [<span data-ttu-id="c51c5-123">Zdarzenia REST Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="c51c5-123">Partner Center REST events</span></span>](partner-center-webhook-events.md) | <span data-ttu-id="c51c5-124">Definiuje zdarzenia zmiany zasobów REST, które są obsługiwane przez elementy webhook Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="c51c5-124">Defines the REST resource change events that are supported by Partner Center webhooks.</span></span> |
| [<span data-ttu-id="c51c5-125">Języki obsługiwane przez Centrum partnerskie i ustawienia regionalne</span><span class="sxs-lookup"><span data-stu-id="c51c5-125">Partner Center supported languages and locales</span></span>](partner-center-supported-languages-and-locales.md) | <span data-ttu-id="c51c5-126">Wyświetla listę ustawień regionalnych, języków i krajów/regionów, które są obsługiwane przez interfejsy API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="c51c5-126">Lists the locales, languages, and country/region codes that are supported in the Partner Center APIs.</span></span> |
| [<span data-ttu-id="c51c5-127">Elementy webhook Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="c51c5-127">Partner Center webhooks</span></span>](partner-center-webhooks.md) | <span data-ttu-id="c51c5-128">Jak odbierać zdarzenia, uwierzytelniać wywołania zwrotne i używać interfejsów API elementu webhook Centrum partnerskiego do tworzenia, przeglądania i aktualizowania rejestracji zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="c51c5-128">How to receive events, authenticate a callback, and use the Partner Center webhook APIs to create, view, and update an event registration.</span></span> |