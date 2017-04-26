---
title: Konfigurieren kompatibler SQL Server-Features mit Stretch-Datenbank | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c8121ede-1aec-459b-b7b0-1408bb3e62fb
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 84464c4553eab6d8e65c0bf6b476ae728e2a8463
ms.lasthandoff: 04/11/2017

---
# <a name="configure-compatible-sql-server-features-with-stretch-database"></a>Konfigurieren kompatibler SQL Server-Features mit Stretch-Datenbank
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Führen Sie einfache Schritte aus, um die folgenden SQL Server-Features für die Arbeit mit Stretch-Datenbank zu konfigurieren.
-   Always On
-   Always Encrypted
-   Transparente Datenverschlüsselung (TDE)
-   Temporale Tabellen

## <a name="configure-always-on-with-stretch-database"></a>Konfigurieren von Always On mit Stretch-Datenbank
Wenn Sie Always On mit Stretch-Datenbank verwenden, müssen Sie sicherstellen, dass der Datenbank-Hauptschlüssel auf den sekundären Replikaten verfügbar ist. Stretch-Datenbank verwendet den Datenbank-Hauptschlüssel zum Sichern der Anmeldeinformationen, die für die Verbindung mit der Azure-Remotedatenbank verwendet werden.

Nachdem Sie die Always On-Verfügbarkeitsgruppe eingerichtet haben, führen Sie die gespeicherte Prozedur **sp_control_dbmasterkey_password** auf jedem sekundären Replikat aus, und stellen Sie das Kennwort für die Stretch-fähige Datenbank bereit. Weitere Informationen und Beispiele finden Sie unter [sp_control_dbmasterkey_password](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md). 

## <a name="configure-always-encrypted-with-stretch-database"></a>Konfigurieren von Always Encrypted mit Stretch-Datenbank
Wenn Sie Always Encrypted und Stretch-Datenbank zusammen verwenden möchten, müssen Sie die Verschlüsselung für die ausgewählten Spalten konfigurieren, bevor Sie Stretch-Datenbank für die Tabelle aktivieren.

Wenn Sie Stretch-Datenbank für die Tabelle bereits aktiviert haben und Sie Always Encrypted-Spalten verwenden möchten, müssen Sie die folgenden Schritte ausführen.
1.   Deaktivieren Sie Stretch-Datenbank für die Tabelle, und holen Sie die Remotedaten aus Azure zurück. Weitere Informationen finden Sie unter [Deaktivieren von Stretch-Datenbank und Zurückholen von Remotedaten](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md).
2.   Konfigurieren Sie Always Encrypted für die ausgewählten Spalten.
3. Aktivieren Sie Stretch-Datenbank für die Tabelle erneut. Weitere Informationen finden Sie unter [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md).

## <a name="configure-transparent-data-encryption-tde-with-stretch-database"></a>Konfigurieren der transparenten Datenverschlüsselung (TDE) mit Stretch-Datenbank

Wenn TDE für die lokale Datenbank aktiviert ist, wird sie auf dem Remoteendpunkt für Stretch-Datenbank nicht automatisch aktiviert. Sie müssen daran denken, dass Sie TDE für den Remoteendpunkt aktivieren, nachdem Sie Stretch für Ihre Datenbank aktiviert haben.

## <a name="configure-temporal-tables-with-stretch-database"></a>Konfigurieren temporaler Tabellen mit Stretch-Datenbank
Wenn Sie temporale Tabellen verwenden, können Sie Stretch-Datenbank für die Verlaufstabelle, aber nicht für die aktuelle Tabelle aktivieren.
-   Hinweise zur Verwendung von temporalen Tabellen mit Stretch-Datenbank finden Sie unter [Verwalten der Beibehaltung von Verlaufsdaten in temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md).
-   Informationen zum Filtern von Zeilen für die Migration aus der Verlaufstabelle mithilfe von gleitenden Fenstern finden Sie unter [Auswählen zu migrierender Zeilen mithilfe einer Filterfunktion](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).
