---
title: "Aktualisieren einer Datenbank durch Trennen und Anfügen (Transact-SQL) | Microsoft-Dokumentation"
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
- database attaching [SQL Server]
- upgrading databases
- database upgrades [SQL Server]
- database detaching [SQL Server]
- detaching databases [SQL Server]
- attaching databases [SQL Server]
ms.assetid: 99f66ed9-3a75-4e38-ad7d-6c27cc3529a9
caps.latest.revision: 73
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d99342c070c23962b70592f3607bc17832815cdc
ms.lasthandoff: 04/11/2017

---
# <a name="upgrade-a-database-using-detach-and-attach-transact-sql"></a>Aktualisieren einer Datenbank durch Trennen und Anfügen (Transact-SQL)
  In diesem Thema wird beschrieben, wie Sie Trenn- und Anfügevorgänge verwenden, um eine Datenbank in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]zu aktualisieren. Nach dem Anfügen an [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]ist die Datenbank sofort verfügbar und wird automatisch aktualisiert.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Empfehlungen](#Recommendations)  
  
-   **So aktualisieren Sie eine SQL Server-Datenbank:**  
  
     [Verwenden von Trenn- und Anfügevorgängen](#SSMSProcedure)  
  
-   **Follow Up:**  [After Upgrading a SQL Server Database](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Die Systemdatenbanken können nicht angefügt werden.  
  
-   Durch das Anfügen und Trennen wird die datenbankübergreifende Besitzverkettung für die Datenbank deaktiviert, da deren Option **datenbankübergreifende Besitzverkettung** auf 0 festgelegt wird. Informationen zum Aktivieren der Verkettung finden Sie unter [Datenbankübergreifende Besitzverkettung (Serverkonfigurationsoption)](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md).  
  
-   Wenn Sie eine replizierte Datenbank anfügen, die nicht getrennt, sondern kopiert wurde:  
  
    -   Wenn Sie die Datenbank an eine aktualisierte Version derselben Serverinstanz anfügen, müssen Sie **sp_vupgrade_replication** ausführen, um die Replikation zu aktualisieren, nachdem der Anfügevorgang abgeschlossen wurde. Weitere Informationen finden Sie unter [sp_vupgrade_replication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql.md).  
  
    -   Wenn Sie die Datenbank an eine andere Serverinstanz anfügen, müssen Sie (unabhängig von der Version) **sp_removedbreplication** ausführen, um die Replikation zu entfernen, nachdem der Anfügevorgang abgeschlossen wurde. Weitere Informationen finden Sie unter [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
###  <a name="Recommendations"></a> Empfehlungen  
 Das Anfügen oder Wiederherstellen von Datenbanken aus unbekannten oder nicht vertrauenswürdigen Quellen wird nicht empfohlen. Solche Datenbanken können bösartigen Code enthalten, der möglicherweise unbeabsichtigten [!INCLUDE[tsql](../../includes/tsql-md.md)] -Code ausführt oder Fehler verursacht, indem er das Schema oder die physische Datenbankstruktur ändert. Bevor Sie eine Datenbank aus einer unbekannten oder nicht vertrauenswürdigen Quelle verwenden, führen Sie auf einem Nichtproduktionsserver [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) für die Datenbank aus. Überprüfen Sie außerdem den Code in der Datenbank, z.B. gespeicherte Prozeduren oder anderen benutzerdefinierten Code.  
  
##  <a name="SSMSProcedure"></a> So aktualisieren Sie eine Datenbank durch Trennen und Anfügen  
  
1.  Trennen Sie die Datenbank. Weitere Informationen finden Sie unter [Trennen einer Datenbank](../../relational-databases/databases/detach-a-database.md).  
  
2.  Optional können Sie die getrennte(n) Datenbankdatei(en) und die Protokolldatei(en) verschieben.  
  
     Sie sollten die Protokolldateien zusammen mit den Datendateien verschieben, auch wenn Sie neue Protokolldateien erstellen möchten. In manchen Fällen sind zum erneuten Anfügen der Datenbank die vorhandenen Protokolldateien erforderlich. Deshalb sollten Sie immer alle getrennten Protokolldateien behalten, bis die Datenbank ohne sie erfolgreich angefügt wurde.  
  
    > [!NOTE]  
    >  Wenn Sie versuchen, die Datenbank ohne Angabe der Protokolldatei anzufügen, wird die Protokolldatei an ihrem ursprünglichen Speicherort gesucht. Ist die ursprüngliche Kopie des Protokolls an diesem Speicherort noch vorhanden, wird diese Kopie angefügt. Wenn Sie die Verwendung der ursprünglichen Protokolldatei verhindern möchten, geben Sie entweder den Pfad der neuen Protokolldatei an, oder entfernen Sie die ursprüngliche Kopie der Protokolldatei (nachdem Sie sie an einen neuen Speicherort kopiert haben).  
  
3.  Fügen Sie die kopierten Dateien an die Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]an. Weitere Informationen finden Sie unter [Attach a Database](../../relational-databases/databases/attach-a-database.md).  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird eine Kopie einer Datenbank aus einer früheren Version von SQL Server aktualisiert. Die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen werden in einem Abfrage-Editorfenster ausgeführt, das mit der Serverinstanz verbunden ist, an die es angefügt ist.  
  
1.  Führen Sie die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen aus, um die Datenbank zu trennen:  
  
    ```  
    USE master;  
    GO  
    EXEC sp_detach_db @dbname = N'MyDatabase';  
    GO  
    ```  
  
2.  Kopieren Sie die Daten- und Protokolldateien an den neuen Speicherort, indem Sie die von Ihnen bevorzugte Vorgehensweise verwenden.  
  
    > [!IMPORTANT]  
    >  Platzieren Sie Datenbank und Transaktionsprotokoll bei einer Produktionsdatenbank auf separaten Datenträgern.  
  
     Um Dateien im Netzwerk auf einen Datenträger auf einem Remotecomputer zu kopieren, verwenden Sie den UNC-Namen (Universal Naming Convention) des Remotespeicherorts. Ein UNC-Name hat das Format **\\\\***Servername***\\***Sharename***\\***Path***\\***Filename*. Wie beim Schreiben von Dateien auf die lokale Festplatte müssen die entsprechenden Berechtigungen für das Lesen oder Schreiben einer Datei auf dem Remotedatenträger dem von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz verwendeten Benutzerkonto erteilt werden.  
  
3.  Führen Sie die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung aus, um die verschobene Datenbank und optional das zugehörige Protokoll anzufügen:  
  
    ```  
    USE master;  
    GO  
    CREATE DATABASE MyDatabase   
        ON (FILENAME = 'C:\MySQLServer\MyDatabase.mdf'),  
        (FILENAME = 'C:\MySQLServer\Database.ldf')  
        FOR ATTACH;  
    GO  
    ```  
  
     In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ist eine neu angefügte Datenbank nicht sofort im Objekt-Explorer sichtbar. Um die Datenbank anzuzeigen, klicken Sie im Objekt-Explorer im Menü **Ansicht** auf **Aktualisieren**. Wenn der **Datenbanken** -Knoten im Objekt-Explorer erweitert wird, wird nun die neu angefügte Datenbank in der Liste der Datenbanken angezeigt.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Aktualisieren einer SQL Server-Datenbank  
 Wenn die Datenbank Volltextindizes aufweist, werden diese beim Upgrade entweder importiert, zurückgesetzt oder neu erstellt, je nach der Einstellung der Servereigenschaft **upgrade_option** . Wenn die Upgradeoption auf „Importieren“ (**upgrade_option** = 2) oder Neu erstellen (**upgrade_option** = 0) festgelegt ist, sind die Volltextindizes während des Upgrades nicht verfügbar. Je nach Menge der indizierten Daten kann der Importvorgang mehrere Stunden dauern; die Neuerstellung sogar bis zu zehnmal länger. Wenn die Upgradeoption auf Importieren festgelegt ist und kein Volltextkatalog verfügbar ist, werden die zugehörigen Volltextindizes neu erstellt. Um die Einstellung der Servereigenschaft **upgrade_option** zu ändern, verwenden Sie [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md).  
  
### <a name="database-compatibility-level-after-upgrade"></a>Datenbank-Kompatibilitätsgrad nach dem Upgrade  
 War der Kompatibilitätsgrad einer Benutzerdatenbank vor dem Upgrade 100 oder höher, wird er nach dem Upgrade beibehalten. War der Kompatibilitätsgrad der aktualisierten Datenbank vor dem Upgrade auf 90 festgelegt, wird er auf 100 erhöht, was dem niedrigsten unterstützten Kompatibilitätsgrad in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] entspricht. Weitere Informationen finden Sie unter [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
### <a name="managing-metadata-on-the-upgraded-server-instance"></a>Verwalten von Metadaten auf der aktualisierten Serverinstanz  
 Wenn Sie eine Datenbank an eine andere Serverinstanz anfügen, müssen Sie möglicherweise einen Teil oder auch alle Metadaten für die Datenbank (z. B. Anmeldenamen, Aufträge und Berechtigungen) auf der anderen Serverinstanz erneut erstellen, um Benutzern und Anwendungen ein konsistentes Verhalten bereitzustellen. Weitere Informationen finden Sie unter [Verwalten von Metadaten beim Bereitstellen einer Datenbank auf einer anderen Serverinstanz &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  
### <a name="service-master-key-and-database-master-key-encryption-changes-from-3des-to-aes"></a>Die Verschlüsselung des Diensthauptschlüssels und Datenbank-Hauptschlüssels wird von 3DES in AES geändert.  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und höhere Versionen schützen den Diensthauptschlüssel (Service Master Key, SMK) und den Datenbank-Hauptschlüssel (Database Master Key, DMK) mithilfe des AES-Verschlüsselungsalgorithmus. AES ist ein neuerer Verschlüsselungsalgorithmus als der in früheren Versionen verwendete 3DES-Algorithmus. Wird eine Datenbank zum ersten Mal an eine neue Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]angefügt oder wiederhergestellt, ist noch keine Kopie des Datenbank-Hauptschlüssels (verschlüsselt vom Diensthauptschlüssel) auf dem Server gespeichert. Der Datenbank-Hauptschlüssel (Database Master Key, DMK) muss mithilfe der Anweisung **OPEN MASTER KEY** entschlüsselt werden. Nachdem der Datenbank-Hauptschlüssel entschlüsselt wurde, können Sie für die Zukunft die automatische Entschlüsselung aktivieren, indem Sie die Anweisung **ALTER MASTER KEY REGENERATE** verwenden. Auf diese Weise können Sie eine Kopie des mit dem Diensthauptschlüssel (Service Master Key, SMK) verschlüsselten Datenbank-Hauptschlüssels für den Server bereitstellen. Wenn eine Datenbank von einer früheren Version aktualisiert wurde, sollte der DMK neu generiert werden, damit er den neueren AES-Algorithmus verwendet. Weitere Informationen zum Neugenerieren des DMK finden Sie unter [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md). Die zum Neugenerieren des DMK zum Upgrade auf AES erforderliche Zeit hängt von der Anzahl der Objekte ab, die durch den DMK geschützt werden. Der DMK muss nur einmal auf AES aktualisiert und neu generiert werden. Dies hat keine Auswirkungen auf zukünftige Neugenerierungen im Rahmen einer Schlüsselrotationsstrategie.  
  
  
