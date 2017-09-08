---
title: Anzeigen und Durchsuchen von Daten mit SQL (Exemplarische Vorgehensweise) | Microsoft Docs
ms.custom: 
ms.date: 07/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: d3835d6d-e68b-486d-81a0-81b717cc6134
caps.latest.revision: 33
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3f531d6b3bd3732c6c4d8c257561a3b3c5c865f2
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="view-and-explore-the-data-using-sql-walkthrough"></a>Anzeigen und Durchsuchen von Daten mit SQL (Exemplarische Vorgehensweise)

Durchsuchen von Daten ist ein wichtiger Bestandteil beim Modellieren von Daten und umfasst das Überprüfen der Zusammenfassung von Datenobjekten in Analysen sowie die Visualisierung von Daten. In dieser Lektion untersuchen Sie die Datenobjekte und generieren Darstellungen, die Verwendung beider [!INCLUDE[tsql](../../includes/tsql-md.md)] und R-Funktionen, die in enthaltenen [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].

Darstellungen zum Visualisieren der Daten generiert werden neue Funktionen mit installierten Pakete mit [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].

> [!TIP]
> Sind Sie bereits ein R-Meister?
>   
> Da Sie nun alle Daten heruntergeladen und die Umgebung vorbereitet haben, können Sie das vollständige R-Skript in RStudio oder in einer anderen Umgebung ausführen und die Funktionalität selbst ausprobieren. Öffnen Sie einfach die Datei RSQL_Walkthrough.R, markieren Sie einzelne Zeilen und führen Sie aus – oder das gesamte Skript als eine Demo.
>   
> Weitere Informationen zu RevoScaleR-Funktionen und Tipps zum Arbeiten mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Daten in R erhalten Sie in diesem Tutorial. Es verwendet genau das gleiche Skript.

## <a name="verify-downloaded-data-using-sql-server"></a>Überprüfen Sie die heruntergeladene Daten mithilfe von SQL Server

Stellen Sie zuerst fest, dass Ihre Daten korrekt geladen wurden.

1. Herstellen einer Verbindung mit Ihrem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zielinstanz aus, Ihre bevorzugten Datenbankverwaltungstool, z. B. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Server-Explorer in Visual Studio oder Visual Studio-Code.

2. Wählen Sie die Datenbank, die Sie erstellt haben, die und erweitern, um die neue Datenbank, Tabellen und Funktionen finden Sie unter.
  
    ![rsql_e2e_ssms_newobjects](media/rsql-e2e-ssms-newobjects.PNG)
  
3.  Stellen Sie sicher, dass die Daten ordnungsgemäß geladen, mit der rechten Maustaste in der Tabelle, und wählen Sie **oberste 1000 Zeilen auswählen**. Die Menüoption führt diese Abfrage aus:

    ```SQL
    SELECT TOP 1000 * FROM [dbo].[nyctaxi_sample]
    ```
    Wenn keine Daten in der Tabelle nicht angezeigt werden, wechseln Sie im vorherigen Abschnitt zu [Problembehandlung](/walkthrough-prepare-the-data.md) .

4. Diese Datentabelle wurde für setbasierte Vorgänge optimiert, indem ein [Columnstore-Index](../../relational-databases/indexes/columnstore-indexes-overview.md) hinzugefügt wurde. Führen Sie diese Anweisung, um eine kurze Zusammenfassung für die Tabelle generieren.

    ```SQL
    SELECT DISTINCT [passenger_count]
        , ROUND (SUM ([fare_amount]),0) as TotalFares
        , ROUND (AVG ([fare_amount]),0) as AvgFares
    FROM [dbo].[nyctaxi_sample]
    GROUP BY [passenger_count]
    ORDER BY  AvgFares DESC
    ````
    In der nächsten Lektion generieren Sie einige komplexere Zusammenfassungen mit R.

## <a name="next-lesson"></a>Nächste Lektion

[Zusammenfassen von Daten mithilfe von R](/walkthrough-view-and-summarize-data-using-r.md)

## <a name="previous-lesson"></a>Vorherige Lektion

[Vorbereiten der Daten mithilfe von PowerShell](/walkthrough-prepare-the-data.md)

