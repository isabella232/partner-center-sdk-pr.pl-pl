---
title: Rejestrowanie szczegółów aplikacji dla Centrum partnerskiego w chmurze krajowej firmy Microsoft
description: Dowiedz się, jak i dlaczego deweloperzy aplikacji dla Centrum partnerskiego w chmurze firmy Microsoft muszą rejestrować szczegółowe informacje o swojej aplikacji za pomocą usługi Azure AD za pomocą Azure Portal.
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 887cb71c752ac5d9c61398536711545c19cc7600
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770147"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud-through-the-azure-portal"></a><span data-ttu-id="25f7a-103">Rejestrowanie szczegółowych informacji o aplikacji dla Centrum partnerskiego w chmurze krajowej firmy Microsoft za pomocą Azure Portal</span><span class="sxs-lookup"><span data-stu-id="25f7a-103">Register app details for Partner Center for Microsoft National Cloud through the Azure portal</span></span>

<span data-ttu-id="25f7a-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="25f7a-104">**Applies to:**</span></span>

- <span data-ttu-id="25f7a-105">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="25f7a-105">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="25f7a-106">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="25f7a-106">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="25f7a-107">Deweloperzy muszą rejestrować szczegółowe informacje o swojej aplikacji za pomocą usługi Azure AD za pomocą Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="25f7a-107">Developers must register details about their app with Azure AD through the Azure portal.</span></span> <span data-ttu-id="25f7a-108">Pozwala to zagwarantować, że tylko określone aplikacje będą mogły łączyć się z danymi partnera i klienta.</span><span class="sxs-lookup"><span data-stu-id="25f7a-108">This helps ensure that only specified apps are able to connect to partner and customer data.</span></span>

<span data-ttu-id="25f7a-109">Centrum partnerskie dla Microsoft Cloud dla instytucji rządowych USA wymaga obecnie zarządzania aplikacjami za poorednictwem programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25f7a-109">For Partner Center for Microsoft Cloud for US Government, you currently must manage apps through PowerShell.</span></span> <span data-ttu-id="25f7a-110">Aby uzyskać więcej informacji, zobacz [dokumentację referencyjną Azure PowerShell](/powershell/module/Azuread/#applications).</span><span class="sxs-lookup"><span data-stu-id="25f7a-110">For more information, see the [Azure PowerShell reference documentation](/powershell/module/Azuread/#applications).</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="25f7a-111">Należy pamiętać o następujących dodatkowych wymaganiach podczas tworzenia aplikacji dla Centrum partnerskiego na Microsoft Cloud Niemcy lub centrum partnerskie dla Microsoft Cloud dla instytucji rządowych USA.</span><span class="sxs-lookup"><span data-stu-id="25f7a-111">Be aware of the following additional requirements when you create an app for Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government.</span></span>

## <a name="web-apps"></a><span data-ttu-id="25f7a-112">Aplikacje internetowe</span><span class="sxs-lookup"><span data-stu-id="25f7a-112">Web apps</span></span>

<span data-ttu-id="25f7a-113">W przypadku usługi Web Apps wykonaj następujące procedury, aby zarejestrować identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25f7a-113">For web apps, use the following procedures to register your application ID.</span></span>

### <a name="create-or-update-web-app"></a><span data-ttu-id="25f7a-114">Utwórz lub zaktualizuj aplikację sieci Web</span><span class="sxs-lookup"><span data-stu-id="25f7a-114">Create or update web app</span></span>

