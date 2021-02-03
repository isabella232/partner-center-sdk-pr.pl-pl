---
title: Pobieranie rekordów dotyczących wykorzystania platformy Azure przez klienta
description: Korzystając z interfejsu API wykorzystania platformy Azure, można uzyskać rekordy wykorzystania subskrypcji platformy Azure klienta przez określony czas.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bcdeb51b04039fd05b923150c85119385c0537e0
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768102"
---
# <a name="get-a-customers-utilization-records-for-azure"></a><span data-ttu-id="747ad-103">Pobieranie rekordów dotyczących wykorzystania platformy Azure przez klienta</span><span class="sxs-lookup"><span data-stu-id="747ad-103">Get a customer's utilization records for Azure</span></span>

<span data-ttu-id="747ad-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="747ad-104">**Applies to:**</span></span>

- <span data-ttu-id="747ad-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="747ad-105">Partner Center</span></span>
- <span data-ttu-id="747ad-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="747ad-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="747ad-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="747ad-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="747ad-108">Możesz uzyskać rekordy wykorzystania subskrypcji platformy Azure klienta przez określony czas przy użyciu interfejsu API użycia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="747ad-108">You can get the utilization records of a customer's Azure subscription for a specified time period using the Azure utilization API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="747ad-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="747ad-109">Prerequisites</span></span>

- <span data-ttu-id="747ad-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="747ad-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="747ad-111">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="747ad-111">This scenario supports authentication with both standalone app and App+User credentials.</span></span>

- <span data-ttu-id="747ad-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="747ad-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="747ad-113">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="747ad-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="747ad-114">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="747ad-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="747ad-115">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="747ad-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="747ad-116">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="747ad-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="747ad-117">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="747ad-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="747ad-118">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="747ad-118">A subscription identifier.</span></span>

<span data-ttu-id="747ad-119">Ten interfejs API zwraca codziennie i co godzinę użycie nieklasyfikowane dla dowolnego przedziału czasu.</span><span class="sxs-lookup"><span data-stu-id="747ad-119">This API returns daily and hourly unrated consumption for an arbitrary time span.</span></span> <span data-ttu-id="747ad-120">Jednak *ten interfejs API nie jest obsługiwany w przypadku planów platformy Azure*.</span><span class="sxs-lookup"><span data-stu-id="747ad-120">However, *this API isn't supported for Azure plans*.</span></span> <span data-ttu-id="747ad-121">Jeśli masz plan platformy Azure, zapoznaj się z artykułem [Pobierz fakturę za rozliczane opłaty za wiersze](get-invoice-unbilled-consumption-lineitems.md) i [Pobierz faktury za użycie](get-invoice-billed-consumption-lineitems.md) .</span><span class="sxs-lookup"><span data-stu-id="747ad-121">If you have an Azure plan, see the articles [Get invoice unbilled consumption line items](get-invoice-unbilled-consumption-lineitems.md) and [Get invoice billed consumption line items](get-invoice-billed-consumption-lineitems.md) instead.</span></span> <span data-ttu-id="747ad-122">W tych artykułach opisano, jak uzyskać zużycie znamionowe na poziomie dziennym dla każdego z zasobów.</span><span class="sxs-lookup"><span data-stu-id="747ad-122">These articles describe how to get rated consumption at a daily level per meter per resource.</span></span> <span data-ttu-id="747ad-123">To użycie stawki jest równoznaczne z codziennymi danymi ziarna, które są udostępniane przez interfejs API użycia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="747ad-123">This rate consumption is equivalent to the daily grain data provided by the Azure utilization API.</span></span> <span data-ttu-id="747ad-124">Aby pobrać dane użycia, należy użyć identyfikatora faktury.</span><span class="sxs-lookup"><span data-stu-id="747ad-124">You'll need to use the invoice identifier to retrieve billed usage data.</span></span> <span data-ttu-id="747ad-125">Można też użyć bieżących i poprzednich okresów, aby uzyskać szacowane oszacowania użycia.</span><span class="sxs-lookup"><span data-stu-id="747ad-125">Or, you can use current and previous periods to get unbilled usage estimates.</span></span> <span data-ttu-id="747ad-126">*Dane o godzinowych ziarnach i dowolnych filtrach zakresów dat nie są obecnie obsługiwane w przypadku zasobów subskrypcji planu platformy Azure*.</span><span class="sxs-lookup"><span data-stu-id="747ad-126">*Hourly grain data and arbitrary date range filters aren't currently supported for Azure plan subscription resources*.</span></span>

