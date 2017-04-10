---
title: "Grundlegendes zur inkrementellen Generierung | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Inkrementelle Generierung [Analysis Services]"
  - "Schemagenerierungs-Assistent, inkrementelle Generierung"
  - "Relationales Schema [Analysis Services], inkrementelle Generierung"
ms.assetid: 3ca0aa63-3eb5-4fe9-934f-8e96dee84eaa
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 29
---
# Grundlegendes zur inkrementellen Generierung
  Nach der Generierung des Anfangsschemas können Sie Cube- und Dimensionsdefinitionen mithilfe von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]ändern und dann den Schemagenerierungs-Assistenten erneut ausführen. Der Assistent aktualisiert das Schema in der Themenbereichsdatenbank und in der zugehörigen Datenquellensicht, um die Änderungen wiederzugeben. Dabei werden die aktuell in den erneut zu generierenden Tabellen vorhandenen Daten so weit wie möglich beibehalten. Wenn Sie die Tabellen nach der Anfangsgenerierung geändert haben, werden diese Änderungen, falls möglich, vom Schemagenerierungs-Assistenten unter Berücksichtigung folgender Regeln beibehalten:  
  
-   Wurde eine Tabelle vorher vom Assistenten generiert, wird die Tabelle überschrieben. Sie können verhindern, dass eine vom Assistenten erstellte Tabelle überschrieben wird, indem Sie die **AllowChangesDuringGeneration** -Eigenschaft für die Tabelle in der Datenquellensicht in **false**ändern. Wenn Sie die Steuerung einer Tabelle übernehmen, wird die Tabelle wie jede andere benutzerdefinierte Tabelle behandelt und bleibt von der erneuten Generierung unberührt. Wenn Sie eine Tabelle aus der Generierung entfernen, können Sie die **AllowChangesDuringGeneration** -Eigenschaft für die Tabelle später in der Datenquellensicht in **true** ändern und die Tabelle für Änderungen durch den Assistenten erneut öffnen. Weitere Informationen finden Sie unter [Ändern von Eigenschaften in einer Datenquellensicht &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/change-properties-in-a-data-source-view-analysis-services.md).  
  
-   Wurde eine Tabelle der Datenquellensicht oder der zugrunde liegenden Datenbank nicht durch den Assistenten hinzugefügt, wird die Tabelle nicht überschrieben.  
  
 Wenn der Schemagenerierungs-Assistent Tabellen erneut generiert, die vorher in der Themenbereichsdatenbank generiert wurden, können Sie wählen, ob der Assistent in diesen Tabellen vorhandene Daten beibehalten soll.  
  
## Unterstützen der Beibehaltung von Daten  
 Im Allgemeinen behält der Schemagenerierungs-Assistenten Daten bei, die in den von ihm erstellten Tabellen gespeichert sind. Darüber hinaus werden Daten auch dann vom Assistenten beibehalten, wenn Sie Spalten zu Tabellen hinzufügen, die vom Assistenten generiert wurden. Sie können diese Funktion verwenden, um Dimensionen und Cubes hinzuzufügen oder zu ändern und dann die zugrunde liegenden Objekte erneut zu generieren, ohne die in den zugrunde liegenden Tabellen gespeicherten Daten erneut laden zu müssen.  
  
> [!NOTE]  
>  Wenn Sie Daten aus durch Trennzeichen getrennten Textdateien laden, können Sie auch wählen, ob der Schemagenerierungs-Assistent diese Dateien und die in ihnen enthaltenen Daten während der erneuten Generierung überschreiben soll. Textdateien werden entweder vollständig oder überhaupt nicht überschrieben. Diese Dateien werden vom Schemagenerierungs-Assistent nicht teilweise überschrieben. Standardmäßig werden diese Dateien nicht überschrieben.  
  
### Teilweise Beibehaltung  
 Der Schemagenerierungs-Assistent kann vorhandene Daten in einigen Fällen nicht beibehalten. Die folgende Tabelle enthält Beispiele für Situationen, in denen der Assistent bei der erneuten Generierung nicht alle in den zugrunde liegenden Tabellen vorhandenen Daten beibehalten kann.  
  
