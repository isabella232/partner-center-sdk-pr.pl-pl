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
# <a name="remove-a-reseller-relationship-with-a-customer"></a><span data-ttu-id="5bc72-103">Usuwanie relacji odsprzedaży z klientem</span><span class="sxs-lookup"><span data-stu-id="5bc72-103">Remove a reseller relationship with a customer</span></span>

<span data-ttu-id="5bc72-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="5bc72-104">**Applies To**</span></span>

- <span data-ttu-id="5bc72-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="5bc72-105">Partner Center</span></span>

<span data-ttu-id="5bc72-106">Usuń relację odsprzedawcy z klientem, do którego nie masz już transakcji.</span><span class="sxs-lookup"><span data-stu-id="5bc72-106">Remove a reseller relationship with a customer that you no longer have transactions with.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bc72-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5bc72-107">Prerequisites</span></span>

- <span data-ttu-id="5bc72-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5bc72-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5bc72-109">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5bc72-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="5bc72-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5bc72-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5bc72-111">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="5bc72-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5bc72-112">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="5bc72-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5bc72-113">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="5bc72-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5bc72-114">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="5bc72-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5bc72-115">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5bc72-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="5bc72-116">Wszystkie zamówienia wystąpień zarezerwowanych maszyn wirtualnych platformy Azure muszą zostać anulowane przed usunięciem relacji odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="5bc72-116">All Azure Reserved VM Instance orders must be canceled before a reseller relationship is removed.</span></span> <span data-ttu-id="5bc72-117">Zadzwoń do pomocy technicznej platformy Azure w celu anulowania wszelkich otwartych zamówień wystąpień zarezerwowanych maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5bc72-117">Call Azure support for canceling any open Azure Reserved VM Instance orders.</span></span>

## <a name="c"></a><span data-ttu-id="5bc72-118">C\#</span><span class="sxs-lookup"><span data-stu-id="5bc72-118">C\#</span></span>

<span data-ttu-id="5bc72-119">Aby usunąć relację odsprzedawcy dla klienta, należy najpierw upewnić się, że wszystkie aktywne Azure Reserved VM Instances dla tego klienta zostały anulowane.</span><span class="sxs-lookup"><span data-stu-id="5bc72-119">To remove the reseller relationship for a customer, first ensure that any active Azure Reserved VM Instances for that customer are canceled.</span></span> <span data-ttu-id="5bc72-120">Następnie upewnij się, że wszystkie aktywne subskrypcje dla tego klienta zostały zawieszone.</span><span class="sxs-lookup"><span data-stu-id="5bc72-120">Next, ensure that all active subscriptions for that customer are suspended.</span></span> <span data-ttu-id="5bc72-121">Aby to zrobić, określ identyfikator klienta, dla którego chcesz usunąć relację odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="5bc72-121">To do so, determine the ID of the customer for whom you want to delete the reseller relationship.</span></span> <span data-ttu-id="5bc72-122">W poniższym przykładzie kodu użytkownik jest monitowany o podanie identyfikatora klienta.</span><span class="sxs-lookup"><span data-stu-id="5bc72-122">In the following code example, the user is prompted to provide the customer identifier.</span></span>

