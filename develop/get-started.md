---
title: Rozpoczęcie pracy
description: Usługa zestaw SDK Centrum partnerskiego zarządzany interfejs API i interfejs API REST dla partnerów, których można używać do zarządzania danymi klientów, subskrypcji i zamówień.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b5d05f26d63574ef876519091dc1c33c05f36e25
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548757"
---
# <a name="get-started"></a><span data-ttu-id="42c5f-103">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="42c5f-103">Get started</span></span>

<span data-ttu-id="42c5f-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="42c5f-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="42c5f-105">Usługa zestaw SDK Centrum partnerskiego zarządzany interfejs API i interfejs API REST dla partnerów, których można używać do zarządzania danymi klientów, subskrypcji i zamówień.</span><span class="sxs-lookup"><span data-stu-id="42c5f-105">The Partner Center SDK includes a managed API and a REST API for partners to use to manage customer, subscription, and order data.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="42c5f-106">Uzyskiwanie kodu</span><span class="sxs-lookup"><span data-stu-id="42c5f-106">Get the code</span></span>

[<span data-ttu-id="42c5f-107">Pobierz zestaw SDK Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="42c5f-107">Download the Partner Center SDK</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> <span data-ttu-id="42c5f-108">Dostęp do interfejsu API Partner Center dla odsprzedawców pośrednich nie jest obsługiwanym scenariuszem.</span><span class="sxs-lookup"><span data-stu-id="42c5f-108">API access to Partner Center for indirect resellers isn't a supported scenario.</span></span>

## <a name="determine-your-version-of-partner-center"></a><span data-ttu-id="42c5f-109">Określanie wersji Partner Center</span><span class="sxs-lookup"><span data-stu-id="42c5f-109">Determine your version of Partner Center</span></span>

<span data-ttu-id="42c5f-110">Niektóre wersje Partner Center nie mają dostępnego całego zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="42c5f-110">Some versions of Partner Center do not have the entire SDK available.</span></span> <span data-ttu-id="42c5f-111">Aby uzyskać więcej informacji, zobacz Developing for Partner Center for Microsoft National Cloud (Tworzenie aplikacji dla [chmury microsoft national cloud).](developing-for-partner-center-for-microsoft-national-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="42c5f-111">For more information, see [Developing for Partner Center for Microsoft National Cloud](developing-for-partner-center-for-microsoft-national-cloud.md).</span></span>

## <a name="get-the-samples"></a><span data-ttu-id="42c5f-112">Pobierz przykłady</span><span class="sxs-lookup"><span data-stu-id="42c5f-112">Get the samples</span></span>

<span data-ttu-id="42c5f-113">Aby uzyskać więcej informacji na temat fragmentów kodu w języku C#, przykładów REST i przykładowej aplikacji, [zobacz Partner Center przykłady.](partner-center-samples.md)</span><span class="sxs-lookup"><span data-stu-id="42c5f-113">For more information about C# snippets, REST samples, and the sample app, see [Partner Center samples](partner-center-samples.md).</span></span>

## <a name="test-vs-production"></a><span data-ttu-id="42c5f-114">Testowanie a produkcja</span><span class="sxs-lookup"><span data-stu-id="42c5f-114">Test vs. production</span></span>

<span data-ttu-id="42c5f-115">Podczas początkowego pisania i testowania kodu należy użyć konta piaskownicy integracji (i odpowiednich tokenów), aby uniknąć przypadkowego naliczenie nowych opłat, za które firma jest odpowiedzialna.</span><span class="sxs-lookup"><span data-stu-id="42c5f-115">While you are initially writing and testing your code, you should use your integration sandbox account (and the corresponding tokens) so that you don't accidentally incur new charges that your company is responsible for paying.</span></span> <span data-ttu-id="42c5f-116">Aby uzyskać więcej informacji na temat tego środowiska testowego, zobacz [Konfigurowanie dostępu do interfejsu API w Partner Center](set-up-api-access-in-partner-center.md).</span><span class="sxs-lookup"><span data-stu-id="42c5f-116">For more information about this testing environment, see [Set up API access in Partner Center](set-up-api-access-in-partner-center.md).</span></span>

<span data-ttu-id="42c5f-117">Gdy rozwiązanie zostanie przetestowane i będzie gotowe do użycia na rzeczywistych kontach klientów, musisz zaktualizować tokeny, aby używać aplikacji klienckiej usługi Azure AD i klucza tajnego, które odpowiadają głównemu kontu Partner Center podstawowego.</span><span class="sxs-lookup"><span data-stu-id="42c5f-117">When your solution is tested and ready to use on real customer accounts, you'll have to update your tokens so that you're using an Azure AD client app and secret that correspond to your Primary Partner Center account.</span></span>

<span data-ttu-id="42c5f-118">Aby uzyskać porady i sugestie dotyczące testowania i debugowania, w tym więcej informacji na temat testowania w środowisku produkcyjnym (TiP) i piaskownicy integracji, zobacz [Testowanie i debugowanie](test-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="42c5f-118">For tips and suggestions about testing and debugging, including more information about Test-in-Production (TiP) and the Integration Sandbox, see [Test and debug](test-and-debug.md).</span></span>

## <a name="configure-your-authentication"></a><span data-ttu-id="42c5f-119">Konfigurowanie uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="42c5f-119">Configure your authentication</span></span>

<span data-ttu-id="42c5f-120">Aby skonfigurować uwierzytelnianie usługi Azure AD w celu korzystania z interfejsów API Partner Center, zobacz [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="42c5f-120">To configure your Azure AD authentication so that you can use the Partner Center APIs, see [Partner Center authentication](partner-center-authentication.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="42c5f-121">Firma Microsoft wprowadza bezpieczną, skalowalną platformę do uwierzytelniania partnerów dostawców rozwiązań w chmurze (CSP) i dostawców panelu sterowania (CPV) za pośrednictwem architektury Microsoft Azure Multi-Factor Authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="42c5f-121">Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure multi-factor authentication (MFA) architecture.</span></span>
<span data-ttu-id="42c5f-122">Partner Center używa usługi Azure AD do uwierzytelniania, a aby korzystać z interfejsów API Partner Center, musisz poprawnie skonfigurować ustawienia uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="42c5f-122">Partner Center uses Azure AD for authentication, and to use the Partner Center APIs you must configure your authentication settings correctly.</span></span>
>
> <span data-ttu-id="42c5f-123">Aby uzyskać więcej informacji, zobacz [Włączanie bezpiecznego modelu aplikacji.](enable-secure-app-model.md)</span><span class="sxs-lookup"><span data-stu-id="42c5f-123">For more information, see [Enable secure application model](enable-secure-app-model.md).</span></span>

## <a name="get-help"></a><span data-ttu-id="42c5f-124">Uzyskaj pomoc</span><span class="sxs-lookup"><span data-stu-id="42c5f-124">Get help</span></span>

<span data-ttu-id="42c5f-125">Partnerzy mogą uzyskać pomoc techniczną w [zestaw SDK Centrum partnerskiego Yammer grupy](https://go.microsoft.com/fwlink/p/?LinkID=717360).</span><span class="sxs-lookup"><span data-stu-id="42c5f-125">Partners can get support at the [Partner Center SDK Yammer group](https://go.microsoft.com/fwlink/p/?LinkID=717360).</span></span> <span data-ttu-id="42c5f-126">Aby uzyskać bardziej spersonalizowaną pomoc, deweloperzy mogą korzystać z korzyści pomocy technicznej MPN lub pomocy technicznej Premier.</span><span class="sxs-lookup"><span data-stu-id="42c5f-126">To get more personalized help, developers can use their MPN support benefits or Premier Support.</span></span>

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a><span data-ttu-id="42c5f-127">Dołącz do programu wczesnych użytkowników w interfejsu API i zestawu SDK Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="42c5f-127">Join the Partner Center API and SDK Early Adopter Program</span></span>

<span data-ttu-id="42c5f-128">Aby dowiedzieć się, jak możesz współpracować z firmą Microsoft nad opracowywaniem funkcji i możliwości partnerów, zobacz [Join the Partner Center API and SDK Early Adopter Program](early-adopter-program.md)(Dołączanie do interfejsu API i zestawu SDK wcześnie przyjętego programu).</span><span class="sxs-lookup"><span data-stu-id="42c5f-128">To find out how you can collaborate with Microsoft on the development of Partner features and capabilities, see [Join the Partner Center API and SDK Early Adopter Program](early-adopter-program.md).</span></span>
