---
title: "In der Datenbank Python Analytics für SQL-Entwickler | Microsoft Docs"
ms.custom: 
ms.date: 05/25/2017
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
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 984ff8097b1f28cf11e28cc464c88dc3b9580a12
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="in-database-python-analytics-for-sql-developers"></a>In der Datenbank Python Analytics für SQL-Entwickler

Das Ziel dieser exemplarischen Vorgehensweise werden SQL-Programmierer praktische Beispiele zum Erstellen eines Machine learning-Lösung in SQL Server zur Verfügung stellen. In dieser exemplarischen Vorgehensweise erfahren Sie, wie Sie Python in einer Anwendung zu integrieren, indem Sie gespeicherte Prozeduren Python-Code hinzugefügt.

> [!NOTE]
> Bevorzugen Sie R? Finden Sie unter [dieses Lernprogramms](sqldev-in-database-r-for-sql-developers.md), wodurch bietet eine ähnliche Lösung jedoch werden mit R und kann in SQL Server 2016 oder SQL Server-2017 "EB" ausführen.

## <a name="overview"></a>Übersicht

Das Erstellen einer Ende-zu-Ende-Lösung besteht in der Regel aus Abrufen und Bereinigen von Daten, Durchsuchen von Daten und Verarbeiten von Funktionen, Modelltraining und Optimieren und schließlich Bereitstellung des Modells in der Produktion. Entwickeln und Testen von den eigentlichen Code erfolgt am besten das Verwenden einer dedizierten Entwicklungsumgebung, z. B. diese Python-Tools:

+ PyCharm, eine beliebte-IDE
+ Spyder, Lieferumfang [Visual Studio 2017](https://blogs.msdn.microsoft.com/visualstudio/2017/05/12/a-lap-around-python-in-visual-studio-2017/) bei der Installation der [Data Science-Arbeitslast](https://blogs.msdn.microsoft.com/visualstudio/2016/11/18/data-science-workloads-in-visual-studio-2017-rc/)
+ [Python-Erweiterungen für Visual Studio](https://docs.microsoft.com/visualstudio/python/python-in-visual-studio).

Nachdem Sie erstellt und die Lösung in der IDE getestet haben, können Sie die Python-Code zum Bereitstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit [!INCLUDE[tsql](../../includes/tsql-md.md)] gespeicherten Prozeduren in der vertrauten Umgebung von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

In dieser exemplarischen Vorgehensweise wird angenommen, Sie alle Python-Code, die für die Lösung erforderlichen gegeben wurde haben, und Sie darauf konzentrieren müssen, erstellen und Bereitstellen der Lösung mithilfe von SQL Server.

- [Schritt 1: Herunterladen der Beispieldaten](sqldev-py1-download-the-sample-data.md)

  Laden Sie das Beispieldataset und alle Skriptdateien an einem lokalen Computer herunter.

- [Schritt 2: Importieren von Daten in SQL Server mithilfe von PowerShell](sqldev-py2-import-data-to-sql-server-using-powershell.md)

  Führen Sie ein Powershellskript, das einer Datenbank und eine Tabelle, für die angegebene Instanz erstellt und die Beispieldaten in die Tabelle geladen.

- [Schritt 3: Untersuchen und Visualisieren von Daten](sqldev-py3-explore-and-visualize-the-data.md)

  Führen Sie grundlegende Daten durchsuchen und visualisieren, durch Aufrufen von Python aus [!INCLUDE[tsql](../../includes/tsql-md.md)] gespeicherte Prozeduren.

- [Schritt 4: Erstellen von Datenfunktionen mit T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

  Erstellen Sie neue Features mit benutzerdefinierten SQL-Funktionen.
  
- [Schritt 5: Trainieren und Speichern eines Modells mit T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

   Erstellen Sie und speichern Sie die Machine Learning-Modells mithilfe von Python in gespeicherten Prozeduren.
  
-  [Schritt 6: Operationalisieren des Modells](sqldev-py6-operationalize-the-model.md)

  Nachdem das Modell in der Datenbank gespeichert wurde, rufen Sie das Modell für die Vorhersage verwendet [!INCLUDE[tsql](../../includes/tsql-md.md)].

> [!NOTE]
> Es wird empfohlen, dass Sie nicht verwenden [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] schreiben oder Python-Code zu testen. Wenn der Code, den Sie in einer gespeicherten Prozedur einbetten Probleme aufweist, sind die Informationen, die von der gespeicherten Prozedur zurückgegeben wird in der Regel unzureichend ist, um die Ursache des Fehlers zu verstehen.


### <a name="scenario"></a>Szenario

In dieser exemplarischen Vorgehensweise wird das bekannte NYC Taxi-Dataset verwendet. Um dieser exemplarischen Vorgehensweise schnell und einfach zu gestalten, werden die Daten als Stichprobe genommen. Anhand dieser Daten erstellen Sie ein binäres klassifizierungsmodell, das vorhersagt, ob einem bestimmten Vorgang wahrscheinlich einen Tipp oder nicht abrufen wird basierend auf Spalten, z. B. den Zeitpunkt der Tag, Abstand und Abholung Speicherort.

### <a name="requirements"></a>Anforderungen

Diese exemplarische Vorgehensweise ist für Benutzer gedacht, die bereits mit grundlegenden Datenbank-Vorgängen vertraut sind, z.B. Erstellen von Datenbanken und Tabellen, Importieren von Daten in Tabellen und Erstellen von SQL-Abfragen.

Alle Python-Code wird bereitgestellt. Ein erfahrener SQL-Programmierer sollte in der Lage sein, diese exemplarische Vorgehensweise mit [!INCLUDE[tsql](../../includes/tsql-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder durch Ausführen der bereitgestellten PowerShell-Skripts abzuschließen.

Bevor Sie mit die exemplarischen Vorgehensweise beginnen, müssen Sie diese Vorbereitungen ausführen:

- Installieren eine Instanz von SQL Server-2017 mit Machine Learning-Diensten und Python aktiviert (CTP-Version 2.0 oder höher erforderlich).
- Die Anmeldung, die Sie für diese exemplarische Vorgehensweise verwenden, muss über Berechtigungen zum Erstellen von Datenbanken und anderer Objekte, zum Hochladen von Daten, Auswählen von Daten und Ausführen von gespeicherten Prozeduren verfügen.

## <a name="next-step"></a>Nächster Schritt

  [Schritt 1: Herunterladen der Beispieldaten](sqldev-py1-download-the-sample-data.md)

## <a name="see-also"></a>Siehe auch

[Machine Learning-Dienste mit Python](../python/sql-server-python-services.md)



