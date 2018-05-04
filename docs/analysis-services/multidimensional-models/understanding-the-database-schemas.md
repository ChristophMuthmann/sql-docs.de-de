---
title: Grundlegendes zu Datenbankschemas | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: aff2fa15822aa4a6b38d46bc6a8cd8497be5fa6c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="understanding-the-database-schemas"></a>Grundlegendes zu Datenbankschemas
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Der Schemagenerierungs-Assistent generiert ein nicht normalisiertes relationales Schema für die Datenbank des Themenbereichs auf Basis der Dimensionen und Measuregruppen in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Der Assistent generiert für jede Dimension eine relationale Tabelle zum Speichern von Dimensionsdaten, die als Dimensionstabelle bezeichnet wird, und für jede Measuregruppe eine relationale Tabelle zum Speichern von Faktendaten, die als Faktentabelle bezeichnet wird. Beim Generieren dieser relationalen Tabellen ignoriert der Assistent verknüpfte Dimensionen, verknüpfte Measuregruppen und Serverzeitdimensionen.  
  
## <a name="validation"></a>Überprüfung  
 Bevor das zugrunde liegende relationale Schema generiert wird, überprüft der Schemagenerierungs-Assistent die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Cubes und -Dimensionen. Wenn der Assistent einen Fehler feststellt, wird der Assistent beendet, und die Fehler werden an das Fenster Aufgabenliste in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]berichtet. Im Folgenden finden Sie Beispiele für Fehler, die das Generieren verhindern:  
  
-   Dimensionen, die mehr als ein Schlüsselattribut enthalten.  
  
-   Übergeordnete Attribute, deren Datentypen sich von denen der Schlüsselattribute unterscheiden.  
  
-   Measuregruppen, in denen keine Measures enthalten sind.  
  
-   Degenerierte Dimensionen oder Measures, die fehlerhaft konfiguriert sind.  
  
-   Ersatzschlüssel, die fehlerhaft konfiguriert sind, wie z. B. mehrere Attribute, die den **ScdOriginalID** -Attributtyp verwenden, oder ein Attribut mit dem **ScdOriginalID** -Attributtyp, das nicht an eine Spalte des integer-Datentyps gebunden ist.  
  
## <a name="dimension-tables"></a>Dimensionstabellen  
 Der Schemagenerierungs-Assistent generiert für jede Dimension eine Dimensionstabelle, die in die Datenbank des Themenbereichs eingeschlossen werden soll. Die Struktur der Dimensionstabelle hängt von den Optionen ab, die Sie beim Entwerfen der Dimension, auf der die Dimensionstabelle basiert, ausgewählt haben.  
  
 Spalten  
 Der Assistent generiert eine Spalte für die Bindungen, die den einzelnen Attributen der Dimension zugeordnet sind, auf der die Dimensionstabelle basiert. Hierzu zählen z.B. die Bindungen für die Eigenschaften **KeyColumns**, **NameColumn**, **ValueColumn**, **CustomRollupColumn**, **CustomRollupPropertiesColumn**und **UnaryOperatorColumn** jedes Attributs.  
  
 Beziehungen  
 Der Assistent generiert eine Beziehung zwischen der Spalte jedes übergeordneten Attributs und dem Primärschlüssel der Dimensionstabelle.  
  
 Bei Bedarf generiert der Assistent ebenfalls eine Beziehung zum Primärschlüssel in jeder zusätzlichen Dimensionstabelle, die im Cube als referenzierte Dimension definiert wird.  
  
 Einschränkungen  
 Der Assistent generiert standardmäßig eine PRIMARY KEY-Einschränkung für jede Dimensionstabelle auf Basis des Schlüsselattributs der Dimension. Beim Generieren der PRIMARY KEY-Einschränkung wird standardmäßig eine separate Namensspalte generiert. Ein logischer Primärschlüssel wird in der Datenquellensicht erstellt, auch wenn Sie den Primärschlüssel in der Datenbank nicht erstellen möchten.  
  
