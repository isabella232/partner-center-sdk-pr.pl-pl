---
title: Anulowanie zakupów oprogramowania
description: Opcja samoobsługowego anulowania subskrypcji oprogramowania i zakupów bezterminowego w ramach interfejsów API Centrum partnerskiego.
ms.date: 12/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 25fd10a171fa6ca01f3442d49145443f2382cc18
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768093"
---
# <a name="cancel-software-purchases"></a><span data-ttu-id="15662-103">Anulowanie zakupów oprogramowania</span><span class="sxs-lookup"><span data-stu-id="15662-103">Cancel software purchases</span></span>

<span data-ttu-id="15662-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="15662-104">**Applies to:**</span></span>

- <span data-ttu-id="15662-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="15662-105">Partner Center</span></span>

<span data-ttu-id="15662-106">Możesz użyć interfejsów API Centrum partnerskiego, aby anulować subskrypcje oprogramowania i okresowe zakupy oprogramowania (o ile te zakupy zostały dokonane w oknie anulowania od daty zakupu).</span><span class="sxs-lookup"><span data-stu-id="15662-106">You can use the Partner Center APIs to cancel software subscriptions and perpetual software purchases (as long as those purchases were made within the cancellation window from the purchase date).</span></span> <span data-ttu-id="15662-107">Nie musisz tworzyć biletu pomocy technicznej w celu dokonania takich operacji, a zamiast nich można używać następujących metod samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="15662-107">You don't need to create a support ticket to make such cancellations, and can use the following self-service methods instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15662-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="15662-108">Prerequisites</span></span>

- <span data-ttu-id="15662-109">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="15662-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="15662-110">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="15662-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="15662-111">C\#</span><span class="sxs-lookup"><span data-stu-id="15662-111">C\#</span></span>

<span data-ttu-id="15662-112">Aby anulować kolejność oprogramowania,</span><span class="sxs-lookup"><span data-stu-id="15662-112">To cancel a software order,</span></span>

