---
title: Rejestrowanie szczegółów aplikacji w celu Partner Center dla chmury krajowej firmy Microsoft
description: Dowiedz się, jak i dlaczego deweloperzy aplikacji Partner Center dla chmury Microsoft National Cloud muszą zarejestrować szczegółowe informacje o swojej aplikacji w usłudze Azure AD za pośrednictwem Azure Portal.
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 93d46a17bc26e9586e5e773bdf934653a571367f
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973455"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud-through-the-azure-portal"></a><span data-ttu-id="a690a-103">Rejestrowanie szczegółów aplikacji na Partner Center dla chmury microsoft national za pośrednictwem witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a690a-103">Register app details for Partner Center for Microsoft National Cloud through the Azure portal</span></span>

<span data-ttu-id="a690a-104">**Dotyczy:** Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a690a-104">**Applies to**: Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a690a-105">Deweloperzy muszą zarejestrować szczegółowe informacje o swojej aplikacji w usłudze Azure AD za pośrednictwem Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a690a-105">Developers must register details about their app with Azure AD through the Azure portal.</span></span> <span data-ttu-id="a690a-106">Dzięki temu tylko określone aplikacje będą mogły łączyć się z danymi partnera i klienta.</span><span class="sxs-lookup"><span data-stu-id="a690a-106">This helps ensure that only specified apps are able to connect to partner and customer data.</span></span>

<span data-ttu-id="a690a-107">W Partner Center dla Microsoft Cloud for US Government obecnie musisz zarządzać aplikacjami za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a690a-107">For Partner Center for Microsoft Cloud for US Government, you currently must manage apps through PowerShell.</span></span> <span data-ttu-id="a690a-108">Aby uzyskać więcej informacji, zobacz [dokumentację Azure PowerShell dokumentacji.](/powershell/module/Azuread/#applications)</span><span class="sxs-lookup"><span data-stu-id="a690a-108">For more information, see the [Azure PowerShell reference documentation](/powershell/module/Azuread/#applications).</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="a690a-109">Podczas tworzenia aplikacji dla usługi Microsoft Cloud (Niemcy) lub Partner Center for Partner Center for Microsoft Cloud for US Government należy pamiętać o następujących dodatkowych wymaganiach.</span><span class="sxs-lookup"><span data-stu-id="a690a-109">Be aware of the following additional requirements when you create an app for Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government.</span></span>

## <a name="web-apps"></a><span data-ttu-id="a690a-110">Aplikacje internetowe</span><span class="sxs-lookup"><span data-stu-id="a690a-110">Web apps</span></span>

<span data-ttu-id="a690a-111">W przypadku aplikacji internetowych użyj poniższych procedur, aby zarejestrować identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a690a-111">For web apps, use the following procedures to register your application ID.</span></span>

### <a name="create-or-update-web-app"></a><span data-ttu-id="a690a-112">Tworzenie lub aktualizowanie aplikacji internetowej</span><span class="sxs-lookup"><span data-stu-id="a690a-112">Create or update web app</span></span>

