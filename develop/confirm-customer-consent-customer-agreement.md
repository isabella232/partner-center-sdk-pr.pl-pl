---
title: Potwierdzenie akceptacji przez klienta umowy klienta firmy Microsoft
description: Dowiedz się, jak potwierdzić akceptację Umowa z Klientem Microsoft przy użyciu Partner Center API.
ms.date: 02/08/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 002508109191ede53cd06f25efc38286647fd67c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974016"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a><span data-ttu-id="19552-103">Potwierdzanie akceptacji przez klientów Umowa z Klientem Microsoft przy użyciu Partner Center API</span><span class="sxs-lookup"><span data-stu-id="19552-103">Confirm customer acceptance of the Microsoft Customer Agreement using Partner Center APIs</span></span>

<span data-ttu-id="19552-104">**Dotyczy:** Partner Center</span><span class="sxs-lookup"><span data-stu-id="19552-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="19552-105">**Nie dotyczy:** Partner Center obsługiwane przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="19552-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="19552-106">Partner Center obsługuje obecnie potwierdzenie akceptacji przez klienta Umowa z Klientem Microsoft tylko w chmurze publicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19552-106">Partner Center currently supports confirmation of customer acceptance of the Microsoft Customer Agreement only in the Microsoft public cloud.</span></span>

<span data-ttu-id="19552-107">W tym artykule opisano sposób potwierdzania lub ponownego potwierdzania akceptacji Umowa z Klientem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19552-107">This article describes how to confirm or reconfirm customer acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19552-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="19552-108">Prerequisites</span></span>

