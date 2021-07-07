---
title: Pobieranie kolekcji uprawnień
description: Jak uzyskać kolekcję uprawnień.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7bb8d3aefb11fae0af4bce790b41598d935de57c
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906415"
---
# <a name="get-a-collection-of-entitlements"></a><span data-ttu-id="f11e3-103">Pobieranie kolekcji uprawnień</span><span class="sxs-lookup"><span data-stu-id="f11e3-103">Get a collection of entitlements</span></span>

<span data-ttu-id="f11e3-104">Jak uzyskać kolekcję uprawnień.</span><span class="sxs-lookup"><span data-stu-id="f11e3-104">How to get a collection of entitlements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f11e3-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f11e3-105">Prerequisites</span></span>

- <span data-ttu-id="f11e3-106">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f11e3-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f11e3-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f11e3-107">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="f11e3-108">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f11e3-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f11e3-109">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="f11e3-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f11e3-110">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="f11e3-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f11e3-111">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="f11e3-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f11e3-112">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="f11e3-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f11e3-113">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f11e3-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="f11e3-114">C\#</span><span class="sxs-lookup"><span data-stu-id="f11e3-114">C\#</span></span>

<span data-ttu-id="f11e3-115">Aby uzyskać kolekcję uprawnień dla klienta, uzyskaj interfejs operacji [**uprawnień,**](entitlement-resources.md#entitlement) wywołując metodę  [**IAggregatePartner.Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta.</span><span class="sxs-lookup"><span data-stu-id="f11e3-115">To get an entitlements collection for a customer, obtain an interface to [**Entitlement**](entitlement-resources.md#entitlement) operations by calling the  [**IAggregatePartner.Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="f11e3-116">Następnie pobierz interfejs z właściwości **Entitlements** i wywołaj metodę **Get()** lub **GetAsync(),** aby pobrać kolekcję uprawnień.</span><span class="sxs-lookup"><span data-stu-id="f11e3-116">Then, retrieve the interface from the **Entitlements** property and call the **Get()** or **GetAsync()** method to retrieve the collection of entitlements.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;

// Get the collection of entitlements.
var entitlements = partnerOperations.Customers.ById(customerId).Entitlements.Get();
```

<span data-ttu-id="f11e3-117">Aby wypełnić daty wygaśnięcia dla uprawnień do pobrania, wywołaj te same metody powyżej i ustaw opcjonalny parametr **logiczny showExpiry** na wartość true **Get(true)** lub **GetAsync(true)**.</span><span class="sxs-lookup"><span data-stu-id="f11e3-117">To populate expiry dates for the entitlements to be retrieved, call the same methods above and set the optional boolean parameter **showExpiry** to true **Get(true)** or **GetAsync(true)**.</span></span> <span data-ttu-id="f11e3-118">Oznacza to, że daty wygaśnięcia uprawnień są wymagane (jeśli mają zastosowanie).</span><span class="sxs-lookup"><span data-stu-id="f11e3-118">This indicates that entitlement expiry dates are required (when applicable).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f11e3-119">Lokalne typy uprawnień nie mają dat wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="f11e3-119">On-premise entitlement types do not have expiry dates.</span></span>

## <a name="rest-request"></a><span data-ttu-id="f11e3-120">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="f11e3-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f11e3-121">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="f11e3-121">Request syntax</span></span>

| <span data-ttu-id="f11e3-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="f11e3-122">Method</span></span> | <span data-ttu-id="f11e3-123">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="f11e3-123">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="f11e3-124">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="f11e3-124">**GET**</span></span> | <span data-ttu-id="f11e3-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/entitlements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f11e3-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/entitlements HTTP/1.1</span></span>                            |

### <a name="uri-parameters"></a><span data-ttu-id="f11e3-126">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="f11e3-126">URI parameters</span></span>

<span data-ttu-id="f11e3-127">Podczas tworzenia żądania użyj następującej ścieżki i parametrów zapytania.</span><span class="sxs-lookup"><span data-stu-id="f11e3-127">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="f11e3-128">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f11e3-128">Name</span></span> | <span data-ttu-id="f11e3-129">Typ</span><span class="sxs-lookup"><span data-stu-id="f11e3-129">Type</span></span> | <span data-ttu-id="f11e3-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f11e3-130">Required</span></span> | <span data-ttu-id="f11e3-131">Opis</span><span class="sxs-lookup"><span data-stu-id="f11e3-131">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="f11e3-132">customerId</span><span class="sxs-lookup"><span data-stu-id="f11e3-132">customerId</span></span> | <span data-ttu-id="f11e3-133">ciąg</span><span class="sxs-lookup"><span data-stu-id="f11e3-133">string</span></span> | <span data-ttu-id="f11e3-134">Tak</span><span class="sxs-lookup"><span data-stu-id="f11e3-134">Yes</span></span> | <span data-ttu-id="f11e3-135">Identyfikator GUID sformatowany jako customerId, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="f11e3-135">A GUID formatted customerId that identifies the customer.</span></span> |
| <span data-ttu-id="f11e3-136">typ uprawnień</span><span class="sxs-lookup"><span data-stu-id="f11e3-136">entitlementType</span></span> | <span data-ttu-id="f11e3-137">ciąg</span><span class="sxs-lookup"><span data-stu-id="f11e3-137">string</span></span> | <span data-ttu-id="f11e3-138">Nie</span><span class="sxs-lookup"><span data-stu-id="f11e3-138">No</span></span> | <span data-ttu-id="f11e3-139">Może służyć do określania typu uprawnień do pobrania **(oprogramowanie** lub **reservedInstance).**</span><span class="sxs-lookup"><span data-stu-id="f11e3-139">Can be used to specify the type of entitlements to be retrieved (**software** or **reservedInstance** ).</span></span> <span data-ttu-id="f11e3-140">Jeśli nie zostanie ustawiona, zostaną pobrane wszystkie typy</span><span class="sxs-lookup"><span data-stu-id="f11e3-140">If not set, all types will be retrieved</span></span> |
| <span data-ttu-id="f11e3-141">showExpiry</span><span class="sxs-lookup"><span data-stu-id="f11e3-141">showExpiry</span></span> | <span data-ttu-id="f11e3-142">boolean</span><span class="sxs-lookup"><span data-stu-id="f11e3-142">boolean</span></span> | <span data-ttu-id="f11e3-143">Nie</span><span class="sxs-lookup"><span data-stu-id="f11e3-143">No</span></span> | <span data-ttu-id="f11e3-144">Opcjonalna flaga wskazująca, czy daty wygaśnięcia uprawnień są wymagane.</span><span class="sxs-lookup"><span data-stu-id="f11e3-144">Optional flag that indicates if entitlements expiry dates are required.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f11e3-145">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="f11e3-145">Request headers</span></span>

<span data-ttu-id="f11e3-146">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f11e3-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f11e3-147">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="f11e3-147">Request body</span></span>

<span data-ttu-id="f11e3-148">Brak.</span><span class="sxs-lookup"><span data-stu-id="f11e3-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f11e3-149">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="f11e3-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/entitlements HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="f11e3-150">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="f11e3-150">REST response</span></span>

<span data-ttu-id="f11e3-151">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję [zasobów uprawnień.](entitlement-resources.md#entitlement)</span><span class="sxs-lookup"><span data-stu-id="f11e3-151">If successful, the response body contains a collection of [Entitlement](entitlement-resources.md#entitlement) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f11e3-152">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f11e3-152">Response success and error codes</span></span>

<span data-ttu-id="f11e3-153">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="f11e3-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f11e3-154">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="f11e3-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f11e3-155">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f11e3-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f11e3-156">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f11e3-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 103778
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: EjFdw8fCpkKyMyza.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:42:51 GMT

{
  "totalCount": 2,
  "items": [
    {
      "includedEntitlements": [],
      "referenceOrder": {
        "id": "KaJ8XvkKc_GoNZOUyjVaRJalTBN5MWdV1",
        "lineItemId": "0"
      },
      "productId": "DZH318Z0BQ3W",
      "quantity": 1,
      "entitledArtifacts": [
        {
          "link": {
            "uri": "/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/reservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336",
            "method": "GET",
            "headers": []
          },
          "resourceId": "ebf2e74b-630e-4a09-857d-a1f6c6351336",
          "artifactType": "reservedinstance"
        }
      ],
      "skuId": "007J",
      "entitlementType": "reservedinstance"
      "dynamicAttributes": {
               "reservationType": "virtualmachines"
        }
    },
    {
      "includedEntitlements": [
        {
          "includedEntitlements": [],
          "referenceOrder": {
              "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
              "lineItemId": "0"
          },
          "productId": "DG7GMGF0DWTJ",
          "quantity": 1,
          "entitledArtifacts": [],
          "skuId": "0001",
          "entitlementType": "software"
        },
        {
          "includedEntitlements": [],
          "referenceOrder": {
            "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
            "lineItemId": "0"
          },
            "productId": "DG7GMGF0DWLG",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0002",
            "entitlementType": "software"
          }
        ],
        "referenceOrder": {
          "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
          "lineItemId": "0"
        },
        "productId": "DG7GMGF0DWTK",
        "quantity": 1,
        "entitledArtifacts": [],
        "skuId": "0002",
        "entitlementType": "software"
    }
  ],
  "attributes": {
    "objectType": "Collection"
  }
}
```

## <a name="additional-examples"></a><span data-ttu-id="f11e3-157">Dodatkowe przykłady</span><span class="sxs-lookup"><span data-stu-id="f11e3-157">Additional Examples</span></span>

<span data-ttu-id="f11e3-158">W poniższym przykładzie pokazano, jak pobrać określony typ uprawnień wraz z datami wygaśnięcia (jeśli ma to zastosowanie)</span><span class="sxs-lookup"><span data-stu-id="f11e3-158">The following example shows you how to retrieve a specific type of entitlements along with expiry dates (when applicable)</span></span>

### <a name="c-example"></a><span data-ttu-id="f11e3-159">Przykład w \# języku C</span><span class="sxs-lookup"><span data-stu-id="f11e3-159">C\# example</span></span>

<span data-ttu-id="f11e3-160">Aby pobrać określony typ uprawnień, uzyskaj interfejs **ByEntitlementType** z **interfejsu Entitlements** i użyj metod **Get()** lub **GetAsync().**</span><span class="sxs-lookup"><span data-stu-id="f11e3-160">To retrieve a specific type of entitlements, obtain the **ByEntitlementType** interface from the **Entitlements** interface and use the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("software").Get(true);
```

### <a name="request-example"></a><span data-ttu-id="f11e3-161">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="f11e3-161">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/de3dcef9-9991-459c-ac71-2903d1127414/entitlements?entitlementtype=software&showExpiry=true
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: 6517a410-67ce-4995-9bb7-116a52179f92
MS-CorrelationId: d9eb8194-9b99-4057-a2fe-98bdf05f013c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="f11e3-162">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f11e3-162">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1791
Content-Type: application/json; charset=utf-8
MS-CorrelationId: d9eb8194-9b99-4057-a2fe-98bdf05f013c
MS-RequestId: 6517a410-67ce-4995-9bb7-116a52179f92
X-Locale: en-US
MS-CV: yD+4LBKePUSp/vqJ.0
MS-ServerId: 000002
Date: Mon, 28 Jan 2019 18:31:43 GMT

{
    "totalCount": 2,
    "items": [
        {
            "includedEntitlements": [
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "0",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWM2",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0001",
                    "entitlementType": "software"
                },
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "0",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWMK",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0001",
                    "entitlementType": "software"
                }
            ],
            "referenceOrder": {
                "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                "lineItemId": "0",
                "alternateId": "8f3af3dea1ea"
            },
            "productId": "DG7GMGF0DWM3",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0002",
            "entitlementType": "software"
        },
        {
            "includedEntitlements": [
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "1",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWV1",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0002",
                    "entitlementType": "software"
                },
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "1",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWV2",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0002",
                    "entitlementType": "software"
                }
            ],
            "referenceOrder": {
                "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                "lineItemId": "1",
                "alternateId": "8f3af3dea1ea"
            },
            "productId": "DG7GMGF0DWBQ",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0003",
            "entitlementType": "software",
            "expiryDate": "2022-01-28T00:00:00Z"
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

<span data-ttu-id="f11e3-163">Poniższe przykłady pokazują, jak pobrać informacje o produktach i rezerwacjach z uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="f11e3-163">The following examples show you how to retrieve information about products and reservations from an entitlement.</span></span>

### <a name="retrieve-virtual-machine-reservation-details-from-an-entitlement-by-using-sdk-v18"></a><span data-ttu-id="f11e3-164">Pobieranie szczegółów rezerwacji maszyny wirtualnej z uprawnienia przy użyciu zestawu SDK w wersji 1.8</span><span class="sxs-lookup"><span data-stu-id="f11e3-164">Retrieve virtual machine reservation details from an entitlement by using SDK V1.8</span></span>

### <a name="c-example"></a><span data-ttu-id="f11e3-165">Przykład w \# języku C</span><span class="sxs-lookup"><span data-stu-id="f11e3-165">C\# example</span></span>

<span data-ttu-id="f11e3-166">Aby pobrać więcej szczegółów związanych z rezerwacjami maszyny wirtualnej z uprawnienia, wywołaj wartość URI ujawnioną w obszarze entitledArtifacts.link z wartością artifactType = virtual_machine_reserved_instance.</span><span class="sxs-lookup"><span data-stu-id="f11e3-166">To retrieve more details related to the virtual machine reservations from an entitlement, invoke the URI exposed under entitledArtifacts.link with artifactType = virtual_machine_reserved_instance.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("VirtualMachineReservedInstance").Get();

((VirtualMachineReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.VirtualMachineReservedInstance)).Link.InvokeAsync<VirtualMachineReservedInstanceArtifactDetails>(partnerOperations)
```

### <a name="request-example"></a><span data-ttu-id="f11e3-167">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="f11e3-167">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/virtualmachinereservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="f11e3-168">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f11e3-168">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 368
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: yrdTGsZ7IU2v9okv.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:45:14 GMT

{
  "type": "virtual_machine_reserved_instance",
  "virtualMachineReservations": [
    {
      "reservationId": "99f320db-c029-4c1b-a157-dad76e4481b6",
      "scopeType": "Shared",
      "quantity": 1,
      "expiryDateTime": "2019-02-23T00:00:00",
      "effectiveDateTime": "2018-02-23T18:15:24.6724884Z",
      "provisioningState": "Created"
    }
  ]
}
```

### <a name="retrieve-reservation-details-from-an-entitlement-by-using-sdk-v19"></a><span data-ttu-id="f11e3-169">Pobieranie szczegółów rezerwacji z uprawnienia przy użyciu zestawu SDK w wersji 1.9</span><span class="sxs-lookup"><span data-stu-id="f11e3-169">Retrieve reservation details from an entitlement by using SDK V1.9</span></span>

### <a name="c-example"></a><span data-ttu-id="f11e3-170">Przykład w \# języku C</span><span class="sxs-lookup"><span data-stu-id="f11e3-170">C\# example</span></span>

<span data-ttu-id="f11e3-171">Aby pobrać więcej szczegółów związanych z rezerwacjami z uprawnienia wystąpienia zarezerwowanego, wywołaj URI ujawniony w ```entitledArtifacts.link``` obszarze za pomocą . ```artifactType = reservedinstance```</span><span class="sxs-lookup"><span data-stu-id="f11e3-171">To retrieve more details related to the reservations from a reserved instance entitlement, invoke the URI exposed under ```entitledArtifacts.link``` with ```artifactType = reservedinstance```.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("ReservedInstance").Get();

((ReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.ReservedInstance)).Link.InvokeAsync<ReservedInstanceArtifactDetails>(partnerOperations);
```

### <a name="request-example"></a><span data-ttu-id="f11e3-172">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="f11e3-172">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/reservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="f11e3-173">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f11e3-173">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 368
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: yrdTGsZ7IU2v9okv.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:45:14 GMT

{
  "type": "reservedinstance",
  "virtualMachineReservations": [
    {
      "reservationId": "99f320db-c029-4c1b-a157-dad76e4481b6",
      "scopeType": "Shared",
      "quantity": 1,
      "expiryDateTime": "2019-02-23T00:00:00",
      "effectiveDateTime": "2018-02-23T18:15:24.6724884Z",
      "provisioningState": "Created"
    }
  ]
}
```

### <a name="api-consumers"></a><span data-ttu-id="f11e3-174">Konsumenci interfejsu API</span><span class="sxs-lookup"><span data-stu-id="f11e3-174">API Consumers</span></span>

<span data-ttu-id="f11e3-175">Partnerzy używający interfejsu API do wykonywania zapytań dotyczących uprawnień wystąpienia zarezerwowanego maszyny wirtualnej — zaktualizuj identyfikator URI żądania z elementu **/customers/{customerId}/entitlements do elementu /customers/{customerId}/entitlements?entitlementType=virtualmachinereservedinstance,** aby zachować zgodność z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="f11e3-175">Partners who are using the API to query virtual machine reserved instance entitlements - Update the request URI from **/customers/{customerId}/entitlements to /customers/{customerId}/entitlements?entitlementType=virtualmachinereservedinstance** to maintain backward compatibility.</span></span> <span data-ttu-id="f11e3-176">Aby korzystać z maszyny wirtualnej lub usługi Azure SQL z rozszerzonym kontraktem, zaktualizuj identyfikator URI żądania do **wartości /customers/{customerId}/entitlements?entitlementType=reservedinstance.**</span><span class="sxs-lookup"><span data-stu-id="f11e3-176">To consume virtual machine or Azure SQL with enhanced contract, update the request URI to **/customers/{customerId}/entitlements?entitlementType=reservedinstance**.</span></span>
