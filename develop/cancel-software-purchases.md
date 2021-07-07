---
title: Anulowanie zakupów oprogramowania
description: Samoobsługowa opcja anulowania subskrypcji oprogramowania i bezterminowych zakupów oprogramowania przy użyciu Partner Center API.
ms.date: 12/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 877702ac930919ff72c6cc45a3c0e8ecc7e1b5f4
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974237"
---
# <a name="cancel-software-purchases"></a><span data-ttu-id="f1c5b-103">Anulowanie zakupów oprogramowania</span><span class="sxs-lookup"><span data-stu-id="f1c5b-103">Cancel software purchases</span></span>

<span data-ttu-id="f1c5b-104">Za pomocą interfejsów API Partner Center można anulować subskrypcje oprogramowania i bezterminowe zakupy oprogramowania (o ile te zakupy zostały dokonane w oknie anulowania od daty zakupu).</span><span class="sxs-lookup"><span data-stu-id="f1c5b-104">You can use the Partner Center APIs to cancel software subscriptions and perpetual software purchases (as long as those purchases were made within the cancellation window from the purchase date).</span></span> <span data-ttu-id="f1c5b-105">Nie musisz tworzyć biletu pomocy technicznej, aby anulować takie zmiany, i zamiast tego możesz użyć następujących metod samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="f1c5b-105">You don't need to create a support ticket to make such cancellations, and can use the following self-service methods instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1c5b-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f1c5b-106">Prerequisites</span></span>

- <span data-ttu-id="f1c5b-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f1c5b-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f1c5b-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f1c5b-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="f1c5b-109">C\#</span><span class="sxs-lookup"><span data-stu-id="f1c5b-109">C\#</span></span>

<span data-ttu-id="f1c5b-110">Aby anulować zamówienie oprogramowania,</span><span class="sxs-lookup"><span data-stu-id="f1c5b-110">To cancel a software order,</span></span>

