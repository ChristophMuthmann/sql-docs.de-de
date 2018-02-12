---
title: "Lernprogramme für SQL Server-Python | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 09/19/2017
vapplies_to:
- SQL Server 2017
dev_langs:
- Python
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 42a9339f5983eeef28250db7a384f37efd4dad9d
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2018
---
# <a name="sql-server-python-tutorials"></a>SQL Server-Python-Lernprogramme
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

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

+ [In der Datenbank Python-Analyse für SQL-Entwickler](sqldev-in-database-python-for-sql-developers.md)

  NEU! Erstellen Sie eine vollständige Python-Lösung mithilfe von T-SQL-gespeicherten Prozeduren. Alle Python-Code ist enthalten.

+ [Bereitstellen und nutzen ein Python-Modell](..\python\publish-consume-python-code.md)

  Erfahren Sie, wie Sie ein Python-Modell anhand der neuesten Version von Microsoft Machine Learning-Server bereitstellen.

## <a name="python-samples"></a>Python-Beispiele

Markieren Sie diese Beispiele und Demos, die von der SQL Server-Entwicklungsteam bereitgestellten Methoden, mit denen Sie eingebettete Analytics in echten Anwendungen verwenden können.

+ [Erstellen eines Vorhersagemodells über Python- und SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

  Erfahren Sie, wie eine Ski Vermietung Business Machine learning-zukünftige Vermietung Vorhersagen verwenden kann dadurch die Business-Plan und die Mitarbeiter, zukünftige Bedarf zu decken.

  > [!TIP]
  > Enthält nun die systemeigene Bewertung aus Python-Modellen!

+ [Ausführen von Kunden über Python- und SQL Server-clustering](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    Erfahren Sie, wie die Kmeans-Algorithmus verwenden, um nicht überwachten Gruppieren von Kunden ausführen.

## <a name="bkmk_Prerequisites"></a>Voraussetzungen

Um diese Lernprogramme verwenden zu können, müssen Sie SQL Server 2017 Machine Learning Services (Datenbankintern) installiert haben. SQL Server-2017 unterstützt R oder Python. Allerdings müssen Sie installieren das Extensibility Framework, das Machine Learning unterstützt, und wählen Python als Sprache für die Installation. Sie können R und Python auf demselben Computer installieren.

> [!NOTE]
>
> Unterstützung für Python ist ein neues Feature in SQL Server-2017 und CTP-Version 2.0 oder höher erfordert. Obwohl die Funktion im Vorabversion und wird nicht unterstützt für produktionsumgebungen vorliegt, möchten wir probieren es aus, und senden Feedback einladen.

**SQL Server 2017**

Nach dem Ausführen von SQL Server-Setup, vergessen Sie nicht folgenden wichtigen Schritte aus:

+ Die externen Skript Ausführung-Funktion aktivieren, indem ausgeführt `sp_configure 'external scripts enabled', 1`.
+ Starten Sie den Server neu.
+ Stellen Sie sicher, dass der Dienst, der die externe Runtime Ruft die erforderlichen Berechtigungen verfügt.
+ Sicherstellen Sie, dass die SQL-Anmeldung oder die Windows-Benutzerkonto erforderlichen Berechtigungen zum Verbinden mit dem Server, der zum Lesen von Daten und das Beispiel erforderlichen Datenbankobjekte zu erstellen.

Wenn Probleme auftreten, finden Sie in diesem Artikel finden Sie einige häufig auftretende Probleme: [Problembehandlung Machine Learning-Dienste](../machine-learning-troubleshooting-faq.md)

## <a name="see-also"></a>Siehe auch

[R-Tutorials für SQL Server](sql-server-r-tutorials.md)
