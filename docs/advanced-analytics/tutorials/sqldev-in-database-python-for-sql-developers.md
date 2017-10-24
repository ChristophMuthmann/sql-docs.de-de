---
title: "In der Datenbank Python Analytics für SQL-Entwickler | Microsoft Docs"
ms.custom: 
ms.date: 10/13/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2f28400200105e8e63f787cbcda58c183ba00da5
ms.openlocfilehash: 725d69f4c0799cf5911cb8764aa7d0f3b6cbc48d
ms.contentlocale: de-de
ms.lasthandoff: 10/18/2017

---
# <a name="in-database-python-analytics-for-sql-developers"></a>In der Datenbank Python-Analyse für SQL-Entwickler

Das Ziel dieser exemplarischen Vorgehensweise ist bereitzustellen, SQL-Programmierer praktische Beispiele zum Erstellen eines Machine learning-Projektmappe mithilfe von Python, die in SQL Server ausgeführt wird. In dieser exemplarischen Vorgehensweise erfahren Sie, wie gespeicherte Prozeduren Python-Code hinzu, und führen Sie gespeicherte Prozeduren zum Erstellen und Vorhersagen von Modellen.

> [!NOTE]
> Bevorzugen Sie R? Finden Sie unter [dieses Lernprogramms](sqldev-in-database-r-for-sql-developers.md), dem bietet eine ähnlichen Lösung jedoch werden mit R und in SQL Server 2016 oder 2017 von SQL Server ausgeführt werden können.

## <a name="overview"></a>Übersicht

Der Vorgang der Erstellung einer Machine Learning-Lösung ist ein komplexes, die mehrere Tools und die Koordination von Experten in mehreren Phasen umfassen können:

+ Abrufen und Bereinigen von Daten
+ Untersuchen der Daten und Erstellen von Merkmalen, die für die Modellierung hilfreich.
+ Trainieren und Optimieren des Modells
+ Bereitstellung bis hin zur Produktion

**Der Schwerpunkt dieser exemplarischen Vorgehensweise ist erstellen und Bereitstellen einer Lösung, die mithilfe von SQL Server.**

Die Daten stammen aus bekannten NYC Taxi DataSet. Um dieser exemplarischen Vorgehensweise schnell und einfach zu gestalten, werden die Daten als Stichprobe genommen. Erstellen Sie ein binäres klassifizierungsmodell, das vorhersagt, ob einem bestimmten Vorgang wahrscheinlich einen Tipp oder nicht abrufen wird basierend auf Spalten, z. B. den Zeitpunkt der Tag, Abstand und Abholung Speicherort.

Alle Aufgaben können ausgeführt werden, mit [!INCLUDE[tsql](../../includes/tsql-md.md)] gespeicherten Prozeduren in der vertrauten Umgebung von[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]

- [Schritt 1: Herunterladen der Beispieldaten](sqldev-py1-download-the-sample-data.md)

    Laden Sie das Beispieldataset und alle Skriptdateien an einem lokalen Computer herunter.

- [Schritt 2: Importieren von Daten nach SQL Server mithilfe von PowerShell](sqldev-py2-import-data-to-sql-server-using-powershell.md)

    Führen Sie ein Powershellskript, das einer Datenbank und eine Tabelle, für die angegebene Instanz erstellt und die Beispieldaten in die Tabelle geladen.

- [Schritt 3: Durchsuchen und Visualisieren von Daten mithilfe von Python](sqldev-py3-explore-and-visualize-the-data.md)

    Führen Sie grundlegende Daten durchsuchen und visualisieren, durch Aufrufen von Python aus [!INCLUDE[tsql](../../includes/tsql-md.md)] gespeicherte Prozeduren.