> [!NOTE]  
>  Ein Fehler tritt auf, wenn mehr als ein Schlüsselattribut in der Dimension, auf der die Dimensionstabelle basiert, angegeben wird.  
  
 Übersetzungen  
 Der Assistent generiert eine separate Tabelle für die übersetzten Werte eines beliebigen Attributs, das eine Übersetzungsspalte erfordert. Des Weiteren erstellt der Assistent eine separate Spalte für jede erforderliche Sprache.  
  
## <a name="fact-tables"></a>Faktentabellen  
 Der Schemagenerierungs-Assistent generiert für jede Measuregruppe eines Cubes eine Faktentabelle, die in die Datenbank des Themenbereichs eingeschlossen werden soll. Die Struktur der Faktentabelle hängt von den Optionen ab, die Sie beim Entwerfen der Measuregruppe, auf der die Faktentabelle basiert, ausgewählt haben. Des Weiteren hängt die Struktur von den zwischen der Measuregruppe und den eingeschlossenen Dimensionen erstellten Beziehungen ab.  
  
 Spalten  
 Der Assistent generiert für jedes Measure eine Spalte. Dies gilt nicht für Measures, die die **Count** -Aggregationsfunktion verwenden. Für diese Art von Measures ist in der Faktentabelle keine entsprechende Spalte erforderlich.  
  
 Der Assistent generiert ebenfalls eine Spalte pro Granularitätsattributspalte für jede reguläre Dimensionsbeziehung der Measuregruppe. Bei Bedarf generiert der Assistent mindestens eine Spalte für die Bindungen, die jedem Attribut einer Dimension mit einer Faktendimensionsbeziehung zur Measuregruppe, auf der die Tabelle basiert, zugeordnet sind.  
  
 Beziehungen  
 Der Assistent generiert eine Beziehung für jede reguläre Dimensionsbeziehung der Faktentabelle zum Granularitätsattribut der Dimensionstabelle. Wenn die Granularität auf dem Schlüsselattribut der Dimensionstabelle basiert, wird die Beziehung in der Datenbank und in der Datenquellensicht erstellt. Wenn die Granularität auf einem anderen Attribut basiert, wird die Beziehung nur in der Datenquellensicht erstellt.  
  
 Wenn Sie im Assistenten die Indizes generieren, wird ein nicht gruppierter Index für jede dieser Beziehungsspalten generiert.  
  
 Einschränkungen  
 Primärschlüssel werden nicht in Faktentabellen generiert.  
  
 Wenn Sie die referenzielle Integrität erzwingen möchten, werden bei Bedarf Einschränkungen für die referenzielle Integrität zwischen Dimensionstabellen und Faktentabellen generiert.  
  
 Übersetzungen  
 Der Assistent generiert eine separate Tabelle für die übersetzten Werte beliebiger Eigenschaften der Measuregruppe, die eine Übersetzungsspalte erfordert. Des Weiteren erstellt der Assistent eine separate Spalte für jede erforderliche Sprache.  
  
## <a name="data-type-conversion-and-default-lengths"></a>Datentypkonvertierung und Standardlängen  
 Der Schemagenerierungs-Assistent ignoriert Datentypen in allen Fällen außer in Spalten, die den Datentyp [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **wchar** verwenden. Die **wchar** -Datengröße wird direkt in den **nvarchar** -Datentyp übersetzt. Wenn die angegebene Länge einer Spalte, die die **wchar** -Größe verwendet, 4.000 Byte überschreitet, generiert der Schemagenerierungs-Assistent einen Fehler.  
  
 Wenn für ein Datenelement, wie z. B. die Bindung eines Attributs, keine Länge angegeben ist, wird für die Spalte die in der folgenden Tabelle aufgelistete Standardlänge verwendet.  
  
|Datenelement|Standardlänge (Byte)|  
|---------------|------------------------------|  
|KeyColumn|50|  
|NameColumn|50|  
|CustomRollupColumn|3000|  
|CustomRollupPropertiesColumn|500|  
|UnaryOperatorColumn|1|  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zur inkrementellen Generierung](../../analysis-services/multidimensional-models/understanding-incremental-generation.md)   
 [Verwalten von Änderungen an Datenquellensichten und Datenquellen](../../analysis-services/multidimensional-models/manage-changes-to-data-source-views-and-data-sources.md)  
  
  