1. <span data-ttu-id="a690a-113">Przejdź do [strony Azure Portal — Rejestracje aplikacji,](https://go.microsoft.com/fwlink/?linkid=2083908) aby zarejestrować aplikację.</span><span class="sxs-lookup"><span data-stu-id="a690a-113">Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app.</span></span> <span data-ttu-id="a690a-114">Zaloguj się do witryny Azure Portal przy użyciu służbowego lub osobistego konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a690a-114">Sign in to the Azure portal using either a work or school account or a personal Microsoft account.</span></span>

2. <span data-ttu-id="a690a-115">Wybierz **pozycję Nowa rejestracja.**</span><span class="sxs-lookup"><span data-stu-id="a690a-115">Select **New registration**.</span></span> <span data-ttu-id="a690a-116">Aby uzyskać więcej informacji, zobacz [Szybki start: rejestrowanie aplikacji za pomocą Platforma tożsamości Microsoft](/azure/active-directory/develop/quickstart-register-app).</span><span class="sxs-lookup"><span data-stu-id="a690a-116">For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span></span>

### <a name="configure-api-access-permissions-for-web-app"></a><span data-ttu-id="a690a-117">Konfigurowanie uprawnień dostępu do interfejsu API dla aplikacji internetowej</span><span class="sxs-lookup"><span data-stu-id="a690a-117">Configure API access permissions for web app</span></span>

1. <span data-ttu-id="a690a-118">Wybierz aplikację.</span><span class="sxs-lookup"><span data-stu-id="a690a-118">Choose your app.</span></span> <span data-ttu-id="a690a-119">Przejdź do **Ustawienia** aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="a690a-119">Go to **Settings** of the Web app.</span></span>

2. <span data-ttu-id="a690a-120">W **sekcji Dostęp do interfejsu API** wybierz pozycję Wymagane **uprawnienia**</span><span class="sxs-lookup"><span data-stu-id="a690a-120">In **API Access** section, choose **Required permissions**</span></span>

3. <span data-ttu-id="a690a-121">Aby uzyskać Windows uprawnień usługi Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="a690a-121">For Windows Azure Active directory permissions:</span></span>

    1. <span data-ttu-id="a690a-122">Wybierz **Windows Azure Active Directory uprawnień.**</span><span class="sxs-lookup"><span data-stu-id="a690a-122">Choose **Windows Azure Active Directory permissions**.</span></span>

    2. <span data-ttu-id="a690a-123">W **uprawnienia aplikacji**, wybierz odczytu danych katalogu.</span><span class="sxs-lookup"><span data-stu-id="a690a-123">In **Applications permissions**, select Read directory data.</span></span>

    3. <span data-ttu-id="a690a-124">Zapisz uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="a690a-124">Save the permissions.</span></span>

4. <span data-ttu-id="a690a-125">Zanotuj identyfikator aplikacji **w sekcji** Właściwości aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="a690a-125">Note the application ID in the **Properties** section of your web app.</span></span>

### <a name="add-a-secret-key-to-your-app"></a><span data-ttu-id="a690a-126">Dodawanie klucza tajnego do aplikacji</span><span class="sxs-lookup"><span data-stu-id="a690a-126">Add a secret key to your app</span></span>

1. <span data-ttu-id="a690a-127">Przejdź do **sekcji Klucze** aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="a690a-127">Go to the **Keys** section of your web app.</span></span>

2. <span data-ttu-id="a690a-128">Wprowadź opis klucza i wybierz czas trwania na 1 lub 2 lata, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="a690a-128">Enter key description and select duration as 1 or 2 years, as you need.</span></span>

3. <span data-ttu-id="a690a-129">Zapisz i skopiuj wartość klucza tajnego.</span><span class="sxs-lookup"><span data-stu-id="a690a-129">Save and copy the secret key value.</span></span> <span data-ttu-id="a690a-130">**Ta wartość nie zostanie ponownie pokazana po opuszczeniu tej strony.**</span><span class="sxs-lookup"><span data-stu-id="a690a-130">**This value will not be shown again once you leave this page.**</span></span>

<span data-ttu-id="a690a-131">Konfiguracja aplikacji internetowej powinna mieć następujące szczegóły:</span><span class="sxs-lookup"><span data-stu-id="a690a-131">You should have the following details from the web app configuration:</span></span>

- <span data-ttu-id="a690a-132">Identyfikator aplikacji</span><span class="sxs-lookup"><span data-stu-id="a690a-132">Application ID</span></span>
- <span data-ttu-id="a690a-133">Klucz tajny aplikacji</span><span class="sxs-lookup"><span data-stu-id="a690a-133">Application secret</span></span>

### <a name="register-the-web-app-in-partner-center"></a><span data-ttu-id="a690a-134">Rejestrowanie aplikacji internetowej w Partner Center</span><span class="sxs-lookup"><span data-stu-id="a690a-134">Register the Web app in Partner Center</span></span>

1. <span data-ttu-id="a690a-135">Zaloguj się do witryny [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="a690a-135">Sign in to [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com).</span></span>

2. <span data-ttu-id="a690a-136">Wybierz **pozycję Pulpit nawigacyjny,** a następnie **wybierz pozycję Ustawienia,** a następnie wybierz **pozycję Zarządzanie aplikacją.**</span><span class="sxs-lookup"><span data-stu-id="a690a-136">Choose **Dashboard**, then choose **Account Settings**, then choose **App Management**.</span></span>

3. <span data-ttu-id="a690a-137">W sekcji **Aplikacja internetowa** wybierz pozycję **Zarejestruj istniejącą aplikację.**</span><span class="sxs-lookup"><span data-stu-id="a690a-137">In the **Web App** section, choose **Register existing app**.</span></span>

4. <span data-ttu-id="a690a-138">Wybierz aplikację internetową utworzoną w Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a690a-138">Select the web app you created in Azure portal.</span></span>

5. <span data-ttu-id="a690a-139">Wybierz **pozycję Zarejestruj aplikację.**</span><span class="sxs-lookup"><span data-stu-id="a690a-139">Choose **register your app**.</span></span>

## <a name="native-apps"></a><span data-ttu-id="a690a-140">Aplikacje natywne</span><span class="sxs-lookup"><span data-stu-id="a690a-140">Native apps</span></span>

<span data-ttu-id="a690a-141">Aplikacje natywne nie muszą być zarejestrowane w Partner Center.</span><span class="sxs-lookup"><span data-stu-id="a690a-141">Native apps do not need to be registered to Partner Center.</span></span> <span data-ttu-id="a690a-142">Jednak te aplikacje należy skonfigurować tak, aby zapewniały dostęp do Partner Center API.</span><span class="sxs-lookup"><span data-stu-id="a690a-142">But these apps need to be configured to provide access to Partner Center APIs.</span></span>

>[!NOTE]
><span data-ttu-id="a690a-143">Przed utworzeniem aplikacji natywnej w Azure Portal zaloguj się do usługi Partner Center przy użyciu poświadczeń użytkownika administratora z dzierżawy partnera.</span><span class="sxs-lookup"><span data-stu-id="a690a-143">Before creating a native app in the Azure portal, log in into Partner Center using the admin user credentials from the partner tenant.</span></span> <span data-ttu-id="a690a-144">Powoduje to utworzenie ustawień w dzierżawie w celu włączenia uprawnień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a690a-144">This creates the settings on the tenant to enable app permissions.</span></span>

### <a name="create-native-app"></a><span data-ttu-id="a690a-145">Tworzenie aplikacji natywnej</span><span class="sxs-lookup"><span data-stu-id="a690a-145">Create native app</span></span>

1. <span data-ttu-id="a690a-146">Przejdź do [strony Azure Portal — Rejestracje aplikacji,](https://go.microsoft.com/fwlink/?linkid=2083908) aby zarejestrować aplikację.</span><span class="sxs-lookup"><span data-stu-id="a690a-146">Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app.</span></span> <span data-ttu-id="a690a-147">Zaloguj się do witryny Azure Portal przy użyciu służbowego lub osobistego konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a690a-147">Sign in to the Azure portal using either a work or school account or a personal Microsoft account.</span></span>

2. <span data-ttu-id="a690a-148">Wybierz **pozycję Nowa rejestracja.**</span><span class="sxs-lookup"><span data-stu-id="a690a-148">Select **New registration**.</span></span> <span data-ttu-id="a690a-149">Aby uzyskać więcej informacji, zobacz [Szybki start: rejestrowanie aplikacji za pomocą Platforma tożsamości Microsoft](/azure/active-directory/develop/quickstart-register-app).</span><span class="sxs-lookup"><span data-stu-id="a690a-149">For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span></span>

### <a name="configure-api-access-permissions-for-native-app"></a><span data-ttu-id="a690a-150">Konfigurowanie uprawnień dostępu interfejsu API dla aplikacji natywnej</span><span class="sxs-lookup"><span data-stu-id="a690a-150">Configure API access permissions for native app</span></span>

1. <span data-ttu-id="a690a-151">Wybierz aplikację.</span><span class="sxs-lookup"><span data-stu-id="a690a-151">Choose your app.</span></span> <span data-ttu-id="a690a-152">Przejdź do obszaru **Settings** (Ustawienia).</span><span class="sxs-lookup"><span data-stu-id="a690a-152">Go to **Settings**.</span></span>

2. <span data-ttu-id="a690a-153">W dostępie do interfejsu API wybierz **pozycję Wymagane uprawnienia.**</span><span class="sxs-lookup"><span data-stu-id="a690a-153">In API Access, choose **Required permissions**.</span></span>

3. <span data-ttu-id="a690a-154">Wybierz **Windows Azure Active Directory uprawnień.**</span><span class="sxs-lookup"><span data-stu-id="a690a-154">Choose **Windows Azure Active Directory permissions**.</span></span> <span data-ttu-id="a690a-155">W **uprawnienia delegowane**, wybierz te uprawnienia:</span><span class="sxs-lookup"><span data-stu-id="a690a-155">In **Delegated permissions**, select these permissions:</span></span>

    - <span data-ttu-id="a690a-156">**Logowanie i odczyt profilu użytkownika**</span><span class="sxs-lookup"><span data-stu-id="a690a-156">**Sign in and read user profile**</span></span>
    - <span data-ttu-id="a690a-157">**Odczyt danych katalogu**</span><span class="sxs-lookup"><span data-stu-id="a690a-157">**Read directory data**</span></span>
    - <span data-ttu-id="a690a-158">**Dostęp do katalogu jako zalogowany użytkownik**</span><span class="sxs-lookup"><span data-stu-id="a690a-158">**Access the directory as the signed-in user**</span></span>
    - <span data-ttu-id="a690a-159">**Odczytywanie wszystkich grup**</span><span class="sxs-lookup"><span data-stu-id="a690a-159">**Read all groups**</span></span>

4. <span data-ttu-id="a690a-160">Zapisz uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="a690a-160">Save the permissions.</span></span>

5. <span data-ttu-id="a690a-161">Wybierz **pozycję Dodaj** w opcji Wymagane **uprawnienia.**</span><span class="sxs-lookup"><span data-stu-id="a690a-161">Choose **Add** in **Required permissions**.</span></span>

6. <span data-ttu-id="a690a-162">Wybierz pozycję **Wybierz interfejs API**.</span><span class="sxs-lookup"><span data-stu-id="a690a-162">Choose **Select an API**.</span></span>

    1. <span data-ttu-id="a690a-163">W polu wyszukiwania wprowadź nazwę **Microsoft Partner Center** i wybierz ją z listy wyników.</span><span class="sxs-lookup"><span data-stu-id="a690a-163">In the search box, enter **Microsoft Partner Center** and select it from the results list.</span></span>

    2. <span data-ttu-id="a690a-164">Wybierz pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="a690a-164">Choose **Select**.</span></span>

7. <span data-ttu-id="a690a-165">Wybierz pozycję **Wybierz uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="a690a-165">Choose **Select permissions**.</span></span>

    1. <span data-ttu-id="a690a-166">Wybierz **pozycję Dostęp Partner Center PPE.**</span><span class="sxs-lookup"><span data-stu-id="a690a-166">Select **Access Partner Center PPE**.</span></span>
    
    2. <span data-ttu-id="a690a-167">Wybierz pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="a690a-167">Choose **Select**.</span></span>

8. <span data-ttu-id="a690a-168">Wybierz pozycję **Gotowe**.</span><span class="sxs-lookup"><span data-stu-id="a690a-168">Choose **Done**.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="a690a-169">Zanotuj identyfikator aplikacji we właściwościach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a690a-169">Note the application ID in the Properties of your app.</span></span>

<span data-ttu-id="a690a-170">Nie musisz rejestrować aplikacji natywnych w Partner Center, ale aplikacja natywna musi być za zgodą administratora.</span><span class="sxs-lookup"><span data-stu-id="a690a-170">You do not need to register native apps in Partner Center, however the native app must be admin consented.</span></span> <span data-ttu-id="a690a-171">Zanotuj identyfikator aplikacji natywnej.</span><span class="sxs-lookup"><span data-stu-id="a690a-171">Note the application ID of your native app.</span></span>
