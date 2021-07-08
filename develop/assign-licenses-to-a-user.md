---
title: Przypisywanie licencji do użytkownika
description: Dowiedz się, jak przypisywać licencje do użytkownika klienta za pośrednictwem Partner Center API, takich jak korzystanie z interfejsów \# API C lub REST.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 88ce0f185b0b043c4a7862b7f9808fb8805d40b9
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974373"
---
# <a name="assign-licenses-to-a-user-via-partner-center-apis"></a><span data-ttu-id="14c4b-103">Przypisywanie licencji do użytkownika za pośrednictwem Partner Center API</span><span class="sxs-lookup"><span data-stu-id="14c4b-103">Assign licenses to a user via Partner Center APIs</span></span>

<span data-ttu-id="14c4b-104">Jak przypisać licencje do użytkownika klienta.</span><span class="sxs-lookup"><span data-stu-id="14c4b-104">How to assign licenses to a customer user.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14c4b-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="14c4b-105">Prerequisites</span></span>

- <span data-ttu-id="14c4b-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="14c4b-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="14c4b-107">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="14c4b-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="14c4b-108">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="14c4b-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="14c4b-109">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="14c4b-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="14c4b-110">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="14c4b-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="14c4b-111">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="14c4b-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="14c4b-112">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="14c4b-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="14c4b-113">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="14c4b-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="14c4b-114">Identyfikator użytkownika klienta.</span><span class="sxs-lookup"><span data-stu-id="14c4b-114">A customer user identifier.</span></span> <span data-ttu-id="14c4b-115">Ten identyfikator identyfikuje użytkownika, do którego ma zostać przypisana licencja.</span><span class="sxs-lookup"><span data-stu-id="14c4b-115">This ID identifies the user to whom to assign the license.</span></span>

- <span data-ttu-id="14c4b-116">Identyfikator jednostki SKU produktu, który identyfikuje produkt licencji.</span><span class="sxs-lookup"><span data-stu-id="14c4b-116">A product SKU identifier that identifies the product for the license.</span></span>

## <a name="assigning-licenses-through-code"></a><span data-ttu-id="14c4b-117">Przypisywanie licencji za pomocą kodu</span><span class="sxs-lookup"><span data-stu-id="14c4b-117">Assigning licenses through code</span></span>

<span data-ttu-id="14c4b-118">Po przypisaniu licencji do użytkownika musisz wybrać jedną z kolekcji subskrybowanych jednostki SKU klienta.</span><span class="sxs-lookup"><span data-stu-id="14c4b-118">When you assign licenses to a user, you must choose from the customer's collection of subscribed SKUs.</span></span> <span data-ttu-id="14c4b-119">Następnie po zidentyfikowaniu produktów, które chcesz przypisać, musisz uzyskać identyfikator SKU produktu dla każdego produktu w celu wykonania przypisań.</span><span class="sxs-lookup"><span data-stu-id="14c4b-119">Then, having identified the products that you want to assign, you must obtain the product SKU ID for each product in order to make the assignments.</span></span> <span data-ttu-id="14c4b-120">Każde [**wystąpienie klasy SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) zawiera właściwość [**ProductSku,**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) z której można odwołać się do [**obiektu ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) i uzyskać [**identyfikator**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).</span><span class="sxs-lookup"><span data-stu-id="14c4b-120">Each [**SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) instance contains a [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) property from which you can reference the [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) object and get the [**ID**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).</span></span>

