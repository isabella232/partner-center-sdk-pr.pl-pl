---
title: Możliwości piaskownicy partnera obsługujące relację odsprzedawcy
description: Piaskownica partnerów ma możliwość obsługi relacji między partnerem a klientem
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: af46811b3615e1f904a9619de85b0aca7622490b
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711869"
---
# <a name="partner-sandbox-capabilities-that-support-reseller-relationship"></a>Możliwości piaskownicy partnera obsługujące relację odsprzedawcy

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

W tym artykule wyjaśniono, co jest obsługiwane w piaskownicy dla relacji odsprzedawcy między partnerem a klientem. 

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia konta Centrum partnerskiego. Scenariusz piaskownicy obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznej, jak i aplikacji oraz poświadczeń użytkownika.
- Identyfikator klienta (identyfikator dzierżawy klienta). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard/home)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta (identyfikator dzierżawy klienta).
- Wszystkie Azure Reserved Virtual Machine Instances i zamówienia zakupu oprogramowania muszą zostać anulowane przed usunięciem klienta z piaskownicy integracji z poradami.

## <a name="scenarios-supporting-reseller-relationship"></a>Scenariusze obsługujące relację odsprzedawcy

1.  Bezpośredni partnerzy rozliczeń i dostawcy pośredniego w piaskownicy mogą tworzyć relacje z klientem piaskownicy. 
2.  Bezpośredni partnerzy rachunków w piaskownicy i dostawcy pośrednii nie mogą zapraszać klientów w piaskownicy.



### <a name="in-the-sandbox"></a>W piaskownicy

**Bezpośredni partnerzy Bill**:

• Może dodawać istniejących klientów

• Nie można zażądać relacji z nowymi klientami

**Dostawcy Pośrednii**:

• Może dodawać istniejących klientów

• Nie można zażądać relacji z nowymi klientami

• Nie może mieć relacji z odsprzedawcą pośrednią

**Pośredni odsprzedawca**: (wkrótce)

• Mogą mieć relacje z istniejącymi klientami

• Nie można zażądać nowych relacji lub dodać nowych klientów

### <a name="in-partner-center"></a>W centrum partnerskim

**Bezpośredni partnerzy Bill**:

• Może dodawać nowych klientów

• Może zażądać relacji z nowymi klientami

**Dostawcy Pośrednii**:

• Może dodawać nowych klientów

• Może zażądać relacji z nowymi klientami

• Mogą mieć relacje z pośrednimi odsprzedawcami

**Odsprzedawcy Pośrednii**:

• Nie można dodać nowych klientów

• Może zażądać relacji z nowymi klientami

3. Bezpośredni partner rozliczeń i dostawcy pośredniego w piaskownicy mogą usunąć relację odsprzedawcy z interfejsu użytkownika i interfejsu API Centrum partnerskiego.

4. Relacja usuwania odsprzedawcy z piaskownicy spowoduje wywołanie usuwania AP klienta. Spowoduje to usunięcie relacji, a także usunięcie dzierżawy klienta. {baseURL}/v1/Customers/{customer-Tenant-id}

Aby uzyskać szczegółowe informacje, Skorzystaj z [relacji usuwanie odsprzedawcy](remove-a-reseller-relationship-with-a-customer.md) dla klienta. Istnieją jednak pewne różnice między możliwościami produktu i piaskownicy.

### <a name="request-syntax"></a>SKŁADNIA ŻĄDANIA

|**Metoda**|**Usuwanie**|
|-------------|------------|
|Usuń|{baseURL}/v1/Customers/{customer-Tenant-id} |

Treść żądania nie

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](./error-codes.md).

## <a name="next-steps"></a>Następne kroki

- [Aktywuj subskrypcje piaskownicy dla produktów portalu Azure Marketplace](activate-sandbox-subscription-azure-marketplace-products.md)

- [Anulowanie zamówienia z piaskownicy](cancel-an-order-from-the-integration-sandbox.md)

- [Testowanie i debugowanie](test-and-debug.md)