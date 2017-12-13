---
title: Behandeln von Fehlern und Warnungen (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- errors [XML for Analysis]
- inline errors [XMLA]
- SOAP faults [XML for Analysis]
- XML for Analysis, errors
- faults [XML for Analysis]
- messages [XML for Analysis]
- XMLA, errors
- warnings [XML for Analysis]
- inline warnings [XMLA]
ms.assetid: ab895282-098d-468e-9460-032598961f45
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 04170950534e6cb0020edb371ea265478fe73b97
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="handling-errors-and-warnings-xmla"></a>Behandeln von Fehlern und Warnungen (XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Fehlerbehandlung ist notwendig, wenn XML for Analysis (XMLA) [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) oder [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) Methodenaufruf wird nicht ausgeführt, wird erfolgreich ausgeführt, aber Fehler oder Warnungen generiert oder wird erfolgreich ausgeführt, aber gibt Ergebnisse zurück die Fehler enthalten.  
  
|Fehler|Bericht|  
|-----------|---------------|  
|Der XMLA-Methodenaufruf wird nicht ausgeführt|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gibt eine SOAP-Fehlernachricht mit den Details des Fehlers.<br /><br /> Weitere Informationen finden Sie im Abschnitt [Behandeln von SOAP-Fehlern](#handling_soap_faults).|  
|Fehler oder Warnungen bei erfolgreichem Methodenaufruf|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]enthält eine [Fehler](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md) oder [Warnung](../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md) -Element für jeden Fehler oder jede Warnung bzw. in die [Nachrichten](../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md) Eigenschaft von der [Root](../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) Element, das die Ergebnisse des Methodenaufrufs enthält.<br /><br /> Weitere Informationen finden Sie im Abschnitt [Behandeln von Fehlern und Warnungen](#handling_errors_and_warnings).|  
|Fehler im Ergebnis bei erfolgreichem Methodenaufruf|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]enthält ein Inline- **Fehler** oder **Warnung** Element foder the erroder oder Warning, jeweils in die entsprechende [Zelle](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md) oder [Zeile](../../analysis-services/xmla/xml-elements-properties/row-element-xmla.md) ein Element der Ergebnisse des Methodenaufrufs.<br /><br /> Weitere Informationen finden Sie im Abschnitt [Behandeln von Inlinefehlern und -warnungen](#handling_inline_errors_and_warnings).|  
  
##  <a name="handling_soap_faults"></a>Behandeln von SOAP-Fehlern  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Gibt einen SOAP-Fehler zurück, wenn die folgenden Situationen auftreten:  
  
-   Die SOAP-Nachricht, die die XMLA-Methode enthält, ist nicht wohlgeformt oder konnte nicht überprüft werden, indem die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Instanz.  
  
-   Eine Kommunikations- oder anderer Fehler ist in Bezug auf die SOAP-Nachricht, die die XMLA-Methode enthält, aufgetreten.  
  
-   Die XMLA-Methode wurde nicht auf der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz ausgeführt.  
  
 Die SOAP-Fehlercodes für XMLstartA beginnen mit „XMLForAnalysis“ gefolgt von einem Punkt und dem hexadezimalen HRESULT-Ergebniscode. Beispielsweise wird ein Fehlercode von „`0x80000005`“ formatiert als „`XMLForAnalysis.0x80000005`“. Weitere Informationen über das SOAP-Fehlerformat finden Sie unter „Soap Fault in the W3C Simple Object Access Protocol (SOAP) 1.1“.  
  
### <a name="fault-code-information"></a>Fehlercodeinformationen  
 Die folgende Tabelle zeigt die XMLA-Fehlercodeinformationen, die im Detailabschnitt der SOAP-Antwort enthalten sind. Die Spalten sind die Attribute eines Fehlers im Detailabschnitt eines SOAP-Fehlers.  
  
|Spaltenname|Typ|Description|Null zulässig<sup>1</sup>|  
|-----------------|----------|-----------------|------------------------------|  
|**ErrorCode**|**UnsignedInt**|Rückgabecode, der den Erfolg oder das Scheitern der Methode angibt. Der Hexadezimalwert muss in einen **UnsignedInt** -Wert konvertiert werden.|Nein|  
|**WarningCode**|**UnsignedInt**|Rückgabecode, der eine Warnbedingung angibt. Der Hexadezimalwert muss in einen **UnsignedInt** -Wert konvertiert werden.|ja|  
|**Description**|**String**|Fehler- oder Warnungstext und Beschreibung, die durch die Komponente zurückgegeben werden, die den Fehler erzeugt hat.|ja|  
|**Quelle**|**String**|Name der Komponente, die den Fehler oder die Warnung generiert hat.|ja|  
|**HelpFile**|**String**|Pfad oder URL zur Hilfedatei oder dem Thema, das den Fehler oder die Warnung beschreibt.|ja|  
  
 <sup>1</sup> gibt an, ob die Daten ist erforderlich und müssen zurückgegeben werden, oder gibt an, ob die Daten optional sind und eine null-Zeichenfolge ist zulässig, wenn die Spalte nicht anwendbar ist.  
  
 Im Folgenden finden Sie ein Beispiel für einen SOAP-Fehler, der auftrat, als ein Methodenaufruf fehlschlug:  
  
```  
<?xml version="1.0"?>  
   <SOAP-ENV:Envelope  
   xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"  
   SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">  
      <SOAP-ENV:Fault>  
         <faultcode>XMLAnalysisError.0x80000005</faultcode>  
         <faultstring>The XML for Analysis provider encountered an error.</faultstring>  
         <faultactor>XML for Analysis Provider</faultactor>  
         <detail>  
<Error  
ErrorCode="2147483653"  
Description="An unexpected error has occurred."  
Source="XML for Analysis Provider"  
HelpFile="" />  
         </detail>  
      </SOAP-ENV:Fault>  
</SOAP-ENV:Envelope>  
```  
  
##  <a name="handling_errors_and_warnings"></a>Behandeln von Fehlern und Warnungen  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Gibt die **Nachrichten** Eigenschaft in der **Root** Element foder a Command if nach Ausführung des Befehls die folgenden Situationen auftreten:  
  
-   Die Methode selber schlug nicht fehl, aber ein Fehler aufgetreten ist, auf die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz nach erfolgreicher des Methodenaufrufs Ausführung.  
  
-   Die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz gibt eine Warnung zurück, wenn der Befehl erfolgreich ist.  
  
 Die **Messages** -Eigenschaft folgt allen Eigenschaften, die im **root** -Element enthalten sind, und kann ein oder mehr **Message** -Elemente enthalten. Jedes **Message** -Element kann entweder ein einzelnes **error** - oder ein **warning** -Element enthalten, das entweder Fehler oder Warnungen beschreibt, die beim angegebenen Befehl aufgetreten sind.  
  
 Weitere Informationen zu Fehlern und Warnungen, die in enthaltenen der **Nachrichten** Eigenschaft finden Sie unter [Messages-Element &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md).  
  
### <a name="handling-errors-during-serialization"></a>Behandeln von Fehlern während der Serialisierung  
 Wenn ein Fehler, nachdem auftritt die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Instanz wurde bereits gestartet Serialisierung der Ausgabe eines erfolgreich ausgeführten Befehls [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gibt eine [Ausnahme](../../analysis-services/xmla/xml-elements-properties/exception-element-xmla.md) Element in einem anderen Namespace zum Zeitpunkt des Fehlers. Die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz schließt dann alle geöffneten Elemente, damit die an den Client gesendete XML-Dokument gültig ist. Die Instanz gibt darüber hinaus ein **Messages** -Element zurück, das eine Beschreibung des Fehlers enthält.  
  
##  <a name="handling_inline_errors_and_warnings"></a>Behandeln von Inlinefehlern und-Warnungen  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Gibt ein Inlineschema zurück **Fehler** oder **Warnung** für einen Befehl aus, wenn der XMLA-Methode selber schlug nicht fehl, jedoch spezifisch für ein Datenelement in den Ergebnissen, die von der Methode zurückgegebenen in Fehler der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz, nachdem der XMLA-Methodenaufruf war erfolgreich.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Gibt Inline- **Fehler** und **Warnung** -Elemente an, wenn Probleme im Zusammenhang mit einer Zelle oder anderen Daten, die sich als Bestandteil einer **Stamm** Element mit der [ MDDataSet](../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) Datentyp auftreten, z. B. Sicherheits- oder Formatierungsfehler einer Zelle. In diesen Fällen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gibt eine **Fehler** oder **Warnung** Element in der **Zelle** oder **Zeile** Element, das den Fehler enthält oder "Warnung" und jeweils.  
  
 Das folgende Beispiel veranschaulicht ein Resultset, das einen Fehler im zurückgegebenen Rowset enthält eine **Execute** -Methode der [Anweisung](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md) Befehl.  
  
```  
<return>  
   ...  
   <root>  
      ...  
      <CellData>  
      ...  
         <Cell CellOrdinal="10">  
            <Value>  
               <Error>  
                  <ErrorCode>2148497527</ErrorCode>   
                  <Description>Security Error.</Description>   
               </Error>  
            </Value>  
         </Cell>  
      </CellData>  
      ...  
   </root>  
   ...  
</return>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Entwickeln mit XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