<span data-ttu-id="14c4b-121">Żądanie przypisania licencji musi zawierać licencje z jednej grupy licencji.</span><span class="sxs-lookup"><span data-stu-id="14c4b-121">A license assignment request must contain licenses from a single license group.</span></span> <span data-ttu-id="14c4b-122">Na przykład nie można przypisać licencji z grup [**Grupa1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) i **Grupa2** w tym samym żądaniu.</span><span class="sxs-lookup"><span data-stu-id="14c4b-122">For example, you cannot assign licenses from [**Group1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) and **Group2** in the same request.</span></span> <span data-ttu-id="14c4b-123">Próba przypisania licencji z więcej niż jednej grupy w jednym żądaniu nie powiedzie się z odpowiednim błędem.</span><span class="sxs-lookup"><span data-stu-id="14c4b-123">An attempt to assign licenses from more than one group in a single request will fail with an appropriate error.</span></span> <span data-ttu-id="14c4b-124">Aby dowiedzieć się, jakie licencje są dostępne dla grupy licencji, zobacz [Get a list of available licenses by license group (Uzyskiwanie](get-a-list-of-available-licenses-by-license-group.md)listy dostępnych licencji według grupy licencji).</span><span class="sxs-lookup"><span data-stu-id="14c4b-124">To find out what licenses are available by license group, see [Get a list of available licenses by license group](get-a-list-of-available-licenses-by-license-group.md).</span></span>

<span data-ttu-id="14c4b-125">Oto kroki przypisywania licencji za pomocą kodu:</span><span class="sxs-lookup"><span data-stu-id="14c4b-125">Here are the steps to assign licenses through code:</span></span>

1. <span data-ttu-id="14c4b-126">Utworzyć wystąpienia [**obiektu LicenseAssignment.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)</span><span class="sxs-lookup"><span data-stu-id="14c4b-126">Instantiate a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) object.</span></span> <span data-ttu-id="14c4b-127">Ten obiekt umożliwia określenie przypisanej przez program sku produktu i planów usług.</span><span class="sxs-lookup"><span data-stu-id="14c4b-127">You use this object to specify the product SKU and service plans to assign.</span></span>

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. <span data-ttu-id="14c4b-128">Wypełnij właściwości obiektu, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="14c4b-128">Populate the object properties as shown below.</span></span> <span data-ttu-id="14c4b-129">W tym kodzie przyjęto założenie, że masz już identyfikator SKU produktu i że wszystkie dostępne plany usług zostaną przypisane (to oznacza, że żaden nie zostanie wykluczony).</span><span class="sxs-lookup"><span data-stu-id="14c4b-129">This code assumes that you already have the product SKU ID, and that all of the available service plans will be assigned (that is, none will be excluded).</span></span>

    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. <span data-ttu-id="14c4b-130">Jeśli nie masz identyfikatora jednostki SKU produktu, musisz pobrać kolekcję subskrybowanych jednostki SKU i pobrać identyfikator jednostki SKU produktu z jednej z nich.</span><span class="sxs-lookup"><span data-stu-id="14c4b-130">If you don't have the product SKU ID, you need to retrieve the collection of subscribed SKUs and get the product SKU ID from one of them.</span></span> <span data-ttu-id="14c4b-131">Oto przykład, jeśli znasz nazwę sku produktu.</span><span class="sxs-lookup"><span data-stu-id="14c4b-131">Here is an example if you know the product SKU name.</span></span>

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. <span data-ttu-id="14c4b-132">Następnie należy utworzyć nową listę typu [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)i dodać obiekt licencji.</span><span class="sxs-lookup"><span data-stu-id="14c4b-132">Next, instantiate a new list of type [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment), and add the license object.</span></span> <span data-ttu-id="14c4b-133">Możesz przypisać więcej niż jedną licencję, dodając każdą z nich indywidualnie do listy.</span><span class="sxs-lookup"><span data-stu-id="14c4b-133">You can assign more than one license by adding each individually to the list.</span></span> <span data-ttu-id="14c4b-134">Licencje uwzględnione na tej liście muszą pochodzić z tej samej grupy licencji.</span><span class="sxs-lookup"><span data-stu-id="14c4b-134">The licenses included in this list must be from the same license group.</span></span>

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. <span data-ttu-id="14c4b-135">Utwórz wystąpienie [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) i przypisz listę przypisań licencji do właściwości [**LicensesToAssign.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign)</span><span class="sxs-lookup"><span data-stu-id="14c4b-135">Create a [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) instance and assign the list of license assignments to the [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) property.</span></span>

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. <span data-ttu-id="14c4b-136">Wywołaj [**metodę Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) lub [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) i przekaż obiekt aktualizacji licencji, jak pokazano poniżej, aby przypisać licencje.</span><span class="sxs-lookup"><span data-stu-id="14c4b-136">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) method and pass the license update object as shown below to assign the licenses.</span></span>

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a><span data-ttu-id="14c4b-137">C\#</span><span class="sxs-lookup"><span data-stu-id="14c4b-137">C\#</span></span>

