---
title: Przypisywanie licencji do użytkownika
description: Dowiedz się, jak przypisywać licencje do użytkownika klienta za pośrednictwem interfejsów API Centrum partnerskiego, takich jak korzystanie z \# interfejsów API języka C lub Rest.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6eb0b953b9157e48074415bb3207e2946cfb2ab4
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768546"
---
# <a name="assign-licenses-to-a-user-via-partner-center-apis"></a><span data-ttu-id="25018-103">Przypisywanie licencji do użytkownika za pośrednictwem interfejsów API Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="25018-103">Assign licenses to a user via Partner Center APIs</span></span>

<span data-ttu-id="25018-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="25018-104">**Applies to:**</span></span>

- <span data-ttu-id="25018-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="25018-105">Partner Center</span></span>

<span data-ttu-id="25018-106">Przypisywanie licencji do użytkownika klienta.</span><span class="sxs-lookup"><span data-stu-id="25018-106">How to assign licenses to a customer user.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25018-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="25018-107">Prerequisites</span></span>

- <span data-ttu-id="25018-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="25018-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="25018-109">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="25018-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="25018-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="25018-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="25018-111">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="25018-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="25018-112">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="25018-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="25018-113">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="25018-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="25018-114">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="25018-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="25018-115">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="25018-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="25018-116">Identyfikator użytkownika klienta.</span><span class="sxs-lookup"><span data-stu-id="25018-116">A customer user identifier.</span></span> <span data-ttu-id="25018-117">Ten identyfikator identyfikuje użytkownika, do którego ma zostać przypisana licencja.</span><span class="sxs-lookup"><span data-stu-id="25018-117">This ID identifies the user to whom to assign the license.</span></span>

- <span data-ttu-id="25018-118">Identyfikator jednostki SKU produktu identyfikujący produkt na potrzeby licencji.</span><span class="sxs-lookup"><span data-stu-id="25018-118">A product SKU identifier that identifies the product for the license.</span></span>

## <a name="assigning-licenses-through-code"></a><span data-ttu-id="25018-119">Przypisywanie licencji za poorednictwem kodu</span><span class="sxs-lookup"><span data-stu-id="25018-119">Assigning licenses through code</span></span>

<span data-ttu-id="25018-120">W przypadku przypisywania licencji do użytkownika należy wybrać z kolekcji subskrybowanych jednostek SKU klienta.</span><span class="sxs-lookup"><span data-stu-id="25018-120">When you assign licenses to a user, you must choose from the customer's collection of subscribed SKUs.</span></span> <span data-ttu-id="25018-121">Następnie po zidentyfikowaniu produktów, które chcesz przypisać, należy uzyskać identyfikator jednostki SKU produktu dla każdego produktu w celu przypisania.</span><span class="sxs-lookup"><span data-stu-id="25018-121">Then, having identified the products that you want to assign, you must obtain the product SKU ID for each product in order to make the assignments.</span></span> <span data-ttu-id="25018-122">Każde wystąpienie [**SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) zawiera właściwość [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) , z której można odwołać się do obiektu [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) i uzyskać [**Identyfikator**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).</span><span class="sxs-lookup"><span data-stu-id="25018-122">Each [**SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) instance contains a [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) property from which you can reference the [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) object and get the [**ID**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).</span></span>

<span data-ttu-id="25018-123">Żądanie przypisania licencji musi zawierać licencje z pojedynczej grupy licencji.</span><span class="sxs-lookup"><span data-stu-id="25018-123">A license assignment request must contain licenses from a single license group.</span></span> <span data-ttu-id="25018-124">Na przykład nie można przypisać licencji z [**grupa1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) i **group2** w tym samym żądaniu.</span><span class="sxs-lookup"><span data-stu-id="25018-124">For example, you cannot assign licenses from [**Group1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) and **Group2** in the same request.</span></span> <span data-ttu-id="25018-125">Próba przypisania licencji z więcej niż jednej grupy w pojedynczym żądaniu zakończy się niepowodzeniem z powodu odpowiedniego błędu.</span><span class="sxs-lookup"><span data-stu-id="25018-125">An attempt to assign licenses from more than one group in a single request will fail with an appropriate error.</span></span> <span data-ttu-id="25018-126">Aby dowiedzieć się, jakie licencje są dostępne dla grupy licencji, zobacz sekcję [Pobieranie listy dostępnych licencji według grupy licencji](get-a-list-of-available-licenses-by-license-group.md).</span><span class="sxs-lookup"><span data-stu-id="25018-126">To find out what licenses are available by license group, see [Get a list of available licenses by license group](get-a-list-of-available-licenses-by-license-group.md).</span></span>

<span data-ttu-id="25018-127">Poniżej przedstawiono procedurę przypisywania licencji za pomocą kodu:</span><span class="sxs-lookup"><span data-stu-id="25018-127">Here are the steps to assign licenses through code:</span></span>

1. <span data-ttu-id="25018-128">Utwórz wystąpienie obiektu [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) .</span><span class="sxs-lookup"><span data-stu-id="25018-128">Instantiate a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) object.</span></span> <span data-ttu-id="25018-129">Ten obiekt służy do określania jednostki SKU produktu i planów usług do przypisania.</span><span class="sxs-lookup"><span data-stu-id="25018-129">You use this object to specify the product SKU and service plans to assign.</span></span>

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. <span data-ttu-id="25018-130">Wypełnij właściwości obiektu, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="25018-130">Populate the object properties as shown below.</span></span> <span data-ttu-id="25018-131">Ten kod zakłada, że masz już identyfikator SKU produktu i że wszystkie dostępne plany usług zostaną przypisane (oznacza to, że żaden z nich nie zostanie wykluczony).</span><span class="sxs-lookup"><span data-stu-id="25018-131">This code assumes that you already have the product SKU ID, and that all of the available service plans will be assigned (that is, none will be excluded).</span></span>

    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. <span data-ttu-id="25018-132">Jeśli nie masz identyfikatora SKU produktu, musisz pobrać kolekcję subskrybowanych jednostek SKU i uzyskać identyfikator SKU produktu z jednego z nich.</span><span class="sxs-lookup"><span data-stu-id="25018-132">If you don't have the product SKU ID, you need to retrieve the collection of subscribed SKUs and get the product SKU ID from one of them.</span></span> <span data-ttu-id="25018-133">Oto przykład, jeśli znasz nazwę jednostki SKU produktu.</span><span class="sxs-lookup"><span data-stu-id="25018-133">Here is an example if you know the product SKU name.</span></span>

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. <span data-ttu-id="25018-134">Następnie Utwórz wystąpienie nowej listy typu [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)i Dodaj obiekt License.</span><span class="sxs-lookup"><span data-stu-id="25018-134">Next, instantiate a new list of type [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment), and add the license object.</span></span> <span data-ttu-id="25018-135">Do listy można przypisać więcej niż jedną licencję.</span><span class="sxs-lookup"><span data-stu-id="25018-135">You can assign more than one license by adding each individually to the list.</span></span> <span data-ttu-id="25018-136">Licencje zawarte na tej liście muszą należeć do tej samej grupy licencji.</span><span class="sxs-lookup"><span data-stu-id="25018-136">The licenses included in this list must be from the same license group.</span></span>

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. <span data-ttu-id="25018-137">Utwórz wystąpienie [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) i przypisz listę przypisań licencji do właściwości [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) .</span><span class="sxs-lookup"><span data-stu-id="25018-137">Create a [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) instance and assign the list of license assignments to the [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) property.</span></span>

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. <span data-ttu-id="25018-138">Wywołaj metodę [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) lub [**onasync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) i przekaż obiekt aktualizacji licencji, jak pokazano poniżej, aby przypisać licencje.</span><span class="sxs-lookup"><span data-stu-id="25018-138">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) method and pass the license update object as shown below to assign the licenses.</span></span>

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a><span data-ttu-id="25018-139">C\#</span><span class="sxs-lookup"><span data-stu-id="25018-139">C\#</span></span>

