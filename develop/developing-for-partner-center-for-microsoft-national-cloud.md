---
title: Tworzenie aplikacji dla Centrum partnerskiego dla chmur krajowych firmy Microsoft
description: Różnice dotyczące zestawu SDK Centrum partnerskiego podczas tworzenia dla Centrum partnerskiego w chmurach narodowych firmy Microsoft.
MS-HAID:
- pc\_apiv2.developing\_with\_different\_partner\_center\_versions
- pc\_apiv2.developing\_for\_partner\_center\_for\_microsoft\_national\_cloud
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7882846de0c591b21fe73345f560613f535d1788
ms.sourcegitcommit: 529b07030a874d644cf947790f4b53cdff438dd4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768149"
---
# <a name="developing-for-partner-center-for-microsoft-national-clouds"></a>Tworzenie aplikacji dla Centrum partnerskiego dla chmur krajowych firmy Microsoft

**Dotyczy:**

- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Centrum partnerskie ma jeden zestaw dokumentacji zestawu SDK. Jednak niektóre funkcje mogą być niedostępne w wersjach usługi Partner Center dla chmur narodowych firmy Microsoft.

Deweloperzy muszą rozważyć zmiany w zestawie SDK dla następujących wersji Centrum partnerskiego:

- [Centrum partnerskie obsługiwane przez firmę 21Vianet](#partner-center-operated-by-21vianet)
- [Centrum partnerskie dla Microsoft Cloud Niemcy](#partner-center-for-microsoft-cloud-germany)
- [Centrum partnerskie Microsoft Cloud for US Government](#partner-center-for-microsoft-cloud-for-us-government)

Każdy artykuł zestawu SDK Centrum partnerskiego zawiera listę odpowiednich wersji Centrum partnerskiego. W każdym zarządzanym artykule znajdują się także odpowiednie wersje Centrum partnerskiego w sekcji **wymagania** .

## <a name="partner-center-operated-by-21vianet"></a>Centrum partnerskie obsługiwane przez firmę 21Vianet

Różnice między *centrum partnerskim* i *centrum partnerskim obsługiwane przez firmę 21Vianet* są następujące:

- Nie można programowo zresetować hasła dla użytkownika klienta lub pełnego partnera.

- Subskrypcje na platformę Azure nie są dostępne.

- Nie można zarządzać licencjami dla użytkownika klienta. Zamiast tego klienci muszą zarządzać licencjami przy użyciu Centrum administracyjnego pakietu Office 365.

- Wszystkie żądania pomocy technicznej są zarządzane za pomocą Centrum partnerskiego obsługiwanego przez firmę 21Vianet. Żądania obsługi i aktualizacje usług nie są stosowane.

## <a name="partner-center-for-microsoft-cloud-germany"></a>Centrum partnerskie dla Microsoft Cloud Niemcy

> [!IMPORTANT]
> W oparciu o ewolucję potrzeb klientów Nasza strategia chmury dla Niemiec będzie koncentrować się na dostawie nowych regionów w chmurze w Niemczech, które są zgodne z naszą globalną ofertą w chmurze. Z tym fokusem nie będziemy już akceptować nowych klientów ani wdrażać nowych usług z obecnie dostępnego Microsoft Cloud Niemiec. Istniejący klienci mogą nadal korzystać z aktualnych dostępnych usług w chmurze, które zostaną zachowane z wymaganymi aktualizacjami zabezpieczeń.
>
> W przód nowi klienci mogą korzystać z dostępnych obecnie regionów europejskich lub nowych regionów w Niemczech, gdy staną się dostępne. Aby uzyskać więcej informacji, zobacz [Microsoft w celu dostarczania usług w chmurze z nowych centrów danych w Niemczech](https://news.microsoft.com/europe/2018/08/31/microsoft-to-deliver-cloud-services-from-new-datacentres-in-germany-in-2019-to-meet-evolving-customer-needs/).

Różnice między *centrum partnerskim* a *centrum partnerskim Microsoft Cloud Niemcy* są następujące:

- Partnerzy nie mogą tworzyć użytkowników dla organizacji klienta ani przypisywać ról.
  - Partnerzy mogą odczytywać pola, ale nie mogą ich zapisywać ani aktualizować.
  - Partnerzy muszą ręcznie utworzyć lub zaktualizować użytkowników swoich klientów w centrum administracyjnym pakietu Office 365 lub przez Azure Portal. Zobacz [dokumentację Azure Active Directory](/azure/active-directory/).

- Nie można zarządzać licencjami dla użytkowników Twojego klienta przy użyciu Centrum partnerskiego dla Microsoft Cloudego portalu lub interfejsów API. Zamiast tego należy użyć Centrum administracyjnego pakietu Office 365 lub usługi Azure Active GroupD bezpośredniego zarządzania licencjami (już wkrótce) do zarządzania licencjami.
  - (Opcjonalnie) możesz użyć usługi Azure AD interfejs API programu Graph. Zobacz [Przypisywanie licencji do użytkownika](/graph/api/user-assignlicense). W centrum partnerskim dla Microsoft Cloud Niemcy upewnij się, że używasz punktu końcowego grafu `https://graph.cloudapi.de` zamiast `https://graph.windows.net` .

- Nie można programowo zresetować hasła dla użytkownika klienta lub pełnego partnera. Użyj centrum administracyjnego pakietu Office 365 lub Azure Portal. Zobacz [Resetowanie hasła użytkownika w Azure Active Directory](/azure/active-directory/fundamentals/active-directory-users-reset-password-azure-portal). W kroku 1 należy zalogować się do Azure Portal Microsoft Cloud Niemcy.

- Deweloperzy muszą ręcznie zarejestrować swój identyfikator swojej aplikacji, aby zintegrować funkcje interfejsu API/zestawu SDK Centrum partnerskiego w aplikacji dla Centrum partnerskiego na Microsoft Cloud Niemcy. Aby uzyskać więcej informacji, zobacz [rejestrowanie szczegółowych informacji o aplikacji dla Centrum partnerskiego w usłudze Microsoft National Cloud](create-apps-for-partner-center-for-microsoft-national-clouds.md).

## <a name="partner-center-for-microsoft-cloud-for-us-government"></a>Centrum partnerskie Microsoft Cloud for US Government

Różnice między *centrum partnerskim* i *centrum partnerskim Microsoft Cloud dla instytucji rządowych USA* są następujące:

- Subskrypcje pakietu Office 365 nie są obecnie dostępne dla Centrum partnerskiego dla Microsoft Cloud dla instytucji rządowych USA.

- Istniejący Partnerzy wspierający Microsoft Cloud dla instytucji rządowych USA muszą utworzyć nowe konta w centrum partnerskim dla Microsoft Cloud dla instytucji rządowych USA.

- Microsoft Cloud dla klientów rządowych w Stanach Zjednoczonych muszą być transakcyjne dla jednego partnera.
  - Nie mają zastosowania wielokanałowe i wielopartnerskie i żądanie relacji z istniejącym klientem w ramach Microsoft Cloud dla instytucji rządowych USA. To ograniczenie wynika z faktu, że pakiet Office 365 nie jest obecnie dostępny.

- Partnerzy nie mogą tworzyć użytkowników dla organizacji klienta ani przypisywać ról.
  - Partnerzy mogą odczytywać pola, ale nie mogą ich zapisywać ani aktualizować. Partnerzy muszą ręcznie utworzyć lub zaktualizować użytkowników swoich klientów w Azure Portal. Zobacz [dokumentację Azure Active Directory](/azure/active-directory/).

- Nie można programowo zresetować hasła dla użytkownika klienta lub pełnego partnera. Użyj Azure Portal. Zobacz [Resetowanie hasła użytkownika w Azure Active Directory](/azure/active-directory/active-directory-users-reset-password-azure-portal). W kroku 1 musisz zalogować się do Azure Portal Microsoft Cloud dla instytucji rządowych USA.

- Punkty końcowe REST Centrum partnerskiego Microsoft Cloud dla instytucji rządowych USA są takie same jak w przypadku Centrum partnerskiego: `https://api.partnercenter.microsoft.com` .

- Deweloperzy muszą ręcznie zarejestrować swój identyfikator swojej aplikacji, aby zintegrować funkcje interfejsu API/zestawu SDK Centrum partnerskiego w aplikacji dla Centrum partnerskiego na Microsoft Cloud dla instytucji rządowych USA. Aby uzyskać więcej informacji, zobacz [rejestrowanie szczegółowych informacji o aplikacji dla Centrum partnerskiego w usłudze Microsoft National Cloud](create-apps-for-partner-center-for-microsoft-national-clouds.md).
