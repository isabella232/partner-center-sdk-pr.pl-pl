---
title: Pobieranie rekordów dotyczących wykorzystania platformy Azure przez klienta
description: Za pomocą interfejsu API wykorzystania platformy Azure można pobrać rekordy wykorzystania subskrypcji platformy Azure klienta w określonym przedziale czasu.
ms.date: 04/19/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 23c8d18462081c6d6c95c1d969f269cbb3f8754b
ms.sourcegitcommit: abefe11421edc421491f14b257b2408b4f29b669
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/20/2021
ms.locfileid: "107745596"
---
# <a name="get-a-customers-utilization-records-for-azure"></a><span data-ttu-id="58444-103">Pobieranie rekordów dotyczących wykorzystania platformy Azure przez klienta</span><span class="sxs-lookup"><span data-stu-id="58444-103">Get a customer's utilization records for Azure</span></span>

<span data-ttu-id="58444-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="58444-104">**Applies to:**</span></span>

- <span data-ttu-id="58444-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="58444-105">Partner Center</span></span>
- <span data-ttu-id="58444-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="58444-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="58444-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="58444-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="58444-108">Rekordy wykorzystania subskrypcji platformy Azure klienta w określonym przedziale czasu można uzyskać przy użyciu interfejsu API użycia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="58444-108">You can get the utilization records of a customer's Azure subscription for a specified time period using the Azure utilization API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58444-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="58444-109">Prerequisites</span></span>

- <span data-ttu-id="58444-110">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="58444-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="58444-111">Ten scenariusz obsługuje uwierzytelnianie zarówno za pomocą aplikacji autonomicznej, jak i poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="58444-111">This scenario supports authentication with both standalone app and App+User credentials.</span></span>

- <span data-ttu-id="58444-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="58444-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="58444-113">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="58444-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="58444-114">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="58444-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="58444-115">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="58444-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="58444-116">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="58444-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="58444-117">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="58444-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="58444-118">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="58444-118">A subscription identifier.</span></span>

<span data-ttu-id="58444-119">Ten interfejs API zwraca dzienne i godzinowe zużycie bez użycia dla dowolnego zakresu czasu.</span><span class="sxs-lookup"><span data-stu-id="58444-119">This API returns daily and hourly unrated consumption for an arbitrary time span.</span></span> <span data-ttu-id="58444-120">Ten interfejs *API nie jest jednak obsługiwany w przypadku planów platformy Azure.*</span><span class="sxs-lookup"><span data-stu-id="58444-120">However, *this API isn't supported for Azure plans*.</span></span> <span data-ttu-id="58444-121">Jeśli masz plan platformy Azure, zapoznaj się z artykułami Get [invoice un-billed consumption line items](get-invoice-unbilled-consumption-lineitems.md) (Uzyskiwanie niezafakturowanych elementów zużycia za faktury) i Get invoice billed consumption line items (Uzyskiwanie pozycji zużycia rozliczanych na podstawie [faktury).](get-invoice-billed-consumption-lineitems.md)</span><span class="sxs-lookup"><span data-stu-id="58444-121">If you have an Azure plan, see the articles [Get invoice un-billed consumption line items](get-invoice-unbilled-consumption-lineitems.md) and [Get invoice billed consumption line items](get-invoice-billed-consumption-lineitems.md) instead.</span></span> <span data-ttu-id="58444-122">W tych artykułach opisano sposób oceny zużycia na poziomie dziennym na miernik na zasób.</span><span class="sxs-lookup"><span data-stu-id="58444-122">These articles describe how to get rated consumption at a daily level per meter per resource.</span></span> <span data-ttu-id="58444-123">To użycie jest równoważne z dziennymi danymi ziarna dostarczanymi przez interfejs API użycia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="58444-123">This rate consumption is equivalent to the daily grain data provided by the Azure utilization API.</span></span> <span data-ttu-id="58444-124">Aby pobrać rozliczane dane użycia, należy użyć identyfikatora faktury.</span><span class="sxs-lookup"><span data-stu-id="58444-124">You'll need to use the invoice identifier to retrieve billed usage data.</span></span> <span data-ttu-id="58444-125">Możesz też użyć bieżących i poprzednich okresów, aby uzyskać niezapłaszone oszacowania użycia.</span><span class="sxs-lookup"><span data-stu-id="58444-125">Or, you can use current and previous periods to get un-billed usage estimates.</span></span> <span data-ttu-id="58444-126">*Dane ziarna godzinowego i dowolne filtry zakresu dat nie są* obecnie obsługiwane w przypadku zasobów subskrypcji planu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="58444-126">*Hourly grain data and arbitrary date range filters aren't currently supported for Azure plan subscription resources*.</span></span>

