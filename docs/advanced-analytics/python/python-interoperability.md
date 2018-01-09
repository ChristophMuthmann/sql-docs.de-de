---
title: "Python-Interoperabilität mit SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 11/03/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 71b578fb47a7bd7881f2681206a0f69f5c37facb
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="python-interoperability-with-sql-server"></a>Python-Interoperabilität mit SQL Server

In diesem Thema wird beschrieben, die Python-Komponenten, die installiert werden, wenn Sie das Feature aktivieren **Machine Learning-Services (Datenbankintern)** , und wählen Sie als Sprache Python.

## <a name="python-components"></a>Python-Komponenten

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]Die Python-ausführbaren Dateien werden nicht geändert werden. Die Python-Laufzeit unabhängig von der SQL-Tools installiert ist und ausgeführt wird, außerhalb von der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Prozess.

Die Verteilung, die mit einem bestimmten anfallen [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Instanz finden Sie in den Ordner mit der Instanz verknüpft ist.

Beispielsweise, wenn Sie Machine Learning-Dienste mit der Python-Option auf der Standardinstanz installiert haben, suchen Sie unter:

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

Installation von SQL Server 2017 Machine Learning Services fügt die Anaconda-Verteilung von Python hinzu. Insbesondere werden die Installationsprogramme Anaconda 3 verwendet, basierend auf den Branch Anaconda 4.3. Die erwartete Python-Ebene für SQL Server-2017 ist Python 3.5.

## <a name="new-python-packages-in-this-release"></a>Neuer Python-Pakete in dieser Version

Eine Liste der Pakete, die die Anaconda-Verteilung unterstützt, finden Sie unter der Continuum Analytics-Website: [Anaconda Paketliste](https://docs.continuum.io/anaconda/pkg-docs)

Machine Learning Services in SQL Server-2017 enthält auch die neue **Revoscalepy** -Bibliothek für Python.

Diese Bibliothek bietet Funktionen, die von der **"revoscaler"** -Paket für Microsoft R. Das heißt, es unterstützt die Erstellung von remote rechenkontexte als auch eine verschiedene skalierbare Machine Learning-Modellen, z. B. **RxLinMod**. Weitere Informationen zu "revoscaler" finden Sie unter [verteilt und die parallele Berechnung mit ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing).

Die [Microsoftml für Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) Paket wird als Teil des SQL Server-Machine Learning installiert, wenn Sie Python für Ihre Installation hinzufügen. Dieses Paket enthält viele Machine learning-Algorithmen, die wurden optimiert für Geschwindigkeit und Genauigkeit als auch Inline-Transformationen für das Arbeiten mit Text und Bildern. Weitere Informationen finden Sie unter [mithilfe des MicrosoftML-Pakets mit SQL Server](https://docs.microsoft.com/sql/advanced-analytics/using-the-microsoftml-package).

Microsoftml und Revoscalepy sind eng verbunden; in Microsoftml verwendete Datenquellen werden als Revoscalepy Objekte definiert. Kontext-Einschränkungen in Revoscalepy Übertragung in Microsoftml zu berechnen. Nämlich die gesamte Funktionalität ist für lokale Vorgänge verfügbar, aber Wechsel zu einem remote-computekontext RxInSqlServer erfordert.

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

[Python-Bibliotheken und -Datentypen](python-libraries-and-data-types.md)
