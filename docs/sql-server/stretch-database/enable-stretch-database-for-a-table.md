---
title: "Aktivieren von Stretch-Datenbank für eine Tabelle | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/05/2016
ms.prod: stretch-database
ms.prod_service: sql-non-specified
ms.service: database-engine
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, enabling table
- enabling table for Stretch Database
ms.assetid: de4ac0c5-46ef-4593-a11e-9dd9bcd3ccdc
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: 18ca9bfffcc53e715668634e0a59e33775c9f2c2
ms.contentlocale: de-de
ms.lasthandoff: 07/29/2017

---
# <a name="enable-stretch-database-for-a-table"></a>Aktivieren von Stretch-Datenbank für eine Tabelle
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Wählen Sie **Stretch > Aktivieren** aus, um eine Tabelle für Stretch-Datenbank zu konfigurieren. So wird in SQL Server Management Studio für eine Tabelle der Assistent zum **Aktivieren der Tabelle für Stretch** geöffnet. Sie können auch Transact-SQL verwenden, um Stretch-Datenbank für eine vorhandene Tabelle zu aktivieren. Alternativ können Sie eine neue, für Stretch-Datenbank aktivierte Tabelle erstellen.  
  
-   Wenn Sie kalte Daten in einer separaten Tabelle speichern, können Sie die gesamte Tabelle migrieren.  
  
-   Wenn Ihre Tabelle sowohl heiße als auch kalte Daten enthält, können Sie eine Filterfunktion zum Auswählen der zu migrierenden Zeilen angeben.    
 
 **Voraussetzungen**. Wenn Sie **Stretch &gt; Aktivieren** für eine Tabelle auswählen und Stretch-Datenbank noch nicht für die Datenbank aktiviert haben, konfiguriert der Assistent zuerst die Datenbank für Stretch-Datenbank. Führen Sie die Schritte unter [Erste Schritte durch Ausführen des Assistenten zum Aktivieren von Stretch für eine Datenbank](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md) anstelle der in diesem Thema aufgeführten Schritte durch.  
  
 **Berechtigungen**. Um die Stretch-Datenbank auf einer Datenbank oder für eine Tabelle zu aktivieren, benötigen Sie "db_owner"-Berechtigungen. Um Stretch-Datenbank für eine Tabelle zu aktivieren, benötigen Sie außerdem ALTER-Berechtigungen für die Tabelle.  

 >   [!NOTE]
 > Wenn Sie Stretch-Datenbank später deaktivieren, sollten Sie daran denken, dass durch die Deaktivierung von Stretch-Datenbank für eine Tabelle oder Datenbank das Remoteobjekt nicht gelöscht wird. Wenn Sie die Remotetabelle oder Remotedatenbank löschen möchten, müssen Sie sie mithilfe des Azure-Verwaltungsportals löschen. Die Remoteobjekte erzeugen weiterhin Azure-Kosten, bis Sie die Objekte manuell löschen.
 
##  <a name="EnableWizardTable"></a> Verwenden des Assistenten zum Aktivieren von Stretch-Datenbank für eine Tabelle  
 **Starten des Assistenten**  
 1.  Wählen Sie im Objekt-Explorer in SQL Server Management Studio die Tabelle aus, für die Sie Stretch aktivieren möchten.  
  
2.  Klicken Sie mit der rechten Maustaste, wählen Sie **Stretch**, und wählen Sie anschließend **Aktivieren** aus, um den Assistenten zu starten.  
  
 **Einführung**  
 Überprüfen Sie den Zweck des Assistenten und die Voraussetzungen.  
  
 **Auswählen von Datenbanktabellen**  
 Vergewissern Sie sich, dass die Tabelle, die Sie aktivieren möchten, angezeigt wird und ausgewählt ist.  
  
 Sie können eine ganze Tabelle migrieren oder eine einfache Filterfunktion im Assistenten angeben. Wenn Sie zum Auswählen zu migrierender Zeilen eine andere Art von Filterfunktion verwenden möchten, führen Sie einen der folgenden Schritte aus.  
  
-   Beenden Sie den Assistenten, und führen Sie die ALTER TABLE-Anweisung aus, um Stretch für die Tabelle zu aktivieren und eine Filterfunktion anzugeben.  
  