## <a name="azure-utilization-api"></a><span data-ttu-id="58444-127">Interfejs API wykorzystania platformy Azure</span><span class="sxs-lookup"><span data-stu-id="58444-127">Azure utilization API</span></span>

<span data-ttu-id="58444-128">Ten interfejs API wykorzystania platformy Azure zapewnia dostęp do rekordów wykorzystania w okresie, który reprezentuje, kiedy wykorzystanie zostało zgłoszone w systemie rozliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="58444-128">This Azure utilization API provides access to utilization records for a time period that represents when the utilization was reported in the billing system.</span></span> <span data-ttu-id="58444-129">Zapewnia dostęp do tych samych danych użycia, które są używane do tworzenia i obliczania pliku uzgodnień.</span><span class="sxs-lookup"><span data-stu-id="58444-129">It provides access to the same utilization data that is used to create and calculate the reconciliation file.</span></span> <span data-ttu-id="58444-130">Nie ma jednak wiedzy na temat logiki pliku uzgodnień systemu rozliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="58444-130">However, it does not have knowledge of billing system reconciliation file logic.</span></span> <span data-ttu-id="58444-131">Nie należy oczekiwać, że wyniki podsumowania pliku uzgodnień będą zgodne z wynikiem pobranym z tego interfejsu API dokładnie w tym samym okresie.</span><span class="sxs-lookup"><span data-stu-id="58444-131">You should not expect reconciliation file summary results to match the result retrieved from this API exactly for the same time period.</span></span>

<span data-ttu-id="58444-132">Na przykład system rozliczeń pobiera te same dane użycia i stosuje reguły opóźnień w celu określenia, co jest uwzględnione w pliku uzgodnień.</span><span class="sxs-lookup"><span data-stu-id="58444-132">For example, the billing system takes the same utilization data and applies lateness rules to determine what is accounted for in a reconciliation file.</span></span> <span data-ttu-id="58444-133">Po zamknięciu okresu rozliczeniowego całe użycie do końca dnia zakończenia okresu rozliczeniowego jest uwzględniane w pliku uzgodnień.</span><span class="sxs-lookup"><span data-stu-id="58444-133">When a billing period closes, all usage until the end of the day that the billing period ends is included in the reconciliation file.</span></span> <span data-ttu-id="58444-134">Każde późne użycie w okresie rozliczeniowym, które jest zgłaszane w ciągu 24 godzin po zakończeniu okresu rozliczeniowego, jest uwzględniane w następnym pliku uzgodnień.</span><span class="sxs-lookup"><span data-stu-id="58444-134">Any late usage within the billing period that is reported within 24 hours after the billing period ends is accounted for in the next reconciliation file.</span></span> <span data-ttu-id="58444-135">Aby uzyskać informacje na temat reguł opóźniań dotyczących sposobu rozlinia partnera, zobacz Get consumption data for an Azure subscription (Uzyskiwanie danych użycia [dla subskrypcji platformy Azure).](/previous-versions/azure/reference/mt219001(v=azure.100))</span><span class="sxs-lookup"><span data-stu-id="58444-135">For the lateness rules of how the partner is billed, see [Get consumption data for an Azure subscription](/previous-versions/azure/reference/mt219001(v=azure.100)).</span></span>

<span data-ttu-id="58444-136">Ten interfejs API REST jest stronicowany.</span><span class="sxs-lookup"><span data-stu-id="58444-136">This REST API is paged.</span></span> <span data-ttu-id="58444-137">Jeśli ładunek odpowiedzi jest większy niż jedna strona, musisz użyć następnego linku, aby uzyskać następną stronę rekordów wykorzystania.</span><span class="sxs-lookup"><span data-stu-id="58444-137">If the response payload is larger than a single page, you must follow the next link to get the next page of utilization records.</span></span>

### <a name="scenario--partner-a-has-transferred-billing-ownership-of-azure-legacy-subscription-145p-to-partner-b"></a><span data-ttu-id="58444-138">Scenariusz: Partner A przeniesiono własność rozliczeń starszej subskrypcji platformy Azure (145P) do partnera B</span><span class="sxs-lookup"><span data-stu-id="58444-138">Scenario : Partner A has transferred billing ownership of Azure Legacy Subscription (145P) to Partner B</span></span>

