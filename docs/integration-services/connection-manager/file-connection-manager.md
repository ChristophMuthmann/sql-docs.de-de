---
title: Dateiverbindungs-Manager | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- folders [Integration Services], connections
- files [Integration Services], connections
- files [Integration Services]
- connection managers [Integration Services], File
- connections [Integration Services], files
- File connection manager
ms.assetid: 019078bc-44ee-4975-9169-0f9a89e3f3be
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9737d90041d9916bf4a1fae892391d2255cc55ab
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="file-connection-manager"></a>Dateiverbindungs-Manager
  Mit einem Dateiverbindungs-Manager kann ein Paket auf eine vorhandene Datei oder einen vorhandenen Ordner verweisen bzw. eine Datei oder einen Ordner zur Laufzeit erstellen. Beispielsweise können Sie auf eine Excel-Datei verweisen. Zur Ausführung bestimmter Komponenten in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] werden in Dateien enthaltene Informationen verwendet. Beispielsweise kann ein Task SQL ausführen auf eine Datei verweisen, die die SQL-Anweisungen enthält, die vom Task ausgeführt werden. Mit anderen Komponenten werden Vorgänge für Dateien ausgeführt. Mit dem Task Dateisystem kann beispielsweise auf eine Datei verwiesen werden, die an einen neuen Ort kopiert werden soll.  
  
## <a name="usage-types-of-the-file-connection-manager"></a>Verwendungstypen des Dateiverbindungs-Managers  
 Mit der **FileUsageType** -Eigenschaft des Dateiverbindungs-Managers wird angegeben, wie die Dateiverbindung verwendet wird. Der Dateiverbindungs-Manager kann eine Datei bzw. einen Ordner erstellen und eine vorhandene Datei bzw. einen vorhandenen Ordner verwenden.  
  
 In der folgenden Tabelle sind die Werte von **FileUsageType**aufgeführt.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**0**|Der Dateiverbindungs-Manager verwendet eine vorhandene Datei.|  
|**1**|Der Dateiverbindungs-Manager erstellt eine Datei.|  
|**2**|Der Dateiverbindungs-Manager verwendet einen vorhandenen Ordner.|  
|**3**|Der Dateiverbindungs-Manager erstellt einen Ordner.|  
  
## <a name="multiple-file-or-folder-connections"></a>Mehrere Datei- oder Ordnerverbindungen  
 Der Dateiverbindungs-Manager kann nur auf eine einzige Datei oder einen einzigen Ordner verweisen. Wenn Sie auf mehrere Dateien oder Ordner verweisen möchten, verwenden Sie anstelle eines Dateiverbindungs-Managers einen Verbindungs-Manager für mehrere Dateien. Weitere Informationen finden Sie unter [Multiple Files Connection Manager](../../integration-services/connection-manager/multiple-files-connection-manager.md).  
  
## <a name="configuration-of-the-file-connection-manager"></a>Konfiguration des Verbindungs-Managers für Dateien  
 Wenn Sie einem Paket einen Dateiverbindungs-Manager hinzufügen, erstellt [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] einen Verbindungs-Manager, der zur Laufzeit in eine Dateiverbindung aufgelöst wird, die Eigenschaften der Dateiverbindung festlegt und der **Connections** -Sammlung des Pakets die Dateiverbindung hinzufügt.  
  
 Die **ConnectionManagerType** -Eigenschaft des Verbindungs-Managers ist auf **FILE**festgelegt.  
  
 Es gibt folgende Möglichkeiten, um einen Dateiverbindungs-Manager zu konfigurieren:  
  
-   Geben Sie den Verwendungstyp an.  
  
-   Geben Sie eine Datei oder einen Ordner an.  
  
 Sie können die ConnectionString-Eigenschaft für den Dateiverbindungs-Manager festlegen, indem Sie einen Ausdruck im Eigenschaftenfenster von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]angeben. Fügen Sie jedoch im **Dateiverbindungs-Manager-Editor**für **Datei/Ordner**einen Pfad für eine Datei oder einen Ordner hinzu, um Überprüfungsfehler zu vermeiden, wenn Sie die Datei oder den Ordner mit einem Ausdruck angeben.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können, finden Sie unter [Dateiverbindungs-Manager-Editor](../../integration-services/connection-manager/file-connection-manager-editor.md).  
  
 Weitere Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> und unter [Programmgesteuertes Hinzufügen von Verbindungen](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)aufgeführt.  
  
  
