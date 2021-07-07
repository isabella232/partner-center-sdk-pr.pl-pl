---
title: Możliwości dostawcy pośredniego CSP w piaskownicy
description: Dostawcy pośredni mogą tworzyć pośrednich odsprzedawców w piaskownicy do celów testowych.
ms.date: 05/20/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vinayks-ms
ms.author: vinayks
ms.openlocfilehash: da35dadd4e13247e923259a1cf3a67852f4b9e00
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445905"
---
# <a name="csp-indirect-provider-sandbox-capabilities-for-creating-indirect-reseller-accounts"></a><span data-ttu-id="a0ef5-103">Możliwości piaskownicy dostawcy pośredniego dostawcy CSP do tworzenia kont odsprzedawcy pośredniego</span><span class="sxs-lookup"><span data-stu-id="a0ef5-103">CSP Indirect provider sandbox capabilities for creating Indirect reseller accounts</span></span> 

<span data-ttu-id="a0ef5-104">**Odpowiednie role:** Dostawca pośredni</span><span class="sxs-lookup"><span data-stu-id="a0ef5-104">**Appropriate roles**: Indirect provider</span></span>

<span data-ttu-id="a0ef5-105">Dostawcy pośredni dostawcy CSP mogą utworzyć CSP Indirect Reseller piaskownicy za pośrednictwem własnego konta piaskownicy warstwy 2 w Partner Center Portal.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-105">CSP Indirect Providers can create a CSP Indirect Reseller Sandbox account via through their own Tier 2 Sandbox account in Partner Center portal.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a0ef5-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a0ef5-106">Prerequisites</span></span> 

<span data-ttu-id="a0ef5-107">Partner Center poświadczeń piaskownicy dostawcy pośredniego (warstwa 2).</span><span class="sxs-lookup"><span data-stu-id="a0ef5-107">Partner Center Indirect Provider (Tier 2) sandbox credentials.</span></span> <span data-ttu-id="a0ef5-108">Scenariusz piaskownicy obsługuje uwierzytelnianie zarówno przy użyciu autonomicznej aplikacji, jak i poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-108">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span> 
 

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a><span data-ttu-id="a0ef5-109">Dostawca pośredni piaskownicy — tworzenie odsprzedawcy pośredniego piaskownicy przy Partner Center interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="a0ef5-109">Sandbox Indirect Provider – Create Sandbox Indirect Reseller using the Partner Center user interface</span></span> 

 <span data-ttu-id="a0ef5-110">Jest to funkcja dostępna tylko w piaskownicy, która umożliwia dostawcom pośrednim piaskownicy tworzenie konta odsprzedawcy pośredniego piaskownicy za pośrednictwem Partner Center portalu.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-110">This is a Sandbox-only feature that allows Sandbox Indirect Providers the ability to create a Sandbox Indirect Reseller account through the Partner Center portal.</span></span>

<span data-ttu-id="a0ef5-111">W następujących scenariuszach dostawcy pośredni mogą zrobić dla pośrednich odsprzedawców w piaskownicy za pośrednictwem Partner Center interfejsu użytkownika:</span><span class="sxs-lookup"><span data-stu-id="a0ef5-111">The following scenarios are what Indirect providers can do for indirect resellers in Sandbox through the Partner Center user interface:</span></span> 

1. <span data-ttu-id="a0ef5-112">Dostawcy pośredni dostawcy CSP mogą utworzyć konto CSP Indirect Reseller piaskownicy za pośrednictwem własnego konta piaskownicy warstwy 2 w Partner Center Portal.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-112">CSP Indirect Providers can create a CSP Indirect Reseller Sandbox account through their own Tier 2 Sandbox account in Partner Center portal.</span></span>
2. <span data-ttu-id="a0ef5-113">Odsprzedawcy pośredni dostawcy CSP mogą wyświetlać klientów według dostawców pośrednich.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-113">CSP Indirect Resellers can view customer by Indirect Providers.</span></span> 

1. <span data-ttu-id="a0ef5-114">Odsprzedawcy pośredni programu CSP mogą zarządzać kontem klienta przy użyciu delegowanych uprawnień administratora.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-114">CSP Indirect Resellers can manage the customer account using delegated admin permissions.</span></span>

