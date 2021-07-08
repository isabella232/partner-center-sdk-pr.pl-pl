---
title: Dokumentacja interfejsu API REST Centrum partnerskiego
description: Dowiedz się, jak partnerzy programu CSP mogą używać Partner Center API REST w celu zintegrowania oprogramowania CRM i rozliczeń z systemami firmy Microsoft w celu lepszego zarządzania kontami klientów.
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 18621fdb94f91f066b69a11f7d557410d653787e
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548043"
---
# <a name="partner-center-rest-api-reference-to-rest-urls-rest-headers-rest-resources-and-rest-events"></a><span data-ttu-id="77d1a-103">Partner Center API REST do adresów URL REST, nagłówków REST, zasobów REST i zdarzeń REST</span><span class="sxs-lookup"><span data-stu-id="77d1a-103">Partner Center REST API reference to REST URLs, REST headers, REST resources, and REST events</span></span>

<span data-ttu-id="77d1a-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="77d1a-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="partner-center-rest-api"></a><span data-ttu-id="77d1a-105">Partner Center REST API</span><span class="sxs-lookup"><span data-stu-id="77d1a-105">Partner Center REST API</span></span>

<span data-ttu-id="77d1a-106">Interfejs API REST usługi Partner Center pomaga partnerom firmy Dostawca rozwiązań w chmurze (CSP) zintegrować istniejące oprogramowanie CRM lub rozliczeniowe z systemami firmy Microsoft, które zarządzają kontami klientów, składają zamówienia, zarządzają subskrypcjami i obsługują żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="77d1a-106">The Partner Center REST API helps Cloud Solution Provider (CSP) partners integrate their existing CRM or billing software with the Microsoft systems that manage customer accounts, place orders, manage subscriptions, and handle support requests.</span></span>

<span data-ttu-id="77d1a-107">Aby uzyskać więcej informacji na temat tego, co interfejs API może zrobić, w tym przykładowy kod, zobacz temat [Scenariusze,](scenarios.md) w tym omówienie w tle.</span><span class="sxs-lookup"><span data-stu-id="77d1a-107">For more information about what the API can do, including sample code, see the [Scenarios](scenarios.md) topic, including the background overview.</span></span>

<span data-ttu-id="77d1a-108">Przed rozpoczęciem kodowania przeczytaj temat [Wprowadzenie.](get-started.md)</span><span class="sxs-lookup"><span data-stu-id="77d1a-108">Before you begin coding, read the [Get started](get-started.md) topic.</span></span> <span data-ttu-id="77d1a-109">Ten artykuł zawiera informacje dotyczące konfigurowania kont testowych i produkcyjnych, uzyskiwania uwierzytelniania i znajdowania przykładowego kodu.</span><span class="sxs-lookup"><span data-stu-id="77d1a-109">This article contains information about setting up your test and production accounts, getting authentication working, and finding the sample code.</span></span>

<span data-ttu-id="77d1a-110">Aby uzyskać przewodnik informacyjny objaśnijący poszczególne interfejsy API, zobacz [Partner Center API REST.](/rest/api/partner-center-rest/)</span><span class="sxs-lookup"><span data-stu-id="77d1a-110">For a reference guide explaining each API, see [Partner Center REST API](/rest/api/partner-center-rest/).</span></span>

## <a name="topics"></a><span data-ttu-id="77d1a-111">Tematy</span><span class="sxs-lookup"><span data-stu-id="77d1a-111">Topics</span></span>

| <span data-ttu-id="77d1a-112">Temat</span><span class="sxs-lookup"><span data-stu-id="77d1a-112">Topic</span></span> | <span data-ttu-id="77d1a-113">Opis</span><span class="sxs-lookup"><span data-stu-id="77d1a-113">Description</span></span> |
| ----- | ----------- |
| [<span data-ttu-id="77d1a-114">Partner Center REST API</span><span class="sxs-lookup"><span data-stu-id="77d1a-114">Partner Center REST API</span></span>](/rest/api/partner-center-rest/) | <span data-ttu-id="77d1a-115">Dokumentacja każdego interfejsu API REST dostępnego dla Partner Center.</span><span class="sxs-lookup"><span data-stu-id="77d1a-115">Reference of each REST API available for Partner Center.</span></span> |
| [<span data-ttu-id="77d1a-116">Adresy URL REST Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="77d1a-116">Partner Center REST URLs</span></span>](partner-center-rest-urls.md) | <span data-ttu-id="77d1a-117">Definiuje punkty końcowe interfejsu API REST dla różnych wersji Partner Center.</span><span class="sxs-lookup"><span data-stu-id="77d1a-117">Defines the REST API endpoints for different versions of Partner Center.</span></span> |
| [<span data-ttu-id="77d1a-118">Nagłówki REST Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="77d1a-118">Partner Center REST headers</span></span>](headers.md) | <span data-ttu-id="77d1a-119">Definiuje nagłówki żądań i odpowiedzi używane przez interfejs API REST.</span><span class="sxs-lookup"><span data-stu-id="77d1a-119">Defines the request and response headers used by the REST API.</span></span> |
| [<span data-ttu-id="77d1a-120">Zasoby REST Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="77d1a-120">Partner Center REST resources</span></span>](partner-center-rest-resources.md) | <span data-ttu-id="77d1a-121">Definiuje konstrukcje JSON reprezentujące obiekty potrzebne do korzystania z interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="77d1a-121">Defines the JSON constructs that represent the objects needed to use the REST API.</span></span> |
| [<span data-ttu-id="77d1a-122">Zdarzenia REST Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="77d1a-122">Partner Center REST events</span></span>](partner-center-webhook-events.md) | <span data-ttu-id="77d1a-123">Definiuje zdarzenia zmiany zasobów REST, które są obsługiwane przez Partner Center webhook.</span><span class="sxs-lookup"><span data-stu-id="77d1a-123">Defines the REST resource change events that are supported by Partner Center webhooks.</span></span> |
| [<span data-ttu-id="77d1a-124">Języki obsługiwane przez Centrum partnerskie i ustawienia regionalne</span><span class="sxs-lookup"><span data-stu-id="77d1a-124">Partner Center supported languages and locales</span></span>](partner-center-supported-languages-and-locales.md) | <span data-ttu-id="77d1a-125">Wyświetla listę lokalizacji regionalnych, języków i kodów krajów/regionów, które są obsługiwane w Partner Center API.</span><span class="sxs-lookup"><span data-stu-id="77d1a-125">Lists the locales, languages, and country/region codes that are supported in the Partner Center APIs.</span></span> |
| [<span data-ttu-id="77d1a-126">Elementy webhook Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="77d1a-126">Partner Center webhooks</span></span>](partner-center-webhooks.md) | <span data-ttu-id="77d1a-127">Jak odbierać zdarzenia, uwierzytelniać wywołanie zwrotne i używać interfejsów API Partner Center webhook do tworzenia, wyświetlania i aktualizowania rejestracji zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="77d1a-127">How to receive events, authenticate a callback, and use the Partner Center webhook APIs to create, view, and update an event registration.</span></span> |
