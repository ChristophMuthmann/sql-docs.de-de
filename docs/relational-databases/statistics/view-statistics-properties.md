---
title: Anzeigen der Statistikeigenschaften | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: statistics
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-statistics
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.statistics.details.f1
helpviewer_keywords:
- viewing statistics properties
- statistics [SQL Server], viewing properties
ms.assetid: 0eaa2101-006e-4015-9979-3468b50e0aaa
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 350224343e6c64c53d12205bce7133a8cd4da289
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="view-statistics-properties"></a>Anzeigen von Statistikeigenschaften
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Sie können die aktuelle Abfrageoptimierungsstatistik für eine Tabelle oder eine indizierte Sicht in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]anzeigen. Statistikobjekte enthalten einen Header mit Metadaten über die Statistik, ein Histogramm mit der Verteilung der Werte in der ersten Schlüsselspalte des Statistikobjekts sowie einen Dichtevektor zum Messen der Korrelation zwischen Spalten. Weitere Informationen zu Histogrammen und Dichtevektoren finden Sie unter [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md).  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Security](#Security)  
  
-   **So zeigen Sie Statistikeigenschaften an mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Zum Anzeigen des Statistikobjekts muss der Benutzer Besitzer der Tabelle sein, oder der Benutzer muss ein Mitglied der festen Serverrolle **sysadmin** , der festen Datenbankrolle **db_owner** oder der festen Datenbankrolle **db_ddladmin** sein.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-view-statistics-properties"></a>So zeigen Sie Statistikeigenschaften an  
  
1.  Klicken Sie im **Objekt-Explorer**auf das Pluszeichen, um die Datenbank zu erweitern, in der Sie eine neue Statistik erstellen möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Tabellen** zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um die Tabelle zu erweitern, in der Sie die Eigenschaften der Statistik anzeigen möchten.  
  
4.  Klicken Sie auf das Pluszeichen, um den Ordner **Statistik** zu erweitern.  
  
5.  Klicken Sie mit der rechten Maustaste auf das Statistikobjekt, dessen Eigenschaften Sie anzeigen möchten, und wählen Sie **Eigenschaften**aus.  
  
6.  Wählen Sie im Dialogfeld **Statistikeigenschaften –** *statistics_name* im Bereich **Seite auswählen** die Option **Details**aus.  
  
     Die folgenden Eigenschaften werden im Dialogfeld **Statistikeigenschaften –**  **statistics_name** *statistics_name* angezeigt.  
  
     **Tabellenname**  
     Zeigt den Namen der Tabelle an, die von den Statistiken beschrieben wird.  
  
     **Statistikname**  
     Zeigt den Namen des Datenbankobjekts an, in dem die Statistiken gespeichert sind.  
  
     **Statistik für INDEXstatistics_name**  
     Dieses Textfeld zeigt die Eigenschaften an, die vom Statistikobjekt zurückgegeben werden. Diese Eigenschaften sind in drei Abschnitte unterteilt: STAT_HEADER, DENSITY_VECTOR und HISTOGRAM.  
  
     Die folgenden Informationen beschreiben die Spalten, die im Resultset für STAT_HEADER zurückgegeben werden.  
  
     **Name**  
     Name des Statistikobjekts.  
  
     **Updated**  
     Datum und Uhrzeit des letzten Updates der Statistik.  
  
     **Zeilen**  
     Gesamtanzahl der Zeilen in der Tabelle oder indizierten Sicht zum Zeitpunkt des letzten Updates der Statistik. Wenn die Statistik gefiltert wird oder einem gefilterten Index entspricht, kann die Anzahl der Zeilen geringer als die Anzahl der Zeilen in der Tabelle sein.  
  
     **Rows Sampled**  
     Gesamtzahl der Zeilen, die für die statistischen Berechnungen in die Stichprobe aufgenommen wurden. Wenn Rows Sampled < Rows, sind das angezeigte Histogramm und die Dichteergebnisse Schätzungen auf Grundlage der als Stichprobe entnommenen Zeilen.  
  
     **Schritte**  
     Anzahl der Schritte im Histogramm. Jeder Schritt umfasst einen Bereich von Spaltenwerten gefolgt von einem oberen Spaltengrenzwert. Die Histogrammschritte werden in der Statistik in der ersten Schlüsselspalte definiert. Die maximale Anzahl von Schritten ist 200.  
  
     **Density**  
     Berechnet als 1 / *verschiedene Werte* für alle Werte in der ersten Schlüsselspalte des Statistikobjekts mit Ausnahme der Begrenzungswerte des Histogramms. Dieser Dichtewert wird vom Abfrageoptimierer nicht verwendet und für die Abwärtskompatibilität mit Versionen vor SQL Server 2008 angezeigt.  
  
     **Average Key Length**  
     Durchschnittliche Anzahl von Bytes pro Wert für alle Schlüsselspalten im Statistikobjekt.  
  
     **String Index**  
     "Ja" gibt an, dass das Statistikobjekt Statistiken über Zusammenfassungen von Zeichenfolgen enthält, um die Kardinalitätsschätzungen für Abfrageprädikate, die den LIKE-Operator verwenden, zu verbessern, z. B. `WHERE ProductName LIKE '%Bike'`. Zusammenfassungen von Zeichenfolgen werden getrennt vom Histogramm gespeichert und in der ersten Schlüsselspalte des Statistikobjekts erstellt, wenn es vom Typ **char**, **varchar**, **nchar**, **nvarchar**, **varchar(max)**, **nvarchar(max)**, **text**, or **ntext**ist.  
  
     **Filterausdruck**  
     Prädikat für die Teilmenge von Tabellenzeilen, die im Statistikobjekt enthalten sind. NULL = Nicht gefilterte Statistik.  
  
     **Unfiltered Rows**  
     Gesamtzahl von Zeilen in der Tabelle vor dem Anwenden des Filterausdrucks. Wenn Filter Expression NULL ist, ist Unfiltered Rows gleich Rows.  
  
     Die folgenden Informationen beschreiben die Spalten, die im Resultset für DENSITY_VECTOR zurückgegeben werden.  
  
     **All Density**  
     Die Dichte ist 1 / *verschiedene Werte*. Die Ergebnisse zeigen die Dichte für jedes Präfix von Spalten im Statistikobjekt mit einer Zeile pro Dichte an. Bei einem unterschiedlichen Wert handelt es sich um eine unterschiedliche Liste der Spaltenwerte pro Zeile und pro Spaltenpräfix. Wenn das Statistikobjekt beispielsweise Schlüsselspalten (A, B, C) enthält, geben die Ergebnisse die Dichte der unterschiedlichen Wertelisten jedes dieser Spaltenpräfixe an: (A), (A, B) und (A, B, C). Mit dem Präfix (A, B, C) ist jede dieser Listen eine Liste unterschiedlicher Werte: (3, 5, 6), (4, 4, 6), (4, 5, 6), (4, 5, 7). Mit dem Präfix (A, B) weisen dieselben Spaltenwerte diese Listen unterschiedlicher Werte auf: (3, 5), (4, 4) und (4, 5).  
  
     **Average Length**  
     Durchschnittliche Länge in Bytes zum Speichern einer Liste der Spaltenwerte für das Spaltenpräfix. Wenn die Werte in der Liste (3, 5, 6) beispielsweise jeweils 4 Bytes erfordern, beträgt die Länge 12 Bytes.  
  
     **Spalten**  
     Namen der Spalten im Präfix, für die All Density und Average Length angezeigt werden.  
  
     Die folgenden Informationen beschreiben die Spalten, die im Resultset für HISTOGRAM zurückgegeben werden.  
  
     **RANGE_HI_KEY**  
     Oberer Spaltengrenzwert für einen Histogrammschritt. Der Spaltenwert wird auch als Schlüsselwert bezeichnet.  
  
     **RANGE_ROWS**  
     Geschätzte Anzahl von Zeilen, deren Spaltenwerte innerhalb eines Histogrammschritts liegen, ohne den oberen Grenzwert.  
  
     **EQ_ROWS**  
     Geschätzte Anzahl von Zeilen, deren Spaltenwerte der Obergrenze des Histogrammschritts entsprechen.  
  
     **DISTINCT_RANGE_ROWS**  
     Geschätzte Anzahl von Zeilen mit einem unterschiedlichen Spaltenwert innerhalb eines Histogrammschritts ohne den oberen Grenzwert.  
  
     **AVG_RANGE_ROWS**  
     Durchschnittliche Anzahl von Zeilen mit doppelten Spaltenwerten in einem Histogrammschritt ohne den oberen Grenzwert (RANGE_ROWS / DISTINCT_RANGE_ROWS für DISTINCT_RANGE_ROWS > 0).  
  
7.  Klicken Sie auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-view-statistics-properties"></a>So zeigen Sie Statistikeigenschaften an  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- The following example displays all statistics information for the AK_Address_rowguid index of the Person.Address table.   
    DBCC SHOW_STATISTICS ("Person.Address", AK_Address_rowguid);   
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md).  
  
#### <a name="to-find-all-of-the-statistics-on-a-table-or-view"></a>So suchen Sie nach allen Statistiken einer Tabelle oder Sicht  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    /*Gets the following information: name and ID of the statistics, whether the statistics were created automatically or by the user, whether the statistics were created with the NORECOMPUTE option, and whether the statistics have a filter and, if so, what that filter is.  
    */  
    SELECT name AS statistics_name  
        ,stats_id  
        ,auto_created  
        ,user_created  
        ,no_recompute  
        ,has_filter  
        ,filter_definition  
    -- using the sys.stats catalog view  
    FROM sys.stats  
    -- for the Sales.SpecialOffer table  
    WHERE object_id = OBJECT_ID('Sales.SpecialOffer');  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md).  
  
  
