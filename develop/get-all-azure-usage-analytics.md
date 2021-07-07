---
title: Pobieranie wszystkich informacji analitycznych dotyczących użycia platformy Azure
description: Jak uzyskać wszystkie informacje dotyczące analizy użycia platformy Azure.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 7fe987c7dc50d55b26cd72d5aead52963eb1cfbe
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760219"
---
# <a name="get-all-azure-usage-analytics-information"></a><span data-ttu-id="02c2a-103">Pobieranie wszystkich informacji analitycznych dotyczących użycia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="02c2a-103">Get all Azure usage analytics information</span></span>

<span data-ttu-id="02c2a-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="02c2a-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="02c2a-105">Jak uzyskać wszystkie informacje dotyczące analizy użycia platformy Azure dla klientów.</span><span class="sxs-lookup"><span data-stu-id="02c2a-105">How to get all the Azure usage analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02c2a-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="02c2a-106">Prerequisites</span></span>

- <span data-ttu-id="02c2a-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="02c2a-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="02c2a-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="02c2a-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="02c2a-109">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="02c2a-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="02c2a-110">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="02c2a-110">Request syntax</span></span>

| <span data-ttu-id="02c2a-111">Metoda</span><span class="sxs-lookup"><span data-stu-id="02c2a-111">Method</span></span>  | <span data-ttu-id="02c2a-112">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="02c2a-112">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="02c2a-113">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="02c2a-113">**GET**</span></span> | <span data-ttu-id="02c2a-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="02c2a-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="02c2a-115">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="02c2a-115">URI parameters</span></span>

