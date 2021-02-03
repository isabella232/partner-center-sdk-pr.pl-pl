---
title: Anulowanie zamówienia z piaskownicy integracji
description: Dowiedz się, jak za pomocą interfejsów API usługi Partner Center anulować różne typy zamówień subskrypcji z kont piaskownicy integracji.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 363bf209e27d5223259c8c533710a3b35bbef1e6
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768597"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a><span data-ttu-id="eca49-103">Anulowanie zamówienia z piaskownicy integracji przy użyciu interfejsów API usługi Partner Center</span><span class="sxs-lookup"><span data-stu-id="eca49-103">Cancel an order from the integration sandbox using Partner Center APIs</span></span>

<span data-ttu-id="eca49-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="eca49-104">**Applies to:**</span></span>

- <span data-ttu-id="eca49-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="eca49-105">Partner Center</span></span>
- <span data-ttu-id="eca49-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="eca49-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="eca49-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="eca49-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="eca49-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="eca49-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="eca49-109">W tym artykule opisano sposób używania interfejsów API usługi Partner Center do anulowania różnych typów zamówień subskrypcji z kont piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="eca49-109">This article describes how to use Partner Center APIs to cancel different types of subscription orders from integration sandbox accounts.</span></span> <span data-ttu-id="eca49-110">Takie zamówienia mogą obejmować wystąpienia zarezerwowane, oprogramowanie i komercyjne zamówienie na oprogramowanie Marketplace jako usługa (SaaS).</span><span class="sxs-lookup"><span data-stu-id="eca49-110">Such orders can include reserved instances, software, and commercial marketplace Software as a Service (SaaS) subscription orders.</span></span>

>[!NOTE]
><span data-ttu-id="eca49-111">Należy pamiętać, że anulowane subskrypcje wystąpień zarezerwowanych lub komercyjnych zakupów rynkowych SaaS są możliwe tylko z kont piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="eca49-111">Please be aware that the cancellations of reserved instance, or commercial marketplace SaaS subscription orders are only possible from integration sandbox accounts.</span></span>  

