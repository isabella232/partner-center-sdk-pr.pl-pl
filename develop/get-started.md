---
title: Rozpoczęcie pracy
description: Zestaw SDK Centrum partnerskiego zawiera zarządzany interfejs API i interfejs API REST dla partnerów służących do zarządzania danymi klienta, subskrypcji i zamówień.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9c2af1e11dbda19489a27e37c7f3de8ede90fd1c
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767913"
---
# <a name="get-started"></a>Rozpoczęcie pracy

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Zestaw SDK Centrum partnerskiego zawiera zarządzany interfejs API i interfejs API REST dla partnerów służących do zarządzania danymi klienta, subskrypcji i zamówień.

## <a name="get-the-code"></a>Uzyskiwanie kodu

[Pobierz zestaw SDK Centrum partnerskiego](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> Dostęp za pomocą interfejsu API do Centrum partnerskiego dla pośrednich odsprzedawcy nie jest obsługiwanym scenariuszem.

## <a name="determine-your-version-of-partner-center"></a>Określ swoją wersję Centrum partnerskiego

Niektóre wersje Centrum partnerskiego nie mają dostępnego całego zestawu SDK. Aby uzyskać więcej informacji, zobacz [Tworzenie aplikacji dla firm partnerskich w chmurze firmy Microsoft](developing-for-partner-center-for-microsoft-national-cloud.md).

## <a name="get-the-samples"></a>Pobierz przykłady

Aby uzyskać więcej informacji na temat fragmentów języka C#, przykładów REST i przykładowej aplikacji, zobacz [przykłady Centrum partnerskiego](partner-center-samples.md).

## <a name="test-vs-production"></a>Test a produkcja

Podczas pierwszego pisania i testowania kodu, należy użyć konta piaskownicy integracji (i odpowiednich tokenów), aby nie nawiązać przypadkowo ponoszenia nowych opłat, które firma zobowiązana do płacenia. Aby uzyskać więcej informacji o tym środowisku testowym, zobacz [Konfigurowanie dostępu do interfejsu API w centrum partnerskim](set-up-api-access-in-partner-center.md).

Gdy Twoje rozwiązanie zostanie przetestowane i będzie gotowe do użycia na rzeczywistych kontach klienta, musisz zaktualizować tokeny, aby korzystać z aplikacji klienckiej usługi Azure AD i wpisu tajnego odpowiadającego Twojemu podstawowemu kontu Centrum partnerskiego.

Aby uzyskać porady i sugestie dotyczące testowania i debugowania, w tym więcej informacji na temat testów w środowisku produkcyjnym (TiP) i piaskownicy integracji, zobacz [testowanie i debugowanie](test-and-debug.md).

## <a name="configure-your-authentication"></a>Konfigurowanie uwierzytelniania

Aby skonfigurować uwierzytelnianie usługi Azure AD w taki sposób, aby można było używać interfejsów API Centrum partnerskiego, zobacz [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).

> [!IMPORTANT]
> Firma Microsoft wprowadza bezpieczną i skalowalną platformę do uwierzytelniania partnerów dostawcy rozwiązań w chmurze (CSP) i dostawców panelu sterowania (CPV) za pomocą Microsoft Azure architekturę uwierzytelniania wieloskładnikowego (MFA).
Centrum partnerskie używa usługi Azure AD do uwierzytelniania i korzystania z interfejsów API Centrum partnerskiego należy prawidłowo skonfigurować ustawienia uwierzytelniania.
>
> Aby uzyskać więcej informacji, zobacz [Włączanie bezpiecznego modelu aplikacji](enable-secure-app-model.md).

## <a name="get-help"></a>Uzyskaj pomoc

Partnerzy mogą uzyskać pomoc techniczną w [grupie yammera zestawu SDK Centrum partnerskiego](https://go.microsoft.com/fwlink/p/?LinkID=717360). Aby uzyskać bardziej spersonalizowaną pomoc, deweloperzy mogą korzystać z korzyści z pomocy technicznej MPN lub pomoc techniczna Premium.

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a>Dołącz do programu wczesnych użytkowników w interfejsu API i zestawu SDK Centrum partnerskiego

Aby dowiedzieć się, w jaki sposób można współpracować z firmą Microsoft w zakresie opracowywania funkcji i możliwości partnerów, zobacz [dodatek do interfejsu API Centrum partnerskiego i zestawu SDK wczesnego oprogramowania do wdrażania](early-adopter-program.md).
