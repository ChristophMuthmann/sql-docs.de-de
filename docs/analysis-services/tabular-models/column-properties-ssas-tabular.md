---
title: "Spalteneigenschaften (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.bidtoolset.columnprop.f1"
ms.assetid: 4046c1a3-46c7-47db-b355-52e9c2f23671
caps.latest.revision: 14
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 14
---
# Spalteneigenschaften (SSAS – tabellarisch)
  In diesem Thema werden die Spalteneigenschaften für tabellarische Modelle beschrieben.  
  
 Abschnitte in diesem Thema:  
  
-   [Spalteneigenschaften](#bkmk_properties)  
  
-   [So konfigurieren Sie Eigenschaftseinstellungen für Spalten](#bkmk_config_prop)  
  
##  <a name="bkmk_properties"></a> Spalteneigenschaften  
 **Standard**  
  
|Eigenschaft|Standardeinstellung|Description|  
|--------------|---------------------|-----------------|  
|**Spaltenname**||Der Name der Spalte, der im Modell gespeichert und in der Feldliste von Berichtserstellungsclients angezeigt wird.|  
|**Datenformat**|Wird automatisch während des Imports bestimmt.|Gibt das Anzeigeformat an, das für Daten in dieser Spalte verwendet werden soll. Diese Eigenschaft verfügt über folgende Optionen:<br /><br /> **Allgemein**<br /><br /> **Decimal Number**<br /><br /> **Ganze Zahl**<br /><br /> **Währung**<br /><br /> **Prozentwert**<br /><br /> **Wissenschaftlich**<br /><br /> Nachdem Sie ein Datenformat festgelegt haben, können Sie Eigenschaften festlegen, die für jedes Format spezifisch sind. Wenn Sie z. B. das Format **Währung** wählen, können Sie die Anzahl der sichtbaren Dezimalstellen festlegen und das Tausendertrennzeichen und das Währungssymbol auswählen.<br /><br /> <br /><br /> Wenn die Spaltenwerte Bilder enthalten, siehe **Repräsentatives Bild**.|  
|**Datentyp**|Wird automatisch während des Imports bestimmt.|Gibt den Datentyp für alle Werte in der Spalte an.|  
|**Description**||Eine Textbeschreibung für die Spalte.<br /><br /> In bestimmten Berichtserstellungsclients wird die Beschreibung als QuickInfo angezeigt, wenn der Endbenutzer den Cursor über dieser Spalte in der Feldliste hält.|  
|**Hidden**|False|Gibt an, ob die Spalte in den Feldlisten von Berichtserstellungsclients ausgeblendet wird.<br /><br /> Legen Sie diese Eigenschaft auf **True** fest, um diese Spalte in der Anzeige auszublenden. Zum Beispiel sind Spalten, die Bezeichner oder Schlüssel enthalten, für den Endbenutzer in der Regel nicht nützlich.<br /><br /> Wenn Sie eine Spalte im Berichtserstellungsclient ausblenden, wird das Feld nicht in den Modelldaten unterdrückt. Das Feld ist immer noch sichtbar, wenn Sie eine Abfrage für das Modell erstellen. Eine ausgeblendete Spalte kann weiterhin für Gruppierungen oder Sortierungen verwendet werden.<br /><br /> Die Eigenschaft **Ausgeblendet** stellt keinerlei Datensicherheit bereit. Verwenden Sie Zeilenfilter in Rollen, wenn Sie Daten schützen möchten. Weitere Informationen finden Sie unter [Rollen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/roles-ssas-tabular.md).|  
|**Nach Spalte sortieren**||Gibt eine andere Spalte an, nach der die Werte in dieser Spalte sortiert werden. Zwischen den beiden Spalten muss eine Beziehung vorhanden sein.<br /><br /> Dieser Wert muss der Name einer vorhandenen Spalte sein. Sie können keine Formel oder Measure angeben.|  
  
 **Berichterstellungseigenschaften**  
  
 Ausführliche Informationen über das Festlegen der [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]-Tabellenverhaltenseigenschaften finden Sie unter [Konfigurieren von Tabellenverhaltenseigenschaften für Power View-Berichte &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/configure-table-behavior-properties-for-power-view-reports-ssas-tabular.md).  
  
|Eigenschaft|Standardeinstellung|Description|  
|--------------|---------------------|-----------------|  
|Standardbild|False|Gibt an, welche Spalte ein Bild bereitstellt, das die Zeilendaten (z. B. eine Foto-ID in einem Mitarbeiterdatensatz) darstellt.|  
|Standardbeschriftung|False|Legt fest, welche Spalte einen Anzeigenamen angibt, um Zeilendaten (z. B. Mitarbeitername in einem Mitarbeiterdatensatz) darzustellen.|  
|Bild-URL/Datenkategorie (SP1)|False|Gibt den Wert in dieser Spalte als Link zu einem Bild auf einem Server an. Beispiel: http://localhost/images/image1.jpg.|  
|Eindeutige Zeilen beibehalten|False|Gibt an, welche Spalten Werte enthalten, die als eindeutig behandelt werden sollen, auch wenn sie Duplikate sind (z. B. Mitarbeitervorname und Nachname betreffend; in jenen Fällen, bei denen zwei oder mehr Mitarbeiter den gleichen Namen haben).|  
|Zeilenbezeichner|False|Gibt eine Spalte an, die nur eindeutige Werte enthält. Dadurch kann diese Spalte als interner Gruppierungsschlüssel verwendet werden.|  
|Zusammenfassen nach|Standardwert|Gibt Berichtserstellungsclienttools an, die die Aggregatfunktion SUM für die Spaltenberechnungen übernehmen, wenn einer Feldliste diese Spalte hinzugefügt wird. Wählen Sie es aus der Dropdownliste aus, um die Standardberechnung zu ändern. Diese Eigenschaft gilt nur für Spalten vom aggregierbaren Typ.|  
|Position der Tabellendetails|Kein Standardfeld festgelegt|Gibt diese Spalte an, oder einem Satz von Feldern von einer einzelnen Tabelle kann ein Measure hinzugefügt werden, um die Tabellenvisualisierungserfahrung in einem Berichtserstellungsclient zu verbessern.|  
  
##  <a name="bkmk_config_prop"></a> So konfigurieren Sie Eigenschaftseinstellungen für Spalten  
  
1.  Wählen Sie im Modell-Designer eine Spalte in einer Tabelle aus.  
  
2.  Klicken Sie im Fenster **Eigenschaften** auf eine Eigenschaft, und geben Sie dann einen Wert ein, oder klicken Sie auf den Pfeil nach unten, um eine Option auszuwählen.  
  
## Siehe auch  
 [Power View-Berichterstellungseigenschaften &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/power-view-reporting-properties-ssas-tabular.md)   
 [Ausblenden oder Einfrieren von Spalten &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/hide-or-freeze-columns-ssas-tabular.md)   
 [Hinzufügen von Spalten zu einer Tabelle &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/add-columns-to-a-table-ssas-tabular.md)  
  
  