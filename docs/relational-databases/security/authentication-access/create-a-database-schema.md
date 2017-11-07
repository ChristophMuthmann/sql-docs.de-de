---
title: Erstellen eines Datenbankschemas | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.schemas.general.f1
helpviewer_keywords:
- creating schemas with Management Studio
- CREATE SCHEMA [Management Studio]
- database schemas
- schemas [SQL Server], creating
ms.assetid: ed2a5522-f4d2-4111-95a4-d3e1e5081739
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: HT
ms.sourcegitcommit: 3a224f5be40f6f7a68a28cb4c8f741c24527e8bd
ms.openlocfilehash: b164e70bf4b1e7586d8e70ab8edb7baa1dfcaade
ms.contentlocale: de-de
ms.lasthandoff: 07/31/2017

---
# <a name="create-a-database-schema"></a>Erstellen eines Datenbankschemas
  In diesem Thema wird beschrieben, wie ein Schema in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]erstellt wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So erstellen Sie ein Schema mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Das neue Schema ist im Besitz einer der folgenden Prinzipale auf Datenbankebene: Datenbankbenutzer, Datenbankrolle oder Anwendungsrolle. Objekte, die innerhalb eines Schemas erstellt werden, gehören dem Besitzer des Schemas und haben für **principal_id** in **sys.objects** einen NULL-Wert. Der Besitz von Objekten, die Schemas als Bereich aufweisen, kann an jeden Prinzipal auf Datenbankebene übertragen werden, aber der Schemabesitzer behält immer die CONTROL-Berechtigung für Objekte innerhalb des Schemas.  
  
-   Wenn Sie beim Erstellen eines Datenbankobjekts einen gültigen Domänenprinzipal als Objektbesitzer (Benutzer oder Gruppe) angeben, wird der Domänenprinzipal der Datenbank als Schema hinzugefügt. Das neue Schema befindet sich im Besitz des Domänenprinzipals.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
  
-   Erfordert die CREATE SCHEMA-Berechtigung für die Datenbank.  
  
-   Um einen anderen Benutzer als den Besitzer des zu erstellenden Schemas anzugeben, benötigt der Aufrufer die IMPERSONATE-Berechtigung für diesen Benutzer. Wenn eine Datenbankrolle als Besitzer angegeben wird, muss der Aufrufer entweder über eine Mitgliedschaft in der Rolle oder die ALTER-Berechtigung für die Rolle verfügen.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
##### <a name="to-create-a-schema"></a>So erstellen Sie ein Schema  
  
1.  Erweitern Sie im Objekt-Explorer den Ordner **Datenbanken** .  
  
2.  Erweitern Sie die Datenbank, in der das neue Datenbankschema erstellt werden soll.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Ordner **Sicherheit** , zeigen Sie auf **Neu**, und wählen Sie **Schema**aus.  
  
4.  Geben Sie im Dialogfeld **Schema - Neu** auf der Seite **Allgemein** im Feld **Schemaname** einen Namen für das neue Schema ein.  
  
5.  Geben Sie im Feld **Schemabesitzer** den Namen eines Datenbankbenutzers oder einer Rolle ein, der bzw. die über das Schema verfügen soll. Klicken Sie alternativ auf **Suchen** , um das Dialogfeld **Rollen und Benutzer suchen** zu öffnen.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>Zusätzliche Optionen  
 Das Dialogfeld **Schema - Neu** verfügt zudem über Optionen auf zwei zusätzlichen Seiten: **Berechtigungen** und **Erweiterte Eigenschaften**.  
  
-   Auf der Seite **Berechtigungen** werden alle möglichen sicherungsfähigen Elemente und die Berechtigungen für diese sicherungsfähigen Elemente aufgelistet, die für die Anmeldung gewährt werden können.  
  
-   Mithilfe der Seite **Erweiterte Eigenschaften** können Sie Datenbankbenutzern benutzerdefinierte Eigenschaften hinzufügen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-create-a-schema"></a>So erstellen Sie ein Schema  
  
1.  Stellen Sie im Objekt-Explorer **** eine Verbindung mit einer [!INCLUDE[ssDE](../../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Im folgenden Beispiel wird das Schema `Chains` erstellt, und anschließend die Tabelle `Sizes`.  
    ```sql  
    CREATE SCHEMA Chains;
    GO
    CREATE TABLE Chains.Sizes (ChainID int, width dec(10,2));
    ```

4.  Weitere Optionen können in einer einzelnen Anweisung durchgeführt werden. In folgendem Beispiel wird das Schema `Sprockets` erstellt, das im Besitz von Annik ist und die Tabelle `NineProngs` enthält. Die Anweisung erteilt Mandar die Berechtigung für `SELECT` und verweigert Prasanna die Berechtigung für `SELECT`.  

    ```sql  
    CREATE SCHEMA Sprockets AUTHORIZATION Annik  
        CREATE TABLE NineProngs (source int, cost int, partnumber int)  
        GRANT SELECT ON SCHEMA::Sprockets TO Mandar  
        DENY SELECT ON SCHEMA::Sprockets TO Prasanna;  
    GO  
    ```  
5. Führen Sie die folgende Anweisung aus, um die Schemas in dieser Datenbank anzuzeigen:

   ```sql
   SELECT * FROM sys.schemas;
   ```

 Weitere Informationen finden Sie unter [CREATE SCHEMA &#40;Transact-SQL&#41;](../../../t-sql/statements/create-schema-transact-sql.md).  
  
  