1. <span data-ttu-id="f1c5b-111">Przekaż poświadczenia konta do metody [**CreatePartnerOperations,**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) aby uzyskać interfejs [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) w celu uzyskania operacji partnera.</span><span class="sxs-lookup"><span data-stu-id="f1c5b-111">Pass your account credentials to the [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to get partner operations.</span></span>

2. <span data-ttu-id="f1c5b-112">Wybierz konkretne [zamówienie,](order-resources.md#order) które chcesz anulować.</span><span class="sxs-lookup"><span data-stu-id="f1c5b-112">Select a particular [Order](order-resources.md#order) you wish to cancel.</span></span> <span data-ttu-id="f1c5b-113">Wywołaj [**metodę Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, a następnie **orders.ById() z** identyfikatorem zamówienia.</span><span class="sxs-lookup"><span data-stu-id="f1c5b-113">Call the [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier, followed by **Orders.ById()** with order identifier.</span></span>

3. <span data-ttu-id="f1c5b-114">Wywołaj **metodę Get** lub **GetAsync,** aby pobrać zamówienie.</span><span class="sxs-lookup"><span data-stu-id="f1c5b-114">Call the **Get** or **GetAsync** method to retrieve the order.</span></span>

4. <span data-ttu-id="f1c5b-115">Ustaw właściwość [**Order.Status**](order-resources.md#order) na `cancelled` wartość .</span><span class="sxs-lookup"><span data-stu-id="f1c5b-115">Set the [**Order.Status**](order-resources.md#order) property to `cancelled`.</span></span>

5. <span data-ttu-id="f1c5b-116">(Opcjonalnie) Jeśli chcesz określić niektóre pozycje do anulowania, ustaw element [**Order.LineItems**](order-resources.md#order) na listę elementów wierszy, które chcesz anulować.</span><span class="sxs-lookup"><span data-stu-id="f1c5b-116">(Optional) If you want to specify certain line items for cancellation, set the [**Order.LineItems**](order-resources.md#order) to list of line items that you want to cancel.</span></span>

6. <span data-ttu-id="f1c5b-117">Użyj metody **Patch(),** aby zaktualizować kolejność.</span><span class="sxs-lookup"><span data-stu-id="f1c5b-117">Use the **Patch()** method to update the order.</span></span>

``` csharp
// IPartnerCredentials accountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner accountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(accountCredentials);

// Cancel order
var order = accountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order.LineItems = new List<OrderLineItem> {
    order.LineItems.First()
};
order = accountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a><span data-ttu-id="f1c5b-118">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="f1c5b-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f1c5b-119">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="f1c5b-119">Request syntax</span></span>

| <span data-ttu-id="f1c5b-120">Metoda</span><span class="sxs-lookup"><span data-stu-id="f1c5b-120">Method</span></span>     | <span data-ttu-id="f1c5b-121">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="f1c5b-121">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="f1c5b-122">**Patch**</span><span class="sxs-lookup"><span data-stu-id="f1c5b-122">**PATCH**</span></span> | <span data-ttu-id="f1c5b-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f1c5b-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="f1c5b-124">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="f1c5b-124">URI parameters</span></span>

<span data-ttu-id="f1c5b-125">Użyj następujących parametrów zapytania, aby usunąć klienta.</span><span class="sxs-lookup"><span data-stu-id="f1c5b-125">Use the following query parameters to delete a customer.</span></span>

| <span data-ttu-id="f1c5b-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f1c5b-126">Name</span></span>                   | <span data-ttu-id="f1c5b-127">Typ</span><span class="sxs-lookup"><span data-stu-id="f1c5b-127">Type</span></span>     | <span data-ttu-id="f1c5b-128">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f1c5b-128">Required</span></span> | <span data-ttu-id="f1c5b-129">Opis</span><span class="sxs-lookup"><span data-stu-id="f1c5b-129">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f1c5b-130">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="f1c5b-130">**customer-tenant-id**</span></span> | <span data-ttu-id="f1c5b-131">**guid**</span><span class="sxs-lookup"><span data-stu-id="f1c5b-131">**guid**</span></span> | <span data-ttu-id="f1c5b-132">Y</span><span class="sxs-lookup"><span data-stu-id="f1c5b-132">Y</span></span>        | <span data-ttu-id="f1c5b-133">Wartość jest identyfikatorem dzierżawy klienta w formacie GUID, który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="f1c5b-133">The value is a GUID formatted customer tenant identifier that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="f1c5b-134">**order-id**</span><span class="sxs-lookup"><span data-stu-id="f1c5b-134">**order-id**</span></span> | <span data-ttu-id="f1c5b-135">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="f1c5b-135">**string**</span></span> | <span data-ttu-id="f1c5b-136">Y</span><span class="sxs-lookup"><span data-stu-id="f1c5b-136">Y</span></span>        | <span data-ttu-id="f1c5b-137">Wartość jest ciągiem oznaczający identyfikator zamówienia, które chcesz anulować.</span><span class="sxs-lookup"><span data-stu-id="f1c5b-137">The value is a string that denotes the identifier of the order that you want to cancel.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f1c5b-138">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="f1c5b-138">Request headers</span></span>

<span data-ttu-id="f1c5b-139">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f1c5b-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f1c5b-140">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="f1c5b-140">Request body</span></span>

```http
{
    “id”: “2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    status": "cancelled",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS"
        }
    ]
}
```

### <a name="request-example"></a><span data-ttu-id="f1c5b-141">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="f1c5b-141">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    "status": "cancelled",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS"
        }
    ]
}
```

## <a name="rest-response"></a><span data-ttu-id="f1c5b-142">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="f1c5b-142">REST response</span></span>

<span data-ttu-id="f1c5b-143">W przypadku powodzenia ta metoda zwraca zamówienie ze anulowanym wierszem.</span><span class="sxs-lookup"><span data-stu-id="f1c5b-143">If successful, this method returns the order with canceled line items.</span></span>

<span data-ttu-id="f1c5b-144">Stan zamówienia zostanie oznaczony  jako anulowane, jeśli wszystkie pozycje w zamówieniu zostaną anulowane lub zakończone, jeśli nie wszystkie pozycje w zamówieniu zostaną anulowane. </span><span class="sxs-lookup"><span data-stu-id="f1c5b-144">The order status will be marked as either **cancelled** if all the line items in the order are canceled, or **completed** if not all line items in the order are canceled.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f1c5b-145">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f1c5b-145">Response success and error codes</span></span>

<span data-ttu-id="f1c5b-146">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="f1c5b-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f1c5b-147">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="f1c5b-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f1c5b-148">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="f1c5b-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f1c5b-149">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f1c5b-149">Response example</span></span>

<span data-ttu-id="f1c5b-150">W poniższej przykładowej odpowiedzi widać, że liczba elementów wiersza z identyfikatorem oferty **`DG7GMGF0FKZV:0003:DG7GMGF0DWMS`** stała się zerem (0).</span><span class="sxs-lookup"><span data-stu-id="f1c5b-150">In the following example response, you can see that the quantity of line item with the offer identifier **`DG7GMGF0FKZV:0003:DG7GMGF0DWMS`** has become zero (0).</span></span> <span data-ttu-id="f1c5b-151">Ta zmiana oznacza, że element wiersza, który został oznaczony do anulowania, został pomyślnie anulowany.</span><span class="sxs-lookup"><span data-stu-id="f1c5b-151">This change means that the line item that was marked for cancellation has been canceled successfully.</span></span> <span data-ttu-id="f1c5b-152">Przykładowe zamówienie zawiera inne pozycje, które nie zostały anulowane, co oznacza, że stan całego zamówienia zostanie oznaczony jako **ukończone,** a nie anulowany .</span><span class="sxs-lookup"><span data-stu-id="f1c5b-152">The example order contains other line items that weren't canceled, which means that the status of the overall order will be marked as **completed**, not **cancelled**.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    "alternateId": "c403d91b21d2",
    "referenceCustomerId": "45411344-b09d-47e7-9653-542006bf9766",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS",
            "termDuration": "P3Y",
            "transactionType": "New",
            "friendlyName": "SQL Server Enterprise - 2 Core License Pack - 3 year",
            "quantity": 0,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0FKZV?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0FKZV/skus/0003?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0FKZV/skus/0003/availabilities/DG7GMGF0DWMS?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "lineItemNumber": 1,
            "offerId": "DG7GMGF0DVT7:000C:DG7GMGF0FVZM",
            "termDuration": "P3Y",
            "transactionType": "New",
            "friendlyName": "Windows Server CAL - 1 Device CAL - 3 year",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DVT7?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DVT7/skus/000C?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DVT7/skus/000C/availabilities/DG7GMGF0FVZM?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-12-12T17:33:56.1306495Z",
    "status": "completed",
    "transactionType": "UserPurchase",
    "links": {
        "self": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
            "method": "GET",
            "headers": []
        },
        "provisioningStatus": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "patchOperation": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
            "method": "PATCH",
            "headers": []
        }
    },
    "client": {
        "marketplaceCountry": "US",
        "deviceFamily": "UniversalStore-PartnerCenter",
        "name": "Partner Center API"
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
