---
title: Anulowanie zamówienia z piaskownicy integracji
description: Dowiedz się, jak za pomocą Partner Center API anulować różne typy zamówień subskrypcji z kont piaskownicy integracji.
ms.date: 04/28/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4c4b658f406e420d8d3cd425688364fe3d440d3d
ms.sourcegitcommit: a3a78ec0f5078645b5a4f3b534165eef30f2c822
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/30/2021
ms.locfileid: "113104975"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a><span data-ttu-id="b5447-103">Anulowanie zamówienia z piaskownicy integracji przy użyciu Partner Center API</span><span class="sxs-lookup"><span data-stu-id="b5447-103">Cancel an order from the integration sandbox using Partner Center APIs</span></span>

<span data-ttu-id="b5447-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b5447-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b5447-105">W tym artykule opisano, jak za pomocą Partner Center API anulować różne typy zamówień subskrypcji z kont piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="b5447-105">This article describes how to use Partner Center APIs to cancel different types of subscription orders from integration sandbox accounts.</span></span> <span data-ttu-id="b5447-106">Takie zamówienia mogą obejmować wystąpienia zarezerwowane, oprogramowanie i zamówienia subskrypcji oprogramowania jako usługi (SaaS) na platformie handlowej.</span><span class="sxs-lookup"><span data-stu-id="b5447-106">Such orders can include reserved instances, software, and commercial marketplace Software as a Service (SaaS) subscription orders.</span></span>

> [!NOTE] 
> <span data-ttu-id="b5447-107">Należy pamiętać, że anulowanie zamówień subskrypcji SaaS wystąpienia zarezerwowanego lub komercyjnej platformy handlowej jest możliwe tylko z kont piaskownicy integracji.</span><span class="sxs-lookup"><span data-stu-id="b5447-107">Please be aware that the cancellations of reserved instance, or commercial marketplace SaaS subscription orders are only possible from integration sandbox accounts.</span></span> <span data-ttu-id="b5447-108">Nie można anulować żadnych zamówień piaskownicy starszych niż 60 dni Partner Center.</span><span class="sxs-lookup"><span data-stu-id="b5447-108">Any sandbox orders which are older than 60 days cannot be cancelled from Partner Center.</span></span>