1. <span data-ttu-id="25f7a-115">Przejdź do strony [Rejestracje aplikacji Azure Portal](https://go.microsoft.com/fwlink/?linkid=2083908) , aby zarejestrować aplikację.</span><span class="sxs-lookup"><span data-stu-id="25f7a-115">Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app.</span></span> <span data-ttu-id="25f7a-116">Zaloguj się do witryny Azure Portal przy użyciu służbowego lub osobistego konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="25f7a-116">Sign in to the Azure portal using either a work or school account or a personal Microsoft account.</span></span>

2. <span data-ttu-id="25f7a-117">Wybierz pozycję **Nowa rejestracja**.</span><span class="sxs-lookup"><span data-stu-id="25f7a-117">Select **New registration**.</span></span> <span data-ttu-id="25f7a-118">Aby uzyskać więcej informacji, zobacz [Szybki Start: rejestrowanie aplikacji na platformie tożsamości firmy Microsoft](/azure/active-directory/develop/quickstart-register-app).</span><span class="sxs-lookup"><span data-stu-id="25f7a-118">For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span></span>

### <a name="configure-api-access-permissions-for-web-app"></a><span data-ttu-id="25f7a-119">Konfigurowanie uprawnień dostępu do interfejsu API dla aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="25f7a-119">Configure API access permissions for web app</span></span>

1. <span data-ttu-id="25f7a-120">Wybierz aplikację.</span><span class="sxs-lookup"><span data-stu-id="25f7a-120">Choose your app.</span></span> <span data-ttu-id="25f7a-121">Przejdź do pozycji **Ustawienia** aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="25f7a-121">Go to **Settings** of the Web app.</span></span>

2. <span data-ttu-id="25f7a-122">W sekcji **dostęp do interfejsu API** wybierz **wymagane uprawnienia**</span><span class="sxs-lookup"><span data-stu-id="25f7a-122">In **API Access** section, choose **Required permissions**</span></span>

3. <span data-ttu-id="25f7a-123">W przypadku uprawnień usługi Windows Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="25f7a-123">For Windows Azure Active directory permissions:</span></span>

    1. <span data-ttu-id="25f7a-124">Wybierz **uprawnienia Azure Active Directory systemu Windows**.</span><span class="sxs-lookup"><span data-stu-id="25f7a-124">Choose **Windows Azure Active Directory permissions**.</span></span>

    2. <span data-ttu-id="25f7a-125">W obszarze **uprawnienia aplikacji** wybierz pozycję Odczytaj dane katalogu.</span><span class="sxs-lookup"><span data-stu-id="25f7a-125">In **Applications permissions**, select Read directory data.</span></span>

    3. <span data-ttu-id="25f7a-126">Zapisz uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="25f7a-126">Save the permissions.</span></span>

4. <span data-ttu-id="25f7a-127">Zanotuj identyfikator aplikacji w sekcji **Właściwości** aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="25f7a-127">Note the application ID in the **Properties** section of your web app.</span></span>

### <a name="add-a-secret-key-to-your-app"></a><span data-ttu-id="25f7a-128">Dodawanie klucza tajnego do aplikacji</span><span class="sxs-lookup"><span data-stu-id="25f7a-128">Add a secret key to your app</span></span>

1. <span data-ttu-id="25f7a-129">Przejdź do sekcji **klucze** aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="25f7a-129">Go to the **Keys** section of your web app.</span></span>

2. <span data-ttu-id="25f7a-130">Wprowadź opis klucza i wybierz czas trwania w zakresie od 1 do 2 lat, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="25f7a-130">Enter key description and select duration as 1 or 2 years, as you need.</span></span>

3. <span data-ttu-id="25f7a-131">Zapisz i skopiuj wartość klucza tajnego.</span><span class="sxs-lookup"><span data-stu-id="25f7a-131">Save and copy the secret key value.</span></span> <span data-ttu-id="25f7a-132">**Ta wartość nie będzie ponownie wyświetlana po opuszczeniu tej strony.**</span><span class="sxs-lookup"><span data-stu-id="25f7a-132">**This value will not be shown again once you leave this page.**</span></span>

<span data-ttu-id="25f7a-133">W konfiguracji aplikacji sieci Web powinny znajdować się następujące szczegółowe informacje:</span><span class="sxs-lookup"><span data-stu-id="25f7a-133">You should have the following details from the web app configuration:</span></span>

- <span data-ttu-id="25f7a-134">Identyfikator aplikacji</span><span class="sxs-lookup"><span data-stu-id="25f7a-134">Application ID</span></span>
- <span data-ttu-id="25f7a-135">Klucz tajny aplikacji</span><span class="sxs-lookup"><span data-stu-id="25f7a-135">Application secret</span></span>

### <a name="register-the-web-app-in-partner-center"></a><span data-ttu-id="25f7a-136">Rejestrowanie aplikacji sieci Web w centrum partnerskim</span><span class="sxs-lookup"><span data-stu-id="25f7a-136">Register the Web app in Partner Center</span></span>

1. <span data-ttu-id="25f7a-137">Zaloguj się do [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com) .</span><span class="sxs-lookup"><span data-stu-id="25f7a-137">Log in to [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com).</span></span>

2. <span data-ttu-id="25f7a-138">Wybierz pozycję **pulpit nawigacyjny**, a następnie wybierz pozycję **Ustawienia konta**, a następnie wybierz pozycję **Zarządzanie aplikacjami**.</span><span class="sxs-lookup"><span data-stu-id="25f7a-138">Choose **Dashboard**, then choose **Account Settings**, then choose **App Management**.</span></span>

3. <span data-ttu-id="25f7a-139">W sekcji **aplikacja sieci Web** wybierz pozycję **zarejestruj istniejącą aplikację**.</span><span class="sxs-lookup"><span data-stu-id="25f7a-139">In the **Web App** section, choose **Register existing app**.</span></span>

4. <span data-ttu-id="25f7a-140">Wybierz aplikację sieci Web utworzoną w Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="25f7a-140">Select the web app you created in Azure portal.</span></span>

5. <span data-ttu-id="25f7a-141">Wybierz pozycję **zarejestruj aplikację**.</span><span class="sxs-lookup"><span data-stu-id="25f7a-141">Choose **register your app**.</span></span>

## <a name="native-apps"></a><span data-ttu-id="25f7a-142">Aplikacje natywne</span><span class="sxs-lookup"><span data-stu-id="25f7a-142">Native apps</span></span>

<span data-ttu-id="25f7a-143">Aplikacje natywne nie muszą być zarejestrowane w centrum partnerskim.</span><span class="sxs-lookup"><span data-stu-id="25f7a-143">Native apps do not need to be registered to Partner Center.</span></span> <span data-ttu-id="25f7a-144">Jednak te aplikacje muszą być skonfigurowane w taki sposób, aby zapewnić dostęp do interfejsów API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="25f7a-144">But these apps need to be configured to provide access to Partner Center APIs.</span></span>

>[!NOTE]
><span data-ttu-id="25f7a-145">Przed utworzeniem aplikacji natywnej w Azure Portal Zaloguj się do Centrum partnerskiego przy użyciu poświadczeń użytkownika administratora z dzierżawy partnerskiej.</span><span class="sxs-lookup"><span data-stu-id="25f7a-145">Before creating a native app in the Azure portal, log in into Partner Center using the admin user credentials from the partner tenant.</span></span> <span data-ttu-id="25f7a-146">Spowoduje to utworzenie ustawień dzierżawy w celu włączenia uprawnień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25f7a-146">This creates the settings on the tenant to enable app permissions.</span></span>

### <a name="create-native-app"></a><span data-ttu-id="25f7a-147">Tworzenie aplikacji natywnej</span><span class="sxs-lookup"><span data-stu-id="25f7a-147">Create native app</span></span>

1. <span data-ttu-id="25f7a-148">Przejdź do strony [Rejestracje aplikacji Azure Portal](https://go.microsoft.com/fwlink/?linkid=2083908) , aby zarejestrować aplikację.</span><span class="sxs-lookup"><span data-stu-id="25f7a-148">Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app.</span></span> <span data-ttu-id="25f7a-149">Zaloguj się do witryny Azure Portal przy użyciu służbowego lub osobistego konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="25f7a-149">Sign in to the Azure portal using either a work or school account or a personal Microsoft account.</span></span>

2. <span data-ttu-id="25f7a-150">Wybierz pozycję **Nowa rejestracja**.</span><span class="sxs-lookup"><span data-stu-id="25f7a-150">Select **New registration**.</span></span> <span data-ttu-id="25f7a-151">Aby uzyskać więcej informacji, zobacz [Szybki Start: rejestrowanie aplikacji na platformie tożsamości firmy Microsoft](/azure/active-directory/develop/quickstart-register-app).</span><span class="sxs-lookup"><span data-stu-id="25f7a-151">For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span></span>

### <a name="configure-api-access-permissions-for-native-app"></a><span data-ttu-id="25f7a-152">Konfigurowanie uprawnień dostępu do interfejsu API dla aplikacji natywnej</span><span class="sxs-lookup"><span data-stu-id="25f7a-152">Configure API access permissions for native app</span></span>

1. <span data-ttu-id="25f7a-153">Wybierz aplikację.</span><span class="sxs-lookup"><span data-stu-id="25f7a-153">Choose your app.</span></span> <span data-ttu-id="25f7a-154">Przejdź do obszaru **Settings** (Ustawienia).</span><span class="sxs-lookup"><span data-stu-id="25f7a-154">Go to **Settings**.</span></span>

2. <span data-ttu-id="25f7a-155">W obszarze dostęp do interfejsu API wybierz pozycję **wymagane uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="25f7a-155">In API Access, choose **Required permissions**.</span></span>

3. <span data-ttu-id="25f7a-156">Wybierz **uprawnienia Azure Active Directory systemu Windows**.</span><span class="sxs-lookup"><span data-stu-id="25f7a-156">Choose **Windows Azure Active Directory permissions**.</span></span> <span data-ttu-id="25f7a-157">W obszarze **uprawnienia delegowane** wybierz następujące uprawnienia:</span><span class="sxs-lookup"><span data-stu-id="25f7a-157">In **Delegated permissions**, select these permissions:</span></span>

    - <span data-ttu-id="25f7a-158">**Logowanie i odczyt profilu użytkownika**</span><span class="sxs-lookup"><span data-stu-id="25f7a-158">**Sign in and read user profile**</span></span>
    - <span data-ttu-id="25f7a-159">**Odczyt danych katalogu**</span><span class="sxs-lookup"><span data-stu-id="25f7a-159">**Read directory data**</span></span>
    - <span data-ttu-id="25f7a-160">**Dostęp do katalogu jako zalogowany użytkownik**</span><span class="sxs-lookup"><span data-stu-id="25f7a-160">**Access the directory as the signed-in user**</span></span>
    - <span data-ttu-id="25f7a-161">**Odczytuj wszystkie grupy**</span><span class="sxs-lookup"><span data-stu-id="25f7a-161">**Read all groups**</span></span>

4. <span data-ttu-id="25f7a-162">Zapisz uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="25f7a-162">Save the permissions.</span></span>

5. <span data-ttu-id="25f7a-163">Wybierz pozycję **Dodaj** w obszarze **wymagane uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="25f7a-163">Choose **Add** in **Required permissions**.</span></span>

6. <span data-ttu-id="25f7a-164">Wybierz pozycję **Wybierz interfejs API**.</span><span class="sxs-lookup"><span data-stu-id="25f7a-164">Choose **Select an API**.</span></span>

    1. <span data-ttu-id="25f7a-165">W polu wyszukiwania wprowadź **Centrum partnerskie firmy Microsoft** i wybierz je z listy wyników.</span><span class="sxs-lookup"><span data-stu-id="25f7a-165">In the search box, enter **Microsoft Partner Center** and select it from the results list.</span></span>

    2. <span data-ttu-id="25f7a-166">Wybierz pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="25f7a-166">Choose **Select**.</span></span>

7. <span data-ttu-id="25f7a-167">Wybierz pozycję **Wybierz uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="25f7a-167">Choose **Select permissions**.</span></span>

    1. <span data-ttu-id="25f7a-168">Wybierz pozycję **Access partner centrum ŚOI**.</span><span class="sxs-lookup"><span data-stu-id="25f7a-168">Select **Access Partner Center PPE**.</span></span>
    
    2. <span data-ttu-id="25f7a-169">Wybierz pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="25f7a-169">Choose **Select**.</span></span>

8. <span data-ttu-id="25f7a-170">Wybierz pozycję **Gotowe**.</span><span class="sxs-lookup"><span data-stu-id="25f7a-170">Choose **Done**.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="25f7a-171">Zanotuj identyfikator aplikacji we właściwościach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25f7a-171">Note the application ID in the Properties of your app.</span></span>

<span data-ttu-id="25f7a-172">Nie musisz rejestrować natywnych aplikacji w centrum partnerskim, jednak aplikacja natywna musi być zgodna z administratorem.</span><span class="sxs-lookup"><span data-stu-id="25f7a-172">You do not need to register native apps in Partner Center, however the native app must be admin consented .</span></span> <span data-ttu-id="25f7a-173">Zanotuj identyfikator aplikacji w aplikacji natywnej.</span><span class="sxs-lookup"><span data-stu-id="25f7a-173">Note the application ID of your native app.</span></span>
