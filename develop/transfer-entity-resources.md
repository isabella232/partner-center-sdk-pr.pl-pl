---
title: Zasoby TransferEntity
description: Partner tworzy przeniesienie, gdy klient chce, aby jego subskrypcja została przeniesiona do innego partnera.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 544b9682bb0e1428fad088c818a62492198897b2
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530144"
---
# <a name="transferentity-resources"></a>Zasoby TransferEntity

Partner tworzy przeniesienie, gdy klient chce, aby jego subskrypcja została przeniesiona do innego partnera.

## <a name="transferentity"></a>TransferEntity

Opisuje transferEntity.

| Właściwość              | Typ             | Opis                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| identyfikator                    | ciąg           | Identyfikator transferEntity, który jest dostarczany po pomyślnym utworzeniu obiektu transferEntity.                               |
| createdTime (czas utworzenia)           | DateTime         | Data utworzenia przeniesieniaJedność w formacie daty i godziny. Stosowane po pomyślnym utworzeniu transferEntity.      |
| lastModifiedTime      | DateTime         | Data ostatniej aktualizacji transakcji transferEntity w formacie daty i godziny. Stosowane po pomyślnym utworzeniu transferEntity. |
| lastModifiedUser      | ciąg           | Użytkownik, który ostatnio zaktualizował transferEntity. Stosowane po pomyślnym utworzeniu transferEntity.                          |
| Customername          | ciąg           | Opcjonalny. Nazwa klienta, którego subskrypcje są przenoszone.                                              |
| customerTenantId      | ciąg           | Identyfikator GUID sformatowany jako identyfikator klienta, który identyfikuje klienta. Stosowane po pomyślnym utworzeniu transferEntity.         |
| partnertenantid       | ciąg           | Identyfikator GUID sformatowany jako identyfikator partnera, który identyfikuje partnera.                                                                   |
| sourcePartnerName (Nazwa partycji źródłowej)     | ciąg           | Opcjonalny. Nazwa organizacji partnera, który inicjuje przeniesienie.                                           |
| sourcePartnerTenantId | ciąg           | Identyfikator GUID sformatowany jako identyfikator partnera, który identyfikuje partnera inicjujące przeniesienie.                                           |
| targetPartnerName (nazwa_serwera_docelowego)     | ciąg           | Opcjonalny. Nazwa organizacji partnera, której celem jest przeniesienie.                                         |
| targetPartnerTenantId | ciąg           | Identyfikator GUID sformatowany jako partner-id, który identyfikuje partnera, do którego jest skierowany transfer.                                  |
| lineItems             | Tablica obiektów | Tablica zasobów [TransferLineItem.](#transferlineitem)                                                   |
| status                | ciąg           | Stan transferEntity. Możliwe wartości to "Aktywne" (można je usunąć/przesłać) i "Ukończono" (zostało już zakończone). Stosowane po pomyślnym utworzeniu transferEntity.|

## <a name="transferlineitem"></a>TransferLineItem

Reprezentuje jeden element zawarty w transferEntity.

| Właściwość             | Typ                             | Opis                                                                                             |
|----------------------|----------------------------------|---------------------------------------------------------------------------------------------------------|
| identyfikator                   | ciąg                           | Unikatowy identyfikator elementu wiersza przeniesienia. Stosowane po pomyślnym utworzeniu transferEntity.   |
| subscriptionId       | ciąg                           | Identyfikator subskrypcji.                                                                            |
| quantity             | int                              | Liczba licencji lub wystąpień.                                                                    |
| billingCycle         | Obiekt                           | Typ cyklu rozliczeniowego ustawiony dla bieżącego okresu.                                                   |
| Friendlyname         | ciąg                           | Opcjonalny. Przyjazna nazwa elementu zdefiniowanego przez partnera w celu uujednoznania.                   |
| partnerIdOnRecord    | ciąg                           | PartnerId on Record (MPNID) przy zakupie, który ma miejsce po zaakceptowaniu przeniesienia.                 |
| offerId              | ciąg                           | Identyfikator oferty.    |
| addonItems           | Lista obiektów **TransferLineItem** | Kolekcja elementów wiersza transferEntity dla dodatków, które zostaną przeniesione wraz z subskrypcją podstawową, która jest przesyłana. Stosowane po pomyślnym utworzeniu transferEntity.|
| transferError        | ciąg                           | Stosowane po transferEntity jest akceptowana w przypadku błędu.                |
| status               | ciąg           | Stan lineitem w transferEntity.|

## <a name="transfersubmitresult"></a>TransferSubmitResult

Reprezentuje wynik przeniesienia zaakceptować.

| Właściwość          | Typ                                                  | Opis                        |
|-------------------|-------------------------------------------------------|------------------------------------|
| orders            | Lista [obiektów Order.](order-resources.md#order)    | Kolekcja zamówień.          |
| transferErrors    | Lista [obiektów TransferError.](#transfererror)      | Kolekcja błędów transferu. |

## <a name="transfererror"></a>TransferError

Reprezentuje błąd, który występuje po zaakceptowaniu transferu.

| Właściwość          | Typ   | Opis                                     |
|-------------------|--------|-------------------------------------------------|
| transferGroupId   | ciąg | Identyfikator grupy zamówień zamówienia z błędem. |
| kod              | int    | Kod błędu.                                 |
| description (opis)       | ciąg | Opis błędu.                   |
| lineItems         | Lista obiektów **TransferLineItem** | Kolekcja elementów wiersza transferEntity, które są częścią błędu transferu.|

## <a name="transfererrorcode"></a>TransferErrorCode

Element [Enum/dotnet/api/system.enum) z wartościami wskazującymi typ błędu zamówienia.

| Wartość | Położenie | Opis |
| --- | --- | --- |
| PartnerTokenMissing | 800001 | Brak tokenu partnera w kontekście żądania. |
| InvalidInput | 800002 | Nieprawidłowe dane wejściowe żądania. |
| ServiceException | 800003 | Nieoczekiwany błąd usługi. |
| InvalidOfferId | 800004 | Nieprawidłowy identyfikator oferty. |
| CreateOrderError | 800005 | Tworzenie zamówienia nie powiodło się. |
| MpnIdNotFound | 800015 | Nie znaleziono identyfikatora MPN. |
| NotValidIndirectResellerMpnId | 800016 | Identyfikator MPN nie jest prawidłowym odsprzedawcą pośrednim. |
| TransferIdNotFound | 900100   | Nie znaleziono żądania przeniesienia.   |
| TransferNotAllowedIfStatusIsInProgress | 900101 | Żądanie przeniesienia jest już w toku.|
| TransferNotAllowedIfStatusIsCompleted | 900102 | Żądanie przeniesienia jest już ukończone.|
| TransferCreateOrderError | 900103 | Zamówienie przeniesienia nie powiodło się.|
| TransferProcessedByAnotherRequest | 900104 | Transfer jest przetwarzany przez inne żądanie.|