## <a name="azure-utilization-api"></a><span data-ttu-id="747ad-127">Interfejs API użycia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="747ad-127">Azure utilization API</span></span>

<span data-ttu-id="747ad-128">Ten interfejs API wykorzystania platformy Azure zapewnia dostęp do rekordów użycia w okresie, który reprezentuje, kiedy wykorzystanie zostało zgłoszone w systemie rozliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="747ad-128">This Azure utilization API provides access to utilization records for a time period that represents when the utilization was reported in the billing system.</span></span> <span data-ttu-id="747ad-129">Zapewnia dostęp do tych samych danych użycia, które są używane do tworzenia i obliczania pliku uzgadniania.</span><span class="sxs-lookup"><span data-stu-id="747ad-129">It provides access to the same utilization data that is used to create and calculate the reconciliation file.</span></span> <span data-ttu-id="747ad-130">Nie ma jednak informacji o logice pliku uzgodnienia systemu rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="747ad-130">However, it does not have knowledge of billing system reconciliation file logic.</span></span> <span data-ttu-id="747ad-131">Nie należy oczekiwać, że wyniki podsumowania plików są zgodne z wynikami pobranymi z tego interfejsu API dokładnie dla tego samego okresu.</span><span class="sxs-lookup"><span data-stu-id="747ad-131">You should not expect reconciliation file summary results to match the result retrieved from this API exactly for the same time period.</span></span>

<span data-ttu-id="747ad-132">Na przykład system rozliczeń pobiera te same dane dotyczące użycia i stosuje reguły opóźnienia, aby określić, co jest uwzględnione w pliku uzgadniania.</span><span class="sxs-lookup"><span data-stu-id="747ad-132">For example, the billing system takes the same utilization data and applies lateness rules to determine what is accounted for in a reconciliation file.</span></span> <span data-ttu-id="747ad-133">Gdy okres rozliczeniowy zostanie zamknięty, wszystkie użycie do końca dnia, w którym kończy się okres rozliczeniowy, zostanie uwzględniony w pliku uzgodnienia.</span><span class="sxs-lookup"><span data-stu-id="747ad-133">When a billing period closes, all usage until the end of the day that the billing period ends is included in the reconciliation file.</span></span> <span data-ttu-id="747ad-134">Każde późniejsze użycie w okresie rozliczeniowym, które jest zgłaszane w ciągu 24 godzin po zakończeniu okresu rozliczeniowego, jest uwzględniane w następnym pliku uzgodnienia.</span><span class="sxs-lookup"><span data-stu-id="747ad-134">Any late usage within the billing period that is reported within 24 hours after the billing period ends is accounted for in the next reconciliation file.</span></span> <span data-ttu-id="747ad-135">Aby uzyskać reguły dotyczące opóźnień związanych z naliczaniem partnera, zobacz [pobieranie danych dotyczących zużycia dla subskrypcji platformy Azure](/previous-versions/azure/reference/mt219001(v=azure.100)).</span><span class="sxs-lookup"><span data-stu-id="747ad-135">For the lateness rules of how the partner is billed, see [Get consumption data for an Azure subscription](/previous-versions/azure/reference/mt219001(v=azure.100)).</span></span>

