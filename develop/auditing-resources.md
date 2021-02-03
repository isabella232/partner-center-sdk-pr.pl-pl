---
title: Inspekcja zasobów
description: Dowiedz się więcej o zasobach inspekcji usługi Partner Center, takich jak AuditRecord, których możesz użyć do pobrania rekordu działania Centrum partnerskiego.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c4b39cbc4d69447fbc8e6ef4528dd6dce11cd3f4
ms.sourcegitcommit: fa183a942f51cab8bdb42dbe7da4c8eab550e0a0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2021
ms.locfileid: "98759179"
---
# <a name="auditing-resources-that-help-you-get-a-record-of-partner-center-activity"></a>Inspekcja zasobów, które pomagają uzyskać rekord działania Centrum partnerskiego

**Dotyczy:**

- Centrum partnerskie

Można użyć następujących zasobów z operacjami inspekcji.

## <a name="auditrecord"></a>AuditRecord

Reprezentuje rekord operacji wykonywanej przez użytkownika lub aplikację partnera.

| Właściwość | Typ | Opis |
| --- | --- | ---|
| customerId | ciąg | Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta. |
| customerName | ciąg | Nazwa klienta. |
| userPrincipalName | ciąg | Główna nazwa użytkownika lub identyfikator użytkownika. Zazwyczaj ta właściwość jest nazwą logowania użytkownika w stylu internetowym w formacie adresu e-mail, na podstawie standardu Internet RFC 822. |
| applicationId | ciąg | Ciąg identyfikujący aplikację, która wykonała operację. |
| resourceType | ciąg | Typ zasobu, na który należy wykonać operację. Możliwe wartości:,,,,,,,,, `customer` `customer_user` ,, `order` `subscription` `license` `third_party_add_on` `mpn_association` `transfer` `application` `application_credential` `partner_user` `partner_relationship` , `partner_customer_dap` . |
| resourceOldValue | ciąg | Stara wartość zasobu. |
| resourceNewValue | ciąg | Nowa wartość zasobu. |
| operationType | ciąg | Typ wykonywanej operacji. Możliwe wartości:,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,, `update_customer_qualification` `update_subscription` `upgrade_subscription` `convert_trial_subscription` `add_customer` `update_customer_billing_profile` `update_customer_partner_contract_company_name` `update_customer_spending_budget` `delete_customer` `remove_partner_customer_relationship` `create_order` `update_order` `create_customer_user` `delete_customer_user` `update_customer_user` `update_customer_user_licenses` `reset_customer_user_password` `update_customer_user_principal_name` `restore_customer_user` `create_mpn_association` `update_mpn_association` `update_sfb_customer_user_licenses` `update_transfer` `create_partner_relationship` `register_application` `unregister_application` `add_application_credential` `remove_application_credential` `create_partner_user` `update_partner_user` `create_self_serve_policy` `update_self_serve_policy` `create_self_serve_policy` `delete_self_serve_policy` `remove_partner_relationship` `delete_tip_customer` `create_related_referral` `update_related_referral` `create_referral` `update_referral` `get_software_key` `get_software_download_link` `increase_spending_limit` `ready_invoice` `create_agreement` `extend_relationship` `create_transfer` `dap_admin_relationship_approved` `dap_admin_relationship_terminated` . |
| operationDate | ciąg w formacie daty i godziny UTC | Data i godzina wykonania operacji. |
| operationStatus | ciąg | Stan inspekcji operacji. Możliwe wartości: `succeeded` , `failed` , lub `progress` , co oznacza, że operacja jest nadal w toku. |
| customizedData  | Tablica obiektów | Dodatkowe informacje. Każdy obiekt zawiera dwie pary klucz-wartość JSON: pierwszy to `key` i wartość ciągu, sekunda `value` i wartość ciągu. Liczba obiektów w tablicy zależy od typu wykonywanej operacji. |
| atrybuty | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych. |
