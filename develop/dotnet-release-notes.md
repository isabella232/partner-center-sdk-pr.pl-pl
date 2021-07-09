---
title: Partner Center o wersji zestawu .NET SDK
description: Informacje o wersji najnowszej wersji zestawu SDK platformy Partner Center .NET.
ms.date: 07/07/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1532d48c00550f5eb437ed0164d6a1f7bb340dd
ms.sourcegitcommit: 53c94db33b09c30e762b842c4275b2b531dba932
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/09/2021
ms.locfileid: "113522638"
---
# <a name="net-sdk-release-notes"></a><span data-ttu-id="ca871-103">Informacje o wersji zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ca871-103">.NET SDK release notes</span></span>

<span data-ttu-id="ca871-104">Poniższe informacje o wersji są dostępne dla nowych wersji zestawu [Microsoft Partner Center .NET SDK.](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter)</span><span class="sxs-lookup"><span data-stu-id="ca871-104">The following release notes are available for new versions of [Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter).</span></span> <span data-ttu-id="ca871-105">Przykłady dla [zestawu SDK platformy .NET można znaleźć](https://github.com/Microsoft/Partner-Center-DotNet-Samples) GitHub.</span><span class="sxs-lookup"><span data-stu-id="ca871-105">You can find [.NET SDK samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) on GitHub.</span></span> <span data-ttu-id="ca871-106">Dokumentacja interfejsu [API platformy Partner Center .NET znajduje](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) się w przeglądarce interfejsów API platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="ca871-106">You can find the [Partner Center .NET API reference](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) in the .NET API Browser.</span></span>

## <a name="version-201"></a><span data-ttu-id="ca871-107">Wersja 2.0.1</span><span class="sxs-lookup"><span data-stu-id="ca871-107">Version 2.0.1</span></span>

<span data-ttu-id="ca871-108">[Zestaw Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/2.0.1) w wersji 2.0.1 jest teraz ogólnie dostępny.</span><span class="sxs-lookup"><span data-stu-id="ca871-108">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/2.0.1) v2.0.1 is now general availability.</span></span> <span data-ttu-id="ca871-109">Zaktualizowane [GitHub przykłady](https://github.com/Microsoft/Partner-Center-DotNet-Samples) są również dostępne.</span><span class="sxs-lookup"><span data-stu-id="ca871-109">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="ca871-110">W tej wersji uwzględniono następujące zmiany:</span><span class="sxs-lookup"><span data-stu-id="ca871-110">The following changes are included in this version:</span></span>

> [!NOTE]
> <span data-ttu-id="ca871-111">Niektóre zmiany wprowadzone w ramach nowych doświadczeń handlowych ("NCE"), które są obecnie dostępne na podstawie zaproszenia tylko dla partnerów, którzy są częścią nowego doświadczenia handlowego M365/D365 w wersji Technical Preview.</span><span class="sxs-lookup"><span data-stu-id="ca871-111">Some of changes introduced as part of New Commerce Experiences (“NCE”) which are currently available based on invitation only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span> <span data-ttu-id="ca871-112">Partnerzy, którzy nie są częścią nowej prywatnej wersji zapoznawczej handlu, nie powinni zauważyć wpływu i powinni być zgodni z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="ca871-112">Partners who are not part of New commerce private preview should not notice impacts and should be backward compatible.</span></span>

### <a name="common"></a><span data-ttu-id="ca871-113">Wspólne</span><span class="sxs-lookup"><span data-stu-id="ca871-113">Common</span></span>
* <span data-ttu-id="ca871-114">Zmiana odwołania do biblioteki uwierzytelniania — odwołanie jest zmieniane z biblioteki Azure Active Directory Authentication Library[(ADAL)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)na bibliotekę Microsoft Authentication Library[(MSAL)](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet)</span><span class="sxs-lookup"><span data-stu-id="ca871-114">Change on the reference to authentication library – The reference is changed from Azure Active Directory Authentication Library ([ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)) to Microsoft Authentication Library ([MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet))</span></span>

  <span data-ttu-id="ca871-115">Należy wprowadzić następujące zmiany, aby upewnić się, że msal działa prawidłowo w aplikacji lub przykładzie .NET:</span><span class="sxs-lookup"><span data-stu-id="ca871-115">Following changes should be made to ensure MSAL runs correctly on your application or .NET sample:</span></span>

  * <span data-ttu-id="ca871-116">Dodaj `https://login.microsoftonline.com/common/oauth2/nativeclient` jako RedirectUrl dla aplikacji mobilnych i klasycznych</span><span class="sxs-lookup"><span data-stu-id="ca871-116">Add `https://login.microsoftonline.com/common/oauth2/nativeclient` as RedirectUrl for Mobile and desktop applications</span></span>
  * <span data-ttu-id="ca871-117">Dodaj **domenę** do sekcji UserAuthentication w pliku konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca871-117">Add **Domain** into UserAuthentication section in your application configuration file.</span></span> 

    <span data-ttu-id="ca871-118">Domena to Azure Active Directory lub identyfikator dzierżawy, w której utworzono aplikację usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca871-118">Domain is the Azure Active Directory domain or tenant ID where the Azure AD application was created</span></span>

* <span data-ttu-id="ca871-119">[Kody błędów](error-codes.md) — dodano nowy kod błędu</span><span class="sxs-lookup"><span data-stu-id="ca871-119">[Error codes](error-codes.md) – New error code added</span></span> 
  * <span data-ttu-id="ca871-120">408: Limit czasu żądania</span><span class="sxs-lookup"><span data-stu-id="ca871-120">408: Request timeout</span></span>
  * <span data-ttu-id="ca871-121">504: Limit czasu bramy</span><span class="sxs-lookup"><span data-stu-id="ca871-121">504: Gateway timeout</span></span> 

### <a name="manage-billing"></a><span data-ttu-id="ca871-122">Zarządzanie rozliczeniami</span><span class="sxs-lookup"><span data-stu-id="ca871-122">Manage billing</span></span>

* <span data-ttu-id="ca871-123">[Elementy wiersza faktury —](get-invoiceline-items.md) nowe atrybuty dodane do następujących interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="ca871-123">[Invoice line-items](get-invoiceline-items.md) - new attributes added to following APIs:</span></span>
  * `GET /invoices/{invoice-id}/lineitems?provider={provider}&invoicelineitemtype=billinglineitems`
  * `GET /invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems`

  <span data-ttu-id="ca871-124">Nowe atrybuty:</span><span class="sxs-lookup"><span data-stu-id="ca871-124">New attributes:</span></span> 
  * <span data-ttu-id="ca871-125">productQualifiers</span><span class="sxs-lookup"><span data-stu-id="ca871-125">productQualifiers</span></span>
  * <span data-ttu-id="ca871-126">subscriptionStartDate</span><span class="sxs-lookup"><span data-stu-id="ca871-126">subscriptionStartDate</span></span>
  * <span data-ttu-id="ca871-127">subscriptionEndDate</span><span class="sxs-lookup"><span data-stu-id="ca871-127">subscriptionEndDate</span></span>
  * <span data-ttu-id="ca871-128">referenceId</span><span class="sxs-lookup"><span data-stu-id="ca871-128">referenceId</span></span>
  * <span data-ttu-id="ca871-129">creditReasonCode (dotyczy tylko NCE)</span><span class="sxs-lookup"><span data-stu-id="ca871-129">creditReasonCode  (Only applicable to NCE)</span></span>
  * <span data-ttu-id="ca871-130">promotionId</span><span class="sxs-lookup"><span data-stu-id="ca871-130">promotionId</span></span> 


* <span data-ttu-id="ca871-131">[Elementy liniowe dziennego użycia ocenianego](get-invoice-billed-consumption-lineitems.md) — nowe atrybuty dodane do następującego interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="ca871-131">[Daily rated usage Line-items](get-invoice-billed-consumption-lineitems.md) – new attributes added to following API:</span></span> 
  * `GET /invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems`
  
  <span data-ttu-id="ca871-132">Nowe atrybuty:</span><span class="sxs-lookup"><span data-stu-id="ca871-132">New attributes:</span></span> 
  * <span data-ttu-id="ca871-133">hasPartnerEarnedCredit (dotyczy tylko NCE)</span><span class="sxs-lookup"><span data-stu-id="ca871-133">hasPartnerEarnedCredit (Only applicable to NCE)</span></span>
  * <span data-ttu-id="ca871-134">creditType (dotyczy tylko NCE)</span><span class="sxs-lookup"><span data-stu-id="ca871-134">creditType (Only applicable to NCE)</span></span>
  * <span data-ttu-id="ca871-135">rateOfCredit (dotyczy tylko NCE)</span><span class="sxs-lookup"><span data-stu-id="ca871-135">rateOfCredit (Only applicable to NCE)</span></span>


### <a name="manage-orders"></a><span data-ttu-id="ca871-136">Zarządzanie zamówieniami</span><span class="sxs-lookup"><span data-stu-id="ca871-136">Manage orders</span></span>

* <span data-ttu-id="ca871-137">[Zasoby subskrypcji](subscription-resources.md) — dodano nową właściwość.</span><span class="sxs-lookup"><span data-stu-id="ca871-137">[Subscription Resources](subscription-resources.md) – New property added.</span></span> 
  * <span data-ttu-id="ca871-138">CancellationAllowedUntilDate — (dotyczy tylko NCE)</span><span class="sxs-lookup"><span data-stu-id="ca871-138">CancellationAllowedUntilDate  - (Only applicable to NCE)</span></span>

* <span data-ttu-id="ca871-139">Zasoby przejściowe (dotyczy tylko NCE) — dodano nową właściwość</span><span class="sxs-lookup"><span data-stu-id="ca871-139">Transition Resources (Only applicable to NCE) – New property added</span></span> 
  * <span data-ttu-id="ca871-140">FromSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="ca871-140">FromSubscriptionId</span></span>

### <a name="manage-customer-accounts"></a><span data-ttu-id="ca871-141">Zarządzanie kontami klientów</span><span class="sxs-lookup"><span data-stu-id="ca871-141">Manage customer accounts</span></span>

* <span data-ttu-id="ca871-142">[Weryfikowanie adresu](validate-an-address.md) — odpowiedź jest zmieniana z wartości logicznych na nowy model dla interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="ca871-142">[Validate an address](validate-an-address.md) – Response is changed from a Boolean to a new model for API:</span></span>
  * `POST /validations/address`
  
  <span data-ttu-id="ca871-143">Nowy model odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="ca871-143">New response model:</span></span> 
  * <span data-ttu-id="ca871-144">AddressValidationResponse</span><span class="sxs-lookup"><span data-stu-id="ca871-144">AddressValidationResponse</span></span>

* <span data-ttu-id="ca871-145">Synchroniczny interfejs API kwalifikacji klienta jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="ca871-145">Customer’s qualification synchronous API is deprecated.</span></span>  


## <a name="version-1170"></a><span data-ttu-id="ca871-146">Wersja 1.17.0</span><span class="sxs-lookup"><span data-stu-id="ca871-146">Version 1.17.0</span></span>

<span data-ttu-id="ca871-147">[Zestaw Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) w wersji 1.17.0 jest teraz ogólnie dostępny.</span><span class="sxs-lookup"><span data-stu-id="ca871-147">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v1.17.0 is now general availability.</span></span> <span data-ttu-id="ca871-148">Zaktualizowane [GitHub przykłady](https://github.com/Microsoft/Partner-Center-DotNet-Samples) są również dostępne.</span><span class="sxs-lookup"><span data-stu-id="ca871-148">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="ca871-149">W tej wersji uwzględniono następujące zmiany:</span><span class="sxs-lookup"><span data-stu-id="ca871-149">The following changes are included in this version:</span></span>

* <span data-ttu-id="ca871-150">Aktualizacja inspekcji — dodano nowe typy operacji, aby wiedzieć, kiedy klient zatwierdził i zakończył działanie daP</span><span class="sxs-lookup"><span data-stu-id="ca871-150">Audit Updated - Added new operation types for knowing when the customer approved and terminated DAP</span></span>
  * [<span data-ttu-id="ca871-151">DapAdminRelationshipApproved</span><span class="sxs-lookup"><span data-stu-id="ca871-151">DapAdminRelationshipApproved</span></span>](auditing-resources.md)
  * [<span data-ttu-id="ca871-152">DapAdminRelationshipTerminated</span><span class="sxs-lookup"><span data-stu-id="ca871-152">DapAdminRelationshipTerminated</span></span>](auditing-resources.md)

* <span data-ttu-id="ca871-153">Zaktualizowano inspekcję — dodano nowe typy zasobów i operacji na potrzeby obsługi scenariusza roli katalogu klienta</span><span class="sxs-lookup"><span data-stu-id="ca871-153">Audit Updated – Added new resource and operation types for supporting the customer directory role scenario</span></span>
  * <span data-ttu-id="ca871-154">Typ zasobu "[CustomerDirectoryRole](auditing-resources.md)"</span><span class="sxs-lookup"><span data-stu-id="ca871-154">Resource type "[CustomerDirectoryRole](auditing-resources.md)"</span></span>
  * <span data-ttu-id="ca871-155">Typy operacji "[AddUserMember](auditing-resources.md)" i "[RemoveUserMember](auditing-resources.md)"</span><span class="sxs-lookup"><span data-stu-id="ca871-155">Operation types "[AddUserMember](auditing-resources.md)" and "[RemoveUserMember](auditing-resources.md)"</span></span>

* <span data-ttu-id="ca871-156">Aktualizacje zestawu SDK dla konta klientów — obsługa następujących interfejsów API</span><span class="sxs-lookup"><span data-stu-id="ca871-156">SDK Updates to Customers Account - Support for following API's</span></span>
  * <span data-ttu-id="ca871-157">GET /customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus</span><span class="sxs-lookup"><span data-stu-id="ca871-157">GET /customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus</span></span>
  * <span data-ttu-id="ca871-158">GET /customers/{customer-tenant-id}/qualifications</span><span class="sxs-lookup"><span data-stu-id="ca871-158">GET /customers/{customer-tenant-id}/qualifications</span></span> 
  * <span data-ttu-id="ca871-159">POST /customers/{customer_id}/qualifications?code={validationCode}</span><span class="sxs-lookup"><span data-stu-id="ca871-159">POST /customers/{customer_id}/qualifications?code={validationCode}</span></span>

* <span data-ttu-id="ca871-160">**Następujące zmiany wprowadzone w ramach nowego handlu, które są obecnie dostępne na podstawie zaproszenia tylko dla partnerów, którzy są częścią nowego doświadczenia handlowego M365/D365 w wersji Technical Preview.**</span><span class="sxs-lookup"><span data-stu-id="ca871-160">**Following changes introduced as part of New Commerce which are currently available based on invitation only to partners who are part of the M365/D365 new commerce experience technical preview.**</span></span> <span data-ttu-id="ca871-161">Partnerzy, którzy nie są częścią nowej prywatnej wersji zapoznawczej handlu, nie powinni zauważyć wpływu i powinni być zgodni z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="ca871-161">Partners who are not part of New commerce private preview should not notice impacts and should be backward compatible.</span></span>
  * <span data-ttu-id="ca871-162">Zmiany katalogu:</span><span class="sxs-lookup"><span data-stu-id="ca871-162">Catalog Changes:</span></span>
    * <span data-ttu-id="ca871-163">GET /products/{product-id}/skus/{sku-id}</span><span class="sxs-lookup"><span data-stu-id="ca871-163">GET /products/{product-id}/skus/{sku-id}</span></span>
  * <span data-ttu-id="ca871-164">Zakup i zarządzanie:</span><span class="sxs-lookup"><span data-stu-id="ca871-164">Purchase and Manage:</span></span>
    * <span data-ttu-id="ca871-165">GET /customers/{customerId}/subscriptions</span><span class="sxs-lookup"><span data-stu-id="ca871-165">GET /customers/{customerId}/subscriptions</span></span>
    * <span data-ttu-id="ca871-166">GET /customers/{customerId}/subscriptions/{subscriptionId}</span><span class="sxs-lookup"><span data-stu-id="ca871-166">GET /customers/{customerId}/subscriptions/{subscriptionId}</span></span>
    * <span data-ttu-id="ca871-167">PATCH /customers/{customerId}/subscriptions/{subscriptionId}</span><span class="sxs-lookup"><span data-stu-id="ca871-167">PATCH /customers/{customerId}/subscriptions/{subscriptionId}</span></span>
    * <span data-ttu-id="ca871-168">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities</span><span class="sxs-lookup"><span data-stu-id="ca871-168">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities</span></span>
    * <span data-ttu-id="ca871-169">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span><span class="sxs-lookup"><span data-stu-id="ca871-169">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span></span>
    * <span data-ttu-id="ca871-170">POST /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span><span class="sxs-lookup"><span data-stu-id="ca871-170">POST /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span></span>


## <a name="version-1163"></a><span data-ttu-id="ca871-171">Wersja 1.16.3</span><span class="sxs-lookup"><span data-stu-id="ca871-171">Version 1.16.3</span></span>

<span data-ttu-id="ca871-172">[Zestaw MICROSOFT Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) w wersji 1.16.3 jest teraz ogólnie dostępny.</span><span class="sxs-lookup"><span data-stu-id="ca871-172">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v1.16.3 is now general availability.</span></span> <span data-ttu-id="ca871-173">Zaktualizowane [GitHub przykłady](https://github.com/Microsoft/Partner-Center-DotNet-Samples) są również dostępne.</span><span class="sxs-lookup"><span data-stu-id="ca871-173">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="ca871-174">W tej wersji uwzględniono następujące zmiany:</span><span class="sxs-lookup"><span data-stu-id="ca871-174">The following changes are included in this version:</span></span>

* <span data-ttu-id="ca871-175">SelfServePolicies — dodano nowe funkcje</span><span class="sxs-lookup"><span data-stu-id="ca871-175">SelfServePolicies - new functionality added</span></span>
  * [<span data-ttu-id="ca871-176">GetSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="ca871-176">GetSelfServePolicies</span></span>](get-a-self-serve-policy-by-id.md)
  * [<span data-ttu-id="ca871-177">GetListOfSelfServicePolicies</span><span class="sxs-lookup"><span data-stu-id="ca871-177">GetListOfSelfServicePolicies</span></span>](get-a-list-of-self-serve-policies.md)
  * [<span data-ttu-id="ca871-178">CreateSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="ca871-178">CreateSelfServePolicies</span></span>](create-a-self-serve-policy.md)
  * [<span data-ttu-id="ca871-179">UpdateSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="ca871-179">UpdateSelfServePolicies</span></span>](update-a-self-serve-policy.md)
  * [<span data-ttu-id="ca871-180">DeleteSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="ca871-180">DeleteSelfServePolicies</span></span>](delete-a-self-serve-policy.md)

* <span data-ttu-id="ca871-181">Profil firmy klientów</span><span class="sxs-lookup"><span data-stu-id="ca871-181">Customers Company Profile</span></span>
  * <span data-ttu-id="ca871-182">Dodano [wartość OrganizationRegistrationNumber](create-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="ca871-182">Added [OrganizationRegistrationNumber](create-a-customer.md)</span></span>

* <span data-ttu-id="ca871-183">CustomerBillingProfile.DefaultAddress</span><span class="sxs-lookup"><span data-stu-id="ca871-183">CustomerBillingProfile.DefaultAddress</span></span>
  * <span data-ttu-id="ca871-184">Dodano wartość MiddleName</span><span class="sxs-lookup"><span data-stu-id="ca871-184">Added MiddleName</span></span>

## <a name="version-1162"></a><span data-ttu-id="ca871-185">Wersja 1.16.2</span><span class="sxs-lookup"><span data-stu-id="ca871-185">Version 1.16.2</span></span>

<span data-ttu-id="ca871-186">[Zestaw MICROSOFT Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) w wersji 1.16.2 jest teraz ogólnie dostępny.</span><span class="sxs-lookup"><span data-stu-id="ca871-186">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v1.16.2 is now general availability.</span></span> <span data-ttu-id="ca871-187">Zaktualizowane [GitHub przykłady](https://github.com/Microsoft/Partner-Center-DotNet-Samples) są również dostępne.</span><span class="sxs-lookup"><span data-stu-id="ca871-187">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="ca871-188">W tej wersji uwzględniono następujące zmiany:</span><span class="sxs-lookup"><span data-stu-id="ca871-188">The following changes are included in this version:</span></span>

* <span data-ttu-id="ca871-189">Zaktualizuj obsługiwane typy operacji dla rekordu inspekcji.</span><span class="sxs-lookup"><span data-stu-id="ca871-189">Update supported operation types for Audit Record.</span></span> <span data-ttu-id="ca871-190">Nowo dodane to:</span><span class="sxs-lookup"><span data-stu-id="ca871-190">The newly added ones are:</span></span>
  * <span data-ttu-id="ca871-191">CreateSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="ca871-191">CreateSelfServePolicy</span></span>
  * <span data-ttu-id="ca871-192">UpdateSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="ca871-192">UpdateSelfServePolicy</span></span>
  * <span data-ttu-id="ca871-193">DeleteSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="ca871-193">DeleteSelfServePolicy</span></span>
  * <span data-ttu-id="ca871-194">RemovePartnerRelationship</span><span class="sxs-lookup"><span data-stu-id="ca871-194">RemovePartnerRelationship</span></span>
  * <span data-ttu-id="ca871-195">DeleteTipCustomer</span><span class="sxs-lookup"><span data-stu-id="ca871-195">DeleteTipCustomer</span></span>
  * <span data-ttu-id="ca871-196">CreateRelatedReferral</span><span class="sxs-lookup"><span data-stu-id="ca871-196">CreateRelatedReferral</span></span>
  * <span data-ttu-id="ca871-197">UpdateRelatedReferral</span><span class="sxs-lookup"><span data-stu-id="ca871-197">UpdateRelatedReferral</span></span>

* <span data-ttu-id="ca871-198">Tworzenie żądania obsługi jest teraz przestarzałe</span><span class="sxs-lookup"><span data-stu-id="ca871-198">Service request creation is now deprecated</span></span>
* <span data-ttu-id="ca871-199">Tematy pomocy technicznej są teraz przestarzałe</span><span class="sxs-lookup"><span data-stu-id="ca871-199">Support topics are now deprecated</span></span>


## <a name="version-1161"></a><span data-ttu-id="ca871-200">Wersja 1.16.1</span><span class="sxs-lookup"><span data-stu-id="ca871-200">Version 1.16.1</span></span>

<span data-ttu-id="ca871-201">[Zestaw Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) w wersji 1.16.1 jest teraz ogólnie dostępny.</span><span class="sxs-lookup"><span data-stu-id="ca871-201">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v1.16.1 is now general availability.</span></span> <span data-ttu-id="ca871-202">Zaktualizowane [GitHub przykłady](https://github.com/Microsoft/Partner-Center-DotNet-Samples) są również dostępne.</span><span class="sxs-lookup"><span data-stu-id="ca871-202">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="ca871-203">W tej wersji uwzględniono następujące zmiany:</span><span class="sxs-lookup"><span data-stu-id="ca871-203">The following changes are included in this version:</span></span>

<span data-ttu-id="ca871-204">Zmigrowaliśmy istniejącą platformę Microsoft zestaw SDK Centrum partnerskiego .NET Framework do .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="ca871-204">We have migrated the existing Microsoft Partner Center SDK from .NET Framework to .NET Standard 2.0 platform.</span></span> <span data-ttu-id="ca871-205">Dzięki temu zestaw SDK będzie zgodny z istniejącymi aplikacjami przy użyciu .NET Framework 4.6.1 i jego nowych.</span><span class="sxs-lookup"><span data-stu-id="ca871-205">This will make the SDK compatible with existing applications using .NET Framework 4.6.1 and above.</span></span> <span data-ttu-id="ca871-206">Zestaw SDK będzie obsługiwać program .NET Core 2.0 i jego więcej.</span><span class="sxs-lookup"><span data-stu-id="ca871-206">The SDK will support .NET Core 2.0 and above.</span></span> <span data-ttu-id="ca871-207">Sprawdź [obsługę implementacji .NET](/dotnet/standard/net-standard) przed jej przenoszeniem do istniejących aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca871-207">Check [.NET implementation support](/dotnet/standard/net-standard) before porting it to existing applications.</span></span>   


## <a name="version-1153"></a><span data-ttu-id="ca871-208">Wersja 1.15.3</span><span class="sxs-lookup"><span data-stu-id="ca871-208">Version 1.15.3</span></span>
<span data-ttu-id="ca871-209">[Zestaw MICROSOFT Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) w wersji 1.15.3 jest teraz ogólnie dostępny.</span><span class="sxs-lookup"><span data-stu-id="ca871-209">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v1.15.3 is now general availability.</span></span> <span data-ttu-id="ca871-210">Dostępne są również zaktualizowane interfejsy API REST [GitHub przykłady](https://github.com/Microsoft/Partner-Center-DotNet-Samples) interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="ca871-210">Updated REST APIs and [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="ca871-211">W tej wersji uwzględniono następujące zmiany:</span><span class="sxs-lookup"><span data-stu-id="ca871-211">The following changes are included in this version:</span></span>

* <span data-ttu-id="ca871-212">Umowa partnerska</span><span class="sxs-lookup"><span data-stu-id="ca871-212">Partner Agreement</span></span>
  * <span data-ttu-id="ca871-213">Dodano możliwość weryfikowania przez dostawców [pośrednich Microsoft Partner Agreement stanu odsprzedawców pośrednich.](verify-indirect-reseller-mpa-status.md)</span><span class="sxs-lookup"><span data-stu-id="ca871-213">Added the ability for indirect providers to [verify Microsoft Partner Agreement status of indirect resellers](verify-indirect-reseller-mpa-status.md).</span></span>
* <span data-ttu-id="ca871-214">Produkty</span><span class="sxs-lookup"><span data-stu-id="ca871-214">Products</span></span>
  * <span data-ttu-id="ca871-215">Następujące dwa interfejsy zostały nieprawidłowo umieszczone w przestrzeni nazw Microsoft.Store.PartnerCenter.Products.</span><span class="sxs-lookup"><span data-stu-id="ca871-215">The following two interfaces were incorrectly placed under the Microsoft.Store.PartnerCenter.Products namespace.</span></span> <span data-ttu-id="ca871-216">Teraz znajdują się one w przestrzeni nazw Microsoft.Store.PartnerCenter.Customers.Products.</span><span class="sxs-lookup"><span data-stu-id="ca871-216">Now, they are located under the Microsoft.Store.PartnerCenter.Customers.Products namespace.</span></span>
    * <span data-ttu-id="ca871-217">ICustomerProductByReservationScope</span><span class="sxs-lookup"><span data-stu-id="ca871-217">ICustomerProductByReservationScope</span></span>
    * <span data-ttu-id="ca871-218">ICustomerSkuByReservationScope</span><span class="sxs-lookup"><span data-stu-id="ca871-218">ICustomerSkuByReservationScope</span></span>
