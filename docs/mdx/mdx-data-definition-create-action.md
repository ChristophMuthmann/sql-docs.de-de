---
title: CREATE ACTION-Anweisung (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE ACTION
- Action
- CREATE
- CREATE_ACTION
dev_langs: kbMDX
helpviewer_keywords:
- invocation types [MDX]
- dimensions [Analysis Services], actions
- CREATE ACTION statement
- cubes [Analysis Services], actions
- actions [MDX]
- hierarchies [Analysis Services], actions
ms.assetid: 0419f349-ece2-42ba-8552-a1023f268a41
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7b2ba808abe506ddf10078e7f8dd4ae0f693c1b6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mdx-data-definition---create-action"></a>MDX-Datendefinition - Aktion zu erstellen
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt eine Aktion, die einem Cube, einer Dimension, einer Hierarchie oder einem untergeordneten Objekt zugeordnet werden kann.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE ACTION CURRENTCUBE | Cube_Name  
   .Action_Name <action body>  
<action body> ::=   
FOR   
        CUBE   
    | Hierarchy_Name [MEMBERS]   
    | Level_Name [MEMBERS]   
    | CELLS   
    | SET }   
      AS 'MDX_Expression'   
        [, TYPE = '  
              { URL   
            | HTML   
            | STATEMENT   
               | DATASET   
            | ROWSET   
            | COMMANDLINE   
               | PROPRIETARY }   
         ']  
   [ , INVOCATION = 'INTERACTIVE | ON_OPEN | BATCH ' ]  
   [ , APPLICATION = String_Expression ]  
   [ , DESCRIPTION = String_Expression ]  
   [ , CAPTION = 'MDX_Expression' ]  
```  
  
## <a name="arguments"></a>Argumente  
 *Cube_Name*  
 Eine gültige Zeichenfolge, die einen Cubenamen bereitstellt.  
  
 *Action_ Name*  
 Eine gültige Zeichenfolge, die den Namen der zu erstellenden Aktion bereitstellt.  
  
 *Hierarchy_ Name*  
 Eine gültige Zeichenfolge, die einen Hierarchienamen bereitstellt.  
  
 *Level_ Name*  
 Eine gültige Zeichenfolge, die einen Ebenennamen bereitstellt.  
  
 *Member_ Name*  
 Eine gültige Zeichenfolge, die einen Elementnamen oder Elementschlüssel bereitstellt.  
  
 *MDX_Expression*  
 Ein gültiger MDX-Ausdruck.  
  
 *String_Expression*  
 Ein gültiger Zeichenfolgenausdruck.  
  
## <a name="remarks"></a>Hinweise  
 Es ist möglich, dass Clientanwendungen unsichere Aktionen erstellen und ausführen oder unsichere Funktionen verwenden. Um diese Situationen zu vermeiden, verwenden die **Safety Options** Eigenschaft. Weitere Informationen finden Sie im Abschnitt zur Safety Options-Eigenschaft.  
  
> [!NOTE]  
>  Diese Anweisung wird nur aus Gründen der Abwärtskompatibilität bereitgestellt. Aktionen, die noch nicht mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], z. B. Drillthrough- oder berichtsaktionen, werden nicht unterstützt.  
  
## <a name="action-types"></a>Aktionstypen  
 Die folgende Tabelle beschreibt die verschiedenen Typen von verfügbaren Aktionen im [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
|Aktionstyp|Description|  
|-----------------|-----------------|  
|**URL**|Die zurückgegebene Aktionszeichenfolge ist eine URL, die mit einem Internetbrowser geöffnet werden sollte.<br /><br /> Hinweis: Wenn diese Aktion nicht mit beginnt `http://` oder `https://`, die Aktion wird an den Browser nicht verfügbar sein, es sei denn, **SafetyOptions** festgelegt ist, um **DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL**.|  
|**HTML**|Die zurückgegebene Aktionszeichenfolge ist ein HTML-Skript. Die Zeichenfolge sollte in einer Datei gespeichert werden, und die Datei sollte mit einem Internetbrowser gerendert werden. In diesem Fall kann ein ganzes Skript als Teil des generierten HTML-Codes ausgeführt werden.|  
|**ANWEISUNG**|Die zurückgegebene Aktionszeichenfolge ist eine Anweisung, durch Festlegen von auszuführenden muss, die **ICommand::SetText** -Methode eines Befehlsobjekts auf die Zeichenfolge und das Aufrufen der **ICommand:: Execute**Methode. Wenn der Befehl nicht erfolgreich ausgeführt werden kann, wird ein Fehler zurückgegeben.|  
|**DATASET**|Die zurückgegebene Aktionszeichenfolge ist eine MDX-Anweisung, die für die Ausführung durch die Einstellung muss der **ICommand::SetText** -Methode eines Befehlsobjekts auf die Zeichenfolge und das Aufrufen der **ICommand:: Execute** Methode. Die angeforderte Schnittstelle ID (IID) sollte **IDataset**. Der Befehl ist erfolgreich, wenn ein Dataset erstellt wurde. Die Clientanwendung sollte dem Benutzer das Durchsuchen des zurückgegebenen Datasets ermöglichen.|  
|**ROWSET**|Ähnlich wie **DATASET**, aber statt der IID anzufordern **IDataset**, sollte die Clientanwendung IID bitten **IRowset**. Der Befehl ist erfolgreich, wenn ein Rowset erstellt wurde. Die Clientanwendung sollte dem Benutzer das Durchsuchen des zurückgegebenen Rowsets ermöglichen.|  
|**BEFEHLSZEILE**|Die Clientanwendung sollte die Aktionszeichenfolge ausführen. Die Zeichenfolge stellt eine Befehlszeile dar.|  
|**PROPRIETÄRE**|Eine Clientanwendung sollte die Aktion nicht anzeigen oder ausführen, wenn sie nicht über benutzerdefiniertes, nicht generisches Wissen über die bestimmte Aktion verfügt. Proprietäre Aktionen werden nicht an die Clientanwendung zurückgegeben, es sei denn, die Clientanwendung für diese, indem Sie auf die entsprechende Einschränkung explizit fordert die **APPLICATION_NAME**.|  
  
## <a name="invocation-types"></a>Aufruftypen  
 In der folgenden Tabelle sind die verschiedenen Typen von Aufrufen beschrieben, die in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] zur Verfügung stehen. Der Aufruftyp wird nur von der Clientanwendung verwendet, um zu bestimmen, wann die Aktion aufgerufen werden soll. Das Aufrufverhalten der Aktion selbst wird nicht durch den Aufruftyp bestimmt.  
  
