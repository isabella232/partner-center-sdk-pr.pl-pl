---
title: Usuwanie relacji odsprzedaży z klientem
description: Jak usunąć relację odsprzedawcy z klientem, z którym nie masz już transakcji.
ms.date: 01/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 084797997e57c63b5c447379bb08ecb88ebd0cc4
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768277"
---
# <a name="remove-a-reseller-relationship-with-a-customer"></a>Usuwanie relacji odsprzedaży z klientem

**Dotyczy**

- Centrum partnerskie

Usuń relację odsprzedawcy z klientem, do którego nie masz już transakcji.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Wszystkie zamówienia wystąpień zarezerwowanych maszyn wirtualnych platformy Azure muszą zostać anulowane przed usunięciem relacji odsprzedawcy. Zadzwoń do pomocy technicznej platformy Azure w celu anulowania wszelkich otwartych zamówień wystąpień zarezerwowanych maszyn wirtualnych platformy Azure.

## <a name="c"></a>C\#

Aby usunąć relację odsprzedawcy dla klienta, należy najpierw upewnić się, że wszystkie aktywne Azure Reserved VM Instances dla tego klienta zostały anulowane. Następnie upewnij się, że wszystkie aktywne subskrypcje dla tego klienta zostały zawieszone. Aby to zrobić, określ identyfikator klienta, dla którego chcesz usunąć relację odsprzedawcy. W poniższym przykładzie kodu użytkownik jest monitowany o podanie identyfikatora klienta.

Aby określić, czy Azure Reserved VM Instances dla klienta muszą zostać anulowane, Pobierz kolekcję uprawnień przez wywołanie metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu identyfikatora klienta, aby określić klienta i Właściwość [**uprawnień**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) do pobrania interfejsu do operacji zbierania uprawnień. Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) , aby pobrać kolekcję uprawnień. Odfiltruj kolekcję dla dowolnych uprawnień [**z wartością typu uprawnieńtype**](entitlement-resources.md#entitlementtype) [**. VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) , a jeśli istnieją, Anuluj je, wywołując pomoc techniczną przed kontynuowaniem.

Następnie Pobierz kolekcję subskrypcji klienta, wywołując metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu identyfikatora klienta, aby określić klienta i Właściwość [**subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) do pobrania interfejsu do operacji zbierania subskrypcji. Na koniec Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) , aby pobrać kolekcję subskrypcje klienta. Przechodząc do kolekcji subskrypcji i upewnij się, że żadna z subskrypcji nie ma żadnej subskrypcji. wartość właściwości [**status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) elementu [**SubscriptionStatus. Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus). Jeśli subskrypcja jest nadal aktywna, zapoznaj się z tematem [wstrzymywanie subskrypcji](https://review.docs.microsoft.com/partner-center/develop/suspend-a-subscription) , aby uzyskać informacje na temat sposobu jej wstrzymania.

Po potwierdzeniu, że wszystkie aktywne Azure Reserved VM Instances dla tego klienta zostały anulowane, a wszystkie aktywne subskrypcje są zawieszone, można usunąć relację odsprzedawcy dla klienta. Najpierw utwórz nowy obiekt [Customer/dotnet/API/Microsoft. Store. partnercenter. models. Customers. Customers) z właściwością [Customer. RelationshipToPartner/dotnet/API/Microsoft. Store. partnercenter. models. Customers. Customer. RelationshipToPartner) ustawioną na wartość [**CustomerPartnerRelationship. None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship). Następnie Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu identyfikatora klienta, aby określić klienta, i Wywołaj metodę **patch** , przekazując nowy obiekt klienta.

Aby ponownie ustanowić relację, powtórz proces [Żądaj relacji odsprzedawcy/partnera — centrum/projektowanie/żądanie-odsprzedawca-relacja ").

``` csharp
// IAggregatePartner partnerOperations;

// Prompt the user the enter the customer ID.
var customerIdToDeleteRelationshipOf = this.Context.ConsoleHelper.ReadNonEmptyString("Please enter the ID of the customer you want to delete the relationship with", "The customer ID can't be empty");

// Determine if there are any active Azure Reserved VM Instances for this customer.
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Entitlements.Get();

If (entitlements.Items.Where(x => x.EntitlementType == EntitlementType.VirtualMachineReservedInstance).Any())
{
    this.Context.ConsoleHelper.Warning("Please cancel Azure Reserved Virtual Machine Instance orders through support and try again. Aborting the delete customer relationship operation");
               return;
}

// Verify that there are no active subscriptions.
ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Subscriptions.Get();
IList<Subscription> subscriptions = new List<Subscription>(customerSubscriptions.Items);

foreach (Subscription customerSubscription in subscriptions)
{
    if (customerSubscription.Status == SubscriptionStatus.Active)
    {
        this.Context.ConsoleHelper.Warning(String.Format("Subscription with ID :{0}  OfferName: {1} cannot be in active state, ", customerSubscription.Id, customerSubscription.OfferName));
        this.Context.ConsoleHelper.Warning("Please Suspend all the Subscriptions and try again. Aborting the delete customer relationship operation");
               return;
    }
}

// Delete the customer's relationship to the partner.
Customer customer = new Customer();
customer.RelationshipToPartner = CustomerPartnerRelationship.None;
customer = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Patch(customer);

if (customer.RelationshipToPartner == CustomerPartnerRelationship.None)
{
    this.Context.ConsoleHelper.Success("Customer Partner Relationship successfully deleted");
}
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Project**: PartnerSDK. FeatureSample **Klasa**: DeletePartnerCustomerRelationship.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda     | Identyfikator URI żądania                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **WYSŁANA**  | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Ta tabela zawiera listę wymaganych parametrów zapytania, aby usunąć relację odsprzedawcy.

| Nazwa                   | Typ     | Wymagane | Opis                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **Identyfikator dzierżawy klienta** | **guid** | Y        | Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , który identyfikuje klienta. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

W treści żądania wymagany jest zasób **klienta** . Upewnij się, że właściwość **RelationshipToPartner** ma wartość none.

### <a name="request-example"></a>Przykład żądania

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Authorization: Bearer <token>
Content-Length: 74
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9b4bf2ca-f374-4d51-9113-781ca87b8380
MS-RequestId: 9fef8b23-6e3e-45d2-8678-e9fe89c35af5
Date: Fri, 12 Jan 2018 00:31:55 GMT

{
    "relationshipToPartner":"none",
    "attributes":{
        "objectType":"Customer"
    }
}
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda usuwa relację odsprzedawcy dla określonego klienta.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
MS-RequestId: 7988dde4-b516-472c-b226-6d53fb18f04e
MS-CorrelationId: 9b4bf2ca-f374-4d51-9113-781ca87b8380
X-Locale: en-US
Content-Type: application/json
Content-Length: 242
Expect: 100-continue

{
    "Id":null,
    "CommerceId":null,
    "CompanyProfile":null,
    "BillingProfile":null,
    "RelationshipToPartner":"none",
    "AllowDelegatedAccess":null,
    "UserCredentials":null,
    "CustomDomains":null,
    "AssociatedPartnerId":null,
    "Attributes":{
        "ObjectType":"Customer"
    }
}
```