|<span data-ttu-id="02c2a-116">Parametr</span><span class="sxs-lookup"><span data-stu-id="02c2a-116">Parameter</span></span>        |<span data-ttu-id="02c2a-117">Typ</span><span class="sxs-lookup"><span data-stu-id="02c2a-117">Type</span></span>                        |<span data-ttu-id="02c2a-118">Opis</span><span class="sxs-lookup"><span data-stu-id="02c2a-118">Description</span></span>               |
|:----------------|:---------------------------|:-------------------------|
|<span data-ttu-id="02c2a-119">top (pierwsze)</span><span class="sxs-lookup"><span data-stu-id="02c2a-119">top</span></span>              | <span data-ttu-id="02c2a-120">ciąg</span><span class="sxs-lookup"><span data-stu-id="02c2a-120">string</span></span>                     | <span data-ttu-id="02c2a-121">Liczba wierszy danych do zwrócenia w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="02c2a-121">The number of rows of data to return in the request.</span></span> <span data-ttu-id="02c2a-122">Wartość maksymalna i wartość domyślna, jeśli nie zostanie określona, to 10000.</span><span class="sxs-lookup"><span data-stu-id="02c2a-122">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="02c2a-123">Jeśli w zapytaniu znajduje się więcej wierszy, treść odpowiedzi zawiera następny link, za pomocą których można zażądać następnej strony danych.</span><span class="sxs-lookup"><span data-stu-id="02c2a-123">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span>                        |
|<span data-ttu-id="02c2a-124">Pomiń</span><span class="sxs-lookup"><span data-stu-id="02c2a-124">skip</span></span>             | <span data-ttu-id="02c2a-125">int</span><span class="sxs-lookup"><span data-stu-id="02c2a-125">int</span></span>                        | <span data-ttu-id="02c2a-126">Liczba wierszy do pominięcia w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="02c2a-126">The number of rows to skip in the query.</span></span> <span data-ttu-id="02c2a-127">Ten parametr umożliwia stronicować duże zestawy danych.</span><span class="sxs-lookup"><span data-stu-id="02c2a-127">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="02c2a-128">Na przykład `top=10000 and skip=0` program pobiera pierwsze 10 000 wierszy danych, pobiera kolejne `top=10000 and skip=10000` 10000 wierszy danych i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="02c2a-128">For example, `top=10000 and skip=0` retrieves the first 10000 rows of data, `top=10000 and skip=10000` retrieves the next 10000 rows of data, and so on.</span></span>                       |
|<span data-ttu-id="02c2a-129">filter</span><span class="sxs-lookup"><span data-stu-id="02c2a-129">filter</span></span>           | <span data-ttu-id="02c2a-130">ciąg</span><span class="sxs-lookup"><span data-stu-id="02c2a-130">string</span></span>                     | <span data-ttu-id="02c2a-131">Parametr *filtru* żądania zawiera co najmniej jedną instrukcje, które filtruje wiersze w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="02c2a-131">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="02c2a-132">Każda instrukcja zawiera pole i wartość, które są skojarzone z operatorami lub , a instrukcje można łączyć przy `eq` `ne` użyciu instrukcji lub `and` `or` .</span><span class="sxs-lookup"><span data-stu-id="02c2a-132">Each statement contains a field and value that are associated with the `eq` or `ne` operators, and statements can be combined using `and` or `or`.</span></span> <span data-ttu-id="02c2a-133">Można określić następujące ciągi:</span><span class="sxs-lookup"><span data-stu-id="02c2a-133">You can specify the following strings:</span></span><br/><br/>                                                       `customerTenantId`<br/> `customerName`<br/> `subscriptionId`<br/> `subscriptionName`<br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/><span data-ttu-id="02c2a-134">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="02c2a-134">**Example:**</span></span><br/> `.../usage/azure?filter=meterCategory eq 'Data Management'`<br/><br/> <span data-ttu-id="02c2a-135">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="02c2a-135">**Example:**</span></span><br/>`.../usage/azure?filter=meterCategory eq 'Data Management' or (usageDate le cast('2018-01-01', Edm.DateTimeOffset) and usageDate le cast('2018-04-01', Edm.DateTimeOffset))`                        |
|<span data-ttu-id="02c2a-136">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="02c2a-136">aggregationLevel</span></span> | <span data-ttu-id="02c2a-137">ciąg</span><span class="sxs-lookup"><span data-stu-id="02c2a-137">string</span></span>                    | <span data-ttu-id="02c2a-138">Określa zakres czasu, dla którego mają zostać pobrane zagregowane dane.</span><span class="sxs-lookup"><span data-stu-id="02c2a-138">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="02c2a-139">Może być jednym z następujących ciągów: `day` `week` , lub `month` .</span><span class="sxs-lookup"><span data-stu-id="02c2a-139">Can be one of the following strings: `day`, `week`, or `month`.</span></span> <span data-ttu-id="02c2a-140">Jeśli nie zostanie on nieokreślony, wartość domyślna to `day` .</span><span class="sxs-lookup"><span data-stu-id="02c2a-140">If unspecified, the default is `day`.</span></span><br/><br/>                                              <span data-ttu-id="02c2a-141">Parametr `aggregationLevel` nie jest obsługiwany bez parametru `groupby` .</span><span class="sxs-lookup"><span data-stu-id="02c2a-141">The `aggregationLevel` parameter isn't supported without a `groupby`.</span></span> <span data-ttu-id="02c2a-142">Parametr `aggregationLevel` ma zastosowanie do wszystkich pól dat obecnych w tabeli `groupby` .</span><span class="sxs-lookup"><span data-stu-id="02c2a-142">The `aggregationLevel` parameter applies to all date fields present in the `groupby`.</span></span>                                                      |
|<span data-ttu-id="02c2a-143">Orderby</span><span class="sxs-lookup"><span data-stu-id="02c2a-143">orderby</span></span>          |<span data-ttu-id="02c2a-144">ciąg</span><span class="sxs-lookup"><span data-stu-id="02c2a-144">string</span></span>                     | <span data-ttu-id="02c2a-145">Instrukcja, która nakazuje wartości danych wynikowych dla każdej instalacji.</span><span class="sxs-lookup"><span data-stu-id="02c2a-145">A statement that orders the result data values for each install.</span></span> <span data-ttu-id="02c2a-146">Składnia jest następująca: `...&orderby=field [order],field [order],...`</span><span class="sxs-lookup"><span data-stu-id="02c2a-146">The syntax is `...&orderby=field [order],field [order],...`.</span></span> <span data-ttu-id="02c2a-147">Parametr `field` może być jednym z następujących ciągów:</span><span class="sxs-lookup"><span data-stu-id="02c2a-147">The `field` parameter can be one of the following strings:</span></span><br/><br/>                    `customerTenantId`<br/>`customerName`<br/>`subscriptionId`<br/>`subscriptionName`<br/>`usageDate`<br/>`resourceLocation`<br/>`meterCategory`<br/>`meterSubcategory`<br/>`meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/> <span data-ttu-id="02c2a-148">Parametr *order* jest opcjonalny i może mieć wartość lub , aby określić kolejność rosnącą lub malejącą odpowiednio dla `asc` każdego `desc` pola.</span><span class="sxs-lookup"><span data-stu-id="02c2a-148">The *order* parameter is optional and can be `asc` or `desc` to specify ascending or descending order for each field, respectively.</span></span> <span data-ttu-id="02c2a-149">Wartość domyślna to `asc`.</span><span class="sxs-lookup"><span data-stu-id="02c2a-149">The default is `asc`.</span></span><br/><br/><span data-ttu-id="02c2a-150">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="02c2a-150">**Example:**</span></span><br/> `...&orderby=meterCategory,meterUnit`                                                                                           |
|<span data-ttu-id="02c2a-151">Groupby</span><span class="sxs-lookup"><span data-stu-id="02c2a-151">groupby</span></span>          |<span data-ttu-id="02c2a-152">ciąg</span><span class="sxs-lookup"><span data-stu-id="02c2a-152">string</span></span>                    | <span data-ttu-id="02c2a-153">Instrukcja, która stosuje agregację danych tylko do określonych pól.</span><span class="sxs-lookup"><span data-stu-id="02c2a-153">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="02c2a-154">Można określić następujące pola:</span><span class="sxs-lookup"><span data-stu-id="02c2a-154">You can specify the following fields:</span></span><br/><br/>                                                                                                                     `customerTenantId`<br/>`customerName`<br/> `subscriptionId` <br/> `subscriptionName` <br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit` <br/> `reservationOrderId` <br/> `reservationId` <br/> `consumptionMeterId` <br/> `serviceType` <br/><br/><span data-ttu-id="02c2a-155">Zwracane wiersze danych będą zawierać pola określone w `groupby`  parametrze i *wartości Quantity*.</span><span class="sxs-lookup"><span data-stu-id="02c2a-155">The returned data rows will contain the fields specified in the `groupby`  parameter and the *Quantity*.</span></span><br/><br/><span data-ttu-id="02c2a-156">Parametru `groupby` można używać z `aggregationLevel` parametrem .</span><span class="sxs-lookup"><span data-stu-id="02c2a-156">The `groupby` parameter can be used with the `aggregationLevel` parameter.</span></span><br/><br/><span data-ttu-id="02c2a-157">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="02c2a-157">**Example:**</span></span><br/>`...&groupby=meterCategory,meterUnit` |

