---
title: Informacje o wersji zestawu SDK platformy .NET dla Centrum partnerskiego
description: Informacje o wersji dla najnowszej wersji zestawu SDK platformy .NET dla usługi Partner Center.
ms.date: 09/18/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2fe309500cc80e962c101ad97f0712bef7e11eb3
ms.sourcegitcommit: f7fce0b35ab1579e59136abc357b71cf768b81b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/23/2021
ms.locfileid: "104895537"
---
# <a name="net-sdk-release-notes"></a>Informacje o wersji zestawu SDK platformy .NET

Poniższe informacje o wersji są dostępne dla nowych wersji [zestawu .NET SDK programu Microsoft Partner Center](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter). [Przykłady zestawu SDK dla platformy .NET](https://github.com/Microsoft/Partner-Center-DotNet-Samples) można znaleźć w witrynie GitHub. [Informacje o interfejsie API platformy .NET Centrum partnerskiego](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) można znaleźć w przeglądarce interfejsu API platformy .NET.

## <a name="version-1170"></a>1.17.0 wersja

[Zestaw Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v 1.17.0 jest teraz ogólnie dostępny. Zaktualizowane [przykłady serwisu GitHub](https://github.com/Microsoft/Partner-Center-DotNet-Samples) są również dostępne. W tej wersji uwzględniono następujące zmiany:

* Inspekcja została zaktualizowana — dodano nowe typy operacji w celu znajomości sytuacji, w których klient zatwierdził i zakończył DAP
  * [DapAdminRelationshipApproved](auditing-resources.md)
  * [DapAdminRelationshipTerminated](auditing-resources.md)

* Inspekcja została zaktualizowana — dodano nowe typy zasobów i operacji na potrzeby obsługi scenariusza roli katalogu klienta
  * Typ zasobu "[CustomerDirectoryRole](auditing-resources.md)"
  * Typy operacji "[AddUserMember](auditing-resources.md)" i "[RemoveUserMember](auditing-resources.md)"

* Aktualizacje zestawu SDK na koncie klientów — Obsługa następujących interfejsów API
  * Pobierz/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus
  * Pobierz/Customers/{Customer-tenant-ID}/Qualifications 
  * Ogłoś/Customers/{customer_id}/Qualifications? Code = {validationCode}

* **Następujące zmiany wprowadzono w ramach nowych rodzajów handlu, które są obecnie dostępne na podstawie zaproszenia dla partnerów, którzy są częścią M365/D365 New Commerce Experience Technical Preview.** Partnerzy, którzy nie są częścią nowej prywatnej wersji zapoznawczej commerce, nie powinni mieć wpływu i powinny być zgodni z poprzednimi wersjami.
  * Zmiany w katalogu:
    * Pobierz/Products/{Product-ID}/SKUs/{SKU-ID}
  * Kup i Zarządzaj:
    * Pobierz/customers/{customerId}/subscriptions
    * Pobierz/customers/{customerId}/subscriptions/{subscriptionId}
    * /Customers/{customerId}/subscriptions/{subscriptionId} poprawek
    * Pobierz/customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities
    * Pobierz/customers/{customerId}/subscriptions/{subscriptionId}/transitions
    * Opublikuj/customers/{customerId}/subscriptions/{subscriptionId}/transitions


## <a name="version-1163"></a>1.16.3 wersja

[Zestaw Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v 1.16.3 jest teraz ogólnie dostępny. Zaktualizowane [przykłady serwisu GitHub](https://github.com/Microsoft/Partner-Center-DotNet-Samples) są również dostępne. W tej wersji uwzględniono następujące zmiany:

* SelfServePolicies — dodano nowe funkcje
  * [GetSelfServePolicies](get-a-self-serve-policy-by-id.md)
  * [GetListOfSelfServicePolicies](get-a-list-of-self-serve-policies.md)
  * [CreateSelfServePolicies](create-a-self-serve-policy.md)
  * [UpdateSelfServePolicies](update-a-self-serve-policy.md)
  * [DeleteSelfServePolicies](delete-a-self-serve-policy.md)

* Profil firmy dla klientów
  * Dodano [OrganizationRegistrationNumber](create-a-customer.md)

* CustomerBillingProfile.DefaultAddress
  * Dodano MiddleName

## <a name="version-1162"></a>1.16.2 wersja

[Zestaw Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v 1.16.2 jest teraz ogólnie dostępny. Zaktualizowane [przykłady serwisu GitHub](https://github.com/Microsoft/Partner-Center-DotNet-Samples) są również dostępne. W tej wersji uwzględniono następujące zmiany:

* Aktualizacja obsługiwanych typów operacji dla rekordu inspekcji. Nowo dodane są następujące:
  * CreateSelfServePolicy
  * UpdateSelfServePolicy
  * DeleteSelfServePolicy
  * RemovePartnerRelationship
  * DeleteTipCustomer
  * CreateRelatedReferral
  * UpdateRelatedReferral

* Tworzenie żądania obsługi jest obecnie przestarzałe
* Tematy pomocy technicznej są obecnie przestarzałe


## <a name="version-1161"></a>1.16.1 wersja

[Zestaw Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v 1.16.1 jest teraz ogólnie dostępny. Zaktualizowane [przykłady serwisu GitHub](https://github.com/Microsoft/Partner-Center-DotNet-Samples) są również dostępne. W tej wersji uwzględniono następujące zmiany:

Przeprowadzono migrację istniejącego zestawu SDK Centrum partnerskiego firmy Microsoft, .NET Framework na .NET Standard platformę 2,0. Spowoduje to udostępnienie zestawu SDK zgodnego z istniejącymi aplikacjami przy użyciu .NET Framework 4.6.1 i nowszych. Zestaw SDK będzie obsługiwał platformę .NET Core 2,0 i nowsze. Sprawdź [obsługę implementacji platformy .NET](/dotnet/standard/net-standard) przed przekazaniem jej do istniejących aplikacji.   


## <a name="version-1153"></a>1.15.3 wersja
[Zestaw Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v 1.15.3 jest teraz ogólnie dostępny. Dostępne są również zaktualizowane interfejsy API REST i [przykłady usługi GitHub](https://github.com/Microsoft/Partner-Center-DotNet-Samples) . W tej wersji uwzględniono następujące zmiany:

* Umowa partnerska
  * Dodano możliwość weryfikowania przez dostawców pośrednich [stanu umowy partnerskiej firmy Microsoft w odniesieniu do pośrednich odsprzedawcaów](verify-indirect-reseller-mpa-status.md).
* Produkty
  * Poniższe dwa interfejsy zostały nieprawidłowo umieszczone w przestrzeni nazw Microsoft. Store. PartnerCenter. Products. Teraz znajdują się one w przestrzeni nazw Microsoft. Store. PartnerCenter. Customers. Products.
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope
