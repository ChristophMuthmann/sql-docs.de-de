---
title: Lernprogramme für SQL Server-Python | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c99e5605dad537fddef20fbd091a61cc4e711471
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
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

   In dieser Lektion wird veranschaulicht, wie Sie Code von einem Remoteserver Python-Terminal ausführen können mithilfe von SQL Server-computekontext. Sie sollten mit Python-Tools und Umgebungen etwas vertraut sein. Beispielcode wird vorausgesetzt, ein Modell mithilfe erstellt **RxLinMod**, aus dem neuen **Revoscalepy** Bibliothek. 

+ [In der Datenbank Python-Analyse für SQL-Entwickler](sqldev-in-database-python-for-sql-developers.md)

    Diese exemplarische End-to-End-Vorgehensweise veranschaulicht, wie eine vollständige Python-Lösung mithilfe von T-SQL-gespeicherten Prozeduren erstellen. Alle Python-Code ist enthalten.


## <a name="python-samples"></a>Python-Beispiele

Markieren Sie diese Beispiele und Demos, die von der SQL Server-Entwicklungsteam bereitgestellten Methoden, mit denen Sie eingebettete Analytics in echten Anwendungen verwenden können.

+ [Erstellen eines Vorhersagemodells über Python- und SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

  Erfahren Sie, wie eine Ski Vermietung Business Machine learning-zukünftige Vermietung Vorhersagen verwenden kann dadurch die Business-Plan und die Mitarbeiter, zukünftige Bedarf zu decken.

  > [!TIP]
  > Enthält nun die systemeigene Bewertung aus Python-Modellen!

+ [Ausführen von Kunden über Python- und SQL Server-clustering](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    Erfahren Sie, wie die Kmeans-Algorithmus verwenden, um nicht überwachten Gruppieren von Kunden ausführen.

## <a name="bkmk_Prerequisites"></a>Voraussetzungen

Um diese Lernprogramme verwenden zu können, benötigen Sie SQL Server-2017 und müssen Sie explizit zu installieren und aktivieren Sie das Feature "" Machine Learning-Services (Datenbankintern). 

SQL Server-2017 R und Python-Sprachen unterstützt, aber keines von beiden installiert oder standardmäßig aktiviert. Ausführen von Python erfordert, dass das Extensibility Framework aktiviert werden, und Sie Python als Sprache für die Installation auswählen. 

### <a name="post-installation-configuration-tips"></a>Tipps für die Konfiguration nach der installation

Nach SQL Server-Setup ausführen, müssen Sie möglicherweise führen Sie einige zusätzliche Schritte erforderlich, um sicherzustellen, dass Python und SQL Server kommunizieren:

+ Die externen Skript Ausführung-Funktion aktivieren, indem ausgeführt `sp_configure 'external scripts enabled', 1`.
+ Starten Sie den Server neu. 
+ Öffnen der **Services** Systemsteuerung, um zu überprüfen, ob Launchpad gestartet wurde. 
+ Stellen Sie sicher, dass der Dienst, der die externe Runtime Ruft die erforderlichen Berechtigungen verfügt. Weitere Informationen finden Sie unter [implizite Authentifizierung aktivieren](../r/add-sqlrusergroup-to-database.md).
+ Öffnen Sie einen Port in der Firewall für SQL Server, und aktivieren Sie erforderlichen Netzwerkprotokolle zu.
+ Sicherstellen Sie, dass die SQL-Anmeldung oder die Windows-Benutzerkonto erforderlichen Berechtigungen zum Verbinden mit dem Server, der zum Lesen von Daten und das Beispiel erforderlichen Datenbankobjekte zu erstellen.

Finden Sie in diesem Artikel finden Sie einige häufig auftretende Probleme: [Problembehandlung Machine Learning-Dienste](../machine-learning-troubleshooting-faq.md)

### <a name="resource-management"></a>Ressourcenverwaltung

Sie können R und Python auf demselben Computer installieren, aber ausführt, kann erhebliche Ressourcen erforderlich. Wenn "nicht genügend Arbeitsspeicher" Fehler auftreten oder Machine Learning-Aufträge ausgeführt, dass der Prinzipal die Verwendung des Servers dafür vorgesehen ist, können Sie die Größe des Arbeitsspeichers reduzieren, die mit dem Datenbankmodul zugeordnet ist. Weitere Informationen finden Sie unter [verwalten und Überwachen von Python in SQL Server](../python/managing-and-monitoring-python-solutions.md).

## <a name="see-also"></a>Siehe auch

[R-Tutorials für SQL Server](sql-server-r-tutorials.md)
