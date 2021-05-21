---
title: Możliwości dostawcy pośredniego CSP w piaskownicy
description: Dostawcy pośredni mogą tworzyć pośrednich odsprzedawców w piaskownicy do celów testowych.
ms.date: 05/20/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vinayks-ms
ms.author: vinayks
ms.openlocfilehash: bd0f38103e6b6f93ab5da386042b00801b683ccd
ms.sourcegitcommit: 1aeaa12705a5945b8aab6bca254fedebd9c8bc4e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2021
ms.locfileid: "110244607"
---
# <a name="csp-indirect-provider-sandbox-capabilities-for-creating-indirect-reseller-accounts"></a>Możliwości piaskownicy dostawcy pośredniego CSP do tworzenia kont odsprzedawcy pośredniego 

**Dotyczy**

- Centrum partnerskie

**Odpowiednie role**

- Dostawca pośredni

Dostawcy pośredni dostawcy CSP mogą utworzyć konto CSP Indirect Reseller piaskownicy za pośrednictwem własnego konta piaskownicy warstwy 2 w Partner Center Portal.


## <a name="prerequisites"></a>Wymagania wstępne 

Partner Center piaskownicy dostawcy pośredniego (warstwa 2). Scenariusz piaskownicy obsługuje uwierzytelnianie zarówno przy użyciu autonomicznej aplikacji, jak i poświadczeń aplikacji i użytkownika. 
 

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a>Dostawca pośredni piaskownicy — tworzenie odsprzedawcy pośredniego piaskownicy przy Partner Center interfejsu użytkownika 

 Jest to funkcja piaskownicy, która umożliwia dostawcom pośrednim piaskownicy tworzenie konta odsprzedawcy pośredniego piaskownicy za pośrednictwem Partner Center portal.

Następujące scenariusze to, co dostawcy pośredni mogą zrobić dla odsprzedawców pośrednich w piaskownicy za pośrednictwem Partner Center interfejsu użytkownika: 

1. Dostawcy pośredni dostawcy CSP mogą utworzyć konto CSP Indirect Reseller piaskownicy za pośrednictwem własnego konta piaskownicy warstwy 2 w Partner Center Portal.
2. Odsprzedawcy pośredni w programie CSP mogą wyświetlać klientów według dostawców pośrednich. 

1. Odsprzedawcy pośredni programu CSP mogą zarządzać kontem klienta przy użyciu delegowanych uprawnień administratora.

1. Dostawcy pośredni dostawcy CSP mogą zapraszać pośrednich odsprzedawców CSP.
 
1. Dostawcy pośredni dostawcy CSP mogą usunąć konto CSP Indirect Reseller piaskownicy za pośrednictwem własnego konta piaskownicy warstwy 2 w Partner Center Portal.

    a.  Gdy dostawca pośredni piaskownicy usuwa relację z odsprzedawcą pośrednim piaskownicy.

    b.  Sprawdź, czy odsprzedawca pośredni ma jakiekolwiek inne relacje z innymi dostawcami. Jeśli tak, zostanie usunięta tylko relacja z tym konkretnym dostawcą pośrednim.

    c. Jeśli jest to jedyna relacja dla ir, to ir zostanie usunięte.

1. CSP Indirect Provider usunąć CSP Indirect Reseller.

    a. Jest to funkcja dostępna tylko w piaskownicy, która umożliwia dostawcom pośrednim piaskownicy usuwanie odsprzedawców pośrednich piaskownicy.
     
1. Wymagania wstępne dotyczące usuwania odsprzedawcy pośredniego piaskownicy:

    1. Wstrzymaj subskrypcje dla każdego klienta odsprzedawcy pośredniego piaskownicy.

    1. Usuń wszystkich klientów odsprzedawcy pośredniego.

1. Dozwolony limit 5 odsprzedawców pośrednich piaskownicy na dostawcę pośredniego piaskownicy. Po usunięciu odsprzedawcy pośredniego piaskownicy limit przydziału zostanie zresetowany.

### <a name="pre-requisites"></a>Wymagania wstępne

- Dozwolony limit 5 odsprzedawców pośrednich piaskownicy na dostawcę pośredniego piaskownicy. 

- Ten sam identyfikator MPN może służyć do tworzenia wielu kont piaskownicy odsprzedawcy pośredniego, jeśli kraj identyfikatora MPN i kraj piaskownicy odsprzedawcy pośredniego są takie same. Jeśli masz dostępny testowy identyfikator MPN, możesz go użyć lub uzyskać listę identyfikatorów MPN za pośrednictwem naszego kanału [usługi Yammer.]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ) Jeśli nie masz dostępu do usługi Yammer, usługa Yammer poprosi Cię o dostęp.
 
- Tylko 75 klientów jest dozwolonych na dostawcę pośredniego piaskownicy

## <a name="create-csp-indirect-reseller-sandbox-account"></a>Tworzenie CSP Indirect Reseller piaskownicy

1. Zaloguj się Partner Center za pośrednictwem konta piaskownicy warstwy 2. 

2. Przejdź do pozycji Odsprzedawcy pośredni z menu po lewej stronie. 

3. Kliknij przycisk "Dodaj piaskownicę odsprzedawcy". 

4. Wypełnij formularz rejestracji konta. Nie wymaga to wyjaśnień, ale pamiętaj, że tworzysz konto piaskownicy dla odsprzedawcy pośredniego. To konto nie zostanie poddane testowi i zostanie aktywowane zaraz po zakończeniu rejestracji konta.  

5. Po utworzeniu konta w portalu otrzymasz poświadczenia administratora globalnego dla konta piaskownicy Odsprzedawca pośredni. Pamiętaj, aby zapisać go natychmiast. W przeciwnym razie nie będzie można zalogować się jako piaskownica odsprzedawcy pośredniego. 

6. Wyloguj się i zaloguj się ponownie Partner Center przy użyciu nowych poświadczeń dla piaskownicy odsprzedawcy pośredniego. Poznaj możliwości, które możesz wykonać jako odsprzedawca pośredni. Niektóre z nich to:  

    - Zarządzanie profilami  

    - Zarządzanie użytkownikami i rolami 

    - Zarządzanie dostawcami pośrednimi 

    - Zarządzanie klientami piaskownicy CSP 

    - Zarządzanie relacjami
    
     
## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a>Dostawca pośredni piaskownicy — usuwanie odsprzedawcy pośredniego piaskownicy przy Partner Center interfejsu użytkownika

 Jest to funkcja dostępna tylko w piaskownicy, która umożliwia dostawcom pośrednim piaskownicy usuwanie istniejącego konta odsprzedawcy pośredniego piaskownicy za pośrednictwem Partner Center portalu. 

### <a name="pre-requisites-to-delete-sandbox-indirect-reseller"></a>Wymagania wstępne usunięcia odsprzedawcy pośredniego piaskownicy:

Istniejące konto CSP Indirect Reseller piaskownicy skojarzone z Twoim własnym kontem CSP Indirect Provider piaskownicy warstwy 2.  
 

## <a name="delete-csp-indirect-reseller-sandbox-account"></a>Usuwanie CSP Indirect Reseller piaskownicy

1. Zaloguj się Partner Center przy użyciu konta piaskownicy warstwy 2. 

2. Przejdź do pozycji Odsprzedawcy pośredni z menu po lewej stronie. 

3. Kliknij link **Usuń piaskownicę odsprzedawcy** obok konta piaskownicy odsprzedawcy pośredniego, które chcesz usunąć. Konto piaskownicy odsprzedawcy pośredniego zostanie trwale usunięte i nie będzie można go odzyskać. 

## <a name="api-references"></a>Dokumentacja interfejsu API

- Tworzenie odsprzedawcy pośredniego 
- Usuwanie odsprzedawcy pośredniego 

 

 