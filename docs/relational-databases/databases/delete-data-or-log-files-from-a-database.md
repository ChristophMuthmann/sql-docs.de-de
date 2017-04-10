---
title: "L&#246;schen von Daten- oder Protokolldateien aus einer Datenbank | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Protokolle [SQL Server], Dateien"
  - "Löschen von Dateien"
  - "Entfernen von Dateien"
  - "Entfernen von Daten"
  - "Datenlöschungen [SQL Server]"
  - "Dateilöschung [SQL Server]"
  - "Löschen von Daten"
ms.assetid: 0db4018c-ce2c-4ba1-bb29-1e4f3791c925
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# L&#246;schen von Daten- oder Protokolldateien aus einer Datenbank
  In diesem Thema wird beschrieben, wie Daten- oder Protokolldateien in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]gelöscht werden.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Erforderliche Komponenten](#Prerequisites)  
  
     [Sicherheit](#Security)  
  
-   **So löschen Sie Daten- oder Protokolldateien aus einer Datenbank mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Eine Datei muss leer sein, bevor sie gelöscht werden kann. Weitere Informationen finden Sie unter [Verkleinern einer Datei](../../relational-databases/databases/shrink-a-file.md).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So löschen Sie Daten- oder Protokolldateien aus einer Datenbank  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **Datenbanken**, klicken Sie mit der rechten Maustaste auf die Datenbank, aus der Sie die Datei löschen möchten, und klicken Sie anschließend auf **Eigenschaften**.  
  
3.  Wählen Sie die Seite **Dateien** aus.  
  
4.  Wählen Sie im Raster **Datenbankdateien** die zu löschende Datei aus, und klicken Sie dann auf **Entfernen**.  
  
5.  Klicken Sie auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So löschen Sie Daten- oder Protokolldateien aus einer Datenbank  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird die Datei `test1dat4` entfernt.  
  
 [!code-sql[DatabaseDDL#AlterDatabase4](../../relational-databases/databases/codesnippet/tsql/delete-data-or-log-files_1.sql)]  
  
 Weitere Beispiele finden Sie unter [ALTER DATABASE-Optionen Datei und Dateigruppe &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20File%20and%20Filegroup%20Options%20\(Transact-SQL\).md).  
  
## Siehe auch  
 [Verkleinern einer Datenbank](../../relational-databases/databases/shrink-a-database.md)   
 [Hinzufügen von Daten- oder Protokolldateien zu einer Datenbank](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)  
  
  