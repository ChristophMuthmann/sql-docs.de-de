---
title: Benutzerdefinierte Workflow-XML-Beschreibung (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: e267e5f4-38bb-466d-82e8-871eabeec07e
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ca6f208bab4ed0b7932d3bd5f7e9a911b8b2c8af
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-custom-workflow---xml-description"></a>Erstellen Sie einen benutzerdefinierten Workflow - XML-Beschreibung
  In [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] wird die <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A>-Methode beim Start eines Workflows vom SQL Server MDS Workflow Integration Service aufgerufen. Diese Methode empfängt Metadaten und Daten zum Element, das die Workflowgeschäftsregel als XML-Block ausgelöst hat. Code, der einen workflowhandler implementiert beispielsweise finden Sie unter [Beispiel für einen benutzerdefinierten Workflow &#40; Master Data Services &#41; ](../../master-data-services/develop/create-a-custom-workflow-example.md).  
  
 Das folgende Beispiel zeigt eine mögliche Darstellung der XML, die an den Workflowhandler gesendet wird:  
  
```scr  
<ExternalAction>  
  <Type>TEST</Type>  
  <SendData>1</SendData>  
  <Server_URL>This is my test!</Server_URL>  
  <Action_ID>Test Workflow</Action_ID>  
  <Model_ID>5</Model_ID>  
  <Model_Name>Customer</Model_Name>  
  <Entity_ID>34</Entity_ID>  
  <Entity_Name>Customer</Entity_Name>  
  <Version_ID>8</Version_ID>  
  <MemberType_ID>1</MemberType_ID>  
  <Member_ID>12</Member_ID>  
  <MemberData>  
    <ID>12</ID>  
    <Version_ID>8</Version_ID>  
    <ValidationStatus_ID>3</ValidationStatus_ID>  
    <ChangeTrackingMask>0</ChangeTrackingMask>  
    <EnterDTM>2011-02-25T20:16:36.650</EnterDTM>  
    <EnterUserID>2</EnterUserID>  
    <EnterUserName>MyUserName</EnterUserName>  
    <EnterUserMuid>EEF91D48-B673-4D83-B95F-5A363C11DE91</EnterUserMuid>  
    <EnterVersionId>8</EnterVersionId>  
    <EnterVersionName>VERSION_1</EnterVersionName>  
    <EnterVersionMuid>52B788C2-2750-4651-9DB0-2CB05A88AA5A</EnterVersionMuid>  
    <LastChgDTM>2011-02-25T20:16:36.650</LastChgDTM>  
    <LastChgUserID>2</LastChgUserID>  
    <LastChgUserName>MyUserName</LastChgUserName>  
    <LastChgUserMuid>EEF91D48-B673-4D83-B95F-5A363C11DE91</LastChgUserMuid>  
    <LastChgVersionId>8</LastChgVersionId>  
    <LastChgVersionName>VERSION_1</LastChgVersionName>  
    <LastChgVersionMuid>52B788C2-2750-4651-9DB0-2CB05A88AA5A</LastChgVersionMuid>  
    <Name>Test Customer</Name>  
    <Code>TC</Code>  
  </MemberData>  
</ExternalAction>  
```  
  
 In der folgenden Tabelle werden einige der Tags beschrieben, die in dieser XML enthalten sind:  
  
|Tag|Description|  
|---------|-----------------|  
|\<Typ >|Der Text, die Sie eingegeben, in haben der **Workflowtyp** in das Textfeld [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] zum Identifizieren der benutzerdefinierten Workflowassembly zu laden.|  
|\<SendData >|Ein boolescher Wert, der gesteuert wird, indem Sie die **Elementdaten in die Nachricht einfügen** CheckBox-Element im [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]. Der Wert 1 bedeutet, dass die \<MemberData > Abschnitt gesendet wird; andernfalls die \<MemberData > Abschnitt wird nicht gesendet.|  
|< Server_URL >|Der Text, die Sie eingegeben, in haben der **workflowsite** in das Textfeld [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].|  
|< Action_ID >|Der Text, die Sie eingegeben, in haben der **Workflowname** in das Textfeld [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].|  
|\<MemberData >|Enthält die Daten des Elements, das die Workflowaktion ausgelöst hat. Dies liegt vor, wenn nur der Wert des \<SendData > 1 ist.|  
|\<Geben Sie*Xxx*>|Dieser Tagsatz enthält Metadaten zur Erstellung des Elements, beispielsweise den Zeitpunkt der Erstellung und den Ersteller.|  
|\<LastChg*Xxx*>|Dieser Tagsatz enthält Metadaten zur letzten Änderung des Elements, beispielsweise den Zeitpunkt und Autor.|  
|\<Name >|Das erste Attribut des Elements, das geändert wurde. Dieses Beispielelement enthält nur Namens- und Codeattribute.|  
|\<Code >|Das nächste Attribut des Elements, das geändert wurde. Enthielt dieses Beispielelement mehr Attribute, würden sie diesem nachfolgen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie einen benutzerdefinierten Workflow &#40; Master Data Services &#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)   
 [Beispiel für einen benutzerdefinierten Workflow &#40; Master Data Services &#41;](../../master-data-services/develop/create-a-custom-workflow-example.md)  
  
  
