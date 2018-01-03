---
title: RevoScaleR-Funktionen zum Arbeiten mit SQL Server-Daten | Microsoft Docs
ms.custom: 
ms.date: 08/20/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 5f3c9864-9c75-4688-947d-0940045b2671
caps.latest.revision: "9"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 473ef6ddde2e1c1b143806e48a7c53a2542c43ec
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/20/2017
---
# <a name="revoscaler-functions-for-working-with-sql-server-data"></a>RevoScaleR-Funktionen zum Arbeiten mit SQL Server-Daten

Dieses Thema enthält eine Übersicht über die wichtigsten Funktionen, die im "revoscaler" für das Arbeiten mit SQL Server-Daten bereitgestellt.

Eine vollständige Liste der ScaleR-Funktionen und deren Verwendung, finden Sie unter der [Microsoft R Server](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) Verweis.

## <a name="create-sql-server-data-sources"></a>Erstellen von SQL Server-Datenquellen

Mit den folgenden Funktionen können Sie eine [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Datenquelle definieren. Ein Datenquellenobjekt ist ein Container, der eine Verbindungszeichenfolge zusammen mit dem gewünschten Datensatz als Tabelle, Ansicht oder Abfrage definiert angibt. Aufrufe von gespeicherten Prozeduren werden nicht unterstützt.

+ [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) -definieren Sie eine [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] -Datenquellenobjekt.

+ [RxOdbcData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxodbcdata) -Datenobjekten für andere ODBC-Datenbanken zu erstellen. 

## <a name="perform-ddl-statements"></a>Ausführen von DDL-Anweisungen

DDL-Anweisungen können von R, ausgeführt werden, wenn Sie die erforderlichen Berechtigungen für die Instanz und Datenbank aufweisen. Die folgenden Funktionen verwenden die ODBC-Aufrufe zum Ausführen von DDL-Anweisungen oder das Schema der Datenbank abrufen.

+ `rxSqlServerTableExists`und [RxSqlServerDropTable](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdroptable) -Löschen einer [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] -Tabelle ab, oder Überprüfen Sie das Vorhandensein einer Datenbanktabelle oder-Objekt

+ [RxExecuteSQLDDL](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexecutesqlddl) -führen Sie einen Befehl (Data Definition Language, Datendefinitionssprache) definiert oder Datenbankobjekte bearbeitet. Diese Funktion kann keine Daten zurückgeben, und dient nur zum Abrufen oder Ändern der Objektschema und die Metadaten.

## <a name="define-or-manage-compute-contexts"></a>Definieren Sie oder verwalten Sie rechenkontexte

Mit den folgenden Funktionen können Sie einen neuen Rechenkontext definieren, den Rechenkontext wechseln oder den aktuellen Rechenkontext identifizieren.

+ [RxComputeContext](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxcomputecontext): Erstellt einen Rechenkontext.

+ [rxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver): Generiert einen SQL Server-Rechenkontext, mit dem **ScaleR**-Funktionen in SQL Server R Services ausgeführt werden können. Dieser Rechenkontext wird derzeit nur für SQL Server-Instanzen unter Windows unterstützt.

+ `rxGetComputeContext`und [RxSetComputeContext](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetcomputecontext) - abrufen oder Festlegen der aktiven computekontext.

## <a name="move-data-and-transform-data"></a>Verschieben von Daten und Transformieren von Daten

Nachdem Sie ein Datenquellenobjekt erstellt haben, können Sie jedoch stattdessen das Laden von Daten hinein, Transformieren von Daten oder Schreiben neue Daten in das angegebene Ziel. Abhängig von der Größe der Daten in der Quelle können Sie die Batchgröße auch als Teil der Datenquelle definieren und Daten in Blöcken verschieben.

+ [RxOpen Methoden](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxopen-methods) – überprüfen Sie, ob eine Datenquelle verfügbar ist, öffnen oder schließen eine Datenquelle, Lesen von Daten aus einer Quelle, Schreiben von Daten an das Ziel, und schließen eine Datenquelle

+ [RxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) -Verschieben von Daten aus einer Datenquelle in Speichern von Dateien oder in einem Datenrahmen.

+ [RxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) -Transformieren von Daten beim Verschieben zwischen Datenquellen.

Die folgenden Funktionen können verwendet werden, um einen lokalen Datenspeicher im XDF-Format zu erstellen. Diese Datei kann nützlich sein, wenn Sie mit mehr Daten arbeiten als in einem Batch aus der Datenbank übertragen werden können oder als in den Speicher passen.

Z. B. Wenn Sie regelmäßig große Mengen von Daten aus einer Datenbank auf einer lokalen Arbeitsstation verschieben, anstatt Abfrage der Datenbank wiederholt für jeden Vorgang R können Sie die XDF-Datei als eine Art des Caches auf die Daten lokal speichern, und klicken Sie dann in Ihrem R-Arbeitsbereich arbeiten.

+ [RxXdfData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxxdfdata) -erstellt ein XDF-Datenobjekt

+ [RxReadXdf](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxreadxdf) -liest Daten aus einer XDF-Datei in einem Datenrahmen

Weitere Informationen zum Arbeiten mit diesen Funktionen, einschließlich der Verwendung von Daten als Datenquellen [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], finden Sie unter [so wird's gemacht-Handbücher für die Datenanalyse in Microsoft R](https://docs.microsoft.com/r-server/r/how-to-introduction).
