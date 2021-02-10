---
title: Potwierdzenie akceptacji przez klienta umowy klienta firmy Microsoft
description: Dowiedz się, w jaki sposób potwierdzić akceptację umowy klienta firmy Microsoft przy użyciu interfejsów API Centrum partnerskiego.
ms.date: 02/08/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 62a6cebd5d6d093377dd5940dcff6204b7095c70
ms.sourcegitcommit: ebb36208d6e2dea705f62b7d60d471f10c55132e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/09/2021
ms.locfileid: "100006066"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a><span data-ttu-id="553af-103">Potwierdzenie akceptacji przez klienta umowy klienta firmy Microsoft przy użyciu interfejsów API Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="553af-103">Confirm customer acceptance of the Microsoft Customer Agreement using Partner Center APIs</span></span>

<span data-ttu-id="553af-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="553af-104">**Applies to:**</span></span>

- <span data-ttu-id="553af-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="553af-105">Partner Center</span></span>

<span data-ttu-id="553af-106">Centrum partnerskie obecnie obsługuje Potwierdzanie akceptacji przez klienta umowy klienta firmy Microsoft tylko w *chmurze publicznej firmy Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="553af-106">Partner Center currently supports confirmation of customer acceptance of the Microsoft Customer Agreement only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="553af-107">Ta funkcja nie ma obecnie zastosowania do:</span><span class="sxs-lookup"><span data-stu-id="553af-107">This functionality doesn't currently apply to:</span></span>

- <span data-ttu-id="553af-108">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="553af-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="553af-109">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="553af-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="553af-110">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="553af-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="553af-111">W tym artykule opisano sposób potwierdzania lub ponownego potwierdzania akceptacji przez klienta umowy klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="553af-111">This article describes how to confirm or re-confirm customer acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="553af-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="553af-112">Prerequisites</span></span>

