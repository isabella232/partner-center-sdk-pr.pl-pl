---
title: Sprawdzanie dostępności domeny
description: Jak określić, czy domena jest dostępna do użycia.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e2b8f0438516cc0aff9c4d8159c22de43ec582e4
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530280"
---
# <a name="verify-domain-availability"></a><span data-ttu-id="9ad51-103">Sprawdzanie dostępności domeny</span><span class="sxs-lookup"><span data-stu-id="9ad51-103">Verify domain availability</span></span>

<span data-ttu-id="9ad51-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9ad51-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9ad51-105">Jak określić, czy domena jest dostępna do użycia.</span><span class="sxs-lookup"><span data-stu-id="9ad51-105">How to determine if a domain is available for use.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ad51-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9ad51-106">Prerequisites</span></span>

- <span data-ttu-id="9ad51-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9ad51-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9ad51-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9ad51-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9ad51-109">Domena (na przykład `contoso.onmicrosoft.com` ).</span><span class="sxs-lookup"><span data-stu-id="9ad51-109">A domain (for example `contoso.onmicrosoft.com`).</span></span>

## <a name="c"></a><span data-ttu-id="9ad51-110">C\#</span><span class="sxs-lookup"><span data-stu-id="9ad51-110">C\#</span></span>

<span data-ttu-id="9ad51-111">Aby sprawdzić, czy domena jest dostępna, najpierw wywołaj [**element IAggregatePartner.Domains,**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) aby uzyskać interfejs operacji domeny.</span><span class="sxs-lookup"><span data-stu-id="9ad51-111">To verify if a domain is available, first call [**IAggregatePartner.Domains**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) to obtain an interface to domain operations.</span></span> <span data-ttu-id="9ad51-112">Następnie wywołaj [**metodę ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) z domeną, aby to sprawdzić.</span><span class="sxs-lookup"><span data-stu-id="9ad51-112">Then call the [**ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) method with the domain to check.</span></span> <span data-ttu-id="9ad51-113">Ta metoda pobiera interfejs do operacji dostępnych dla określonej domeny.</span><span class="sxs-lookup"><span data-stu-id="9ad51-113">This method retrieves an interface to the operations available for a specific domain.</span></span> <span data-ttu-id="9ad51-114">Na koniec wywołaj [**metodę Exists,**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) aby sprawdzić, czy domena już istnieje.</span><span class="sxs-lookup"><span data-stu-id="9ad51-114">Finally, call the [**Exists**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) method to see if the domain already exists.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

<span data-ttu-id="9ad51-115">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9ad51-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9ad51-116">**Project:** zestaw SDK Centrum partnerskiego Samples Class : CheckDomainAvailability.cs **(Klasa** przykładów zestaw SDK Centrum partnerskiego: CheckDomainAvailability.cs)</span><span class="sxs-lookup"><span data-stu-id="9ad51-116">**Project**: Partner Center SDK Samples **Class**: CheckDomainAvailability.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9ad51-117">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="9ad51-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9ad51-118">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="9ad51-118">Request syntax</span></span>

| <span data-ttu-id="9ad51-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="9ad51-119">Method</span></span>   | <span data-ttu-id="9ad51-120">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="9ad51-120">Request URI</span></span>                                                              |
|----------|--------------------------------------------------------------------------|
| <span data-ttu-id="9ad51-121">**Głowy**</span><span class="sxs-lookup"><span data-stu-id="9ad51-121">**HEAD**</span></span> | <span data-ttu-id="9ad51-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domena} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9ad51-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domain} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9ad51-123">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="9ad51-123">URI parameter</span></span>

<span data-ttu-id="9ad51-124">Użyj następującego parametru zapytania, aby zweryfikować dostępność domeny.</span><span class="sxs-lookup"><span data-stu-id="9ad51-124">Use the following query parameter to verify domain availability.</span></span>

| <span data-ttu-id="9ad51-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9ad51-125">Name</span></span>       | <span data-ttu-id="9ad51-126">Typ</span><span class="sxs-lookup"><span data-stu-id="9ad51-126">Type</span></span>       | <span data-ttu-id="9ad51-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9ad51-127">Required</span></span> | <span data-ttu-id="9ad51-128">Opis</span><span class="sxs-lookup"><span data-stu-id="9ad51-128">Description</span></span>                                   |
|------------|------------|----------|-----------------------------------------------|
| <span data-ttu-id="9ad51-129">**Domeny**</span><span class="sxs-lookup"><span data-stu-id="9ad51-129">**domain**</span></span> | <span data-ttu-id="9ad51-130">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="9ad51-130">**string**</span></span> | <span data-ttu-id="9ad51-131">Y</span><span class="sxs-lookup"><span data-stu-id="9ad51-131">Y</span></span>        | <span data-ttu-id="9ad51-132">Ciąg, który identyfikuje domenę do sprawdzenia.</span><span class="sxs-lookup"><span data-stu-id="9ad51-132">A string that identifies the domain to check.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9ad51-133">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="9ad51-133">Request headers</span></span>

<span data-ttu-id="9ad51-134">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="9ad51-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9ad51-135">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="9ad51-135">Request body</span></span>

<span data-ttu-id="9ad51-136">Brak</span><span class="sxs-lookup"><span data-stu-id="9ad51-136">None</span></span>

### <a name="request-example"></a><span data-ttu-id="9ad51-137">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="9ad51-137">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="9ad51-138">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="9ad51-138">REST response</span></span>

<span data-ttu-id="9ad51-139">Jeśli domena istnieje, nie jest dostępna do użycia i zwracany jest kod stanu odpowiedzi 200 OK.</span><span class="sxs-lookup"><span data-stu-id="9ad51-139">If the domain exists, it isn't available for use and a response status code 200 OK is returned.</span></span> <span data-ttu-id="9ad51-140">Jeśli domena nie zostanie znaleziona, jest dostępna do użycia i zwracany jest kod stanu odpowiedzi 404 Nie znaleziono.</span><span class="sxs-lookup"><span data-stu-id="9ad51-140">If the domain isn't found, it's available for use and a response status code 404 Not Found is returned.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9ad51-141">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9ad51-141">Response success and error codes</span></span>

<span data-ttu-id="9ad51-142">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="9ad51-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9ad51-143">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="9ad51-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9ad51-144">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="9ad51-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-for-when-the-domain-is-already-in-use"></a><span data-ttu-id="9ad51-145">Przykład odpowiedzi dla sytuacji, gdy domena jest już w użyciu</span><span class="sxs-lookup"><span data-stu-id="9ad51-145">Response example for when the domain is already in use</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a><span data-ttu-id="9ad51-146">Przykład odpowiedzi dotyczącej tego, kiedy domena jest dostępna</span><span class="sxs-lookup"><span data-stu-id="9ad51-146">Response example for when the domain is available</span></span>

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
