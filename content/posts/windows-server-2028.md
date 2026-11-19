---
title: "Windows Server 2028 in anteprima: le novità della build 29706"
date: 2026-11-19
description: "Server Core, Hyper-V, ReFS Boot, NVMe over Fabrics, Entra ID, Intune e rimozioni previste nella prossima release LTSC."
tags: ["Windows Server 2028", "Hyper-V", "Intune", "Azure Arc", "Storage", "Sicurezza"]
draft: false
---

Microsoft ha annunciato a Ignite 2026 la **public preview di Windows Server 2028**, prossima versione del Long-Term Servicing Channel (LTSC). L’annuncio del 17 novembre coincide con la build **29706**, la prima del programma Insider con il nome Windows Server 2028. La documentazione pubblicata finora distingue le funzioni presenti nelle build Insider, le anteprime riservate ad alcuni clienti e le funzionalità annunciate per la release finale. [Ignite 2026 Book of News](https://news.microsoft.com/events/ignite/2026/book-of-news/) · [Note della build 29706](https://techcommunity.microsoft.com/discussions/windowsserverinsiders/announcing-windows-server-vnext-preview-build-29706/4574165)

## Edizioni, immagini e compatibilità tra build

La build 29706 offre **Standard** e **Datacenter** con le opzioni Server Core e Desktop Experience. Datacenter Azure Edition è disponibile per la valutazione in macchina virtuale. Il programma distribuisce immagini ISO e VHDX. La scadenza della build è fissata al **15 ottobre 2027**. Nelle note consultate Microsoft non indica una data di disponibilità generale. Windows Server 2025 figura ancora come release LTSC corrente. [Note della build 29706](https://techcommunity.microsoft.com/discussions/windowsserverinsiders/announcing-windows-server-vnext-preview-build-29706/4574165) · [Informazioni sulle release di Windows Server](https://learn.microsoft.com/en-us/windows-server/get-started/windows-server-release-info)

Microsoft ha stabilito la build **29531** come nuova base per la sequenza Insider. Gli aggiornamenti dalle preview precedenti a questa build sono fuori dal perimetro di supporto, anche dove il programma di installazione consente tecnicamente di avviarli. La distribuzione delle build successive tramite il canale Insider è ripresa con la 29550. Questa compatibilità riguarda il passaggio tra build **vNext**. Le matrici di aggiornamento dalla release LTSC corrente e di compatibilità con i prodotti server seguono la documentazione specifica dei rispettivi prodotti. [Note della build 29706](https://techcommunity.microsoft.com/discussions/windowsserverinsiders/announcing-windows-server-vnext-preview-build-29706/4574165)

## Server Core e sicurezza di base

Le nuove installazioni **Server Core** adottano impostazioni di sicurezza più restrittive fin dal primo avvio. Il perimetro documentato comprende firewall, autenticazione, accessi privilegiati, gestione remota, crittografia, integrità del codice e audit. Microsoft limita i nuovi default alle installazioni pulite di Server Core nella preview. L’installazione e la baseline sono due livelli distinti della configurazione: il primo determina lo stato iniziale del sistema, mentre GPO e strumenti di gestione possono applicare impostazioni successive. [Hardened Server Core](https://techcommunity.microsoft.com/blog/WindowsServerNewsandBestPractices/announcing-hardened-server-core-for-windows-server-insiders/4574239) · [Funzionalità della preview](https://learn.microsoft.com/en-us/windows-server/get-started/whats-new-windows-server-2028)

Per **SMB**, firma e cifratura agiscono su aspetti diversi. La firma tutela l’integrità dei messaggi, mentre la cifratura protegge anche la riservatezza del traffico. La build 29706 introduce inoltre **SMB Policy Controller**: un amministratore seleziona un profilo per una condivisione esistente, in base al carico e alle esigenze di sicurezza o prestazioni. Lo strumento distingue le impostazioni della share da quelle di server e riconcilia le modifiche che si discostano dal profilo. [SMB Policy Controller nella preview](https://learn.microsoft.com/en-us/windows-server/get-started/whats-new-windows-server-2028#smb-policy-controller)

### Crittografia post-quantum e TLS

Microsoft ha annunciato il supporto alla crittografia post-quantum e alla gestione automatizzata dei certificati. Nel caso di TLS, uno scambio di chiavi ibrido combina un meccanismo tradizionale e uno post-quantum nella negoziazione del segreto di sessione. La nota della build 29706 riporta una race condition che può provocare l’arresto di **LSASS** quando un server TLS negozia determinati gruppi ibridi ML-KEM. Microsoft descrive un workaround temporaneo nella nota della build. L’avviso riguarda lo scambio di chiavi ibrido lato server e va letto nel contesto della specifica build Insider. [Book of News](https://news.microsoft.com/events/ignite/2026/book-of-news/) · [Problemi noti della build 29706](https://techcommunity.microsoft.com/discussions/windowsserverinsiders/announcing-windows-server-vnext-preview-build-29706/4574165)

## Hyper-V: Trusted Launch e Windows Admin Center

**Trusted Launch** per VM Hyper-V **Generation 2** combina Secure Boot, vTPM e protezione dello stato guest. Secure Boot verifica i componenti della catena di avvio. Il vTPM dà al guest un TPM virtuale, utilizzabile, per esempio, per vincolare chiavi al suo stato. La protezione dello stato guest riguarda i dati della VM che devono essere conservati dall’host. Questi meccanismi rendono rilevante anche il modo in cui lo stato protetto viene trasferito o ripristinato su altri host. [Annuncio Trusted Launch per Hyper-V](https://techcommunity.microsoft.com/blog/WindowsServerNewsandBestPractices/announcing-trusted-launch-for-virtual-machines-for-windows-server-insiders/4537082)

Al 19 novembre, la scheda Microsoft Learn della **public preview** esclude lo spostamento di una Trusted Launch VM su un altro host, Failover Clustering, Hyper-V Replica e la verifica dell’integrità del boot. Microsoft ha annunciato separatamente una **private preview** dell’integrazione con Windows Admin Center vMode che mostra lo stato di integrità del boot. Il perimetro di ciascun programma determina quali scenari risultano disponibili. [Limiti della public preview](https://learn.microsoft.com/en-us/windows-server/get-started/whats-new-windows-server-2028#trusted-launch-for-generation-2-virtual-machines) · [Private preview Trusted Launch in vMode](https://techcommunity.microsoft.com/blog/windows-admin-center-blog/tvm-in-windows-admin-center-vmode-is-in-private-preview/4574161)

Il prodotto **Windows Admin Center 2611 in Virtualization Mode**, invece, è già in disponibilità generale. Microsoft dichiara fino a **1.000 host Hyper-V e 25.000 VM per istanza**, oltre all’onboarding in Azure Arc, al backup e ripristino della configurazione di vMode e alla gestione dei certificati con Active Directory Certificate Services. Queste sono capacità del piano di gestione. L’uso di una funzionalità specifica di Hyper-V dipende anche dalla build e dal supporto degli host gestiti. [Annuncio Windows Admin Center 2611](https://techcommunity.microsoft.com/blog/windows-admin-center-blog/virtualization-mode-in-windows-admin-center-is-now-generally-available/4573651)

## Storage: NVMe locale, NVMe-oF e ReFS Boot

**NVMe nativo** riguarda il percorso di accesso ai dispositivi NVMe collegati localmente. Microsoft annuncia lo stack NVMe nativo abilitato per impostazione predefinita su Windows Server 2028. **NVMe over Fabrics**, invece, espone namespace remoti come dischi Windows tramite un initiator integrato. Il trasporto TCP usa la normale connettività IP Ethernet. Il trasporto RDMA richiede supporto e configurazione compatibili lungo il percorso di rete. Nella preview documentata l’initiator si gestisce da riga di comando, il multipathing è fuori dal perimetro e il recupero dopo alcuni guasti di rete è limitato. [Annuncio Windows Server 2028](https://techcommunity.microsoft.com/blog/windowsservernewsandbestpractices/windows-server-2028-a-trusted-foundation-for-an-evolving-enterprise/4574112) · [Documentazione dell’initiator NVMe-oF](https://techcommunity.microsoft.com/blog/WindowsServerNewsandBestPractices/introducing-the-windows-nvme-of-initiator-preview-in-windows-server-insiders-bui/4501344)

**ReFS Boot** consente di formattare in ReFS il volume su cui risiede Windows. Il layout documentato richiede firmware UEFI e disco GPT. Il volume di sistema operativo in ReFS convive con una partizione di ripristino **WinRE in NTFS**. Poiché ReFS non supporta la riduzione del volume, una distribuzione con file di risposta deve riservare esplicitamente lo spazio per WinRE. La documentazione della preview indica almeno **2 GB** per la partizione di ripristino. Le VM Generation 1 sono fuori dal perimetro. [Deploy con ReFS Boot e file di risposta](https://learn.microsoft.com/en-us/windows-server/storage/refs/refs-boot-windows-server-unattend) · [ReFS Boot nella preview](https://learn.microsoft.com/en-us/windows-server/get-started/whats-new-windows-server-2028#refs-boot)

**Quick Machine Recovery** usa WinRE con accesso alla rete dopo ripetuti errori di avvio per cercare su Windows Update una correzione pubblicata da Microsoft. Il recupero dipende dall’esistenza di una correzione applicabile. Microsoft documenta la funzionalità anche per **Windows Server 2025**, a partire dall’aggiornamento di sicurezza di ottobre 2026. [Quick Machine Recovery](https://learn.microsoft.com/en-us/windows-server/get-started/whats-new-windows-server-2028#quick-machine-recovery)

## Entra ID, Intune, Autopatch e Azure Arc

La 29706 introduce scenari di **Microsoft Entra join** e accesso al server con account Entra. Microsoft descrive l’enrollment automatico in Intune per server Entra joined idonei e l’enrollment mediante Group Policy per gli scenari hybrid joined supportati. La funzionalità è **opt-in** e riservata alle build Insider idonee in ambienti non produttivi. [Identità e gestione in Windows Server 2028 Preview](https://learn.microsoft.com/en-us/windows-server/get-started/whats-new-windows-server-2028) · [Novità di Microsoft Intune](https://learn.microsoft.com/en-us/intune/whats-new)

Intune documenta inventario, distribuzione di applicazioni Win32, impostazioni di configurazione tramite CSP, compliance e un sottoinsieme delle capacità di aggiornamento. Lo stato di compliance può fornire un segnale a Conditional Access. Le impostazioni di Windows Update for Business e Windows Autopatch sono soggette al perimetro della preview. Azure Arc può operare sullo stesso server ed è facoltativo per l’enrollment Intune. Il ruolo di Arc comprende governance e monitoraggio dell’infrastruttura. Le assegnazioni Intune continuano a usare gruppi, ruoli e filtri supportati. [Gestione dei server in Intune](https://learn.microsoft.com/en-us/intune/whats-new)

La 29706 include anche **PowerShell 7** accanto a Windows PowerShell 5.1. Le due shell usano eseguibili distinti, rispettivamente `pwsh.exe` e `powershell.exe`. La presenza della nuova shell lascia disponibile il runtime su cui si basano moduli e script esistenti. [PowerShell 7 nella build 29706](https://learn.microsoft.com/en-us/windows-server/get-started/whats-new-windows-server-2028#powershell-7)

## WSUS e componenti legacy

Microsoft Learn elenca le seguenti rimozioni per Windows Server 2028. La pagina specifica che la presenza effettiva dei componenti nelle build Insider può differire dal piano e che l’elenco può cambiare prima della disponibilità generale. [Funzionalità rimosse o non più sviluppate](https://learn.microsoft.com/en-us/windows-server/get-started/removed-deprecated-features-windows-server?tabs=ws28-preview)

| Componente | Stato documentato |
| --- | --- |
| **WSUS** | Rimozione del ruolo server in Windows Server 2028. Il ruolo rimane disponibile nelle release precedenti, incluso Windows Server 2025, secondo il relativo ciclo di vita. |
| **WINS** | Rimozione del ruolo server per la risoluzione dei nomi NetBIOS. |
| **SMBv1** | Rimozione del protocollo dall’immagine di Windows Server 2028. |
| **DirectAccess, PPTP e L2TP** | Rimozione di DirectAccess e dell’accesso remoto via PPTP o L2TP. |
| **VBScript, WMIC e at.exe** | Rimozione del runtime VBScript e dei client legacy WMIC e AT. WMI rimane disponibile. |
| **.NET Framework 3.5** | Passaggio a un modello di distribuzione standalone per i prodotti interessati. |

La rimozione di WSUS riguarda il ruolo di distribuzione e approvazione degli aggiornamenti su Windows Server 2028. La preview Intune descrive un insieme di capacità MDM e di aggiornamento. L’annuncio di queste capacità lascia aperta la valutazione dei flussi basati su approvazioni locali, server downstream e reti senza accesso diretto a Windows Update. [Rimozioni documentate](https://learn.microsoft.com/en-us/windows-server/get-started/removed-deprecated-features-windows-server?tabs=ws28-preview) · [Novità Intune](https://learn.microsoft.com/en-us/intune/whats-new)

## Inferenza locale e disponibilità dell’hardware

A Ignite Microsoft ha presentato la possibilità di eseguire inferenza vicino ai dati aziendali, citando Windows ML, Foundry Local, vLLM e llama.cpp. L’annuncio comprende Microsoft Execution Containers per l’isolamento e un’integrazione con Agent 365 per la governance. Microsoft colloca le funzionalità di **hybrid intelligence** in un programma di accesso anticipato limitato. La disponibilità dipende anche dall’hardware e dalla piattaforma di esecuzione. [Ignite 2026 Book of News](https://news.microsoft.com/events/ignite/2026/book-of-news/)

Per l’acceleratore **AMD MI350P**, Microsoft indica una preview nella prima metà del 2027 su Windows Server 2025 e successivi. Il supporto per **NVIDIA DGX Station for Windows con GB300** è indicato per la disponibilità generale di Windows Server 2028. Sono indicazioni per configurazioni hardware specifiche. Le immagini Insider seguono un proprio ciclo di rilascio. [Windows Experience Blog](https://blogs.windows.com/windowsexperience/2026/11/17/microsoft-ignite-2026-building-windows-for-the-next-era-of-work/)

*Stato delle informazioni al 19 novembre 2026. Per il perimetro effettivo della preview fanno fede le note della singola build e le schede di supporto delle funzionalità.*
