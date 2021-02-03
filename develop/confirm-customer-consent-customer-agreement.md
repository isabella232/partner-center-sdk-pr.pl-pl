---
title: Potwierdzenie akceptacji przez klienta umowy klienta firmy Microsoft
description: Dowiedz się, w jaki sposób potwierdzić akceptację umowy klienta firmy Microsoft przy użyciu interfejsów API Centrum partnerskiego.
ms.date: 02/04/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 239ca43c70fb8aa7f0d06e564e6c0726b235ffbe
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768590"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a><span data-ttu-id="54995-103">Potwierdzenie akceptacji przez klienta umowy klienta firmy Microsoft przy użyciu interfejsów API Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="54995-103">Confirm customer acceptance of the Microsoft Customer Agreement using Partner Center APIs</span></span>

<span data-ttu-id="54995-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="54995-104">**Applies to:**</span></span>

- <span data-ttu-id="54995-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="54995-105">Partner Center</span></span>

<span data-ttu-id="54995-106">Centrum partnerskie obecnie obsługuje Potwierdzanie akceptacji przez klienta umowy klienta firmy Microsoft tylko w *chmurze publicznej firmy Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="54995-106">Partner Center currently supports confirmation of customer acceptance of the Microsoft Customer Agreement only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="54995-107">Ta funkcja nie ma obecnie zastosowania do:</span><span class="sxs-lookup"><span data-stu-id="54995-107">This functionality doesn't currently apply to:</span></span>

- <span data-ttu-id="54995-108">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="54995-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="54995-109">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="54995-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="54995-110">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="54995-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="54995-111">W tym artykule opisano sposób potwierdzania lub ponownego potwierdzania akceptacji przez klienta umowy klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="54995-111">This article describes how to confirm or re-confirm customer acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54995-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="54995-112">Prerequisites</span></span>

