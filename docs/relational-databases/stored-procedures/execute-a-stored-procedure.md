---
title: "Ausführen einer gespeicherten Prozedur | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stored-Procs
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.executeprocedure.general.f1
- sql13.swb.executeprocedure.f1
helpviewer_keywords:
- stored procedures [SQL Server], parameters
- extended stored procedures [SQL Server], executing
- system stored procedures [SQL Server], executing
- stored procedures [SQL Server], executing
- user-defined stored procedures [SQL Server]
ms.assetid: a0b1337d-2059-4872-8c62-3f967d8b170f
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c1e76212425f01aba20c8a0d0fdb548415559be1
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="execute-a-stored-procedure"></a>Ausführen einer gespeicherten Prozedur
  In diesem Thema wird beschrieben, wie Sie eine gespeicherte Prozedur in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]ausführen.  
  
 Zum Ausführen einer gespeicherten Prozedur stehen zwei Möglichkeiten zur Verfügung. Der erste und gebräuchlichste Ansatz besteht darin, dass eine Anwendung oder ein Benutzer die Prozedur aufruft. Der zweite Ansatz ist das Einrichten der Prozedur zur automatischen Ausführung beim Start einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Wenn eine Prozedur von einer Anwendung oder einem Benutzer aufgerufen wird, wird das [!INCLUDE[tsql](../../includes/tsql-md.md)] EXECUTE- oder EXEC-Schlüsselwort explizit im Aufruf angegeben. Falls es sich bei der Prozedur um die erste Anweisung im [!INCLUDE[tsql](../../includes/tsql-md.md)] -Batch handelt, kann sie alternativ ohne das Schlüsselwort aufgerufen und ausgeführt werden.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Empfehlungen](#Recommendations)  
  
     [Sicherheit](#Security)  
  
-   **Ausführen einer gespeicherten Prozedur mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Die Sortierung der aufrufenden Datenbank wird beim Zuordnen von Systemprozedurnamen verwendet. Aus diesem Grund muss in Prozeduraufrufen immer die genaue Groß-/Kleinschreibung von Systemprozedurnamen verwendet werden. Der folgende Code schlägt z. B. fehl, wenn er im Kontext einer Datenbank ausgeführt wird, bei deren Sortierung die Groß-/Kleinschreibung beachtet wird:  
  
    ```tsql  
    EXEC SP_heLP; -- Will fail to resolve because SP_heLP does not equal sp_help  
    ```  
  
     Fragen Sie die Katalogsichten [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) und [sys.system_parameters](../../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md) ab, um die genauen Systemprozedurnamen anzuzeigen.  
  
-   Wenn eine benutzerdefinierte Prozedur den gleichen Namen besitzt wie eine Systemprozedur, wird die benutzerdefinierte Prozedur möglicherweise nie ausgeführt.  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Ausführen von gespeicherten Systemprozeduren  
  
     Systemprozeduren beginnen mit dem Präfix **sp_**. Da sie in allen benutzer- und systemdefinierten Datenbanken logisch angezeigt werden, können sie in jeder Datenbank ausgeführt werden, ohne den Prozedurnamen voll zu qualifizieren. Es wird jedoch empfohlen, die Namen aller Systemprozeduren mit dem **sys** -Schemanamen für das Schema zu qualifizieren, um Namenskonflikte zu vermeiden. Das folgende Beispiel zeigt die empfohlene Methode für das Aufrufen einer Systemprozedur.  
  
    ```tsql  
    EXEC sys.sp_who;  
    ```  
  
-   Ausführen von benutzerdefinierten gespeicherten Prozeduren  
  
     Beim Ausführen einer benutzerdefinierten Prozedur empfiehlt es sich, den Prozedurnamen mit dem Schemanamen zu qualifizieren. Auf diese Weise lässt sich die Leistung geringfügig verbessern, da [!INCLUDE[ssDE](../../includes/ssde-md.md)] nicht mehrere Schemas durchsuchen muss. Zudem können Sie so verhindern, dass die falsche Prozedur ausgeführt, wenn eine Datenbank in mehreren Schemas über Prozeduren mit dem gleichen Namen verfügt.  
  
     Das folgende Beispiel zeigt die empfohlene Methode für das Ausführen einer benutzerdefinierten Prozedur. Beachten Sie, dass die Prozedur einen Eingabeparameter akzeptiert. Informationen zum Angeben von Ein- und Ausgabeparametern finden Sie unter [Angeben von Parametern](../../relational-databases/stored-procedures/specify-parameters.md).  
  
    ```tsql  
    USE AdventureWorks2012;  
    GO  
    EXEC dbo.uspGetEmployeeManagers @BusinessEntityID = 50;  
    ```  
  
     -Oder-  
  
    ```tsql  
    EXEC AdventureWorks2012.dbo.uspGetEmployeeManagers 50;  
    GO  
    ```  
  
     Wird der nicht gekennzeichnete Name einer benutzerdefinierten Prozedur angegeben, durchsucht [!INCLUDE[ssDE](../../includes/ssde-md.md)] die folgenden Schemas in der angegebenen Reihenfolge nach der Prozedur:  
  
    1.  Das **sys** -Schema der aktuellen Datenbank.  
  
    2.  Das Standardschema des Aufrufers, wenn die Prozedur als Batch oder dynamisches SQL ausgeführt wird. Falls aber der nicht qualifizierte Name der Prozedur im Textkörper einer anderen Prozedurdefinition vorkommt, wird als nächstes das Schema durchsucht, das diese andere Prozedur enthält.  
  
    3.  Das **dbo** -Schema in der aktuellen Datenbank  
  
-   Automatisches Ausführen von gespeicherten Prozeduren  
  
     Zur automatischen Ausführung markierte Prozeduren werden bei jedem Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt, und die **master** -Datenbank wird während dieses Startprozesses wiederhergestellt. Das Einrichten von Prozeduren zur automatischen Ausführung kann für Datenbankwartungsvorgänge oder die fortlaufende Ausführung von Prozeduren als Hintergrundprozesse nützlich sein. Die automatische Ausführung kann auch verwendet werden, um System- oder Wartungstasks in **tempdb**auszuführen, z. B. das Erstellen einer globalen temporären Tabelle. Auf diese Weise wird sichergestellt, dass eine solche temporäre Tabelle immer vorhanden ist, wenn **tempdb** beim Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu erstellt wird.  
  
     Eine automatisch ausgeführte Prozedur wird mit den Berechtigungen ausgeführt, die den Mitgliedern der festen Serverrolle **sysadmin** zugewiesen sind. Alle Fehlermeldungen, die von der Prozedur erzeugt werden, werden in das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll geschrieben.  
  
     Es gibt keine Beschränkung für die Anzahl der Autostartprozeduren. Bedenken Sie jedoch, dass jede dieser Prozeduren während der Ausführung jeweils einen Arbeitsthread belegt. Wenn Sie beim Systemstart mehrere Prozeduren ausführen müssen, diese aber nicht parallel ausgeführt werden müssen, legen Sie eine Prozedur als Autostartprozedur fest, und schreiben Sie diese Prozedur so, dass sie die anderen Prozeduren aufruft. Dadurch wird nur ein Arbeitsthread benötigt.  
  
    > [!TIP]  
    >  Von einer automatisch ausgeführten Prozedur sollten keine Resultsets zurückgegeben werden. Da die Prozedur von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und nicht von einer Anwendung oder einem Benutzer ausgeführt wird, gibt es kein Ausgabeziel für die Resultsets.  
  
-   Festlegen, Löschen und Steuern der automatischen Ausführung  
  
     Nur der Systemadministrator (**sa**) kann eine Prozedur für die automatische Ausführung markieren. Die Prozedur muss sich außerdem in der **master** -Datenbank im Besitz von **sa**befinden und darf keine Eingabe- oder Ausgabeparameter enthalten.  
  
     Verwenden Sie [sp_procoption](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md) für folgende Aufgaben:  
  
    1.  Angeben einer vorhandenen Prozedur als Startprozedur.  
  
    2.  Verhindern der Ausführung einer Prozedur beim Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
###  <a name="Security"></a> Sicherheit  
 Weitere Informationen finden Sie unter [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md) und [EXECUTE AS-Klausel &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
####  <a name="Permissions"></a> Berechtigungen  
 Weitere Informationen finden Sie unter [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)ausführen.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-execute-a-stored-procedure"></a>So führen Sie eine gespeicherte Prozedur aus  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]her, erweitern Sie diese Instanz und dann **Datenbanken**.  
  
2.  Erweitern Sie die gewünschte Datenbank, **Programmierbarkeit**und dann **Gespeicherte Prozeduren**.  
  
3.  Klicken Sie mit der rechten Maustaste auf die gewünschte benutzerdefinierte gespeicherte Prozedur, und klicken Sie dann auf **Gespeicherte Prozedur ausführen**.  
  
4.  Geben Sie im Dialogfeld **Prozedur ausführen** einen Wert für jeden Parameter an, und legen Sie fest, ob er einen NULL-Wert übergeben soll.  
  
     **Parameter**  
     Zeigt den Namen des Parameters an.  
  
     **Datentyp**  
     Zeigt den Datentyp des Parameters an.  
  
     **Ausgabeparameter**  
     Zeigt an, ob es sich um einen Ausgabeparameter handelt.  
  
     **NULL-Wert übergeben**  
     Übergibt als Wert des Parameters einen NULL-Wert.  
  
     **Wert**  
     Geben Sie den Wert des Parameters bei Aufruf der Prozedur ein.  
  
5.  Klicken Sie auf **OK**, um die gespeicherte Prozedur auszuführen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-execute-a-stored-procedure"></a>So führen Sie eine gespeicherte Prozedur aus  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. Dieses Beispiel zeigt, wie eine gespeicherte Prozedur ausgeführt wird, die einen Parameter erwartet. Im Beispiel wird die gespeicherte Prozedur `uspGetEmployeeManagers` mit dem  `6` -Parameterwert `@EmployeeID` ausgeführt.  
  
```tsql  
USE AdventureWorks2012;  
GO  
EXEC dbo.uspGetEmployeeManagers 6;  
GO  
```  
  
#### <a name="to-set-or-clear-a-procedure-for-executing-automatically"></a>So legen Sie die automatische Ausführung für eine gespeicherte Prozedur fest oder deaktivieren Sie sie  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. Dieses Beispiel zeigt, wie [sp_procoption](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md) verwendet wird, um die automatische Ausführung einer Prozedur festzulegen.  
  
```tsql  
USE AdventureWorks2012;  
GO  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionName = ] 'startup'   
    , @OptionValue = 'on';  
```  
  
#### <a name="to-stop-a-procedure-from-executing-automatically"></a>So verhindern Sie die automatische Ausführung einer Prozedur  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. Dieses Beispiel zeigt, wie [sp_procoption](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md) verwendet wird, um die automatische Ausführung einer Prozedur zu beenden.  
  
```tsql  
USE AdventureWorks2012;  
GO  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionValue = 'off';  
```  
  
###  <a name="TsqlExample"></a> Beispiel (Transact-SQL)  
  
## <a name="see-also"></a>Siehe auch  
 [Angeben von Parametern](../../relational-databases/stored-procedures/specify-parameters.md)   
 [Konfigurieren der Serverkonfigurationsoption Startprozeduren suchen](../../database-engine/configure-windows/configure-the-scan-for-startup-procs-server-configuration-option.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [Gespeicherte Prozeduren &#40;Datenbankmodul&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)  
  
  
