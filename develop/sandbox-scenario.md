---
title: Możliwości piaskownicy dla relacji odsprzedawcy
description: Piaskownica partnera ma możliwość obsługi relacji między partnerem a klientem
ms.date: 05/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 14133627a607c6e4151a90c37565e5f62823345e007eb55d87100de25d1f161a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996856"
---
# <a name="sandbox-capabilities-for-reseller-relationship"></a>Możliwości piaskownicy dla relacji odsprzedawcy

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

W tym artykule wyjaśniono, co jest obsługiwane w piaskownicy w przypadku relacji odsprzedawcy między partnerem a klientem. 

## <a name="prerequisites"></a>Wymagania wstępne

- Partner Center poświadczenia konta. Scenariusz piaskownicy obsługuje uwierzytelnianie zarówno przy użyciu autonomicznej aplikacji, jak i poświadczeń aplikacji i użytkownika.
- Identyfikator klienta (customer-tenant-id). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard/home). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta (customer-tenant-id).
- Wszystkie Azure Reserved Virtual Machine Instances i zamówienia zakupu oprogramowania muszą zostać anulowane przed usunięciem klienta z piaskownicy integracji Porada.

## <a name="scenarios-supporting-reseller-relationship"></a>Scenariusze obsługi relacji odsprzedawcy

1.  Partnerzy rozliczani bezpośrednio w piaskownicy i dostawcy pośredni mogą tworzyć relacje z klientem piaskownicy. 
2.  Partnerzy rozliczani bezpośrednio i dostawcy pośredni piaskownicy nie mogą zapraszać klientów piaskownicy.

3. Dostawcy pośredni i partner rozliczani bezpośrednio w piaskownicy mogą usunąć relację odsprzedawcy z interfejsu Partner Center i interfejsu API.

4. W przypadku relacji odsprzedawcy usunięcia piaskownicy zostanie wywołana nazwa Usuń klienta AP. Spowoduje to usunięcie relacji i dzierżawy klienta. {baseURL}/v1/Customers/{customer-Tenant-id}


    ### <a name="in-the-sandbox"></a>W piaskownicy

    **Partnerzy rozliczani bezpośrednio:**

    - Może dodawać istniejących klientów

    - Nie można zażądać relacji z nowymi klientami

    **Dostawcy pośredni:**

    - Może dodawać istniejących klientów

    - Nie można zażądać relacji z nowymi klientami

    - Nie można mieć relacji z odsprzedawcą pośrednim

    **Odsprzedawca pośredni:** 

    -   Może mieć relacje z istniejącymi klientami

    -   Nie można zażądać nowych relacji lub dodać nowych klientów

    ### <a name="in-partner-center"></a>W Partner Center

    **Partnerzy rozliczani bezpośrednio:**

    -   Może dodawać nowych klientów

    -   Może żądać relacji z nowymi klientami

    **Dostawcy pośredni:**

    -   Może dodawać nowych klientów

    -   Może żądać relacji z nowymi klientami

    -   Może mieć relacje z odsprzedawcami pośrednimi

    **Odsprzedawcy pośredni:**

    -   Nie można dodać nowych klientów

    -   Może żądać relacji z nowymi klientami


Aby uzyskać [szczegółowe informacje,](remove-a-reseller-relationship-with-a-customer.md) postępuj zgodnie z działem usuwania relacji odsprzedawcy dla klienta. Istnieją jednak pewne różnice między możliwościami produktów i piaskownicy.

### <a name="request-syntax"></a>SKŁADNIA ŻĄDANIA

|**Metoda**|**Usuwanie**|
|-------------|------------|
|Usuń|{baseURL}/v1/Customers/{customer-Tenant-id} |

Brak treści żądania

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](./error-codes.md)

## <a name="next-steps"></a>Następne kroki

- [Aktywowanie subskrypcji piaskownicy dla Azure Marketplace produktów](activate-sandbox-subscription-azure-marketplace-products.md)

- [Anulowanie zamówienia z piaskownicy](cancel-an-order-from-the-integration-sandbox.md)

- [Testowanie i debugowanie](test-and-debug.md)