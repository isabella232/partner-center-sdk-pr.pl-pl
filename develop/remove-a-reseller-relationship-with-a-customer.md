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
# <a name="remove-a-reseller-relationship-with-a-customer"></a><span data-ttu-id="2cbff-103">Usuwanie relacji odsprzedaży z klientem</span><span class="sxs-lookup"><span data-stu-id="2cbff-103">Remove a reseller relationship with a customer</span></span>

<span data-ttu-id="2cbff-104">Usuń relację odsprzedawcy z klientem, z który nie masz już transakcji.</span><span class="sxs-lookup"><span data-stu-id="2cbff-104">Remove a reseller relationship with a customer that you no longer have transactions with.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2cbff-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2cbff-105">Prerequisites</span></span>

- <span data-ttu-id="2cbff-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2cbff-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2cbff-107">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2cbff-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="2cbff-108">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2cbff-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2cbff-109">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="2cbff-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2cbff-110">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="2cbff-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2cbff-111">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="2cbff-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2cbff-112">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="2cbff-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2cbff-113">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2cbff-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="2cbff-114">Wszystkie zamówienia wystąpień zarezerwowanych maszyn wirtualnych platformy Azure muszą zostać anulowane przed usunięciem relacji odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="2cbff-114">All Azure Reserved VM Instance orders must be canceled before a reseller relationship is removed.</span></span> <span data-ttu-id="2cbff-115">Skontaktuj się z pomocą techniczną platformy Azure, aby anulować wszystkie otwarte zamówienia wystąpień zarezerwowanych maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2cbff-115">Call Azure support for canceling any open Azure Reserved VM Instance orders.</span></span>

## <a name="c"></a><span data-ttu-id="2cbff-116">C\#</span><span class="sxs-lookup"><span data-stu-id="2cbff-116">C\#</span></span>

<span data-ttu-id="2cbff-117">Aby usunąć relację odsprzedawcy dla klienta, najpierw upewnij się, że wszystkie aktywne Azure Reserved VM Instances dla tego klienta zostały anulowane.</span><span class="sxs-lookup"><span data-stu-id="2cbff-117">To remove the reseller relationship for a customer, first ensure that any active Azure Reserved VM Instances for that customer are canceled.</span></span> <span data-ttu-id="2cbff-118">Następnie upewnij się, że wszystkie aktywne subskrypcje dla tego klienta są wstrzymane.</span><span class="sxs-lookup"><span data-stu-id="2cbff-118">Next, ensure that all active subscriptions for that customer are suspended.</span></span> <span data-ttu-id="2cbff-119">W tym celu określ identyfikator klienta, dla którego chcesz usunąć relację odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="2cbff-119">To do so, determine the ID of the customer for whom you want to delete the reseller relationship.</span></span> <span data-ttu-id="2cbff-120">W poniższym przykładzie kodu użytkownik jest monitowany o podanie identyfikatora klienta.</span><span class="sxs-lookup"><span data-stu-id="2cbff-120">In the following code example, the user is prompted to provide the customer identifier.</span></span>

