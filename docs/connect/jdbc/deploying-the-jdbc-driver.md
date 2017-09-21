---
title: Bereitstellen des JDBC-Treibers | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3ad3508d-d9b1-47fb-a63b-21cdc3ed44e0
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 24e796670985c803b1a6f8a067ed6e8a548379e9
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="deploying-the-jdbc-driver"></a>Bereitstellen des JDBC-Treibers
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Bei der Bereitstellung einer Anwendung, von denen abhängt der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], müssen Sie den JDBC-Treiber zusammen mit der Anwendung verteilen. Im Gegensatz zu Windows Data Access Components (Windows DAC), die eine Komponente des Windows-Betriebssystems ist, gilt der JDBC-Treiber um eine Komponente von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
 Es gibt zwei Möglichkeiten, um den JDBC-Treiber mit der Anwendung bereitzustellen. Eine Möglichkeit besteht darin, die JDBC-Treiberdateien in ein eigenes benutzerdefiniertes Installationspaket aufzunehmen. Der zweite Ansatz umfasst die Verwendung der JDBC-Installationspaket von Microsoft, das Sie herunterladen können die [Microsoft JDBC Driver für SQL Server Developer Center](http://go.microsoft.com/fwlink/?LinkId=70166).  
  
 In den folgenden Abschnitten wird beschrieben, wie das JDBC-Installationspaket unter Windows- und UNIX-Betriebssystemen verwendet wird.  
  
> [!NOTE]  
>  Allgemeine Informationen zur Bereitstellung von Java-Anwendungen finden Sie auf der Java-Website.  
  
## <a name="deploying-the-jdbc-driver-on-windows-systems"></a>Bereitstellen des JDBC-Treibers auf Windows-Systemen  
 Wenn Sie den JDBC-Treiber auf Windows-Betriebssystemen bereitstellen, müssen Sie die ausführbare Zip-Dateiversion des Installationspakets, das normalerweise heißt verwenden `sqljdbc_<version>_<language>.exe`.  
  
 Wenn die ausführbare Zip-Datei automatisch ausgeführt werden, müssen Sie verwenden die `/auto` Befehlszeilenoption in der Befehlszeile oder in einer Batchdatei wie folgt:  
  
 `sqljdbc_<version>_<language>.exe /auto`  
  
> [!NOTE]  
>  Bei Verwendung der `/auto` Option, es ist nicht tatsächlich Hintergrundinstallation, wie ein WinZip-Dialogfeld auf dem Bildschirm des Benutzers angezeigt wird. Es sind jedoch keine Benutzereingaben erforderlich, da das Dialogfeld nach Abschluss der Dekomprimierung automatisch geschlossen wird.  
  
## <a name="deploying-the-driver-on-unix-systems"></a>Bereitstellen des JDBC-Treibers auf UNIX-Systemen  
 Wenn Sie den JDBC-Treiber auf UNIX-Betriebssystemen bereitstellen, müssen Sie die Gzip-Dateiversion des Installationspakets, das normalerweise heißt verwenden `sqljdbc_<version>_<language>.tar.gz`.  
  
 Vor der Installation des JDBC-Treibers müssen ggf. die Dienstprogramme "gzip" und "tar" auf dem System des Benutzers installiert und die Ordner mit den ausführbaren Dateien für die Dienstprogramme zur Umgebungsvariablen PATH hinzugefügt werden.  
  
 Navigieren Sie zum Entpacken der komprimierten TAR-Datei zu dem Verzeichnis, in das der Treiber entpackt werden soll, und geben Sie den folgenden Befehl ein:  
  
 `gzip -d sqljdbc_<version>_<language>.tar.gz`  
  
 Verschieben Sie die TAR-Datei zum Entpacken zu dem Verzeichnis, in dem der Treiber installiert werden soll, und geben Sie den folgenden Befehl ein:  
  
 `tar –xf sqljdbc_<version>_<language>.tar`  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über die JDBC-Treiber](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  