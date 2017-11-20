---
title: Erweitern einer Fehlerausgabe with the Script Component | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting-data-flow-script-component-examples
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- transformations [Integration Services], components
- Script component [Integration Services], examples
- error outputs [Integration Services], enhancing
- Script component [Integration Services], transformation components
ms.assetid: f7c02709-f1fa-4ebd-b255-dc8b81feeaa5
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 3881b57f4089dbb075d019f9bd1a88a96a307b72
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="enhancing-an-error-output-with-the-script-component"></a>Erweitern einer Fehlerausgabe mit der Skriptkomponente
  Standardmäßig werden die beiden zusätzlichen Spalten in einer [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Fehlerausgabe, ErrorCode und ErrorColumn, enthalten nur numerische Codes darstellen, die eine Fehlernummer und die ID der Spalte, in dem der Fehler aufgetreten ist. Diese numerischen Werte möglicherweise nur von begrenztem Nutzen, ohne die entsprechende fehlerbeschreibung und den Spaltennamen.  
  
 In diesem Thema wird beschrieben, wie die fehlerbeschreibung und den Namen der Spalte im Datenfluss vorhandenen fehlerausgabedaten hinzufügen, indem Sie mithilfe der Skriptkomponente. Im Beispiel wird die Fehlerbeschreibung einem bestimmten vordefinierten [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Fehlercode hinzugefügt. Dazu wird die <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>-Schnittstelle verwendet, die von der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A>-Eigenschaft der Skriptkomponente bereitgestellt wird. Im Beispiel fügt den Namen der Spalte entspricht der erfassten Herkunfts-ID mithilfe der <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130.GetIdentificationStringByID%2A> Methode derselben Schnittstelle.  
  
> [!NOTE]  
>  Wenn Sie eine Komponente erstellen möchten, die Sie einfacher in mehreren Datenflusstasks und Paketen wiederverwenden können, empfiehlt es sich, den Code in diesem Skriptkomponentenbeispiel als Ausgangspunkt für eine benutzerdefinierte Datenflusskomponente zu verwenden. Weitere Informationen finden Sie unter [Entwickeln einer benutzerdefinierten Datenflusskomponente](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="example"></a>Beispiel  
 Das hier dargestellte Beispiel verwendet eine Skriptkomponente als Transformation konfiguriert, um die fehlerbeschreibung und den Namen der Spalte im Datenfluss vorhandenen fehlerausgabedaten hinzufügen.  
  
 Weitere Informationen zum Konfigurieren von für die Verwendung der Skriptkomponente als Transformation im Datenfluss finden Sie unter [Erstellen einer synchronen Transformation mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md) und [Erstellen einer asynchronen Transformation mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md).  
  
#### <a name="to-configure-this-script-component-example"></a>So konfigurieren Sie dieses Skriptkomponentenbeispiel  
  
1.  Konfigurieren Sie vor dem Erstellen der neuen Skriptkomponente eine Upstreamkomponente im Datenfluss, um Zeilen zur zugehörigen Fehlerausgabe umzuleiten, sobald ein Fehler auftritt oder Daten abgeschnitten werden. Möglicherweise möchten Sie zu Testzwecken eine Komponente so konfigurieren, dass auf jeden Fall Fehler auftreten – beispielsweise, indem Sie eine Transformation zum Suchen zwischen zwei Tabellen konfigurieren, und die Suche einen Fehler meldet.  
  
2.  Fügen Sie der Datenfluss-Designeroberfläche eine neue Skriptkomponente hinzu, und konfigurieren Sie sie als Transformation.  
  
3.  Verbinden Sie die Fehlerausgabe der Upstreamkomponente mit der neuen Skriptkomponente.  
  
4.  Öffnen der **Skript Transformations-Editor**, und klicken Sie auf die **Skript** Seite für die **ScriptLanguage** -Eigenschaft, wählen Sie die Skriptsprache.  
  
5.  Klicken Sie auf **Bearbeitungsskript** So öffnen die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE, und fügen Sie den unten dargestellten Beispielcode hinzu.  
  
6.  Schließen Sie VSTA.  
  
7.  Das Skript Transformations-Editor auf die **Eingabespalten** Seite, wählen Sie die ErrorCode und ErrorColumn-Spalten.  
  
8.  Auf der **Eingaben und Ausgaben** Seite, fügen Sie zwei neue Spalten hinzu.  
  
    -   Fügen Sie eine neue Ausgabespalte des Typs **Zeichenfolge** mit dem Namen **ErrorDescription**. Vergrößern Sie die Standardlänge der neuen Spalte auf 255, damit auch lange Meldungen angezeigt werden können.  
  
    -   Fügen Sie eine andere neue Ausgabespalte des Typs **Zeichenfolge** mit dem Namen **ColumnName**. Erhöhen Sie die standardmäßige Länge der neuen Spalte auf 255, damit lange Werte unterstützen.  
  
9. Schließen der **Skript Transformations-Editor.**  
  
10. Fügen Sie die Ausgabe der Skriptkomponente an ein geeignetes Ziel an. Ein Flatfileziel ist die einfachste Möglichkeit zur Konfiguration bei Ad-hoc-Tests.  
  
11. Führen Sie das Paket aus.  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
      Row.ErrorDescription = _  
        Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
      Dim componentMetaData130 = TryCast(Me.ComponentMetaData, IDTSComponentMetaData130)  
      If componentMetaData130 IsNot Nothing Then  
        Row.ColumnName = componentMetaData130.GetIdentificationStringByID(Row.ErrorColumn)  
         End If  
  
    End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
{  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
  
      Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
  
      var componentMetaData130 = this.ComponentMetaData as IDTSComponentMetaData130;  
      if (componentMetaData130 != null)  
        {  
            Row.ColumnName = componentMetaData130.GetIdentificationStringByID(Row.ErrorColumn);  
        }  
  
    }  
}  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md)   
 [Verwenden von Fehlerausgaben in einer Datenflusskomponente](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [Erstellen einer synchronen Transformation mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
  
  