|Art der Datenänderung|Behandlung|  
|-------------------------|---------------|  
|Inkompatible Datentypänderung|Der Schemagenerierungs-Assistent verwendet, falls möglich, Standard- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentypkonvertierungen, um vorhandene Daten von einem Datentyp in einen anderen zu konvertieren. Wenn Sie jedoch den Datentyp eines Attributs in einen Typ ändern, der mit den vorhandenen Daten nicht kompatibel ist, werden die Daten der betroffenen Spalte vom Assistenten gelöscht.|  
|Fehler in der referentiellen Integrität|Wenn Sie eine Dimension oder einen Cube mit Daten ändern und die Änderung bei der erneuten Generierung einen Fehler in der referentiellen Integrität verursacht, werden alle Daten in der Fremdschlüsseltabelle vom Assistenten gelöscht. Die gelöschten Daten sind nicht auf die Spalte beschränkt, die die Verletzung der Fremdschlüsseleinschränkung verursacht hat, oder auf die Zeilen mit den Fehlern in der referentiellen Integrität. Wenn Sie beispielsweise den Dimensionsschlüssel in ein Attribut mit nicht eindeutigen oder NULL-Daten ändern, werden alle vorhandenen Daten in der Fremdschlüsseltabelle gelöscht. Darüber hinaus kann das Löschen aller Dateien in einer Tabelle zu einem kaskadierenden Effekt und zu weiteren Verletzungen der referentiellen Integrität führen.|  
|Gelöschtes Attribut oder gelöschte Dimension|Wenn Sie ein Attribut aus einer Dimension löschen, löscht der Schemagenerierungs-Assistent die Spalte, die dem gelöschten Attribut zugeordnet ist. Wenn Sie eine Dimension löschen, löscht der Assistent die Tabelle, die der gelöschten Dimension zugeordnet ist. In diesen Fällen löscht der Assistent die Daten, die in der gelöschten Spalte oder Tabelle enthalten sind.|  
  
 Der Schemagenerierungs-Assistent gibt vor dem Löschen von Daten eine Warnung aus, damit Sie den Assistenten abbrechen können, ohne Daten zu verlieren. Der Schemagenerierungs-Assistent ist jedoch nicht in der Lage, zwischen einem erwarteten Datenverlust und einem unerwarteten Datenverlust zu unterscheiden. Wenn Sie den Assistenten ausführen, werden die Tabellen und Spalten mit Daten, die gelöscht werden, in einem Dialogfeld aufgelistet. Sie können den Assistenten entweder fortfahren und die Daten löschen lassen, oder Sie brechen den Assistenten ab und überarbeiten die Änderungen, die Sie an Tabellen und Spalten vorgenommen haben.  
  
## Unterstützen von Cube- und Dimensionsänderungen  
 Wenn Sie die Eigenschaften von Dimensionen und Cubes ändern,  werden die entsprechenden Objekte in der zugrunde liegenden Themenbereichsdatenbank sowie in der zugehörigen Datenquellensicht wie in der folgenden Tabelle beschrieben vom Schemagenerierungs-Assistenten erneut generiert.  
  
 Löschen eines Objekts, z. B. einer Dimension, eines Cubes oder eines Attributs  
 Der Schemagenerierungs-Assistent löscht die zugrunde liegenden Objekte, denen das gelöschte Objekt zugeordnet ist. Wenn Sie einer vom Assistenten erstellten Tabelle Spalten hinzufügen, verhindern die neuen Spalten nicht das Löschen der Tabelle. Das Löschen eines Objekts führt dazu, dass die in den zugrunde liegenden Objekten gespeicherten Daten gelöscht werden, und kann bei Fehlern in der referentiellen Integrität auch zum Löschen weiterer Daten führen.  
  
 Umbenennen eines Objekts, z. B. einer Dimension, eines Cubes oder eines Attributs  
 Der Schemagenerierungs-Assistent benennt die zugrunde liegenden Objekte, denen das umbenannte Objekt zugeordnet ist, um. Der Assistent benennt auch alle betroffenen Objekte, z. B. Primärschlüssel, um. Vorhandene Daten in den zugrunde liegenden Objekten werden beibehalten.  
  
 Ändern eines Objekts, z. B. Ändern seines Datentyps  
 Der Schemagenerierungs-Assistent ändert die zugrunde liegenden Objekte, denen das geänderte Objekt zugeordnet ist. Vorhandene Daten in den zugrunde liegenden Objekten in den Datenbanken werden beibehalten, es sei denn, der neue Datentyp ist mit den vorhandenen Daten nicht kompatibel.  
  
 Hinzufügen eines neuen Objekts, z. B. einer Dimension, eines Cubes oder eines Attributs  
 Der Schemagenerierungs-Assistent fügt die zugrunde liegenden Objekte, denen das neue Objekt zugeordnet ist, hinzu.  
  
 Kann der Schemagenerierungs-Assistent die erforderliche Änderung wegen des Vorhandenseins eines Benutzerobjekts in der Themenbereichsdatenbank nicht vornehmen (da das Datenbankmodul einen Fehler zurückgibt), erzeugt der Schemagenerierungs-Assistent einen Fehler und zeigt den vom Datenbankmodul zurückgegebenen Fehler an. Wenn Sie beispielsweise eine Primärschlüsseleinschränkung oder einen nicht gruppierten Index für eine Tabelle erstellen, nachdem der Assistent die Tabelle generiert hat, wird diese Tabelle nicht vom Schemagenerierungs-Assistenten gelöscht, da er die Einschränkung bzw. den Index nicht erstellt hat.  
  
