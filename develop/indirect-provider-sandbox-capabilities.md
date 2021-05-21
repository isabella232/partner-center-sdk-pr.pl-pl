---
title: Możliwości dostawcy pośredniego CSP w piaskownicy
description: Dostawcy pośredni mogą tworzyć pośrednich odsprzedawców w piaskownicy do celów testowych.
ms.date: 05/20/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vinayks-ms
ms.author: vinayks
ms.openlocfilehash: bd0f38103e6b6f93ab5da386042b00801b683ccd
ms.sourcegitcommit: 1aeaa12705a5945b8aab6bca254fedebd9c8bc4e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2021
ms.locfileid: "110244607"
---
# <a name="csp-indirect-provider-sandbox-capabilities-for-creating-indirect-reseller-accounts"></a><span data-ttu-id="fac16-103">Możliwości piaskownicy dostawcy pośredniego CSP do tworzenia kont odsprzedawcy pośredniego</span><span class="sxs-lookup"><span data-stu-id="fac16-103">CSP Indirect provider sandbox capabilities for creating Indirect reseller accounts</span></span> 

<span data-ttu-id="fac16-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="fac16-104">**Applies to**</span></span>

- <span data-ttu-id="fac16-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="fac16-105">Partner Center</span></span>

<span data-ttu-id="fac16-106">**Odpowiednie role**</span><span class="sxs-lookup"><span data-stu-id="fac16-106">**Appropriate roles**</span></span>

- <span data-ttu-id="fac16-107">Dostawca pośredni</span><span class="sxs-lookup"><span data-stu-id="fac16-107">Indirect provider</span></span>

<span data-ttu-id="fac16-108">Dostawcy pośredni dostawcy CSP mogą utworzyć konto CSP Indirect Reseller piaskownicy za pośrednictwem własnego konta piaskownicy warstwy 2 w Partner Center Portal.</span><span class="sxs-lookup"><span data-stu-id="fac16-108">CSP Indirect Providers can create a CSP Indirect Reseller Sandbox account via through their own Tier 2 Sandbox account in Partner Center portal.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="fac16-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fac16-109">Prerequisites</span></span> 

<span data-ttu-id="fac16-110">Partner Center piaskownicy dostawcy pośredniego (warstwa 2).</span><span class="sxs-lookup"><span data-stu-id="fac16-110">Partner Center Indirect Provider (Tier 2) sandbox credentials.</span></span> <span data-ttu-id="fac16-111">Scenariusz piaskownicy obsługuje uwierzytelnianie zarówno przy użyciu autonomicznej aplikacji, jak i poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fac16-111">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span> 
 

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a><span data-ttu-id="fac16-112">Dostawca pośredni piaskownicy — tworzenie odsprzedawcy pośredniego piaskownicy przy Partner Center interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="fac16-112">Sandbox Indirect Provider – Create Sandbox Indirect Reseller using the Partner Center user interface</span></span> 

 <span data-ttu-id="fac16-113">Jest to funkcja piaskownicy, która umożliwia dostawcom pośrednim piaskownicy tworzenie konta odsprzedawcy pośredniego piaskownicy za pośrednictwem Partner Center portal.</span><span class="sxs-lookup"><span data-stu-id="fac16-113">This is a Sandbox- only feature that allows Sandbox Indirect Providers the ability to create Sandbox Indirect Reseller account through the Partner Center portal.</span></span>

<span data-ttu-id="fac16-114">Następujące scenariusze to, co dostawcy pośredni mogą zrobić dla odsprzedawców pośrednich w piaskownicy za pośrednictwem Partner Center interfejsu użytkownika:</span><span class="sxs-lookup"><span data-stu-id="fac16-114">The following scenarios are what Indirect providers can do for indirect resellers in Sandbox through the Partner Center user interface:</span></span> 

1. <span data-ttu-id="fac16-115">Dostawcy pośredni dostawcy CSP mogą utworzyć konto CSP Indirect Reseller piaskownicy za pośrednictwem własnego konta piaskownicy warstwy 2 w Partner Center Portal.</span><span class="sxs-lookup"><span data-stu-id="fac16-115">CSP Indirect Providers can create a CSP Indirect Reseller Sandbox account through their own Tier 2 Sandbox account in Partner Center portal.</span></span>
2. <span data-ttu-id="fac16-116">Odsprzedawcy pośredni w programie CSP mogą wyświetlać klientów według dostawców pośrednich.</span><span class="sxs-lookup"><span data-stu-id="fac16-116">CSP Indirect Resellers can view customer by Indirect Providers.</span></span> 

