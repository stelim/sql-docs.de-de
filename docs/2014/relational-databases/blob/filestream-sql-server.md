---
title: FILESTREAM (SQL Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server]
- FILESTREAM [SQL Server], about
- FILESTREAM [SQL Server], overview
ms.assetid: 9a5a8166-bcbe-4680-916c-26276253eafa
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1db3c3efe332eb65504c9476a569ec54b49cc1a9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087240"
---
# <a name="filestream-sql-server"></a>FILESTREAM (SQL Server)
  FILESTREAM ermöglicht es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-basierten Anwendungen, nicht strukturierte Daten wie beispielsweise Dokumente und Bilder im Dateisystem zu speichern. Anwendungen können die umfassenden Streaming-APIs und die Leistung des Dateisystems nutzen und dabei die Transaktionskonsistenz zwischen den nicht strukturierten Daten und den entsprechenden strukturierten Daten erhalten.  
  
 FILESTREAM integriert die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in ein NTFS-Dateisystem gespeichert `varbinary(max)` binary large Object (BLOB)-Daten im Dateisystem. [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen können FILESTREAM-Daten eingefügt, aktualisiert, abgefragt, gesucht und gesichert werden. Die Win32-Dateisystemschnittstellen stellen Streamingzugriff auf die Daten bereit.  
  
 FILESTREAM verwendet den NT-Systemcache zum Zwischenspeichern von Dateidaten. Dies wirkt allen negativen Auswirkungen entgegen, die FILESTREAM-Daten auf die [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Leistung haben könnten. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Pufferpool wird nicht verwendet, deshalb steht dieser Arbeitsspeicher für die Abfragebearbeitung zur Verfügung.  
  
 FILESTREAM wird bei der Installation oder beim Upgrade von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nicht automatisch aktiviert. Sie müssen FILESTREAM mit dem SQL Server-Konfigurations-Manager und [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aktivieren. Um FILESTREAM zu verwenden, müssen Sie eine Datenbank mit einer bestimmten Dateigruppe erstellen bzw. ändern, sodass sie diese Dateigruppe enthält. Anschließend erstellen oder Ändern einer Tabelle, sodass sie enthält eine `varbinary(max)` Spalte mit dem FILESTREAM-Attribut. Anschließend können Sie [!INCLUDE[tsql](../../includes/tsql-md.md)] und Win32 zur Verwaltung der FILESTREAM-Daten verwenden.  
  
 Weitere Informationen zum Installieren und Verwenden von FILESTREAM finden Sie in der Liste [Verwandte Aufgaben](#reltasks).  
  
##  <a name="whentouse"></a> Verwendungsbereiche von FILESTREAM  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],-BLOBs kann standard sein `varbinary(max)` Daten, die Daten in Tabellen oder FILESTREAM speichert `varbinary(max)` Objekte, die die Daten im Dateisystem zu speichern. Größe und Verwendung der Daten bestimmen, ob Sie sie in einer Datenbank oder im Dateisystem speichern sollten. Wenn die folgenden Bedingungen zutreffen, sollten Sie die Verwendung von FILESTREAM in Betracht ziehen:  
  
-   Die Objekte, die gespeichert werden, sind im Durchschnitt größer als 1 MB.  
  
-   Schneller Lesezugriff ist wichtig.  
  
-   Sie entwickeln Anwendungen, die eine mittlere Ebene für die Anwendungslogik nutzen.  
  
 Bei kleineren Objekte ist die Streamingleistung oft besser, wenn `varbinary(max)`-BLOBs in der Datenbank gespeichert werden.  
  
  
##  <a name="storage"></a> FILESTREAM-Speicherung  
 FILESTREAM-Speicherung wird als implementiert eine `varbinary(max)` Spalte, in dem die Daten als BLOBs im Dateisystem gespeichert ist. Die Größe der BLOBs wird nur durch die Volumegröße des Dateisystems beschränkt. Der Standard `varbinary(max)` Beschränkung der Dateigröße auf 2 GB gilt nicht für BLOBs, die im Dateisystem gespeichert werden.  
  
 Um anzugeben, dass die Daten in einer Spalte im Dateisystem gespeichert werden soll, geben Sie das FILESTREAM-Attribut auf eine `varbinary(max)` Spalte. Dies bewirkt, dass [!INCLUDE[ssDE](../../includes/ssde-md.md)] alle Daten der betreffenden Spalte im Dateisystem, aber nicht in der Datenbankdatei speichert.  
  
 FILESTREAM-Daten müssen in FILESTREAM-Dateigruppen gespeichert werden. Eine FILESTREAM-Dateigruppe ist eine besondere Dateigruppe, die Dateisystemverzeichnisse statt der Dateien selbst enthält. Diese Dateisystemverzeichnisse werden als *Datencontainer*bezeichnet. Datencontainer bilden die Schnittstelle zwischen der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Speicherung und der Dateisystemspeicherung.  
  
 Bei Verwendung von FILESTREAM sind die folgenden Punkte zu beachten:  
  
-   Wenn eine Tabelle eine FILESTREAM-Spalte enthält, muss jede Zeile über eine eindeutige Zeilen-ID, die nicht NULL ist, verfügen.  
  
-   Einer FILESTREAM-Dateigruppe können mehrere Datencontainer hinzugefügt werden.  
  
-   FILESTREAM-Datencontainer können nicht geschachtelt werden.  
  
-   Wenn Sie Failoverclustering verwenden, müssen sich die FILESTREAM-Dateigruppen auf freigegebenen Datenträgerressourcen befinden.  
  
-   FILESTREAM-Dateigruppen können auf komprimierten Volumes erstellt werden.  
  
### <a name="integrated-management"></a>Integrierte Verwaltung  
 Weil FILESTREAM als `varbinary(max)`-Spalte implementiert und direkt in [!INCLUDE[ssDE](../../includes/ssde-md.md)] integriert ist, können die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verwaltungstools und -Funktionen für FILESTREAM-Daten eingesetzt werden, ohne in irgendeiner Weise geändert werden zu müssen. Beispielsweise können Sie alle Sicherungs- und Wiederherstellungsmodelle mit FILESTREAM-Daten verwenden, und die FILESTREAM-Daten werden zusammen mit den strukturierten Daten in der Datenbank gesichert. Wenn Sie die FILESTREAM-Daten nicht zusammen mit relationalen Daten sichern möchten, können Sie eine Teilsicherung durchführen, um die FILESTREAM-Dateigruppen auszuschließen.  

  
### <a name="integrated-security"></a>Integrierte Sicherheit  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]werden FILESTREAM-Daten wie alle anderen Daten geschützt: indem Berechtigungen auf der Tabellen- oder Spaltenebene gewährt werden. Wenn ein Benutzer über Berechtigungen zum Öffnen der FILESTREAM-Spalte einer Tabelle verfügt, dann er die zugehörigen Dateien öffnen.  
  
> [!NOTE]  
>  FILESTREAM-Daten können nicht verschlüsselt werden.  
  
 Nur das Konto, unter dem das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienstkonto ausgeführt wird, erhält NTFS-Berechtigungen für den FILESTREAM-Container. Wir empfehlen, dass keinem anderen Konto Berechtigungen für den Datencontainer gewährt werden.  
  
> [!NOTE]  
>  SQL-Anmeldungen funktionieren nicht mit FILESTREAM-Containern. Nur NTFS-Authentifizierung funktioniert mit FILESTREAM-Containern.  
  
##  <a name="dual"></a> Zugreifen auf BLOB-Daten mit Transact-SQL und Dateisystem-Streamingzugriff  
 Nachdem Daten in einer FILESTREAM-Spalte gespeichert wurden, können Sie über [!INCLUDE[tsql](../../includes/tsql-md.md)] -Transaktionen oder mithilfe von Win32-APIs auf die Dateien zugreifen.  
  
### <a name="transact-sql-access"></a>Zugriff über Transact-SQL  
 Mit [!INCLUDE[tsql](../../includes/tsql-md.md)]können Sie FILESTREAM-Daten einfügen, aktualisieren und löschen:  
  
-   Mit einem Einfügevorgang können Sie ein FILESTREAM-Feld vorab mit einem Nullwert, einem leeren Wert oder relativ kurzen Inlinedaten füllen. Große Datenmengen lassen sich jedoch effizienter in eine Datei streamen, wenn Win32-Schnittstellen verwendet werden.  
  
-   Wenn Sie ein FILESTREAM-Feld aktualisieren, ändern Sie die zugrunde liegenden BLOB-Daten im Dateisystem. Wenn ein FILESTREAM-Feld auf NULL festgelegt wird, werden die dem Feld zugeordneten BLOB-Daten gelöscht. Ein segmentiertes Update in [!INCLUDE[tsql](../../includes/tsql-md.md)] , das als UPDATE **.** Write() implementiert wird, kann nicht zur Ausführung von partiellen Updates der Daten eingesetzt werden.  
  
-   Wenn Sie eine Zeile löschen oder eine Tabelle, die FILESTREAM-Daten enthält, löschen oder abschneiden, löschen Sie auch die zugrunde liegenden BLOB-Daten im Dateisystem.  
  
### <a name="file-system-streaming-access"></a>Dateisystem-Streamingzugriff  
 Die Win32-Streamingunterstützung funktioniert im Kontext von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Transaktionen. Im Rahmen einer Transaktion können Sie mithilfe von FILESTREAM-Funktionen, einen logischen UNC-Pfad für eine Datei ermitteln. Sie verwenden dann die OpenSqlFilestream-API, um ein Dateihandle abzurufen. Dieses Handle kann dann von Win32-Dateistreamingschnittstellen, wie ReadFile() und WriteFile(), verwendet werden, um über das Dateisystem auf die Datei zuzugreifen und diese zu aktualisieren.  
  
 Weil Dateivorgänge transaktionsgebunden sind, können Sie FILESTREAM-Dateien nicht über das Dateisystem löschen oder umbenennen.  
  
 **Anweisungsmodell**  
  
 Der FILESTREAM Dateisystemzugriff modelliert eine [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung, indem die Datei geöffnet und geschlossen wird. Die Anweisung beginnt, wenn ein Dateihandle geöffnet wird, und endet, wenn das Handle geschlossen wird. Wenn beispielsweise ein Handle zum Schreiben geschlossen wird, dann wird ein möglicherweise für die Tabelle registrierter AFTER-Trigger so ausgelöst, als wäre eine UPDATE-Anweisung abgeschlossen worden.  
  
 **Storage Namespace**  
  
 Bei FILESTREAM wird der BLOB-physische Dateisystemnamespace für BLOB von [!INCLUDE[ssDE](../../includes/ssde-md.md)] gesteuert. Eine neue intrinsische Funktion namens [PathName](/sql/relational-databases/system-functions/pathname-transact-sql)liefert den logischen UNC-Pfads des BLOBs, das mit jeder einzelnen FILESTREAM-Zelle der Tabelle verknüpft ist. Die Anwendung verwendet diesen logischen Pfad, um das Win32-Handle zu erhalten und die BLOB-Daten mithilfe der gewöhnlichen Win32-Dateisystemschnittstellen zu bearbeiten. Die Funktion gibt NULL zurück, wenn der Wert der FILESTREAM-Spalte gleich NULL ist.  
  
 **Transaktiver Dateisystemzugriff**  
  
 Die neue systeminterne Funktion [GET_FILESTREAM_TRANSACTION_CONTEXT ()](/sql/t-sql/functions/get-filestream-transaction-context-transact-sql)gibt das Token zurück, das die aktuelle Transaktion darstellt, mit der die Sitzung verknüpft ist. Die Transaktion muss bereits gestartet, aber noch nicht abgebrochen oder eingetragen worden sein. Durch den Bezug eines Tokens bindet die Anwendung die FILESTREAM-Dateisystem-Streamingvorgänge an eine gestartete Transaktion. Die Funktion gibt NULL zurück, wenn keine explizit gestartete Transaktion vorliegt.  
  
 Alle Dateihandles müssen geschlossen werden, bevor die Transaktion abgebrochen oder eingetragen wird. Wenn ein Handle nach Abschluss einer Transaktion geöffnet bleibt, verursachen weitere Lesevorgänge unter Verwendung des Handles einen Fehler. Weitere Schreibvorgänge unter Verwendung des Handles werden zwar ausgeführt, aber die Daten werden nicht auf den Datenträger geschrieben. Wenn die Datenbank oder die [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz geschlossen wird, werden alle geöffneten Handles ungültig.  
  
 **Dauerhaftigkeit von Transaktionen**  
  
 Bei Verwendung von FILESTREAM wird beim Eintragen einer Transaktion von [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Dauerhaftigkeit von Transaktionen für FILESTREAM-BLOB-Daten sichergestellt, die über einen Streamingzugriff auf das Dateisystem geändert werden.  
  
 **Isolationssemantik**  
  
 Die Isolationssemantik wird durch die [!INCLUDE[ssDE](../../includes/ssde-md.md)] Transaktionsisolationsstufen bestimmt. Für den [!INCLUDE[tsql](../../includes/tsql-md.md)] - und den Dateisystemzugriff wird nur die Read Committed-Isolationsstufe unterstützt. Wiederholbare Lesevorgänge und auch serialisierbare sowie Momentaufnahmeisolationen werden unterstützt. Das Lesen von geänderten Daten, für die kein Commit ausgeführt wurde, wird nicht unterstützt.  
  
 Bei Dateisystemzugriffvorgängen zum Öffnen von Dateien wird auf keine Sperren gewartet. Stattdessen schlagen die Öffnungsvorgänge sofort fehl, wenn wegen der Transaktionsisolation nicht auf die Daten zugegriffen werden kann. Die Streaming-API-Aufrufe schlagen mit dem Ergebnis ERROR_SHARING_VIOLATION fehl, wenn der Öffnungsvorgang wegen einer Isolationsverletzung nicht fortgesetzt werden kann.  
  
 Damit Teilaktualisierungen durchgeführt werden können, kann die Anwendung einen Dateisystembefehl (FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT) ausgeben, um den alten Inhalt in die Datei zu laden, auf die das geöffnete Handle verweist. Daraufhin kopiert der Server den alten Inhalt. Um das Leistungsverhalten der Anwendung zu verbessern und zu vermeiden, dass bei der Arbeit mit sehr großen Dateien Wartezeitüberschreitungen auftreten, wird die Verwendung asynchroner E/A empfohlen.  
  
 Wenn der FSCTL-Befehl ausgegeben wird, nachdem in die durch das Handle bezeichnete Datei geschrieben wurde, dann werden die Daten des letzten Schreibvorgangs persistent gespeichert, alle zuvor geschriebenen Daten gehen verloren.  
  
 **Dateisystem-APIs und unterstützte Isolationsstufen**  
  
 Wenn eine Dateisystem-API aufgrund einer Isolationsverletzung eine Datei nicht öffnen kann, wird eine ERROR_SHARING_VIOLATION-Ausnahme zurückgegeben. Diese Isolationsverletzung tritt auf, wenn zwei Transaktionen versuchen, auf dieselbe Datei zuzugreifen. Das Ergebnis des Zugriffsvorgangs ist von dem Modus abhängig, in dem die Datei geöffnet wurde, und von der Version [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , in der die Transaktion ausgeführt wird. In der folgenden sind die möglichen Ergebnisse für zwei Transaktionen aufgeführt, die auf dieselbe Datei zugreifen.  
  
|Transaktion 1|Transaktion 2|Ergebnis unter SQL Server 2008|Ergebnis unter SQL Server 2008 R2 und höheren Versionen|  
|-------------------|-------------------|--------------------------------|------------------------------------------------------|  
|Geöffnet zum Lesen.|Geöffnet zum Lesen.|Beide erfolgreich.|Beide erfolgreich.|  
|Geöffnet zum Lesen.|Geöffnet zum Schreiben.|Beide erfolgreich. Schreibvorgänge unter Transaktion 2 haben keine Auswirkungen auf in Transaktion 1 ausgeführte Lesevorgänge.|Beide erfolgreich. Schreibvorgänge unter Transaktion 2 haben keine Auswirkungen auf in Transaktion 1 ausgeführte Lesevorgänge.|  
|Geöffnet zum Schreiben.|Geöffnet zum Lesen.|Das Öffnen für Transaktion 2 schlägt mit einer ERROR_SHARING_VIOLATION-Ausnahme fehl.|Beide erfolgreich.|  
|Geöffnet zum Schreiben.|Geöffnet zum Schreiben.|Das Öffnen für Transaktion 2 schlägt mit einer ERROR_SHARING_VIOLATION-Ausnahme fehl.|Das Öffnen für Transaktion 2 schlägt mit einer ERROR_SHARING_VIOLATION-Ausnahme fehl.|  
|Geöffnet zum Lesen.|Geöffnet für SELECT.|Beide erfolgreich.|Beide erfolgreich.|  
|Geöffnet zum Lesen.|Geöffnet für UPDATE oder DELETE.|Beide erfolgreich. Schreibvorgänge unter Transaktion 2 haben keine Auswirkungen auf in Transaktion 1 ausgeführte Lesevorgänge.|Beide erfolgreich. Schreibvorgänge unter Transaktion 2 haben keine Auswirkungen auf in Transaktion 1 ausgeführte Lesevorgänge.|  
|Geöffnet zum Schreiben.|Geöffnet für SELECT.|Transaktion 2 ist blockiert, bis Transaktion 1 einen Commit für die Transaktion ausführt, die Transaktion beendet oder bei der Transaktionssperre ein Timeout auftritt.|Beide erfolgreich.|  
|Geöffnet zum Schreiben.|Geöffnet für UPDATE oder DELETE.|Transaktion 2 ist blockiert, bis Transaktion 1 einen Commit für die Transaktion ausführt, die Transaktion beendet oder bei der Transaktionssperre ein Timeout auftritt.|Transaktion 2 ist blockiert, bis Transaktion 1 einen Commit für die Transaktion ausführt, die Transaktion beendet oder bei der Transaktionssperre ein Timeout auftritt.|  
|Geöffnet für SELECT.|Geöffnet zum Lesen.|Beide erfolgreich.|Beide erfolgreich.|  
|Geöffnet für SELECT.|Geöffnet zum Schreiben.|Beide erfolgreich. Schreibvorgänge unter Transaktion 2 haben keine Auswirkungen auf Transaktion 1.|Beide erfolgreich. Schreibvorgänge unter Transaktion 2 haben keine Auswirkungen auf Transaktion 1.|  
|Geöffnet für UPDATE oder DELETE.|Geöffnet zum Lesen.|Der Öffnungsvorgang unter Transaktion 2 schlägt mit einer ERROR_SHARING_VIOLATION-Ausnahme fehl.|Beide erfolgreich.|  
|Geöffnet für UPDATE oder DELETE.|Geöffnet zum Schreiben.|Der Öffnungsvorgang unter Transaktion 2 schlägt mit einer ERROR_SHARING_VIOLATION-Ausnahme fehl.|Der Öffnungsvorgang unter Transaktion 2 schlägt mit einer ERROR_SHARING_VIOLATION-Ausnahme fehl.|  
|Geöffnet für SELECT mit wiederholbarem Lesen.|Geöffnet zum Lesen.|Beide erfolgreich.|Beide erfolgreich.|  
|Geöffnet für SELECT mit wiederholbarem Lesen.|Geöffnet zum Schreiben.|Der Öffnungsvorgang unter Transaktion 2 schlägt mit einer ERROR_SHARING_VIOLATION-Ausnahme fehl.|Der Öffnungsvorgang unter Transaktion 2 schlägt mit einer ERROR_SHARING_VIOLATION-Ausnahme fehl.|  
  
 **Direktes Schreiben von Remoteclients**  
  
 Der Remotedateisystemzugriff auf FILESTREAM-Daten wird über das SMB (Server Message-Block)-Protokoll ermöglicht. Wenn der Client remote ist, werden Schreibvorgänge nicht auf der Clientseite zwischengespeichert. Die Schreibvorgänge werden immer an den Server gesendet. Die Daten können auf der Serverseite zwischengespeichert werden. Es wird empfohlen, dass Anwendungen, die auf Remoteclients ausgeführt werden, kleine Schreibvorgänge konsolidieren, sodass weniger Schreibvorgänge mit größeren Datenmengen durchgeführt werden.  
  
 Die Erstellung von Speicherabbildern (E/A mit Speicherabbildern) mit einem FILESTREAM-Handle wird nicht unterstützt. Wenn Speicherabbilder für FILESTREAM-Daten verwendet werden, kann [!INCLUDE[ssDE](../../includes/ssde-md.md)] weder die Konsistenz und Dauerhaftigkeit der Daten noch die Datenbankintegrität garantieren.  
  
##  <a name="reltasks"></a> Verwandte Aufgaben  
 [Aktivieren und Konfigurieren von FILESTREAM](enable-and-configure-filestream.md)  
  [Erstellen einer FILESTREAM-aktivierten Datenbank](create-a-filestream-enabled-database.md)  
  [Erstellen einer Tabelle zum Speichern von FILESTREAM-Daten](create-a-table-for-storing-filestream-data.md)  
  [ZUgreifen auf FILESTREAM-Daten mit Transact-SQL](access-filestream-data-with-transact-sql.md)  
  [Erstellen von Clientanwendungen für FILESTREAM-Daten](create-client-applications-for-filestream-data.md)  
  [ZUgreifen auf FILESTREAM-Daten mit OpenSqlFilestream](access-filestream-data-with-opensqlfilestream.md)  
  [Vornehmen von Teilupdates an FILESTREAM-Daten](make-partial-updates-to-filestream-data.md)  
  [Vermeiden von Konflikten mit Datenbankvorgängen in FILESTREAM-Anwendungen](avoid-conflicts-with-database-operations-in-filestream-applications.md)  
  [Verschieben einer FILESTREAM-aktivierten Datenbank](move-a-filestream-enabled-database.md)  
  [Einrichten von FILESTREAM auf einem Failovercluster](set-up-filestream-on-a-failover-cluster.md)  
  [Konfigurieren einer Firewall für FILESTREAM-Zugriff](configure-a-firewall-for-filestream-access.md)  
  
##  <a name="relcontent"></a> Verwandte Inhalte  
 [FILESTREAM-Kompatibilität mit anderen SQL Server-Funktionen](filestream-compatibility-with-other-sql-server-features.md)  
  
