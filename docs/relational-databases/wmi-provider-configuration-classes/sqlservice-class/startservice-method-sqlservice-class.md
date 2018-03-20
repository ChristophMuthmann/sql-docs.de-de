---
title: StartService-Methode (SqlService-Klasse) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- StartService Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- StartService method
ms.assetid: 83dfb6bd-dbd5-45d8-aad2-a11926317f91
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 38db686217dbc016105dec20a75b477a0f7225a6
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/19/2018
---
# <a name="startservice-method-sqlservice-class"></a>StartService-Methode (SqlService-Klasse)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Versucht, den Dienst zu starten.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.StartService()  
```  
  
## <a name="parts"></a>Bestandteile  
 *Objekt*  
 Ein [SqlService-Klassenobjekt](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) , das den Dienst darstellt.  
  
## <a name="property-valuereturn-value"></a>Eigenschaftswert/Rückgabewert  
 Ein uint32-Wert, der den einen der folgenden Startstatus angibt:  
  
 0  
 Erfolg. Die Anforderung wurde akzeptiert.  
  
 1  
 Nicht unterstützt. Die Anforderung wird nicht unterstützt.  
  
 2  
 Zugriff verweigert. Der Benutzer hatte keinen entsprechenden Zugriff.  
  
 3  
 Abhängige Dienste werden ausgeführt. Der Dienst kann nicht beendet werden, da andere ausgeführte Dienste davon abhängig sind.  
  
 4  
 Ungültige Dienstkontrolle. Der angeforderte Steuerungscode ist nicht gültig, oder es ist für den Dienst nicht akzeptabel.  
  
 5  
 Die Steuerung kann vom Dienst nicht angenommen werden. Der angeforderte Steuerungscode kann nicht an den Dienst gesendet werden, weil der Status des Diensts (Win32_BaseService:State) 0, 1 oder 2 lautet.  
  
 6  
 Der Dienst ist nicht aktiv. Der Dienst wurde nicht gestartet.  
  
 7  
 Timeout bei der Dienstanforderung. Der Dienst hat auf die Startanforderung nicht rechtzeitig reagiert.  
  
 8  
 Unbekannter Fehler. Beim Starten des Diensts ist ein unbekannter Fehler aufgetreten.  
  
 9  
 Der Pfad wurde nicht gefunden. Der Verzeichnispfad zur ausführbaren Dienstdatei wurde nicht gefunden.  
  
 10  
 Der Dienst wird bereits ausgeführt. Der Dienst wird schon ausgeführt.  
  
 11  
 Die Dienstdatenbank ist gesperrt. Die Datenbank zum Hinzufügen eines neuen Diensts ist gesperrt.  
  
 12  
 Die Dienstabhängigkeit wurde gelöscht. Eine Abhängigkeit, von der dieser Dienst abhängt, wurde aus dem System entfernt.  
  
 13  
 Dienstabhängigkeitenfehler. Der Dienst hat den Dienst nicht gefunden, der von einem abhängigen Dienst benötigt wird.  
  
 14  
 Der Dienst ist deaktiviert. Der Dienst wurde vom System deaktiviert.  
  
 15  
 Fehler bei der Dienstanmeldung. Der Dienst hat nicht die richtige Authentifizierung, um im System ausgeführt zu werden.  
  
 16  
 Der Dienst ist zum Löschen markiert. Der Dienst wird aus dem System entfernt.  
  
 17  
 Der Dienst besitzt keinen Thread. Es gibt keinen Ausführungsthread für den Dienst.  
  
 18  
 Ringabhängigkeitsstatus. Es gibt Ringabhängigkeiten beim Starten des Diensts.  
  
 19  
 Doppelter Name. Es wird ein Dienst unter dem gleichen Namen ausgeführt.  
  
 20  
 Ungültiger Name. Im Namen des Dienstes sind ungültige Zeichen vorhanden.  
  
 21  
 Ungültige Parameter. Ungültige Parameter wurden an den Dienst übergeben.  
  
 22  
 Ungültiges Dienstkonto. Das Konto, unter dem dieser Dienst ausgeführt werden soll, ist nicht gültigt oder verfügt nicht über die Berechtigung zum Ausführen des Diensts.  
  
 23  
 Der Dienst ist bereits vorhanden. Der Dienst ist in der Datenbank der im System verfügbaren Dienste vorhanden.  
  
 24  
 Der Dienst wurde bereits angehalten. Der Dienst ist im System derzeitig angehalten.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="see-also"></a>Siehe auch  
 [Starten und Beenden von Diensten](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