1. <span data-ttu-id="fac16-117">Odsprzedawcy pośredni programu CSP mogą zarządzać kontem klienta przy użyciu delegowanych uprawnień administratora.</span><span class="sxs-lookup"><span data-stu-id="fac16-117">CSP Indirect Resellers  can manage the customer account using delegated admin permissions.</span></span>

1. <span data-ttu-id="fac16-118">Dostawcy pośredni dostawcy CSP mogą zapraszać pośrednich odsprzedawców CSP.</span><span class="sxs-lookup"><span data-stu-id="fac16-118">CSP Indirect Providers can invite CSP Indirect Resellers.</span></span>
 
1. <span data-ttu-id="fac16-119">Dostawcy pośredni dostawcy CSP mogą usunąć konto CSP Indirect Reseller piaskownicy za pośrednictwem własnego konta piaskownicy warstwy 2 w Partner Center Portal.</span><span class="sxs-lookup"><span data-stu-id="fac16-119">CSP Indirect Providers can delete a CSP Indirect Reseller Sandbox account through their own Tier 2 Sandbox account in Partner Center portal.</span></span>

    <span data-ttu-id="fac16-120">a.</span><span class="sxs-lookup"><span data-stu-id="fac16-120">a.</span></span>  <span data-ttu-id="fac16-121">Gdy dostawca pośredni piaskownicy usuwa relację z odsprzedawcą pośrednim piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="fac16-121">When Sandbox Indirect Provider deletes relationship with Sandbox Indirect Reseller.</span></span>

    <span data-ttu-id="fac16-122">b.</span><span class="sxs-lookup"><span data-stu-id="fac16-122">b.</span></span>  <span data-ttu-id="fac16-123">Sprawdź, czy odsprzedawca pośredni ma jakiekolwiek inne relacje z innymi dostawcami.</span><span class="sxs-lookup"><span data-stu-id="fac16-123">Check if the Indirect Reseller has any other relationship with other providers.</span></span> <span data-ttu-id="fac16-124">Jeśli tak, zostanie usunięta tylko relacja z tym konkretnym dostawcą pośrednim.</span><span class="sxs-lookup"><span data-stu-id="fac16-124">If so, only the relationship with that specific Indirect provider will be removed.</span></span>

    <span data-ttu-id="fac16-125">c.</span><span class="sxs-lookup"><span data-stu-id="fac16-125">c.</span></span> <span data-ttu-id="fac16-126">Jeśli jest to jedyna relacja dla ir, to ir zostanie usunięte.</span><span class="sxs-lookup"><span data-stu-id="fac16-126">If that is the only relationship for the IR, then the IR will be deleted.</span></span>

1. <span data-ttu-id="fac16-127">CSP Indirect Provider usunąć CSP Indirect Reseller.</span><span class="sxs-lookup"><span data-stu-id="fac16-127">CSP Indirect Provider can delete a CSP Indirect Reseller.</span></span>

    <span data-ttu-id="fac16-128">a.</span><span class="sxs-lookup"><span data-stu-id="fac16-128">a.</span></span> <span data-ttu-id="fac16-129">Jest to funkcja dostępna tylko w piaskownicy, która umożliwia dostawcom pośrednim piaskownicy usuwanie odsprzedawców pośrednich piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="fac16-129">This is a Sandbox-only feature that allows Sandbox Indirect Providers the ability to delete Sandbox Indirect Resellers.</span></span>
     
1. <span data-ttu-id="fac16-130">Wymagania wstępne dotyczące usuwania odsprzedawcy pośredniego piaskownicy:</span><span class="sxs-lookup"><span data-stu-id="fac16-130">Pre-requisites for deleting a Sandbox Indirect Reseller:</span></span>

    1. <span data-ttu-id="fac16-131">Wstrzymaj subskrypcje dla każdego klienta odsprzedawcy pośredniego piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="fac16-131">Suspend the subscriptions for each customer of Sandbox Indirect Reseller.</span></span>

    1. <span data-ttu-id="fac16-132">Usuń wszystkich klientów odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="fac16-132">Delete all customers of Indirect Reseller.</span></span>

1. <span data-ttu-id="fac16-133">Dozwolony limit 5 odsprzedawców pośrednich piaskownicy na dostawcę pośredniego piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="fac16-133">Limit of 5 Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> <span data-ttu-id="fac16-134">Po usunięciu odsprzedawcy pośredniego piaskownicy limit przydziału zostanie zresetowany.</span><span class="sxs-lookup"><span data-stu-id="fac16-134">Once the Sandbox Indirect reseller is deleted, the quota will be reset.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="fac16-135">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fac16-135">Pre-requisites</span></span>

- <span data-ttu-id="fac16-136">Dozwolony limit 5 odsprzedawców pośrednich piaskownicy na dostawcę pośredniego piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="fac16-136">Limit of 5 Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> 