- [Schritt 4: Erstellen von Data-Funktionen, die mithilfe von Python in T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    Erstellen Sie neue Features mit benutzerdefinierten SQL-Funktionen.
  
- [Schritt 5: Trainieren Sie, und speichern Sie ein Python-Modell mithilfe des T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    Erstellen Sie und speichern Sie die Machine Learning-Modells mithilfe von Python in gespeicherten Prozeduren.
  
    Diese exemplarische Vorgehensweise veranschaulicht, wie Sie eine binäre klassifikationsaufgabe ausführen; die Daten können Sie Modelle für Regression oder mehrklassiges klassifizierungsmodell erstellen.

  
-  [Schritt 6: Operationalisieren Sie die Python-Modell](sqldev-py6-operationalize-the-model.md)

    Nachdem das Modell in der Datenbank gespeichert wurde, rufen Sie das Modell für die Vorhersage verwendet [!INCLUDE[tsql](../../includes/tsql-md.md)].

## <a name="requirements"></a>Anforderungen

### <a name="prerequisites"></a>Erforderliche Komponenten

+ Installieren Sie eine Instanz von SQL Server-2017 mit Machine Learning-Dienste und Python aktiviert. Weitere Informationen finden Sie unter [Einrichten von SQL Server-Machine Learning-Services mit Python](../python/setup-python-machine-learning-services.md).
+ Die Anmeldung, die Sie für diese exemplarische Vorgehensweise verwenden, muss über Berechtigungen zum Erstellen von Datenbanken und anderer Objekte, zum Hochladen von Daten, Auswählen von Daten und Ausführen von gespeicherten Prozeduren verfügen.

### <a name="experience-level"></a>Erfahrung

Sie sollten mit grundlegenden Datenbankvorgängen, wie Datenbanken und Tabellen erstellen, Importieren von Daten in Tabellen und Erstellen von SQL-Abfragen vertraut sein.

Ein erfahrener SQL-Programmierer sollte in der Lage sein, diese exemplarische Vorgehensweise mit [!INCLUDE[tsql](../../includes/tsql-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder durch Ausführen der bereitgestellten PowerShell-Skripts abzuschließen.

Python: Grundkenntnisse ist hilfreich, jedoch nicht erforderlich. Alle Python-Code wird bereitgestellt.

Einige Kenntnisse von PowerShell ist hilfreich.

### <a name="tools"></a>Tools

Für dieses Lernprogramm möchten wir davon ausgegangen, dass Sie die Bereitstellungsphase erreicht haben. Sie haben Daten bereinigen gegeben wurde, führen Sie die T-SQL-Code für das Feature engineering und Python-Code arbeiten. Aus diesem Grund können Sie dieses Lernprogramm mit der SQL Server Management Studio oder ein anderes Tool, das SQL-Anweisungen unterstützt abschließen.

+ [Übersicht über SQL Server-tools](https://docs.microsoft.com/sql/tools/overview-sql-tools) 

Wenn Sie zum Entwickeln und Testen von Python-Code werden soll, oder eine Python-Projektmappe debuggen, wird empfohlen, mithilfe einer dedizierten Umgebung:

+ **Visual Studio-2017** unterstützt beide R und [Python](https://blogs.msdn.microsoft.com/visualstudio/2017/05/12/a-lap-around-python-in-visual-studio-2017/). Es wird empfohlen die [Data Science-arbeitsauslastung](https://blogs.msdn.microsoft.com/visualstudio/2016/11/18/data-science-workloads-in-visual-studio-2017-rc/), das auch R und f# unterstützt.
+ Wenn Sie eine frühere Version von Visual Studio ist [Python-Erweiterungen für Visual Studio](https://docs.microsoft.com/visualstudio/python/python-in-visual-studio) erleichtert es, mehrere Python-Umgebungen verwalten.
+ PyCharm ist eine beliebte IDE zwischen Python-Entwickler.

    > [!NOTE]
    > Im Allgemeinen zu vermeiden, schreiben oder testen neuen Python-Code in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Wenn der Code, den Sie in einer gespeicherten Prozedur einbetten Probleme aufweist, sind die Informationen, die von der gespeicherten Prozedur zurückgegeben wird in der Regel unzureichend ist, um die Ursache des Fehlers zu verstehen.

Verwenden Sie die folgenden Ressourcen helfen Ihnen beim Planen und führen Sie eine erfolgreiche maschinelle-Projekt:

+ [Team Data Science-Prozess](https://docs.microsoft.com/azure/machine-learning/team-data-science-process/overview)

### <a name="estimated-time-required"></a>Geschätzte Zeit, die erforderlich sind

|Schritt| Zeit (Stunden)|
|----|----|
|Herunterladen der Beispieldaten| 0:15|
|Importieren von Daten in SQL Server mit PowerShell|0:15|
|Durchsuchen und Visualisieren von Daten|0:20|
|Erstellen von Data-Funktionen, die mithilfe des T-SQL|0:30|
|Trainieren Sie und speichern Sie ein Modell mithilfe des T-SQL|0:15|
|Das Modell operationalisieren|0:40|

## <a name="get-started"></a>Erste Schritte

  [Schritt 1: Herunterladen der Beispieldaten](sqldev-py1-download-the-sample-data.md)