<span data-ttu-id="2cbff-121">Aby ustalić, czy należy anulować jakikolwiek element Azure Reserved VM Instances klienta, pobierz kolekcję uprawnień, wywołując metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu identyfikatora klienta w celu określenia klienta oraz właściwość [**Entitlements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) w celu pobrania interfejsu operacji zbierania uprawnień.</span><span class="sxs-lookup"><span data-stu-id="2cbff-121">To determine if any Azure Reserved VM Instances for the customer must be canceled, retrieve the collection of entitlements by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and the [**Entitlements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to entitlement collection operations.</span></span> <span data-ttu-id="2cbff-122">Wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) aby pobrać kolekcję uprawnień.</span><span class="sxs-lookup"><span data-stu-id="2cbff-122">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) method to retrieve the entitlement collection.</span></span> <span data-ttu-id="2cbff-123">Przefiltruj kolekcję pod celu uzyskania uprawnień z wartością [**EntitlementType.VirtualMachineReservedInstance,**](entitlement-resources.md#entitlementtype) a jeśli istnieją, anuluj je, wywołując pomoc techniczną przed podjęciem pracy. [](entitlement-resources.md#entitlementtype)</span><span class="sxs-lookup"><span data-stu-id="2cbff-123">Filter the collection for any entitlements with an [**EntitlementType**](entitlement-resources.md#entitlementtype) value of [**EntitlementType.VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) and if there are any, cancel them by calling support before proceeding.</span></span>

<span data-ttu-id="2cbff-124">Następnie pobierz kolekcję subskrypcji klienta, wywołując metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu identyfikatora klienta w celu określenia klienta, oraz właściwość [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) w celu pobrania interfejsu operacji zbierania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2cbff-124">Then, retrieve a collection of the customer's subscriptions by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to subscription collection operations.</span></span> <span data-ttu-id="2cbff-125">Na koniec wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) aby pobrać kolekcję subskrypcji klienta.</span><span class="sxs-lookup"><span data-stu-id="2cbff-125">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) method to retrieve the customer's subscriptions collection.</span></span> <span data-ttu-id="2cbff-126">Przejdź przez kolekcję subskrypcji i upewnij się, że żadna z subskrypcji nie ma wartości właściwości [**Subscriptions.Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) [**o wartości SubscriptionStatus.Active.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus)</span><span class="sxs-lookup"><span data-stu-id="2cbff-126">Traverse the subscription collection and ensure that none of the subscriptions have a [**Subscriptions.Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property value of [**SubscriptionStatus.Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="2cbff-127">Jeśli subskrypcja jest nadal aktywna, zobacz [Wstrzymywanie subskrypcji,](suspend-a-subscription.md) aby uzyskać informacje na temat sposobu jej wstrzymania.</span><span class="sxs-lookup"><span data-stu-id="2cbff-127">If a subscription is still active, see [Suspend a subscription](suspend-a-subscription.md) for information on how to suspend it.</span></span>

<span data-ttu-id="2cbff-128">Po potwierdzeniu, że wszystkie aktywne Azure Reserved VM Instances dla tego klienta zostaną anulowane i wszystkie aktywne subskrypcje zostaną zawieszone, możesz usunąć relację odsprzedawcy dla klienta.</span><span class="sxs-lookup"><span data-stu-id="2cbff-128">After confirming that all active Azure Reserved VM Instances for that customer are canceled and all active subscriptions are suspended, you can remove the reseller relationship for the customer.</span></span> <span data-ttu-id="2cbff-129">Najpierw utwórz nowy obiekt [Customer/dotnet/api/microsoft.store.partnercenter.models.customers.customer) z właściwością [Customer.RelationshipToPartner/dotnet/api/microsoft.store.partnercenter.models.customers.customer.relationshiptopartner) ustawioną na [**CustomerPartnerRelationship.None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship).</span><span class="sxs-lookup"><span data-stu-id="2cbff-129">First, create a new [Customer/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object with the [Customer.RelationshipToPartner/dotnet/api/microsoft.store.partnercenter.models.customers.customer.relationshiptopartner) property set to [**CustomerPartnerRelationship.None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship).</span></span> <span data-ttu-id="2cbff-130">Następnie wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu identyfikatora klienta, aby określić klienta, i wywołaj metodę **Patch,** przekazując obiekt nowego klienta.</span><span class="sxs-lookup"><span data-stu-id="2cbff-130">Then call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and call the **Patch** method, passing in the new customer object.</span></span>

<span data-ttu-id="2cbff-131">Aby ponownie ustanowić relację, powtórz proces [żądanie relacji odsprzedawcy/centrum partnerskiego/develop/request-reseller-relationship).</span><span class="sxs-lookup"><span data-stu-id="2cbff-131">To re-establish the relationship, repeat the process of [requesting a reseller relationship/partner-center/develop/request-reseller-relationship).</span></span>

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

<span data-ttu-id="2cbff-132">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2cbff-132">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2cbff-133">**Project:** PartnerSDK.FeatureSample, **klasa**: DeletePartnerCustomerRelationship.cs</span><span class="sxs-lookup"><span data-stu-id="2cbff-133">**Project**: PartnerSDK.FeatureSample **Class**: DeletePartnerCustomerRelationship.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2cbff-134">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="2cbff-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2cbff-135">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="2cbff-135">Request syntax</span></span>

| <span data-ttu-id="2cbff-136">Metoda</span><span class="sxs-lookup"><span data-stu-id="2cbff-136">Method</span></span>     | <span data-ttu-id="2cbff-137">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="2cbff-137">Request URI</span></span>                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2cbff-138">**Patch**</span><span class="sxs-lookup"><span data-stu-id="2cbff-138">**PATCH**</span></span>  | <span data-ttu-id="2cbff-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/ HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2cbff-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/ HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="2cbff-140">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="2cbff-140">URI parameter</span></span>

<span data-ttu-id="2cbff-141">Ta tabela zawiera listę parametrów zapytania wymaganych do usunięcia relacji odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="2cbff-141">This table lists the required query parameters to remove a reseller relationship.</span></span>

| <span data-ttu-id="2cbff-142">Nazwa</span><span class="sxs-lookup"><span data-stu-id="2cbff-142">Name</span></span>                   | <span data-ttu-id="2cbff-143">Typ</span><span class="sxs-lookup"><span data-stu-id="2cbff-143">Type</span></span>     | <span data-ttu-id="2cbff-144">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2cbff-144">Required</span></span> | <span data-ttu-id="2cbff-145">Opis</span><span class="sxs-lookup"><span data-stu-id="2cbff-145">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="2cbff-146">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="2cbff-146">**customer-tenant-id**</span></span> | <span data-ttu-id="2cbff-147">**guid**</span><span class="sxs-lookup"><span data-stu-id="2cbff-147">**guid**</span></span> | <span data-ttu-id="2cbff-148">Y</span><span class="sxs-lookup"><span data-stu-id="2cbff-148">Y</span></span>        | <span data-ttu-id="2cbff-149">Wartość to identyfikator GUID sformatowany **jako customer-tenant-id,** który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="2cbff-149">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2cbff-150">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="2cbff-150">Request headers</span></span>

<span data-ttu-id="2cbff-151">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2cbff-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2cbff-152">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="2cbff-152">Request body</span></span>

<span data-ttu-id="2cbff-153">W **treści** żądania jest wymagany zasób Klient.</span><span class="sxs-lookup"><span data-stu-id="2cbff-153">A **Customer** resource is required in the request body.</span></span> <span data-ttu-id="2cbff-154">Upewnij **się, że właściwość RelationshipToPartner** została ustawiona na wartość none.</span><span class="sxs-lookup"><span data-stu-id="2cbff-154">Ensure the **RelationshipToPartner** property has been set to none.</span></span>

### <a name="request-example"></a><span data-ttu-id="2cbff-155">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="2cbff-155">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="2cbff-156">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="2cbff-156">REST response</span></span>

<span data-ttu-id="2cbff-157">W przypadku powodzenia ta metoda usuwa relację odsprzedawcy dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="2cbff-157">If successful, this method removes a reseller relationship for the specified customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2cbff-158">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2cbff-158">Response success and error codes</span></span>

<span data-ttu-id="2cbff-159">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="2cbff-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2cbff-160">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="2cbff-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2cbff-161">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2cbff-161">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2cbff-162">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2cbff-162">Response example</span></span>

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
