---
title: Tworzenie aplikacji dla Partner Center dla chmur krajowych firmy Microsoft
description: zestaw SDK Centrum partnerskiego różnice podczas tworzenia aplikacji dla Partner Center dla chmur krajowych firmy Microsoft.
MS-HAID:
- pc\_apiv2.developing\_with\_different\_partner\_center\_versions
- pc\_apiv2.developing\_for\_partner\_center\_for\_microsoft\_national\_cloud
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d38a35fb88b4835716e429aeed731a0d55d9a669
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906463"
---
# <a name="developing-for-partner-center-for-microsoft-national-clouds"></a>Tworzenie aplikacji dla Partner Center dla chmur krajowych firmy Microsoft

**Dotyczy:** Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Partner Center zawiera jeden zestaw dokumentacji zestawu SDK. Jednak niektóre funkcje mogą nie być dostępne w wersjach usługi Partner Center dla chmur krajowych firmy Microsoft.

Deweloperzy muszą wziąć pod uwagę zmiany w zestawie SDK dla następujących wersji Partner Center:

- [Centrum partnerskie obsługiwane przez firmę 21Vianet](#partner-center-operated-by-21vianet)
- [Centrum partnerskie dla Microsoft Cloud Niemcy](#partner-center-for-microsoft-cloud-germany)
- [Centrum partnerskie Microsoft Cloud for US Government](#partner-center-for-microsoft-cloud-for-us-government)

Każdy zestaw SDK Centrum partnerskiego zawiera listę odpowiednich Partner Center wersji. Każdy zarządzany artykuł referencyjny zawiera również listę Partner Center wersji w **sekcji** Wymagania.

## <a name="partner-center-operated-by-21vianet"></a>Centrum partnerskie obsługiwane przez firmę 21Vianet

Różnice między partnerami między *Partner Center* *a Partner Center obsługiwanymi przez firmę 21Vianet* są:

- Nie można programowo zresetować hasła użytkownika klienta lub pełnego partnera.

- Subskrypcje platformy Azure nie są dostępne.

- Nie można zarządzać licencjami dla użytkownika klienta. Zamiast tego klienci muszą używać centrum administracyjnego Office 365 do zarządzania licencjami.

- Wszystkie żądania pomocy technicznej są zarządzane za pośrednictwem Partner Center obsługiwanych przez firmę 21Vianet. Żądania obsługi i aktualizacje usług nie mają zastosowania.

## <a name="partner-center-for-microsoft-cloud-germany"></a>Centrum partnerskie dla Microsoft Cloud Niemcy

> [!IMPORTANT]
> W oparciu o ewolucję potrzeb klientów nasza strategia chmury dla Niemiec koncentruje się na dostarczeniu nowych regionów chmury w Niemczech, które są spójne z naszą ofertą chmury globalnej. Dzięki temu nie będziemy już akceptować nowych klientów ani wdrażać żadnych nowych usług z obecnie dostępnej usługi Microsoft Cloud w Niemczech. Istniejący klienci mogą nadal korzystać z bieżących dostępnych obecnie usług w chmurze, które będziemy utrzymywać z niezbędnymi aktualizacjami zabezpieczeń.
>
> W przyszłości nowi klienci mogą korzystać z obecnie dostępnych regionów europejskich lub nowych regionów w Niemczech, gdy staną się dostępne. Aby uzyskać więcej informacji, zobacz [Microsoft to deliver cloud services from new datacenters in Germany (Firma Microsoft](https://news.microsoft.com/europe/2018/08/31/microsoft-to-deliver-cloud-services-from-new-datacentres-in-germany-in-2019-to-meet-evolving-customer-needs/)może dostarczać usługi w chmurze z nowych centrów danych w Niemczech).

Różnice między partnerami w Partner Center *a* *Partner Center dla usługi Microsoft Cloud Germany* są:

- Partnerzy nie mogą tworzyć użytkowników dla swojej organizacji klienta ani przypisywać ról.
  - Partnerzy mogą odczytywać pola, ale nie mogą ich zapisywać ani aktualizować.
  - Partnerzy muszą ręcznie tworzyć lub aktualizować użytkowników swoich klientów w Office 365 administracyjnym lub za pośrednictwem Azure Portal. Zobacz [Azure Active Directory dokumentacji.](/azure/active-directory/)

- Nie można zarządzać licencjami dla użytkowników klienta przy użyciu interfejsów API Partner Center dla portalu Microsoft Cloud Germany. Zamiast tego należy użyć centrum administracyjnego Office 365 lub zarządzania licencjami usługi Azure Active Directly Group (wkrótce) w celu zarządzania licencjami.
  - (Opcjonalnie) możesz użyć interfejsu API usługi Azure AD Graph API. Zobacz [Przypisywanie licencji do użytkownika.](/graph/api/user-assignlicense) W Partner Center microsoft Cloud Germany należy użyć punktu końcowego usługi Graph `https://graph.cloudapi.de` zamiast `https://graph.windows.net` .

- Nie można programowo zresetować hasła użytkownika klienta lub pełnego partnera. Użyj centrum Office 365 administracyjnego lub Azure Portal. Zobacz [Resetowanie hasła użytkownika w Azure Active Directory](/azure/active-directory/fundamentals/active-directory-users-reset-password-azure-portal). W kroku 1 musisz zalogować się do witryny Azure Portal for Microsoft Cloud Germany.

- Deweloperzy muszą ręcznie zarejestrować swój identyfikator aplikacji, aby zintegrować Partner Center API/SDK w swojej aplikacji na Partner Center dla usługi Microsoft Cloud Germany. Aby uzyskać więcej informacji, zobacz Register app details for Partner Center for Microsoft National Cloud (Rejestrowanie szczegółów aplikacji [dla platformy Microsoft National Cloud).](create-apps-for-partner-center-for-microsoft-national-clouds.md)

## <a name="partner-center-for-microsoft-cloud-for-us-government"></a>Centrum partnerskie Microsoft Cloud for US Government

Różnice między partnerami między *Partner Center* i *Partner Center dla Microsoft Cloud for US Government* są:

- Office 365 subskrypcji nie są obecnie dostępne dla Partner Center dla Microsoft Cloud for US Government.

- Istniejący partnerzy obsługujący Microsoft Cloud for US Government muszą tworzyć nowe konta w Partner Center na Microsoft Cloud for US Government.

- Microsoft Cloud for US Government klienci muszą wykonać transakcję z jednym partnerem.
  - Relacja wielokanałowa i wieloskładnikowa oraz żądanie z istniejącym klientem w Microsoft Cloud for US Government scenariuszy nie mają zastosowania. To ograniczenie wynika Office 365, że nie jest obecnie dostępna.

- Partnerzy nie mogą tworzyć użytkowników dla swojej organizacji klienta ani przypisywać ról.
  - Partnerzy mogą odczytywać pola, ale nie mogą ich zapisywać ani aktualizować. Partnerzy muszą ręcznie tworzyć lub aktualizować użytkowników swoich klientów w Azure Portal. Zobacz [Azure Active Directory dokumentacji.](/azure/active-directory/)

- Nie można programowo zresetować hasła użytkownika klienta lub pełnego partnera. Użyj witryny Azure Portal. Zobacz [Resetowanie hasła użytkownika w Azure Active Directory](/azure/active-directory/active-directory-users-reset-password-azure-portal). W kroku 1 musisz zalogować się do Azure Portal, aby Microsoft Cloud for US Government.

- Punkty końcowe REST dla Partner Center dla Microsoft Cloud for US Government są takie same jak dla Partner Center: `https://api.partnercenter.microsoft.com` .

- Deweloperzy muszą ręcznie zarejestrować swój identyfikator aplikacji, aby zintegrować Partner Center API/SDK w swojej aplikacji na Partner Center for Microsoft Cloud for US Government. Aby uzyskać więcej informacji, zobacz Register app details for Partner Center for Microsoft National Cloud (Rejestrowanie szczegółów aplikacji [dla platformy Microsoft National Cloud).](create-apps-for-partner-center-for-microsoft-national-clouds.md)