- <span data-ttu-id="fac16-137">Ten sam identyfikator MPN może służyć do tworzenia wielu kont piaskownicy odsprzedawcy pośredniego, jeśli kraj identyfikatora MPN i kraj piaskownicy odsprzedawcy pośredniego są takie same.</span><span class="sxs-lookup"><span data-stu-id="fac16-137">Same MPN ID can be used to create multiple Indirect Reseller Sandbox accounts if MPN ID country and Indirect Reseller Sandbox country are same.</span></span> <span data-ttu-id="fac16-138">Jeśli masz dostępny testowy identyfikator MPN, możesz go użyć lub uzyskać listę identyfikatorów MPN za pośrednictwem naszego kanału [usługi Yammer.]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 )</span><span class="sxs-lookup"><span data-stu-id="fac16-138">If you have a test MPN ID available, you can use it, or you can get a list of MPN IDs through our [Yammer channel]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ).</span></span> <span data-ttu-id="fac16-139">Jeśli nie masz dostępu do usługi Yammer, usługa Yammer poprosi Cię o dostęp.</span><span class="sxs-lookup"><span data-stu-id="fac16-139">If you don’t have access to Yammer, Yammer will ask you to request access.</span></span>
 
- <span data-ttu-id="fac16-140">Tylko 75 klientów jest dozwolonych na dostawcę pośredniego piaskownicy</span><span class="sxs-lookup"><span data-stu-id="fac16-140">Only 75 customers are allowed per Sandbox Indirect Provider</span></span>

## <a name="create-csp-indirect-reseller-sandbox-account"></a><span data-ttu-id="fac16-141">Tworzenie CSP Indirect Reseller piaskownicy</span><span class="sxs-lookup"><span data-stu-id="fac16-141">Create CSP Indirect Reseller Sandbox account</span></span>

1. <span data-ttu-id="fac16-142">Zaloguj się Partner Center za pośrednictwem konta piaskownicy warstwy 2.</span><span class="sxs-lookup"><span data-stu-id="fac16-142">Sign into Partner Center via your Tier 2 Sandbox account.</span></span> 

2. <span data-ttu-id="fac16-143">Przejdź do pozycji Odsprzedawcy pośredni z menu po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fac16-143">Navigate to Indirect Resellers from the left menu.</span></span> 

3. <span data-ttu-id="fac16-144">Kliknij przycisk "Dodaj piaskownicę odsprzedawcy".</span><span class="sxs-lookup"><span data-stu-id="fac16-144">Click on “Add Reseller Sandbox” button.</span></span> 

4. <span data-ttu-id="fac16-145">Wypełnij formularz rejestracji konta.</span><span class="sxs-lookup"><span data-stu-id="fac16-145">Fill the account enrollment form.</span></span> <span data-ttu-id="fac16-146">Nie wymaga to wyjaśnień, ale pamiętaj, że tworzysz konto piaskownicy dla odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="fac16-146">It's self-explanatory but remember you are creating a Sandbox account for an Indirect Reseller.</span></span> <span data-ttu-id="fac16-147">To konto nie zostanie poddane testowi i zostanie aktywowane zaraz po zakończeniu rejestracji konta.</span><span class="sxs-lookup"><span data-stu-id="fac16-147">This account won't undergo vetting and will be activated as soon as you finish the account enrollment.</span></span>  

5. <span data-ttu-id="fac16-148">Po utworzeniu konta w portalu otrzymasz poświadczenia administratora globalnego dla konta piaskownicy Odsprzedawca pośredni.</span><span class="sxs-lookup"><span data-stu-id="fac16-148">Once the account is created, you will get the Global Admin credentials for the Indirect Reseller sandbox account on the portal.</span></span> <span data-ttu-id="fac16-149">Pamiętaj, aby zapisać go natychmiast. W przeciwnym razie nie będzie można zalogować się jako piaskownica odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="fac16-149">Remember to save it immediately,  otherwise, you won't be able to sign in as an Indirect Reseller Sandbox.</span></span> 

