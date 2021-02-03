---
title: Pobieranie potwierdzenia akceptacji przez klienta umowy dotyczącej platformy Microsoft Cloud
description: W tym artykule wyjaśniono, jak uzyskać potwierdzenie akceptacji przez klienta umowy Microsoft Cloud.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
aauthor: khakiali
ms.author: alikhaki
ms.openlocfilehash: d91f70cbd8bc9b8622b8d41ab9e601e2aee2cfab
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768446"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a><span data-ttu-id="988b0-103">Pobieranie potwierdzenia akceptacji przez klienta umowy dotyczącej platformy Microsoft Cloud</span><span class="sxs-lookup"><span data-stu-id="988b0-103">Get confirmation of customer acceptance of Microsoft Cloud Agreement</span></span>

<span data-ttu-id="988b0-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="988b0-104">**Applies To**</span></span>

- <span data-ttu-id="988b0-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="988b0-105">Partner Center</span></span>

> [!NOTE]
> <span data-ttu-id="988b0-106">Zasób z **umową** jest obecnie obsługiwany przez centrum partnerskie tylko w chmurze publicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="988b0-106">The **Agreement** resource is currently supported by Partner Center in the Microsoft public cloud only.</span></span> <span data-ttu-id="988b0-107">Nie dotyczy:</span><span class="sxs-lookup"><span data-stu-id="988b0-107">It isn't applicable to:</span></span>
>
> - <span data-ttu-id="988b0-108">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="988b0-108">Partner Center operated by 21Vianet</span></span>
> - <span data-ttu-id="988b0-109">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="988b0-109">Partner Center for Microsoft Cloud Germany</span></span>
> - <span data-ttu-id="988b0-110">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="988b0-110">Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="prerequisites"></a><span data-ttu-id="988b0-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="988b0-111">Prerequisites</span></span>

- <span data-ttu-id="988b0-112">W przypadku korzystania z zestawu SDK platformy .NET w programie Partner Center wymagany jest program w wersji 1,9 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="988b0-112">If you are using the Partner Center .NET SDK, version 1.9 or newer is required.</span></span>

- <span data-ttu-id="988b0-113">W przypadku korzystania z zestawu SDK języka Java Centrum partnerskiego wymagana jest wersja 1,8 lub nowsza.</span><span class="sxs-lookup"><span data-stu-id="988b0-113">If you are using the Partner Center Java SDK, version 1.8 or newer is required.</span></span>

- <span data-ttu-id="988b0-114">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](./partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="988b0-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="988b0-115">Ten scenariusz obsługuje tylko uwierzytelnianie aplikacji i użytkowników.</span><span class="sxs-lookup"><span data-stu-id="988b0-115">This scenario supports only supports app + user authentication.</span></span>

- <span data-ttu-id="988b0-116">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="988b0-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="988b0-117">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="988b0-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="988b0-118">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="988b0-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="988b0-119">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="988b0-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="988b0-120">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="988b0-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="988b0-121">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="988b0-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="net-version-14-or-newer"></a><span data-ttu-id="988b0-122">.NET (wersja 1,4 lub nowsza)</span><span class="sxs-lookup"><span data-stu-id="988b0-122">.NET (version 1.4 or newer)</span></span>

<span data-ttu-id="988b0-123">Aby pobrać potwierdzenia, które zostały wcześniej dostarczone przez klienta:</span><span class="sxs-lookup"><span data-stu-id="988b0-123">To retrieve confirmation(s) of customer acceptance that was previously provided:</span></span>

- <span data-ttu-id="988b0-124">Użyj metody **IAggregatePartner. Customers** i Wywołaj metodę **ById** z określonym identyfikatorem klienta.</span><span class="sxs-lookup"><span data-stu-id="988b0-124">Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.</span></span>

- <span data-ttu-id="988b0-125">Pobierz Właściwość **Agreements** i przefiltruj wyniki do Microsoft Cloudej umowy przez wywołanie metody **ByAgreementType** .</span><span class="sxs-lookup"><span data-stu-id="988b0-125">Fetch the **Agreements** property and filter the results to Microsoft Cloud Agreement by calling **ByAgreementType** method.</span></span>

- <span data-ttu-id="988b0-126">Wywoływanie metody **Get** lub **GetAsync** .</span><span class="sxs-lookup"><span data-stu-id="988b0-126">Call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

<span data-ttu-id="988b0-127">Pełny przykład można znaleźć w klasie [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) z projektu [aplikacji testowej konsoli](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .</span><span class="sxs-lookup"><span data-stu-id="988b0-127">A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="net-version-19---113"></a><span data-ttu-id="988b0-128">.NET (wersja 1,9-1,13)</span><span class="sxs-lookup"><span data-stu-id="988b0-128">.NET (version 1.9 - 1.13)</span></span>

<span data-ttu-id="988b0-129">Aby pobrać potwierdzenie podanej wcześniej akceptacji klienta:</span><span class="sxs-lookup"><span data-stu-id="988b0-129">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="988b0-130">Użyj kolekcji **IAggregatePartner. Customers** i Wywołaj metodę **ById** przy użyciu identyfikatora określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="988b0-130">Use the **IAggregatePartner.Customers** collection and call the **ById** method with the specified customer's identifier.</span></span> <span data-ttu-id="988b0-131">Następnie Pobierz Właściwość **Agreement** , a następnie wywołując metody **Get** lub **GetAsync** .</span><span class="sxs-lookup"><span data-stu-id="988b0-131">Then, get the **Agreements** property, followed by calling the **Get** or **GetAsync** methods.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a><span data-ttu-id="988b0-132">Java</span><span class="sxs-lookup"><span data-stu-id="988b0-132">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="988b0-133">Aby pobrać potwierdzenie podanej wcześniej akceptacji klienta:</span><span class="sxs-lookup"><span data-stu-id="988b0-133">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="988b0-134">Użyj funkcji **IAggregatePartner. GetCustomers** i wywołaj funkcję **byId** z identyfikatorem określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="988b0-134">Use the **IAggregatePartner.getCustomers** function and call the **byId** function with the specified customer's identifier.</span></span> <span data-ttu-id="988b0-135">Następnie Pobierz funkcję **Getagreements** , a następnie wywołując funkcję **Get** .</span><span class="sxs-lookup"><span data-stu-id="988b0-135">Then, get the **getAgreements** function, followed by calling the **get** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

<span data-ttu-id="988b0-136">Pełny przykład można znaleźć w klasie [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) z projektu [aplikacji testowej konsoli](https://github.com/Microsoft/Partner-Center-Java-Samples) .</span><span class="sxs-lookup"><span data-stu-id="988b0-136">A complete sample can be found in the [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.</span></span>

## <a name="powershell"></a><span data-ttu-id="988b0-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="988b0-137">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="988b0-138">Aby pobrać potwierdzenie podanej wcześniej akceptacji klienta:</span><span class="sxs-lookup"><span data-stu-id="988b0-138">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="988b0-139">Użyj polecenia [**Get-PartnerCustomerAgreement**](/powershell/module/partnercenter/get-partnercustomeragreement) .</span><span class="sxs-lookup"><span data-stu-id="988b0-139">Use the [**Get-PartnerCustomerAgreement**](/powershell/module/partnercenter/get-partnercustomeragreement) command.</span></span>

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest-request"></a><span data-ttu-id="988b0-140">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="988b0-140">REST request</span></span>

<span data-ttu-id="988b0-141">Aby pobrać potwierdzenie podanej wcześniej akceptacji klienta, zapoznaj się z poniższymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="988b0-141">To retrieve confirmation of customer acceptance provided previously, see the following instructions.</span></span>

<span data-ttu-id="988b0-142">Utwórz nowy zasób **umowy** z odpowiednimi informacjami o certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="988b0-142">Create a new **Agreement** resource with the relevant certification information.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="988b0-143">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="988b0-143">Request syntax</span></span>

| <span data-ttu-id="988b0-144">Metoda</span><span class="sxs-lookup"><span data-stu-id="988b0-144">Method</span></span> | <span data-ttu-id="988b0-145">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="988b0-145">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="988b0-146">GET</span><span class="sxs-lookup"><span data-stu-id="988b0-146">GET</span></span>    | <span data-ttu-id="988b0-147">[*\{ BASEURL \}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Agreements http/1.1</span><span class="sxs-lookup"><span data-stu-id="988b0-147">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="988b0-148">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="988b0-148">URI parameter</span></span>

<span data-ttu-id="988b0-149">Użyj następującego parametru zapytania, aby określić klienta, który chcesz potwierdzić.</span><span class="sxs-lookup"><span data-stu-id="988b0-149">Use the following query parameter to specify the customer you are confirming.</span></span>

| <span data-ttu-id="988b0-150">Nazwa</span><span class="sxs-lookup"><span data-stu-id="988b0-150">Name</span></span>             | <span data-ttu-id="988b0-151">Typ</span><span class="sxs-lookup"><span data-stu-id="988b0-151">Type</span></span> | <span data-ttu-id="988b0-152">Wymagane</span><span class="sxs-lookup"><span data-stu-id="988b0-152">Required</span></span> | <span data-ttu-id="988b0-153">Opis</span><span class="sxs-lookup"><span data-stu-id="988b0-153">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="988b0-154">CustomerTenantId</span><span class="sxs-lookup"><span data-stu-id="988b0-154">CustomerTenantId</span></span> | <span data-ttu-id="988b0-155">GUID</span><span class="sxs-lookup"><span data-stu-id="988b0-155">GUID</span></span> | <span data-ttu-id="988b0-156">Y</span><span class="sxs-lookup"><span data-stu-id="988b0-156">Y</span></span>        | <span data-ttu-id="988b0-157">Wartość jest identyfikatorem GUID w formacie **CustomerTenantId** , który umożliwia określenie klienta.</span><span class="sxs-lookup"><span data-stu-id="988b0-157">The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="988b0-158">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="988b0-158">Request headers</span></span>

<span data-ttu-id="988b0-159">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="988b0-159">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="988b0-160">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="988b0-160">Request body</span></span>

<span data-ttu-id="988b0-161">Brak.</span><span class="sxs-lookup"><span data-stu-id="988b0-161">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="988b0-162">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="988b0-162">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="988b0-163">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="988b0-163">REST response</span></span>

<span data-ttu-id="988b0-164">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów **umowy** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="988b0-164">If successful, this method returns a collection of **Agreement** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="988b0-165">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="988b0-165">Response success and error codes</span></span>

<span data-ttu-id="988b0-166">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="988b0-166">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="988b0-167">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="988b0-167">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="988b0-168">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="988b0-168">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="988b0-169">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="988b0-169">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 2,
    "items":
    [
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2018-07-28T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2017-08-01T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        }
    ]
}
```
