---
title: 'Analysis Services Tutorial Lektion 1: erstellen ein neuen tabellenmodellprojekts | Microsoft Docs'
description: Beschreibt, wie ein neues Analysis Services Tutorials-Projekt zu erstellen.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 55213810bdc40bf817b1349715474974d6a72540
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-tabular-model-project"></a>Erstellen Sie ein Projekt für tabellarische Modelle

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In dieser Lektion verwenden Sie Visual Studio mit SQL Server Data Tools (SSDT) oder Visual Studio 2017 mit Microsoft Analysis Services-Projekten VSIX-Methode, um ein neues Projekt für tabellarische Modelle mit Kompatibilitätsgrad 1400 zu erstellen. Sobald das neue Projekt erstellt wurde, können Sie beginnen Hinzufügen von Daten und die Erstellung des Modells. In dieser Lektion werden Ihnen auch eine kurze Einführung in das tabellarische Modell erstellungsumgebung in Visual Studio.  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **10 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten

Dieser Artikel ist die erste Lektion in ein Lernprogramm zur tabellenmodellerstellung. Um diese Lektion abzuschließen, gibt es mehrere Voraussetzungen, dass Sie direkte haben müssen. Weitere Informationen finden Sie unter [Analysis Services – Adventure Works-Lernprogramm](../tutorial-tabular-1400/as-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Erstellen eines neuen Tabellenmodellprojekts  
  
#### <a name="to-create-a-new-tabular-model-project"></a>So erstellen Sie ein neues Tabellenmodellprojekt  
  
1.  In Visual Studio auf die **Datei** Menü klicken Sie auf **neu** > **Projekt**.  
  
2.  In der **neues Projekt** Dialogfeld erweitern Sie **installiert** > **Business Intelligence** > **Analysis Services**, und klicken Sie dann auf **tabellarischen Analysis Services-Projekts**.  
  
3.  In **Namen**, Typ **AW Internet Sales**, und geben Sie einen Speicherort für die Projektdateien.  
  
    Standardmäßig **Projektmappenname** ist identisch mit den Namen des Projekts; Sie können jedoch einen anderen Projektmappennamen eingeben.  
  
4.  Klicken Sie auf **OK**.  
  
5.  In der **Designer für tabellarische Modelle** wählen Sie im Dialogfeld **integrierten Arbeitsbereich**.  
  
    Der Arbeitsbereich hostet eine tabellarische Modelldatenbank mit dem gleichen Namen wie das Projekt während der Modellerstellung an. Arbeitsbereich "integrierte" bedeutet, dass dadurch entfällt die Notwendigkeit, installieren Sie eine separate Instanz der Analysis Services-Server für die Modellerstellung verwendet eine integrierte Instanz von Visual Studio.
      
6.  In **Kompatibilitätsgrad**Option **SQL Server 2017 / Azure Analysis Services (1400)**.   
 
    ![als Lektion 1 zu tmd](../tutorial-tabular-1400/media/as-lesson1-tmd.png)
      
    Wenn SQL Server 2017 / Azure Analysis Services (1400) im Compatibility Level Listenfeld nicht angezeigt wird, verwenden Sie nicht die neueste Version von SQL Server Data Tools. Sie können die neueste Version unter [Installieren von SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)herunterladen.  
      
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a>Grundlegendes zu SSDT tabellenmodellerstellung Umgebung  

Nun, dass Sie ein neues tabellarisches Modellprojekt erstellt haben, werfen wir einen Moment Zeit, untersuchen Sie das tabellarische Modell erstellungsumgebung in Visual Studio.  
  
Nachdem das Projekt erstellt wurde, wird er in Visual Studio geöffnet. Auf der rechten Seite in **tabellarische Modell-Explorer**, finden Sie unter eine Strukturansicht der Objekte in Ihrem Modell. Da Sie Daten noch nicht geschehen importiert haben, sind die Ordner leer. Sie können einen Ordner Objekt zum Ausführen von Aktionen, ähnlich wie auf der Menüleiste auf rechtsklicken. Während Sie in diesem Lernprogramm durchlaufen, verwenden Sie das tabellarische Modell-Explorer, um verschiedene Objekte in Ihrem Modellprojekt zu navigieren.

![Zeit als Lektion 1 zu](../tutorial-tabular-1400/media/as-lesson1-tme.png)

Klicken Sie auf die **Projektmappen-Explorer** Registerkarte. Hier sehen Sie Ihre **Model.bim** Datei. Wenn Sie das Designer-Fenster auf der linken Seite (das leere Fenster mit der Registerkarte Model.bim) im sehen **Projektmappen-Explorer**unter **AW Internet Sales Projekt**, doppelklicken Sie auf die **Model.bim** Datei. Die Model.bim-Datei enthält die Metadaten für das Modellprojekt erstellen. 

![Se als Lektion 1 zu](../tutorial-tabular-1400/media/as-lesson1-se.png)
  
Klicken Sie auf **Model.bim**. In der **Eigenschaften** Fenster sehen Sie die Modelleigenschaften, die wichtigste die **DirectQuery-Modus** Eigenschaft. Diese Eigenschaft gibt an, ob das Modell im InMemory-Modus (aus) oder DirectQuery-Modus (On) bereitgestellt wird. In diesem Lernprogramm erstellen und das Modell im InMemory Modus bereitstellen.

![als Lektion 1 zu Eigenschaften](../tutorial-tabular-1400/media/as-lesson1-properties.png)
  
Wenn Sie ein Modellprojekt erstellen, bestimmte Modelleigenschaften werden automatisch festgelegt gemäß den datenmodellierungseinstellungen, die angegeben werden können die **Tools** Menü > **Optionen** (Dialogfeld). Die Eigenschaften für die Datensicherung, Beibehaltung des Arbeitsbereichs und den Arbeitsbereichsserver geben an, wie und wo die Arbeitsbereichsdatenbank (Datenbank zur Modellerstellung) gesichert, speicherintern beibehalten und erstellt wird. Sie können diese Einstellungen später ändern, falls erforderlich, aber lassen Sie diese Eigenschaften unverändert.  

In **Projektmappen-Explorer**, mit der rechten Maustaste **AW Internet Sales** (Projekt), und klicken Sie dann auf **Eigenschaften**. Die **Eigenschaftenseiten des AW Internet Sales** Dialogfeld wird angezeigt. Sie legen Sie einige dieser Eigenschaften später bei der Bereitstellung des Modells.  
  
Wenn Sie SSDT installiert haben, wurden der Visual Studio-Umgebung mehrere neue Menüelemente hinzugefügt. Klicken Sie auf die **Modell** Menü. Dort können können Sie Daten importieren, Arbeitsbereichsdaten aktualisieren Durchsuchen des Modells in Excel, Perspektiven und Rollen erstellen, die modellsicht auswählen und Berechnungsoptionen festlegen. Klicken Sie auf die **Tabelle** Menü. Dort können können Sie erstellen und Verwalten von Beziehungen, datumstabelleneigenschaften festlegen, Partitionen erstellen und Tabelleneigenschaften bearbeiten. Wenn Sie auf die **Spalte** Menü Sie hinzufügen und Löschen von Spalten in einer Tabelle, Fixieren Sie Spalten und Angeben der Sortierreihenfolge. SSDT fügt auch einige Schaltflächen der Leiste hinzu. Besonders hilfreich ist die AutoSumme-Funktion, um ein standardaggregationsmeasure für eine ausgewählte Spalte zu erstellen. Weitere Schaltflächen in der Symbolleiste bieten einen schnellen Zugriff auf häufig verwendete Funktionen und Befehle.  
  
Erkunden Sie einige der Dialogfelder und Positionen für verschiedene Funktionen, die für die Erstellung von Tabellenmodellen konzipiert sind. Während einige Elemente noch nicht aktiv sind, können Sie dennoch einen Einblick in die Umgebung zur tabellenmodellerstellung abrufen.  
  

## <a name="whats-next"></a>Wie geht es weiter?

[Lektion 2: Abrufen von Daten](../tutorial-tabular-1400/as-lesson-2-get-data.md).

  
  
  
