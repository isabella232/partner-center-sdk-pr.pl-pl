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
# <a name="get-started"></a><span data-ttu-id="20483-103">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="20483-103">Get started</span></span>

<span data-ttu-id="20483-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="20483-104">**Applies To**</span></span>

- <span data-ttu-id="20483-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="20483-105">Partner Center</span></span>
- <span data-ttu-id="20483-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="20483-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="20483-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="20483-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="20483-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="20483-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="20483-109">Zestaw SDK Centrum partnerskiego zawiera zarządzany interfejs API i interfejs API REST dla partnerów służących do zarządzania danymi klienta, subskrypcji i zamówień.</span><span class="sxs-lookup"><span data-stu-id="20483-109">The Partner Center SDK includes a managed API and a REST API for partners to use to manage customer, subscription, and order data.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="20483-110">Uzyskiwanie kodu</span><span class="sxs-lookup"><span data-stu-id="20483-110">Get the code</span></span>

[<span data-ttu-id="20483-111">Pobierz zestaw SDK Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="20483-111">Download the Partner Center SDK</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> <span data-ttu-id="20483-112">Dostęp za pomocą interfejsu API do Centrum partnerskiego dla pośrednich odsprzedawcy nie jest obsługiwanym scenariuszem.</span><span class="sxs-lookup"><span data-stu-id="20483-112">API access to Partner Center for indirect resellers isn't a supported scenario.</span></span>

## <a name="determine-your-version-of-partner-center"></a><span data-ttu-id="20483-113">Określ swoją wersję Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="20483-113">Determine your version of Partner Center</span></span>

<span data-ttu-id="20483-114">Niektóre wersje Centrum partnerskiego nie mają dostępnego całego zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="20483-114">Some versions of Partner Center do not have the entire SDK available.</span></span> <span data-ttu-id="20483-115">Aby uzyskać więcej informacji, zobacz [Tworzenie aplikacji dla firm partnerskich w chmurze firmy Microsoft](developing-for-partner-center-for-microsoft-national-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="20483-115">For more information, see [Developing for Partner Center for Microsoft National Cloud](developing-for-partner-center-for-microsoft-national-cloud.md).</span></span>

## <a name="get-the-samples"></a><span data-ttu-id="20483-116">Pobierz przykłady</span><span class="sxs-lookup"><span data-stu-id="20483-116">Get the samples</span></span>

<span data-ttu-id="20483-117">Aby uzyskać więcej informacji na temat fragmentów języka C#, przykładów REST i przykładowej aplikacji, zobacz [przykłady Centrum partnerskiego](partner-center-samples.md).</span><span class="sxs-lookup"><span data-stu-id="20483-117">For more information about C# snippets, REST samples, and the sample app, see [Partner Center samples](partner-center-samples.md).</span></span>

## <a name="test-vs-production"></a><span data-ttu-id="20483-118">Test a produkcja</span><span class="sxs-lookup"><span data-stu-id="20483-118">Test vs. production</span></span>

<span data-ttu-id="20483-119">Podczas pierwszego pisania i testowania kodu, należy użyć konta piaskownicy integracji (i odpowiednich tokenów), aby nie nawiązać przypadkowo ponoszenia nowych opłat, które firma zobowiązana do płacenia.</span><span class="sxs-lookup"><span data-stu-id="20483-119">While you are initially writing and testing your code, you should use your integration sandbox account (and the corresponding tokens) so that you don't accidentally incur new charges that your company is responsible for paying.</span></span> <span data-ttu-id="20483-120">Aby uzyskać więcej informacji o tym środowisku testowym, zobacz [Konfigurowanie dostępu do interfejsu API w centrum partnerskim](set-up-api-access-in-partner-center.md).</span><span class="sxs-lookup"><span data-stu-id="20483-120">For more information about this testing environment, see [Set up API access in Partner Center](set-up-api-access-in-partner-center.md).</span></span>

<span data-ttu-id="20483-121">Gdy Twoje rozwiązanie zostanie przetestowane i będzie gotowe do użycia na rzeczywistych kontach klienta, musisz zaktualizować tokeny, aby korzystać z aplikacji klienckiej usługi Azure AD i wpisu tajnego odpowiadającego Twojemu podstawowemu kontu Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="20483-121">When your solution is tested and ready to use on real customer accounts, you'll have to update your tokens so that you're using an Azure AD client app and secret that correspond to your Primary Partner Center account.</span></span>

<span data-ttu-id="20483-122">Aby uzyskać porady i sugestie dotyczące testowania i debugowania, w tym więcej informacji na temat testów w środowisku produkcyjnym (TiP) i piaskownicy integracji, zobacz [testowanie i debugowanie](test-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="20483-122">For tips and suggestions about testing and debugging, including more information about Test-in-Production (TiP) and the Integration Sandbox, see [Test and debug](test-and-debug.md).</span></span>

## <a name="configure-your-authentication"></a><span data-ttu-id="20483-123">Konfigurowanie uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="20483-123">Configure your authentication</span></span>

<span data-ttu-id="20483-124">Aby skonfigurować uwierzytelnianie usługi Azure AD w taki sposób, aby można było używać interfejsów API Centrum partnerskiego, zobacz [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="20483-124">To configure your Azure AD authentication so that you can use the Partner Center APIs, see [Partner Center authentication](partner-center-authentication.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20483-125">Firma Microsoft wprowadza bezpieczną i skalowalną platformę do uwierzytelniania partnerów dostawcy rozwiązań w chmurze (CSP) i dostawców panelu sterowania (CPV) za pomocą Microsoft Azure architekturę uwierzytelniania wieloskładnikowego (MFA).</span><span class="sxs-lookup"><span data-stu-id="20483-125">Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure multi-factor authentication (MFA) architecture.</span></span>
<span data-ttu-id="20483-126">Centrum partnerskie używa usługi Azure AD do uwierzytelniania i korzystania z interfejsów API Centrum partnerskiego należy prawidłowo skonfigurować ustawienia uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="20483-126">Partner Center uses Azure AD for authentication, and to use the Partner Center APIs you must configure your authentication settings correctly.</span></span>
>
> <span data-ttu-id="20483-127">Aby uzyskać więcej informacji, zobacz [Włączanie bezpiecznego modelu aplikacji](enable-secure-app-model.md).</span><span class="sxs-lookup"><span data-stu-id="20483-127">For more information, see [Enable secure application model](enable-secure-app-model.md).</span></span>

## <a name="get-help"></a><span data-ttu-id="20483-128">Uzyskaj pomoc</span><span class="sxs-lookup"><span data-stu-id="20483-128">Get help</span></span>

<span data-ttu-id="20483-129">Partnerzy mogą uzyskać pomoc techniczną w [grupie yammera zestawu SDK Centrum partnerskiego](https://go.microsoft.com/fwlink/p/?LinkID=717360).</span><span class="sxs-lookup"><span data-stu-id="20483-129">Partners can get support at the [Partner Center SDK Yammer group](https://go.microsoft.com/fwlink/p/?LinkID=717360).</span></span> <span data-ttu-id="20483-130">Aby uzyskać bardziej spersonalizowaną pomoc, deweloperzy mogą korzystać z korzyści z pomocy technicznej MPN lub pomoc techniczna Premium.</span><span class="sxs-lookup"><span data-stu-id="20483-130">To get more personalized help, developers can use their MPN support benefits or Premier Support.</span></span>

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a><span data-ttu-id="20483-131">Dołącz do programu wczesnych użytkowników w interfejsu API i zestawu SDK Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="20483-131">Join the Partner Center API and SDK Early Adopter Program</span></span>

<span data-ttu-id="20483-132">Aby dowiedzieć się, w jaki sposób można współpracować z firmą Microsoft w zakresie opracowywania funkcji i możliwości partnerów, zobacz [dodatek do interfejsu API Centrum partnerskiego i zestawu SDK wczesnego oprogramowania do wdrażania](early-adopter-program.md).</span><span class="sxs-lookup"><span data-stu-id="20483-132">To find out how you can collaborate with Microsoft on the development of Partner features and capabilities, see [Join the Partner Center API and SDK Early Adopter Program](early-adopter-program.md).</span></span>
