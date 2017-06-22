---
title: "Vorbereiten von Excel-Daten für mobile Reporting Services-Berichte | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 02/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 16698f8d-bfc7-4eca-9e97-82c99d8bc08e
caps.latest.revision: 14
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c057de4b56529de08385a1e13e1a119550632eda
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="prepare-excel-data-for-reporting-services-mobile-reports"></a>Vorbereiten von Excel-Daten für mobile Berichte von Reporting Services
  
Es gibt Einiges zu bedenken, wenn Sie eine Excel-Datei und Arbeitsblätter für die Verwendung mit einem mobilen Bericht vorbereiten :  
  
## <a name="do"></a>Sie sollten  
  
- ein Arbeitsblatt pro Dataset verwenden.  
- einen Spaltenkopf in der ersten Zeilen einrichten.  
- die Datentypen in jeder Spalte konsistent halten.  
- die Zellen in Excel im richtigen Datentyp formatieren.  
- die Daten in Arbeitsblättern ablegen, nicht im Datenmodell in Excel.  
- sicherstellen, dass die gesamte Spalte mit der gleichen Formel berechnet wird, wenn Sie Formeln verwenden.  
- Excel 2007 oder höher verwenden.  
- Excel-Dateien mit der Erweiterung XLSX speichern.  
          
## <a name="dont"></a>Sie sollten auf keinen Fall  
  
- Bilder, Diagramme, PivotTables oder andere eingebettete Objekte in Dataset-Arbeitsblättern verwenden.  
- berechnete Zeilen oder Ergebniszeilen verwenden.  
- die Datei während des Imports in Excel geöffnet lassen.  
- Zahlen manuell formatieren, indem Sie Währungen oder andere Symbole hinzufügen.  
- eine Arbeitsmappe mit Daten aus dem Datenmodell verwenden.  
  
## <a name="worksheets"></a>Arbeitsblätter  
          
Wenn Sie eine Excel-Datei als Dataset für einen mobilen Bericht vorbereiten, sollten Sie sicherstellen, dass Sie nur ein Dataset pro Arbeitsblatt verwenden. Jedes einzelne Arbeitsblatt wird als einzelne Tabelle in [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] importiert. Gleichnamige Arbeitsblätter aus mehreren Excel-Quellen werden beim Importieren durch Anfügen von aufsteigenden Zahlen umbenannt. Wenn eine Arbeitsmappe beispielsweise drei Arbeitsblätter namens „MyWorksheet“ enthält, werden das zweite und dritte in „MyWorksheet0“ und „MyWorksheet1“ umbenannt. Der folgende Screenshot zeigt die ersten Zeilen eines idealen Excel-Arbeitsblatts, das für den Import bereit ist.  
  
![SS_MRP_ExcelDataSheet](../../reporting-services/mobile-reports/media/ss-mrp-exceldatasheet.png)  
          
## <a name="column-headers"></a>Spaltenköpfe  
  
Wie im obigen Beispiel zu sehen ist, enthält die erste Zeile den Namen der Metrik dieser Spalte. [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] behält diese Spaltenköpfe als einfachen Verweis in den Einstellungen des Katalogelements bei. Spaltenköpfe sind jedoch nicht erforderlich. Falls diese fehlen, generiert [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] Überschriften mithilfe der Excel-Konvention A, B, C,..., AA, BB...  
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]erkennt automatisch Kopfzeilen, wenn Excel-Arbeitsmappen importiert werden, indem die Datentypen für die ersten beiden Zellen in jeder Spalte miteinander verglichen werden. Wenn die Datentypen der ersten beiden Zellen in einer beliebigen Spalte nicht übereinstimmen, wird bestimmt, dass die erste Zeile Spaltenüberschriften enthalten soll. Wenn eine Tabelle also numerische Spaltenköpfe besitzt, sollten Sie ihnen eine Zeichenfolge voranstellen, sodass diese als Spaltenüberschriften beim Importvorgang erkannt werden.  
  
## <a name="cells"></a>Zellen  
  