<span data-ttu-id="25018-140">Aby przypisać licencję do użytkownika klienta, należy najpierw utworzyć wystąpienie obiektu [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) i wypełnić właściwości [**identyfikatora skuId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) i [**ExcludedPlans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) .</span><span class="sxs-lookup"><span data-stu-id="25018-140">To assign a license to a customer user, first instantiate a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) object, and populate the [**Skuid**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) and [**ExcludedPlans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) properties.</span></span> <span data-ttu-id="25018-141">Ten obiekt służy do określania jednostki SKU produktu do przypisania i planów usług, które mają zostać wykluczone.</span><span class="sxs-lookup"><span data-stu-id="25018-141">You use this object to specify the product SKU to assign and service plans to exclude.</span></span> <span data-ttu-id="25018-142">Następnie Utwórz wystąpienie nowej listy typu **LicenseAssignment** i Dodaj obiekt License do listy.</span><span class="sxs-lookup"><span data-stu-id="25018-142">Next, instantiate a new list of type **LicenseAssignment**, and add the license object to the list.</span></span> <span data-ttu-id="25018-143">Następnie Utwórz wystąpienie [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) i przypisz listę przypisań licencji do właściwości [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) .</span><span class="sxs-lookup"><span data-stu-id="25018-143">Then create a [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) instance and assign the list of license assignments to the [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) property.</span></span>

<span data-ttu-id="25018-144">Następnie użyj metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta i metodę [**users. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem użytkownika identyfikującym użytkownika.</span><span class="sxs-lookup"><span data-stu-id="25018-144">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="25018-145">Następnie uzyskaj interfejs do operacji aktualizacji licencji użytkownika klienta z właściwości [**LicenseUpdates**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) .</span><span class="sxs-lookup"><span data-stu-id="25018-145">Then get an interface to customer user license update operations from the [**LicenseUpdates**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) property.</span></span>

<span data-ttu-id="25018-146">Na koniec Wywołaj metodę [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) lub [**onasync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) i przekaż obiekt aktualizacji licencji, aby przypisać licencję.</span><span class="sxs-lookup"><span data-stu-id="25018-146">Finally, call the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) method and pass the license update object to assign the license.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerUserId;
// string selectedCustomerId;
// string selectedProductSkuId;

// Instantiate and populate a LicenseAssignment object.
LicenseAssignment license = new LicenseAssignment();
license.SkuId = selectedProductSkuId;
license.ExcludedPlans = null;

// Instantiate a list of licenses to assign and add the license to it.
List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
licenseList.Add(license);

// Instantiate a LicenseUpdate object and add the list of licenses to assign.
LicenseUpdate updateLicense = new LicenseUpdate();
updateLicense.LicensesToAssign = licenseList;

