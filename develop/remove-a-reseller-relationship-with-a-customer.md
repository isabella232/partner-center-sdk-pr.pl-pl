---
title: Usuwanie relacji odsprzedaży z klientem
description: Jak usunąć relację odsprzedawcy z klientem, z który nie masz już transakcji.
ms.date: 01/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 45eca3564c3b9078e04d1f8155d08849a589d52f
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446602"
---
# <a name="remove-a-reseller-relationship-with-a-customer"></a>Usuwanie relacji odsprzedaży z klientem

Usuń relację odsprzedawcy z klientem, z który nie masz już transakcji.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Wszystkie zamówienia wystąpień zarezerwowanych maszyn wirtualnych platformy Azure muszą zostać anulowane przed usunięciem relacji odsprzedawcy. Skontaktuj się z pomocą techniczną platformy Azure, aby anulować wszystkie otwarte zamówienia wystąpień zarezerwowanych maszyn wirtualnych platformy Azure.

## <a name="c"></a>C\#

Aby usunąć relację odsprzedawcy dla klienta, najpierw upewnij się, że wszystkie aktywne Azure Reserved VM Instances dla tego klienta zostały anulowane. Następnie upewnij się, że wszystkie aktywne subskrypcje dla tego klienta są wstrzymane. W tym celu określ identyfikator klienta, dla którego chcesz usunąć relację odsprzedawcy. W poniższym przykładzie kodu użytkownik jest monitowany o podanie identyfikatora klienta.

Aby ustalić, czy należy anulować jakikolwiek element Azure Reserved VM Instances klienta, pobierz kolekcję uprawnień, wywołując metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu identyfikatora klienta w celu określenia klienta oraz właściwość [**Entitlements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) w celu pobrania interfejsu operacji zbierania uprawnień. Wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) aby pobrać kolekcję uprawnień. Przefiltruj kolekcję pod celu uzyskania uprawnień z wartością [**EntitlementType.VirtualMachineReservedInstance,**](entitlement-resources.md#entitlementtype) a jeśli istnieją, anuluj je, wywołując pomoc techniczną przed podjęciem pracy. [](entitlement-resources.md#entitlementtype)

Następnie pobierz kolekcję subskrypcji klienta, wywołując metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu identyfikatora klienta w celu określenia klienta, oraz właściwość [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) w celu pobrania interfejsu operacji zbierania subskrypcji. Na koniec wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) aby pobrać kolekcję subskrypcji klienta. Przejdź przez kolekcję subskrypcji i upewnij się, że żadna z subskrypcji nie ma wartości właściwości [**Subscriptions.Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) [**o wartości SubscriptionStatus.Active.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus) Jeśli subskrypcja jest nadal aktywna, zobacz [Wstrzymywanie subskrypcji,](suspend-a-subscription.md) aby uzyskać informacje na temat sposobu jej wstrzymania.

Po potwierdzeniu, że wszystkie aktywne Azure Reserved VM Instances dla tego klienta zostaną anulowane i wszystkie aktywne subskrypcje zostaną zawieszone, możesz usunąć relację odsprzedawcy dla klienta. Najpierw utwórz nowy obiekt [Customer/dotnet/api/microsoft.store.partnercenter.models.customers.customer) z właściwością [Customer.RelationshipToPartner/dotnet/api/microsoft.store.partnercenter.models.customers.customer.relationshiptopartner) ustawioną na [**CustomerPartnerRelationship.None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship). Następnie wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu identyfikatora klienta, aby określić klienta, i wywołaj metodę **Patch,** przekazując obiekt nowego klienta.

Aby ponownie ustanowić relację, powtórz proces [żądanie relacji odsprzedawcy/centrum partnerskiego/develop/request-reseller-relationship).

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

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** PartnerSDK.FeatureSample, **klasa**: DeletePartnerCustomerRelationship.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda     | Identyfikator URI żądania                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **Patch**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/ HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Ta tabela zawiera listę parametrów zapytania wymaganych do usunięcia relacji odsprzedawcy.

| Nazwa                   | Typ     | Wymagane | Opis                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **identyfikator dzierżawy klienta** | **guid** | Y        | Wartość to identyfikator GUID sformatowany **jako customer-tenant-id,** który identyfikuje klienta. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

W **treści** żądania jest wymagany zasób Klient. Upewnij **się, że właściwość RelationshipToPartner** została ustawiona na wartość none.

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

W przypadku powodzenia ta metoda usuwa relację odsprzedawcy dla określonego klienta.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)

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
