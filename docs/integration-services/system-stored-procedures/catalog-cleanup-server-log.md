---
title: Catalog.cleanup_server_log | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0dedb685-d3a6-4bd6-8afd-58d98853deee
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1195bbfcc77cb6b96ea5a68cd1a95c2b2126a81e
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcleanupserverlog"></a>Catalog.cleanup_server_log
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Bereinigt die Vorgangsprotokolle, um die SSISDB-Datenbank in einen Zustand zu versetzen, in dem Sie den Wert der Eigenschaft SERVER_OPERATION_ENCRYPTION_LEVEL ändern können.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
cleanup_server_log  
  
```  
  
## <a name="arguments"></a>Argumente  
 Keine.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 für Erfolg und 1 für den Fehler.  
  
## <a name="result-sets"></a>Resultsets  
 Keine.  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   Lese- und AUSFÜHRUNGSBERECHTIGUNGEN für das Projekt und ggf. READ-Berechtigungen für die Umgebung auf die verwiesen wird.  
  
-   Mitgliedschaft in der **Ssis_admin** -Datenbankrolle.  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 Diese gespeicherte Prozedur löst Fehler in den folgenden Szenarien:  
  
-   Es gibt einen oder mehrere aktive Vorgänge in der SSISDB-Datenbank.  
  
-   Die SSISDB-Datenbank ist nicht im Einzelbenutzermodus befindet.  
  
## <a name="remarks"></a>Hinweise  
 SQL Server 2012 Service Pack 2 hinzugefügt, der Eigenschaft SERVER_OPERATION_ENCRYPTION_LEVEL, um die **internal.catalog_properties** Tabelle. Diese Eigenschaft hat zwei mögliche Werte:  
  
-   **PER_EXECUTION (1)** – das Zertifikat und symmetrische Schlüssel verwendet, für den Schutz von vertraulichen Execution-Parametern und ausführungsprotokolle werden für jede Ausführung erstellt. Dies ist der Standardwert. Sie können in Leistungsprobleme (Deadlocks, fehlerhafte Wartung Aufträge usw.) in einer produktionsumgebung ausführen, da Zertifikatsschlüssel/für jede Ausführung generiert werden. Diese Einstellung bietet jedoch ein höheres Maß an Sicherheit als der andere Wert (2).  
  
-   **PER_PROJECT (2)** – das Zertifikat und den symmetrischen Schlüssel für den Schutz von sensiblen Parameter werden für jedes Projekt erstellt. Dies bietet Ihnen eine bessere Leistung als die PER_EXECUTION-Ebene, da der Schlüssel und das Zertifikat einmal für ein Projekt und nicht für jede Ausführung generiert werden.  
  
 Auszuführende stehen Ihnen die [catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md) gespeicherte Prozedur aus, bevor Sie zwischen 1 und 2 (oder) zwischen 2 und 1 der SERVER_OPERATION_ENCRYPTION_LEVEL ändern können. Vor dem Ausführen dieser gespeicherten Prozedur, führen Sie folgende Schritte aus:  
  
1.  Stellen Sie sicher, dass der Wert der Eigenschaft OPERATION_CLEANUP_ENABLED, auf "true" in festgelegt ist der [Catalog. catalog_properties &#40; SSISDB-Datenbank &#41; ](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) Tabelle.  
  
2.  Die Integration Services-Datenbank (SSISDB) auf den Einzelbenutzermodus festgelegt. Starten Sie in SQL Server Management Studio im Dialogfeld Eigenschaften für SSISDB, wechseln Sie zur Registerkarte "Optionen" und legen Sie den Zugriff beschränken-Eigenschaft auf Einzelbenutzermodus (SINGLE_USER). Legen Sie nach dem Ausführen der Cleanup_server_log gespeicherte Prozedur den Wert der Eigenschaft auf den ursprünglichen Wert zurückzusetzen.  
  
3.  Führen Sie die gespeicherte Prozedur [catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md).  
  
4.  Jetzt, fahren Sie fort, und ändern Sie den Wert der Eigenschaft SERVER_OPERATION_ENCRYPTION_LEVEL in die [Catalog. catalog_properties &#40; SSISDB-Datenbank &#41; ](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) Tabelle.  
  
5.  Führen Sie die gespeicherte Prozedur [catalog.cleanup_server_execution_keys](../../integration-services/system-stored-procedures/catalog-cleanup-server-execution-keys.md) , um Zertifikate Schlüssel aus der SSISDB-Datenbank zu bereinigen. Löschen von Zertifikaten und Schlüsseln aus der SSISDB-Datenbank kann sehr lange dauern, damit es in regelmäßigen Abständen während Nebenzeiten ausgeführt werden soll.  
  
     Geben Sie den Umfang oder die Ebene (Ausführung im Vergleich zu Project) und die Anzahl der Schlüssel gelöscht werden soll. Die Standardgröße des Stapel für die Löschung ist 1000. Wenn Sie die Ebene auf 2 festlegen, werden nur dann, wenn die zugehörigen Projekte gelöscht wurden Schlüssel und Zertifikate gelöscht.  
  
 Weitere Informationen finden Sie unter den folgenden Knowledge Base-Artikel. [FIX: Leistungsprobleme auftreten, wenn SSISDB, als die Bereitstellung verwenden in SQL Server 2012 speichern](http://support.microsoft.com/kb/2972285)  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die Prozedur Cleanup_server_log gespeichert.  
  
```tsql  
USE [SSISDB]  
GO  
  
DECLARE@return_value int  
EXEC@return_value = [internal].[cleanup_server_log]  
SELECT'Return Value' = @return_value  
GO  
  
```  
  
  
