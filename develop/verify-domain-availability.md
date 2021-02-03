---
title: Sprawdzanie dostępności domeny
description: Jak ustalić, czy domena jest dostępna do użycia.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 84edb5b7510642ec44dad3d4f92349e40eb10b24
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768278"
---
# <a name="verify-domain-availability"></a><span data-ttu-id="fb536-103">Sprawdzanie dostępności domeny</span><span class="sxs-lookup"><span data-stu-id="fb536-103">Verify domain availability</span></span>

<span data-ttu-id="fb536-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="fb536-104">**Applies To**</span></span>

- <span data-ttu-id="fb536-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="fb536-105">Partner Center</span></span>
- <span data-ttu-id="fb536-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="fb536-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="fb536-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="fb536-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="fb536-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="fb536-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="fb536-109">Jak ustalić, czy domena jest dostępna do użycia.</span><span class="sxs-lookup"><span data-stu-id="fb536-109">How to determine if a domain is available for use.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb536-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fb536-110">Prerequisites</span></span>

- <span data-ttu-id="fb536-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fb536-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fb536-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fb536-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fb536-113">Domena (na przykład `contoso.onmicrosoft.com` ).</span><span class="sxs-lookup"><span data-stu-id="fb536-113">A domain (for example `contoso.onmicrosoft.com`).</span></span>

## <a name="c"></a><span data-ttu-id="fb536-114">C\#</span><span class="sxs-lookup"><span data-stu-id="fb536-114">C\#</span></span>

<span data-ttu-id="fb536-115">Aby sprawdzić, czy domena jest dostępna, najpierw Wywołaj [**IAggregatePartner. domen**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) , aby uzyskać interfejs do operacji na domenie.</span><span class="sxs-lookup"><span data-stu-id="fb536-115">To verify if a domain is available, first call [**IAggregatePartner.Domains**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) to obtain an interface to domain operations.</span></span> <span data-ttu-id="fb536-116">Następnie Wywołaj metodę [**ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) z domeną, aby sprawdzić.</span><span class="sxs-lookup"><span data-stu-id="fb536-116">Then call the [**ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) method with the domain to check.</span></span> <span data-ttu-id="fb536-117">Ta metoda pobiera interfejs do operacji dostępnych dla określonej domeny.</span><span class="sxs-lookup"><span data-stu-id="fb536-117">This method retrieves an interface to the operations available for a specific domain.</span></span> <span data-ttu-id="fb536-118">Na koniec Wywołaj metodę [**EXISTS**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) , aby sprawdzić, czy domena już istnieje.</span><span class="sxs-lookup"><span data-stu-id="fb536-118">Finally, call the [**Exists**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) method to see if the domain already exists.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

<span data-ttu-id="fb536-119">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="fb536-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="fb536-120">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: CheckDomainAvailability.cs</span><span class="sxs-lookup"><span data-stu-id="fb536-120">**Project**: Partner Center SDK Samples **Class**: CheckDomainAvailability.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="fb536-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="fb536-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fb536-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="fb536-122">Request syntax</span></span>

| <span data-ttu-id="fb536-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="fb536-123">Method</span></span>   | <span data-ttu-id="fb536-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="fb536-124">Request URI</span></span>                                                              |
|----------|--------------------------------------------------------------------------|
| <span data-ttu-id="fb536-125">**MTP**</span><span class="sxs-lookup"><span data-stu-id="fb536-125">**HEAD**</span></span> | <span data-ttu-id="fb536-126">[*{baseURL}*](partner-center-rest-urls.md)/V1/Domains/{Domain} http/1.1</span><span class="sxs-lookup"><span data-stu-id="fb536-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domain} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="fb536-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="fb536-127">URI parameter</span></span>

<span data-ttu-id="fb536-128">Użyj następującego parametru zapytania, aby sprawdzić dostępność domeny.</span><span class="sxs-lookup"><span data-stu-id="fb536-128">Use the following query parameter to verify domain availability.</span></span>

| <span data-ttu-id="fb536-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fb536-129">Name</span></span>       | <span data-ttu-id="fb536-130">Typ</span><span class="sxs-lookup"><span data-stu-id="fb536-130">Type</span></span>       | <span data-ttu-id="fb536-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fb536-131">Required</span></span> | <span data-ttu-id="fb536-132">Opis</span><span class="sxs-lookup"><span data-stu-id="fb536-132">Description</span></span>                                   |
|------------|------------|----------|-----------------------------------------------|
| <span data-ttu-id="fb536-133">**domeny**</span><span class="sxs-lookup"><span data-stu-id="fb536-133">**domain**</span></span> | <span data-ttu-id="fb536-134">**parametry**</span><span class="sxs-lookup"><span data-stu-id="fb536-134">**string**</span></span> | <span data-ttu-id="fb536-135">Y</span><span class="sxs-lookup"><span data-stu-id="fb536-135">Y</span></span>        | <span data-ttu-id="fb536-136">Ciąg, który identyfikuje domenę do sprawdzenia.</span><span class="sxs-lookup"><span data-stu-id="fb536-136">A string that identifies the domain to check.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fb536-137">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="fb536-137">Request headers</span></span>

<span data-ttu-id="fb536-138">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fb536-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fb536-139">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="fb536-139">Request body</span></span>

<span data-ttu-id="fb536-140">Brak</span><span class="sxs-lookup"><span data-stu-id="fb536-140">None</span></span>

### <a name="request-example"></a><span data-ttu-id="fb536-141">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="fb536-141">Request example</span></span>

```http
HEAD https://api.partnercenter.microsoft.com/v1/domains/contoso.onmicrosoft.com HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="fb536-142">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="fb536-142">REST response</span></span>

<span data-ttu-id="fb536-143">Jeśli domena istnieje, nie jest dostępna do użycia i zwracany jest kod stanu odpowiedzi 200 OK.</span><span class="sxs-lookup"><span data-stu-id="fb536-143">If the domain exists, it isn't available for use and a response status code 200 OK is returned.</span></span> <span data-ttu-id="fb536-144">Jeśli domena nie zostanie znaleziona, jest ona dostępna do użycia i zwracany jest kod stanu odpowiedzi 404.</span><span class="sxs-lookup"><span data-stu-id="fb536-144">If the domain isn't found, it's available for use and a response status code 404 Not Found is returned.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fb536-145">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fb536-145">Response success and error codes</span></span>

<span data-ttu-id="fb536-146">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="fb536-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fb536-147">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="fb536-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fb536-148">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fb536-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-for-when-the-domain-is-already-in-use"></a><span data-ttu-id="fb536-149">Przykład odpowiedzi dla sytuacji, gdy domena jest już używana</span><span class="sxs-lookup"><span data-stu-id="fb536-149">Response example for when the domain is already in use</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a><span data-ttu-id="fb536-150">Przykład odpowiedzi dla momentu dostępności domeny</span><span class="sxs-lookup"><span data-stu-id="fb536-150">Response example for when the domain is available</span></span>

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