- <span data-ttu-id="54995-113">W przypadku korzystania z zestawu SDK platformy .NET w programie Partner Center wymagany jest program w wersji 1,14 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="54995-113">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="54995-114">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](./partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="54995-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="54995-115">*Ten scenariusz obsługuje tylko uwierzytelnianie aplikacji i użytkowników.*</span><span class="sxs-lookup"><span data-stu-id="54995-115">*This scenario only supports App+User authentication.*</span></span>

- <span data-ttu-id="54995-116">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="54995-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="54995-117">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="54995-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="54995-118">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="54995-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="54995-119">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="54995-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="54995-120">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="54995-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="54995-121">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="54995-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="54995-122">Data (**dateAgreed**), gdy klient zaakceptował umowę klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="54995-122">The date (**dateAgreed**) when the customer accepted the Microsoft Customer Agreement.</span></span>

- <span data-ttu-id="54995-123">Informacje o użytkowniku z organizacji klienta, które zaakceptowali umowę klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="54995-123">Information about the user from the customer organization that accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="54995-124">Obejmuje to następujące działania:</span><span class="sxs-lookup"><span data-stu-id="54995-124">This includes:</span></span>
  - <span data-ttu-id="54995-125">Imię</span><span class="sxs-lookup"><span data-stu-id="54995-125">First name</span></span>
  - <span data-ttu-id="54995-126">Nazwisko</span><span class="sxs-lookup"><span data-stu-id="54995-126">Last name</span></span>
  - <span data-ttu-id="54995-127">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="54995-127">Email address</span></span>
  - <span data-ttu-id="54995-128">Numer telefonu (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="54995-128">Phone number (optional)</span></span>

## <a name="net"></a><span data-ttu-id="54995-129">.NET</span><span class="sxs-lookup"><span data-stu-id="54995-129">.NET</span></span>

<span data-ttu-id="54995-130">Aby potwierdzić lub ponownie potwierdzić akceptację klienta umowy klienta firmy Microsoft:</span><span class="sxs-lookup"><span data-stu-id="54995-130">To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="54995-131">Pobierz metadane umowy dla umowy klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="54995-131">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="54995-132">Musisz uzyskać **TemplateID** umowy klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="54995-132">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="54995-133">Aby uzyskać więcej informacji, zobacz [Pobieranie metadanych umów dla umowy klienta firmy Microsoft](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="54995-133">For more details, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. <span data-ttu-id="54995-134">Utwórz nowy obiekt **umowy** zawierający szczegóły potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="54995-134">Create a new **Agreement** object containing details of the confirmation.</span></span>

3. <span data-ttu-id="54995-135">Użyj kolekcji **IAgreggatePartner. Customers** i Wywołaj metodę **ById** z określonym **identyfikatorem dzierżawy klienta**.</span><span class="sxs-lookup"><span data-stu-id="54995-135">Use the **IAgreggatePartner.Customers** collection and call the **ById** method with the specified **customer-tenant-id**.</span></span>

4. <span data-ttu-id="54995-136">Użyj właściwości **Agreements** , a następnie wywoływanie metody **Create** lub **Async**.</span><span class="sxs-lookup"><span data-stu-id="54995-136">Use the **Agreements** property, followed by calling **Create** or **CreateAsync**.</span></span>

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

<span data-ttu-id="54995-137">Pełny przykład można znaleźć w klasie [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) z projektu [aplikacji testowej konsoli](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .</span><span class="sxs-lookup"><span data-stu-id="54995-137">A complete sample can be found in the [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="54995-138">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="54995-138">REST request</span></span>

<span data-ttu-id="54995-139">Aby potwierdzić lub ponownie potwierdzić akceptację klienta umowy klienta firmy Microsoft:</span><span class="sxs-lookup"><span data-stu-id="54995-139">To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="54995-140">Pobierz metadane umowy dla umowy klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="54995-140">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="54995-141">Musisz uzyskać **TemplateID** umowy klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="54995-141">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="54995-142">Aby uzyskać więcej informacji, zobacz [Pobieranie metadanych umów dla umowy klienta firmy Microsoft](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="54995-142">For more details, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

2. <span data-ttu-id="54995-143">Utwórz nowy zasób [ **umowy**](agreement-resources.md) , aby potwierdzić, że klient zaakceptował umowę klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="54995-143">Create a new [**Agreement** resource](agreement-resources.md) to confirm that a customer has accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="54995-144">Użyj następującej [składni żądania REST](#request-syntax).</span><span class="sxs-lookup"><span data-stu-id="54995-144">Use the following [REST request syntax](#request-syntax).</span></span>

### <a name="request-syntax"></a><span data-ttu-id="54995-145">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="54995-145">Request syntax</span></span>

| <span data-ttu-id="54995-146">Metoda</span><span class="sxs-lookup"><span data-stu-id="54995-146">Method</span></span> | <span data-ttu-id="54995-147">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="54995-147">Request URI</span></span>                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="54995-148">POST</span><span class="sxs-lookup"><span data-stu-id="54995-148">POST</span></span>   | <span data-ttu-id="54995-149">[*\{ BASEURL \}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Agreements http/1.1</span><span class="sxs-lookup"><span data-stu-id="54995-149">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="54995-150">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="54995-150">URI parameter</span></span>

<span data-ttu-id="54995-151">Użyj następującego parametru zapytania, aby określić klienta, który potwierdzasz.</span><span class="sxs-lookup"><span data-stu-id="54995-151">Use the following query parameter to specify the customer that you're confirming.</span></span>

| <span data-ttu-id="54995-152">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54995-152">Name</span></span>               | <span data-ttu-id="54995-153">Typ</span><span class="sxs-lookup"><span data-stu-id="54995-153">Type</span></span> | <span data-ttu-id="54995-154">Wymagane</span><span class="sxs-lookup"><span data-stu-id="54995-154">Required</span></span> | <span data-ttu-id="54995-155">Opis</span><span class="sxs-lookup"><span data-stu-id="54995-155">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="54995-156">Identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="54995-156">customer-tenant-id</span></span> | <span data-ttu-id="54995-157">GUID</span><span class="sxs-lookup"><span data-stu-id="54995-157">GUID</span></span> | <span data-ttu-id="54995-158">Tak</span><span class="sxs-lookup"><span data-stu-id="54995-158">Yes</span></span> | <span data-ttu-id="54995-159">Wartość jest identyfikatorem GUID, który jest sformatowanym identyfikatorem **dzierżawy**, który umożliwia określenie klienta.</span><span class="sxs-lookup"><span data-stu-id="54995-159">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="54995-160">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="54995-160">Request headers</span></span>

<span data-ttu-id="54995-161">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="54995-161">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="54995-162">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="54995-162">Request body</span></span>

<span data-ttu-id="54995-163">W tej tabeli opisano wymagane właściwości w treści żądania REST.</span><span class="sxs-lookup"><span data-stu-id="54995-163">This table describes the required properties in the REST request body.</span></span>

| <span data-ttu-id="54995-164">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54995-164">Name</span></span>      | <span data-ttu-id="54995-165">Typ</span><span class="sxs-lookup"><span data-stu-id="54995-165">Type</span></span>   | <span data-ttu-id="54995-166">Opis</span><span class="sxs-lookup"><span data-stu-id="54995-166">Description</span></span>                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="54995-167">Umowa</span><span class="sxs-lookup"><span data-stu-id="54995-167">Agreement</span></span> | <span data-ttu-id="54995-168">object</span><span class="sxs-lookup"><span data-stu-id="54995-168">object</span></span> | <span data-ttu-id="54995-169">Szczegóły dostarczone przez partnera w celu potwierdzenia akceptacji umowy klienta firmy Microsoft przez klienta.</span><span class="sxs-lookup"><span data-stu-id="54995-169">Details provided by partner to confirm customer acceptance of the Microsoft Customer Agreement.</span></span> |

#### <a name="agreement"></a><span data-ttu-id="54995-170">Umowa</span><span class="sxs-lookup"><span data-stu-id="54995-170">Agreement</span></span>

<span data-ttu-id="54995-171">Ta tabela zawiera opis minimalnych wymaganych pól w celu utworzenia [zasobu **umowy**](agreement-resources.md).</span><span class="sxs-lookup"><span data-stu-id="54995-171">This table describes the minimum required fields to create an [**Agreement** resource](agreement-resources.md).</span></span>

| <span data-ttu-id="54995-172">Właściwość</span><span class="sxs-lookup"><span data-stu-id="54995-172">Property</span></span>       | <span data-ttu-id="54995-173">Typ</span><span class="sxs-lookup"><span data-stu-id="54995-173">Type</span></span>   | <span data-ttu-id="54995-174">Opis</span><span class="sxs-lookup"><span data-stu-id="54995-174">Description</span></span>                              |
|----------------|--------|------------------------------------------|
| <span data-ttu-id="54995-175">primaryContact</span><span class="sxs-lookup"><span data-stu-id="54995-175">primaryContact</span></span> | [<span data-ttu-id="54995-176">Kontakt</span><span class="sxs-lookup"><span data-stu-id="54995-176">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="54995-177">Informacje o użytkowniku z organizacji klienta, którzy zaakceptowali umowę klienta firmy Microsoft, w tym:  **FirstName**, **LastName**, **email** i numer **telefonu** (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="54995-177">Information about the user from the customer organization who accepted the Microsoft Customer Agreement, including:  **firstName**, **lastName**, **email** and **phoneNumber** (optional)</span></span> |
| <span data-ttu-id="54995-178">dateAgreed</span><span class="sxs-lookup"><span data-stu-id="54995-178">dateAgreed</span></span>     | <span data-ttu-id="54995-179">ciąg w formacie daty i godziny czasu UTC</span><span class="sxs-lookup"><span data-stu-id="54995-179">string in UTC date time format</span></span> |<span data-ttu-id="54995-180">Data zaakceptowania umowy przez klienta.</span><span class="sxs-lookup"><span data-stu-id="54995-180">The date when the customer accepted the agreement.</span></span> |
| <span data-ttu-id="54995-181">templateId</span><span class="sxs-lookup"><span data-stu-id="54995-181">templateId</span></span>     | <span data-ttu-id="54995-182">ciąg</span><span class="sxs-lookup"><span data-stu-id="54995-182">string</span></span> | <span data-ttu-id="54995-183">Unikatowy identyfikator typu umowy akceptowany przez klienta.</span><span class="sxs-lookup"><span data-stu-id="54995-183">Unique identifier of the agreement type accepted by the customer.</span></span> <span data-ttu-id="54995-184">Możesz uzyskać **templateId** dla umowy klienta Microsoft, pobierając metadane umowy dla umowy klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="54995-184">You can obtain the **templateId** for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement.</span></span> <span data-ttu-id="54995-185">Aby uzyskać szczegółowe informacje, zobacz artykuł [Pobierz metadane umowy dla umowy klienta firmy Microsoft](./get-customer-agreement-metadata.md) .</span><span class="sxs-lookup"><span data-stu-id="54995-185">See [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md) for details.</span></span> |
| <span data-ttu-id="54995-186">typ</span><span class="sxs-lookup"><span data-stu-id="54995-186">type</span></span>           | <span data-ttu-id="54995-187">ciąg</span><span class="sxs-lookup"><span data-stu-id="54995-187">string</span></span> | <span data-ttu-id="54995-188">Typ umowy akceptowany przez klienta.</span><span class="sxs-lookup"><span data-stu-id="54995-188">Agreement type accepted by the customer.</span></span> <span data-ttu-id="54995-189">Jeśli klient zaakceptuje umowę klienta firmy Microsoft, należy użyć "MicrosoftCustomerAgreement".</span><span class="sxs-lookup"><span data-stu-id="54995-189">Use "MicrosoftCustomerAgreement" if customer accepted the Microsoft Customer Agreement.</span></span> |

#### <a name="request-example"></a><span data-ttu-id="54995-190">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="54995-190">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="54995-191">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="54995-191">REST response</span></span>

<span data-ttu-id="54995-192">Jeśli to się powiedzie, metoda zwraca [zasób **umowy**](./agreement-resources.md).</span><span class="sxs-lookup"><span data-stu-id="54995-192">If successful, this method returns an [**Agreement** resource](./agreement-resources.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="54995-193">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="54995-193">Response success and error codes</span></span>

<span data-ttu-id="54995-194">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="54995-194">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="54995-195">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="54995-195">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="54995-196">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="54995-196">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="54995-197">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="54995-197">Response example</span></span>

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