1. <span data-ttu-id="15662-113">Przekaż poświadczenia konta do metody [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) , aby uzyskać Interfejs [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) w celu pobrania operacji partnerskich.</span><span class="sxs-lookup"><span data-stu-id="15662-113">Pass your account credentials to the [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to get partner operations.</span></span>

2. <span data-ttu-id="15662-114">Wybierz określoną [kolejność](order-resources.md#order) , którą chcesz anulować.</span><span class="sxs-lookup"><span data-stu-id="15662-114">Select a particular [Order](order-resources.md#order) you wish to cancel.</span></span> <span data-ttu-id="15662-115">Wywołaj metodę [**Customers. ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, a następnie **Orders. ById ()** z identyfikatorem zamówienia.</span><span class="sxs-lookup"><span data-stu-id="15662-115">Call the [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier, followed by **Orders.ById()** with order identifier.</span></span>

3. <span data-ttu-id="15662-116">Wywołaj metodę **Get** lub **GetAsync** , aby pobrać zamówienie.</span><span class="sxs-lookup"><span data-stu-id="15662-116">Call the **Get** or **GetAsync** method to retrieve the order.</span></span>

4. <span data-ttu-id="15662-117">Ustaw właściwość [**Order. status**](order-resources.md#order) na wartość `cancelled` .</span><span class="sxs-lookup"><span data-stu-id="15662-117">Set the [**Order.Status**](order-resources.md#order) property to `cancelled`.</span></span>

5. <span data-ttu-id="15662-118">Obowiązkowe Jeśli chcesz określić niektóre elementy wiersza do anulowania, ustaw polecenie [**Order. LineItems**](order-resources.md#order) na listę elementów wiersza, które chcesz anulować.</span><span class="sxs-lookup"><span data-stu-id="15662-118">(Optional) If you want to specify certain line items for cancellation, set the [**Order.LineItems**](order-resources.md#order) to list of line items that you want to cancel.</span></span>

6. <span data-ttu-id="15662-119">Aby zaktualizować kolejność, użyj metody **patch ()** .</span><span class="sxs-lookup"><span data-stu-id="15662-119">Use the **Patch()** method to update the order.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="15662-120">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="15662-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="15662-121">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="15662-121">Request syntax</span></span>

| <span data-ttu-id="15662-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="15662-122">Method</span></span>     | <span data-ttu-id="15662-123">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="15662-123">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="15662-124">**WYSŁANA**</span><span class="sxs-lookup"><span data-stu-id="15662-124">**PATCH**</span></span> | <span data-ttu-id="15662-125">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="15662-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="15662-126">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="15662-126">URI parameters</span></span>

<span data-ttu-id="15662-127">Użyj następujących parametrów zapytania, aby usunąć klienta.</span><span class="sxs-lookup"><span data-stu-id="15662-127">Use the following query parameters to delete a customer.</span></span>

| <span data-ttu-id="15662-128">Nazwa</span><span class="sxs-lookup"><span data-stu-id="15662-128">Name</span></span>                   | <span data-ttu-id="15662-129">Typ</span><span class="sxs-lookup"><span data-stu-id="15662-129">Type</span></span>     | <span data-ttu-id="15662-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="15662-130">Required</span></span> | <span data-ttu-id="15662-131">Opis</span><span class="sxs-lookup"><span data-stu-id="15662-131">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="15662-132">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="15662-132">**customer-tenant-id**</span></span> | <span data-ttu-id="15662-133">**guid**</span><span class="sxs-lookup"><span data-stu-id="15662-133">**guid**</span></span> | <span data-ttu-id="15662-134">Y</span><span class="sxs-lookup"><span data-stu-id="15662-134">Y</span></span>        | <span data-ttu-id="15662-135">Wartość to identyfikator GUID w formacie identyfikatora dzierżawy klienta, który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="15662-135">The value is a GUID formatted customer tenant identifier that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="15662-136">**Identyfikator zamówienia**</span><span class="sxs-lookup"><span data-stu-id="15662-136">**order-id**</span></span> | <span data-ttu-id="15662-137">**parametry**</span><span class="sxs-lookup"><span data-stu-id="15662-137">**string**</span></span> | <span data-ttu-id="15662-138">Y</span><span class="sxs-lookup"><span data-stu-id="15662-138">Y</span></span>        | <span data-ttu-id="15662-139">Wartość jest ciągiem, który oznacza identyfikator zamówienia, który ma zostać anulowany.</span><span class="sxs-lookup"><span data-stu-id="15662-139">The value is a string that denotes the identifier of the order that you want to cancel.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="15662-140">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="15662-140">Request headers</span></span>

<span data-ttu-id="15662-141">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="15662-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="15662-142">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="15662-142">Request body</span></span>

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

### <a name="request-example"></a><span data-ttu-id="15662-143">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="15662-143">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="15662-144">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="15662-144">REST response</span></span>

<span data-ttu-id="15662-145">Jeśli to się powiedzie, metoda zwraca zamówienie z anulowanymi elementami wiersza.</span><span class="sxs-lookup"><span data-stu-id="15662-145">If successful, this method returns the order with canceled line items.</span></span>

<span data-ttu-id="15662-146">Stan zamówienia zostanie oznaczony jako **anulowany** , jeśli wszystkie elementy wiersza w zamówieniu zostaną anulowane lub **ukończone** , jeśli nie wszystkie elementy wiersza w zamówieniu zostaną anulowane.</span><span class="sxs-lookup"><span data-stu-id="15662-146">The order status will be marked as either **cancelled** if all the line items in the order are cancelled, or **completed** if not all line items in the order are canceled.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="15662-147">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="15662-147">Response success and error codes</span></span>

<span data-ttu-id="15662-148">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="15662-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="15662-149">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="15662-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="15662-150">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="15662-150">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="15662-151">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="15662-151">Response example</span></span>

<span data-ttu-id="15662-152">W poniższym przykładzie odpowiedzi można zobaczyć, że ilość elementu wiersza o identyfikatorze oferty **`DG7GMGF0FKZV:0003:DG7GMGF0DWMS`** stała się równa zero (0).</span><span class="sxs-lookup"><span data-stu-id="15662-152">In the following example response, you can see that the quantity of line item with the offer identifier **`DG7GMGF0FKZV:0003:DG7GMGF0DWMS`** has become zero (0).</span></span> <span data-ttu-id="15662-153">Ta zmiana oznacza, że element wiersza, który został oznaczony do anulowania został pomyślnie anulowany.</span><span class="sxs-lookup"><span data-stu-id="15662-153">This change means that the line item that was marked for cancellation has been canceled successfully.</span></span> <span data-ttu-id="15662-154">Przykładowa kolejność zawiera inne elementy wiersza, które nie zostały anulowane, co oznacza, że stan zamówienia ogólnego zostanie oznaczony jako **ukończone**, a nie **anulowane**.</span><span class="sxs-lookup"><span data-stu-id="15662-154">The example order contains other line items that weren't canceled, which means that the status of the overall order will be marked as **completed**, not **cancelled**.</span></span>

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
