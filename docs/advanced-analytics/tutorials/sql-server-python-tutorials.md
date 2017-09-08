---
title: "Lernprogramme für SQL Server-Python | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/29/2017
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
caps.latest.revision: 1
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b891cda72d5a69aafe461918674218fd3279c423
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="sql-server-python-tutorials"></a>SQL Server-Python-Lernprogramme

Dieser Artikel enthält eine Liste der Lernprogramme und Beispiele, in denen die Verwendung von Python mit SQL Server-2017 veranschaulicht. Durch diese Beispiele und Demos erfahren Sie:

+ Zum Ausführen von Python von T-SQL
+ Was sind remote und lokalen rechenkontexten und wie die Python-Code mithilfe von SQL Server-Computer ausgeführt werden kann
+ Gewusst wie: Umschließen von Python-Code in einer gespeicherten Prozedur
+ Optimieren der Python-Code für eine SQL-produktionsumgebung
+ Reale Szenarien für das Einbetten von Machine Learning in Anwendungen

Informationen zu Anforderungen und Setup finden Sie unter [Voraussetzungen](#bkmk_Prerequisites).

## <a name="bkmk_pythontutorials"></a>Python-Lernprogramme

+ [Ausführen von Python in T-SQL](run-python-using-t-sql.md)

   Grundlegendes zum Aufrufen von Python in T-SQL mit den Erweiterungsmechanismus Vorreiterrolle beim in SQL Server 2016.

+ [Erstellen Sie ein Machine learning-Modell in Revoscalepy mit Python](use-python-revoscalepy-to-create-model.md)

   Erstellen Sie ein Modell mithilfe **RxLinMod**, aus dem neuen **Revoscalepy** Bibliothek. Starten Sie den Code von einem remote-Python-Terminal, sondern die Modellierung wird stattfinden in der SQL Server-computekontext.

+ [Erstellen eines Vorhersagemodells mit Python (GitHub)](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/python/getting-started/rental-prediction)

  Erstellen Sie ein Machine Learning-Modell zur Vorhersage von Anforderung für ein Unternehmen der Ski-Vermietung und operationalisieren Sie dieses Modell für die täglichen Bedarf Vorhersage mithilfe von gespeicherten Prozeduren. Alle Code und Daten bereitgestellt.

+ [In der Datenbank Python-Analyse für SQL-Entwickler](sqldev-in-database-python-for-sql-developers.md)

  NEU! Erstellen Sie eine vollständige Python-Lösung mithilfe von T-SQL-gespeicherten Prozeduren. Alle Python-Code ist enthalten.

+ [Bereitstellen und nutzen ein Python-Modell](..\python\publish-consume-python-code.md)

  Erfahren Sie, wie Sie ein Python-Modell anhand der neuesten Version von Microsoft Machine Learning-Server bereitstellen.

## <a name="python-samples"></a>Python-Beispiele

Markieren Sie diese Beispiele und Demos, die von der SQL Server-Entwicklungsteam bereitgestellten Methoden, mit denen Sie eingebettete Analytics in echten Anwendungen verwenden können.

+ [Erstellen eines Vorhersagemodells über Python- und SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

  Erfahren Sie, wie eine Ski Vermietung Business Machine learning-zukünftige Vermietung Vorhersagen verwenden kann dadurch die Business-Plan und die Mitarbeiter, zukünftige Bedarf zu decken.

+ [NEU! Ausführen von Kunden über Python- und SQL Server-clustering](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    Erfahren Sie, wie die Kmeans-Algorithmus verwenden, um nicht überwachten Gruppieren von Kunden ausführen.

## <a name="bkmk_Prerequisites"></a>Voraussetzungen

Um diese Lernprogramme verwenden zu können, müssen Sie SQL Server 2017 Machine Learning Services (Datenbankintern) installiert haben. SQL Server-2017 unterstützt R oder Python. Allerdings müssen Sie installieren das Extensibility Framework, das Machine Learning unterstützt, und wählen Python als Sprache für die Installation. Sie können R und Python auf demselben Computer installieren.

> [!NOTE]
>
> Unterstützung für Python ist ein neues Feature in SQL Server-2017 und CTP-Version 2.0 oder höher erfordert. Obwohl die Funktion im Vorabversion und wird nicht unterstützt für produktionsumgebungen vorliegt, möchten wir probieren es aus, und senden Feedback einladen.

**SQL Server 2017**

Nach dem Ausführen von SQL Server-Setup, vergessen Sie nicht folgenden wichtigen Schritte aus:

+ Aktivieren Sie die externen Skript Ausführung-Funktion, indem Sie ausgeführt wird`sp_configure 'external scripts enabled', 1`
+ Neustarten des Servers
+ Stellen Sie sicher, dass der Dienst, der die externe Runtime ruft erforderlichen Berechtigungen verfügt.
+ Sicherstellen Sie, dass der SQL-Anmeldung oder die Windows-Benutzerkonto hat erforderlichen Berechtigungen zum Verbinden mit dem Server, der zum Lesen von Daten und erstellen das Beispiel erforderlichen Datenbankobjekte

Wenn Probleme auftreten, finden Sie in diesem Artikel finden Sie einige häufig auftretende Probleme: [Problembehandlung Machine Learning-Dienste](../machine-learning-troubleshooting-faq.md)

## <a name="see-also"></a>Siehe auch

[R-Lernprogramme für SQL Server](sql-server-r-tutorials.md)

