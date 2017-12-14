---
title: "Ändern des Kontos für die Scale Out-Protokollierung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dcedbe0d2c2ef2c2089af1e2a8b31fbeb75ce2fc
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="change-the-account-for-scale-out-logging"></a>Ändern des Kontos für die Scale Out-Protokollierung
Beim Ausführen von Paketen in Scale Out werden die Ereignismeldungen mit einem automatisch erstellten Benutzer **##MS_SSISLogDBWorkerAgentLogin##** in SSISDB gespeichert. Bei der Anmeldung dieses Benutzers wird die SQL Server-Authentifizierung verwendet. Um das Konto zu ändern, gehen Sie mit folgenden Schritten vor:

## <a name="1-create-a-user-of-ssisdb"></a>1. Erstellen eines SSISDB-Benutzers
Anweisungen zum Erstellen eines Datenbankbenutzers finden Sie unter [Erstellen eines Datenbankbenutzers](../../relational-databases/security/authentication-access/create-a-database-user.md).

## <a name="2-add-the-user-to-database-role-ssisclusterworker"></a>2. Hinzufügen des Benutzers zur Datenbankrolle „ssis_cluster_worker“

Anweisungen zum Verknüpfen einer Datenbankrolle finden Sie unter [Verknüpfen einer Rolle](../../relational-databases/security/authentication-access/join-a-role.md).

## <a name="3-update-logging-information-in-ssisdb"></a>3. Aktualisieren der Protokollierungsinformationen in SSISDB 
Rufen Sie die gespeicherte Prozedur [catalog].[update_logdb_info] mit SQL Server-Name und Verbindungszeichenfolge als Parameter auf.

#### <a name="example"></a>Beispiel
```sql
SET @serverName = CONVERT(sysname, SERVERPROPERTY('servername'))
SET @connectionString = 'Data Source=' + @serverName + ';Initial Catalog=SSISDB;Integrated Security=SSPI;'
EXEC [internal].[update_logdb_info] @serverName, @connectionString
GO
```

## <a name="4-restart-scale-out-worker-service"></a>4. Neustarten des Diensts Scale Out-Worker

> [!NOTE]
> Wenn Sie ein Windows-Benutzerkonto für die Protokollierung verwenden, muss es dasselbe Konto sein, dass den Scale Out-Worker-Dienst ausführt. Andernfalls tritt bei der Anmeldung bei SQL Server ein Fehler auf.