<span data-ttu-id="58444-139">Jeśli partner przenosi własność rozliczeń starszej subskrypcji platformy Azure na innego partnera, gdy nowy partner wywołuje interfejs API wykorzystania dla przeniesionej subskrypcji, musi użyć identyfikatora subskrypcji handlowej (który pojawia się na koncie usługi Partner Center), a nie identyfikatora uprawnień platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="58444-139">If a partner transfers billing ownership of an Azure legacy subscription to another partner, when new the new partner calls Utilization API for transferred subscription they have to use Commerce Subscription ID (which shows up in their Partner Center account) rather than the Azure Entitlement ID.</span></span> <span data-ttu-id="58444-140">Identyfikator uprawnień platformy Azure jest wyświetlany dla partnera B tylko wtedy, gdy jest administratorem w imieniu klienta (AOBO) w imieniu klienta Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="58444-140">Azure Entitlement ID appears for Partner B only when they are Admin on behalf of (AOBO) to Customer's Azure portal.</span></span> 

<span data-ttu-id="58444-141">Aby pomyślnie wywołać interfejs API wykorzystania przeniesionej subskrypcji, nowy partner musi użyć identyfikatora subskrypcji handlowej.</span><span class="sxs-lookup"><span data-stu-id="58444-141">To successfully call the Utilization API for the transferred subscription, the new partner needs to use the Commerce Subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="58444-142">C\#</span><span class="sxs-lookup"><span data-stu-id="58444-142">C\#</span></span>

<span data-ttu-id="58444-143">Aby uzyskać rekordy wykorzystania platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="58444-143">To obtain the Azure Utilization Records:</span></span>

1. <span data-ttu-id="58444-144">Pobierz identyfikator klienta i identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="58444-144">Get the customer ID and subscription ID.</span></span>

2. <span data-ttu-id="58444-145">Wywołaj [**metodę IAzureUtilizationCollection.Query,**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) aby zwrócić metodę [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) zawierającą rekordy wykorzystania.</span><span class="sxs-lookup"><span data-stu-id="58444-145">Call the [**IAzureUtilizationCollection.Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) method to return a [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) that contains the utilization records.</span></span>

3. <span data-ttu-id="58444-146">Uzyskaj moduł wyliczający rekord wykorzystania platformy Azure w celu przechodzenia między stronami wykorzystania.</span><span class="sxs-lookup"><span data-stu-id="58444-146">Obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span> <span data-ttu-id="58444-147">Ten krok jest wymagany, ponieważ kolekcja zasobów jest stronicowana.</span><span class="sxs-lookup"><span data-stu-id="58444-147">This step is required, because the resource collection is paged.</span></span>

