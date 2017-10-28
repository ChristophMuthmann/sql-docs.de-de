---
title: "Erstellen einer Server- und Datenbank-Überwachungsspezifikation | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.sqlaudit.dbaudit.general.f1
helpviewer_keywords:
- audits [SQL Server], creating database specification
- database audit [SQL Server]
ms.assetid: 26ee85de-6e97-4318-b526-900924d96e62
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6d5beb8f3b18bd4dd99039b0f2b38ce731140726
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="create-a-server-audit-and-database-audit-specification"></a>Erstellen einer Server- und Datenbank-Überwachungsspezifikation
  In diesem Thema wird beschrieben, wie eine Serverüberwachung und Datenbanküberwachungsspezifikation in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]erstellt wird.  
  
 Bei der*Überwachung* einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oder einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank werden Ereignisse im System verfolgt und protokolliert. Das *SQL Server Audit* -Objekt listet eine einzelne Instanz an Aktionen oder Aktionsgruppen auf Server- oder Datenbankebene auf, die überwacht werden soll. Die Überwachung wird auf [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanzebene ausgeführt. Es können mehrere Überwachungen pro [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz vorliegen. Das Objekt für die *Überwachungsspezifikation auf Datenbankebene* gehört ebenfalls zu einer Überwachung. Sie können eine Datenbank-Überwachungsspezifikation pro SQL Server-Datenbank und pro Überwachung erstellen. Weitere Informationen finden Sie unter [SQL Server Audit &#40;Datenbankmodul&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So erstellen Sie eine Server- und Datenbank-Überwachungsspezifikation mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
 Datenbank-Überwachungsspezifikationen sind nicht sicherungsfähige Objekte, die sich in einer gegebenen Datenbank befinden. Wenn eine Datenbank-Überwachungsspezifikation erstellt wird, befindet sich diese in einem deaktivierten Zustand.  
  
 Wenn Sie in einer Benutzerdatenbank eine Datenbank-Überwachungsspezifikation erstellen oder ändern, sollten Sie keine Überwachungsaktionen für Serverbereichsobjekte einschließen, z. B. die Systemsichten. Wenn Objekte mit Serverbereich eingeschlossen sind, wird die Überwachung zwar erstellt. Die Objekte mit Serverbereich sind jedoch nicht enthalten, und es wird kein Fehler zurückgegeben. Verwenden Sie eine Datenbank-Überwachungsspezifikation in der master-Datenbank, um Objekte mit Serverbereich zu überwachen.  
  
 Die Datenbank-Überwachungsspezifikationen befinden sich in der Datenbank, in der sie erstellt werden, mit Ausnahme der Systemdatenbank **tempdb** .  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
  
-   Benutzer mit der ALTER ANY DATABASE AUDIT-Berechtigung können Datenbank-Überwachungsspezifikationen erstellen und sie an eine beliebige Überwachung binden.  
  
-   Nachdem eine Datenbank-Überwachungsspezifikation erstellt wurde, kann diese von Prinzipalen mit den Berechtigungen CONTROL SERVER und ALTER ANY DATABASE AUDIT oder von Prinzipalen mit Zugriff auf das sysadmin-Konto angezeigt werden.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-create-a-server-audit"></a>So erstellen Sie eine Serverüberwachung  
  
1.  Erweitern Sie im Objekt-Explorer den Ordner **Sicherheit** .  
  
2.  Klicken Sie mit der rechten Maustaste auf den Ordner **Überwachungen** , und wählen Sie dann **Neue Überwachung**aus. Weitere Informationen finden Sie unter [Create a Server Audit and Server Audit Specification](../../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md).  
  
3.  Nachdem Sie alle Optionen ausgewählt haben, klicken Sie auf **OK**.  
  
#### <a name="to-create-a-database-level-audit-specification"></a>So erstellen Sie eine Überwachungsspezifikation auf Datenbankebene  
  
1.  Erweitern Sie im Objekt-Explorer die Datenbank, in der Sie eine Überwachungsspezifikation erstellen möchten.  
  
2.  Erweitern Sie den Ordner **Sicherheit** .  
  
3.  Klicken Sie mit der rechten Maustaste auf den Ordner **Datenbank-Überwachungsspezifikationen** und dann auf **Neue Datenbank-Überwachungsspezifikation**.  
  
     Die folgenden Optionen sind im Dialogfeld **Datenbank-Überwachungsspezifikation erstellen** verfügbar.  
  
     **Name**  
     Der Name der Datenbank-Überwachungsspezifikation. Er wird automatisch generiert, wenn Sie eine neue Serverüberwachungsspezifikation erstellen, er kann jedoch bearbeitet werden.  
  
     **Überwachung**  
     Der Name einer vorhandenen Datenbanküberwachung. Geben Sie den Namen der Überwachung ein, oder wählen Sie ihn aus der Liste aus.  
  
     **Überwachungsaktionstyp**  
     Gibt die aufzuzeichnenden Überwachungsaktionsgruppen auf Datenbankebene und Überwachungsaktionen an. Eine Liste der Überwachungsaktionsgruppen auf Datenbankebene und Überwachungsaktionen sowie eine Beschreibung der darin enthaltenen Ereignisse finden Sie unter [SQL Server Audit-Aktionsgruppen und -Aktionen](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
     **Objektschema**  
     Zeigt das Schema für den angegebenen **Objektnamen**an.  
  
     **Objektnamen**  
     Der Name des zu überwachenden Objekts. Das Objekt ist nur für Überwachungsaktionen verfügbar, es gilt nicht für Überwachungsgruppen.  
  
     **Auslassungspunkte (…)**  
     Öffnet das Dialogfeld **Objekte auswählen** , in dem Sie anhand des angegebenen **Überwachungsaktionstyps**nach einem verfügbaren Objekt suchen und es auswählen können.  
  
     **Prinzipalname**  
     Das Konto, anhand dessen die Überwachung für das zu überwachende Objekt gefiltert wird.  
  
     **Auslassungspunkte (…)**  
     Öffnet das Dialogfeld **Objekte auswählen** , in dem Sie nach einem verfügbaren Objekt anhand des angegebenen **Objektnamens**suchen und es auswählen können.  
  
4.  Nachdem Sie alle Optionen ausgewählt haben, klicken Sie auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-create-a-server-audit"></a>So erstellen Sie eine Serverüberwachung  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE master ;  
    GO  
    -- Create the server audit.   
    CREATE SERVER AUDIT Payrole_Security_Audit  
        TO FILE ( FILEPATH =   
    'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA' ) ;   
    GO  
    -- Enable the server audit.   
    ALTER SERVER AUDIT Payrole_Security_Audit   
    WITH (STATE = ON) ;  
    ```  
  
#### <a name="to-create-a-database-level-audit-specification"></a>So erstellen Sie eine Überwachungsspezifikation auf Datenbankebene  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. Im folgenden Beispiel wird die Serverüberwachung mit dem Namen `Audit_Pay_Tables`, in der die SELECT- und INSERT-Anweisungen des `dbo`-Benutzers überwacht werden, für die `HumanResources.EmployeePayHistory`-Tabelle anhand der obigen Serverüberwachung erstellt.  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    -- Create the database audit specification.   
    CREATE DATABASE AUDIT SPECIFICATION Audit_Pay_Tables  
    FOR SERVER AUDIT Payrole_Security_Audit  
    ADD (SELECT , INSERT  
         ON HumanResources.EmployeePayHistory BY dbo )   
    WITH (STATE = ON) ;   
    GO  
  
    ```  
  
 Weitere Informationen finden Sie unter [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-transact-sql.md) und [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-audit-specification-transact-sql.md).  
  
  

