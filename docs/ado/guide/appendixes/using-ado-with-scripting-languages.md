---
title: Verwenden von ADO mit Skriptsprachen | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripting languages [ADO]
- ADO, scripting languages
ms.assetid: 76fc4d00-0c9f-422b-af5c-af6ed8fb29d8
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a0f909233d29c84e1c64ca19f100fdd1eabf4d61
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-ado-with-scripting-languages"></a>Verwenden von ADO mit Skriptsprachen
Innerhalb einer skriptumgebung können mit ADO Daten über die serverseitigen Skripts verfügbar machen. In diesem Szenario ADO, die zugrunde liegenden OLE DB-Anbieter, die es verwendet, und beliebige andere Komponenten, die erforderlich sind, um auf einen bestimmten Datenspeicher verweisen auf einem Server mit Internetinformationsdienste (Internet Information Services, IIS) installiert sind. ADO ist mithilfe von Active Server Pages (ASP), ist eine Komponente, die in ein Skript, das HTML-Daten, z. B. generieren kann verwiesen wird. Diese HTML-Inhalt kann über HTTP auf einen Webbrowser für den Client übergeben werden. Mithilfe von Skripts können auf der Webseite Aktionen zurück an das serverseitige Skript gestattet aktualisieren, durchsuchen und anzeigen bestimmte Daten gesendet.  
  
 Bevor Sie ein ActiveX-Objekt in einer Webseite verwenden, ist es wichtig zu wissen, ob das Objekt sicher für Skripting. Wenn ein Objekt als "sicher für Skripting" eingestuft wird, bedeutet dies, dass das Steuerelement nicht schädliche Aktionen, auf dem Computer des Benutzers ausführen kann und daher ausgeführt werden, kann ohne die Zustimmung des Benutzers angefordert. In der folgenden Tabelle listet die ADO-Objekte und gibt an, ob sie für die Skripterstellung sicher sind.  
  
|Objekt|Speichern für Skripting?|  
|------------|-------------------------|  
|ADO-Verbindung|ja|  
|ADO-Befehl|Nein|  
|ADO-Parameter|Nein|  
|ADO-Recordset|ja|  
|ADO-Datensatz|ja|  
|ADO-Datenstrom|ja|  
|ADO-Fehler|Nein|  
|ADOX-Katalog|Nein|  
|ADOX CellSet|Nein|  
|RDS DataControl|ja|  
|RDS-Datenspeicher|ja|  
|RDS DataFactory|Nein|  
  
 In der folgenden Tabelle listet die Anbieter, die mit Windows DAC/MDAC enthalten, und gibt an, ob sie für die Skripterstellung sicher sind.  
  
|Anbieter|Speichern für Skripting?|  
|--------------|-------------------------|  
|Form|ja|  
|Beibehalten|ja|  
|Remote|ja|  
|OLE DB-Anbieter für SQLServer (SQLOLEDB)|Nein|  
|OLE DB-Anbieter für ODBC (MSDASQL)|Nein|  
  
## <a name="odbc-data-sources"></a>ODBC-Datenquellen  
 Ein deutlicher Unterschied zwischen Skripts und nicht-scripting ADO-Code ist der ODBC-Datenquelle verwendet. Für nicht-scripting-Anwendungen können Sie in der ODBC-Datenquellen-Administrator eine Benutzer-DSN erstellen. Für Skripts, die unter IIS ausgeführt werden, müssen Sie eine System-DSN erstellen. Andernfalls werden Ihre Skripts die Datenquelle, die Sie erstellt haben, nicht erkannt. Dies gilt für alle Skripts ADO-Anwendung mithilfe der Microsoft OLE DB-Anbieter für ODBC über Microsoft IIS.  
  
## <a name="referencing-the-ado-library"></a>Verweis auf die ADO-Bibliothek  
 Nicht zutreffend mit Skriptsprachen.  
  
## <a name="handling-events"></a>Behandlung von Ereignissen  
 Nicht zutreffend mit Skriptsprachen.  
  
 Die folgenden Themen enthalten weitere Informationen zum Verwenden von ADO mit Skriptsprachen an:  
  
-   [VBScript-ADO-Programmierung](../../../ado/guide/appendixes/vbscript-ado-programming.md)  
  
-   [JScript-ADO-Programmierung](../../../ado/guide/appendixes/jscript-ado-programming.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [Mithilfe von ADO mit Microsoft Visual Basic](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-basic.md)   
 [Verwenden von ADO mit Microsoft Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md)   

