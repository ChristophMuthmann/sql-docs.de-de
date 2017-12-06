---
title: "Erstellen einer Entwurfszeitkomponente für ein benutzerdefiniertes Berichtselement | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: custom-report-items
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: custom report items, creating
ms.assetid: 323fd58a-a462-4c48-b188-77ebc0b4212e
caps.latest.revision: "37"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 746ca3586d58f561278eb25ad9459e6102b8b55a
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="creating-a-custom-report-item-design-time-component"></a>Erstellen einer Entwurfszeitkomponente für ein benutzerdefiniertes Berichtselement
  Die Entwurfszeitkomponente für ein benutzerdefiniertes Berichtselement ist eine Steuerung, die in der Berichts-Designer-Umgebung von Visual Studio verwendet werden kann. Diese Komponente bietet eine aktivierte Entwurfsoberfläche, die Drag und Drop-Vorgänge, Integration in den Eigenschaftenbrowser von [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] und die Möglichkeit zum Bereitstellen von Editoren für benutzerdefinierte Eigenschaften zulassen.  
  
 Mit der Entwurfszeitkomponente für ein benutzerdefiniertes Berichtselement können Benutzer ein benutzerdefiniertes Berichtselement auf einem Bericht in der Entwurfsumgebung positionieren, benutzerdefinierte Dateneigenschaften auf dem benutzerdefinierten Berichtselement festlegen und das benutzerdefinierte Berichtselement anschließend als Teil des Berichtsprojekts speichern.  
  
 Die mit der Entwurfszeitkomponente der Entwicklungsumgebung festgelegten Eigenschaften werden von der Host-Entwurfsumgebung serialisiert und deserialisiert und dann als Elemente in der RDL-Datei (Report Definition Language, Berichtsdefinitionssprache) gespeichert. Wenn der Bericht vom Berichtsprozessor ausgeführt wird, werden die mit der Entwurfszeitkomponente festgelegten Eigenschaften vom Berichtsprozessor an eine Laufzeitkomponente für ein benutzerdefiniertes Berichtselement übergeben, die das benutzerdefinierte Berichtselement rendert und wieder an den Berichtsprozessor zurückgibt.  
  
