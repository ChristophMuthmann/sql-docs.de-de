---
title: catalog.cleanup_server_log | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0dedb685-d3a6-4bd6-8afd-58d98853deee
caps.latest.revision: "5"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6cf0f550930ac73199276dc403763f49ce45b5e7
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="catalogcleanupserverlog"></a>catalog.cleanup_server_log
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Bereinigt die Vorgangsprotokolle, um die SSISDB-Datenbank in einen Zustand zu versetzen, in dem Sie den Wert der Eigenschaft SERVER_OPERATION_ENCRYPTION_LEVEL ändern können.  
  
## <a name="syntax"></a>Syntax  
  
```sql
catalog.cleanup_server_log  
```  
  
## <a name="arguments"></a>Argumente  
 Keine.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (null) für „erfolgreich“ und 1 für „fehlgeschlagen“.  
  
## <a name="result-sets"></a>Resultsets  
 Keine.  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   READ- und EXECUTE-Berechtigungen für das Projekt und ggf. READ-Berechtigungen für die Umgebung, auf die verwiesen wird.  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**.  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 Diese gespeicherte Prozedur löst Fehler in den folgenden Szenarios aus:  
  
-   Es gibt mindestens einen aktiven Vorgang in SSISDB.  
  
-   Die SSIS-Datenbank befindet sich nicht im Einzelbenutzermodus.  
  
## <a name="remarks"></a>Hinweise  
 In SQL Server 2012 Service Pack 2 wird die Eigenschaft „SERVER_OPERATION_ENCRYPTION_LEVEL“ der Tabelle **internal.catalog_properties** hinzugefügt. Die Eigenschaft verfügt über zwei mögliche Werte:  
  
-   **PER_EXECUTION (1):** Das Zertifikat und der symmetrische Schlüssel, die zum Schutz von sensiblen Ausführungsparametern und -protokollen verwendet werden, werden für jede Ausführung erstellt. Möglicherweise entstehen Probleme mit der Leistung (Deadlocks, fehlerhafte Wartungsaufträge, etc.) in einer Produktumgebung, da für jede Ausführung Zertifikate bzw. Schlüssel generiert werden. Trotzdem bietet diese Einstellung ein höheres Maß an Sicherheit als der andere Wert (2).  
  
-   **PER_PROJECT (2):** Das Zertifikat und der symmetrische Schlüssel, die zum Schutz von sensiblen Parametern verwendet werden, werden für jedes Projekt erstellt. PER_PROJECT (2) ist der Standardwert. Diese Einstellung bietet eine bessere Leistung als die PER_EXECUTION-Ebene, da der Schlüssel und das Zertifikat nur einmal pro Projekt anstatt für jede Ausführung generiert werden.  
  
 Sie müssen die gespeicherte [catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md)-Prozedur ausführen, bevor Sie SERVER_OPERATION_ENCRYPTION_LEVEL von 2 auf 1 oder von 1 auf 2 ändern können. Führen Sie die folgenden Schritte aus, bevor Sie diese gespeicherte Prozedur ausführen:  
  
1.  Stellen Sie sicher, dass der Wert der Eigenschaft OPERATION_CLEANUP_ENABLED in der Tabelle [catalog.catalog_properties (SSISDB Database)](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) auf TRUE festgelegt ist.  
  
2.  Legen Sie die Integration Services-Datenbank (SSISDB) auf den Einzelbenutzermodus fest. Starten Sie in SQL Server Management Studio das Dialogfeld „Datenbankeigenschaften“ für SSISDB, wechseln Sie zur Registerkarte „Optionen“, und legen Sie die Eigenschaft „Zugriff beschränken“ auf den Einzelbenutzermodus fest (SINGLE_USER). Nachdem Sie die gespeicherte „cleanup_server_log“-Prozedur ausgeführt haben, setzen Sie den Eigenschaftswert auf den ursprünglichen Wert zurück.  
  
3.  Führen Sie die gespeicherte [catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md)-Prozedur fest.  
  
4.  Jetzt können Sie den Wert der Eigenschaft SERVER_OPERATION_ENCRYPTION_LEVEL in der Tabelle [catalog.catalog_properties (SSISDB Database)](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) ändern.  
  
5.  Führen Sie die gespeicherte [catalog.cleanup_server_execution_keys](../../integration-services/system-stored-procedures/catalog-cleanup-server-execution-keys.md)-Prozedur aus, um Zertifikatschlüssel aus der SSIS-Datenbank zu bereinigen. Das Löschen von Zertifikaten und Schlüssel aus der SSIS-Datenbank nimmt möglicherweise einige Zeit in Anspruch. Aus diesem Grund sollten Sie diesen Vorgang regelmäßig außerhalb der Spitzenzeiten ausführen.  
  
     Sie können auch den Bereich oder die Ebene (Ausführung bzw. Projekt) angeben und festlegen, wie viele Schlüssel gelöscht werden sollen. Die Standardbatchgröße zum Löschen beträgt 1000. Wenn Sie die Ebene auf 2 festlegen, werden die Schlüssel und Zertifikate nur gelöscht, wenn zugehörige Projekte gelöscht worden sind.  
  
 Weitere Informationen finden Sie im folgenden Knowledge Base-Artikel: [FIX: Performance issues when you use SSISDB as your deployment store in SQL Server 2012 (Fehlerbehebung: Probleme mit der Leistung bei der Verwendung von SSISDB als Bereitstellungsspeicher in SQL Server 2012)](http://support.microsoft.com/kb/2972285).  
  
## <a name="example"></a>Beispiel  
 Mithilfe des folgenden Beispiels wird die gespeicherte „cleanup_server_log“-Prozedur aufgerufen.  
  
```sql  
USE [SSISDB]  
GO  
  
DECLARE@return_value int  
EXEC@return_value = [internal].[cleanup_server_log]  
SELECT'Return Value' = @return_value  
GO   
```  
  
  
