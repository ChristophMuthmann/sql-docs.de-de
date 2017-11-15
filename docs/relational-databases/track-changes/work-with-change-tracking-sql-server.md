---
title: "Verwenden der Änderungsnachverfolgung (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- change tracking [SQL Server], making changes
- change tracking [SQL Server], troubleshooting
- updating data [SQL Server]
- troubleshooting [SQL Server], change tracking
- data changes [SQL Server]
- tracking data changes [SQL Server]
- data [SQL Server], changing
- change tracking [SQL Server], data restore
- change tracking [SQL Server], ensuring consistent results
- change tracking [SQL Server], handling changes
ms.assetid: 5aec22ce-ae6f-4048-8a45-59ed05f04dc5
caps.latest.revision: "26"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: faa2c1baefe2d745944ef42239675f1766d0e6e5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="work-with-change-tracking-sql-server"></a>Verwenden der Änderungsnachverfolgung (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Anwendungen, die die Änderungsnachverfolgung verwenden, müssen in der Lage sein,  Überarbeitungen abzurufen, diese auf einen anderen Datenspeicher anzuwenden und die Quelldatenbank zu aktualisieren. In diesem Thema wird beschrieben, wie diese Tasks ausgeführt werden. Zudem wird beschrieben, welche Rolle die Änderungsnachverfolgung spielt, wenn ein Failover auftritt und eine Datenbank von einer Sicherung wiederhergestellt werden muss.  
  
##  <a name="Obtain"></a> Abrufen von Änderungen mithilfe der Änderungsnachverfolgungsfunktionen  
 Beschreibt, wie mithilfe der Änderungsnachverfolgungsfunktionen Änderungen und Informationen zu den in einer Datenbank vorgenommenen Änderungen abgerufen werden können.  
  
### <a name="about-the-change-tracking-functions"></a>Informationen zu Änderungsnachverfolgungsfunktionen  
 Anwendungen können mit den folgenden Funktionen die in einer Datenbank vorgenommenen Änderungen sowie die Informationen zu diesen Änderungen abrufen:  
  
 CHANGETABLE(CHANGES …)-Funktion  
 Diese Rowsetfunktion wird verwendet, um Änderungsinformationen abzufragen. Die Funktion fragt die in den internen Änderungsnachverfolgungstabellen gespeicherten Daten ab. Die Funktion gibt ein Resultset zurück, das die Primärschlüssel der Zeilen enthält, die sich geändert haben. Außerdem werden weitere Informationen zurückgegeben, z. B. der Vorgang, die aktualisierten Spalten und die Version der Zeile.  
  
 CHANGETABLE(CHANGES …) verwendet die letzte Synchronisierungsversion als Argument. Die letzte Synchronisierungsversion wird mit der `@last_synchronization_version` -Variablen abgerufen. Die Semantik der letzten Synchronisierungsversion lautet wie folgt:  
  
-   Der aufrufende Client hat alle Änderungen bis zur letzten Synchronisierungsversion (einschließlich) abgerufen.  
  
-   CHANGETABLE(CHANGES …) gibt also alle Änderungen zurück, die nach der letzten Synchronisierungsversion vorgenommen wurden.  
  
     Die folgende Abbildung zeigt, wie CHANGETABLE (CHANGES.) verwendet wird, um Änderungen abzurufen.  
  
     ![Beispiel für Abfrageausgabe bei der Änderungsnachverfolgung](../../relational-databases/track-changes/media/queryoutput.gif "Beispiel für Abfrageausgabe bei der Änderungsnachverfolgung")  
  
 CHANGE_TRACKING_CURRENT_VERSION()-Funktion  
 Diese Funktion wird zum Abrufen der aktuellen Version verwendet. Diese wird das nächste Mal verwendet, wenn Änderungen abgerufen werden. Diese Version stellt die Version der letzten Transaktion dar, für die ein Commit ausgeführt wurde.  
  
 CHANGE_TRACKING_MIN_VALID_VERSION()-Funktion  
 Diese Funktion wird verwendet, um die minimal gültige Version abzurufen, über die ein Client verfügen muss, damit CHANGETABLE() gültige Ergebnisse zurückgibt. Der Client muss die Version der letzten Synchronisierung mit dem Wert abgleichen, der von dieser Funktion zurückgegeben wird. Wenn die Version der letzten Synchronisierung niedriger ist als die von dieser Funktion zurückgegebene Version, kann der Client keine gültigen Ergebnisse von CHANGETABLE() abrufen und muss neu initialisiert werden.  
  
### <a name="obtaining-initial-data"></a>Abrufen der Anfangsdaten  
 Damit eine Anwendung Änderungen abrufen kann, muss sie zunächst die Anfangsdaten und die Synchronisierungsversion abfragen. Die Anwendung muss die entsprechenden Daten direkt aus der Tabelle abrufen und dann CHANGE_TRACKING_CURRENT_VERSION() zum Abrufen der Anfangsversion verwenden. Diese Version wird beim ersten Abrufen von Änderungen an CHANGETABLE (CHANGES.) übergeben.  
  
 Das folgende Beispiel zeigt, wie die Anfangsversion der Synchronisierung und das Anfangsdataset abgerufen werden.  
  
```tsql  
    -- Obtain the current synchronization version. This will be used next time that changes are obtained.  
    SET @synchronization_version = CHANGE_TRACKING_CURRENT_VERSION();  
  
    -- Obtain initial data set.  
    SELECT  
        P.ProductID, P.Name, P.ListPrice  
    FROM  
        SalesLT.Product AS P  
```  
  
### <a name="using-the-change-tracking-functions-to-obtain-changes"></a>Verwenden der Änderungsnachverfolgungsfunktionen zum Abrufen von Änderungen  
 Verwenden Sie die Funktion CHANGETABLE(CHANGES…), um die geänderten Zeilen einer Tabelle und die zugehörigen Änderungsinformationen abzurufen. Beispielsweise werden mit der folgenden Abfrage die Änderungen für die `SalesLT.Product` -Tabelle abgerufen.  
  
```tsql  
SELECT  
    CT.ProductID, CT.SYS_CHANGE_OPERATION,  
    CT.SYS_CHANGE_COLUMNS, CT.SYS_CHANGE_CONTEXT  
FROM  
    CHANGETABLE(CHANGES SalesLT.Product, @last_synchronization_version) AS CT  
  
```  
  
 In der Regel möchte ein Client nicht nur die Primärschlüssel, sondern die neuesten Daten für eine Zeile abrufen. In diesem Fall führt eine Anwendung die Ergebnisse der CHANGETABLE(CHANGES …)-Funktion mit den Daten in der Benutzertabelle zusammen. Beispiel: Bei der folgenden Abfrage wird die Funktion mit der `SalesLT.Product` -Tabelle verknüpft, um die Werte der `Name` -Spalte und der `ListPrice` -Spalte abzurufen. Beachten Sie, dass `OUTER JOIN`verwendet wird. Dies ist erforderlich, um sicherzustellen, dass die Änderungsinformationen für die Zeilen zurückgegeben werden, die aus der Benutzertabelle gelöscht wurden.  
  
```tsql  
SELECT  
    CT.ProductID, P.Name, P.ListPrice,  
    CT.SYS_CHANGE_OPERATION, CT.SYS_CHANGE_COLUMNS,  
    CT.SYS_CHANGE_CONTEXT  
FROM  
    SalesLT.Product AS P  
RIGHT OUTER JOIN  
    CHANGETABLE(CHANGES SalesLT.Product, @last_synchronization_version) AS CT  
ON  
    P.ProductID = CT.ProductID  
```  
  
 Verwenden Sie die CHANGE_TRACKING_CURRENT_VERSION()-Funktion wie im folgenden Beispiel gezeigt, um die in der nächsten Änderungsenumeration zu verwendende Version abzurufen.  
  
```tsql  
SET @synchronization_version = CHANGE_TRACKING_CURRENT_VERSION()  
```  
  
 Beim Abrufen von Änderungen muss eine Anwendung sowohl CHANGETABLE(CHANGES...) als auch CHANGE_TRACKING_CURRENT_VERSION() verwenden, wie im folgenden Beispiel gezeigt.  
  
```tsql  
-- Obtain the current synchronization version. This will be used the next time CHANGETABLE(CHANGES...) is called.  
SET @synchronization_version = CHANGE_TRACKING_CURRENT_VERSION();  
  
-- Obtain incremental changes by using the synchronization version obtained the last time the data was synchronized.  
SELECT  
    CT.ProductID, P.Name, P.ListPrice,  
    CT.SYS_CHANGE_OPERATION, CT.SYS_CHANGE_COLUMNS,  
    CT.SYS_CHANGE_CONTEXT  
FROM  
    SalesLT.Product AS P  
RIGHT OUTER JOIN  
    CHANGETABLE(CHANGES SalesLT.Product, @last_synchronization_version) AS CT  
ON  
    P.ProductID = CT.ProductID  
```  
  
### <a name="version-numbers"></a>Versionsnummern  
 Eine Datenbank mit aktivierter Änderungsnachverfolgung verfügt über einen Versionszähler, der hochgezählt wird, wenn Änderungen an den nachverfolgten Tabellen vorgenommen werden. Jede geänderte Zeile verfügt über eine ihr zugeordnete Versionsnummer. Wenn eine Anforderung zur Abfrage von Änderungen an eine Anwendung gesendet wird, wird eine Funktion aufgerufen, die eine Versionsnummer angibt. Die Funktion gibt Informationen über alle Änderungen zurück, die ab dieser Version vorgenommen wurden. In gewisser Hinsicht entspricht die Änderungsnachverfolgungsversion dem Konzept des **rowversion** -Datentyps.  
  
### <a name="validating-the-last-synchronized-version"></a>Überprüfen der letzten Synchronisierungsversion  
 Informationen über Änderungen werden für einen beschränkten Zeitraum beibehalten. Dieser Zeitraum wird mit dem CHANGE_RETENTION-Parameter festgelegt, der als Teil von ALTER DATABASE angegeben werden kann.  
  
 Beachten Sie, dass der mit CHANGE_RETENTION angegebene Zeitraum festlegt, wie häufig alle Anwendungen Änderungen von der Datenbank anfordern müssen. Wenn der Wert für *last_synchronization_version* einer Anwendung älter ist als die minimal gültige Synchronisierungsversion für eine Tabelle, kann diese Anwendung keine gültige Änderungsenumeration ausführen. Das liegt daran, dass einige Änderungsinformationen möglicherweise bereinigt wurden. Vor dem Abrufen von Änderungen mit CHANGETABLE(CHANGES …) muss eine Anwendung also den Wert von *last_synchronization_version* , der an CHANGETABLE(CHANGES …) übergeben werden soll, überprüfen. Wenn der Wert von *last_synchronization_version* nicht gültig ist, müssen alle Daten von der Anwendung neu initialisiert werden.  
  
 Im folgenden Beispiel wird gezeigt, wie die Gültigkeit des `last_synchronization_version` -Werts für die einzelnen Tabellen überprüft wird.  
  
```tsql  
-- Check individual table.  
IF (@last_synchronization_version < CHANGE_TRACKING_MIN_VALID_VERSION(  
                                   OBJECT_ID('SalesLT.Product')))  
BEGIN  
  -- Handle invalid version and do not enumerate changes.  
  -- Client must be reinitialized.  
END  
```  
  
 Wie im folgenden Beispiel gezeigt, kann die Gültigkeit des `last_synchronization_version` -Werts für alle Tabellen in der Datenbank überprüft werden.  
  
```tsql  
-- Check all tables with change tracking enabled  
IF EXISTS (  
  SELECT COUNT(*) FROM sys.change_tracking_tables  
  WHERE min_valid_version > @last_synchronization_version )  
BEGIN  
  -- Handle invalid version & do not enumerate changes  
  -- Client must be reinitialized  
END  
```  
  
### <a name="using-column-tracking"></a>Verwenden der Spaltennachverfolgung  
 Die Spaltennachverfolgung ermöglicht Anwendungen, Daten statt für die gesamte Zeile nur für die Spalten abzurufen, die geändert wurden. Nehmen Sie z. B. an, eine Tabelle hat ein oder mehrere große Spalten, in denen selten Änderungen vorgenommen werden, sowie andere Spalten, in denen häufig Änderungen vorgenommen werden. Ohne die Spaltennachverfolgung kann eine Anwendung nur die Änderung einer Zeile erkennen, sodass alle Daten, einschließlich der Daten in den großen Spalten, synchronisiert werden müssten. Mit der Spaltennachverfolgung kann eine Anwendung ermitteln, in welcher Spalte Daten geändert wurden, und nur die geänderten Daten synchronisieren.  
  
 Die Spaltennachverfolgungsinformationen sind in der SYS_CHANGE_COLUMNS-Spalte enthalten, die von der CHANGETABLE(CHANGES …)-Funktion zurückgegeben wird.  
  
 Die Spaltennachverfolgung kann so verwendet werden, dass NULL für Spalten ohne Änderungen zurückgegeben wird. Wenn die Spalte in NULL geändert werden kann, muss eine separate Spalte zurückgegeben werden, um anzugeben, ob die Spalte geändert wurde.  
  
 Im folgenden Beispiel wird für die Spalte `CT_ThumbnailPhoto` der Wert `NULL` zurückgegeben, wenn diese nicht geändert wurde. Der Wert dieser Spalte kann jedoch auch `NULL` lauten, da sie in `NULL` geändert werden kann. In diesem Fall kann die Anwendung mit der Spalte `CT_ThumbNailPhoto_Changed` angeben, ob die Spalte geändert wurde.  
  
```tsql  
DECLARE @PhotoColumnId int = COLUMNPROPERTY(  
    OBJECT_ID('SalesLT.Product'),'ThumbNailPhoto', 'ColumnId')  
  
SELECT  
    CT.ProductID, P.Name, P.ListPrice, -- Always obtain values.  
    CASE  
           WHEN CHANGE_TRACKING_IS_COLUMN_IN_MASK(  
                     @PhotoColumnId, CT.SYS_CHANGE_COLUMNS) = 1  
            THEN ThumbNailPhoto  
            ELSE NULL  
      END AS CT_ThumbNailPhoto,  
      CHANGE_TRACKING_IS_COLUMN_IN_MASK(  
                     @PhotoColumnId, CT.SYS_CHANGE_COLUMNS) AS  
                                   CT_ThumbNailPhoto_Changed  
     CT.SYS_CHANGE_OPERATION, CT.SYS_CHANGE_COLUMNS,  
     CT.SYS_CHANGE_CONTEXT  
FROM  
     SalesLT.Product AS P  
INNER JOIN  
     CHANGETABLE(CHANGES SalesLT.Product, @last_synchronization_version) AS CT  
ON  
     P.ProductID = CT.ProductID AND  
     CT.SYS_CHANGE_OPERATION = 'U'  
```  
  
### <a name="obtaining-consistent-and-correct-results"></a>Abrufen von konsistenten und richtigen Ergebnissen  
 Zum Abrufen der Änderungsdaten für eine Tabelle sind mehrere Schritte erforderlich. Beachten Sie, dass möglicherweise inkonsistente oder falsche Ergebnisse zurückgegeben werden, wenn Sie bestimmte Vorgänge nicht berücksichtigen.  
  
 Beispiel: Zum Abrufen der Änderungen in einer Tabelle mit dem Namen Sales und einer Tabelle mit dem Namen SalesOrders führt eine Anwendung die folgenden Schritte aus:  
  
1.  Überprüfung der letzten Synchronisierungsversion mit CHANGE_TRACKING_MIN_VALID_VERSION()  
  
2.  Abrufen der Version, die beim nächsten Abrufen von Änderungen verwendet werden kann, mit CHANGE_TRACKING_CURRENT_VERSION()  
  
3.  Abrufen der Änderungen für die Tabelle Sales mit CHANGETABLE(CHANGES …)  
  
4.  Abrufen der Änderungen für die Tabelle SalesOrders mit CHANGETABLE(CHANGES …)  
  
 In der Datenbank werden zwei Prozesse ausgeführt, die sich auf die von den oben genannten Schritten zurückgegebenen Ergebnisse auswirken können:  
  
-   Der im Hintergrund ausgeführte Cleanupprozess entfernt Änderungsnachverfolgungsinformationen, die älter sind als die angegebene Beibehaltungsdauer.  
  
     Beim Cleanupprozess handelt es sich um einen eigenen, im Hintergrund ausgeführten Prozess, der die Beibehaltungsdauer verwendet, die bei der Konfiguration der Änderungsnachverfolgung für die Datenbank angegeben wurde. Das Problem liegt darin, dass der Cleanupprozess genau in dem Zeitraum nach der Überprüfung der letzten Synchronisierungsversion und vor dem Aufruf von CHANGETABLE(CHANGES…) ausgeführt werden kann. In diesem Fall kann es vorkommen, dass die gerade für gültig befundene letzte Synchronisierungsversion beim Abruf der Änderungen nicht mehr gültig ist. Aus diesem Grund kann es hier zu falschen Ergebnissen kommen.  
  
-   In den Tabellen Sales und SalesOrders werden fortlaufende DML-Vorgänge ausgeführt, wie z. B. folgende:  
  
    -   Mit der CHANGE_TRACKING_CURRENT_VERSION()-Funktion können Änderungen an den Tabellen vorgenommen werden, nachdem die Version für die nächste Aufzählung von Änderungen abgerufen wurde. In diesem Fall werden möglicherweise mehr Änderungen zurückgegeben als erwartet.  
  
    -   Ein Commit für eine Transaktion kann in dem Zeitraum zwischen dem Aufruf der Funktion zum Abrufen der Änderungen in der Tabelle Sales und dem Aufruf der Funktion zum Abrufen der Änderungen in der Tabelle SalesOrders ausgeführt werden. In diesem Fall enthalten die Ergebnisse für die Tabelle SalesOrders möglicherweise einen Fremdschlüsselwert, der in der Tabelle Sales nicht vorhanden ist.  
  
 Zur Handhabung dieser aufgelisteten Fälle wird die Verwendung der Momentaufnahmeisolation empfohlen. Hierdurch können Sie die Konsistenz der Änderungsinformationen sicherstellen und Racebedingungen im Zusammenhang mit dem im Hintergrund ausgeführten Cleanupprozess vermeiden. Ohne die Verwendung von Momentaufnahmetransaktionen ist die Entwicklung einer Anwendung, die die Änderungsnachverfolgung verwendet, mit erheblich mehr Aufwand verbunden.  
  
#### <a name="using-snapshot-isolation"></a>Verwenden der Momentaufnahmeisolation  
 Die Änderungsnachverfolgung wurde für die Verwendung mit der Momentaufnahmeisolation optimiert. Die Momentaufnahmeisolation muss für die Datenbank aktiviert werden. Alle zum Abrufen von Änderungen erforderlichen Schritte müssen in eine Momentaufnahmetransaktion eingeschlossen werden. Hierdurch können Sie sicherstellen, dass die während des Abrufens von Änderungen an den Daten vorgenommenen Änderungen für die Abfragen in der Momentaufnahmetransaktion nicht sichtbar sind.  
  
 Führen Sie die folgenden Schritte aus, um Daten in einer Momentaufnahmetransaktion abzurufen:  
  
1.  Legen Sie die Transaktionsisolationsstufe auf MOMENTAUFNAHME fest, und starten Sie die Transaktion.  
  
2.  Überprüfen Sie die letzte Synchronisierungsversion mit CHANGE_TRACKING_MIN_VALID_VERSION().  
  
3.  Rufen Sie die Version, die bei der nächsten Aufzählung von Änderungen verwendet wird, mit CHANGE_TRACKING_CURRENT_VERSION() ab.  
  
4.  Rufen Sie die Änderungen für die Tabelle Sales mit CHANGETABLE(CHANGES …) ab.  
  
5.  Rufen Sie die Änderungen für die Tabelle SalesOrders mit CHANGETABLE(CHANGES …) ab.  
  
6.  Führen Sie einen Commit für die Transaktion aus.  
  
 Folgendes ist zu beachten, wenn alle Schritte zum Abrufen von Änderungen innerhalb einer Momentaufnahmetransaktion erfolgen:  
  
-   Wenn nach der Überprüfung der letzten Synchronisierungsversion eine Bereinigung durchgeführt wird, sind die Ergebnisse der CHANGETABLE(CHANGES …)-Funktion dennoch gültig, da die vom Cleanupprozess durchgeführten Löschvorgänge innerhalb der Transaktion nicht sichtbar sind.  
  
-   Alle Änderungen, die nach dem Abrufen der nächsten Synchronisierungsversion an den Tabellen Sales und SalesOrders vorgenommen werden, sind nicht sichtbar, und der Aufruf der CHANGETABLE(CHANGES …)-Funktion gibt keine Änderungen mit Versionen zurück, die neuer sind als die von der CHANGE_TRACKING_CURRENT_VERSION()-Funktion zurückgegebene Version. Die Konsistenz zwischen den Tabellen Sales und SalesOrders wird ebenfalls sichergestellt, da die Transaktionen, für die ein Commit zwischen den Aufrufen der CHANGETABLE(CHANGES …)-Funktion ausgeführt wird, nicht sichtbar sind.  
  
 Das folgende Beispiel zeigt, wie die Momentaufnahmeisolation für eine Datenbank aktiviert wird.  
  
```tsql  
-- The database must be configured to enable snapshot isolation.  
ALTER DATABASE AdventureWorksLT  
    SET ALLOW_SNAPSHOT_ISOLATION ON;  
```  
  
 Eine Momentaufnahmetransaktion wird wie folgt verwendet:  
  
```tsql  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
BEGIN TRAN  
  -- Verify that version of the previous synchronization is valid.  
  -- Obtain the version to use next time.  
  -- Obtain changes.  
COMMIT TRAN  
```  
  
 Weitere Informationen über Momentaufnahmentransaktion finden Sie unter [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
#### <a name="alternatives-to-using-snapshot-isolation"></a>Alternativen zur Verwendung der Momentaufnahmeisolation  
 Es gibt Alternativen zur Verwendung der Momentaufnahmeisolation, die jedoch einen größeren Aufwand erfordern, um sicherzustellen, dass alle Anwendungsanforderungen erfüllt werden. Gehen Sie wie folgt vor, um sicherzustellen, dass der Wert *last_synchronization_version* gültig ist und dass vor dem Abrufen der Änderungen keine Daten durch den Cleanupprozess entfernt werden:  
  
1.  Überprüfen Sie den Wert *last_synchronization_version* nach dem Aufrufen der CHANGETABLE()-Funktion.  
  
2.  Überprüfen Sie den Wert *last_synchronization_version* bei jeder Abfrage zum Abrufen von Änderungen mit CHANGETABLE().  
  
 Änderungen können nach dem Abrufen der Synchronisierungsversion für die nächste Aufzählung auftreten. Dieses Problem lässt sich auf zwei Arten lösen: Welche Option Sie verwenden, hängt von der Anwendung ab und wie diese die Nebeneffekte des jeweiligen Ansatzes handhabt:  
  
-   Ignorieren Sie Änderungen, deren Version neuer ist als die neue Synchronisierungsversion.  
  
     Dieser Ansatz hat den Nebeneffekt, dass eine neue oder aktualisierte Zeile übersprungen wird, wenn diese vor der neuen Synchronisierungsversion erstellt oder aktualisiert wurde und danach ebenfalls aktualisiert wird. Bei einer neuen Zeile kann ein Problem mit der referenziellen Integrität auftreten, wenn eine erstellte Zeile in einer anderen Tabelle auf die übersprungene Zeile verweist. Eine aktualisierte Zeile wird übersprungen und erst beim nächsten Mal synchronisiert.  
  
-   Berücksichtigen Sie alle Änderungen, auch die, deren Version neuer ist als die neue Synchronisierungsversion.  
  
     Die Zeilen, deren Version neuer ist als die neue Synchronisierungsversion, werden bei der nächsten Synchronisation erneut abgerufen. Dies muss von der Anwendung entsprechend berücksichtigt werden.  
  
 Zusätzlich zu den beiden oben genannten Optionen können Sie abhängig vom Vorgang einen Ansatz entwerfen, der beide Optionen kombiniert. Sie können beispielsweise eine Anwendung entwickeln, für die es am besten ist, dass Änderungen mit einer neueren Version als die nächste Synchronisierungsversion ignoriert werden, bei denen es sich um Erstellungs- oder Löschvorgänge handelt, Updatevorgänge jedoch nicht ignoriert werden.  
  
> [!NOTE]  
>  Zur Auswahl des richtigen Ansatzes für die Anwendung, wenn Sie die Änderungsnachverfolgung (oder benutzerdefinierte Nachverfolgungsmechanismen) verwenden, sind umfangreiche Analysen erforderlich. Aus diesem Grund ist es viel einfacher, die Momentaufnahmeisolation zu verwenden.  
  
##  <a name="Handles"></a> Handhabung der Änderungen an einer Datenbank durch die Änderungsnachverfolgung  
 Einige Anwendungen, die die Änderungsnachverfolgung verwenden, führen die bidirektionale Synchronisierung mit einem anderen Datenspeicher aus. Das heißt, der andere Datenspeicher wird mit den in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank vorgenommenen Änderungen aktualisiert, und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank wird mit den in dem anderen Datenspeicher vorgenommenen Änderungen aktualisiert.  
  
 Zur Aktualisierung der lokalen Datenbank mit Änderungen von einem anderen Datenspeicher muss die Anwendung die folgenden Vorgänge ausführen:  
  
-   Überprüfung auf Konflikte.  
  
     Zu einem Konflikt kommt es, wenn die gleichen Daten in beiden Datenspeichern gleichzeitig geändert werden. Die Anwendung muss überprüfen können, ob solche Konflikte vorliegen, und genügend Informationen erfassen, um den Konflikt zu beheben.  
  
-   Speichern von Anwendungskontextinformationen.  
  
     Die Anwendung speichert Daten mit Änderungsnachverfolgungsinformationen. Diese Informationen stehen beim Abrufen von Änderungen aus der lokalen Datenbank neben anderen Änderungsnachverfolgungsinformationen zur Verfügung. Ein gängiges Beispiel dieser Kontextinformationen ist die ID des Datenspeichers, in dem die Änderung vorgenommen wurde.  
  
 Zur Ausführung der oben genannten Vorgänge kann eine Synchronisierungsanwendung die folgenden Funktionen verwenden:  
  
-   CHANGETABLE(VERSION…)  
  
     Beim Vornehmen von Änderungen kann eine Anwendung diese Funktion zur Überprüfung auf Konflikte verwenden. Die Funktion ruft die letzten Änderungsnachverfolgungsinformationen für eine angegebene Zeile in einer änderungsnachverfolgten Tabelle ab. Die Änderungsnachverfolgungsinformationen schließen die Version der letzten Änderung der Zeile ein. Die Anwendung kann dann mithilfe dieser Informationen ermitteln, ob die Zeile seit der letzten Synchronisierung der Anwendung geändert wurde.  
  
-   WITH CHANGE_TRACKING_CONTEXT  
  
     Eine Anwendung kann diese Klausel verwenden, um Kontextdaten zu speichern.  
  
### <a name="checking-for-conflicts"></a>Überprüfung auf Konflikte  
 Bei der bidirektionalen Synchronisierung muss die Clientanwendung ermitteln, ob eine Zeile seit dem letzten Abrufen der Änderungen durch die Anwendung aktualisiert wurde.  
  
 Das folgende Beispiel zeigt, wie die Überprüfung auf Konflikte mit der CHANGETABLE(VERSION …)-Funktion effizient und ohne separate Abfrage ausgeführt wird. Im Beispiel wird von `CHANGETABLE(VERSION …)` die `SYS_CHANGE_VERSION` für die von `@product id`bestimmte Zeile angegeben. `CHANGETABLE(CHANGES …)` kann die gleichen Informationen abrufen, aber das wäre weniger effizient. Wenn der Wert von `SYS_CHANGE_VERSION` für die Zeile größer ist als der Wert von `@last_sync_version`, liegt ein Konflikt vor. Wenn ein Konflikt vorliegt, wird die Zeile nicht aktualisiert. Die `ISNULL()` -Prüfung ist erforderlich, da möglicherweise keine Änderungsinformationen für die Zeile verfügbar sind. Es sind keine Änderungsinformationen vorhanden, wenn die Zeile seit der Aktivierung der Änderungsverfolgung oder seit der Bereinigung der Änderungsinformationen nicht aktualisiert wurde.  
  
```tsql  
-- Assumption: @last_sync_version has been validated.  
  
UPDATE  
    SalesLT.Product  
SET  
    ListPrice = @new_listprice  
FROM  
    SalesLT.Product AS P  
WHERE  
    ProductID = @product_id AND  
    @last_sync_version >= ISNULL (  
        SELECT CT.SYS_CHANGE_VERSION  
        FROM CHANGETABLE(VERSION SalesLT.Product,  
                        (ProductID), (P.ProductID)) AS CT),  
        0)  
```  
  
 Mit dem folgenden Code kann die Anzahl der aktualisierten Zeilen überprüft werden, und es können weitere Informationen über den Konflikt ermittelt werden.  
  
```tsql  
-- If the change cannot be made, find out more information.  
IF (@@ROWCOUNT = 0)  
BEGIN  
    -- Obtain the complete change information for the row.  
    SELECT  
        CT.SYS_CHANGE_VERSION, CT.SYS_CHANGE_CREATION_VERSION,  
        CT.SYS_CHANGE_OPERATION, CT.SYS_CHANGE_COLUMNS  
    FROM  
        CHANGETABLE(CHANGES SalesLT.Product, @last_sync_version) AS CT  
    WHERE  
        CT.ProductID = @product_id;  
  
    -- Check CT.SYS_CHANGE_VERSION to verify that it really was a conflict.  
    -- Check CT.SYS_CHANGE_OPERATION to determine the type of conflict:  
    -- update-update or update-delete.  
    -- The row that is specified by @product_id might no longer exist   
    -- if it has been deleted.  
END  
```  
  
### <a name="setting-context-information"></a>Speichern von Kontextinformationen  
 Die WITH CHANGE_TRACKING_CONTEXT-Klausel ermöglicht die Speicherung von Kontextinformationen zusammen mit den Änderungsinformationen. Diese Informationen können dann aus der Spalte SYS_CHANGE_CONTEXT abgerufen werden, die von CHANGETABLE(CHANGES …) zurückgegeben wird.  
  
 Kontextinformationen werden in der Regel verwendet, um die Quelle der Änderungen zu identifizieren. Wenn die Quelle einer Änderung identifiziert werden kann, können diese Informationen von einem Datenspeicher verwendet werden, um das Abrufen von Änderungen bei der nächsten Synchronisierung zu vermeiden.  
  
```tsql  
  -- Try to update the row and check for a conflict.  
  WITH CHANGE_TRACKING_CONTEXT (@source_id)  
  UPDATE  
     SalesLT.Product  
  SET  
      ListPrice = @new_listprice  
  FROM  
      SalesLT.Product AS P  
  WHERE  
     ProductID = @product_id AND  
     @last_sync_version >= ISNULL (  
         (SELECT CT.SYS_CHANGE_VERSION FROM CHANGETABLE(VERSION SalesLT.Product,  
         (ProductID), (P.ProductID)) AS CT),  
         0)  
```  
  
### <a name="ensuring-consistent-and-correct-results"></a>Sicherstellen von konsistenten und richtigen Ergebnissen  
 Eine Anwendung muss bei der Überprüfung des Werts von @last_sync_version den Cleanupprozess berücksichtigen. Grund hierfür ist, dass Daten möglicherweise nach dem Aufruf von CHANGE_TRACKING_MIN_VALID_VERSION(), jedoch vor Durchführung des Updates entfernt werden.  
  
> [!IMPORTANT]  
>  Wir empfehlen die Verwendung der Momentaufnahmeisolation und das Vornehmen der Änderungen in einer Momentaufnahmetransaktion.  
  
```tsql  
-- Prerequisite is to ensure ALLOW_SNAPSHOT_ISOLATION is ON for the database.  
  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
BEGIN TRAN  
    -- Verify that last_sync_version is valid.  
    IF (@last_sync_version <  
CHANGE_TRACKING_MIN_VALID_VERSION(OBJECT_ID(‘SalesLT.Product’)))  
    BEGIN  
       RAISERROR (N’Last_sync_version too old’, 16, -1);  
    END  
    ELSE  
    BEGIN  
        -- Try to update the row.  
        -- Check @@ROWCOUNT and check for a conflict.  
    END  
COMMIT TRAN  
```  
  
> [!NOTE]  
>  Es besteht die Möglichkeit, dass die bei der Momentaufnahmetransaktion aktualisierte Zeile bereits in einer anderen Transaktion aktualisiert wurde, nachdem die Momentaufnahmetransaktion gestartet wurde. In diesem Fall tritt ein Momentaufnahmeisolations-Updatekonflikt auf und bewirkt, dass die Transaktion beendet wird. Wiederholen Sie in diesem Fall das Update. Dies führt dann dazu, dass ein Änderungsnachverfolgungskonflikt erkannt wird und keine Zeilen geändert werden.  
  
##  <a name="DataRestore"></a> Änderungsnachverfolgung und Datenwiederherstellung  
 Bei Anwendungen, für die eine Synchronisierung erforderlich ist, muss der Fall berücksichtigt werden, dass eine für die Änderungsnachverfolgung aktivierte Datenbank eine frühere Version der Daten wiederherstellt. Dies kann auftreten, wenn eine Datenbank aus einer Sicherung wiederhergestellt wird, wenn ein Failover zu einer asynchronen Spiegeldatenbank besteht oder wenn beim Protokollversand ein Fehler auftritt. Das folgende Beispiel veranschaulicht dieses Szenario:  
  
1.  Für Tabelle T1 werden Änderungen nachverfolgt, und die minimal gültige Version für die Tabelle ist 50.  
  
2.  Eine Clientanwendung synchronisiert die Daten bei Version 100 und ruft Informationen über alle Änderungen zwischen Version 50 und 100 ab.  
  
3.  Nach Version 100 werden zusätzliche Änderungen an der Tabelle T1 vorgenommen.  
  
4.  Bei Version 120 tritt ein Fehler auf, und der Datenbankadministrator stellt die Datenbank mit Datenverlust wieder her. Nach der Wiederherstellung enthält die Tabelle Daten bis einschließlich Version 70, und die minimale synchronisierte Version ist weiterhin 50.  
  
     Dies bedeutet, dass der synchronisierte Datenspeicher über Daten verfügt, die nicht mehr im primären Datenspeicher vorhanden sind.  
  
5.  T1 wird häufig aktualisiert. Die aktuelle Version ist daher 130.  
  
6.  Die Clientanwendung synchronisiert erneut und gibt als zuletzt synchronisierte Version 100 aus. Die Überprüfung dieser Version durch den Client ist erfolgreich, da 100 größer als 50 ist.  
  
     Der Client ruft die Änderungen zwischen Version 100 und 130 ab. Zu diesem Zeitpunkt weiß der Client nicht, dass die Änderungen zwischen Version 70 und 100 nicht die gleichen wie zuvor sind. Die Daten auf dem Client und dem Server sind nicht synchronisiert.  
  
 Beachten Sie, dass es keine Probleme bei der Synchronisierung gäbe, wenn die Datenbank auf einen Punkt nach Version 100 wiederhergestellt würde. Der Client und der Server würden während des nächsten Synchronisierungsintervalls Daten ordnungsgemäß synchronisieren.  
  
 Die Änderungsnachverfolgung bietet keine Unterstützung bei der Wiederherstellung nach einem Datenverlust. Es gibt jedoch zwei Optionen zum Erkennen dieser Art von Synchronisierungsproblemen:  
  
-   Speichern Sie eine Datenbankversions-ID auf dem Server, und aktualisieren Sie diesen Wert immer dann, wenn eine Datenbank wiederhergestellt wird oder auf sonstige Weise ein Datenverlust auftritt. Die ID würde in jeder Clientanwendung gespeichert, und jeder Client müsste diese ID beim Synchronisieren der Daten überprüfen. Wenn Datenverlust auftritt, stimmen die IDs nicht überein, und die Clients würden eine Neuinitialisierung durchführen. Ein Nachteil besteht darin, dass der Client eine unnötige Neuinitialisierung durchführt, wenn der Datenverlust nicht über die letzte Synchronisierungsgrenze hinaus erfolgt ist.  
  
-   Zeichnen Sie die Versionsnummer der letzten Synchronisierung auf dem Server auf, wenn ein Client Änderungen abfragt. Wenn ein Problem mit den Daten vorliegt, stimmen die Versionsnummern der letzten Synchronisierung nicht überein. Dies weist darauf hin, dass eine Neuinitialisierung erforderlich ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Nachverfolgen von Datenänderungen &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [Informationen zur Änderungsnachverfolgung &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)   
 [Verwalten der Änderungsnachverfolgung &#40;SQL Server&#41;](../../relational-databases/track-changes/manage-change-tracking-sql-server.md)   
 [Aktivieren und Deaktivieren der Änderungsnachverfolgung &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)   
 [CHANGETABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [CHANGE_TRACKING_MIN_VALID_VERSION &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)   
 [CHANGE_TRACKING_CURRENT_VERSION &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-current-version-transact-sql.md)   
 [WITH CHANGE_TRACKING_CONTEXT &#40;Transact-SQL&#41;](../../relational-databases/system-functions/with-change-tracking-context-transact-sql.md)  
  
  
