---
title: "Wiederherstellen des Diensthauptschlüssels | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- service master key [SQL Server], importing
- service master key [SQL Server], restoring
ms.assetid: 14bdbbbe-d384-4692-b670-4243d2466fe1
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 341662ff65d44b63738b869999ab78191f991a6f
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="restore-the-service-master-key"></a>Wiederherstellen des Diensthauptschlüssels
  In diesem Thema wird beschrieben, wie der Diensthauptschlüssel in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[tsql](../../../includes/tsql-md.md)]wiederhergestellt wird.  
  
> [!WARNING]  
>  Es ist unwahrscheinlich, dass die Notwendigkeit zum Wiederherstellen des Diensthauptschlüssels eintreten wird. Sollte dies doch erforderlich sein, muss dies mit äußerster Sorgfalt erfolgen. Weitere Informationen finden Sie unter [Back Up the Service Master Key](../../../relational-databases/security/encryption/back-up-the-service-master-key.md).  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   [So stellen Sie den Diensthauptschlüssel mithilfe von Transact-SQL wieder her](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Bei der Wiederherstellung des Diensthauptschlüssels werden alle Schlüssel und geheimen Bereiche von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] entschlüsselt, die mit dem aktuellen Diensthauptschlüssel verschlüsselt wurden. Diese Schlüssel werden dann mit dem aus der Sicherungsdatei geladenen Diensthauptschlüssel verschlüsselt.  
  
-   Falls einer dieser Entschlüsselungsvorgänge nicht erfolgreich ausgeführt werden kann, tritt bei der Wiederherstellung ein Fehler auf. Sie können die FORCE-Option verwenden, um Fehler zu ignorieren, dies kann jedoch zum Verlust von Daten führen, die nicht entschlüsselt werden können.  
  
-   Das Neugenerieren der Verschlüsselungshierarchie ist ein ressourcenintensiver Vorgang. Die Ausführung dieses Vorgangs sollte außerhalb der Hauptzeiten geplant werden.  
  
> [!CAUTION]  
>  Der Diensthauptschlüssel ist der Stamm der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verschlüsselungshierarchie. Mit dem Diensthauptschlüssel werden alle Schlüssel in der Struktur direkt oder indirekt geschützt. Wenn ein abhängiger Schlüssel während der erzwungenen Wiederherstellung nicht entschlüsselt werden kann, gehen die durch diesen Schlüssel geschützten Daten verloren.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die CONTROL SERVER-Berechtigung auf dem Server.  
  
##  <a name="SSMSProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-restore-the-service-master-key"></a>So stellen Sie den Diensthauptschlüssel wieder her  
  
1.  Rufen Sie entweder von einem physischen Sicherungsmedium oder einem Verzeichnis im lokalen Dateisystem eine Kopie des gesicherten Diensthauptschlüssels ab.  
  
2.  Stellen Sie im Objekt-Explorer **** eine Verbindung mit einer [!INCLUDE[ssDE](../../../includes/ssde-md.md)]-Instanz her.  
  
3.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
4.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- Restores the service master key from a backup file.  
    RESTORE SERVICE MASTER KEY   
        FROM FILE = 'c:\temp_backups\keys\service_master_key'   
        DECRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';  
    GO  
    ```  
  
    > [!NOTE]  
    >  Der Dateipfad zum Schlüssel und das Kennwort (sofern es vorhanden ist) des Schlüssels unterscheiden sich von den obigen Informationen. Stellen Sie sicher, dass beide für den Server und die Schlüsseleinrichtung spezifisch sind.  
  
  
