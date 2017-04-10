---
title: "Umbenennen von Indizes | Microsoft Docs"
ms.custom: ""
ms.date: "02/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-indexes"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Umbenennen von Indizes"
  - "Indexnamen [SQL Server]"
  - "Indizes [SQL Server], umbenennen"
ms.assetid: d3d612a1-ea1b-4d99-85d2-0a2ad54f4b0e
caps.latest.revision: 27
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 27
---
# Umbenennen von Indizes
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie ein Index in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]umbenannt wird. Wenn Sie einen Index umbenennen, wird der aktuelle Name des Indexes durch den neuen Namen ersetzt, den Sie bereitstellen. Der angegebene Name muss innerhalb der Tabelle oder Sicht eindeutig sein. So können z.B. zwei Tabellen über einen Index mit dem Namen **XPK_1** verfügen; innerhalb derselben Tabelle können jedoch nicht zwei Indizes mit dem Namen **XPK_1** verwendet werden. Sie können keinen Index mit dem gleichen Namen erstellen, den ein vorhandener deaktivierter Index aufweist. Das Umbenennen eines Indexes bewirkt nicht, dass der Index neu erstellt wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So benennen Sie einen Index um mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
 Wenn Sie eine PRIMARY KEY- oder eine UNIQUE-Einschränkung für eine Tabelle erstellen, wird für die Tabelle automatisch ein Index erstellt, der denselben Namen wie die Einschränkung erhält. Da Indexnamen innerhalb der Tabelle eindeutig sein müssen, können Sie keinen Index erstellen oder umbenennen, wenn dieser anschließend denselben Namen wie eine vorhandene PRIMARY KEY- oder UNIQUE-Einschränkung für die Tabelle verwendet.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für den Index.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So benennen Sie einen Index mit dem Tabellen-Designer um  
  
1.  Klicken Sie im Objekt-Explorer auf das Pluszeichen, um die Datenbank zu erweitern, die die Tabelle enthält, in der Sie einen Index umbenennen möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Tabellen** zu erweitern.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Tabelle, für die Sie einen Index umbenennen möchten, und wählen Sie **Entwurf**.  
  
4.  Klicken Sie im Menü **Tabellen-Designer** auf **Indizes/Schlüssel**.  
  
5.  Wählen Sie im Textfeld **Ausgewählter Primärschlüssel/eindeutiger Schlüssel oder Index** den Index aus, den Sie umbenennen möchten.  
  
6.  Klicken Sie im Raster auf **Name** , und geben Sie in das Textfeld einen neuen Namen ein.  
  
7.  Klicken Sie auf **Schließen**.  
  
8.  Klicken Sie im Menü **Datei** auf **Speichern** *table_name*.  
  
#### So benennen Sie einen Index mit dem Objekt-Explorer um  
  
1.  Klicken Sie im Objekt-Explorer auf das Pluszeichen, um die Datenbank zu erweitern, die die Tabelle enthält, in der Sie einen Index umbenennen möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Tabellen** zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um die Tabelle zu erweitern, für die Sie einen Index umbenennen möchten.  
  
4.  Klicken Sie auf das Pluszeichen, um den Ordner **Indizes** zu erweitern.  
  
5.  Klicken Sie mit der rechten Maustaste auf den Index, den Sie umbenennen möchten, und wählen Sie **Umbenennen**.  
  
6.  Geben Sie den neuen Namen des Indexes ein, und drücken Sie die EINGABETASTE.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So benennen Sie einen Index um  
  
1.  Stellen Sie im Objekt-Explorer ** **eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    --Renames the IX_ProductVendor_VendorID index on the Purchasing.ProductVendor table to IX_VendorID.   
  
    EXEC sp_rename N'Purchasing.ProductVendor.IX_ProductVendor_VendorID', N'IX_VendorID', N'INDEX';   
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md).  
  
  