### <a name="request-headers"></a><span data-ttu-id="02c2a-158">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="02c2a-158">Request headers</span></span>

<span data-ttu-id="02c2a-159">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="02c2a-159">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="02c2a-160">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="02c2a-160">Request body</span></span>

<span data-ttu-id="02c2a-161">Brak.</span><span class="sxs-lookup"><span data-stu-id="02c2a-161">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="02c2a-162">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="02c2a-162">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="02c2a-163">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="02c2a-163">REST response</span></span>

<span data-ttu-id="02c2a-164">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [użycia platformy Azure.](partner-center-analytics-resources.md#csp-program-azure-usage-analytics)</span><span class="sxs-lookup"><span data-stu-id="02c2a-164">If successful, the response body contains a collection of [Azure usage](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="02c2a-165">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="02c2a-165">Response success and error codes</span></span>

<span data-ttu-id="02c2a-166">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="02c2a-166">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="02c2a-167">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="02c2a-167">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="02c2a-168">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="02c2a-168">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="02c2a-169">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="02c2a-169">Response example</span></span>

```http
{
  "customerTenantId": "39A1DFAC-4969-4F31-AF94-D76588189CFE",
  "customerName": "A",
  "subscriptionId": "EC649980-D623-49F5-B7C1-80CC772B83A8",
  "subscriptionName": "AZURE PURCHSE SAMPLE APP",
  "usageDate": "2018-05-27T00:00:00",
  "resourceLocation": "useast",
  "meterCategory": "Data Management",
  "meterSubcategory": "None",
  "meterUnit": "10,000s",
  "reservationOrderId": "",
  "reservationId": "",
  "consumptionMeterId": "",
  "serviceType": "",
  "quantity": 20
}
```

## <a name="see-also"></a><span data-ttu-id="02c2a-170">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="02c2a-170">See also</span></span>

- [<span data-ttu-id="02c2a-171">Analiza Centrum partnerskiego — zasoby</span><span class="sxs-lookup"><span data-stu-id="02c2a-171">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
