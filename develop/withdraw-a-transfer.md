---
title: Chylić transfer
description: Jak odtworzyć utworzony transfer subskrypcji dla klienta.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3c15cf09b4e466e178c7afb5f9d324fe1199418e
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445208"
---
# <a name="withdraw-a-transfer"></a><span data-ttu-id="704fe-103">Chylić transfer</span><span class="sxs-lookup"><span data-stu-id="704fe-103">Withdraw a transfer</span></span>

## <a name="prerequisites"></a><span data-ttu-id="704fe-104">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="704fe-104">Prerequisites</span></span>

- <span data-ttu-id="704fe-105">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="704fe-105">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="704fe-106">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="704fe-106">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="704fe-107">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="704fe-107">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="704fe-108">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="704fe-108">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="704fe-109">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="704fe-109">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="704fe-110">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="704fe-110">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="704fe-111">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="704fe-111">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="704fe-112">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="704fe-112">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="704fe-113">Identyfikator transferu dla istniejącego transferu.</span><span class="sxs-lookup"><span data-stu-id="704fe-113">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="704fe-114">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="704fe-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="704fe-115">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="704fe-115">Request syntax</span></span>

| <span data-ttu-id="704fe-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="704fe-116">Method</span></span>    | <span data-ttu-id="704fe-117">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="704fe-117">Request URI</span></span>                                                                                                 |
|-----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="704fe-118">**Usunąć**</span><span class="sxs-lookup"><span data-stu-id="704fe-118">**DELETE**</span></span>| <span data-ttu-id="704fe-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/transfers/{transfer-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="704fe-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>      |

### <a name="uri-parameter"></a><span data-ttu-id="704fe-120">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="704fe-120">URI parameter</span></span>

<span data-ttu-id="704fe-121">Użyj następującego parametru ścieżki, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="704fe-121">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="704fe-122">Nazwa</span><span class="sxs-lookup"><span data-stu-id="704fe-122">Name</span></span>            | <span data-ttu-id="704fe-123">Typ</span><span class="sxs-lookup"><span data-stu-id="704fe-123">Type</span></span>     | <span data-ttu-id="704fe-124">Wymagane</span><span class="sxs-lookup"><span data-stu-id="704fe-124">Required</span></span> | <span data-ttu-id="704fe-125">Opis</span><span class="sxs-lookup"><span data-stu-id="704fe-125">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="704fe-126">**identyfikator klienta**</span><span class="sxs-lookup"><span data-stu-id="704fe-126">**customer-id**</span></span> | <span data-ttu-id="704fe-127">ciąg</span><span class="sxs-lookup"><span data-stu-id="704fe-127">string</span></span>   | <span data-ttu-id="704fe-128">Tak</span><span class="sxs-lookup"><span data-stu-id="704fe-128">Yes</span></span>      | <span data-ttu-id="704fe-129">Identyfikator klienta sformatowany w formacie GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="704fe-129">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="704fe-130">**transfer-id**</span><span class="sxs-lookup"><span data-stu-id="704fe-130">**transfer-id**</span></span> | <span data-ttu-id="704fe-131">ciąg</span><span class="sxs-lookup"><span data-stu-id="704fe-131">string</span></span>   | <span data-ttu-id="704fe-132">Tak</span><span class="sxs-lookup"><span data-stu-id="704fe-132">Yes</span></span>      | <span data-ttu-id="704fe-133">Identyfikator GUID sformatowany transfer-id, który identyfikuje transfer.</span><span class="sxs-lookup"><span data-stu-id="704fe-133">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="704fe-134">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="704fe-134">Request headers</span></span>

<span data-ttu-id="704fe-135">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="704fe-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="704fe-136">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="704fe-136">Request example</span></span>

```http
DELETE /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
Connection: keep-alive
```

## <a name="rest-response"></a><span data-ttu-id="704fe-137">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="704fe-137">REST response</span></span>

<span data-ttu-id="704fe-138">W przypadku powodzenia ta metoda zwraca wartość No Content (204).</span><span class="sxs-lookup"><span data-stu-id="704fe-138">If successful, this method returns No Content (204).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="704fe-139">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="704fe-139">Response success and error codes</span></span>

<span data-ttu-id="704fe-140">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="704fe-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="704fe-141">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="704fe-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="704fe-142">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="704fe-142">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="704fe-143">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="704fe-143">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
Date: Tue, 24 Mar 2020 23:44:06 GMT
```