<span data-ttu-id="747ad-136">Ten interfejs API REST jest stronicowany.</span><span class="sxs-lookup"><span data-stu-id="747ad-136">This REST API is paged.</span></span> <span data-ttu-id="747ad-137">Jeśli ładunek odpowiedzi jest większy niż jedna strona, należy wykonać kolejne łącze, aby uzyskać następną stronę rekordów użycia.</span><span class="sxs-lookup"><span data-stu-id="747ad-137">If the response payload is larger than a single page, you must follow the next link to get the next page of utilization records.</span></span>

## <a name="c"></a><span data-ttu-id="747ad-138">C\#</span><span class="sxs-lookup"><span data-stu-id="747ad-138">C\#</span></span>

<span data-ttu-id="747ad-139">Aby uzyskać rekordy użycia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="747ad-139">To obtain the Azure Utilization Records:</span></span>

1. <span data-ttu-id="747ad-140">Pobierz identyfikator klienta i Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="747ad-140">Get the customer ID and subscription ID.</span></span>

2. <span data-ttu-id="747ad-141">Wywołaj metodę [**IAzureUtilizationCollection. Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) , aby zwrócić element [**resourcecollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) , który zawiera rekordy użycia.</span><span class="sxs-lookup"><span data-stu-id="747ad-141">Call the [**IAzureUtilizationCollection.Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) method to return a [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) that contains the utilization records.</span></span>

3. <span data-ttu-id="747ad-142">Uzyskaj moduł wyliczający rekordu wykorzystania platformy Azure, aby przechodzenie przez strony użycia.</span><span class="sxs-lookup"><span data-stu-id="747ad-142">Obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span> <span data-ttu-id="747ad-143">Ten krok jest wymagany, ponieważ jest stronicowana kolekcja zasobów.</span><span class="sxs-lookup"><span data-stu-id="747ad-143">This step is required, because the resource collection is paged.</span></span>

- <span data-ttu-id="747ad-144">**Przykład**: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="747ad-144">**Sample**: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="747ad-145">**Projekt**: przykłady dla zestawu SDK Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="747ad-145">**Project**: Partner Center SDK Samples</span></span>
- <span data-ttu-id="747ad-146">**Klasa**: GetAzureSubscriptionUtilization.cs</span><span class="sxs-lookup"><span data-stu-id="747ad-146">**Class**: GetAzureSubscriptionUtilization.cs</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

IPartner partner = PartnerService.Instance.CreatePartnerOperations(credentials);