<span data-ttu-id="14c4b-138">Aby przypisać licencję do użytkownika klienta, najpierw należy utworzyć wystąpienia obiektu [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) i wypełnić właściwości [**Skuid**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) i [**ExcludedPlans.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans)</span><span class="sxs-lookup"><span data-stu-id="14c4b-138">To assign a license to a customer user, first instantiate a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) object, and populate the [**Skuid**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) and [**ExcludedPlans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) properties.</span></span> <span data-ttu-id="14c4b-139">Ten obiekt umożliwia określenie produktu SKU do przypisania i plany usługi do wykluczenia.</span><span class="sxs-lookup"><span data-stu-id="14c4b-139">You use this object to specify the product SKU to assign and service plans to exclude.</span></span> <span data-ttu-id="14c4b-140">Następnie należy utworzyć nową listę typu **LicenseAssignment** i dodać obiekt licencji do listy.</span><span class="sxs-lookup"><span data-stu-id="14c4b-140">Next, instantiate a new list of type **LicenseAssignment**, and add the license object to the list.</span></span> <span data-ttu-id="14c4b-141">Następnie utwórz wystąpienie [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) i przypisz listę przypisań licencji do właściwości [**LicensesToAssign.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign)</span><span class="sxs-lookup"><span data-stu-id="14c4b-141">Then create a [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) instance and assign the list of license assignments to the [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) property.</span></span>

<span data-ttu-id="14c4b-142">Następnie użyj metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta, oraz metody [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem użytkownika w celu zidentyfikowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="14c4b-142">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="14c4b-143">Następnie pobierz interfejs do operacji aktualizacji licencji użytkownika klienta z [**właściwości LicenseUpdates.**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates)</span><span class="sxs-lookup"><span data-stu-id="14c4b-143">Then get an interface to customer user license update operations from the [**LicenseUpdates**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) property.</span></span>

<span data-ttu-id="14c4b-144">Na koniec wywołaj [**metodę Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) lub [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) i przekaż obiekt aktualizacji licencji, aby przypisać licencję.</span><span class="sxs-lookup"><span data-stu-id="14c4b-144">Finally, call the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) method and pass the license update object to assign the license.</span></span>

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

<span data-ttu-id="14c4b-145">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="14c4b-145">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="14c4b-146">**Project:** zestaw SDK Centrum partnerskiego Samples **Class**: CustomerUserAssignLicenses.cs</span><span class="sxs-lookup"><span data-stu-id="14c4b-146">**Project**: Partner Center SDK Samples **Class**: CustomerUserAssignLicenses.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="14c4b-147">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="14c4b-147">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="14c4b-148">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="14c4b-148">Request syntax</span></span>

| <span data-ttu-id="14c4b-149">Metoda</span><span class="sxs-lookup"><span data-stu-id="14c4b-149">Method</span></span>   | <span data-ttu-id="14c4b-150">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="14c4b-150">Request URI</span></span>                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="14c4b-151">**Post**</span><span class="sxs-lookup"><span data-stu-id="14c4b-151">**POST**</span></span> | <span data-ttu-id="14c4b-152">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/users/{user-id}/licenseupdates HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="14c4b-152">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenseupdates HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="14c4b-153">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="14c4b-153">URI parameters</span></span>