// Update the user licenses.
var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
```

<span data-ttu-id="25018-147">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="25018-147">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="25018-148">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: CustomerUserAssignLicenses.cs</span><span class="sxs-lookup"><span data-stu-id="25018-148">**Project**: Partner Center SDK Samples **Class**: CustomerUserAssignLicenses.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="25018-149">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="25018-149">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="25018-150">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="25018-150">Request syntax</span></span>

| <span data-ttu-id="25018-151">Metoda</span><span class="sxs-lookup"><span data-stu-id="25018-151">Method</span></span>   | <span data-ttu-id="25018-152">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="25018-152">Request URI</span></span>                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="25018-153">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="25018-153">**POST**</span></span> | <span data-ttu-id="25018-154">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/users/{User-ID}/licenseupdates http/1.1</span><span class="sxs-lookup"><span data-stu-id="25018-154">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenseupdates HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="25018-155">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="25018-155">URI parameters</span></span>

<span data-ttu-id="25018-156">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="25018-156">Use the following path parameters to identify the customer and user.</span></span>

| <span data-ttu-id="25018-157">Nazwa</span><span class="sxs-lookup"><span data-stu-id="25018-157">Name</span></span>        | <span data-ttu-id="25018-158">Typ</span><span class="sxs-lookup"><span data-stu-id="25018-158">Type</span></span>   | <span data-ttu-id="25018-159">Wymagane</span><span class="sxs-lookup"><span data-stu-id="25018-159">Required</span></span> | <span data-ttu-id="25018-160">Opis</span><span class="sxs-lookup"><span data-stu-id="25018-160">Description</span></span>                                       |
|-------------|--------|----------|---------------------------------------------------|
| <span data-ttu-id="25018-161">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="25018-161">customer-id</span></span> | <span data-ttu-id="25018-162">ciąg</span><span class="sxs-lookup"><span data-stu-id="25018-162">string</span></span> | <span data-ttu-id="25018-163">Tak</span><span class="sxs-lookup"><span data-stu-id="25018-163">Yes</span></span>      | <span data-ttu-id="25018-164">Identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="25018-164">A GUID formatted ID that identifies the customer.</span></span> |
| <span data-ttu-id="25018-165">user-id</span><span class="sxs-lookup"><span data-stu-id="25018-165">user-id</span></span>     | <span data-ttu-id="25018-166">ciąg</span><span class="sxs-lookup"><span data-stu-id="25018-166">string</span></span> | <span data-ttu-id="25018-167">Tak</span><span class="sxs-lookup"><span data-stu-id="25018-167">Yes</span></span>      | <span data-ttu-id="25018-168">Identyfikator GUID, który identyfikuje użytkownika.</span><span class="sxs-lookup"><span data-stu-id="25018-168">A GUID formatted ID that identifies the user.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="25018-169">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="25018-169">Request headers</span></span>

<span data-ttu-id="25018-170">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="25018-170">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="25018-171">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="25018-171">Request body</span></span>

<span data-ttu-id="25018-172">W treści żądania należy uwzględnić zasób [LicenseUpdate](license-resources.md#licenseupdate) , który określa licencje do przypisania.</span><span class="sxs-lookup"><span data-stu-id="25018-172">Include a [LicenseUpdate](license-resources.md#licenseupdate) resource in the request body that specifies the licenses to assign.</span></span>

### <a name="request-example"></a><span data-ttu-id="25018-173">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="25018-173">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/554526aa-cf5e-46fa-95df-98dbc55d8a1e/licenseupdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 183
Expect: 100-continue

{
    "LicensesToAssign": [{
            "ExcludedPlans": null,
            "SkuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "LicensesToRemove": null,
    "LicenseWarnings": null,
    "Attributes": {
        "ObjectType": "LicenseUpdate"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="25018-174">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="25018-174">REST response</span></span>

<span data-ttu-id="25018-175">Jeśli to się powiedzie, zwracany jest kod stanu odpowiedzi HTTP 201, a treść odpowiedzi zawiera zasób [LicenseUpdate](license-resources.md#licenseupdate) z informacjami o licencji.</span><span class="sxs-lookup"><span data-stu-id="25018-175">If successful, an HTTP response status code 201 is returned and the response body contains a [LicenseUpdate](license-resources.md#licenseupdate) resource with the license information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="25018-176">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="25018-176">Response success and error codes</span></span>

<span data-ttu-id="25018-177">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="25018-177">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="25018-178">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="25018-178">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="25018-179">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="25018-179">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="25018-180">Przykład odpowiedzi (powodzenie)</span><span class="sxs-lookup"><span data-stu-id="25018-180">Response example (success)</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 139
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CV: 5AnzcZQrvUqCq3kd.0
MS-ServerId: 030020525
Date: Thu, 20 Apr 2017 21:50:39 GMT

{
    "licensesToAssign": [{
            "skuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "licenseWarnings": [],
    "attributes": {
        "objectType": "LicenseUpdate"
    }
}
```

### <a name="response-example-license-isnt-available"></a><span data-ttu-id="25018-181">Przykład odpowiedzi (licencja jest niedostępna)</span><span class="sxs-lookup"><span data-stu-id="25018-181">Response example (license isn't available)</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 341
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: f4f3b748-8b22-4d07-a5a1-dceb32824192
MS-CV: 5npA0K22CUmWPOzB.0
MS-ServerId: 102030524
Date: Thu, 20 Apr 2017 22:12:36 GMT

{
    "code": 60012,
    "description": "We&#39;re sorry, it looks like you've run out of licenses. Buy more licenses, and then try again.",
    "data": ["LicenseQuotaExceededException : Subscription with Account 0c39d6d5-c70d-4c55-bc02-f620844f3fd1 and SKU f8a1db68-be16-40ed-86d5-cb42ce701560 does not have any available licenses left."],
    "source": "PartnerFD"
}
```
