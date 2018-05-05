---
title: 'Schritt 1: Konfigurieren von Pyodbc Python-Entwicklungsumgebung | Microsoft Docs'
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: python
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: beb0c34f5645615a69944088163ad157d59d3c3a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>Schritt 1: Konfigurieren der Entwicklungsumgebung für Pyodbc Python-Entwicklung

## <a name="windows"></a>Windows  
Herstellen einer Verbindung mit SQL-Datenbank mithilfe von Python - Pyodbc unter Windows:
  
1. **Herunterladen von Python-installer**  
  Wenn Ihr Computer nicht installieren Sie Python verfügt. Wechseln Sie die [Python-Downloadseite](https://www.python.org/downloads/windows/) und das entsprechende Installationsprogramm herunterzuladen. Für das Beispiel auf einem 64-Bit-Computer herunterladen Installationsprogramm Python 2.7 oder 3.5 (x 64).  
  
2. **Installieren Sie Python** sobald das Installationsprogramm heruntergeladen wurde, gehen Sie folgendermaßen vor: ein. Doppelklicken Sie auf die Datei, um das Installationsprogramm zu starten. B. Wählen Sie Ihre Sprache aus, und akzeptieren. c. Befolgen Sie die Anweisungen auf dem Bildschirm und Python sollte auf dem Computer installiert werden. d. Sie können also überprüfen Python installiert gehen Sie auf C:\Python27 oder C:\Python35 und Python - V oder Py - V (für 3.x) ausgeführt wird 
      
3. [**Installieren Sie den Microsoft ODBC-Treiber**](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)
  
4. **Öffnen Sie als Administrator cmd.exe**     

5. **Installieren Sie Pyodbc Verwendung von Pip - Python-Paket-manager**
```  
> cd C:\Python27\Scripts>  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
Herstellen einer Verbindung mit SQL-Datenbank mithilfe von Python - Pyodbc auf Ubuntu und RedHat:
  
1. **Geöffneten Terminaldienste**  

2. **Installieren Sie Microsoft ODBC Driver 13 für Linux** für Ubuntu 15.04 + 
``` 
> sudo su  
> wget https://gallery.technet.microsoft.com/ODBC-Driver-13-for-Ubuntu-b87369f0/file/154097/2/installodbc.sh  
> sh installodbc.sh  
```   

  Für RedHat 6 7 
``` 
> sudo su 
> wget https://gallery.technet.microsoft.com/ODBC-Driver-13-for-SQL-8d067754/file/153653/4/install.sh 
> sh install.sh 
```  
  
3.  **Installieren von pyodbc**  
```  
> sudo -H pip install pyodbc
```