- <span data-ttu-id="58444-148">**Przykład:** [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="58444-148">**Sample**: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="58444-149">**Projekt**: zestaw SDK Centrum partnerskiego przykłady</span><span class="sxs-lookup"><span data-stu-id="58444-149">**Project**: Partner Center SDK Samples</span></span>
- <span data-ttu-id="58444-150">**Klasa**: GetAzureSubscriptionUtilization.cs</span><span class="sxs-lookup"><span data-stu-id="58444-150">**Class**: GetAzureSubscriptionUtilization.cs</span></span>

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

## <a name="java"></a><span data-ttu-id="58444-151">Java</span><span class="sxs-lookup"><span data-stu-id="58444-151">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="58444-152">Aby uzyskać rekordy wykorzystania platformy Azure, musisz najpierw uzyskać identyfikator klienta i identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="58444-152">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="58444-153">Następnie wywołaj funkcję **IAzureUtilizationCollection.query,** aby zwrócić funkcję **ResourceCollection** zawierającą rekordy wykorzystania.</span><span class="sxs-lookup"><span data-stu-id="58444-153">You then call the **IAzureUtilizationCollection.query** function to return a **ResourceCollection** that contains the utilization records.</span></span> <span data-ttu-id="58444-154">Ponieważ kolekcja zasobów jest stronicowana, należy uzyskać moduł wyliczający rekord wykorzystania platformy Azure, aby przechodzić między stronami wykorzystania.</span><span class="sxs-lookup"><span data-stu-id="58444-154">Because the resource collection is paged, you must then obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span>

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

## <a name="powershell"></a><span data-ttu-id="58444-155">PowerShell</span><span class="sxs-lookup"><span data-stu-id="58444-155">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="58444-156">Aby uzyskać rekordy wykorzystania platformy Azure, musisz najpierw uzyskać identyfikator klienta i identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="58444-156">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="58444-157">Następnie wywołaj pozycję [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md).</span><span class="sxs-lookup"><span data-stu-id="58444-157">You then call the [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md).</span></span> <span data-ttu-id="58444-158">To polecenie zwróci wszystkie rekordy dostępne w określonym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="58444-158">This command will return all records available for the specified period of time.</span></span>

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a><span data-ttu-id="58444-159">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="58444-159">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="58444-160">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="58444-160">Request syntax</span></span>

| <span data-ttu-id="58444-161">Metoda</span><span class="sxs-lookup"><span data-stu-id="58444-161">Method</span></span> | <span data-ttu-id="58444-162">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="58444-162">Request URI</span></span> |
|------- | ----------- |
| <span data-ttu-id="58444-163">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="58444-163">**GET**</span></span> | <span data-ttu-id="58444-164">*{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/utilizations/azure?start \_ time={godzina rozpoczęcia}&\_ zakończenia={czas zakończenia}&stopień szczegółowości={stopień szczegółowości}&pokaż \_ szczegóły={True}</span><span class="sxs-lookup"><span data-stu-id="58444-164">*{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/utilizations/azure?start\_time={start-time}&end\_time={end-time}&granularity={granularity}&show\_details={True}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="58444-165">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="58444-165">URI parameters</span></span>

<span data-ttu-id="58444-166">Użyj następującej ścieżki i parametrów zapytania, aby pobrać rekordy wykorzystania.</span><span class="sxs-lookup"><span data-stu-id="58444-166">Use the following path and query parameters to get the utilization records.</span></span>

| <span data-ttu-id="58444-167">Nazwa</span><span class="sxs-lookup"><span data-stu-id="58444-167">Name</span></span> | <span data-ttu-id="58444-168">Typ</span><span class="sxs-lookup"><span data-stu-id="58444-168">Type</span></span> | <span data-ttu-id="58444-169">Wymagane</span><span class="sxs-lookup"><span data-stu-id="58444-169">Required</span></span> | <span data-ttu-id="58444-170">Opis</span><span class="sxs-lookup"><span data-stu-id="58444-170">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="58444-171">identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="58444-171">customer-tenant-id</span></span> | <span data-ttu-id="58444-172">ciąg</span><span class="sxs-lookup"><span data-stu-id="58444-172">string</span></span> | <span data-ttu-id="58444-173">Tak</span><span class="sxs-lookup"><span data-stu-id="58444-173">Yes</span></span> | <span data-ttu-id="58444-174">Ciąg w formacie identyfikatora GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="58444-174">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="58444-175">subscription-id</span><span class="sxs-lookup"><span data-stu-id="58444-175">subscription-id</span></span> | <span data-ttu-id="58444-176">ciąg</span><span class="sxs-lookup"><span data-stu-id="58444-176">string</span></span> | <span data-ttu-id="58444-177">Tak</span><span class="sxs-lookup"><span data-stu-id="58444-177">Yes</span></span> | <span data-ttu-id="58444-178">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="58444-178">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="58444-179">start_time</span><span class="sxs-lookup"><span data-stu-id="58444-179">start_time</span></span> | <span data-ttu-id="58444-180">ciąg w formacie przesunięcia daty i godzin UTC</span><span class="sxs-lookup"><span data-stu-id="58444-180">string in UTC date-time offset format</span></span> | <span data-ttu-id="58444-181">Tak</span><span class="sxs-lookup"><span data-stu-id="58444-181">Yes</span></span> | <span data-ttu-id="58444-182">Początek zakresu czasu, który reprezentuje, kiedy wykorzystanie zostało zgłoszone w systemie rozliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="58444-182">The start of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="58444-183">End_time</span><span class="sxs-lookup"><span data-stu-id="58444-183">end_time</span></span> | <span data-ttu-id="58444-184">ciąg w formacie przesunięcia daty i godzin UTC</span><span class="sxs-lookup"><span data-stu-id="58444-184">string in UTC date-time offset format</span></span> | <span data-ttu-id="58444-185">Tak</span><span class="sxs-lookup"><span data-stu-id="58444-185">Yes</span></span> | <span data-ttu-id="58444-186">Koniec zakresu czasu, który reprezentuje, kiedy wykorzystanie zostało zgłoszone w systemie rozliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="58444-186">The end of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="58444-187">Ziarnistość</span><span class="sxs-lookup"><span data-stu-id="58444-187">granularity</span></span> | <span data-ttu-id="58444-188">ciąg</span><span class="sxs-lookup"><span data-stu-id="58444-188">string</span></span> | <span data-ttu-id="58444-189">Nie</span><span class="sxs-lookup"><span data-stu-id="58444-189">No</span></span> | <span data-ttu-id="58444-190">Definiuje poziom szczegółowości agregacji użycia.</span><span class="sxs-lookup"><span data-stu-id="58444-190">Defines the granularity of usage aggregations.</span></span> <span data-ttu-id="58444-191">Dostępne opcje to: `daily` (ustawienie domyślne) i `hourly` .</span><span class="sxs-lookup"><span data-stu-id="58444-191">Available options are: `daily` (default) and `hourly`.</span></span>
| <span data-ttu-id="58444-192">show_details</span><span class="sxs-lookup"><span data-stu-id="58444-192">show_details</span></span> | <span data-ttu-id="58444-193">boolean</span><span class="sxs-lookup"><span data-stu-id="58444-193">boolean</span></span> | <span data-ttu-id="58444-194">Nie</span><span class="sxs-lookup"><span data-stu-id="58444-194">No</span></span> | <span data-ttu-id="58444-195">Określa, czy uzyskać szczegóły użycia na poziomie wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="58444-195">Specifies whether to get the instance-level usage details.</span></span> <span data-ttu-id="58444-196">Wartość domyślna to `true`.</span><span class="sxs-lookup"><span data-stu-id="58444-196">The default is `true`.</span></span> |
| <span data-ttu-id="58444-197">size</span><span class="sxs-lookup"><span data-stu-id="58444-197">size</span></span> | <span data-ttu-id="58444-198">liczba</span><span class="sxs-lookup"><span data-stu-id="58444-198">number</span></span> | <span data-ttu-id="58444-199">Nie</span><span class="sxs-lookup"><span data-stu-id="58444-199">No</span></span> | <span data-ttu-id="58444-200">Określa liczbę agregacji zwróconych przez pojedyncze wywołanie interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="58444-200">Specifies the number of aggregations returned by a single API call.</span></span> <span data-ttu-id="58444-201">Wartość domyślna to 1000.</span><span class="sxs-lookup"><span data-stu-id="58444-201">The default is 1000.</span></span> <span data-ttu-id="58444-202">Wartość maksymalna to 1000.</span><span class="sxs-lookup"><span data-stu-id="58444-202">The max is 1000.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="58444-203">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="58444-203">Request headers</span></span>

<span data-ttu-id="58444-204">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="58444-204">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="58444-205">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="58444-205">Request body</span></span>

<span data-ttu-id="58444-206">Brak</span><span class="sxs-lookup"><span data-stu-id="58444-206">None</span></span>

### <a name="request-example"></a><span data-ttu-id="58444-207">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="58444-207">Request example</span></span>

<span data-ttu-id="58444-208">Poniższe przykładowe żądanie generuje wyniki podobne do tego, co plik uzgodnień będzie pokazywać w okresie 7/2–8/1.</span><span class="sxs-lookup"><span data-stu-id="58444-208">The following example request produces results similar to what the reconciliation file will show for the period 7/2 - 8/1.</span></span> <span data-ttu-id="58444-209">Te wyniki mogą nie być dokładnie zgodne (zobacz sekcję Interfejs [API użycia platformy Azure,](#azure-utilization-api) aby uzyskać szczegółowe informacje).</span><span class="sxs-lookup"><span data-stu-id="58444-209">These results may not match exactly (see the section [Azure utilization API](#azure-utilization-api) for details).</span></span>

<span data-ttu-id="58444-210">To przykładowe żądanie zwraca dane dotyczące wykorzystania zgłoszone w systemie rozliczeniowym między godziną 7/2 o godzinie 12:00 (UTC) a 8/2 o godzinie 12:00 (UTC).</span><span class="sxs-lookup"><span data-stu-id="58444-210">This example request returns utilization data reported in the billing system between 7/2 at 12 AM (UTC) and 8/2 at 12 AM (UTC).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="58444-211">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="58444-211">REST response</span></span>

<span data-ttu-id="58444-212">W przypadku powodzenia ta metoda zwraca kolekcję zasobów [rekordu użycia platformy Azure](azure-utilization-record-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="58444-212">If successful, this method returns a collection of [Azure Utilization Record](azure-utilization-record-resources.md) resources in the response body.</span></span> <span data-ttu-id="58444-213">Jeśli dane użycia platformy Azure nie są jeszcze gotowe w systemie zależnym, ta metoda zwraca kod stanu HTTP 204 z nagłówkiem Retry-After danych.</span><span class="sxs-lookup"><span data-stu-id="58444-213">If the Azure utilization data isn't yet ready in a dependent system, this method returns an HTTP Status Code 204 with a Retry-After header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="58444-214">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="58444-214">Response success and error codes</span></span>

<span data-ttu-id="58444-215">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="58444-215">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="58444-216">Użyj narzędzia śledzenia sieci, aby odczytać kod stanu HTTP, typ [kodu błędu](error-codes.md)i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="58444-216">Use a network trace tool to read the HTTP status code, [error code type](error-codes.md), and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="58444-217">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="58444-217">Response example</span></span>

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