<span data-ttu-id="5bc72-123">Aby określić, czy Azure Reserved VM Instances dla klienta muszą zostać anulowane, Pobierz kolekcję uprawnień przez wywołanie metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu identyfikatora klienta, aby określić klienta i Właściwość [**uprawnień**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) do pobrania interfejsu do operacji zbierania uprawnień.</span><span class="sxs-lookup"><span data-stu-id="5bc72-123">To determine if any Azure Reserved VM Instances for the customer must be canceled, retrieve the collection of entitlements by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and the [**Entitlements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to entitlement collection operations.</span></span> <span data-ttu-id="5bc72-124">Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) , aby pobrać kolekcję uprawnień.</span><span class="sxs-lookup"><span data-stu-id="5bc72-124">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) method to retrieve the entitlement collection.</span></span> <span data-ttu-id="5bc72-125">Odfiltruj kolekcję dla dowolnych uprawnień [**z wartością typu uprawnieńtype**](entitlement-resources.md#entitlementtype) [**. VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) , a jeśli istnieją, Anuluj je, wywołując pomoc techniczną przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="5bc72-125">Filter the collection for any entitlements with an [**EntitlementType**](entitlement-resources.md#entitlementtype) value of [**EntitlementType.VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) and if there are any, cancel them by calling support before proceeding.</span></span>

<span data-ttu-id="5bc72-126">Następnie Pobierz kolekcję subskrypcji klienta, wywołując metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu identyfikatora klienta, aby określić klienta i Właściwość [**subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) do pobrania interfejsu do operacji zbierania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5bc72-126">Then, retrieve a collection of the customer's subscriptions by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to subscription collection operations.</span></span> <span data-ttu-id="5bc72-127">Na koniec Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) , aby pobrać kolekcję subskrypcje klienta.</span><span class="sxs-lookup"><span data-stu-id="5bc72-127">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) method to retrieve the customer's subscriptions collection.</span></span> <span data-ttu-id="5bc72-128">Przechodząc do kolekcji subskrypcji i upewnij się, że żadna z subskrypcji nie ma żadnej subskrypcji. wartość właściwości [**status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) elementu [**SubscriptionStatus. Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span><span class="sxs-lookup"><span data-stu-id="5bc72-128">Traverse the subscription collection and ensure that none of the subscriptions have a [**Subscriptions.Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property value of [**SubscriptionStatus.Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="5bc72-129">Jeśli subskrypcja jest nadal aktywna, zapoznaj się z tematem [wstrzymywanie subskrypcji](https://review.docs.microsoft.com/partner-center/develop/suspend-a-subscription) , aby uzyskać informacje na temat sposobu jej wstrzymania.</span><span class="sxs-lookup"><span data-stu-id="5bc72-129">If a subscription is still active, see [Suspend a subscription](https://review.docs.microsoft.com/partner-center/develop/suspend-a-subscription) for information on how to suspend it.</span></span>

<span data-ttu-id="5bc72-130">Po potwierdzeniu, że wszystkie aktywne Azure Reserved VM Instances dla tego klienta zostały anulowane, a wszystkie aktywne subskrypcje są zawieszone, można usunąć relację odsprzedawcy dla klienta.</span><span class="sxs-lookup"><span data-stu-id="5bc72-130">After confirming that all active Azure Reserved VM Instances for that customer are canceled and all active subscriptions are suspended, you can remove the reseller relationship for the customer.</span></span> <span data-ttu-id="5bc72-131">Najpierw utwórz nowy obiekt [Customer/dotnet/API/Microsoft. Store. partnercenter. models. Customers. Customers) z właściwością [Customer. RelationshipToPartner/dotnet/API/Microsoft. Store. partnercenter. models. Customers. Customer. RelationshipToPartner) ustawioną na wartość [**CustomerPartnerRelationship. None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship).</span><span class="sxs-lookup"><span data-stu-id="5bc72-131">First, create a new [Customer/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object with the [Customer.RelationshipToPartner/dotnet/api/microsoft.store.partnercenter.models.customers.customer.relationshiptopartner) property set to [**CustomerPartnerRelationship.None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship).</span></span> <span data-ttu-id="5bc72-132">Następnie Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu identyfikatora klienta, aby określić klienta, i Wywołaj metodę **patch** , przekazując nowy obiekt klienta.</span><span class="sxs-lookup"><span data-stu-id="5bc72-132">Then call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and call the **Patch** method, passing in the new customer object.</span></span>

<span data-ttu-id="5bc72-133">Aby ponownie ustanowić relację, powtórz proces [Żądaj relacji odsprzedawcy/partnera — centrum/projektowanie/żądanie-odsprzedawca-relacja ").</span><span class="sxs-lookup"><span data-stu-id="5bc72-133">To re-establish the relationship, repeat the process of [requesting a reseller relationship/partner-center/develop/request-reseller-relationship).</span></span>

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

<span data-ttu-id="5bc72-134">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="5bc72-134">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5bc72-135">**Project**: PartnerSDK. FeatureSample **Klasa**: DeletePartnerCustomerRelationship.cs</span><span class="sxs-lookup"><span data-stu-id="5bc72-135">**Project**: PartnerSDK.FeatureSample **Class**: DeletePartnerCustomerRelationship.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5bc72-136">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="5bc72-136">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5bc72-137">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="5bc72-137">Request syntax</span></span>

| <span data-ttu-id="5bc72-138">Metoda</span><span class="sxs-lookup"><span data-stu-id="5bc72-138">Method</span></span>     | <span data-ttu-id="5bc72-139">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="5bc72-139">Request URI</span></span>                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5bc72-140">**WYSŁANA**</span><span class="sxs-lookup"><span data-stu-id="5bc72-140">**PATCH**</span></span>  | <span data-ttu-id="5bc72-141">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/http/1.1</span><span class="sxs-lookup"><span data-stu-id="5bc72-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/ HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="5bc72-142">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="5bc72-142">URI parameter</span></span>

<span data-ttu-id="5bc72-143">Ta tabela zawiera listę wymaganych parametrów zapytania, aby usunąć relację odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="5bc72-143">This table lists the required query parameters to remove a reseller relationship.</span></span>

| <span data-ttu-id="5bc72-144">Nazwa</span><span class="sxs-lookup"><span data-stu-id="5bc72-144">Name</span></span>                   | <span data-ttu-id="5bc72-145">Typ</span><span class="sxs-lookup"><span data-stu-id="5bc72-145">Type</span></span>     | <span data-ttu-id="5bc72-146">Wymagane</span><span class="sxs-lookup"><span data-stu-id="5bc72-146">Required</span></span> | <span data-ttu-id="5bc72-147">Opis</span><span class="sxs-lookup"><span data-stu-id="5bc72-147">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="5bc72-148">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="5bc72-148">**customer-tenant-id**</span></span> | <span data-ttu-id="5bc72-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="5bc72-149">**guid**</span></span> | <span data-ttu-id="5bc72-150">Y</span><span class="sxs-lookup"><span data-stu-id="5bc72-150">Y</span></span>        | <span data-ttu-id="5bc72-151">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="5bc72-151">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5bc72-152">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="5bc72-152">Request headers</span></span>

<span data-ttu-id="5bc72-153">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5bc72-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5bc72-154">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="5bc72-154">Request body</span></span>

<span data-ttu-id="5bc72-155">W treści żądania wymagany jest zasób **klienta** .</span><span class="sxs-lookup"><span data-stu-id="5bc72-155">A **Customer** resource is required in the request body.</span></span> <span data-ttu-id="5bc72-156">Upewnij się, że właściwość **RelationshipToPartner** ma wartość none.</span><span class="sxs-lookup"><span data-stu-id="5bc72-156">Ensure the **RelationshipToPartner** property has been set to none.</span></span>

### <a name="request-example"></a><span data-ttu-id="5bc72-157">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="5bc72-157">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="5bc72-158">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="5bc72-158">REST response</span></span>

<span data-ttu-id="5bc72-159">Jeśli to się powiedzie, ta metoda usuwa relację odsprzedawcy dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="5bc72-159">If successful, this method removes a reseller relationship for the specified customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5bc72-160">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="5bc72-160">Response success and error codes</span></span>

<span data-ttu-id="5bc72-161">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="5bc72-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5bc72-162">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="5bc72-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5bc72-163">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5bc72-163">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5bc72-164">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="5bc72-164">Response example</span></span>

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