1. <span data-ttu-id="a0ef5-115">Dostawcy pośredni dostawcy CSP mogą zapraszać pośrednich odsprzedawców CSP.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-115">CSP Indirect Providers can invite CSP Indirect Resellers.</span></span>
 
1. <span data-ttu-id="a0ef5-116">Dostawcy pośredni dostawcy CSP mogą usunąć konto CSP Indirect Reseller piaskownicy za pośrednictwem własnego konta piaskownicy warstwy 2 w Partner Center Portal.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-116">CSP Indirect Providers can delete a CSP Indirect Reseller Sandbox account through their own Tier 2 Sandbox account in Partner Center portal.</span></span>

    <span data-ttu-id="a0ef5-117">a.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-117">a.</span></span>  <span data-ttu-id="a0ef5-118">Gdy dostawca pośredni piaskownicy usunie relację z odsprzedawcą pośrednim piaskownicy, sprawdź, czy odsprzedawca pośredni ma jakiekolwiek inne relacje z innymi dostawcami.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-118">When Sandbox Indirect Provider deletes the relationship with Sandbox Indirect Reseller, check if the Indirect Reseller has any other relationship with other providers.</span></span> <span data-ttu-id="a0ef5-119">Jeśli tak, zostanie usunięta tylko relacja z tym konkretnym dostawcą pośrednim.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-119">If so, only the relationship with that specific Indirect provider will be removed.</span></span>

    <span data-ttu-id="a0ef5-120">c.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-120">c.</span></span> <span data-ttu-id="a0ef5-121">Jeśli jest to jedyna relacja odsprzedawcy pośredniego, odsprzedawca pośredni zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-121">If that is the only relationship for the Indirect Reseller, then the Indirect Reseller will be deleted.</span></span>

1. <span data-ttu-id="a0ef5-122">Dostawcy pośredni dostawcy CSP mogą usunąć CSP Indirect Reseller.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-122">CSP Indirect Providers can delete a CSP Indirect Reseller.</span></span>

    <span data-ttu-id="a0ef5-123">a.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-123">a.</span></span> <span data-ttu-id="a0ef5-124">Jest to funkcja dostępna tylko w piaskownicy, która umożliwia dostawcom pośrednim piaskownicy usuwanie odsprzedawców pośrednich piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-124">This is a Sandbox-only feature that allows Sandbox Indirect Providers the ability to delete Sandbox Indirect Resellers.</span></span>
     
1. <span data-ttu-id="a0ef5-125">Wymagania wstępne dotyczące usuwania odsprzedawcy pośredniego piaskownicy:</span><span class="sxs-lookup"><span data-stu-id="a0ef5-125">Pre-requisites for deleting a Sandbox Indirect Reseller:</span></span>

    1. <span data-ttu-id="a0ef5-126">Wstrzymaj subskrypcje dla każdego klienta odsprzedawcy pośredniego piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-126">Suspend the subscriptions for each customer of Sandbox Indirect Reseller.</span></span>

    1. <span data-ttu-id="a0ef5-127">Usuń wszystkich klientów odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-127">Delete all customers of Indirect Reseller.</span></span>

1. <span data-ttu-id="a0ef5-128">Dozwolony limit pięciu odsprzedawców pośrednich piaskownicy na dostawcę pośredniego piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-128">Limit of five Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> <span data-ttu-id="a0ef5-129">Po usunięciu odsprzedawcy pośredniego piaskownicy limit przydziału zostanie zresetowany.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-129">Once the Sandbox Indirect reseller is deleted, the quota will be reset.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="a0ef5-130">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a0ef5-130">Pre-requisites</span></span>

- <span data-ttu-id="a0ef5-131">Dozwolony limit pięciu odsprzedawców pośrednich piaskownicy na dostawcę pośredniego piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-131">Limit of five Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> 

