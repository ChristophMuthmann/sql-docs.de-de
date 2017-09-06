---
title: Erstellen ein benutzerdefiniertes Element-Laufzeitkomponente | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom report items, creating
ms.assetid: b3e15a4a-98f8-4dbb-b847-bbcb20327051
caps.latest.revision: 33
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: c8da0d4ac6024281315dc2e8b0b398904c8a1e6c
ms.contentlocale: de-de
ms.lasthandoff: 08/12/2017

---
# <a name="creating-a-custom-report-item-run-time-component"></a>Erstellen einer Laufzeitkomponente für ein benutzerdefiniertes Berichtselement
  Die Laufzeitkomponente Element einer benutzerdefinierten Bericht wird als implementiert eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Komponente, die mit einer beliebigen CLS-kompatiblen Sprache und vom Berichtsprozessor zur Laufzeit aufgerufen wird. Sie definieren die Eigenschaften für die Laufzeitkomponente in der Entwurfsumgebung, indem Sie die entsprechende Entwurfszeitkomponente für ein benutzerdefiniertes Berichtselement ändern.  
  
 Ein Beispiel für ein vollständig implementiertes benutzerdefiniertes Berichtselement finden Sie unter [SQL Server Reporting Services-Produktbeispiele](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="definition-and-instance-objects"></a>Definitions- and Instanzobjekte  
 Vor der Implementierung eines benutzerdefinierten Berichtselements ist es wichtig zu verstehen, den Unterschied zwischen *definitionsobjekten* und *Instanzobjekte*. Definitionsobjekte stellen die RDL-Darstellung des benutzerdefinierten Berichtselements bereit, wohingegen es sich bei Instanzobjekten um die bewerteten Versionen von Definitionsobjekten handelt. Für jedes Element des Berichts gibt es nur ein Definitionsobjekt. Beim Zugreifen auf Eigenschaften auf einem Definitionsobjekt, die Ausdrücke enthalten, erhalten Sie die nicht bewertete Ausdruckszeichenfolge. Instanzobjekte enthalten die bewerteten Versionen der Definitionsobjekte und können in einer 1:n-Beziehung mit dem Definitionsobjekt eines Elements stehen. Wenn beispielsweise ein Bericht einen <xref:Microsoft.ReportingServices.OnDemandReportRendering.Tablix>-Datenbereich besitzt, der ein <xref:Microsoft.ReportingServices.OnDemandReportRendering.CustomReportItem> in einer Detailzeile enthält, ist nur ein einziges Definitionsobjekt vorhanden, es gibt jedoch für jede Zeile im Datenbereich eine Instanz.  
  
## <a name="implementing-the-icustomreportitem-interface"></a>Implementieren der ICustomReportItem-Schnittstelle  
 Zum Erstellen einer **CustomReportItem** Laufzeitkomponente, die Sie implementieren müssen die <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem> -Schnittstelle, die in der Datei Microsoft.ReportingServices.ProcessingCore.dll definiert ist:  
  
```csharp  
namespace Microsoft.ReportingServices.OnDemandReportRendering  
{  
    public interface ICustomReportItem  
    {  
        void GenerateReportItemDefinition(CustomReportItem customReportItem);  
void EvaluateReportItemInstance(CustomReportItem customReportItem);  
    }  
}  
```  
  
 Nachdem die <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem>-Schnittstelle implementiert ist, werden zwei Methodenstubs generiert: <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem.GenerateReportItemDefinition%2A> und <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem.EvaluateReportItemInstance%2A>. Die <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem.GenerateReportItemDefinition%2A>-Methode wird zuerst aufgerufen. Sie wird zum Festlegen der Definitionseigenschaften and zum Erstellen des <xref:Microsoft.ReportingServices.OnDemandReportRendering.Image>-Objekts verwendet, das sowohl die zum Rendern des Elements verwendeten Definitions- und die Instanzeigenschaften enthält. Nachdem die Definitionsobjekte bewertet wurden, wird die <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem.EvaluateReportItemInstance%2A>-Methode aufgerufen. Sie stellt die Instanzobjekte zum Rendern des Elements bereit.  
  
 Im Folgenden sehen Sie eine Beispielimplementierung eines benutzerdefinierten Berichtselements, das den Namen der Steuerung als Bild rendert.  
  
```csharp  
namespace Microsoft.Samples.ReportingServices  
{  
    using System;  
    using System.Collections.Generic;  
    using System.Collections.Specialized;  
    using System.Drawing.Imaging;  
    using System.IO;  
    using System.Text;  
    using Microsoft.ReportingServices.OnDemandReportRendering;  
  
    public class PolygonsCustomReportItem : ICustomReportItem  
    {  
        #region ICustomReportItem Members  
  
        public void GenerateReportItemDefinition(CustomReportItem cri)  
        {  
            // Create the Image object that will be   
            // used to render the custom report item  
            cri.CreateCriImageDefinition();  
            Image polygonImage = (Image)cri.GeneratedReportItem;  
        }  
  
        public void EvaluateReportItemInstance(CustomReportItem cri)  
        {  
            // Get the Image definition  
            Image polygonImage = (Image)cri.GeneratedReportItem;  
  
            // Create the image for the custom report item  
            polygonImage.ImageInstance.ImageData = DrawImage(cri);  
        }  
  
        #endregion  
  
        /// <summary>  
        /// Creates an image of the CustomReportItem's name  
        /// </summary>  
        private byte[] DrawImage(CustomReportItem customReportItem)  
        {  
            int width = 1;          // pixels  
            int height = 1;         // pixels  
            int resolution = 75;    // dpi  
  
            System.Drawing.Bitmap bitmap = new System.Drawing.Bitmap(width, height);  
            bitmap.SetResolution(resolution, resolution);  
  
            System.Drawing.Graphics graphics = System.Drawing.Graphics.FromImage(bitmap);  
            graphics.PageUnit = System.Drawing.GraphicsUnit.Pixel;  
  
            // Get the Font for the Text  
            System.Drawing.Font font = new System.Drawing.Font(System.Drawing.FontFamily.GenericMonospace,  
                12, System.Drawing.FontStyle.Regular);  
  
            // Get the Brush for drawing the Text  
            System.Drawing.Brush brush = new System.Drawing.SolidBrush(System.Drawing.Color.LightGreen);  
  
            // Get the measurements for the image  
            System.Drawing.SizeF maxStringSize = graphics.MeasureString(customReportItem.Name, font);  
            width = (int)(maxStringSize.Width + 2 * font.GetHeight(resolution));  
            height = (int)(maxStringSize.Height + 2 * font.GetHeight(resolution));  
  
            bitmap.Dispose();  
            bitmap = new System.Drawing.Bitmap(width, height);  
            bitmap.SetResolution(resolution, resolution);  
  
            graphics.Dispose();  
            graphics = System.Drawing.Graphics.FromImage(bitmap);  
            graphics.PageUnit = System.Drawing.GraphicsUnit.Pixel;  
  
            // Draw the text  
            graphics.DrawString(customReportItem.Name, font, brush, font.GetHeight(resolution),   
                font.GetHeight(resolution));  
  
            // Create the byte array of the image data  
            MemoryStream memoryStream = new MemoryStream();  
            bitmap.Save(memoryStream, ImageFormat.Bmp);  
            memoryStream.Position = 0;  
            byte[] imageData = new byte[memoryStream.Length];  
            memoryStream.Read(imageData, 0, imageData.Length);  
  
            return imageData;  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Benutzerdefiniertes Element-Architektur](../../reporting-services/custom-report-items/custom-report-item-architecture.md)   
 [Erstellen einer benutzerdefinierten Bericht Element zur Entwurfszeit-Komponente](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)   
 [Klassenbibliotheken für benutzerdefinierten Berichts-Element](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)   
 [Vorgehensweise: Bereitstellen eines benutzerdefinierten Berichtselements](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
  
