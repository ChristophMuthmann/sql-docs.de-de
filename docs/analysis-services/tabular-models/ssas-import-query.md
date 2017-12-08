---
title: Importieren von Daten mithilfe einer systemeigenen Abfrage (Analysis Services) | Microsoft Docs
ms.custom: 
ms.date: 10/26/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1b4d0672b30747729d324386e1f761a377e15ad2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="import-data-by-using-a-native-query"></a>Importieren von Daten mithilfe einer systemeigenen Abfrage

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

Für tabellarische Modelle 1400 bietet die neue Daten abrufen-Benutzeroberfläche in Visual Studio Analysis Services-Projekte enorme Flexibilität beim wie kombinieren können Ihre Daten während des Imports. Dieser Artikel beschreibt das Erstellen einer Verbindungs mit einer Datenquelle und anschließend eine systemeigene SQL-Abfrage zum Importieren von Daten angeben.

Um die in diesem Artikel beschriebenen Aufgaben ausführen zu können, stellen Sie sicher, dass Sie die neueste Version von SSDT verwenden. Wenn Sie Visual Studio 2017 verwenden, stellen Sie sicher, dass Sie heruntergeladen und installiert die September 2017 haben oder höher Microsoft Analysis Services-Projekten VSIX.

[Herunterladen und installieren Sie SSDT](../../ssdt/download-sql-server-data-tools-ssdt.md)

[Herunterladen von Microsoft Analysis Services-Projekten VSIX](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)

## <a name="create-a-datasource-connection"></a>Erstellen Sie eine Datasource-Verbindung
Wenn Sie eine Verbindung mit Ihrer Datenquelle noch nicht haben, müssen Sie eines erstellen.

1. In Visual Studio > **tabellarische Modell-Explorer**, mit der rechten Maustaste **Datenquellen**, und klicken Sie dann auf **neue Datenquelle**.
2. In **Daten abrufen**, wählen Sie die Datasource-Datentyp, und klicken Sie dann auf **verbinden**. Führen Sie zusätzliche Schritte erforderlich, um eine Verbindung mit Ihrer Datenquelle herstellen.


## <a name="enter-a-query-as-a-named-expression"></a>Geben Sie eine Abfrage als einen benannten Ausdruck
1. In **tabellarische Modell-Explorer**, mit der rechten Maustaste **Ausdrücke** > **Ausdrücke bearbeiten**.
2. In **-abfrageeditor**, klicken Sie auf **Abfrage** > **neue Abfrage** > **leere Abfrage**
3. Geben Sie in der Bearbeitungsleiste
    ```
    = Value.NativeQuery(#"DATA SOURCE NAME", "SELECT * FROM …")
    ```
4. So erstellen Sie eine Tabelle in **Abfragen**mit der rechten Maustaste auf die Abfrage, und wählen Sie dann **neue Tabelle erstellen**. Die neue Tabelle müssen den gleichen Namen wie die Abfrage.


## <a name="example"></a>Beispiel
Diese systemeigene Abfrage erstellt eine Tabelle im Modell, das alle Spalten aus der Dimension.Employee-Tabelle in der Datenquelle enthält.

```
= Value.NativeQuery(#"SQL/myserver;WideWorldImportersDW", "SELECT * FROM Dimension.Employee")
```
![Abfrage-Editor](media/ssas-import-query-example.png)


Nach dem Importieren, wird eine Tabelle mit dem Namen Mitarbeiter im Modell erstellt.   

![Abfrage-Editor](media/ssas-import-query-example-table.png)


## <a name="see-also"></a>Siehe auch  
 [Value.NativeQuery](https://msdn.microsoft.com/library/mt736917.aspx)   
 [Identitätswechsel](../../analysis-services/tabular-models/impersonation-ssas-tabular.md)   

  