## Unterstützen von Schemaänderungen  
 Wenn Sie die Eigenschaften der Tabellen oder Spalten in der Themenbereichsdatenbank oder in der zugeordneten Datenquellensicht ändern, behandelt der Schemagenerierungs-Assistent die Änderungen wie in der folgenden Tabelle beschrieben.  
  
 Löschen einer Tabelle oder einer Spalte, die vom Schemagenerierungs-Assistenten generiert wurde  
 Wenn Sie eine Tabelle oder eine Spalte löschen, die vom Schemagenerierungs-Assistenten generiert wurde, wird die gelöschte Tabelle vom Assistenten erneut generiert. Der Assistent stellt keine Warnung bereit, dass die gelöschte Tabelle oder Spalte erneut generiert wird.  
  
 Ändern der Eigenschaften einer Tabelle oder Spalte, die vom Schemagenerierungs-Assistenten erstellt wurde  
 Wenn Sie die Eigenschaften einer Tabelle oder einer Spalte, die vom Schemagenerierungs-Assistenten erstellt wurde, ändern, wird die geänderte Tabelle vom Assistenten ohne die Änderung erneut generiert. Wenn Sie beispielsweise den Datentyp oder die NULL-Zulässigkeit einer Spalte oder die Dateigruppe einer Tabelle ändern, die vom Schemagenerierungs-Assistenten erstellt wurde, bleibt die Änderung nach der erneuten Generierung nicht bestehen. Der Assistent stellt keine Warnung bereit, dass das geänderte Objekt ohne die Änderung erneut generiert wird.  
  
 Hinzufügen einer Spalte zu einer vom Schemagenerierungs-Assistenten erstellten Tabelle oder Hinzufügen einer Tabelle zur Themenbereichsdatenbank oder Stagingbereichsdatenbank  
 Wenn Sie einer vom Schemagenerierungs-Assistenten erstellten Tabelle eine Spalte hinzufügen, behält der Assistent die zusätzliche Spalte zusammen mit den darin gespeicherten Daten bei der erneuten Generation bei. Wenn Sie jedoch der Themenbereichsdatenbank oder der Stagingbereichsdatenbank eine Tabelle hinzufügen, wird die neue Tabelle vom Schemagenerierungs-Assistenten nicht eingebunden. Die hinzugefügte Spalte bzw. Tabelle ist nicht im [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt, in der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank, den DTS-Paketen, der Datenquellensicht oder an anderer Stelle im generierten Schema enthalten.  
  
## Unterstützen von Änderungen an Datenquelle und Datenquellensicht  
 Wird der Schemagenerierungs-Assistent erneut ausgeführt, verwendet er dieselbe Datenquelle und Datenquellensicht wie für die ursprüngliche Generierung. Wenn Sie eine Datenquelle oder Datenquellensicht hinzufügen, wird diese vom Assistenten nicht verwendet. Wenn Sie die ursprüngliche Datenquelle oder Datenquellensicht nach der Anfangsgenerierung löschen, müssen Sie den Assistenten von Anfang an ausführen. Alle bisherigen Einstellungen im Assistenten werden ebenfalls gelöscht. Alle vorhandenen Objekte in einer zugrunde liegenden Datenbank, die mit einer gelöschten Datenquelle oder Datenquellensicht verbunden waren, werden bei dem nächsten Ausführen des Schemagenerierungs-Assistenten als vom Benutzer erstellte Objekte behandelt.  
  
 Gibt die Datenquellensicht nicht den tatsächlichen Status der zugrunde liegenden Datenbank zum Zeitpunkt der Generierung wieder, kann es bei dem Schemagenerierungs-Assistenten zu Fehlern bei der Generierung von Schemas für die Themenbereichsdatenbank und die Stagingbereichsdatenbank kommen. Wenn beispielsweise die Datenquellensicht angibt, dass der Datentyp für eine Spalte auf **int**festgelegt wird, der Datentyp für die Spalte aber tatsächlich auf **string**festgelegt ist, legt der Schemagenerierungs-Assistent den Datentyp für den Fremdschlüssel in Übereinstimmung mit der Datenquellensicht auf **int** fest und erzeugt dann beim Erstellen der Beziehung einen Fehler, da der tatsächliche Datentyp **string**ist.  
  
 Wenn Sie allerdings die Datenquellen-Verbindungszeichenfolge auf eine andere Datenbank aus der vorherigen Generierung ändern, wird kein Fehler generiert. Es wird die neue Datenbank verwendet und keine Änderung an der vorherigen Datenbank vorgenommen.  
  
## Siehe auch  
 [Verwalten von Änderungen an Datenquellensichten und Datenquellen](../../analysis-services/multidimensional-models/manage-changes-to-data-source-views-and-data-sources.md)   
 [Schemagenerierungs-Assistent &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/schema-generation-wizard-analysis-services.md)  
  
  