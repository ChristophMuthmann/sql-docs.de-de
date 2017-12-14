---
title: Verkleinern einer Datei | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.shrinkfile.f1
helpviewer_keywords:
- shrinking files
- decreasing file size
- databases [SQL Server], shrinking
- reducing file size
- size [SQL Server], files
- file size [SQL Server]
ms.assetid: ce5c8798-c039-4ab2-81e7-90a8d688b893
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 833d84c44f7c2ef9cae31cf1908cd5732518b469
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="shrink-a-file"></a>Verkleinern einer Datei
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie eine Daten- oder Protokolldatei in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)] verkleinert wird.  
  
 Mit dem Verkleinern von Datendateien wird Platz gewonnen, indem Datenseiten vom Ende der Datei an nicht belegten Platz weiter am Dateianfang verschoben werden. Wurde am Ende der Datei ausreichend Platz geschaffen, kann die Zuordnung der Datenseiten am Ende der Datei aufgehoben und die Datenseiten können ins Dateisystem zurückgegeben werden.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Empfehlungen](#Recommendations)  
  
     [Sicherheit](#Security)  
  
-   **So verkleinern Sie eine Daten- oder Protokolldatei mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Die primäre Datendatei kann nicht kleiner als die Größe der primären Datei in der model-Datenbank werden.  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Die zum Verkleinern einer Datei verschobenen Daten können an beliebigen freien Platz in der Datei verschoben werden. Dies führt zur Indexfragmentierung und kann die Leistung von Abfragen, die einen Bereich des Indexes suchen, verlangsamen. Zur Vermeidung von Fragmentierung sollten die Dateiindizes nach der Verkleinerung neu erstellt werden.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** oder der festen Datenbankrolle **db_owner** .  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-shrink-a-data-or-log-file"></a>So verkleinern Sie eine Daten- oder Protokolldatei  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **Datenbanken** , und klicken Sie dann mit der rechten Maustaste auf die Datenbank, die Sie verkleinern möchten.  
  
3.  Zeigen Sie auf **Tasks**, zeigen Sie auf **Verkleinern**, und klicken Sie dann auf **Dateien**.  
  
     **Datenbank**  
     Zeigt den Namen der ausgewählten Datenbank an.  
  
     **Dateityp**  
     Wählen Sie den Dateityp für die Datei aus. Die verfügbaren Auswahlmöglichkeiten für den Dateityp sind **Daten** und **Protokoll** . Die Standardauswahl ist **Daten**. Bei der Auswahl eines anderen Dateigruppentyps wird die Auswahl in den anderen Feldern entsprechend geändert.  
  
     **Dateigruppe**  
     Wählen Sie eine Dateigruppe aus der Liste der Dateigruppen aus, die dem oben genannten **Dateityp** zugewiesen sind. Bei der Auswahl einer anderen Dateigruppe wird die Auswahl in den anderen Feldern entsprechend geändert.  
  
     **Dateiname**  
     Wählen Sie eine Datei aus der Liste der verfügbaren Dateien aus, die der ausgewählten Dateigruppe und dem Dateityp entspricht.  
  
     **Speicherort**  
     Zeigt den vollständigen Pfad zur aktuell ausgewählten Datei an. Dieser Pfad kann nicht bearbeitet, aber in die Zwischenablage kopiert werden.  
  
     **Aktuell zugeordneter Speicherplatz**  
     Zeigt bei Datendateien den aktuell zugeordneten Speicherplatz an. Bei Protokolldateien wird der aktuell zugeordnete Speicherplatz angezeigt, der auf der Basis der Ausgabe von DBCC SQLPERF (LOGSPACE) berechnet wurde.  
  
     **Verfügbarer freier Speicherplatz**  
     Zeigt bei Datendateien den aktuell verfügbaren freien Speicherplatz an, der auf der Basis der Ausgabe von DBCC SHOWFILESTATS (fileid) berechnet wurde. Bei Protokolldateien wird der aktuell verfügbare freie Speicherplatz angezeigt, der auf der Basis der Ausgabe von DBCC SQLPERF (LOGSPACE) berechnet wurde.  
  
     **Nicht verwendeten Speicherplatz freigeben**  
     Bewirkt, dass ungenutzter Speicherplatz in den Dateien an das Betriebssystem freigegeben und die Datei auf die zuletzt zugeordnete Größe verkleinert wird, wodurch die Dateigröße ohne Verschieben von Daten reduziert wird. Es wird nicht versucht, verfügbaren Seiten Zeilen erneut zuzuordnen.  
  
     **Seiten vor dem Freigeben von nicht verwendetem Speicherplatz neu organisieren**  
     Entspricht dem Ausführen von DBCC SHRINKFILE zur Angabe der Zieldateigröße. Wenn diese Option ausgewählt ist, muss der Benutzer eine Zieldateigröße im Feld **Datei verkleinern auf** angeben.  
  
     **Datei verkleinern auf**  
     Gibt die Zieldateigröße für den Verkleinerungsvorgang an. Die Größe kann nicht kleiner als der aktuell zugeordnete Speicherplatz und nicht größer als die Summe der Blöcke sein, die der Datei zugeordnet sind. Wenn ein Wert außerhalb der Grenzen eingegeben wird, wird der entsprechend nähere Grenzwert wiederhergestellt, sobald der Fokus geändert oder auf eine der Schaltflächen auf der Symbolleiste geklickt wird.  
  
     **Datei durch Migrieren ihrer Daten zu anderen Dateien in der gleichen Dateigruppe leeren**  
     Migriert alle Daten aus der angegebenen Datei. Diese Option ermöglicht das Löschen der Datei mit der ALTER DATABASE-Anweisung. Sie entspricht dem Ausführen von DBCC SHRINKFILE mit der Option EMPTYFILE.  
  
4.  Wählen Sie den Dateityp und den Dateinamen aus.  
  
5.  Aktivieren Sie optional das Kontrollkästchen **Nicht verwendeten Speicherplatz freigeben** .  
  
     Wenn diese Option ausgewählt wird, wird ungenutzter Speicherplatz in der Datei für das Betriebssystem freigegeben und die Datei auf den zuletzt zugeordneten Block verkleinert. Durch diesen Vorgang wird die Dateigröße ohne Verschieben von Daten reduziert.  
  
6.  Aktivieren Sie optional das Kontrollkästchen **Dateien vor dem Freigeben von nicht belegtem Speicherplatz neu organisieren** . Wenn dieses Kontrollkästchen aktiviert ist, muss der Wert **Datei verkleinern auf** angegeben werden. Standardmäßig ist diese Option deaktiviert.  
  
     Wenn diese Option ausgewählt wird, wird ungenutzter Speicherplatz in der Datei für das Betriebssystem freigegeben, und es wird versucht, Zeilen in nicht zugeordnete Seiten zu verschieben.  
  
7.  Geben Sie optional den maximalen Prozentsatz an freiem Speicherplatz ein, der in der Datenbankdatei verbleiben soll, nachdem die Datenbank verkleinert wurde. Der zulässige Wert liegt zwischen 0 und 99. Diese Option ist nur verfügbar, wenn **Dateien vor dem Freigeben von nicht belegtem Speicherplatz neu organisieren** aktiviert ist.  
  
8.  Aktivieren Sie optional das Kontrollkästchen **Datei durch Migrieren ihrer Daten zu anderen Dateien in der gleichen Dateigruppe leeren** .  
  
     Wenn Sie diese Option aktivieren, werden alle Daten aus der angegebenen Datei in andere Dateien in der Dateigruppe verschoben. Die leere Datei kann anschließend gelöscht werden. Diese Option entspricht dem Ausführen von DBCC SHRINKFILE mit der EMPTYFILE-Option.  
  
9. Klicken Sie auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-shrink-a-data-or-log-file"></a>So verkleinern Sie eine Daten- oder Protokolldatei  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird [DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md) verwendet, um die Größe einer Datendatei mit dem Namen `DataFile1` in der Datenbank `UserDB` auf 7 MB zu verkleinern.  
  
 [!code-sql[DBCC#DBCC_SHRINKFILE1](../../relational-databases/databases/codesnippet/tsql/shrink-a-file_1.sql)]  
  
## <a name="see-also"></a>Siehe auch  
 [DBCC SHRINKDATABASE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)   
 [Verkleinern einer Datenbank](../../relational-databases/databases/shrink-a-database.md)   
 [Löschen von Daten- oder Protokolldateien aus einer Datenbank](../../relational-databases/databases/delete-data-or-log-files-from-a-database.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
  
  
