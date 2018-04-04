---
title: Erweiterte Ereignisse für die Überwachung der PREDICT-Anweisungen | Microsoft Docs
titleSuffix: SQL Server
ms.custom: ''
ms.date: 03/01/2018
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: d517da44f989620003fef35d2e4721eead15d5d5
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="extended-events-for-monitoring-predict-statements"></a>Erweiterte Ereignisse für die Überwachung der PREDICT-Anweisungen

Dieser Artikel beschreibt die erweiterten Ereignissen bereitgestellten in SQL Server, Überwachung und Analyse verwenden können, bei denen Aufträge [PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) Echtzeit Bewertung in SQL Server ausführen.

Echtzeit-Bewertung generiert Bewertungen aus ein Machine learning-Modell, das in SQL Server gespeichert wurde. Die PREDICT-Funktion erfordert keine externe Laufzeit z. B. R oder Python, nur ein Modell, das mit einem bestimmten binären Format erstellt wurde. Weitere Informationen finden Sie unter [Echtzeit Bewertung](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring).

## <a name="prerequisites"></a>Erforderliche Komponenten

Allgemeine Informationen zu für erweiterte Ereignisse (XEvents bezeichnet), und wie Sie Ereignisse in einer Sitzung zu überwachen finden Sie in diesen Artikeln:

+ [Erweiterte Konzepte für Ereignisse und Architektur](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [Richten Sie Ereignis-Erfassung in SSMS](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [Verwalten von ereignissitzungen im Objekt-Explorer](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)

## <a name="table-of-extended-events"></a>Tabelle erweiterter Ereignisse

Die folgenden erweiterten Ereignissen stehen in allen Versionen von SQL Server, unterstützen die [T-SQL-VORHERSAGEN](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) -Anweisung, einschließlich SQL Server on Linux und Azure SQL-Datenbank. 

VORHERSAGEN von T-SQL-Anweisung wurde in SQL Server-2017 eingeführt. 

|name |object_type|description| 
|----|----|----|
|predict_function_completed |Ereignis  |"Vordefiniert" Ausführungszeit "arbeitsaufgliederung"|
|predict_model_cache_hit |Ereignis|Tritt auf, wenn ein Modell aus der Modellcache der PREDICT-Funktion abgerufen werden. Verwenden Sie dieses Ereignis zusammen mit weiteren Predict_model_cache_ *-Ereignissen, um durch die PREDICT-Funktion Modellcache verursachte Probleme zu beheben.|
|predict_model_cache_insert |Ereignis  |   Tritt auf, wenn ein Modell einfügen, in der PREDICT-Funktion Modellcache. Verwenden Sie dieses Ereignis zusammen mit weiteren Predict_model_cache_ *-Ereignissen, um durch die PREDICT-Funktion Modellcache verursachte Probleme zu beheben.    |
|predict_model_cache_miss   |Ereignis|Tritt auf, wenn ein Modell in der PREDICT-Funktion Modellcache nicht gefunden wird. Ein häufige Auftreten dieses Ereignisses möglicherweise, dass SQL Server mehr Arbeitsspeicher benötigt wird. Verwenden Sie dieses Ereignis zusammen mit weiteren Predict_model_cache_ *-Ereignissen, um durch die PREDICT-Funktion Modellcache verursachte Probleme zu beheben.|
|predict_model_cache_remove |Ereignis| Tritt auf, wenn ein Modell aus dem Modellcache für PREDICT-Funktion entfernt wird. Verwenden Sie dieses Ereignis zusammen mit weiteren Predict_model_cache_ *-Ereignissen, um durch die PREDICT-Funktion Modellcache verursachte Probleme zu beheben.|

## <a name="query-for-related-events"></a>Abfrage nach verwandten Ereignissen

Um eine Liste aller Spalten zurückgegeben, die für diese Ereignisse anzuzeigen, führen Sie die folgende Abfrage in SQL Server Management Studio aus:

```sql
SELECT * FROM sys.dm_xe_object_columns WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>Beispiele

So erfassen Sie Informationen über die Leistung einer bewerteten Sitzung VORHERSAGEN:

1. Erstellen Sie eine neue ereignissitzung mit Management Studio oder einem anderen unterstützt erweiterte [Tool](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools).
2. Fügen Sie die Ereignisse `predict_function_completed` und `predict_model_cache_hit` für die Sitzung.
3. Starten Sie die Sitzung für erweiterte Ereignisse.
4. Führen Sie die Abfrage verwendet, die VORHERSAGEN.

Überprüfen Sie in den Ergebnissen dieser Spalten aus:

+ Der Wert für `predict_function_completed` wird ermittelt, wie lange die Abfrage an, das Modell geladen und Bewertung aufgewendet wurde.
+ Der boolesche Wert für `predict_model_cache_hit` gibt an, ob die Abfrage ein zwischengespeichertes Modell oder nicht verwendet. 

### <a name="native-scoring-model-cache"></a>Systemeigene bewerteten Modellcache

Zusätzlich zu den Ereignissen, die speziell für VORHERSAGEN können Sie die folgenden Abfragen verwenden, um weitere Informationen zu den zwischengespeichertes Modell und die Verwendung des Prozedurcaches zu erhalten:

Anzeigen der systemeigenen bewerteten Modellcache an:

```sql
SELECT *
FROM sys.dm_os_memory_clerks
WHERE type = 'CACHESTORE_NATIVESCORING';
```

Zeigen Sie die Objekte im Modellcache:

```sql
SELECT *
FROM sys.dm_os_memory_objects
WHERE TYPE = 'MEMOBJ_NATIVESCORING';
```