<span data-ttu-id="b5447-109">Aby anulować produkcyjne zamówienia oprogramowania za pośrednictwem interfejsu API, [użyj polecenia cancel-software-purchases.](cancel-software-purchases.md)</span><span class="sxs-lookup"><span data-stu-id="b5447-109">To cancel production orders of software through API, use [cancel-software-purchases](cancel-software-purchases.md).</span></span>
<span data-ttu-id="b5447-110">Możesz również anulować produkcyjne zamówienia oprogramowania za pośrednictwem pulpitu [nawigacyjnego, anulując zakup.](/partner-center/csp-software-subscriptions)</span><span class="sxs-lookup"><span data-stu-id="b5447-110">You can also cancel production orders of software through dashboard using [cancel a purchase](/partner-center/csp-software-subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5447-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b5447-111">Prerequisites</span></span>

- <span data-ttu-id="b5447-112">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b5447-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b5447-113">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b5447-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b5447-114">Konto partnera piaskownicy integracji z klientem z aktywnym wystąpieniem zarezerwowanym/ oprogramowaniem /zamówieniami subskrypcji SaaS innych firm.</span><span class="sxs-lookup"><span data-stu-id="b5447-114">An integration sandbox partner account with a customer having active reserved instance / software / third-party SaaS subscription orders.</span></span>

## <a name="c"></a><span data-ttu-id="b5447-115">C\#</span><span class="sxs-lookup"><span data-stu-id="b5447-115">C\#</span></span>

<span data-ttu-id="b5447-116">Aby anulować zamówienie z piaskownicy integracji, przekaż poświadczenia konta do metody , aby uzyskać [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) interfejs do uzyskania operacji [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) partnera.</span><span class="sxs-lookup"><span data-stu-id="b5447-116">To cancel an order from the integration sandbox, pass your account credentials to the [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to get partner operations.</span></span>

<span data-ttu-id="b5447-117">Aby wybrać konkretne [zamówienie,](order-resources.md#order)użyj operacji partnera i wywołaj metodę z identyfikatorem klienta, aby określić klienta, a następnie z identyfikatorem zamówienia, aby określić zamówienie, oraz metodę lub , [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) aby je **`Orders.ById()`** **`Get`** **`GetAsync`** pobrać.</span><span class="sxs-lookup"><span data-stu-id="b5447-117">To select a particular [Order](order-resources.md#order), use the partner operations and call [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer, followed by **`Orders.ById()`** with order identifier to specify the order and finally **`Get`** or **`GetAsync`** method to retrieve it.</span></span>

<span data-ttu-id="b5447-118">Ustaw właściwość [**`Order.Status`**](order-resources.md#order) na i użyj metody , aby `cancelled` **`Patch()`** zaktualizować zamówienie.</span><span class="sxs-lookup"><span data-stu-id="b5447-118">Set the [**`Order.Status`**](order-resources.md#order) property to `cancelled` and use the **`Patch()`** method to update the order.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="b5447-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="b5447-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b5447-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="b5447-120">Request syntax</span></span>

| <span data-ttu-id="b5447-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="b5447-121">Method</span></span>     | <span data-ttu-id="b5447-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="b5447-122">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="b5447-123">**Patch**</span><span class="sxs-lookup"><span data-stu-id="b5447-123">**PATCH**</span></span> | <span data-ttu-id="b5447-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b5447-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b5447-125">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="b5447-125">URI parameter</span></span>

<span data-ttu-id="b5447-126">Użyj następującego parametru zapytania, aby usunąć klienta.</span><span class="sxs-lookup"><span data-stu-id="b5447-126">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="b5447-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b5447-127">Name</span></span>                   | <span data-ttu-id="b5447-128">Typ</span><span class="sxs-lookup"><span data-stu-id="b5447-128">Type</span></span>     | <span data-ttu-id="b5447-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b5447-129">Required</span></span> | <span data-ttu-id="b5447-130">Opis</span><span class="sxs-lookup"><span data-stu-id="b5447-130">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b5447-131">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="b5447-131">**customer-tenant-id**</span></span> | <span data-ttu-id="b5447-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="b5447-132">**guid**</span></span> | <span data-ttu-id="b5447-133">Y</span><span class="sxs-lookup"><span data-stu-id="b5447-133">Y</span></span>        | <span data-ttu-id="b5447-134">Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="b5447-134">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="b5447-135">**order-id**</span><span class="sxs-lookup"><span data-stu-id="b5447-135">**order-id**</span></span> | <span data-ttu-id="b5447-136">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="b5447-136">**string**</span></span> | <span data-ttu-id="b5447-137">Y</span><span class="sxs-lookup"><span data-stu-id="b5447-137">Y</span></span>        | <span data-ttu-id="b5447-138">Wartość jest ciągiem oznaczający identyfikatory zamówień, które muszą zostać anulowane.</span><span class="sxs-lookup"><span data-stu-id="b5447-138">The value is a string denoting the order IDs that need to be canceled.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b5447-139">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="b5447-139">Request headers</span></span>

<span data-ttu-id="b5447-140">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b5447-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b5447-141">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="b5447-141">Request body</span></span>

```http
{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

### <a name="request-example"></a><span data-ttu-id="b5447-142">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="b5447-142">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="b5447-143">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="b5447-143">REST response</span></span>

<span data-ttu-id="b5447-144">W przypadku powodzenia ta metoda zwraca anulowane zamówienie.</span><span class="sxs-lookup"><span data-stu-id="b5447-144">If successful, this method returns the canceled order.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b5447-145">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b5447-145">Response success and error codes</span></span>

<span data-ttu-id="b5447-146">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="b5447-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b5447-147">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="b5447-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b5447-148">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="b5447-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b5447-149">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b5447-149">Response example</span></span>

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