- <span data-ttu-id="a0ef5-132">Tego samego identyfikatora MPN można użyć do utworzenia wielu kont piaskownicy odsprzedawcy pośredniego, jeśli kraj identyfikatora MPN i kraj piaskownicy odsprzedawcy pośredniego są takie same.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-132">Same MPN ID can be used to create multiple Indirect Reseller Sandbox accounts if MPN ID country and Indirect Reseller Sandbox country are same.</span></span> <span data-ttu-id="a0ef5-133">Jeśli masz dostępny testowy identyfikator MPN, możesz go użyć lub uzyskać listę identyfikatorów MPN za pośrednictwem naszego [Yammer kanału]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ).</span><span class="sxs-lookup"><span data-stu-id="a0ef5-133">If you have a test MPN ID available, you can use it, or you can get a list of MPN IDs through our [Yammer channel]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ).</span></span> <span data-ttu-id="a0ef5-134">Jeśli nie masz dostępu do Yammer, Yammer poprosi o dostęp.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-134">If you don’t have access to Yammer, Yammer will ask you to request access.</span></span>
 
- <span data-ttu-id="a0ef5-135">Tylko 75 klientów jest dozwolonych na dostawcę pośredniego piaskownicy</span><span class="sxs-lookup"><span data-stu-id="a0ef5-135">Only 75 customers are allowed per Sandbox Indirect Provider</span></span>

## <a name="create-csp-indirect-reseller-sandbox-account"></a><span data-ttu-id="a0ef5-136">Tworzenie CSP Indirect Reseller piaskownicy</span><span class="sxs-lookup"><span data-stu-id="a0ef5-136">Create CSP Indirect Reseller Sandbox account</span></span>

1. <span data-ttu-id="a0ef5-137">Zaloguj się Partner Center za pomocą konta piaskownicy warstwy 2.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-137">Sign into Partner Center via your Tier 2 Sandbox account.</span></span> 

2. <span data-ttu-id="a0ef5-138">Przejdź do pozycji Odsprzedawcy pośredni z menu po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-138">Navigate to Indirect Resellers from the left menu.</span></span> 

3. <span data-ttu-id="a0ef5-139">Wybierz przycisk **Dodaj piaskownicę odsprzedawcy.**</span><span class="sxs-lookup"><span data-stu-id="a0ef5-139">Select the **Add Reseller Sandbox** button.</span></span> 

4. <span data-ttu-id="a0ef5-140">Wypełnij formularz rejestracji konta.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-140">Fill the account enrollment form.</span></span> <span data-ttu-id="a0ef5-141">Nie wymaga to wyjaśnień, ale pamiętaj, że tworzysz konto piaskownicy dla odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-141">It's self-explanatory but remember you are creating a Sandbox account for an Indirect Reseller.</span></span> <span data-ttu-id="a0ef5-142">To konto nie zostanie poddane testowi i zostanie aktywowane zaraz po zakończeniu rejestracji konta.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-142">This account won't undergo vetting and will be activated as soon as you finish the account enrollment.</span></span>  

5. <span data-ttu-id="a0ef5-143">Po utworzeniu konta w portalu otrzymasz poświadczenia administratora globalnego dla konta piaskownicy Odsprzedawca pośredni.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-143">Once the account is created, you will get the Global Admin credentials for the Indirect Reseller sandbox account on the portal.</span></span> <span data-ttu-id="a0ef5-144">Pamiętaj, aby zapisać go natychmiast. W przeciwnym razie nie będzie można zalogować się jako piaskownica odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-144">Remember to save it immediately,  otherwise, you won't be able to sign in as an Indirect Reseller Sandbox.</span></span> 

6. <span data-ttu-id="a0ef5-145">Wyloguj się i zaloguj się ponownie Partner Center przy użyciu nowych poświadczeń dla piaskownicy odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-145">Sign out and sign in again to Partner Center using the new credentials for Indirect Reseller Sandbox.</span></span> <span data-ttu-id="a0ef5-146">Poznaj możliwości, które możesz wykonać jako odsprzedawca pośredni.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-146">Explore the capabilities you can do as an Indirect Reseller.</span></span> <span data-ttu-id="a0ef5-147">Niektóre z nich to:</span><span class="sxs-lookup"><span data-stu-id="a0ef5-147">Some things are:</span></span>  

    - <span data-ttu-id="a0ef5-148">Zarządzanie profilami</span><span class="sxs-lookup"><span data-stu-id="a0ef5-148">Manage profiles</span></span>  

    - <span data-ttu-id="a0ef5-149">Zarządzanie użytkownikami i rolami</span><span class="sxs-lookup"><span data-stu-id="a0ef5-149">Manage users and roles</span></span> 

    - <span data-ttu-id="a0ef5-150">Zarządzanie dostawcami pośrednimi</span><span class="sxs-lookup"><span data-stu-id="a0ef5-150">Manage Indirect Providers</span></span> 

    - <span data-ttu-id="a0ef5-151">Zarządzanie klientami piaskownicy CSP</span><span class="sxs-lookup"><span data-stu-id="a0ef5-151">Manage CSP Sandbox customers</span></span> 

    - <span data-ttu-id="a0ef5-152">Zarządzanie relacjami</span><span class="sxs-lookup"><span data-stu-id="a0ef5-152">Manage relationships</span></span>
    
     
## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a><span data-ttu-id="a0ef5-153">Dostawca pośredni piaskownicy — usuwanie odsprzedawcy pośredniego piaskownicy przy Partner Center interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="a0ef5-153">Sandbox Indirect Provider – Delete Sandbox Indirect Reseller using the Partner Center user interface</span></span>

 <span data-ttu-id="a0ef5-154">Jest to funkcja dostępna tylko w piaskownicy, która umożliwia dostawcom pośrednim piaskownicy usuwanie istniejącego konta odsprzedawcy pośredniego piaskownicy za pośrednictwem Partner Center portalu.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-154">This is a Sandbox only feature that allows Sandbox Indirect Providers an ability to delete an existing Sandbox Indirect Reseller account via Partner Center portal.</span></span> 

### <a name="pre-requisites-to-delete-sandbox-indirect-reseller"></a><span data-ttu-id="a0ef5-155">Wymagania wstępne usunięcia odsprzedawcy pośredniego piaskownicy:</span><span class="sxs-lookup"><span data-stu-id="a0ef5-155">Pre-requisites to delete sandbox Indirect reseller:</span></span>

<span data-ttu-id="a0ef5-156">Istniejące konto CSP Indirect Reseller piaskownicy skojarzone z Twoim własnym kontem CSP Indirect Provider piaskownicy warstwy 2.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-156">An existing CSP Indirect Reseller Sandbox account associated with your own CSP Indirect Provider Tier-2 Sandbox account.</span></span>  
 

## <a name="delete-csp-indirect-reseller-sandbox-account"></a><span data-ttu-id="a0ef5-157">Usuwanie CSP Indirect Reseller piaskownicy</span><span class="sxs-lookup"><span data-stu-id="a0ef5-157">Delete CSP Indirect Reseller Sandbox account</span></span>

1. <span data-ttu-id="a0ef5-158">Zaloguj się Partner Center przy użyciu konta piaskownicy warstwy 2.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-158">Sign into Partner Center using your Tier 2 Sandbox account.</span></span> 

2. <span data-ttu-id="a0ef5-159">Przejdź do pozycji Odsprzedawcy pośredni z menu po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-159">Navigate to Indirect Resellers from the left menu.</span></span> 

3. <span data-ttu-id="a0ef5-160">Wybierz link **Usuń piaskownicę odsprzedawcy** obok konta piaskownicy odsprzedawcy pośredniego, które chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-160">Select the **Delete Reseller Sandbox** link next to the Indirect Reseller Sandbox account you want to delete.</span></span> <span data-ttu-id="a0ef5-161">Konto piaskownicy odsprzedawcy pośredniego zostanie trwale usunięte i nie będzie można go odzyskać.</span><span class="sxs-lookup"><span data-stu-id="a0ef5-161">The Indirect Reseller Sandbox account will be permanently deleted and cannot be recovered.</span></span> 

## <a name="api-references"></a><span data-ttu-id="a0ef5-162">Dokumentacja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="a0ef5-162">API references</span></span>

- <span data-ttu-id="a0ef5-163">Tworzenie odsprzedawcy pośredniego</span><span class="sxs-lookup"><span data-stu-id="a0ef5-163">Create Indirect Reseller</span></span> 
- <span data-ttu-id="a0ef5-164">Usuwanie odsprzedawcy pośredniego</span><span class="sxs-lookup"><span data-stu-id="a0ef5-164">Delete Indirect Reseller</span></span> 

 

 