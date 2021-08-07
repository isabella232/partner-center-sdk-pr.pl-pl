---
title: Zasoby TransferEntity
description: Partner tworzy przeniesienie, gdy klient chce, aby jego subskrypcja została przeniesiona do innego partnera.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3103c0e9f8e6850336d663a5a38274ce7391e30edd433d08f44071de31b5fc5e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990209"
---
# <a name="transferentity-resources"></a>Zasoby TransferEntity

Partner tworzy przeniesienie, gdy klient chce, aby jego subskrypcja została przeniesiona do innego partnera.

## <a name="transferentity"></a>TransferEntity

Opisuje transferEntity.

| Właściwość              | Typ             | Opis                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| identyfikator                    | ciąg           | Identyfikator transferEntity, który jest dostarczany po pomyślnym utworzeniu obiektu transferEntity.                               |
| createdTime           | DateTime         | Data utworzenia przeniesieniaJednoczność w formacie daty i godziny. Stosowane po pomyślnym utworzeniu transferEntity.      |
| lastModifiedTime      | DateTime         | Data ostatniej aktualizacji transferEntity w formacie daty i godziny. Stosowane po pomyślnym utworzeniu transferEntity. |
| lastModifiedUser      | ciąg           | Użytkownik, który ostatnio zaktualizował transferEntity. Stosowane po pomyślnym utworzeniu wartości transferEntity.                          |
| Customername          | ciąg           | Opcjonalny. Nazwa klienta, którego subskrypcje są przenoszone.                                              |
| customerTenantId      | ciąg           | Identyfikator klienta sformatowany w formacie GUID, który identyfikuje klienta. Stosowane po pomyślnym utworzeniu transferEntity.         |
| partnertenantid       | ciąg           | Identyfikator GUID sformatowany jako partner-id, który identyfikuje partnera.                                                                   |
| sourcePartnerName     | ciąg           | Opcjonalny. Nazwa organizacji partnera, który inicjuje przeniesienie.                                           |
| sourcePartnerTenantId | ciąg           | Identyfikator GUID sformatowany jako partner-id, który identyfikuje partnera inicjatora transferu.                                           |
| targetPartnerName     | ciąg           | Opcjonalny. Nazwa organizacji partnera, do której jest skierowane przeniesienie.                                         |
| targetPartnerTenantId | ciąg           | Identyfikator PARTNERA sformatowany identyfikator GUID, który identyfikuje partnera, do którego jest celem transferu.                                  |
| lineItems             | Tablica obiektów | Tablica [zasobów TransferLineItem.](#transferlineitem)                                                   |
| status                | ciąg           | Stan transferEntity. Możliwe wartości to "Aktywne" (można je usunąć/przesłać) i "Ukończono" (zostały już ukończone). Stosowane po pomyślnym utworzeniu transferEntity.|

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
| transferError        | ciąg                           | Zastosowane po zaakceptowaniu wartości transferEntity w przypadku błędu.                |
| status               | ciąg           | Stan lineitem w transferEntity.|

## <a name="transfersubmitresult"></a>TransferSubmitResult

Reprezentuje wynik akceptacji przeniesienia.

| Właściwość          | Typ                                                  | Opis                        |
|-------------------|-------------------------------------------------------|------------------------------------|
| orders            | Lista obiektów [Order.](order-resources.md#order)    | Kolekcja zamówień.          |
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