---
title: Erweitern einer Fehlerausgabe mit der Skriptkomponente | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: extending-packages-scripting-data-flow-script-component-examples
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 46530444f96d995cd7c53a12378a737b2b36fcf4
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="enhancing-an-error-output-with-the-script-component"></a>Erweitern einer Fehlerausgabe mit der Skriptkomponente
  Standardmäßig enthalten die beiden zusätzlichen Spalten in einer [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Fehlerausgabe – ErrorCode und ErrorColumn – nur numerische Codes, die eine Fehlernummer darstellen, und die ID der Spalte, in der der Fehler auftrat. Diese numerischen Werte sind ohne die entsprechende Fehlerbeschreibung und den Spaltennamen nur von begrenztem Nutzen.  
  
 In diesem Thema wird beschrieben, wie Sie mithilfe der Skriptkomponente den im Datenfluss vorhandenen Fehlerausgabedaten die Fehlerbeschreibung und den Spaltennamen hinzufügen. Im Beispiel wird die Fehlerbeschreibung einem bestimmten vordefinierten [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Fehlercode hinzugefügt. Dazu wird die <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>-Schnittstelle verwendet, die von der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A>-Eigenschaft der Skriptkomponente bereitgestellt wird. Dann wird im Beispiel mithilfe der <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130.GetIdentificationStringByID%2A>-Methode derselben Schnittstelle der Spaltenname hinzugefügt, der der erfassten Herkunfts-ID entspricht.  
  
> [!NOTE]  
>  Wenn Sie eine Komponente erstellen möchten, die Sie einfacher in mehreren Datenflusstasks und Paketen wiederverwenden können, empfiehlt es sich, den Code in diesem Skriptkomponentenbeispiel als Ausgangspunkt für eine benutzerdefinierte Datenflusskomponente zu verwenden. Weitere Informationen finden Sie unter [Entwickeln einer benutzerdefinierten Datenflusskomponente](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel wird gezeigt, wie mit einer Skriptkomponente, die als Transformation konfiguriert ist, den im Datenfluss vorhandenen Fehlerausgabedaten die Fehlerbeschreibung und der Spaltenname hinzugefügt werden.  
  
 Weitere Informationen zum Konfigurieren der Skriptkomponente für die Verwendung als Transformation im Datenfluss finden Sie unter [Erstellen einer synchronen Transformation mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md) und [Creating an Asynchronous Transformation with the Script Component](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md) (Erstellen einer asynchronen Transformation mit der Skriptkomponente).  
  
#### <a name="to-configure-this-script-component-example"></a>So konfigurieren Sie dieses Skriptkomponentenbeispiel  
  
1.  Konfigurieren Sie vor dem Erstellen der neuen Skriptkomponente eine Upstreamkomponente im Datenfluss, um Zeilen zur zugehörigen Fehlerausgabe umzuleiten, sobald ein Fehler auftritt oder Daten abgeschnitten werden. Möglicherweise möchten Sie zu Testzwecken eine Komponente so konfigurieren, dass auf jeden Fall Fehler auftreten – beispielsweise, indem Sie eine Transformation zum Suchen zwischen zwei Tabellen konfigurieren, und die Suche einen Fehler meldet.  
  
2.  Fügen Sie der Datenfluss-Designeroberfläche eine neue Skriptkomponente hinzu, und konfigurieren Sie sie als Transformation.  
  
3.  Verbinden Sie die Fehlerausgabe der Upstreamkomponente mit der neuen Skriptkomponente.  
  
4.  Öffnen Sie den **Transformations-Editor für Skripterstellung**, und wählen Sie auf der Seite **Skript** für die **ScriptLanguage**-Eigenschaft die Skriptsprache aus.  
  
5.  Klicken Sie auf **Skript bearbeiten**, um die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications-IDE (VSTA) zu öffnen und den unten dargestellten Beispielcode einzufügen.  
  
6.  Schließen Sie VSTA.  
  
7.  Wählen Sie im Transformations-Editor für Skripterstellung auf der Seite **Eingabespalten** die Spalten ErrorCode und ErrorColumn aus.  
  
8.  Fügen Sie auf der Seite **Eingaben und Ausgaben** zwei neue Spalten hinzu.  
  
    -   Fügen Sie eine neue Ausgabespalte des Typs **Zeichenfolge** mit dem Namen **ErrorDescription** hinzu. Vergrößern Sie die Standardlänge der neuen Spalte auf 255, damit auch lange Meldungen angezeigt werden können.  
  
    -   Fügen Sie eine weitere neue Ausgabespalte des Typs **Zeichenfolge** mit dem Namen **ColumnName** hinzu. Vergrößern Sie die Standardlänge der neuen Spalte auf 255, damit auch lange Werte angezeigt werden können.  
  
9. Schließen Sie den **Transformations-Editor für Skripterstellung**.  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md)   
 [Verwenden von Fehlerausgaben in einer Datenflusskomponente](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [Erstellen einer synchronen Transformation mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
  
  
