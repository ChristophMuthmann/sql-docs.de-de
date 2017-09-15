---
title: "Markieren von Geschäftsobjekten als sicher für Skripting | Microsoft Docs"
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
- business objects in RDS [ADO]
ms.assetid: 0be98d1a-ab3d-4dce-a166-dacda10d154a
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 05a2131b594d20c4215a2c52422d930c0ac2edfb
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="marking-business-objects-as-safe-for-scripting"></a>Markieren von Geschäftsobjekten als sicher für Skripting
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Um eine sichere Internet-Umgebung zu gewährleisten, müssen Sie Geschäftsobjekte instanziiert mit kennzeichnen die [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) des Objekts [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) Methode als "sicher für Skripting". Sie müssen sicherstellen, dass sie als solche gekennzeichnet werden der Registrierung im Bereich "Lizenz" erst in DCOM verwendet werden können.  
  
> [!NOTE]
>  Als "sicher für Skripting" oder für die Initialisierung gekennzeichnet Geschäftsobjekte können instanziiert und initialisiert, indem jede Person über das Netzwerk. Markieren ein Geschäftsobjekt "sicher für Skripting" ist nicht sicher erleichtern. Es ist äußerst wichtig, um sicherzustellen, dass Geschäftsobjekte codiert sind, mit der höchsten Sicherheit, um sicherzustellen, dass diese Objekte keinen ungeschützten Zugriffspunkt für vertrauliche Daten darstellen.  
  
 Wenn Sie um das Geschäftsobjekt als sicher für Skripting manuell zu kennzeichnen, erstellen Sie eine Textdatei mit der Erweiterung REG, die den folgenden Text enthält. In diesem Beispiel \< *MyActiveXGUID*> ist die GUID-Hexadezimalzahl Ihres Business-Objekts. Die folgenden beiden Zahlen Aktivieren der sicher für Skripting-Funktion:  
  
```  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95801-9882-11CF-9FA9-00AA006C42C4}]  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95802-9882-11CF-9FA9-00AA006C42C4}]  
```  
  
 Speichern Sie die Datei, und führen sie in der Registrierung durch Verwendung des Registrierungs-Editors oder durch Doppelklicken auf die REG-Datei in Windows-Explorer.  
  
 Geschäftsobjekte erstellt in Microsoft Visual Basic können mit dem Paket und die Bereitstellungs-Assistent automatisch als "sicher für Skripting" markiert. Wenn Sie angeben, die Sicherheitseinstellungen des Assistenten gefragt werden, wählen Sie **sicher für die Initialisierung** und **sicher für Skripting**.  
  
 Im letzten Schritt erstellt die Anwendung-Setup-Assistenten eine htm- und eine CAB-Datei. Sie können diese beiden Dateien auf den Zielcomputer kopieren und doppelklicken Sie auf die HTM-Datei, um die Seite laden und registrieren Sie den Server richtig.  
  
 Da das Geschäftsobjekt standardmäßig im Verzeichnis Windows\System32\Occache installiert werden, verschieben Sie es in das Verzeichnis "Windows\System32", und ändern Sie die **HKEY_CLASSES_ROOT\CLSID\\ ** \< *MyActiveXGUID*>\\**InprocServer32** Registrierungsschlüssel auf den richtigen Pfad entsprechen.



