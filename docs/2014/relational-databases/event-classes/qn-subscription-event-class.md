---
title: QN:Subscription (Ereignisklasse) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- event classes [SQL Server], QN:Subscription
ms.assetid: 4916167e-8541-43b4-900e-ec8e6adcbc34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7d60680f4c6f286db1c1d0e47961e75b057b14a9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2018
ms.locfileid: "48192100"
---
# <a name="qnsubscription-event-class"></a>QN:Subscription (Ereignisklasse)
  Das QN:Subscription-Ereignis übermittelt Informationen über Benachrichtigungsabonnements.  
  
## <a name="qnsubscription-event-class-data-columns"></a>Datenspalten der QN:Subscription-Ereignisklasse  
  
|Datenspalte|Typ|Description|Spaltennummer|Filterbar|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|`nvarchar`|Der Name der Clientanwendung, die die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|10|Benutzerkontensteuerung|  
|ClientProcessID|`int`|Die ID, die der Hostcomputer dem Prozess zuweist, in dem die Clientanwendung ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn die Clientprozess-ID durch den Client bereitgestellt wird.|9|Benutzerkontensteuerung|  
|DatabaseID|`int`|Die ID der Datenbank, die durch die USE *database* -Anweisung angegeben wurde, bzw. die ID der Standarddatenbank, wenn für eine bestimmte Instanz keine USE *database*-Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die Server Name-Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|Benutzerkontensteuerung|  
|DatabaseName|`nvarchar`|Der Name der Datenbank, in der die Benutzeranweisung ausgeführt wird.|35|Benutzerkontensteuerung|  
|EventClass|`int`|Ereignistyp = 199.|27|nein|  
|EventSequence|`int`|Die Sequenznummer für dieses Ereignis.|51|nein|  
|EventSubClass|`nvarchar`|Der Typ der Ereignisunterklasse, der weitere Informationen zu jeder Ereignisklasse liefert. Diese Spalte kann die folgenden Werte enthalten:<br /><br /> Abonnement registriert: Gibt an, wann das Abfragebenachrichtigungsabonnement erfolgreich in der Datenbank registriert wird.<br /><br /> Abonnement zurückgespult: Gibt an, wann die [!INCLUDE[ssDE](../../includes/ssde-md.md)] empfängt eine Anforderung, die mit ein vorhandenes Abonnement übereinstimmt. In diesem Fall legt [!INCLUDE[ssDE](../../includes/ssde-md.md)] für den Timeoutwert des vorhandenen Abonnements den in der neuen Abonnementanforderung festgelegten Timeoutwert fest.<br /><br /> Abonnement wurde ausgelöst: Gibt an, wann ein Benachrichtigungsabonnement eine benachrichtigungsmeldung erzeugt.<br /><br /> Broker-Fehler bei der Auslösung: Gibt an, wann eine benachrichtigungsmeldung aufgrund von schlägt fehl, einen [!INCLUDE[ssSB](../../includes/sssb-md.md)] Fehler.<br /><br /> Fehler bei der Auslösung ohne Broker-Fehler: Gibt an, wenn eine Meldung ein Fehler auftritt, aber keine [!INCLUDE[ssSB](../../includes/sssb-md.md)] Fehler.<br /><br /> Broker-Fehler abgefangen: Gibt an, dass [!INCLUDE[ssSB](../../includes/sssb-md.md)] in der von die abfragebenachrichtigung verwendeten Konversation einen Fehler übermittelt.<br /><br /> Abonnement löschversuchs: Gibt an, dass die [!INCLUDE[ssDE](../../includes/ssde-md.md)] hat versucht, das Löschen eines abgelaufenen Abonnement, um Ressourcen freizugeben.<br /><br /> Fehler beim Löschen des Abonnements: Gibt an, dass der Versuch, ein abgelaufenes Abonnement gelöscht hat. Die Löschung des Abonnements wird in [!INCLUDE[ssDE](../../includes/ssde-md.md)] automatisch erneut geplant, um Ressourcen frei zu geben.<br /><br /> Abonnement zerstört: Gibt an, dass die [!INCLUDE[ssDE](../../includes/ssde-md.md)] ein abgelaufenes Abonnement wurde erfolgreich gelöscht.|21|Benutzerkontensteuerung|  
|GroupID|`int`|ID der Arbeitsauslastungsgruppe, in der das SQL-Ablaufverfolgungsereignis ausgelöst wird.|66|Benutzerkontensteuerung|  
|HostName|`nvarchar`|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname durch den Client bereitgestellt wird. Der Hostname kann mithilfe der HOST_NAME-Funktion bestimmt werden.|8|Benutzerkontensteuerung|  
|IsSystem|`int`|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist.<br /><br /> 0 = Benutzer<br /><br /> 1 = System|60|nein|  
|LoginName|`nvarchar`|Der Anmeldename des Benutzers (Anmeldung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherheit oder Windows-Anmeldeinformationen im Format DOMAIN\Username).|11|nein|  
|LoginSID|`image`|Die Sicherheits-ID (SID, Security Identification Number) des angemeldeten Benutzers. Diese Informationen finden Sie in der sys.server_principals-Katalogsicht. Die SID ist für jede Anmeldung beim Server eindeutig.|41|Benutzerkontensteuerung|  
|NTDomainName|`nvarchar`|Die Windows-Domäne, der der Benutzer angehört.|7|Benutzerkontensteuerung|  
|NTUserName|`nvarchar`|Der Name des Benutzers, der Besitzer der Verbindung ist, die dieses Ereignis generiert hat.|6|Benutzerkontensteuerung|  
|RequestID|`int`|Der Bezeichner der Anforderung, die die Anweisung enthält.|49|Benutzerkontensteuerung|  
|ServerName|`nvarchar`|Der Name der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , für die eine Ablaufverfolgung ausgeführt wird.|26|nein|  
|SessionLoginName|`nvarchar`|Der Anmeldename des Benutzers, der die Sitzung geöffnet hat. Wenn beispielsweise eine Anwendung mithilfe von Login1 eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellt und eine Anweisung als Login2 ausführt, zeigt SessionLoginName "Login1" an, und LoginName zeigt "Login2" an. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|Benutzerkontensteuerung|  
|SPID|`int`|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|Benutzerkontensteuerung|  
|StartTime|`datetime`|Zeitpunkt, zu dem das Ereignis begonnen hat (falls vorhanden).|14|Benutzerkontensteuerung|  
|TextData|`ntext`|Gibt ein XML-Dokument mit spezifischen Informationen zu diesem Ereignis zurück. Dieses Dokument stimmt mit dem XML-Schema überein, das auf der Seite [SQL Server Query Notification Profiler Event Schema](http://go.microsoft.com/fwlink/?LinkId=63331) (in englischer Sprache) zur Verfügung gestellt wird.|1|Benutzerkontensteuerung|  
  
  