|Aufruftyp|Description|  
|---------------------|-----------------|  
|**INTERAKTIVE**|Die Aktion sollte von der Clientanwendung durch Benutzerinteraktion aufgerufen werden.|  
|**ON_OPEN**|Die Aktion sollte von der Clientanwendung aufgerufen werden, wenn das Zielobjekt geöffnet wird. Dieser Aufruftyp ist zurzeit nicht implementiert.|  
|**BATCH**|Die Aktion sollte von der Clientanwendung aufgerufen werden, wenn das Zielobjekt an einem von der Clientanwendung bestimmten Batchvorgang beteiligt ist. Dieser Aufruftyp ist zurzeit nicht implementiert.|  
  
### <a name="scope"></a>Scope  
 Jede Aktion ist für einen bestimmten Cube definiert und besitzt einen eindeutigen Namen innerhalb des Cubes. Eine Aktion kann für einen der Bereiche in der folgenden Tabelle gelten.  
  
 Cubebereich  
 Die Aktion ist unabhängig von bestimmten Dimensionen, Elementen oder Zellen. Beispiel: "Launch terminal emulation for AS/400 production system".  
  
 Dimensionsbereich  
 Die Aktion gilt für eine bestimmte Dimension. Diese Aktionen sind nicht von einer bestimmten Auswahl von Ebenen oder Elementen abhängig.  
  
 Ebenenbereich  
 Die Aktion gilt für eine bestimmte Dimensionsebene. Diese Aktionen sind nicht von einer bestimmten Auswahl eines Elements in dieser Dimension abhängig.  
  
 Memberbereich  
 Die Aktion gilt für bestimmte Ebenenelemente.  
  
 Zellenbereich  
 Die Aktion gilt nur für bestimmte Zellen.  
  
 Mengenbereich  
 Die Aktion gilt nur für eine Menge. Der Name **ActionParameterSet**, ist für die Verwendung durch die Anwendung innerhalb des Ausdrucks der Aktion reserviert.  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Datendefinitionsanweisungen &#40; MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
