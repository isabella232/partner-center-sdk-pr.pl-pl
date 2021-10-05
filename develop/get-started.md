---
title: Rozpoczęcie pracy
description: Usługa zestaw SDK Centrum partnerskiego zarządzany interfejs API i interfejs API REST dla partnerów, których można używać do zarządzania danymi klientów, subskrypcji i zamówień.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.custom: intro-get-started
ms.openlocfilehash: affc19c8533fddd7212d52cf02e013531bacdcc5
ms.sourcegitcommit: f112efee7344d739bdbf385adba0c554ea2a63e3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/04/2021
ms.locfileid: "129439314"
---
# <a name="get-started"></a>Rozpoczęcie pracy

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Usługa zestaw SDK Centrum partnerskiego zarządzany interfejs API i interfejs API REST dla partnerów, których można używać do zarządzania danymi klientów, subskrypcji i zamówień.

## <a name="get-the-code"></a>Uzyskiwanie kodu

[Pobierz zestaw SDK Centrum partnerskiego](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> Dostęp interfejsu API do Partner Center dla odsprzedawców pośrednich nie jest obsługiwanym scenariuszem.

## <a name="determine-your-version-of-partner-center"></a>Określanie wersji Partner Center

Niektóre wersje Partner Center nie mają dostępnego całego zestawu SDK. Aby uzyskać więcej informacji, zobacz Developing for Partner Center for Microsoft National Cloud (Tworzenie aplikacji dla [chmury microsoft national cloud).](developing-for-partner-center-for-microsoft-national-cloud.md)

## <a name="get-the-samples"></a>Pobierz przykłady

Aby uzyskać więcej informacji na temat fragmentów kodu w języku C#, przykładów REST i przykładowej aplikacji, [zobacz Partner Center przykłady](partner-center-samples.md).

## <a name="test-vs-production"></a>Testowanie a produkcja

Podczas początkowego pisania i testowania kodu należy użyć konta piaskownicy integracji (i odpowiednich tokenów), aby uniknąć przypadkowego naliczenie nowych opłat, za które firma jest odpowiedzialna. Aby uzyskać więcej informacji na temat tego środowiska testowego, zobacz [Konfigurowanie dostępu do interfejsu API w Partner Center](set-up-api-access-in-partner-center.md).

Gdy rozwiązanie zostanie przetestowane i będzie gotowe do użycia na rzeczywistych kontach klientów, musisz zaktualizować tokeny, aby używać aplikacji klienckiej usługi Azure AD i klucza tajnego, które odpowiadają Głównemu kontu usługi Partner Center.

Aby uzyskać porady i sugestie dotyczące testowania i debugowania, w tym więcej informacji na temat testowania w środowisku produkcyjnym (TiP) i piaskownicy integracji, zobacz [Testowanie i debugowanie](test-and-debug.md).

## <a name="configure-your-authentication"></a>Konfigurowanie uwierzytelniania

Aby skonfigurować uwierzytelnianie usługi Azure AD w celu korzystania z interfejsów API Partner Center, zobacz [Partner Center uwierzytelniania.](partner-center-authentication.md)

> [!IMPORTANT]
> Firma Microsoft wprowadza bezpieczną, skalowalną platformę do uwierzytelniania partnerów dostawców rozwiązań w chmurze (CSP) i dostawców panelu sterowania (CPV) za pośrednictwem architektury usługi Microsoft Azure Multi-Factor Authentication (MFA).
Partner Center używa usługi Azure AD do uwierzytelniania, a aby używać interfejsów API Partner Center, należy poprawnie skonfigurować ustawienia uwierzytelniania.
>
> Aby uzyskać więcej informacji, zobacz [Włączanie bezpiecznego modelu aplikacji.](enable-secure-app-model.md)

## <a name="get-help"></a>Uzyskaj pomoc

Partnerzy mogą uzyskać pomoc techniczną [w zestaw SDK Centrum partnerskiego Yammer grupy](https://go.microsoft.com/fwlink/p/?LinkID=717360). Aby uzyskać bardziej spersonalizowaną pomoc, deweloperzy mogą korzystać z korzyści pomocy technicznej MPN lub pomocy technicznej Premier.

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a>Dołącz do programu wczesnych użytkowników w interfejsu API i zestawu SDK Centrum partnerskiego

Aby dowiedzieć się, jak możesz współpracować z firmą Microsoft nad opracowywaniem funkcji i możliwości partnerów, [zobacz Join the Partner Center API and SDK Early Adopter Program (Dołączanie](early-adopter-program.md)do interfejsu API i zestawu SDK wcześnie przyjętego programu).
