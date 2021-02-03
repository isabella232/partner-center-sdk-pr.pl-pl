---
title: Pobieranie kolekcji uprawnień
description: Jak uzyskać kolekcję uprawnień.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d2cc485429941dd2080bd285553333a01fc0ffd1
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768069"
---
# <a name="get-a-collection-of-entitlements"></a><span data-ttu-id="acaff-103">Pobieranie kolekcji uprawnień</span><span class="sxs-lookup"><span data-stu-id="acaff-103">Get a collection of entitlements</span></span>

<span data-ttu-id="acaff-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="acaff-104">**Applies To**</span></span>

- <span data-ttu-id="acaff-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="acaff-105">Partner Center</span></span>

<span data-ttu-id="acaff-106">Jak uzyskać kolekcję uprawnień.</span><span class="sxs-lookup"><span data-stu-id="acaff-106">How to get a collection of entitlements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acaff-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="acaff-107">Prerequisites</span></span>

- <span data-ttu-id="acaff-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="acaff-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="acaff-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="acaff-109">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="acaff-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="acaff-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="acaff-111">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="acaff-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="acaff-112">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="acaff-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="acaff-113">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="acaff-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="acaff-114">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="acaff-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="acaff-115">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="acaff-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="acaff-116">C\#</span><span class="sxs-lookup"><span data-stu-id="acaff-116">C\#</span></span>

