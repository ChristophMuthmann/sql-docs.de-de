---
title: "Breakpoints festlegen | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.setbreakpoints.f1"
helpviewer_keywords: 
  - "Breakpoints festlegen (Dialogfeld)"
ms.assetid: 876e61b7-875c-43f4-bbce-d7eeb90f6730
caps.latest.revision: 24
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 24
---
# Breakpoints festlegen
  Verwenden Sie das Dialogfeld **Breakpoints festlegen** , um die Ereignisse anzugeben, für die Breakpoints aktiviert werden sollen, sowie um das Verhalten der Breakpoints zu steuern.  
  
## enthalten  
 **Aktiviert**  
 Wählen Sie diese Option aus, um einen Breakpoint für ein Ergebnis zu aktivieren.  
  
 **Unterbrechungsbedingung**  
 Zeigen Sie eine Liste von verfügbaren Ereignissen an, für die Breakpoints festgelegt werden können.  
  
 **Typ der Trefferanzahl**  
 Geben Sie an, wann der Breakpoint wirksam werden soll.  
  
|value|Description|  
|-----------|-----------------|  
|**Always**|Die Ausführung wird immer angehalten, wenn der Breakpoint erreicht wird.|  
|**Trefferanzahl ist gleich**|Die Ausführung wird angehalten, wenn die Anzahl des Auftretens des Breakpoints der Trefferanzahl entspricht.|  
|**Trefferanzahl ist größer als oder gleich**|Die Ausführung wird angehalten, wenn die Anzahl des Auftretens des Breakpoints mindestens so groß wie die Trefferanzahl ist.|  
|**Trefferanzahl mehrfach**|Die Ausführung wird angehalten, wenn ein Mehrfaches der Trefferanzahl erreicht wird. Wenn Sie z. B. diese Option auf 5 festlegen, wird die Ausführung bei jedem fünften Mal angehalten.|  
  
 **Trefferanzahl**  
 Geben Sie die Anzahl der Treffer an, nach denen ein Breakpoint ausgelöst werden soll. Diese Option ist nicht verfügbar, wenn der Breakpoint immer wirksam ist.  
  
## Siehe auch  
 [Debuggen der Ablaufsteuerung](../../integration-services/troubleshooting/debugging-control-flow.md)  
  
  