// Retrieve the utilization records for the last year in pages of 100 records.
var utilizationRecords = partner.Customers[customerId].Subscriptions[subscriptionId].Utilization.Azure.Query(
    DateTimeOffset.Now.AddYears(-1),
    DateTimeOffset.Now,
    size: 100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages.
var utilizationRecordEnumerator = partner.Enumerators.Utilization.Azure.Create(utilizationRecords);

while (utilizationRecordEnumerator.HasValue)
{
    //
    // Insert code here to work with this page.
    //

    // Get the next page.
    utilizationRecordEnumerator.Next();
}
```

## <a name="java"></a><span data-ttu-id="747ad-147">Java</span><span class="sxs-lookup"><span data-stu-id="747ad-147">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="747ad-148">Aby uzyskać rekordy użycia platformy Azure, musisz najpierw mieć identyfikator klienta i Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="747ad-148">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="747ad-149">Następnie należy wywołać funkcję **IAzureUtilizationCollection. Query** w celu zwrócenia elementu **resourcecollection** , który zawiera rekordy użycia.</span><span class="sxs-lookup"><span data-stu-id="747ad-149">You then call the **IAzureUtilizationCollection.query** function to return a **ResourceCollection** that contains the utilization records.</span></span> <span data-ttu-id="747ad-150">Ponieważ kolekcja zasobów jest stronicowana, należy uzyskać moduł wyliczający rekordy wykorzystania platformy Azure, aby przechodzenie przez strony użycia.</span><span class="sxs-lookup"><span data-stu-id="747ad-150">Because the resource collection is paged, you must then obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;

ResourceCollection<AzureUtilizationRecord> utilizationRecords = partnerOperations.getCustomers()
  .byId(customerId).getSubscriptions().byId(subscriptionId)
  .getUtilization().getAzure().query(
      new DateTime().minusYears(1),
      new DateTime(),
      AzureUtilizationGranularity.Daily,
      true,
      100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages
IResourceCollectionEnumerator<ResourceCollection<AzureUtilizationRecord>> utilizationRecordEnumerator =
    partnerOperations.getEnumerators().getUtilization().getAzure().create(utilizationRecords);

while (utilizationRecordEnumerator.hasValue())
{
    //
    // Insert code here to work with this page.
    //

    // get the next page
    utilizationRecordEnumerator.next();
}
```

## <a name="powershell"></a><span data-ttu-id="747ad-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="747ad-151">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="747ad-152">Aby uzyskać rekordy użycia platformy Azure, musisz najpierw mieć identyfikator klienta i Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="747ad-152">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="747ad-153">Następnie Wywołaj polecenie [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md).</span><span class="sxs-lookup"><span data-stu-id="747ad-153">You then call the [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md).</span></span> <span data-ttu-id="747ad-154">To polecenie zwróci wszystkie rekordy dostępne w określonym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="747ad-154">This command will return all records available for the specified period of time.</span></span>

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a><span data-ttu-id="747ad-155">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="747ad-155">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="747ad-156">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="747ad-156">Request syntax</span></span>

| <span data-ttu-id="747ad-157">Metoda</span><span class="sxs-lookup"><span data-stu-id="747ad-157">Method</span></span> | <span data-ttu-id="747ad-158">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="747ad-158">Request URI</span></span> |
|------- | ----------- |
| <span data-ttu-id="747ad-159">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="747ad-159">**GET**</span></span> | <span data-ttu-id="747ad-160">*{baseURL}*/V1/Customers/{Customer-tenant-ID}/subscriptions/{Subscription-ID}/utilizations/Azure? \_ czas rozpoczęcia = {Start-Time} &\_ czas zakończenia = {czas zakończenia} &stopnia szczegółowości = {stopień szczegółowości} &pokazać \_ szczegóły = {true}</span><span class="sxs-lookup"><span data-stu-id="747ad-160">*{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/utilizations/azure?start\_time={start-time}&end\_time={end-time}&granularity={granularity}&show\_details={True}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="747ad-161">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="747ad-161">URI parameters</span></span>

<span data-ttu-id="747ad-162">Użyj następującej ścieżki i parametrów zapytania, aby pobrać rekordy użycia.</span><span class="sxs-lookup"><span data-stu-id="747ad-162">Use the following path and query parameters to get the utilization records.</span></span>

| <span data-ttu-id="747ad-163">Nazwa</span><span class="sxs-lookup"><span data-stu-id="747ad-163">Name</span></span> | <span data-ttu-id="747ad-164">Typ</span><span class="sxs-lookup"><span data-stu-id="747ad-164">Type</span></span> | <span data-ttu-id="747ad-165">Wymagane</span><span class="sxs-lookup"><span data-stu-id="747ad-165">Required</span></span> | <span data-ttu-id="747ad-166">Opis</span><span class="sxs-lookup"><span data-stu-id="747ad-166">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="747ad-167">Identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="747ad-167">customer-tenant-id</span></span> | <span data-ttu-id="747ad-168">ciąg</span><span class="sxs-lookup"><span data-stu-id="747ad-168">string</span></span> | <span data-ttu-id="747ad-169">Tak</span><span class="sxs-lookup"><span data-stu-id="747ad-169">Yes</span></span> | <span data-ttu-id="747ad-170">Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="747ad-170">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="747ad-171">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="747ad-171">subscription-id</span></span> | <span data-ttu-id="747ad-172">ciąg</span><span class="sxs-lookup"><span data-stu-id="747ad-172">string</span></span> | <span data-ttu-id="747ad-173">Tak</span><span class="sxs-lookup"><span data-stu-id="747ad-173">Yes</span></span> | <span data-ttu-id="747ad-174">Ciąg w formacie GUID, który identyfikuje subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="747ad-174">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="747ad-175">start_time</span><span class="sxs-lookup"><span data-stu-id="747ad-175">start_time</span></span> | <span data-ttu-id="747ad-176">ciąg w formacie UTC Data-godzina przesunięcia</span><span class="sxs-lookup"><span data-stu-id="747ad-176">string in UTC date-time offset format</span></span> | <span data-ttu-id="747ad-177">Tak</span><span class="sxs-lookup"><span data-stu-id="747ad-177">Yes</span></span> | <span data-ttu-id="747ad-178">Początek zakresu czasu, który reprezentuje, kiedy wykorzystanie zostało zgłoszone w systemie rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="747ad-178">The start of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="747ad-179">end_time</span><span class="sxs-lookup"><span data-stu-id="747ad-179">end_time</span></span> | <span data-ttu-id="747ad-180">ciąg w formacie UTC Data-godzina przesunięcia</span><span class="sxs-lookup"><span data-stu-id="747ad-180">string in UTC date-time offset format</span></span> | <span data-ttu-id="747ad-181">Tak</span><span class="sxs-lookup"><span data-stu-id="747ad-181">Yes</span></span> | <span data-ttu-id="747ad-182">Koniec zakresu czasu, który reprezentuje, kiedy wykorzystanie zostało zgłoszone w systemie rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="747ad-182">The end of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="747ad-183">stopnia szczegółowości</span><span class="sxs-lookup"><span data-stu-id="747ad-183">granularity</span></span> | <span data-ttu-id="747ad-184">ciąg</span><span class="sxs-lookup"><span data-stu-id="747ad-184">string</span></span> | <span data-ttu-id="747ad-185">Nie</span><span class="sxs-lookup"><span data-stu-id="747ad-185">No</span></span> | <span data-ttu-id="747ad-186">Definiuje stopień szczegółowości agregacji użycia.</span><span class="sxs-lookup"><span data-stu-id="747ad-186">Defines the granularity of usage aggregations.</span></span> <span data-ttu-id="747ad-187">Dostępne opcje to: `daily` (ustawienie domyślne) i `hourly` .</span><span class="sxs-lookup"><span data-stu-id="747ad-187">Available options are: `daily` (default) and `hourly`.</span></span>
| <span data-ttu-id="747ad-188">show_details</span><span class="sxs-lookup"><span data-stu-id="747ad-188">show_details</span></span> | <span data-ttu-id="747ad-189">boolean</span><span class="sxs-lookup"><span data-stu-id="747ad-189">boolean</span></span> | <span data-ttu-id="747ad-190">Nie</span><span class="sxs-lookup"><span data-stu-id="747ad-190">No</span></span> | <span data-ttu-id="747ad-191">Określa, czy mają zostać pobrane szczegóły użycia na poziomie wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="747ad-191">Specifies whether to get the instance-level usage details.</span></span> <span data-ttu-id="747ad-192">Wartość domyślna to `true`.</span><span class="sxs-lookup"><span data-stu-id="747ad-192">The default is `true`.</span></span> |
| <span data-ttu-id="747ad-193">size</span><span class="sxs-lookup"><span data-stu-id="747ad-193">size</span></span> | <span data-ttu-id="747ad-194">liczba</span><span class="sxs-lookup"><span data-stu-id="747ad-194">number</span></span> | <span data-ttu-id="747ad-195">Nie</span><span class="sxs-lookup"><span data-stu-id="747ad-195">No</span></span> | <span data-ttu-id="747ad-196">Określa liczbę agregacji zwracanych przez pojedyncze wywołanie interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="747ad-196">Specifies the number of aggregations returned by a single API call.</span></span> <span data-ttu-id="747ad-197">Wartość domyślna to 1000.</span><span class="sxs-lookup"><span data-stu-id="747ad-197">The default is 1000.</span></span> <span data-ttu-id="747ad-198">Wartość maksymalna to 1000.</span><span class="sxs-lookup"><span data-stu-id="747ad-198">The max is 1000.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="747ad-199">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="747ad-199">Request headers</span></span>

<span data-ttu-id="747ad-200">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="747ad-200">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="747ad-201">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="747ad-201">Request body</span></span>

<span data-ttu-id="747ad-202">Brak</span><span class="sxs-lookup"><span data-stu-id="747ad-202">None</span></span>

### <a name="request-example"></a><span data-ttu-id="747ad-203">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="747ad-203">Request example</span></span>

<span data-ttu-id="747ad-204">Poniższe przykładowe żądanie generuje wyniki podobne do tego, jaki plik uzgadniania będzie wyświetlany przez okres 7/2-8/1.</span><span class="sxs-lookup"><span data-stu-id="747ad-204">The following example request produces results similar to what the reconciliation file will show for the period 7/2 - 8/1.</span></span> <span data-ttu-id="747ad-205">Te wyniki mogą nie być dokładnie zgodne (szczegółowe informacje znajdują się w sekcji [interfejsu API wykorzystania platformy Azure](#azure-utilization-api) ).</span><span class="sxs-lookup"><span data-stu-id="747ad-205">These results may not match exactly (see the section [Azure utilization API](#azure-utilization-api) for details).</span></span>

<span data-ttu-id="747ad-206">To przykładowe żądanie zwraca dane użycia zgłoszone w systemie rozliczeniowym między 7/2 o 12 AM (UTC) i 8/2 o godzinie 00:00 (UTC).</span><span class="sxs-lookup"><span data-stu-id="747ad-206">This example request returns utilization data reported in the billing system between 7/2 at 12 AM (UTC) and 8/2 at 12 AM (UTC).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="747ad-207">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="747ad-207">REST response</span></span>

<span data-ttu-id="747ad-208">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów [rekordu użycia platformy Azure](azure-utilization-record-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="747ad-208">If successful, this method returns a collection of [Azure Utilization Record](azure-utilization-record-resources.md) resources in the response body.</span></span> <span data-ttu-id="747ad-209">Jeśli dane użycia platformy Azure nie są jeszcze gotowe w systemie zależnym, Metoda ta zwraca kod stanu HTTP 204 z nagłówkiem Retry-After.</span><span class="sxs-lookup"><span data-stu-id="747ad-209">If the Azure utilization data isn't yet ready in a dependent system, this method returns an HTTP Status Code 204 with a Retry-After header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="747ad-210">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="747ad-210">Response success and error codes</span></span>

<span data-ttu-id="747ad-211">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="747ad-211">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="747ad-212">Użyj narzędzia do śledzenia sieci, aby odczytać kod stanu HTTP, [typ kodu błędu](error-codes.md)i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="747ad-212">Use a network trace tool to read the HTTP status code, [error code type](error-codes.md), and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="747ad-213">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="747ad-213">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2630
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: PjuGoYrw806o6A3Y.0
MS-ServerId: 030020525
Date: Fri, 04 Aug 2017 23:48:28 GMT

{
  "totalCount": 2,
  "items": [
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        }
      },
      "attributes": {
        "objectType": "AzureUtilizationRecord"
      }
    },
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        },
        "attributes": {
          "objectType": "AzureUtilizationRecord"
        }
      },

      "links": {
        "self": {
          "uri": "customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-06-10T00:00:00Z&end_time=2017-07-09T00:00:00Z&granularity=Daily&show_details=True&size=1000",
          "method": "GET",
          "headers": []
        }
      },
      "attributes": {
        "objectType": "Collection"
      }
    }
  ]
}
```
