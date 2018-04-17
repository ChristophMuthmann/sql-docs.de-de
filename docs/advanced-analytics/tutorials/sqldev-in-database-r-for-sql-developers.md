---
title: In der Datenbank R Analytics für SQL-Entwickler (Lernprogramm) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 21bc5d6af2ad34a23bb56a589f7bcbacb6034ff3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="in-database-r-analytics-for-sql-developers-tutorial"></a>In-Database-R-Analyse für SQL-Entwickler (Lernprogramm)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Das Ziel dieses Lernprogramms ist SQL-Programmierer praktische Beispiele zum Erstellen eines Machine learning-Lösung in SQL Server bereitstellen. In diesem Lernprogramm erfahren Sie, wie Sie R in einer Anwendung oder eine BI-Lösung zu integrieren, indem Sie das Einschließen von R-Code in gespeicherten Prozeduren.

> [!NOTE]
> 
> Die gleiche Projektmappe ist in Python verfügbar. SQL Server-2017 ist erforderlich. Finden Sie unter [In der Datenbank Analytics für Python-Entwickler](../tutorials/sqldev-in-database-python-for-sql-developers.md)

## <a name="overview"></a>Übersicht

Das Erstellen einer Ende-zu-Ende-Lösung besteht in der Regel aus Abrufen und Bereinigen von Daten, Durchsuchen von Daten und Verarbeiten von Funktionen, Modelltraining und Optimieren und schließlich Bereitstellung des Modells in der Produktion. Entwickeln und Testen von den tatsächlichen Code, wird am besten mit einer dedizierten Umgebung ausgeführt. Für R, das kann bedeuten RStudio oder [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)].

Nachdem die Lösung erstellt wurde, können Sie sie jedoch problemlos für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit [!INCLUDE[tsql](../../includes/tsql-md.md)] -gespeicherten Prozeduren in der vertrauten Umgebung von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]bereitstellen.

In diesem Lernprogramm wird davon ausgegangen, dass Sie alle R-Code, die erforderlich sind, für die Projektmappe, und den Fokus auf das Erstellen und Bereitstellen der Lösung mithilfe von SQL Server angegeben wurden.

- [Lektion 1: Herunterladen der Beispieldaten](../tutorials/sqldev-download-the-sample-data.md)

    Laden Sie das Beispieldataset und die Beispiel-SQL-Skriptdateien auf einen lokalen Computer herunter.

- [Lektion 2: Importieren von Daten in SQL Server mit PowerShell](../r/sqldev-import-data-to-sql-server-using-powershell.md)

    Führen Sie ein PowerShell-Skript aus, das eine Datenbank und eine Tabelle auf der [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Instanz erstellt und die Beispieldaten in die Tabelle lädt.

- [Lektion 3: Durchsuchen und Visualisieren von Daten](../tutorials/sqldev-explore-and-visualize-the-data.md)

    Führen Sie grundlegendes Durchsuchen und Visualisieren von Daten durch, indem Sie R-Pakete und Funktionen von [!INCLUDE[tsql](../../includes/tsql-md.md)] -gespeicherten Prozeduren aufrufen.

- [Lektion 4: Erstellen von Data-Funktionen, die mithilfe des T-SQL](../tutorials/sqldev-create-data-features-using-t-sql.md)

    Erstellen Sie neue Features mit benutzerdefinierten SQL-Funktionen.
  
-   [Lektion 5: Trainieren Sie, und speichern Sie ein R-Modell mithilfe des T-SQL](../r/sqldev-train-and-save-a-model-using-t-sql.md)

    Erstellen Sie ein Machine Learning-Modells mithilfe von R in gespeicherten Prozeduren. Speichern Sie das Modell in einer SQL Server-Tabelle.
  
-   [Lektion 6: Operationalisieren des Modells](../tutorials/sqldev-operationalize-the-model.md)

    Nachdem das Modell in der Datenbank gespeichert wurde, rufen Sie das Modell für die Vorhersage von [!INCLUDE[tsql](../../includes/tsql-md.md)] mit gespeicherten Prozeduren auf.

### <a name="scenario"></a>Szenario

Dieses Lernprogramm verwendet ein bekannten öffentlichen Dataset basierend auf Reisen in New York City Taxi. Um den Beispielcode schneller ausgeführt werden soll, erstellt es einen repräsentativen Querschnitt der 1 % der Daten. Sie müssen diese Daten verwenden, ein binäres klassifizierungsmodell erstellen, das vorhersagt, ob es sich bei einem bestimmten Vorgang wahrscheinlich einen Tipp oder nicht abrufen wird basierend auf Spalten, z. B. den Zeitpunkt der Tag, Abstand und Abholung Speicherort.

### <a name="requirements"></a>Anforderungen

Dieses Lernprogramm ist für Benutzer vorgesehen, die bereits mit grundlegenden Datenbankvorgängen, wie Datenbanken und Tabellen erstellen, Importieren von Daten in Tabellen und Erstellen von SQL-Abfragen vertraut sind. Der gesamte R-Code wird bereitgestellt, damit keine R-Entwicklungsumgebung erforderlich ist. Einen erfahrenen SQL-Programmierer sollten in der Lage, mithilfe dieses Beispiel zu vervollständigen [!INCLUDE[tsql](../../includes/tsql-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], und durch das Ausführen der bereitgestellten PowerShell-Skripts.

Bevor Sie das Tutorial starten, müssen Sie jedoch diese Vorbereitungen ausführen:

- Verbinden Sie mit einer Instanz von SQL Server 2016 mit R-Services oder SQL Server-2017 mit Machine Learning-Diensten und R aktiviert.
- Der Anmeldename, mit denen Sie für dieses Lernprogramm benötigen Berechtigungen zum Erstellen von Datenbanken und anderen Objekten, zum Hochladen von Daten, wählen Sie die Daten, und führen Sie gespeicherte Prozeduren.

> [!NOTE]
> Es wird empfohlen, Sie führen **nicht** verwenden [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] schreiben oder R-Code zu testen. Wenn der Code, den Sie in einer gespeicherten Prozedur einbetten Probleme aufweist, sind die Informationen, die von der gespeicherten Prozedur zurückgegeben wird in der Regel unzureichend ist, um die Ursache des Fehlers zu verstehen.
> 
> Für das Debuggen, wird empfohlen, ein Tool wie z. B. [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)], oder RStudio. Die in diesem Tutorial bereitgestellten R-Skripts wurden bereits mit herkömmlichen R-Tools entwickelt und debuggt.

## <a name="next-lesson"></a>Nächste Lektion

[Lektion 1: Herunterladen der Beispieldaten](../tutorials/sqldev-download-the-sample-data.md)
