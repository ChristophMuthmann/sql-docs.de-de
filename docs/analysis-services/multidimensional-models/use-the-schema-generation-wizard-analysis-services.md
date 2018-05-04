---
title: Verwenden der Schemagenerierungs-Assistent (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4b80fef5f104590c6c4c4c71341979dfa451aa81
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="use-the-schema-generation-wizard-analysis-services"></a>Verwenden des Schemagenerierungs-Assistenten (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Beim Schemagenerierungs-Assistenten müssen während der Generierungsphase nur wenige Informationen eingegeben werden. Die meisten Informationen, die der Schemagenerierungs-Assistent zum Generieren relationaler Schemas benötigt, werden aus den [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Cubes und -Dimensionen extrahiert, die Sie bereits im Projekt erstellt haben. Darüber hinaus können Sie anpassen, wie das Schema der Themenbereichsdatenbank generiert wird und wie Objekte im Schema benannt werden.  
  
## <a name="start-the-wizard"></a>Starten des Assistenten  
 Es gibt mehrere Möglichkeiten, den Schemagenerierungs-Assistenten in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] zu öffnen:  
  
-   Klicken Sie mit der rechten Maustaste auf das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projektobjekt, und klicken Sie anschließend im Kontextmenü auf **Relationales Schema generieren** .  
  
-   Klicken Sie auf das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projektobjekt und dann im Menü **Datenbank** auf **Relationales Schema generieren** .  
  
-   Starten Sie den Assistenten innerhalb des Dimensions-Assistenten, indem Sie auf der letzten Seite des Assistenten auf das Kontrollkästchen **Schema jetzt generieren** klicken.  
  
## <a name="step-1-specify-targets"></a>Schritt 1: Angeben von Zielen  
 Sie müssen die Datenquellensicht (Data Source View, DSV) angeben, in der der Schemagenerierungs-Assistent das Schema für die Themenbereichsdatenbank generieren soll. Obwohl Sie eine vorhandene DSV auswählen können, erstellen Sie in der Regel eine neue Sicht auf Grundlage einer Datenquelle. Sie können die Datenquelle basierend auf einer vorhandenen oder neuen Verbindung oder basierend auf einem anderen Objekt erstellen. Der Schemagenerierungs-Assistent generiert das Schema für die Themenbereichsdatenbank in der Datenbank, auf die die Datenquelle verweist, sowie in der Datenquellensicht. Dabei erstellt der Schemagenerierungs-Assistent nicht die Themenbereichsdatenbank selbst, sondern das relationale Schema zur Unterstützung der Cubes und Dimensionen in einer vorhandenen Datenbank, die Sie angeben.  
  
 Wenn der Schemagenerierungs-Assistent die zugrunde liegenden Objekte erstellt, bindet er die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dimensionen und -Cubes mithilfe von Datenquellensicht-Bindungen an die generierten Tabellen und Spalten.  
  
> [!NOTE]  
>  Um die Bindung für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dimensionen und -Cubes an zuvor generierte Objekte aufzuheben, löschen Sie die Datenquellensicht, an die die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Cubes und -Dimensionen gebunden sind, und definieren Sie anschließend die neue Datenquellensicht für die Cubes und Dimensionen mithilfe des Schemagenerierungs-Assistenten.  
  
## <a name="step-3-specify-schema-options-for-the-subject-area-database"></a>Schritt 3: Angeben von Schemaoptionen für die Themenbereichsdatenbank  
 Der Schemagenerierungs-Assistent stellt eine Reihe von Optionen zum Definieren des Schemas bereit, das für die Themenbereichsdatenbank generiert wird. Sie können diese Optionen auf der Seite **Schemaoptionen für die Themenbereichsdatenbank** des Assistenten angeben.  
  
### <a name="specifying-the-schema-owner"></a>Angeben des Schemabesitzers  
 Sie können den Besitzer des Schemas angeben, indem Sie für den Wert von **Besitzendes Schema** eine gültige Zeichenfolge festlegen. Der Standardbesitzer des Schemas ist das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt. Sie können jedoch jeden gewünschten Schemabesitzer angeben.  
  
### <a name="specifying-primary-keys-indexes-and-constraints"></a>Angeben von Primärschlüsseln, Indizes und Einschränkungen  
 Der Schemagenerierungs-Assistent erstellt standardmäßig in jeder Dimensionstabelle in der Themenbereichsdatenbank eine Primärschlüsseleinschränkung. Der Primärschlüssel entspricht dem Attribut, das in der entsprechenden [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dimension als Schlüsselattribut festgelegt ist. Durch diese Einschränkung wird die Verarbeitungsleistung in den meisten Umgebungen bei minimalen Kosten verbessert. Logische Primärschlüssel werden immer in der Datenquellensicht erstellt, auch wenn Sie angeben, dass in der Themenbereichsdatenbank kein Primärschlüssel erstellt werden soll. Um für Dimensionstabellen Primärschlüsseleinschränkungen zu definieren, klicken Sie auf **Primärschlüssel für Dimensionstabellen erstellen**.  
  
 Der Assistent erstellt standardmäßig auch Indizes für die Fremdschlüsselspalten in den einzelnen Faktentabellen. Diese Indizes tragen in den meisten Umgebungen zu einer Verbesserung der Verarbeitungsleistung bei. Die Leistung wird in der Regel verbessert, weil die Verarbeitungsabfrage, die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] generiert, um neue Daten aus der Themenbereichsdatenbank abzurufen, eine erhebliche Anzahl von JOIN-Anweisungen zwischen der Faktentabelle und den Dimensionstabellen enthält. Um Indizes für die Fremdschlüsselspalten in den einzelnen Faktentabellen zu erstellen, klicken Sie auf **Indizes erstellen**.  
  
 Schließlich erzwingt der Assistent standardmäßig referenzielle Integrität zwischen der Faktentabelle und den einzelnen Dimensionstabellen. Auch wenn Sie angeben, dass keine referenzielle Integrität erzwungen werden soll, erstellt der Schemagenerierungs-Assistent dennoch diese Beziehungen in der Datenbank und der Datenquellensicht. Um referenzielle Integrität zu erzwingen, klicken Sie auf **Referenzielle Integrität erzwingen**.  
  
### <a name="preserving-data-for-incremental-generation"></a>Beibehalten von Daten für inkrementelle Generierung  
 Der Schemagenerierungs-Assistent versucht beim erneuten Generieren des Datenbankschemas standardmäßig Daten beizubehalten. Wenn der Schemagenerierungs-Assistent Zeilen aufgrund einer Schemaänderung löschen muss, wird vor dem Löschen der Zeilen eine Warnung angezeigt. So müssen Zeilen möglicherweise gelöscht werden, um Probleme mit der referenziellen Integrität zu beheben, die auftreten, wenn eine Dimension gelöscht oder beim Ändern eines Dimensionsattributs ein Datentyp geändert wurde. Um beim erneuten Generieren des Datenbankschemas Daten beizubehalten, klicken Sie auf **Daten bei erneuter Generierung beibehalten**.  
  
## <a name="step-4-specify-naming-conventions"></a>Schritt 4: Angeben von Benennungskonventionen  
 Auf der Seite **Benennungskonventionen angeben** des Assistenten können Sie die Benennungskonventionen angeben, die der Schemagenerierungs-Assistent beim Generieren bestimmter Objekte in der Themenbereichsdatenbank verwendet. Weitere Informationen über die verfügbaren Optionen auf der Seite **Benennungskonventionen angeben** finden Sie unter [Benennungskonventionen angeben &#40;Schemagenerierungs-Assistent&#41; &#40;Analysis Services – Mehrdimensionale Daten&#41;](http://msdn.microsoft.com/library/02d830ea-5b1f-4485-9f94-d64b8bea592b).  
  
  