> [!NOTE]  
>  Die Entwurfszeitkomponente für ein benutzerdefiniertes Berichtselement wird als [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Komponente implementiert. In diesem Dokument werden Implementierungsdetails beschrieben, die für die Entwurfszeitkomponente eines benutzerdefinierten Berichtselements spezifisch sind. Weitere Informationen zum Entwickeln von Komponenten mit [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] finden Sie in der MSDN Library unter [Komponenten in Visual Studio](http://go.microsoft.com/fwlink/?LinkId=116576).  
  
 Ein Beispiel für ein vollständig implementiertes benutzerdefiniertes Berichtselement finden Sie unter [SQL Server Reporting Services-Produktbeispiele](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="implementing-a-design-time-component"></a>Implementieren einer Entwurfszeitkomponente  
 Die Hauptklasse einer Entwurfszeitkomponente für ein benutzerdefiniertes Berichtselement wird von der **Microsoft.ReportDesigner.CustomReportItemDesigner**-Klasse geerbt. Zusätzlich zu den Standardattributen für eine [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Steuerung sollte die Komponentenklasse ein **CustomReportItem**-Attribut definieren. Dieses Attribut muss dem in der Datei reportserver.config festgelegten Namen des benutzerdefinierten Berichtselements entsprechen. Eine Liste der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Attribute finden Sie unter "Attribute" in der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-SDK-Dokumentation.  
  
 Im folgenden Codebeispiel wird gezeigt, wie Attribute auf eine Entwurfszeitsteuerung für ein benutzerdefiniertes Berichtselement angewendet werden:  
  
```csharp  
namespace PolygonsCRI  
{  
    [LocalizedName("Polygons")]  
    [Editor(typeof(CustomEditor), typeof(ComponentEditor))]  
        [ToolboxBitmap(typeof(PolygonsDesigner),"Polygons.ico")]  
        [CustomReportItem("Polygons")]  
  
    public class PolygonsDesigner : CustomReportItemDesigner  
    {  
...  
```  
  
### <a name="initializing-the-component"></a>Initialisieren der Komponente  
 Sie übergeben benutzerspezifische Eigenschaften für ein benutzerdefiniertes Berichtselement mit einer <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData>-Klasse. Die Implementierung der **CustomReportItemDesigner**-Klasse sollte die **InitializeNewComponent**-Methode überschreiben, um eine neue Instanz der <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData>-Klasse Ihrer Komponente zu erstellen und sie auf die Standardwerte festzulegen.  
  
 Im folgenden Codebeispiel wird ein Beispiel dafür gezeigt, wie die Klasse einer Entwurfszeitkomponente für ein benutzerdefiniertes Berichtselement die **CustomReportItemDesigner.InitializeNewComponent**-Methode überschreibt, um die <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData>-Klasse der Komponente zu initialisieren:  
  
```csharp  
public override void InitializeNewComponent()  
        {  
            CustomData = new CustomData();  
            CustomData.DataRowHierarchy = new DataHierarchy();  
  
            // Shape grouping  
            CustomData.DataRowHierarchy.DataMembers.Add(new DataMember());  
            CustomData.DataRowHierarchy.DataMembers[0].Group = new Group();  
            CustomData.DataRowHierarchy.DataMembers[0].Group.Name = Name + "_Shape";  
            CustomData.DataRowHierarchy.DataMembers[0].Group.GroupExpressions.Add(new ReportExpression());  
  
            // Point grouping  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers.Add(new DataMember());  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group = new Group();  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group.Name = Name + "_Point";  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group.GroupExpressions.Add(new ReportExpression());  
  
            // Static column  
            CustomData.DataColumnHierarchy = new DataHierarchy();  
            CustomData.DataColumnHierarchy.DataMembers.Add(new DataMember());  
  
            // Points  
            IList<IList<DataValue>> dataValues = new List<IList<DataValue>>();  
            CustomData.DataRows.Add(dataValues);  
            CustomData.DataRows[0].Add(new List<DataValue>());  
            CustomData.DataRows[0][0].Add(NewDataValue("X", ""));  
            CustomData.DataRows[0][0].Add(NewDataValue("Y", ""));  
        }  
```  
  
### <a name="modifying-component-properties"></a>Ändern von Komponenteneigenschaften  
 Sie können **CustomData**-Eigenschaften auf verschiedene Arten in der Entwurfsumgebung ändern. Mit dem [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]-Eigenschaftenbrowser können Sie jede Eigenschaft ändern, die von der Entwurfszeitkomponente verfügbar gemacht wurde und die mit dem <xref:System.ComponentModel.BrowsableAttribute>-Attribut gekennzeichnet sind. Außerdem können Sie Eigenschaften ändern, indem Sie Elemente auf die Entwurfsoberfläche des benutzerdefinierten Berichtselements ziehen oder mit der rechten Maustaste auf die Steuerung in der Entwurfsumgebung klicken und im Kontextmenü **Eigenschaften** auswählen, um ein benutzerdefiniertes Eigenschaftenfenster aufzurufen.  
  
 Das folgende Codebeispiel zeigt eine **Microsoft.ReportDesigner.CustomReportItemDesigner.CustomData**-Eigenschaft, auf die das <xref:System.ComponentModel.BrowsableAttribute>-Attribut angewendet wurde:  
  
```csharp  
[Browsable(true), Category("Data")]  
public string DataSetName  
{  
      get  
      {  
         return CustomData.DataSetName;  
      }  
      set  
      {  
         CustomData.DataSetName = value;  
      }  
   }  
  
```  
  
 Sie können für Ihre Entwurfszeitkomponente ein Dialogfeld für benutzerdefinierte Eigenschaften bereitstellen. Die Implementierung des Editors für benutzerdefinierte Eigenschaften sollte von der <xref:System.ComponentModel.ComponentEditor>-Klasse erben und eine Instanz eines Dialogfelds erstellen, die für die Bearbeitung der Eigenschaften verwendet werden kann.  
  
 Im folgenden Beispiel wird die Implementierung einer Klasse, die von <xref:System.ComponentModel.ComponentEditor> erbt, und ein Dialogfeld eines Editors für benutzerdefinierte Eigenschaften dargestellt:  
  
```csharp  
internal sealed class CustomEditor : ComponentEditor  
{  
   public override bool EditComponent(  
      ITypeDescriptorContext context, object component)  
    {  
     PolygonsDesigner designer = (PolygonsDesigner)component;  
     PolygonProperties dialog = new PolygonProperties();  
     dialog.m_designerComponent = designer;  
     DialogResult result = dialog.ShowDialog();  
     if (result == DialogResult.OK)  
     {  
        designer.Invalidate();  
        designer.ChangeService().OnComponentChanged(designer, null, null, null);  
        return true;  
     }  
     else  
        return false;  
    }  
}  
```  
  
 Das Dialogfeld des Editors für benutzerdefinierte Eigenschaften kann den Ausdrucks-Editor des Berichts-Designers aufrufen. Im folgenden Beispiel wird der Ausdrucks-Editor aufgerufen, wenn der Benutzer das erste Element im Kombinationsfeld auswählt:  
  
```csharp  
private void EditableCombo_SelectedIndexChanged(object sender,   
    EventArgs e)  
{  
   ComboBox combo = (ComboBox)sender;  
   if (combo.SelectedIndex == 0 && m_launchEditor)  
   {  
      m_launchEditor = false;  
      ExpressionEditor editor = new ExpressionEditor();  
      string newValue;  
      newValue = (string)editor.EditValue(null, m_designerComponent.Site, m_oldComboValue);  
      combo.Items[0] = newValue;  
   }  
}  
  
```  
  
### <a name="using-designer-verbs"></a>Verwenden von Designerverben  
 Ein Designerverb ist ein mit einem Ereignishandler verknüpfter Menübefehl. Sie können Designerverben hinzufügen, die im Kontextmenü einer Komponente angezeigt werden, wenn die Laufzeitsteuerung für ein benutzerdefiniertes Berichtselement in der Entwurfsumgebung verwendet wird. Mit der **Verbs**-Eigenschaft können Sie die Liste der verfügbaren Designerverben von der Laufzeitkomponente zurückgeben.  
  
 Im folgenden Codebeispiel wird gezeigt, wie ein Designerverb und ein Ereignishandler zu <xref:System.ComponentModel.Design.DesignerVerbCollection> hinzugefügt wird, sowie der Ereignishandlercode dargestellt:  
  
```csharp  
public override DesignerVerbCollection Verbs  
{  
    get  
    {  
        if (m_verbs == null)  
        {  
            m_verbs = new DesignerVerbCollection();  
            m_verbs.Add(new DesignerVerb("Proportional Scaling", new EventHandler(OnProportionalScaling)));  
         m_verbs[0].Checked = (GetCustomProperty("poly:Proportional") == bool.TrueString);  
        }  
  
        return m_verbs;  
    }  
}  
  
private void OnProportionalScaling(object sender, EventArgs e)  
{  
   bool proportional = !  
        (GetCustomProperty("poly:Proportional") == bool.TrueString);  
   m_verbs[0].Checked = proportional;  
   SetCustomProperty("poly:Proportional", proportional.ToString());  
   ChangeService().OnComponentChanged(this, null, null, null);  
   Invalidate();  
}  
```  
  
### <a name="using-adornments"></a>Verwenden von Randsteuerelementen  
 Benutzerdefinierte Berichtselementklassen können ebenfalls eine **Microsoft.ReportDesigner.Design.Adornment**-Klasse implementieren. Ein Randsteuerelement ermöglicht es der Steuerung für ein benutzerdefiniertes Berichtselement, Bereiche außerhalb des Hauptrechtecks der Entwurfsoberfläche bereitzustellen. Diese Bereiche behandeln Benutzeroberflächenereignisse wie Mausklicks und Drag und Drop-Vorgänge. Die im [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **Microsoft.ReportDesigner**-Namespace definierte **Adornment**-Klasse ist eine Pass-Through-Implementierung der <xref:System.Windows.Forms.Design.Behavior.Adorner>-Klasse, die in Windows Forms enthalten ist. Eine vollständige Dokumentation zur **Adorner**-Klasse finden Sie unter [Übersicht über den Behavior-Dienst](http://go.microsoft.com/fwlink/?LinkId=116673) in der MSDN Library. Beispielcode, in dem eine **Microsoft.ReportDesigner.Design.Adornment**-Klasse implementiert wird, finden Sie unter [SQL Server Reporting Services-Produktbeispiele](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
 Weitere Informationen zum Programmieren und Verwenden von Windows Forms in [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] finden Sie in diesen Themen in der MSDN Library:  
  
-   Entwurfszeitattribute für Komponenten  
  
-   Komponenten in [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]  
  
-   Exemplarische Vorgehensweise: Erstellen eines Windows Forms-Steuerelements, das Visual Studio-Entwurfszeitfunktionen nutzt  
  
## <a name="see-also"></a>Siehe auch  
 [Custom Report Item Architecture (Architektur des benutzerdefinierten Berichtselements)](../../reporting-services/custom-report-items/custom-report-item-architecture.md)   
 [Erstellen einer Laufzeitkomponente für ein benutzerdefiniertes Berichtselement](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [Custom Report Item Class Libraries (Klassenbibliotheken für ein benutzerdefiniertes Berichtselement)](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)   
 [Vorgehensweise: Bereitstellen eines benutzerdefinierten Berichtselements](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
  
