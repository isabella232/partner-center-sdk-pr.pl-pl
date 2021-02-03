---
title: Zasoby TransferEntity
description: Partner tworzy transfer, gdy klient chce, aby jego subskrypcja była przenoszona do innego partnera.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 96c43d255fcd31e6dc4de50baa0e19f5d8855685
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768021"
---
# <a name="transferentity-resources"></a>Zasoby TransferEntity

**Dotyczy:**

- Centrum partnerskie

Partner tworzy transfer, gdy klient chce, aby jego subskrypcja była przenoszona do innego partnera.

## <a name="transferentity"></a>TransferEntity

Opisuje transferEntity.

| Właściwość              | Typ             | Opis                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| identyfikator                    | ciąg           | Identyfikator transferEntity, który jest dostarczany po pomyślnym utworzeniu transferEntity.                               |
| createdTime           | DateTime         | Data, w której utworzono transferEntity, w formacie daty i godziny. Stosowane po pomyślnym utworzeniu transferEntity.      |
| lastModifiedTime      | DateTime         | Data ostatniej aktualizacji transferEntity w formacie daty i godziny. Stosowane po pomyślnym utworzeniu transferEntity. |
| lastModifiedUser      | ciąg           | Użytkownik, który ostatnio zaktualizował transferEntity. Stosowane po pomyślnym utworzeniu transferEntity.                          |
| customerName          | ciąg           | Opcjonalny. Nazwa klienta, którego subskrypcje są transferowane.                                              |
| customerTenantId      | ciąg           | Identyfikator GUID sformatowany przez klienta, który identyfikuje klienta. Stosowane po pomyślnym utworzeniu transferEntity.         |
| partnertenantid       | ciąg           | Identyfikator GUID w formacie identyfikatora partnera, który identyfikuje partnera.                                                                   |
| sourcePartnerName     | ciąg           | Opcjonalny. Nazwa organizacji partnera, która inicjuje transfer.                                           |
| sourcePartnerTenantId | ciąg           | Identyfikator GUID w formacie identyfikatora partnera, który identyfikuje partnera inicjującego transfer.                                           |
| targetPartnerName     | ciąg           | Opcjonalny. Nazwa organizacji partnera, do której przeznaczony jest transfer.                                         |
| targetPartnerTenantId | ciąg           | Identyfikator partnera w formacie GUID, który identyfikuje partnera, do którego jest przeznaczony transfer.                                  |
| lineItems             | Tablica obiektów | Tablica zasobów [TransferLineItem](#transferlineitem) .                                                   |
| status                | ciąg           | Stan transferEntity. Możliwe wartości to "Active" (można je usunąć/przesłać) i "ukończone" (zostały już ukończone). Stosowane po pomyślnym utworzeniu transferEntity.|

## <a name="transferlineitem"></a>TransferLineItem

Reprezentuje jeden element zawarty w transferEntity.

| Właściwość             | Typ                             | Opis                                                                                             |
|----------------------|----------------------------------|---------------------------------------------------------------------------------------------------------|
| identyfikator                   | ciąg                           | Unikatowy identyfikator elementu wiersza przeniesienia. Stosowane po pomyślnym utworzeniu transferEntity.   |
| subscriptionId       | ciąg                           | Identyfikator subskrypcji.                                                                            |
| quantity             | int                              | Liczba licencji lub wystąpień.                                                                    |
| billingCycle         | Obiekt                           | Typ cyklu rozliczeniowego ustawiony dla bieżącego okresu.                                                   |
| friendlyName         | ciąg                           | Opcjonalny. Przyjazna nazwa dla elementu zdefiniowanego przez partnera, która pomaga w odróżnieniu od siebie.                   |
| partnerIdOnRecord    | ciąg                           | PartnerId on Record (MPNID) zakupu, który ma miejsce, gdy transfer zostanie zaakceptowany.                 |
| offerId              | ciąg                           | Identyfikator oferty.    |
| addonItems           | Lista obiektów **TransferLineItem** | Kolekcja elementów transferEntity line dla dodatków, które będą transferowane wraz z subskrypcją podstawową, która jest transferowana. Stosowane po pomyślnym utworzeniu transferEntity.|
| transferError        | ciąg                           | Stosowane po zaakceptowaniu transferEntity w przypadku błędu.                |
| status               | ciąg           | Stan LineItem w transferEntity.|

## <a name="transfersubmitresult"></a>TransferSubmitResult

Reprezentuje wynik zaakceptowania transferu.

| Właściwość          | Typ                                                  | Opis                        |
|-------------------|-------------------------------------------------------|------------------------------------|
| orders            | Lista obiektów [kolejności](order-resources.md#order) .    | Kolekcja zamówień.          |
| transferErrors    | Lista obiektów [TransferError](#transfererror) .      | Kolekcja błędów transferu. |

## <a name="transfererror"></a>TransferError

Reprezentuje błąd występujący po zaakceptowaniu transferu.

| Właściwość          | Typ   | Opis                                     |
|-------------------|--------|-------------------------------------------------|
| transferGroupId   | ciąg | Identyfikator grupy kolejności z błędem. |
| kod              | int    | Kod błędu.                                 |
| description (opis)       | ciąg | Opis błędu.                   |
| lineItems         | Lista obiektów **TransferLineItem** | Kolekcja elementów wiersza transferEntity, które są częścią błędu transferu.|

## <a name="transfererrorcode"></a>TransferErrorCode

[Enum/dotnet/API/System. enum) z wartościami, które wskazują typ błędu zamówienia.

| Wartość | Położenie | Opis |
| --- | --- | --- |
| PartnerTokenMissing | 800001 | Brak tokenu partnera w kontekście żądania. |
| InvalidInput | 800002 | Nieprawidłowe dane wejściowe żądania. |
| ServiceException | 800003 | Nieoczekiwany błąd usługi. |
| InvalidOfferId | 800004 | Nieprawidłowy identyfikator oferty. |
| CreateOrderError | 800005 | Tworzenie zamówienia nie powiodło się. |
| MpnIdNotFound | 800015 | Nie znaleziono identyfikatora MPN. |
| NotValidIndirectResellerMpnId | 800016 | Identyfikator MPN nie jest prawidłowym odsprzedawcą pośrednią. |
| TransferIdNotFound | 900100   | Nie znaleziono żądania transferu.   |
| TransferNotAllowedIfStatusIsInProgress | 900101 | Żądanie transferu jest już w toku.|
| TransferNotAllowedIfStatusIsCompleted | 900102 | Żądanie transferu zostało już zakończone.|
| TransferCreateOrderError | 900103 | Zamówienie transferu nie powiodło się.|
| TransferProcessedByAnotherRequest | 900104 | Transfer jest przetwarzany przez inne żądanie.|