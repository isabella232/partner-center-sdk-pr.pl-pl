---
title: Inspekcja zasobów
description: Dowiedz się Partner Center zasobów inspekcji interfejsu API, takich jak AuditRecord, których można użyć do uzyskania rekordu Partner Center aktywności.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 50c90f7e7a5dfb274044fafab87818c7ac8428124ca9072770cc5fd9fa3806d5
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994663"
---
# <a name="auditing-resources-that-help-you-get-a-record-of-partner-center-activity"></a>Inspekcja zasobów, które ułatwiają uzyskiwanie rekordu Partner Center aktywności

Z operacjami inspekcji można używać następujących zasobów.

## <a name="auditrecord"></a>AuditRecord

Reprezentuje rekord operacji wykonywanej przez użytkownika lub aplikację partnera.

| Właściwość | Typ | Opis |
| --- | --- | ---|
| customerId | ciąg | Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta. |
| Customername | ciąg | Nazwa klienta. |
| userPrincipalName | ciąg | Główna nazwa użytkownika lub identyfikator użytkownika. Zazwyczaj ta właściwość to nazwa logowania użytkownika w stylu Internetu w formacie adresu e-mail opartym na standardzie internetowym RFC 822. |
| applicationId | ciąg | Ciąg identyfikujący aplikację, która wykonała operację. |
| resourceType | ciąg | Typ zasobu, na których działa operacja. Możliwe wartości: `customer` , , , , , , , , `customer_user` , , `order` , , , `subscription` , `license` `third_party_add_on` `mpn_association` `transfer` `application` `application_credential` `partner_user` `partner_relationship` `partner_customer_dap` `customer_directory_role` . |
| resourceOldValue | ciąg | Stara wartość zasobu. |
| resourceNewValue | ciąg | Nowa wartość zasobu. |
| operationType | ciąg | Typ wykonanej operacji. Możliwe wartości: , , , , , , (tylko konta integracji `update_customer_qualification` `update_subscription` `upgrade_subscription` `convert_trial_subscription` `add_customer` `update_customer_billing_profile` `update_customer_partner_contract_company_name` `update_customer_spending_budget` `delete_customer` piaskownicy), `remove_partner_customer_relationship` , `create_order` , `update_order` `create_customer_user` `delete_customer_user` `update_customer_user` `update_customer_user_licenses` `reset_customer_user_password` `update_customer_user_principal_name` `restore_customer_user` `create_mpn_association` `update_mpn_association` `update_sfb_customer_user_licenses` `update_transfer` `create_partner_relationship` `register_application` `unregister_application` `add_application_credential` `remove_application_credential` `create_partner_user` `update_partner_user` `create_self_serve_policy` `update_self_serve_policy` , `create_self_serve_policy` `delete_self_serve_policy` `remove_partner_relationship` , , , , `delete_tip_customer` `create_related_referral` , `update_related_referral` `create_referral` , `update_referral` `get_software_key` , `get_software_download_link` `increase_spending_limit` , `ready_invoice` `create_agreement` `extend_relationship` `create_transfer` `dap_admin_relationship_approved` `dap_admin_relationship_terminated` `add_user_member` `remove_user_member` . |
| operationDate | ciąg w formacie daty i godzin UTC | Data i godzina wykonania operacji. |
| operationStatus | ciąg | Stan inspekcji operacji. Możliwe wartości: `succeeded` , lub , co `failed` `progress` oznacza, że operacja jest nadal w toku. |
| customizedData  | tablica obiektów | Dodatkowe informacje. Każdy obiekt zawiera dwie pary klucz-wartość JSON: pierwsza to i wartość ciągu, druga `key` to i wartość `value` ciągu. Liczba obiektów w tablicy zależy od typu wykonanej operacji. |
| atrybuty | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych. |