<span data-ttu-id="acaff-117">Aby uzyskać kolekcję uprawnień dla klienta, uzyskaj [**interfejs do operacji związanych z**](entitlement-resources.md#entitlement) operacjami, wywołując metodę  [**IAggregatePartner. Customers. ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="acaff-117">To get an entitlements collection for a customer, obtain an interface to [**Entitlement**](entitlement-resources.md#entitlement) operations by calling the  [**IAggregatePartner.Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="acaff-118">Następnie Pobierz interfejs z właściwości **uprawnienia** i Wywołaj metodę **Get ()** lub **GetAsync ()** w celu pobrania kolekcji uprawnień.</span><span class="sxs-lookup"><span data-stu-id="acaff-118">Then, retrieve the interface from the **Entitlements** property and call the **Get()** or **GetAsync()** method to retrieve the collection of entitlements.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;

// Get the collection of entitlements.
var entitlements = partnerOperations.Customers.ById(customerId).Entitlements.Get();
```

<span data-ttu-id="acaff-119">Aby wypełnić daty wygaśnięcia uprawnień do pobrania, wywołaj te same metody, a następnie ustaw opcjonalny parametr logiczny **showExpiry** na true **Get (true)** lub **GetAsync (true)**.</span><span class="sxs-lookup"><span data-stu-id="acaff-119">To populate expiry dates for the entitlements to be retrieved, call the same methods above and set the optional boolean parameter **showExpiry** to true **Get(true)** or **GetAsync(true)**.</span></span> <span data-ttu-id="acaff-120">Wskazuje to, że daty wygaśnięcia uprawnień są wymagane (jeśli ma to zastosowanie).</span><span class="sxs-lookup"><span data-stu-id="acaff-120">This indicates that entitlement expiry dates are required (when applicable).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="acaff-121">Typy uprawnień lokalnych nie mają dat wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="acaff-121">On-premise entitlement types do not have expiry dates.</span></span>

## <a name="rest-request"></a><span data-ttu-id="acaff-122">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="acaff-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="acaff-123">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="acaff-123">Request syntax</span></span>

| <span data-ttu-id="acaff-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="acaff-124">Method</span></span> | <span data-ttu-id="acaff-125">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="acaff-125">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="acaff-126">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="acaff-126">**GET**</span></span> | <span data-ttu-id="acaff-127">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{customerId}/entitlements http/1.1</span><span class="sxs-lookup"><span data-stu-id="acaff-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/entitlements HTTP/1.1</span></span>                            |

### <a name="uri-parameters"></a><span data-ttu-id="acaff-128">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="acaff-128">URI parameters</span></span>

<span data-ttu-id="acaff-129">Podczas tworzenia żądania Użyj następującej ścieżki i parametrów zapytania.</span><span class="sxs-lookup"><span data-stu-id="acaff-129">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="acaff-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="acaff-130">Name</span></span> | <span data-ttu-id="acaff-131">Typ</span><span class="sxs-lookup"><span data-stu-id="acaff-131">Type</span></span> | <span data-ttu-id="acaff-132">Wymagane</span><span class="sxs-lookup"><span data-stu-id="acaff-132">Required</span></span> | <span data-ttu-id="acaff-133">Opis</span><span class="sxs-lookup"><span data-stu-id="acaff-133">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="acaff-134">customerId</span><span class="sxs-lookup"><span data-stu-id="acaff-134">customerId</span></span> | <span data-ttu-id="acaff-135">ciąg</span><span class="sxs-lookup"><span data-stu-id="acaff-135">string</span></span> | <span data-ttu-id="acaff-136">Tak</span><span class="sxs-lookup"><span data-stu-id="acaff-136">Yes</span></span> | <span data-ttu-id="acaff-137">Identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="acaff-137">A GUID formatted customerId that identifies the customer.</span></span> |
| <span data-ttu-id="acaff-138">uprawnienietype</span><span class="sxs-lookup"><span data-stu-id="acaff-138">entitlementType</span></span> | <span data-ttu-id="acaff-139">ciąg</span><span class="sxs-lookup"><span data-stu-id="acaff-139">string</span></span> | <span data-ttu-id="acaff-140">Nie</span><span class="sxs-lookup"><span data-stu-id="acaff-140">No</span></span> | <span data-ttu-id="acaff-141">Można go użyć do określenia typu uprawnień do pobrania (**oprogramowanie** lub **reservedInstance** ).</span><span class="sxs-lookup"><span data-stu-id="acaff-141">Can be used to specify the type of entitlements to be retrieved (**software** or **reservedInstance** ).</span></span> <span data-ttu-id="acaff-142">Jeśli nie zostanie ustawiona, zostaną pobrane wszystkie typy</span><span class="sxs-lookup"><span data-stu-id="acaff-142">If not set, all types will be retrieved</span></span> |
| <span data-ttu-id="acaff-143">showExpiry</span><span class="sxs-lookup"><span data-stu-id="acaff-143">showExpiry</span></span> | <span data-ttu-id="acaff-144">boolean</span><span class="sxs-lookup"><span data-stu-id="acaff-144">boolean</span></span> | <span data-ttu-id="acaff-145">Nie</span><span class="sxs-lookup"><span data-stu-id="acaff-145">No</span></span> | <span data-ttu-id="acaff-146">Opcjonalna Flaga wskazująca, czy daty wygaśnięcia uprawnień są wymagane.</span><span class="sxs-lookup"><span data-stu-id="acaff-146">Optional flag which indicates if entitlements expiry dates are required.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="acaff-147">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="acaff-147">Request headers</span></span>

<span data-ttu-id="acaff-148">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="acaff-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="acaff-149">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="acaff-149">Request body</span></span>

<span data-ttu-id="acaff-150">Brak.</span><span class="sxs-lookup"><span data-stu-id="acaff-150">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="acaff-151">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="acaff-151">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/entitlements HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="acaff-152">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="acaff-152">REST response</span></span>

<span data-ttu-id="acaff-153">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [uprawnień](entitlement-resources.md#entitlement) .</span><span class="sxs-lookup"><span data-stu-id="acaff-153">If successful, the response body contains a collection of [Entitlement](entitlement-resources.md#entitlement) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="acaff-154">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="acaff-154">Response success and error codes</span></span>

<span data-ttu-id="acaff-155">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="acaff-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="acaff-156">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="acaff-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="acaff-157">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="acaff-157">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="acaff-158">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="acaff-158">Response example</span></span>

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

## <a name="additional-examples"></a><span data-ttu-id="acaff-159">Dodatkowe przykłady</span><span class="sxs-lookup"><span data-stu-id="acaff-159">Additional Examples</span></span>

<span data-ttu-id="acaff-160">Poniższy przykład pokazuje, jak pobrać określony typ uprawnień wraz z datami wygaśnięcia (jeśli ma to zastosowanie)</span><span class="sxs-lookup"><span data-stu-id="acaff-160">The following example shows you how to retrieve a specific type of entitlements along with expiry dates (when applicable)</span></span>

### <a name="c-example"></a><span data-ttu-id="acaff-161">\#Przykład C</span><span class="sxs-lookup"><span data-stu-id="acaff-161">C\# example</span></span>

<span data-ttu-id="acaff-162">Aby uzyskać określony typ uprawnień, należy uzyskać Interfejs **ByEntitlementType** z interfejsu **uprawnień** i użyć metod **Get ()** lub **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="acaff-162">To retrieve a specific type of entitlements, obtain the **ByEntitlementType** interface from the **Entitlements** interface and use the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("software").Get(true);
```

### <a name="request-example"></a><span data-ttu-id="acaff-163">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="acaff-163">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/de3dcef9-9991-459c-ac71-2903d1127414/entitlements?entitlementtype=software&showExpiry=true
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: 6517a410-67ce-4995-9bb7-116a52179f92
MS-CorrelationId: d9eb8194-9b99-4057-a2fe-98bdf05f013c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="acaff-164">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="acaff-164">Response example</span></span>

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

<span data-ttu-id="acaff-165">W poniższych przykładach pokazano, jak pobrać informacje o produktach i rezerwacjach ze względu na uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="acaff-165">The following examples show you how to retrieve information about products and reservations from an entitlement.</span></span>

### <a name="retrieve-virtual-machine-reservation-details-from-an-entitlement-by-using-sdk-v18"></a><span data-ttu-id="acaff-166">Pobieranie szczegółów rezerwacji maszyn wirtualnych z uprawnień przy użyciu zestawu SDK V 1.8</span><span class="sxs-lookup"><span data-stu-id="acaff-166">Retrieve virtual machine reservation details from an entitlement by using SDK V1.8</span></span>

### <a name="c-example"></a><span data-ttu-id="acaff-167">\#Przykład C</span><span class="sxs-lookup"><span data-stu-id="acaff-167">C\# example</span></span>

<span data-ttu-id="acaff-168">Aby uzyskać więcej szczegółów dotyczących rezerwacji maszyn wirtualnych z uprawnienia, wywołaj identyfikator URI uwidoczniony w obszarze entitledArtifacts. link with artefakttype = virtual_machine_reserved_instance.</span><span class="sxs-lookup"><span data-stu-id="acaff-168">To retrieve more details related to the virtual machine reservations from an entitlement, invoke the URI exposed under entitledArtifacts.link with artifactType = virtual_machine_reserved_instance .</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("VirtualMachineReservedInstance").Get();

((VirtualMachineReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.VirtualMachineReservedInstance)).Link.InvokeAsync<VirtualMachineReservedInstanceArtifactDetails>(partnerOperations)
```

### <a name="request-example"></a><span data-ttu-id="acaff-169">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="acaff-169">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/virtualmachinereservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="acaff-170">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="acaff-170">Response example</span></span>

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

### <a name="retrieve-reservation-details-from-an-entitlement-by-using-sdk-v19"></a><span data-ttu-id="acaff-171">Pobieranie szczegółów rezerwacji z uprawnień przy użyciu zestawu SDK V 1.9</span><span class="sxs-lookup"><span data-stu-id="acaff-171">Retrieve reservation details from an entitlement by using SDK V1.9</span></span>

### <a name="c-example"></a><span data-ttu-id="acaff-172">\#Przykład C</span><span class="sxs-lookup"><span data-stu-id="acaff-172">C\# example</span></span>

<span data-ttu-id="acaff-173">Aby uzyskać więcej szczegółów dotyczących rezerwacji z uprawnienia do wystąpienia zarezerwowanego, wywołaj identyfikator URI uwidoczniony w obszarze ```entitledArtifacts.link``` with ```artifactType = reservedinstance``` .</span><span class="sxs-lookup"><span data-stu-id="acaff-173">To retrieve more details related to the reservations from a reserved instance entitlement, invoke the URI exposed under ```entitledArtifacts.link``` with ```artifactType = reservedinstance```.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("ReservedInstance").Get();

((ReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.ReservedInstance)).Link.InvokeAsync<ReservedInstanceArtifactDetails>(partnerOperations);
```

### <a name="request-example"></a><span data-ttu-id="acaff-174">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="acaff-174">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/reservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="acaff-175">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="acaff-175">Response example</span></span>

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

### <a name="api-consumers"></a><span data-ttu-id="acaff-176">Konsumenci interfejsu API</span><span class="sxs-lookup"><span data-stu-id="acaff-176">API Consumers</span></span>

<span data-ttu-id="acaff-177">Partnerzy korzystający z interfejsu API do wykonywania zapytań dotyczących wystąpień zarezerwowanych maszyn wirtualnych — zaktualizuj identyfikator URI żądania z **/Customers/{customerId}/entitlements na/Customers/{customerId}/entitlements? wartość = virtualmachinereservedinstance** , aby zachować zgodność z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="acaff-177">Partners who are using the API to query virtual machine reserved instance entitlements - Update the request URI from **/customers/{customerId}/entitlements to /customers/{customerId}/entitlements?entitlementType=virtualmachinereservedinstance** to maintain backward compatibility.</span></span> <span data-ttu-id="acaff-178">Aby można było korzystać z maszyny wirtualnej lub usługi Azure SQL z rozszerzonym kontraktem, zaktualizuj identyfikator URI żądania do **/Customers/{customerId}/entitlements? reservedinstance**.</span><span class="sxs-lookup"><span data-stu-id="acaff-178">In order to consume virtual machine or Azure SQL with enhanced contract, update the request URI to **/customers/{customerId}/entitlements?entitlementType=reservedinstance**.</span></span>