- <span data-ttu-id="19552-109">Jeśli używasz zestawu SDK platformy .NET Partner Center, wymagana jest wersja 1.14 lub nowsza.</span><span class="sxs-lookup"><span data-stu-id="19552-109">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="19552-110">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](./partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="19552-110">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="19552-111">*Ten scenariusz obsługuje tylko uwierzytelnianie App+Użytkownik.*</span><span class="sxs-lookup"><span data-stu-id="19552-111">*This scenario only supports App+User authentication.*</span></span>

- <span data-ttu-id="19552-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="19552-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="19552-113">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="19552-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="19552-114">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="19552-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="19552-115">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="19552-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="19552-116">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="19552-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="19552-117">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="19552-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="19552-118">Data **(dateAgreed),** kiedy klient zaakceptował Umowa z Klientem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19552-118">The date (**dateAgreed**) when the customer accepted the Microsoft Customer Agreement.</span></span>

- <span data-ttu-id="19552-119">Informacje o użytkowniku z organizacji klienta, który zaakceptował Umowa z Klientem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19552-119">Information about the user from the customer organization that accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="19552-120">Obejmuje to następujące działania:</span><span class="sxs-lookup"><span data-stu-id="19552-120">This includes:</span></span>
  - <span data-ttu-id="19552-121">Imię</span><span class="sxs-lookup"><span data-stu-id="19552-121">First name</span></span>
  - <span data-ttu-id="19552-122">Nazwisko</span><span class="sxs-lookup"><span data-stu-id="19552-122">Last name</span></span>
  - <span data-ttu-id="19552-123">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="19552-123">Email address</span></span>
  - <span data-ttu-id="19552-124">Telefon (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="19552-124">Phone number (optional)</span></span>
- <span data-ttu-id="19552-125">Jeśli dla klienta zmienią się następujące wartości, program Partner Center zezwoli na Partner Center utworzenia innej umowy dla tego klienta: Imię nazwisko Adres e-mail Telefon numer W przeciwnym razie partnerzy otrzymają następujący kod błędu z powodu utworzenia zduplikowanego klienta</span><span class="sxs-lookup"><span data-stu-id="19552-125">If the following values change for a customer, Partner Center  will allow for another agreement to be created for that customer:       First Name       Last Name       Email address       Phone number Otherwise partners will receive the following error code, due to a duplicate customer being created</span></span>


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

## <a name="net"></a><span data-ttu-id="19552-126">.NET</span><span class="sxs-lookup"><span data-stu-id="19552-126">.NET</span></span>

<span data-ttu-id="19552-127">Aby potwierdzić lub ponownie potwierdzić akceptację przez klienta Umowa z Klientem Microsoft:</span><span class="sxs-lookup"><span data-stu-id="19552-127">To confirm or reconfirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="19552-128">Pobierz metadane umowy dla Umowa z Klientem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19552-128">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="19552-129">Musisz uzyskać **szablon templateId** Umowa z Klientem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19552-129">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="19552-130">Aby uzyskać więcej informacji, zobacz [Get agreement metadata for Umowa z Klientem Microsoft](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="19552-130">For more information, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. <span data-ttu-id="19552-131">Utwórz nowy obiekt **Umowy** zawierający szczegóły potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="19552-131">Create a new **Agreement** object containing details of the confirmation.</span></span>

3. <span data-ttu-id="19552-132">Użyj **kolekcji IAgreggatePartner.Customers** i wywołaj metodę **ById** z określonym **identyfikatorem customer-tenant-id**.</span><span class="sxs-lookup"><span data-stu-id="19552-132">Use the **IAgreggatePartner.Customers** collection and call the **ById** method with the specified **customer-tenant-id**.</span></span>

4. <span data-ttu-id="19552-133">Użyj właściwości **Agreements,** a następnie wywołaj właściwość **Create** lub **CreateAsync.**</span><span class="sxs-lookup"><span data-stu-id="19552-133">Use the **Agreements** property, followed by calling **Create** or **CreateAsync**.</span></span>

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

<span data-ttu-id="19552-134">Pełny przykład można znaleźć w klasie [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) w projekcie [aplikacji testowej konsoli.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)</span><span class="sxs-lookup"><span data-stu-id="19552-134">A complete sample can be found in the [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="19552-135">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="19552-135">REST request</span></span>

<span data-ttu-id="19552-136">Aby potwierdzić lub ponownie potwierdzić akceptację przez klienta Umowa z Klientem Microsoft:</span><span class="sxs-lookup"><span data-stu-id="19552-136">To confirm or reconfirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="19552-137">Pobierz metadane umowy dla Umowa z Klientem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19552-137">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="19552-138">Musisz uzyskać **szablon templateId** Umowa z Klientem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19552-138">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="19552-139">Aby uzyskać więcej informacji, zobacz [Get agreement metadata for Umowa z Klientem Microsoft](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="19552-139">For more information, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

2. <span data-ttu-id="19552-140">Utwórz nowy [ **zasób umowy,**](agreement-resources.md) aby potwierdzić, że klient zaakceptował Umowa z Klientem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19552-140">Create a new [**Agreement** resource](agreement-resources.md) to confirm that a customer has accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="19552-141">Użyj następującej [składni żądania REST.](#request-syntax)</span><span class="sxs-lookup"><span data-stu-id="19552-141">Use the following [REST request syntax](#request-syntax).</span></span>

### <a name="request-syntax"></a><span data-ttu-id="19552-142">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="19552-142">Request syntax</span></span>

| <span data-ttu-id="19552-143">Metoda</span><span class="sxs-lookup"><span data-stu-id="19552-143">Method</span></span> | <span data-ttu-id="19552-144">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="19552-144">Request URI</span></span>                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="19552-145">POST</span><span class="sxs-lookup"><span data-stu-id="19552-145">POST</span></span>   | <span data-ttu-id="19552-146">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="19552-146">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="19552-147">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="19552-147">URI parameter</span></span>

<span data-ttu-id="19552-148">Użyj następującego parametru zapytania, aby określić klienta, który potwierdzasz.</span><span class="sxs-lookup"><span data-stu-id="19552-148">Use the following query parameter to specify the customer that you're confirming.</span></span>

| <span data-ttu-id="19552-149">Nazwa</span><span class="sxs-lookup"><span data-stu-id="19552-149">Name</span></span>               | <span data-ttu-id="19552-150">Typ</span><span class="sxs-lookup"><span data-stu-id="19552-150">Type</span></span> | <span data-ttu-id="19552-151">Wymagane</span><span class="sxs-lookup"><span data-stu-id="19552-151">Required</span></span> | <span data-ttu-id="19552-152">Opis</span><span class="sxs-lookup"><span data-stu-id="19552-152">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="19552-153">identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="19552-153">customer-tenant-id</span></span> | <span data-ttu-id="19552-154">GUID</span><span class="sxs-lookup"><span data-stu-id="19552-154">GUID</span></span> | <span data-ttu-id="19552-155">Tak</span><span class="sxs-lookup"><span data-stu-id="19552-155">Yes</span></span> | <span data-ttu-id="19552-156">Wartość jest identyfikatorem **customer-tenant-id** w formacie IDENTYFIKATORA GUID, który jest identyfikatorem umożliwiającym określenie klienta.</span><span class="sxs-lookup"><span data-stu-id="19552-156">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="19552-157">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="19552-157">Request headers</span></span>

<span data-ttu-id="19552-158">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="19552-158">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="19552-159">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="19552-159">Request body</span></span>

<span data-ttu-id="19552-160">W tej tabeli opisano wymagane właściwości w treści żądania REST.</span><span class="sxs-lookup"><span data-stu-id="19552-160">This table describes the required properties in the REST request body.</span></span>

| <span data-ttu-id="19552-161">Nazwa</span><span class="sxs-lookup"><span data-stu-id="19552-161">Name</span></span>      | <span data-ttu-id="19552-162">Typ</span><span class="sxs-lookup"><span data-stu-id="19552-162">Type</span></span>   | <span data-ttu-id="19552-163">Opis</span><span class="sxs-lookup"><span data-stu-id="19552-163">Description</span></span>                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="19552-164">Umowa</span><span class="sxs-lookup"><span data-stu-id="19552-164">Agreement</span></span> | <span data-ttu-id="19552-165">object</span><span class="sxs-lookup"><span data-stu-id="19552-165">object</span></span> | <span data-ttu-id="19552-166">Szczegółowe informacje udostępniane przez partnera w celu potwierdzenia akceptacji Umowa z Klientem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19552-166">Details provided by partner to confirm customer acceptance of the Microsoft Customer Agreement.</span></span> |

#### <a name="agreement"></a><span data-ttu-id="19552-167">Umowa</span><span class="sxs-lookup"><span data-stu-id="19552-167">Agreement</span></span>

<span data-ttu-id="19552-168">W tej tabeli opisano minimalne pola wymagane do utworzenia zasobu [ **umowy**](agreement-resources.md).</span><span class="sxs-lookup"><span data-stu-id="19552-168">This table describes the minimum required fields to create an [**Agreement** resource](agreement-resources.md).</span></span>

| <span data-ttu-id="19552-169">Właściwość</span><span class="sxs-lookup"><span data-stu-id="19552-169">Property</span></span>       | <span data-ttu-id="19552-170">Typ</span><span class="sxs-lookup"><span data-stu-id="19552-170">Type</span></span>   | <span data-ttu-id="19552-171">Opis</span><span class="sxs-lookup"><span data-stu-id="19552-171">Description</span></span>                              |
|----------------|--------|------------------------------------------|
| <span data-ttu-id="19552-172">primaryContact</span><span class="sxs-lookup"><span data-stu-id="19552-172">primaryContact</span></span> | [<span data-ttu-id="19552-173">Kontakt</span><span class="sxs-lookup"><span data-stu-id="19552-173">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="19552-174">Informacje o użytkowniku z organizacji klienta, który zaakceptował Umowa z Klientem Microsoft, w tym:  **firstName,** **lastName,** **email** i **phoneNumber** (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="19552-174">Information about the user from the customer organization who accepted the Microsoft Customer Agreement, including:  **firstName**, **lastName**, **email**, and **phoneNumber** (optional)</span></span> |
| <span data-ttu-id="19552-175">dateAgreed</span><span class="sxs-lookup"><span data-stu-id="19552-175">dateAgreed</span></span>     | <span data-ttu-id="19552-176">ciąg w formacie daty i godzin UTC</span><span class="sxs-lookup"><span data-stu-id="19552-176">string in UTC date time format</span></span> |<span data-ttu-id="19552-177">Data zaakceptowania umowy przez klienta.</span><span class="sxs-lookup"><span data-stu-id="19552-177">The date when the customer accepted the agreement.</span></span> |
| <span data-ttu-id="19552-178">templateId</span><span class="sxs-lookup"><span data-stu-id="19552-178">templateId</span></span>     | <span data-ttu-id="19552-179">ciąg</span><span class="sxs-lookup"><span data-stu-id="19552-179">string</span></span> | <span data-ttu-id="19552-180">Unikatowy identyfikator typu umowy zaakceptowany przez klienta.</span><span class="sxs-lookup"><span data-stu-id="19552-180">Unique identifier of the agreement type accepted by the customer.</span></span> <span data-ttu-id="19552-181">Możesz uzyskać szablon **templateId** dla Umowa z Klientem Microsoft, pobierania metadanych umowy dla Umowa z Klientem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19552-181">You can obtain the **templateId** for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement.</span></span> <span data-ttu-id="19552-182">Aby [uzyskać szczegółowe informacje, zobacz Umowa z Klientem Microsoft](./get-customer-agreement-metadata.md) Get agreement metadata for Umowa z Klientem Microsoft (Uzyskiwanie metadanych umowy).</span><span class="sxs-lookup"><span data-stu-id="19552-182">See [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md) for details.</span></span> |
| <span data-ttu-id="19552-183">typ</span><span class="sxs-lookup"><span data-stu-id="19552-183">type</span></span>           | <span data-ttu-id="19552-184">ciąg</span><span class="sxs-lookup"><span data-stu-id="19552-184">string</span></span> | <span data-ttu-id="19552-185">Typ umowy zaakceptowany przez klienta.</span><span class="sxs-lookup"><span data-stu-id="19552-185">Agreement type accepted by the customer.</span></span> <span data-ttu-id="19552-186">Użyj "MicrosoftCustomerAgreement", jeśli klient zaakceptował Umowa z Klientem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19552-186">Use "MicrosoftCustomerAgreement" if customer accepted the Microsoft Customer Agreement.</span></span> |

#### <a name="request-example"></a><span data-ttu-id="19552-187">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="19552-187">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="19552-188">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="19552-188">REST response</span></span>

<span data-ttu-id="19552-189">W przypadku powodzenia ta metoda zwraca [ **zasób umowy**](./agreement-resources.md).</span><span class="sxs-lookup"><span data-stu-id="19552-189">If successful, this method returns an [**Agreement** resource](./agreement-resources.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="19552-190">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="19552-190">Response success and error codes</span></span>

<span data-ttu-id="19552-191">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="19552-191">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="19552-192">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="19552-192">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="19552-193">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="19552-193">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="19552-194">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="19552-194">Response example</span></span>

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
