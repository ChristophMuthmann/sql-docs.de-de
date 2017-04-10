---
title: "ScaleR Funktionen zum Arbeiten mit SQL Server-Daten | Microsoft Docs"
ms.custom: ""
ms.date: "01/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 5f3c9864-9c75-4688-947d-0940045b2671
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 7
---
# ScaleR Funktionen zum Arbeiten mit SQL Server-Daten
Dieses Thema enthält eine Übersicht über die wichtigsten ScaleR-Funktionen für die Verwendung mit SQL Server, zusammen mit Kommentaren auf ihre Syntax.

Eine vollständige Liste der ScaleR Funktionen und deren Verwendung, finden Sie unter der [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/index#) Reference in der MSDN Library. 

## Funktionen zum Arbeiten mit SQL Server-Datenquellen
Die folgenden Funktionen können Sie definieren eine [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] -Datenquelle. Ein Objekt ist ein Container, der eine Verbindungszeichenfolge zusammen mit dem Satz von Daten, die angibt entweder als eine Tabelle, Sicht oder Abfrage definiert werden soll, an. Aufrufe von gespeicherten Prozeduren werden nicht unterstützt.  

Zusätzlich zum Definieren einer Datenquelle, können Sie DDL-Anweisungen von R, ausführen, wenn Sie die erforderlichen Berechtigungen für die Instanz und-Datenbank verfügen. 
+ [RxSqlServerData](https://msdn.microsoft.com/microsoft-r/scaler/RxSqlServerData) -definieren Sie eine [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] -Datenquellenobjekt
+ [RxSqlServerDropTable](https://msdn.microsoft.com/microsoft-r/scaler/rxSqlServerDropTable) -Drop eine [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Tabelle
+ [RxSqlServerTableExists](https://msdn.microsoft.com/microsoft-r/scaler/rxSqlServerTableExists) -Überprüfen Sie das Vorhandensein einer Datenbanktabelle oder -Objekt
+ [RxExecuteSQLDDL](https://msdn.microsoft.com/microsoft-r/scaler/rxExecuteSQLDDL) – Führen Sie einen Befehl definieren, bearbeiten oder SQL-Daten zu steuern, aber keine Daten zurück  

## Funktionen zum Definieren oder Verwalten von einem Compute-Kontext
Die folgenden Funktionen können Sie einen neuen Compute-Kontext definieren, Wechseln des Kontexts von Compute oder Compute-Kontext zu identifizieren.
+ [RxComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/RxComputeContext) -Erstellen eines Compute-Kontexts. 
+ [RxInSqlServer](https://msdn.microsoft.com/microsoft-r/scaler/rxInSqlServer) – generieren Sie einen SQL Server-Compute-Kontext, mit dem **ScaleR** Funktionen in SQL Server-R-Dienste ausgeführt.
+ [RxGetComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/rxGetComputeContext) -Compute-Kontext abzurufen. 
+ [RxSetComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/rxSetComputeContext) -Geben Sie die zu verwendende Kontext berechnen. 

## Funktionen für die Verwendung einer Datenquelle
Nachdem Sie ein Datenquellenobjekt erstellt haben, können Sie öffnen, um Daten abzurufen oder neue Daten zu schreiben. Abhängig von der Größe der Daten in der Quelle können Sie auch die Batchgröße als Teil der Datenquelle definieren und Verschieben von Daten in Segmenten. 
+ [RxIsOpen](https://msdn.microsoft.com/microsoft-r/scaler/rxIsOpen) -Überprüfen Sie, ob eine Datenquelle verfügbar ist.
+ [RxOpen](https://msdn.microsoft.com/microsoft-r/scaler/rxOpen) -eine Datenquelle zum Lesen öffnen
+ [RxReadNext](https://msdn.microsoft.com/microsoft-r/scaler/rxReadNext) -Lesen von Daten aus einer Datenquelle
+ [RxWriteNext](https://msdn.microsoft.com/microsoft-r/scaler/rxWriteNext) -Schreiben von Daten in das Ziel
+ [RxClose](https://msdn.microsoft.com/microsoft-r/scaler/rxclose) -Schließen Sie eine Datenquelle

Weitere Informationen zum Arbeiten mit diesen Funktionen ScaleR die kann für Datenquellen außer [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], finden Sie unter [ Microsoft R Server – Erste Schritte](http://msdn.microsoft.com/microsoft-r/rserver/rserver-getting-started).

## Funktionen, die Arbeit mit XDF-Dateien
Die folgenden Funktionen können verwendet werden, um einen lokalen Datencache im XDF Format zu erstellen. Diese Datei kann nützlich sein, beim Arbeiten mit mehr Daten als in einem Batch aus der Datenbank übertragen werden kann, oder mehr Daten als in den Speicher passen.

Wenn Sie regelmäßig große Mengen von Daten aus einer Datenbank auf einer lokalen Arbeitsstation verschieben, anstatt die Abfrage der Datenbank wiederholt für jeden Vorgang R können Sie die Datei XDF die Daten lokal speichern und dann funktioniert des R-Arbeitsbereichs mithilfe der XDF-Datei als Cache für die.

+ `rxImport` -Verschieben von Daten aus einer ODBC-Datenquelle auf die Datei XDF
+ `RxXdfData` – Erstellen Sie ein Datenobjekt XDF
+ `RxDataStep` – Lesen Sie Daten von XDF Int Datenrahmen
+ `rxXdfToDataFrame` – Lesen von Daten aus XDF in einem Datenrahmen
+ `rxReadXdf` -Liest Daten aus XDF in einem Datenrahmen

Ein Beispiel dafür, wie XDF-Dateien verwendet werden, finden Sie in diesem Lernprogramm:  [Data Science Deep Dive - mithilfe der ScaleR-Funktionen](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)

Weitere Informationen zu diesen ScaleR-Funktionen, die zum Übertragen von Daten aus vielen verschiedenen Quellen verwendet werden können, finden Sie unter[ Microsoft R Server – Erste Schritte](http://msdn.microsoft.com/microsoft-r/rserver/rserver-getting-started).

## Siehe auch
[Vergleich von Base R und ScaleR-Funktionen](https://msdn.microsoft.com/microsoft-r/scaler/compare-base-r-scaler-functions)
