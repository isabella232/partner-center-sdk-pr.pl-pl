---
title: Operacje inspekcji działania Centrum partnerskiego
description: Informacje o typie operacji inspekcji interfejsu API Centrum partnerskiego, których można użyć do pobrania rekordu działania Centrum partnerskiego.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 019bebe40c43f6ee1c2ac7da381a86ca190702d4
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768537"
---
# <a name="audit-operations-available-via-partner-center-api-that-show-a-record-of-partner-center-activity"></a><span data-ttu-id="50a28-103">Operacje inspekcji dostępne za pośrednictwem interfejsu API Centrum partnerskiego, które pokazują rekord działania Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="50a28-103">Audit operations available via Partner Center API that show a record of Partner Center activity</span></span>

<span data-ttu-id="50a28-104">Interfejsy API Centrum partnerskiego zapewniają funkcje inspekcji, dzięki czemu można uzyskać rekord działania Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="50a28-104">The Partner Center APIs provide auditing features so you can get a record of Partner Center activity.</span></span>

<span data-ttu-id="50a28-105">Rekordy inspekcji można pobrać z ostatnich 30 dni od bieżącej daty lub dla zakresu dat określonego przez dołączenie daty rozpoczęcia i/lub daty zakończenia.</span><span class="sxs-lookup"><span data-stu-id="50a28-105">You can retrieve audit records for the previous 30 days from the current date, or for a date range specified by including the start date and/or the end date.</span></span> <span data-ttu-id="50a28-106">Należy jednak pamiętać, że ze względu na wydajność dostępność danych dziennika aktywności jest ograniczona do poprzednich 90 dni.</span><span class="sxs-lookup"><span data-stu-id="50a28-106">Note, however, that for performance reasons activity log data availability is limited to the previous 90 days.</span></span> <span data-ttu-id="50a28-107">Żądania z datą rozpoczęcia większą niż 90 dni przed bieżącą datą otrzymają błędny wyjątek żądania (kod błędu: 400) i odpowiedni komunikat.</span><span class="sxs-lookup"><span data-stu-id="50a28-107">Requests with a start date greater than 90 days prior to the current date will receive a bad request exception (error code: 400) and an appropriate message.</span></span>

## <a name="retrieve-audit-records"></a><span data-ttu-id="50a28-108">Pobieranie rekordów inspekcji</span><span class="sxs-lookup"><span data-stu-id="50a28-108">Retrieve audit records</span></span>

<span data-ttu-id="50a28-109">Uzyskaj szczegółowe historyczne rekordy inspekcji operacji wykonywanych przez użytkownika lub aplikację partnera:</span><span class="sxs-lookup"><span data-stu-id="50a28-109">Get detailed historical audit records of operations performed by a partner user or application:</span></span>

- [<span data-ttu-id="50a28-110">Pobieranie rejestru aktywności w Centrum partnerskim</span><span class="sxs-lookup"><span data-stu-id="50a28-110">Get a record of Partner Center activity</span></span>](get-a-record-of-partner-center-activity-by-user.md)
- [<span data-ttu-id="50a28-111">Inspekcja zasobów</span><span class="sxs-lookup"><span data-stu-id="50a28-111">Auditing resources</span></span>](auditing-resources.md)