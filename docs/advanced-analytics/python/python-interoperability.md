---
title: "Python-Interoperabilität | Microsoft Docs"
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 32762183ff5273998848978238788cc830319b91
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="python-interoperability"></a>Python-Interoperabilität

In diesem Thema wird beschrieben, die Python-Komponenten, die installiert werden, wenn Sie das Feature aktivieren **Machine Learning-Services (Datenbankintern)** , und wählen Sie als Sprache Python.

> [!NOTE]
> Unterstützung für Python ist eine Vorabversion-Funktion und befindet sich noch in Bearbeitung.

## <a name="python-components"></a>Python-Komponenten

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]Die Python-ausführbaren Dateien werden nicht geändert werden. Die Python-Laufzeit unabhängig von der SQL-Tools installiert ist und ausgeführt wird, außerhalb von der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Prozess.

Die Verteilung, die mit einem bestimmten anfallen [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Instanz finden Sie in den Ordner mit der Instanz verknüpft ist.

Beispielsweise, wenn Sie Machine Learning-Dienste mit der Python-Option auf der Standardinstanz installiert haben, suchen Sie unter:

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER`

Installation von SQL Server 2017 Machine Learning Services fügt die Anaconda-Verteilung von Python hinzu. Insbesondere werden die Installationsprogramme Anaconda 3 verwendet, basierend auf den Branch Anaconda 4.3. Die erwartete Python-Ebene für SQL Server-2017 ist Python 3.5.

## <a name="new-in-this-release"></a>In dieser Version

Eine Liste der Pakete, die die Anaconda-Verteilung unterstützt, finden Sie unter der Continuum Analytics-Website: [Anaconda Paketliste](https://docs.continuum.io/anaconda/pkg-docs)

Machine Learning Services in SQL Server-2017 enthält auch die neue **Revoscalepy** -Bibliothek für Python.

Diese Bibliothek bietet Funktionen, die von der **"revoscaler"** -Paket für Microsoft R. Das heißt, es unterstützt die Erstellung von remote rechenkontexte als auch eine verschiedene skalierbare Machine Learning-Modellen, z. B. **RxLinMod**. Weitere Informationen zu "revoscaler" finden Sie unter [verteilt und die parallele Berechnung mit ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing).

Da Unterstützung für Python ein vorab veröffentlichtes Feature ist und noch in Entwicklung, die **Revoscalepy** -Bibliothek enthält derzeit nur eine Teilmenge der Funktionen "revoscaler". 

Zukünftige Ergänzungen zählen die [Cognitive Microsoft-Toolkit](https://www.microsoft.com/research/product/cognitive-toolkit/). Diese Bibliothek ist früher als CNTK bezeichnet, unterstützt eine Vielzahl von Modellen neuronaler Netzwerke, einschließlich convolutional Netzwerke (CNN), wiederkehrende Netzwerke (RNN) und lange kurze Begriff Arbeitsspeicher Netzwerke (LSTM).

## <a name="using-python-in-sql-server"></a>Verwenden von Python in SQLServer

Sie importieren die **Revoscalepy** Modul in Ihrem Python-Code und Aufrufen von Funktionen aus dem Modul wie andere Python-Funktionen.

Die Eingabedaten für Python muss tabellarische. Alle Python-Ergebnisse zurückgegeben werden müssen, in Form einer **Pandas** Datenrahmen.

Sie können Ihrem Python-Code in T-SQL, ausführen, indem Sie das Skript in einer gespeicherten Prozedur einbetten.

Oder führen Sie den Code aus einer lokalen Python-IDE und haben Sie das Skript auf dem SQL Server-Computer ausgeführt wird, definieren Sie einen remote-computekontext.

Sie können mit lokalen Daten arbeiten, Abrufen von Daten aus SQL Server oder andere ODBC-Datenquellen oder XDF-Datei-Format zum Austauschen von Daten mit anderen Quellen oder R-Lösungen verwenden.

**Weitere Informationen**

+ Unterstützte Funktionen: [neuerungen Revoscalepy](what-is-revoscalepy.md) 
+ Python-Datentypen unterstützt: [Python-Bibliotheken und Datentypen](python-libraries-and-data-types.md)
+ Unterstützte Datenquellen: ODBC-Datenbanken, SQL Server und XDF-Dateien
+ Unterstützt rechenkontexte: lokale oder SQL Server

### <a name="licensing"></a>Lizenzierung

Im Rahmen der Installation von Machine Learning-Dienste mit Python müssen Sie den Bedingungen der GNU Public License zustimmen.

## <a name="see-also"></a>Siehe auch

[Python-Bibliotheken und Datentypen](python-libraries-and-data-types.md)

