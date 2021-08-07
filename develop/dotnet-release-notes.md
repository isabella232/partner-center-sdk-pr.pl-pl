---
title: Partner Center o wersji zestawu .NET SDK
description: Informacje o wersji najnowszej wersji zestawu SDK platformy Partner Center .NET.
ms.date: 07/07/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6fc6182638cb2cc5457bdfada37b928c88e1ca786e401f7eb8d5309a0abd9310
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991228"
---
# <a name="net-sdk-release-notes"></a>Informacje o wersji zestawu .NET SDK

Poniższe informacje o wersji są dostępne dla nowych wersji zestawu [Microsoft Partner Center .NET SDK.](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter) Przykłady dla [zestawu SDK platformy .NET można znaleźć](https://github.com/Microsoft/Partner-Center-DotNet-Samples) GitHub. Dokumentacja interfejsu [API platformy Partner Center .NET znajduje](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) się w przeglądarce interfejsów API platformy .NET.

## <a name="version-201"></a>Wersja 2.0.1

[Zestaw Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/2.0.1) w wersji 2.0.1 jest teraz ogólnie dostępny. Zaktualizowane [GitHub przykłady](https://github.com/Microsoft/Partner-Center-DotNet-Samples) są również dostępne. W tej wersji uwzględniono następujące zmiany:

> [!NOTE]
> Niektóre zmiany wprowadzone w ramach nowych doświadczeń handlowych ("NCE"), które są obecnie dostępne na podstawie zaproszenia tylko dla partnerów, którzy są częścią nowego doświadczenia handlowego M365/D365 w wersji Technical Preview. Partnerzy, którzy nie są częścią nowej prywatnej wersji zapoznawczej handlu, nie powinni zauważyć wpływu i powinni być zgodni z poprzednimi wersjami.

### <a name="common"></a>Wspólne
* Zmiana odwołania do biblioteki uwierzytelniania — odwołanie jest zmieniane z biblioteki Azure Active Directory Authentication Library[(ADAL)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)na bibliotekę Microsoft Authentication Library[(MSAL)](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet)

  Należy wprowadzić następujące zmiany, aby upewnić się, że msal działa prawidłowo w aplikacji lub przykładzie .NET:

  * Dodawanie `https://login.microsoftonline.com/common/oauth2/nativeclient` jako redirectUrl dla aplikacji mobilnych i klasycznych
  * Dodaj **domenę** do sekcji UserAuthentication w pliku konfiguracji aplikacji. 

    Domena jest domeną Azure Active Directory lub identyfikatorem dzierżawy, w której utworzono aplikację usługi Azure AD

* [Kody błędów](error-codes.md) — dodano nowy kod błędu 
  * 408: Limit czasu żądania
  * 504: Limit czasu bramy 

### <a name="manage-billing"></a>Zarządzanie rozliczeniami

* [Elementy wiersza faktury —](get-invoiceline-items.md) nowe atrybuty dodane do następujących interfejsów API:
  * `GET /invoices/{invoice-id}/lineitems?provider={provider}&invoicelineitemtype=billinglineitems`
  * `GET /invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems`

  Nowe atrybuty: 
  * productQualifiers
  * subscriptionStartDate
  * subscriptionEndDate
  * referenceId
  * creditReasonCode (dotyczy tylko NCE)
  * promotionId 


* [Elementy liniowe dziennego użycia ocenianego](get-invoice-billed-consumption-lineitems.md) — nowe atrybuty dodane do następującego interfejsu API: 
  * `GET /invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems`
  
  Nowe atrybuty: 
  * hasPartnerEarnedCredit (dotyczy tylko NCE)
  * creditType (dotyczy tylko NCE)
  * rateOfCredit (dotyczy tylko NCE)


### <a name="manage-orders"></a>Zarządzanie zamówieniami

* [Zasoby subskrypcji](subscription-resources.md) — dodano nową właściwość. 
  * CancellationAllowedUntilDate — (dotyczy tylko NCE)

* Zasoby przejściowe (dotyczy tylko NCE) — dodano nową właściwość 
  * FromSubscriptionId

### <a name="manage-customer-accounts"></a>Zarządzanie kontami klientów

* [Weryfikowanie adresu](validate-an-address.md) — odpowiedź jest zmieniana z wartości logicznych na nowy model dla interfejsu API:
  * `POST /validations/address`
  
  Nowy model odpowiedzi: 
  * AddressValidationResponse

* Synchroniczny interfejs API kwalifikacji klienta jest przestarzały.  


## <a name="version-1170"></a>Wersja 1.17.0

[Zestaw Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) w wersji 1.17.0 jest teraz ogólnie dostępny. Zaktualizowane [GitHub przykłady](https://github.com/Microsoft/Partner-Center-DotNet-Samples) są również dostępne. W tej wersji uwzględniono następujące zmiany:

* Aktualizacja inspekcji — dodano nowe typy operacji, aby wiedzieć, kiedy klient zatwierdził i zakończył działanie daP
  * [DapAdminRelationshipApproved](auditing-resources.md)
  * [DapAdminRelationshipTerminated](auditing-resources.md)

* Zaktualizowano inspekcję — dodano nowe typy zasobów i operacji na potrzeby obsługi scenariusza roli katalogu klienta
  * Typ zasobu "[CustomerDirectoryRole](auditing-resources.md)"
  * Typy operacji "[AddUserMember](auditing-resources.md)" i "[RemoveUserMember](auditing-resources.md)"

* Aktualizacje zestawu SDK dla konta klientów — obsługa następujących interfejsów API
  * GET /customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus
  * GET /customers/{customer-tenant-id}/qualifications 
  * POST /customers/{customer_id}/qualifications?code={validationCode}

* **Następujące zmiany wprowadzone w ramach nowego handlu, które są obecnie dostępne na podstawie zaproszenia tylko dla partnerów, którzy są częścią nowego doświadczenia handlowego M365/D365 w wersji Technical Preview.** Partnerzy, którzy nie są częścią nowej prywatnej wersji zapoznawczej handlu, nie powinni zauważyć wpływu i powinni być zgodni z poprzednimi wersjami.
  * Zmiany katalogu:
    * GET /products/{identyfikator-produktu}/skus/{identyfikator-jednostki SKU}
  * Zakup i zarządzanie:
    * GET /customers/{customerId}/subscriptions
    * GET /customers/{customerId}/subscriptions/{subscriptionId}
    * PATCH /customers/{customerId}/subscriptions/{subscriptionId}
    * GET /customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities
    * GET /customers/{customerId}/subscriptions/{subscriptionId}/transitions
    * POST /customers/{customerId}/subscriptions/{subscriptionId}/transitions


## <a name="version-1163"></a>Wersja 1.16.3

[Zestaw MICROSOFT Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) w wersji 1.16.3 jest teraz ogólnie dostępny. Zaktualizowane [GitHub przykłady](https://github.com/Microsoft/Partner-Center-DotNet-Samples) są również dostępne. W tej wersji uwzględniono następujące zmiany:

* SelfServePolicies — dodano nowe funkcje
  * [GetSelfServePolicies](get-a-self-serve-policy-by-id.md)
  * [GetListOfSelfServicePolicies](get-a-list-of-self-serve-policies.md)
  * [CreateSelfServePolicies](create-a-self-serve-policy.md)
  * [UpdateSelfServePolicies](update-a-self-serve-policy.md)
  * [DeleteSelfServePolicies](delete-a-self-serve-policy.md)

* Profil firmy klientów
  * Dodano [wartość OrganizationRegistrationNumber](create-a-customer.md)

* CustomerBillingProfile.DefaultAddress
  * Dodano wartość MiddleName

## <a name="version-1162"></a>Wersja 1.16.2

[Zestaw MICROSOFT Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) w wersji 1.16.2 jest teraz ogólnie dostępny. Zaktualizowane [GitHub przykłady](https://github.com/Microsoft/Partner-Center-DotNet-Samples) są również dostępne. W tej wersji uwzględniono następujące zmiany:

* Zaktualizuj obsługiwane typy operacji dla rekordu inspekcji. Nowo dodane to:
  * CreateSelfServePolicy
  * UpdateSelfServePolicy
  * DeleteSelfServePolicy
  * RemovePartnerRelationship
  * DeleteTipCustomer
  * CreateRelatedReferral
  * UpdateRelatedReferral

* Tworzenie żądania obsługi jest teraz przestarzałe
* Tematy pomocy technicznej są teraz przestarzałe


## <a name="version-1161"></a>Wersja 1.16.1

[Zestaw MICROSOFT Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) w wersji 1.16.1 jest teraz ogólnie dostępny. Zaktualizowane [GitHub przykłady](https://github.com/Microsoft/Partner-Center-DotNet-Samples) są również dostępne. W tej wersji uwzględniono następujące zmiany:

Zmigrowaliśmy istniejącą platformę Microsoft zestaw SDK Centrum partnerskiego .NET Framework do .NET Standard 2.0. Dzięki temu zestaw SDK będzie zgodny z istniejącymi aplikacjami przy użyciu .NET Framework 4.6.1 lub 1. Zestaw SDK będzie obsługiwać program .NET Core 2.0 i jego więcej. Sprawdź [obsługę implementacji .NET](/dotnet/standard/net-standard) przed jej przenoszeniem do istniejących aplikacji.   


## <a name="version-1153"></a>Wersja 1.15.3
[Zestaw MICROSOFT Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) w wersji 1.15.3 jest teraz ogólnie dostępny. Dostępne są również zaktualizowane [interfejsy API](https://github.com/Microsoft/Partner-Center-DotNet-Samples) REST GitHub przykłady. W tej wersji uwzględniono następujące zmiany:

* Umowa partnerska
  * Dodano możliwość weryfikowania przez dostawców [pośrednich Microsoft Partner Agreement stanu odsprzedawców pośrednich.](verify-indirect-reseller-mpa-status.md)
* Produkty
  * Następujące dwa interfejsy zostały niepoprawnie umieszczone w przestrzeni nazw Microsoft.Store.PartnerCenter.Products. Teraz znajdują się one w przestrzeni nazw Microsoft.Store.PartnerCenter.Customers.Products.
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope
