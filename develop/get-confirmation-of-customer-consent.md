---
title: Pobieranie potwierdzenia akceptacji przez klienta umowy dotyczącej platformy Microsoft Cloud
description: W tym artykule wyjaśniono, jak uzyskać potwierdzenie akceptacji przez klienta Umowa dotycząca platformy Microsoft Cloud.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
aauthor: khakiali
ms.author: alikhaki
ms.openlocfilehash: 1b1a8cbacb667e579bcd218a29c3f553afce26c2
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549267"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a><span data-ttu-id="76315-103">Pobieranie potwierdzenia akceptacji przez klienta umowy dotyczącej platformy Microsoft Cloud</span><span class="sxs-lookup"><span data-stu-id="76315-103">Get confirmation of customer acceptance of Microsoft Cloud Agreement</span></span>

<span data-ttu-id="76315-104">**Dotyczy:** Partner Center</span><span class="sxs-lookup"><span data-stu-id="76315-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="76315-105">**Nie dotyczy:** Partner Center obsługiwane przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="76315-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="76315-106">Zasób **Umowy** jest obecnie obsługiwany przez Partner Center tylko w chmurze publicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="76315-106">The **Agreement** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76315-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="76315-107">Prerequisites</span></span>

- <span data-ttu-id="76315-108">Jeśli używasz zestawu SDK platformy .NET Partner Center, wymagana jest wersja 1.9 lub nowsza.</span><span class="sxs-lookup"><span data-stu-id="76315-108">If you are using the Partner Center .NET SDK, version 1.9 or newer is required.</span></span>

- <span data-ttu-id="76315-109">Jeśli używasz zestawu SDK Partner Center Java, wymagana jest wersja 1.8 lub nowsza.</span><span class="sxs-lookup"><span data-stu-id="76315-109">If you are using the Partner Center Java SDK, version 1.8 or newer is required.</span></span>

- <span data-ttu-id="76315-110">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](./partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="76315-110">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="76315-111">Ten scenariusz obsługuje tylko uwierzytelnianie aplikacji i użytkowników.</span><span class="sxs-lookup"><span data-stu-id="76315-111">This scenario only supports app + user authentication.</span></span>

- <span data-ttu-id="76315-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="76315-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="76315-113">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="76315-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="76315-114">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="76315-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="76315-115">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="76315-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="76315-116">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="76315-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="76315-117">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="76315-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="net-version-14-or-newer"></a><span data-ttu-id="76315-118">.NET (wersja 1.4 lub nowsza)</span><span class="sxs-lookup"><span data-stu-id="76315-118">.NET (version 1.4 or newer)</span></span>

<span data-ttu-id="76315-119">Aby pobrać potwierdzenie akceptacji klienta, które zostało wcześniej podane:</span><span class="sxs-lookup"><span data-stu-id="76315-119">To retrieve confirmation(s) of customer acceptance that was previously provided:</span></span>

- <span data-ttu-id="76315-120">Użyj **kolekcji IAggregatePartner.Customers** i wywołaj metodę **ById** z określonym identyfikatorem klienta.</span><span class="sxs-lookup"><span data-stu-id="76315-120">Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.</span></span>

- <span data-ttu-id="76315-121">Pobierz właściwość **Agreements** i przefiltruj wyniki, aby Umowa dotycząca platformy Microsoft Cloud przez wywołanie **metody ByAgreementType.**</span><span class="sxs-lookup"><span data-stu-id="76315-121">Fetch the **Agreements** property and filter the results to Microsoft Cloud Agreement by calling **ByAgreementType** method.</span></span>

- <span data-ttu-id="76315-122">Wywołaj **metodę Get** lub **GetAsync.**</span><span class="sxs-lookup"><span data-stu-id="76315-122">Call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

<span data-ttu-id="76315-123">Pełny przykład można znaleźć w klasie [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) w projekcie [aplikacji testowej konsoli.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)</span><span class="sxs-lookup"><span data-stu-id="76315-123">A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="net-version-19---113"></a><span data-ttu-id="76315-124">.NET (wersja 1.9–1.13)</span><span class="sxs-lookup"><span data-stu-id="76315-124">.NET (version 1.9 - 1.13)</span></span>

<span data-ttu-id="76315-125">Aby pobrać potwierdzenie akceptacji klienta podane wcześniej:</span><span class="sxs-lookup"><span data-stu-id="76315-125">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="76315-126">Użyj **kolekcji IAggregatePartner.Customers** i wywołaj metodę **ById** z określonym identyfikatorem klienta.</span><span class="sxs-lookup"><span data-stu-id="76315-126">Use the **IAggregatePartner.Customers** collection and call the **ById** method with the specified customer's identifier.</span></span> <span data-ttu-id="76315-127">Następnie pobierz właściwość **Agreements,** a następnie wywołaj metody **Get** lub **GetAsync.**</span><span class="sxs-lookup"><span data-stu-id="76315-127">Then, get the **Agreements** property, followed by calling the **Get** or **GetAsync** methods.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a><span data-ttu-id="76315-128">Java</span><span class="sxs-lookup"><span data-stu-id="76315-128">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="76315-129">Aby pobrać potwierdzenie akceptacji klienta podane wcześniej:</span><span class="sxs-lookup"><span data-stu-id="76315-129">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="76315-130">Użyj funkcji **IAggregatePartner.getCustomers** i wywołaj funkcję **byId** z określonym identyfikatorem klienta.</span><span class="sxs-lookup"><span data-stu-id="76315-130">Use the **IAggregatePartner.getCustomers** function and call the **byId** function with the specified customer's identifier.</span></span> <span data-ttu-id="76315-131">Następnie pobierz funkcję **getAgreements,** a następnie wywołaj funkcję **get.**</span><span class="sxs-lookup"><span data-stu-id="76315-131">Then, get the **getAgreements** function, followed by calling the **get** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

<span data-ttu-id="76315-132">Pełny przykład można znaleźć w klasie [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) w projekcie [aplikacji testowej konsoli.](https://github.com/Microsoft/Partner-Center-Java-Samples)</span><span class="sxs-lookup"><span data-stu-id="76315-132">A complete sample can be found in the [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.</span></span>

## <a name="powershell"></a><span data-ttu-id="76315-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="76315-133">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="76315-134">Aby pobrać potwierdzenie akceptacji klienta podane wcześniej:</span><span class="sxs-lookup"><span data-stu-id="76315-134">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="76315-135">Użyj polecenia [**Get-PartnerCustomerAgreement.**](/powershell/module/partnercenter/get-partnercustomeragreement)</span><span class="sxs-lookup"><span data-stu-id="76315-135">Use the [**Get-PartnerCustomerAgreement**](/powershell/module/partnercenter/get-partnercustomeragreement) command.</span></span>

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest-request"></a><span data-ttu-id="76315-136">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="76315-136">REST request</span></span>

<span data-ttu-id="76315-137">Aby pobrać potwierdzenie akceptacji klienta podane wcześniej, zobacz następujące instrukcje.</span><span class="sxs-lookup"><span data-stu-id="76315-137">To retrieve confirmation of customer acceptance provided previously, see the following instructions.</span></span>

<span data-ttu-id="76315-138">Utwórz nowy **zasób umowy** z odpowiednimi informacjami o certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="76315-138">Create a new **Agreement** resource with the relevant certification information.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="76315-139">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="76315-139">Request syntax</span></span>

| <span data-ttu-id="76315-140">Metoda</span><span class="sxs-lookup"><span data-stu-id="76315-140">Method</span></span> | <span data-ttu-id="76315-141">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="76315-141">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="76315-142">GET</span><span class="sxs-lookup"><span data-stu-id="76315-142">GET</span></span>    | <span data-ttu-id="76315-143">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="76315-143">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="76315-144">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="76315-144">URI parameter</span></span>

<span data-ttu-id="76315-145">Użyj następującego parametru zapytania, aby określić potwierdzanego klienta.</span><span class="sxs-lookup"><span data-stu-id="76315-145">Use the following query parameter to specify the customer you are confirming.</span></span>

| <span data-ttu-id="76315-146">Nazwa</span><span class="sxs-lookup"><span data-stu-id="76315-146">Name</span></span>             | <span data-ttu-id="76315-147">Typ</span><span class="sxs-lookup"><span data-stu-id="76315-147">Type</span></span> | <span data-ttu-id="76315-148">Wymagane</span><span class="sxs-lookup"><span data-stu-id="76315-148">Required</span></span> | <span data-ttu-id="76315-149">Opis</span><span class="sxs-lookup"><span data-stu-id="76315-149">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="76315-150">CustomerTenantId</span><span class="sxs-lookup"><span data-stu-id="76315-150">CustomerTenantId</span></span> | <span data-ttu-id="76315-151">GUID</span><span class="sxs-lookup"><span data-stu-id="76315-151">GUID</span></span> | <span data-ttu-id="76315-152">Y</span><span class="sxs-lookup"><span data-stu-id="76315-152">Y</span></span>        | <span data-ttu-id="76315-153">Wartość to identyfikator GUID w **formacie CustomerTenantId,** który umożliwia określenie klienta.</span><span class="sxs-lookup"><span data-stu-id="76315-153">The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="76315-154">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="76315-154">Request headers</span></span>

<span data-ttu-id="76315-155">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="76315-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="76315-156">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="76315-156">Request body</span></span>

<span data-ttu-id="76315-157">Brak.</span><span class="sxs-lookup"><span data-stu-id="76315-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="76315-158">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="76315-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="76315-159">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="76315-159">REST response</span></span>

<span data-ttu-id="76315-160">W przypadku powodzenia ta metoda zwraca kolekcję zasobów **umowy** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="76315-160">If successful, this method returns a collection of **Agreement** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="76315-161">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="76315-161">Response success and error codes</span></span>

<span data-ttu-id="76315-162">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="76315-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="76315-163">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="76315-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="76315-164">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="76315-164">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="76315-165">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="76315-165">Response example</span></span>

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
