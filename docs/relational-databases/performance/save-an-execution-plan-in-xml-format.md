---
title: "Speichern eines Ausf&#252;hrungsplans im XML-Format | Microsoft Docs"
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
  - "XML-Abfragepläne [SQL Server]"
  - "Öffnen von Ausführungsplänen"
  - "XML-Showplans [SQL Server]"
  - "Ausführungspläne [SQL Server], speichern"
  - "Speichern von Ausführungsplänen"
ms.assetid: c439e53b-56f3-4442-97c6-dabd48a203d8
caps.latest.revision: 25
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 25
---
# Speichern eines Ausf&#252;hrungsplans im XML-Format
  Verwenden Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , um Ausführungspläne als XML-Datei zu speichern und für die Anzeige zu öffnen.  
  
 Zum Verwenden der Ausführungsplanfunktion in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]oder der XML Showplan-SET-Optionen benötigen Benutzer die entsprechenden Berechtigungen, um die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfrage auszuführen, für die ein Ausführungsplan generiert wird. Den Benutzern muss auch die SHOWPLAN-Berechtigung für alle Datenbanken erteilt werden, auf die die Abfrage verweist.  
  
### So speichern Sie einen Abfrageplan mit den XML Showplan-SET-Optionen  
  
1.  Öffnen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] einen Abfrage-Editor, und stellen Sie eine Verbindung mit [!INCLUDE[ssDE](../../includes/ssde-md.md)] her.  
  
2.  Aktivieren Sie SHOWPLAN_XML mithilfe der folgenden Anweisung:  
  
    ```  
    SET SHOWPLAN_XML ON;  
    GO  
    ```  
  
     Verwenden Sie die folgende Anweisung, um STATISTICS XML zu aktivieren:  
  
    ```  
    SET STATISTICS XML ON;  
    GO  
    ```  
  
     SHOWPLAN_XML generiert für eine Abfrage zur Kompilierungszeit Informationen zum Abfrageausführungsplan, führt die Abfrage aber nicht aus. STATISTICS XML generiert für eine Abfrage zur Laufzeit Informationen zum Abfrageausführungsplan und führt die Abfrage aus.  
  
3.  Abfrage ausführen. Beispiel:  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SET SHOWPLAN_XML ON;  
    GO  
    -- Execute a query.  
    SELECT BusinessEntityID   
    FROM HumanResources.Employee  
    WHERE NationalIDNumber = '509647174';  
    GO  
    SET SHOWPLAN_XML OFF;  
    ```  
  
4.  Klicken Sie im Bereich **Ergebnisse** mit der rechten Maustaste auf den **Microsoft SQL Server XML Showplan**, der den Abfrageplan enthält, und klicken Sie dann auf **Ergebnisse speichern unter**.  
  
5.  Klicken Sie im Dialogfeld **Rasterergebnisse speichern** bzw. **Textergebnisse speichern** im Feld **Dateityp** auf **Alle Dateien (\*.\*)**.  
  
6.  Geben Sie in das Feld **Dateiname** einen Namen im Format \<Name**>.sqlplan**ein, und klicken Sie auf **Speichern**.  
  
### So speichern Sie einen Ausführungsplan mithilfe der SQL Server Management Studio-Optionen  
  
1.  Generieren Sie mit [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] entweder einen geschätzten Ausführungsplan oder einen tatsächlichen Ausführungsplan. Weitere Informationen finden Sie unter [Anzeigen des geschätzten Ausführungsplans](../../relational-databases/performance/display-the-estimated-execution-plan.md) oder [Anzeigen eines tatsächlichen Ausführungsplans](../../relational-databases/performance/display-an-actual-execution-plan.md).  
  
2.  Klicken Sie im Ergebnisbereich auf der Registerkarte **Ausführungsplan** auf den grafischen Ausführungsplan und wählen Sie **Ausführungsplan speichern unter**.  
  
     Alternativ können Sie **Ausführungsplan speichern unter** auch im Menü **Datei** auswählen.  
  
3.  Stellen Sie im Dialogfeld **Speichern unter** sicher, dass der **Dateityp** auf **Ausführungsplandateien (\*.sqlplan)** festgelegt ist.  
  
4.  Geben Sie in das Feld **Dateiname** einen Namen im Format \<Name**>.sqlplan**ein, und klicken Sie auf **Speichern**.  
  
### So öffnen Sie einen gespeicherten XML-Abfrageplan in SQL Server Management Studio  
  
1.  Wählen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]im Menü **Datei** **Öffnen**, und klicken Sie dann auf **Datei**.  
  
2.  Legen Sie im Dialogfeld **Datei öffnen** den **Dateityp** auf **Ausführungsplandateien (\*.sqlplan)** fest, um eine gefilterte Liste der gespeicherten XML-Abfrageplandateien zu erzeugen.  
  
3.  Wählen Sie die XML-Abfrageplandatei aus, die Sie anzeigen möchten, und klicken Sie auf **Öffnen**.  
  
     Alternativ können Sie im Windows-Explorer auf eine Datei mit der Erweiterung **.sqlplan** doppelklicken. Der Plan wird in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] geöffnet.  
  
## Siehe auch  
 [SET SHOWPLAN_XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-xml-transact-sql.md)   
 [SET STATISTICS XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-xml-transact-sql.md)  
  
  