6. <span data-ttu-id="fac16-150">Wyloguj się i zaloguj się ponownie Partner Center przy użyciu nowych poświadczeń dla piaskownicy odsprzedawcy pośredniego.</span><span class="sxs-lookup"><span data-stu-id="fac16-150">Sign out and sign in again to Partner Center using the new credentials for Indirect Reseller Sandbox.</span></span> <span data-ttu-id="fac16-151">Poznaj możliwości, które możesz wykonać jako odsprzedawca pośredni.</span><span class="sxs-lookup"><span data-stu-id="fac16-151">Explore the capabilities you can do as an Indirect Reseller.</span></span> <span data-ttu-id="fac16-152">Niektóre z nich to:</span><span class="sxs-lookup"><span data-stu-id="fac16-152">Some things are :</span></span>  

    - <span data-ttu-id="fac16-153">Zarządzanie profilami</span><span class="sxs-lookup"><span data-stu-id="fac16-153">Manage profiles</span></span>  

    - <span data-ttu-id="fac16-154">Zarządzanie użytkownikami i rolami</span><span class="sxs-lookup"><span data-stu-id="fac16-154">Manage users and roles</span></span> 

    - <span data-ttu-id="fac16-155">Zarządzanie dostawcami pośrednimi</span><span class="sxs-lookup"><span data-stu-id="fac16-155">Manage Indirect Providers</span></span> 

    - <span data-ttu-id="fac16-156">Zarządzanie klientami piaskownicy CSP</span><span class="sxs-lookup"><span data-stu-id="fac16-156">Manage CSP Sandbox customers</span></span> 

    - <span data-ttu-id="fac16-157">Zarządzanie relacjami</span><span class="sxs-lookup"><span data-stu-id="fac16-157">Manage relationships</span></span>
    
     
## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a><span data-ttu-id="fac16-158">Dostawca pośredni piaskownicy — usuwanie odsprzedawcy pośredniego piaskownicy przy Partner Center interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="fac16-158">Sandbox Indirect Provider – Delete Sandbox Indirect Reseller using the Partner Center user interface</span></span>

 <span data-ttu-id="fac16-159">Jest to funkcja dostępna tylko w piaskownicy, która umożliwia dostawcom pośrednim piaskownicy usuwanie istniejącego konta odsprzedawcy pośredniego piaskownicy za pośrednictwem Partner Center portalu.</span><span class="sxs-lookup"><span data-stu-id="fac16-159">This is a Sandbox only feature that allows Sandbox Indirect Providers an ability to delete an existing Sandbox Indirect Reseller account via Partner Center portal.</span></span> 

### <a name="pre-requisites-to-delete-sandbox-indirect-reseller"></a><span data-ttu-id="fac16-160">Wymagania wstępne usunięcia odsprzedawcy pośredniego piaskownicy:</span><span class="sxs-lookup"><span data-stu-id="fac16-160">Pre-requisites to delete sandbox Indirect reseller:</span></span>

<span data-ttu-id="fac16-161">Istniejące konto CSP Indirect Reseller piaskownicy skojarzone z Twoim własnym kontem CSP Indirect Provider piaskownicy warstwy 2.</span><span class="sxs-lookup"><span data-stu-id="fac16-161">An existing CSP Indirect Reseller Sandbox account associated with your own CSP Indirect Provider Tier-2 Sandbox account.</span></span>  
 

## <a name="delete-csp-indirect-reseller-sandbox-account"></a><span data-ttu-id="fac16-162">Usuwanie CSP Indirect Reseller piaskownicy</span><span class="sxs-lookup"><span data-stu-id="fac16-162">Delete CSP Indirect Reseller Sandbox account</span></span>

1. <span data-ttu-id="fac16-163">Zaloguj się Partner Center przy użyciu konta piaskownicy warstwy 2.</span><span class="sxs-lookup"><span data-stu-id="fac16-163">Sign into Partner Center using your Tier 2 Sandbox account.</span></span> 

2. <span data-ttu-id="fac16-164">Przejdź do pozycji Odsprzedawcy pośredni z menu po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fac16-164">Navigate to Indirect Resellers from the left menu.</span></span> 

3. <span data-ttu-id="fac16-165">Kliknij link **Usuń piaskownicę odsprzedawcy** obok konta piaskownicy odsprzedawcy pośredniego, które chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="fac16-165">Click on **Delete Reseller Sandbox** link next to the Indirect Reseller Sandbox account you want to delete.</span></span> <span data-ttu-id="fac16-166">Konto piaskownicy odsprzedawcy pośredniego zostanie trwale usunięte i nie będzie można go odzyskać.</span><span class="sxs-lookup"><span data-stu-id="fac16-166">The Indirect Reseller Sandbox account will be permanently deleted and cannot be recovered.</span></span> 

## <a name="api-references"></a><span data-ttu-id="fac16-167">Dokumentacja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="fac16-167">API references</span></span>

- <span data-ttu-id="fac16-168">Tworzenie odsprzedawcy pośredniego</span><span class="sxs-lookup"><span data-stu-id="fac16-168">Create Indirect Reseller</span></span> 
- <span data-ttu-id="fac16-169">Usuwanie odsprzedawcy pośredniego</span><span class="sxs-lookup"><span data-stu-id="fac16-169">Delete Indirect Reseller</span></span> 

 

 