Die Zellendaten müssen in jeder einzelnen Spalte eines Arbeitsblatt-Datasets übereinstimmen. Jeder Spalte wird beim Importieren ein Datentyp zugewiesen. [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] erkennt Datentypen automatisch als Zeichenfolgen, Double (numerisch), boolesch (TRUE/FALSE) oder datetime. Gemischte Datentypen in der gleichen Spalte können dazu führen, dass diese Erkennung ungenau ist oder vollständig fehlschlägt. Mit dieser Erkennung können mögliche Spaltenüberschriften vom Typ „String“ identifiziert werden. Zellen sollten im richtigen Typ in Excel formatiert werden, um sicherzustellen, dass [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] die gewünschten Typen erkennt. Im obigen Beispiel würden die sechs Spalten wie folgt eingegeben werden:  
*  Eine datetime-Spalte  
*  Eine Zeichenfolgenspalte  
*  Vier Double-Spalten  
  
Wenn ein Arbeitsblatt berechnete Zellen oder Formeln enthält, wird nur der resultierende Anzeigewert in [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]importiert.  
  
## <a name="file-location-and-refreshing-excel-data"></a>Dateispeicherort und Aktualisieren von Excel-Daten  
  
Es gibt keine Einschränkungen, wo Sie Excel-Dateien speichern können, die Sie in [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]importieren. Wenn Sie die Datei jedoch nach dem Importieren verschieben oder umbenennen, können Sie die Daten nicht über den Befehl **Alle Daten aktualisieren** in der Datenansicht aktualisieren.   
  
>**Hinweis:**: [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] aktualisiert Excel-Daten nicht automatisch. Sie können die Daten aktualisieren, indem Sie den [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] **refresh** command, but only if the file hasn't moved.  
  
## <a name="dates"></a>Datumsangaben  
  
Datumsfelder sind für viele mobile Berichte unerlässlich, weswegen Sie sicherstellen sollten, dass die Excel-Zellen ordnungsgemäß als Datumsangaben formatiert sind. In einigen Fällen macht dies eine Konvertierung notwendig. Es folgen einige Beispiele für Formeln, mit denen Excel-Zellen von Text in Datumsangaben konvertiert werden können.  
  
    Week 24-2013=DATE(MID(A2,9,4),1,-2)-WEEKDAY(DATE(MID(A2,9,4),1,3))+MID(A2,6,2)*7  
  
    2013/03/21=DATEVALUE(A1)  
  
    2013-mar-12=DATEVALUE(RIGHT(A1,2)&"-"&MID(A1,6,3)&"-"&LEFT(A1,4))  
  
Nachdem Sie die Zellen konvertiert haben, müssen Sie sie als Datumsangaben formatieren, indem Sie sie oder die gesamte Spalte auswählen > **Kontext**menü > **Zellen formatieren** > **Datum** aus der Liste **Kategorie**. Sie können ebenfalls den Textkonvertierungs-Assistenten von Excel verwenden, um Textzellen in ordnungsgemäß formatierte Datumsangaben zu konvertieren.  
  
## <a name="unsupported"></a>Nicht unterstützt  
  
Arbeitsblattdaten können beim Importieren unvorhersehbare Ergebnisse hervorrufen, wenn sie in einem anderen Format als den oben genannten gespeichert werden. Es ist ratsam, die Arbeitsblätter in einer Excel-Datei auf diejenigen Arbeitsblätter zu begrenzen, die das richtige Format für die Verwendung mit einem mobilen Bericht aufweisen.  
  
Benutzerdefinierte Objekte in Excel-Arbeitsblättern, einschließlich PivotTables, Visualisierungen und Bilder, werden nicht in [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]importiert.  
  
### <a name="see-also"></a>Siehe auch  
- [Vorbereiten von Daten für mobile Berichte von Reporting Services](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)  
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (Erstellen und Veröffentlichen von mobilen Berichten mit dem Publisher für mobile Berichte von SQL Server)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  Anzeigen von [mobilen SQL Server-Berichten und KPIs in der iPad-App](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI für iOS)  
-  Anzeigen von [mobilen SQL Server-Berichten und KPIs in der iPhone-App](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-iphone-kpis-mobile-reports) (Power BI für iOS)  
  
  
  
  
  
  
  


