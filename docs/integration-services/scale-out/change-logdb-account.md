---
title: "Ändern des Kontos für horizontales Skalieren SSIS-Protokollierung | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ec785459e5f9585776d83cde3f460c1e79367e46
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="change-the-account-for-scale-out-logging"></a>Ändern des Kontos für horizontales Skalieren Protokollierung
Beim Ausführen von Paketen in horizontal skalieren, werden die ereignismeldungen in der SSISDB mit einem automatisch erstellten Benutzer protokolliert **"# MS_SSISLogDBWorkerAgentLogin"**. Die Anmeldung dieses Benutzers verwendet SQL Server-Authentifizierung. So ändern Sie das Konto, folgt die folgenden Schritte aus:

## <a name="1-create-a-user-of-ssisdb"></a>1. Erstellen Sie einen Benutzer der SSISDB
Anweisungen zum Erstellen eines Datenbankbenutzers, finden Sie unter [Erstellen eines Datenbankbenutzers](../../relational-databases/security/authentication-access/create-a-database-user.md).

## <a name="2-add-the-user-to-database-role-ssisclusterworker"></a>2. Hinzufügen des Benutzers zur Datenbank Rolle ssis_cluster_worker

Anleitungen Verknüpfung von einer Datenbankrolle finden Sie unter [Verknüpfen einer Rolle](../../relational-databases/security/authentication-access/join-a-role.md).

## <a name="3-update-logging-information-in-ssisdb"></a>3. Protokollieren von Informationen in SSISDB aktualisieren
Rufen Sie die gespeicherte Prozedur [Catalog]. [Update_logdb_info] mit Sql Server-Name und Verbindung Zeichenfolge als Parameter.

#### <a name="example"></a>Beispiel
```sql
SET @serverName = CONVERT(sysname, SERVERPROPERTY('servername'))
SET @connectionString = 'Data Source=' + @serverName + ';Initial Catalog=SSISDB;Integrated Security=SSPI;'
EXEC [internal].[update_logdb_info] @serverName, @connectionString
GO
```

## <a name="4-restart-scale-out-worker-service"></a>4. Scale-Out-Worker-Dienst neu starten

> [!NOTE]
> Wenn Sie ein Windows-Benutzerkonto für die Protokollierung verwenden, muss sie dasselbe Konto Scale-Out-Worker-Dienst ausgeführt wird. Andernfalls schlägt die Anmeldung bei SQL Server fehl.