<span data-ttu-id="14c4b-154">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="14c4b-154">Use the following path parameters to identify the customer and user.</span></span>

| <span data-ttu-id="14c4b-155">Nazwa</span><span class="sxs-lookup"><span data-stu-id="14c4b-155">Name</span></span>        | <span data-ttu-id="14c4b-156">Typ</span><span class="sxs-lookup"><span data-stu-id="14c4b-156">Type</span></span>   | <span data-ttu-id="14c4b-157">Wymagane</span><span class="sxs-lookup"><span data-stu-id="14c4b-157">Required</span></span> | <span data-ttu-id="14c4b-158">Opis</span><span class="sxs-lookup"><span data-stu-id="14c4b-158">Description</span></span>                                       |
|-------------|--------|----------|---------------------------------------------------|
| <span data-ttu-id="14c4b-159">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="14c4b-159">customer-id</span></span> | <span data-ttu-id="14c4b-160">ciąg</span><span class="sxs-lookup"><span data-stu-id="14c4b-160">string</span></span> | <span data-ttu-id="14c4b-161">Tak</span><span class="sxs-lookup"><span data-stu-id="14c4b-161">Yes</span></span>      | <span data-ttu-id="14c4b-162">Identyfikator w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="14c4b-162">A GUID formatted ID that identifies the customer.</span></span> |
| <span data-ttu-id="14c4b-163">user-id</span><span class="sxs-lookup"><span data-stu-id="14c4b-163">user-id</span></span>     | <span data-ttu-id="14c4b-164">ciąg</span><span class="sxs-lookup"><span data-stu-id="14c4b-164">string</span></span> | <span data-ttu-id="14c4b-165">Tak</span><span class="sxs-lookup"><span data-stu-id="14c4b-165">Yes</span></span>      | <span data-ttu-id="14c4b-166">Identyfikator SFORMATOWANY IDENTYFIKATOR GUID, który identyfikuje użytkownika.</span><span class="sxs-lookup"><span data-stu-id="14c4b-166">A GUID formatted ID that identifies the user.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="14c4b-167">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="14c4b-167">Request headers</span></span>

<span data-ttu-id="14c4b-168">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="14c4b-168">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="14c4b-169">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="14c4b-169">Request body</span></span>

<span data-ttu-id="14c4b-170">Uwzględnij [zasób LicenseUpdate](license-resources.md#licenseupdate) w treści żądania, który określa licencje do przypisania.</span><span class="sxs-lookup"><span data-stu-id="14c4b-170">Include a [LicenseUpdate](license-resources.md#licenseupdate) resource in the request body that specifies the licenses to assign.</span></span>

### <a name="request-example"></a><span data-ttu-id="14c4b-171">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="14c4b-171">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="14c4b-172">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="14c4b-172">REST response</span></span>

<span data-ttu-id="14c4b-173">W przypadku powodzenia zwracany jest kod stanu odpowiedzi HTTP 201, a treść odpowiedzi zawiera zasób [LicenseUpdate](license-resources.md#licenseupdate) z informacjami o licencji.</span><span class="sxs-lookup"><span data-stu-id="14c4b-173">If successful, an HTTP response status code 201 is returned and the response body contains a [LicenseUpdate](license-resources.md#licenseupdate) resource with the license information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="14c4b-174">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="14c4b-174">Response success and error codes</span></span>

<span data-ttu-id="14c4b-175">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="14c4b-175">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="14c4b-176">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="14c4b-176">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="14c4b-177">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="14c4b-177">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="14c4b-178">Przykład odpowiedzi (powodzenie)</span><span class="sxs-lookup"><span data-stu-id="14c4b-178">Response example (success)</span></span>

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

### <a name="response-example-license-isnt-available"></a><span data-ttu-id="14c4b-179">Przykład odpowiedzi (licencja nie jest dostępna)</span><span class="sxs-lookup"><span data-stu-id="14c4b-179">Response example (license isn't available)</span></span>

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