-   Führen Sie die ALTER TABLE-Anweisung aus, um eine Filterfunktion anzugeben, nachdem Sie den Assistenten beendet haben. Die erforderlichen Schritte finden Sie unter [Hinzufügen einer Filterfunktion nach Ausführen des Assistenten](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md#addafterwiz).  
  
 Die ALTER TABLE-Syntax wird im weiteren Verlauf dieses Themas beschrieben.  
  
 **Zusammenfassung**  
 Überprüfen Sie die im Assistenten eingegebenen Werte und ausgewählten Optionen. Wählen Sie dann **Fertig stellen** aus, um Stretch zu aktivieren.  
  
 **Ergebnisse**  
 Überprüfen Sie die Ergebnisse.  
  
##  <a name="EnableTSQLTable"></a> Verwenden von Transact-SQL zum Aktivieren von Stretch-Datenbank für eine Tabelle  
 Sie können Stretch-Datenbank mithilfe von Transact-SQL für eine vorhandene Tabelle aktivieren oder damit eine neue, für Stretch-Datenbank aktivierte Tabelle erstellen.  
  
### <a name="options"></a>Optionen  
 Verwenden Sie die folgenden Optionen, wenn Sie CREATE TABLE oder ALTER TABLE ausführen, um Stretch-Datenbank für eine Tabelle zu aktivieren.  
  
-   Verwenden Sie optional die `FILTER_PREDICATE = <function>` -Klausel, um eine Funktion zum Auswählen der zu migrierenden Zeilen anzugeben, wenn die Tabelle sowohl heiße als auch kalte Daten enthält. Das Prädikat muss eine Inline-Tabellenwertfunktion aufrufen. Weitere Informationen hierzu finden Sie unter [Auswählen zu migrierender Zeilen mithilfe einer Filterfunktion](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md). Wenn Sie keine Filterfunktion angeben, wird die gesamte Tabelle migriert.  
  
    > [!IMPORTANT]  
    >  Wenn Sie eine schwache Filterfunktion angeben, wird die Datenmigration ebenfalls unzureichend ausgeführt. Stretch-Datenbank wendet die Filterfunktion mithilfe des CROSS APPLY-Operators auf die Tabelle an.  
  
-   Geben Sie `MIGRATION_STATE = OUTBOUND` an, um sofort mit der Datenmigration zu beginnen, oder  `MIGRATION_STATE = PAUSED` , um den Beginn der Datenmigration zu verschieben.  
  
### <a name="enable-stretch-database-for-an-existing-table"></a>Aktivieren von Stretch-Datenbank für eine vorhandene Tabelle  
 Führen Sie den Befehl ALTER TABLE aus, um eine vorhandene Tabelle für Stretch-Datenbank zu konfigurieren.  
  
 Nachstehend sehen Sie ein Beispiel, das die gesamte Tabelle migriert und sofort mit der Datenmigration beginnt.  
  
```sql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <table name>  
    SET ( REMOTE_DATA_ARCHIVE = ON ( MIGRATION_STATE = OUTBOUND ) ) ;  
GO
```  
  
 Es folgt ein Beispiel, das nur die Zeilen migriert, die durch die Inline-Tabellenwertfunktion `dbo.fn_stretchpredicate` identifiziert wurden, und das die Datenmigration verschiebt. Weitere Informationen zur Filterfunktion finden Sie unter [Auswählen zu migrierender Zeilen mithilfe einer Filterfunktion (Stretch-Datenbank)](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).  
  
```sql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <table name>  
    SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(),  
        MIGRATION_STATE = PAUSED ) ) ;  
 GO
```  
  
 Weitere Informationen hierzu finden Sie unter [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
### <a name="create-a-new-table-with-stretch-database-enabled"></a>Erstellen einer neuen, für Stretch-Datenbank aktivierten Tabelle  
 Führen Sie den Befehl CREATE TABLE aus, um eine neue, für Stretch-Datenbank aktivierte Tabelle zu erstellen.  
  
 Nachstehend sehen Sie ein Beispiel, das die gesamte Tabelle migriert und sofort mit der Datenmigration beginnt.  
  
```sql  
USE <Stretch-enabled database name>;
GO
CREATE TABLE <table name>
    ( ... )  
    WITH ( REMOTE_DATA_ARCHIVE = ON ( MIGRATION_STATE = OUTBOUND ) ) ;  
GO
```  
  
 Es folgt ein Beispiel, das nur die Zeilen migriert, die durch die Inline-Tabellenwertfunktion `dbo.fn_stretchpredicate` identifiziert wurden, und das die Datenmigration verschiebt. Weitere Informationen zur Filterfunktion finden Sie unter [Auswählen zu migrierender Zeilen mithilfe einer Filterfunktion (Stretch-Datenbank)](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).  
  
```sql  
USE <Stretch-enabled database name>;
GO
CREATE TABLE <table name> 
    ( ... )  
    WITH ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(),  
        MIGRATION_STATE = PAUSED ) ) ;  
GO  
```  
  
 Weitere Informationen hierzu finden Sie unter [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
  
  