<span data-ttu-id="eca49-112">Aby anulować zlecenia produkcyjne oprogramowania za pomocą interfejsu API, należy użyć polecenia [Anuluj zakup oprogramowania](cancel-software-purchases.md).</span><span class="sxs-lookup"><span data-stu-id="eca49-112">To cancel production orders of software through API, use [cancel-software-purchases](cancel-software-purchases.md).</span></span>
<span data-ttu-id="eca49-113">Możesz również anulować zlecenia produkcyjne oprogramowania za pośrednictwem pulpitu nawigacyjnego, używając [przycisku Anuluj zakup](/partner-center/csp-software-subscriptions).</span><span class="sxs-lookup"><span data-stu-id="eca49-113">You can also cancel production orders of software through dashboard using [cancel a purchase](/partner-center/csp-software-subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eca49-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eca49-114">Prerequisites</span></span>

- <span data-ttu-id="eca49-115">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="eca49-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="eca49-116">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="eca49-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="eca49-117">Konto partnera piaskownicy integracji z klientem z aktywną alternatywnym wystąpieniem/oprogramowaniem/SaaSą subskrypcją innych firm.</span><span class="sxs-lookup"><span data-stu-id="eca49-117">An integration sandbox partner account with a customer having active reserved instance / software / third-party SaaS subscription orders.</span></span>

## <a name="c"></a><span data-ttu-id="eca49-118">C\#</span><span class="sxs-lookup"><span data-stu-id="eca49-118">C\#</span></span>

<span data-ttu-id="eca49-119">Aby anulować zamówienie z piaskownicy integracji, Przekaż poświadczenia konta do [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) metody w celu uzyskania [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) interfejsu umożliwiającego uzyskanie operacji partnerskich.</span><span class="sxs-lookup"><span data-stu-id="eca49-119">To cancel an order from the integration sandbox, pass your account credentials to the [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to get partner operations.</span></span>

<span data-ttu-id="eca49-120">Aby wybrać określoną [kolejność](order-resources.md#order), użyj operacji partnera i [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metody Call z identyfikatorem klienta, aby określić klienta, a następnie pozycję **`Orders.ById()`** z identyfikatorem zamówienia, aby określić kolejność, a wreszcie **`Get`** lub metodę, **`GetAsync`** Aby ją pobrać.</span><span class="sxs-lookup"><span data-stu-id="eca49-120">To select a particular [Order](order-resources.md#order), use the partner operations and call [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer, followed by **`Orders.ById()`** with order identifier to specify the order and finally **`Get`** or **`GetAsync`** method to retrieve it.</span></span>

<span data-ttu-id="eca49-121">Ustaw [**`Order.Status`**](order-resources.md#order) Właściwość na `cancelled` i użyj metody, **`Patch()`** Aby zaktualizować kolejność.</span><span class="sxs-lookup"><span data-stu-id="eca49-121">Set the [**`Order.Status`**](order-resources.md#order) property to `cancelled` and use the **`Patch()`** method to update the order.</span></span>

``` csharp
// IPartnerCredentials tipAccountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

// Cancel order
var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a><span data-ttu-id="eca49-122">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="eca49-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="eca49-123">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="eca49-123">Request syntax</span></span>

| <span data-ttu-id="eca49-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="eca49-124">Method</span></span>     | <span data-ttu-id="eca49-125">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="eca49-125">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="eca49-126">**WYSŁANA**</span><span class="sxs-lookup"><span data-stu-id="eca49-126">**PATCH**</span></span> | <span data-ttu-id="eca49-127">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="eca49-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="eca49-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="eca49-128">URI parameter</span></span>

<span data-ttu-id="eca49-129">Użyj następującego parametru zapytania, aby usunąć klienta.</span><span class="sxs-lookup"><span data-stu-id="eca49-129">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="eca49-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="eca49-130">Name</span></span>                   | <span data-ttu-id="eca49-131">Typ</span><span class="sxs-lookup"><span data-stu-id="eca49-131">Type</span></span>     | <span data-ttu-id="eca49-132">Wymagane</span><span class="sxs-lookup"><span data-stu-id="eca49-132">Required</span></span> | <span data-ttu-id="eca49-133">Opis</span><span class="sxs-lookup"><span data-stu-id="eca49-133">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="eca49-134">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="eca49-134">**customer-tenant-id**</span></span> | <span data-ttu-id="eca49-135">**guid**</span><span class="sxs-lookup"><span data-stu-id="eca49-135">**guid**</span></span> | <span data-ttu-id="eca49-136">Y</span><span class="sxs-lookup"><span data-stu-id="eca49-136">Y</span></span>        | <span data-ttu-id="eca49-137">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="eca49-137">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="eca49-138">**Identyfikator zamówienia**</span><span class="sxs-lookup"><span data-stu-id="eca49-138">**order-id**</span></span> | <span data-ttu-id="eca49-139">**parametry**</span><span class="sxs-lookup"><span data-stu-id="eca49-139">**string**</span></span> | <span data-ttu-id="eca49-140">Y</span><span class="sxs-lookup"><span data-stu-id="eca49-140">Y</span></span>        | <span data-ttu-id="eca49-141">Wartość jest ciągiem wskazującym identyfikatory kolejności, które muszą być anulowane.</span><span class="sxs-lookup"><span data-stu-id="eca49-141">The value is a string denoting the order IDs that need to be canceled.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="eca49-142">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="eca49-142">Request headers</span></span>

<span data-ttu-id="eca49-143">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="eca49-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="eca49-144">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="eca49-144">Request body</span></span>

```http
{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

### <a name="request-example"></a><span data-ttu-id="eca49-145">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="eca49-145">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

## <a name="rest-response"></a><span data-ttu-id="eca49-146">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="eca49-146">REST response</span></span>

<span data-ttu-id="eca49-147">Jeśli to się powiedzie, metoda zwraca anulowaną kolejność.</span><span class="sxs-lookup"><span data-stu-id="eca49-147">If successful, this method returns the canceled order.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="eca49-148">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="eca49-148">Response success and error codes</span></span>

<span data-ttu-id="eca49-149">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="eca49-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="eca49-150">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="eca49-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="eca49-151">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="eca49-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="eca49-152">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="eca49-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "alternateId": "11fc4bdfd47a",
    "referenceCustomerId": "bd59b416-37f9-4d8f-8df3-5750111fc615",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0DWT0:0001:DG7GMGF0DSQR",
            "termDuration": "",
            "transactionType": "New",
            "friendlyName": "Microsoft Identity Manager 2016 - 1 User CAL",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DWT0?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001/availabilities/DG7GMGF0DSQR?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-02-21T17:56:21.1335741Z",
    "status": "cancelled",
    "transactionType": "UserPurchase",
    "attributes": {
        "objectType": "Order"
    }
}
```