- <span data-ttu-id="553af-113">W przypadku korzystania z zestawu SDK platformy .NET w programie Partner Center wymagany jest program w wersji 1,14 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="553af-113">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="553af-114">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](./partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="553af-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="553af-115">*Ten scenariusz obsługuje tylko uwierzytelnianie aplikacji i użytkowników.*</span><span class="sxs-lookup"><span data-stu-id="553af-115">*This scenario only supports App+User authentication.*</span></span>

- <span data-ttu-id="553af-116">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="553af-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="553af-117">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="553af-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="553af-118">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="553af-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="553af-119">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="553af-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="553af-120">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="553af-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="553af-121">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="553af-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="553af-122">Data (**dateAgreed**), gdy klient zaakceptował umowę klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="553af-122">The date (**dateAgreed**) when the customer accepted the Microsoft Customer Agreement.</span></span>

- <span data-ttu-id="553af-123">Informacje o użytkowniku z organizacji klienta, które zaakceptowali umowę klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="553af-123">Information about the user from the customer organization that accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="553af-124">Obejmuje to następujące działania:</span><span class="sxs-lookup"><span data-stu-id="553af-124">This includes:</span></span>
  - <span data-ttu-id="553af-125">Imię</span><span class="sxs-lookup"><span data-stu-id="553af-125">First name</span></span>
  - <span data-ttu-id="553af-126">Nazwisko</span><span class="sxs-lookup"><span data-stu-id="553af-126">Last name</span></span>
  - <span data-ttu-id="553af-127">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="553af-127">Email address</span></span>
  - <span data-ttu-id="553af-128">Numer telefonu (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="553af-128">Phone number (optional)</span></span>
- <span data-ttu-id="553af-129">Jeśli następujące wartości są zmieniane dla klienta, centrum partnerskie umożliwi utworzenie innej umowy dla tego klienta: imię nazwisko nazwisko numer telefonu adres E-mail w przeciwnym razie partnerzy otrzymają następujący kod błędu ze względu na utworzenie duplikatu klienta</span><span class="sxs-lookup"><span data-stu-id="553af-129">If the following values change for a customer, Partner Center  will allow for another agreement to be created for that customer:       First Name       Last Name       Email address       Phone number Otherwise partners will receive the following error code, due to a duplicate customer being created</span></span>


```
{
"code": 600061,
"message": "A partner confirmed agreement already exists for the customer.",
"description": "A partner confirmed agreement already exists for the customer.",
"errorName": "PartnerConfirmedAgreementAlreadyExists",
"isRetryable": false,
"parameters": {},
"errorMessageExtended": "InternalErrorCode=600061"
}
 ```

## <a name="net"></a><span data-ttu-id="553af-130">.NET</span><span class="sxs-lookup"><span data-stu-id="553af-130">.NET</span></span>

<span data-ttu-id="553af-131">Aby potwierdzić lub ponownie potwierdzić akceptację klienta umowy klienta firmy Microsoft:</span><span class="sxs-lookup"><span data-stu-id="553af-131">To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="553af-132">Pobierz metadane umowy dla umowy klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="553af-132">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="553af-133">Musisz uzyskać **TemplateID** umowy klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="553af-133">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="553af-134">Aby uzyskać więcej informacji, zobacz [Pobieranie metadanych umów dla umowy klienta firmy Microsoft](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="553af-134">For more details, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. <span data-ttu-id="553af-135">Utwórz nowy obiekt **umowy** zawierający szczegóły potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="553af-135">Create a new **Agreement** object containing details of the confirmation.</span></span>

3. <span data-ttu-id="553af-136">Użyj kolekcji **IAgreggatePartner. Customers** i Wywołaj metodę **ById** z określonym **identyfikatorem dzierżawy klienta**.</span><span class="sxs-lookup"><span data-stu-id="553af-136">Use the **IAgreggatePartner.Customers** collection and call the **ById** method with the specified **customer-tenant-id**.</span></span>

4. <span data-ttu-id="553af-137">Użyj właściwości **Agreements** , a następnie wywoływanie metody **Create** lub **Async**.</span><span class="sxs-lookup"><span data-stu-id="553af-137">Use the **Agreements** property, followed by calling **Create** or **CreateAsync**.</span></span>

   ```csharp
   // string selectedCustomerId;

   var agreementToCreate = new Agreement
   {
       DateAgreed = DateTime.UtcNow,
       TemplateId = microsoftCustomerAgreementDetails.TemplateId,
       PrimaryContact = new Contact
       {
           FirstName = "Tania",
           LastName = "Carr",
           Email = "someone@example.com",
           PhoneNumber = "1234567890"
       }
   };

   Agreement agreement = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Create(agreementToCreate);
   ```

<span data-ttu-id="553af-138">Pełny przykład można znaleźć w klasie [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) z projektu [aplikacji testowej konsoli](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .</span><span class="sxs-lookup"><span data-stu-id="553af-138">A complete sample can be found in the [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="553af-139">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="553af-139">REST request</span></span>

<span data-ttu-id="553af-140">Aby potwierdzić lub ponownie potwierdzić akceptację klienta umowy klienta firmy Microsoft:</span><span class="sxs-lookup"><span data-stu-id="553af-140">To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="553af-141">Pobierz metadane umowy dla umowy klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="553af-141">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="553af-142">Musisz uzyskać **TemplateID** umowy klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="553af-142">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="553af-143">Aby uzyskać więcej informacji, zobacz [Pobieranie metadanych umów dla umowy klienta firmy Microsoft](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="553af-143">For more details, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

2. <span data-ttu-id="553af-144">Utwórz nowy zasób [ **umowy**](agreement-resources.md) , aby potwierdzić, że klient zaakceptował umowę klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="553af-144">Create a new [**Agreement** resource](agreement-resources.md) to confirm that a customer has accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="553af-145">Użyj następującej [składni żądania REST](#request-syntax).</span><span class="sxs-lookup"><span data-stu-id="553af-145">Use the following [REST request syntax](#request-syntax).</span></span>

### <a name="request-syntax"></a><span data-ttu-id="553af-146">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="553af-146">Request syntax</span></span>

| <span data-ttu-id="553af-147">Metoda</span><span class="sxs-lookup"><span data-stu-id="553af-147">Method</span></span> | <span data-ttu-id="553af-148">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="553af-148">Request URI</span></span>                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="553af-149">POST</span><span class="sxs-lookup"><span data-stu-id="553af-149">POST</span></span>   | <span data-ttu-id="553af-150">[*\{ BASEURL \}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Agreements http/1.1</span><span class="sxs-lookup"><span data-stu-id="553af-150">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="553af-151">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="553af-151">URI parameter</span></span>

<span data-ttu-id="553af-152">Użyj następującego parametru zapytania, aby określić klienta, który potwierdzasz.</span><span class="sxs-lookup"><span data-stu-id="553af-152">Use the following query parameter to specify the customer that you're confirming.</span></span>

| <span data-ttu-id="553af-153">Nazwa</span><span class="sxs-lookup"><span data-stu-id="553af-153">Name</span></span>               | <span data-ttu-id="553af-154">Typ</span><span class="sxs-lookup"><span data-stu-id="553af-154">Type</span></span> | <span data-ttu-id="553af-155">Wymagane</span><span class="sxs-lookup"><span data-stu-id="553af-155">Required</span></span> | <span data-ttu-id="553af-156">Opis</span><span class="sxs-lookup"><span data-stu-id="553af-156">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="553af-157">Identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="553af-157">customer-tenant-id</span></span> | <span data-ttu-id="553af-158">GUID</span><span class="sxs-lookup"><span data-stu-id="553af-158">GUID</span></span> | <span data-ttu-id="553af-159">Tak</span><span class="sxs-lookup"><span data-stu-id="553af-159">Yes</span></span> | <span data-ttu-id="553af-160">Wartość jest identyfikatorem GUID, który jest sformatowanym identyfikatorem **dzierżawy**, który umożliwia określenie klienta.</span><span class="sxs-lookup"><span data-stu-id="553af-160">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="553af-161">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="553af-161">Request headers</span></span>

<span data-ttu-id="553af-162">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="553af-162">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="553af-163">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="553af-163">Request body</span></span>

<span data-ttu-id="553af-164">W tej tabeli opisano wymagane właściwości w treści żądania REST.</span><span class="sxs-lookup"><span data-stu-id="553af-164">This table describes the required properties in the REST request body.</span></span>

| <span data-ttu-id="553af-165">Nazwa</span><span class="sxs-lookup"><span data-stu-id="553af-165">Name</span></span>      | <span data-ttu-id="553af-166">Typ</span><span class="sxs-lookup"><span data-stu-id="553af-166">Type</span></span>   | <span data-ttu-id="553af-167">Opis</span><span class="sxs-lookup"><span data-stu-id="553af-167">Description</span></span>                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="553af-168">Umowa</span><span class="sxs-lookup"><span data-stu-id="553af-168">Agreement</span></span> | <span data-ttu-id="553af-169">object</span><span class="sxs-lookup"><span data-stu-id="553af-169">object</span></span> | <span data-ttu-id="553af-170">Szczegóły dostarczone przez partnera w celu potwierdzenia akceptacji umowy klienta firmy Microsoft przez klienta.</span><span class="sxs-lookup"><span data-stu-id="553af-170">Details provided by partner to confirm customer acceptance of the Microsoft Customer Agreement.</span></span> |

#### <a name="agreement"></a><span data-ttu-id="553af-171">Umowa</span><span class="sxs-lookup"><span data-stu-id="553af-171">Agreement</span></span>

<span data-ttu-id="553af-172">Ta tabela zawiera opis minimalnych wymaganych pól w celu utworzenia [zasobu **umowy**](agreement-resources.md).</span><span class="sxs-lookup"><span data-stu-id="553af-172">This table describes the minimum required fields to create an [**Agreement** resource](agreement-resources.md).</span></span>

| <span data-ttu-id="553af-173">Właściwość</span><span class="sxs-lookup"><span data-stu-id="553af-173">Property</span></span>       | <span data-ttu-id="553af-174">Typ</span><span class="sxs-lookup"><span data-stu-id="553af-174">Type</span></span>   | <span data-ttu-id="553af-175">Opis</span><span class="sxs-lookup"><span data-stu-id="553af-175">Description</span></span>                              |
|----------------|--------|------------------------------------------|
| <span data-ttu-id="553af-176">primaryContact</span><span class="sxs-lookup"><span data-stu-id="553af-176">primaryContact</span></span> | [<span data-ttu-id="553af-177">Kontakt</span><span class="sxs-lookup"><span data-stu-id="553af-177">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="553af-178">Informacje o użytkowniku z organizacji klienta, którzy zaakceptowali umowę klienta firmy Microsoft, w tym:  **FirstName**, **LastName**, **email** i numer **telefonu** (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="553af-178">Information about the user from the customer organization who accepted the Microsoft Customer Agreement, including:  **firstName**, **lastName**, **email** and **phoneNumber** (optional)</span></span> |
| <span data-ttu-id="553af-179">dateAgreed</span><span class="sxs-lookup"><span data-stu-id="553af-179">dateAgreed</span></span>     | <span data-ttu-id="553af-180">ciąg w formacie daty i godziny czasu UTC</span><span class="sxs-lookup"><span data-stu-id="553af-180">string in UTC date time format</span></span> |<span data-ttu-id="553af-181">Data zaakceptowania umowy przez klienta.</span><span class="sxs-lookup"><span data-stu-id="553af-181">The date when the customer accepted the agreement.</span></span> |
| <span data-ttu-id="553af-182">templateId</span><span class="sxs-lookup"><span data-stu-id="553af-182">templateId</span></span>     | <span data-ttu-id="553af-183">ciąg</span><span class="sxs-lookup"><span data-stu-id="553af-183">string</span></span> | <span data-ttu-id="553af-184">Unikatowy identyfikator typu umowy akceptowany przez klienta.</span><span class="sxs-lookup"><span data-stu-id="553af-184">Unique identifier of the agreement type accepted by the customer.</span></span> <span data-ttu-id="553af-185">Możesz uzyskać **templateId** dla umowy klienta Microsoft, pobierając metadane umowy dla umowy klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="553af-185">You can obtain the **templateId** for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement.</span></span> <span data-ttu-id="553af-186">Aby uzyskać szczegółowe informacje, zobacz artykuł [Pobierz metadane umowy dla umowy klienta firmy Microsoft](./get-customer-agreement-metadata.md) .</span><span class="sxs-lookup"><span data-stu-id="553af-186">See [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md) for details.</span></span> |
| <span data-ttu-id="553af-187">typ</span><span class="sxs-lookup"><span data-stu-id="553af-187">type</span></span>           | <span data-ttu-id="553af-188">ciąg</span><span class="sxs-lookup"><span data-stu-id="553af-188">string</span></span> | <span data-ttu-id="553af-189">Typ umowy akceptowany przez klienta.</span><span class="sxs-lookup"><span data-stu-id="553af-189">Agreement type accepted by the customer.</span></span> <span data-ttu-id="553af-190">Jeśli klient zaakceptuje umowę klienta firmy Microsoft, należy użyć "MicrosoftCustomerAgreement".</span><span class="sxs-lookup"><span data-stu-id="553af-190">Use "MicrosoftCustomerAgreement" if customer accepted the Microsoft Customer Agreement.</span></span> |

#### <a name="request-example"></a><span data-ttu-id="553af-191">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="553af-191">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```

## <a name="rest-response"></a><span data-ttu-id="553af-192">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="553af-192">REST response</span></span>

<span data-ttu-id="553af-193">Jeśli to się powiedzie, metoda zwraca [zasób **umowy**](./agreement-resources.md).</span><span class="sxs-lookup"><span data-stu-id="553af-193">If successful, this method returns an [**Agreement** resource](./agreement-resources.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="553af-194">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="553af-194">Response success and error codes</span></span>

<span data-ttu-id="553af-195">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="553af-195">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="553af-196">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="553af-196">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="553af-197">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="553af-197">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="553af-198">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="553af-198">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 261
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "userId": "3d6f2c09-eb40-48ca-a4b3-d24c9c007531",
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```
